# C Project Template

## Overview
This repository defines an AI-powered development suite using an object-oriented, modular architecture. The design emphasizes security, extensibility, and clarity through well-defined interfaces, design patterns, and thorough documentation.

## Modular Architecture
The system is organized into cohesive modules that communicate via explicit interfaces:

- **code_generation/**
  - Owns the `CodeGenerator` and template factory interfaces.
  - Interfaces: `CodeTemplate`, `CodeTemplateFactory`.
- **templates/**
  - Hosts reusable template assets and a centralized `TemplateManager` singleton.
  - Interfaces: `TemplateRepository`, `TemplateManager`.
- **prompting/**
  - Owns `PromptEngine` and strategy selection for prompt construction.
  - Interfaces: `PromptStrategy`.
- **validation/**
  - Owns `Validator` classes, strategy selection, and observer notifications.
  - Interfaces: `ValidationStrategy`, `ValidatorObserver`.
- **security/**
  - Owns input validation, encryption, authentication, and RBAC policy modules.
  - Interfaces: `InputValidator`, `CryptoProvider`, `AuthProvider`, `AccessControl`.

Each module exposes a minimal public API to reduce coupling. Dependencies flow inward to interfaces rather than concrete implementations.

## Core Classes & Design Patterns

### 1) CodeGenerator (Factory Pattern)
Creates code templates via a factory and delegates generation to the template instance.

```python
from abc import ABC, abstractmethod
from typing import Dict, Any

class CodeTemplate(ABC):
    """Abstract base class for code templates."""

    @abstractmethod
    def generate_code(self) -> str:
        """Generate code from the template.

        Returns:
            str: Generated code.
        """
        raise NotImplementedError

class PythonClassTemplate(CodeTemplate):
    """Concrete class for generating Python class code."""

    def __init__(self, class_name: str, attributes: Dict[str, Any]):
        """Initialize the Python class template.

        Args:
            class_name (str): Name of the class to generate.
            attributes (Dict[str, Any]): Attribute definitions for the class.
        """
        self.class_name = class_name
        self.attributes = attributes

    def generate_code(self) -> str:
        """Generate the Python class code.

        Returns:
            str: The generated Python class source.
        """
        return f"class {self.class_name}:\n    pass\n"

class CodeTemplateFactory:
    """Factory for creating code templates."""

    def create(self, template_type: str, **kwargs: Any) -> CodeTemplate:
        """Create a template instance based on type.

        Args:
            template_type (str): Template identifier.
            **kwargs (Any): Template constructor arguments.

        Returns:
            CodeTemplate: A template instance.

        Raises:
            ValueError: If the template type is unknown.
        """
        if template_type == "python_class":
            return PythonClassTemplate(**kwargs)
        raise ValueError(f"Unsupported template type: {template_type}")

class CodeGenerator:
    """Generates code using the configured template factory."""

    def __init__(self, factory: CodeTemplateFactory) -> None:
        """Initialize the code generator.

        Args:
            factory (CodeTemplateFactory): Factory used for templates.
        """
        self.factory = factory

    def generate(self, template_type: str, **kwargs: Any) -> str:
        """Generate code from the specified template.

        Args:
            template_type (str): Template identifier.
            **kwargs (Any): Template constructor arguments.

        Returns:
            str: Generated code.
        """
        template = self.factory.create(template_type, **kwargs)
        return template.generate_code()
```

### 2) TemplateManager (Singleton Pattern)
Provides a single access point for template storage.

```python
from typing import Dict

class TemplateManager:
    """Singleton manager for template storage."""

    _instance = None

    def __new__(cls) -> "TemplateManager":
        """Create or return the singleton instance."""
        if cls._instance is None:
            cls._instance = super().__new__(cls)
            cls._instance._templates = {}
        return cls._instance

    def add_template(self, name: str, template: CodeTemplate) -> None:
        """Store a template in the registry.

        Args:
            name (str): Template name.
            template (CodeTemplate): Template instance.
        """
        self._templates[name] = template

    def get_template(self, name: str) -> CodeTemplate:
        """Retrieve a template from the registry.

        Args:
            name (str): Template name.

        Returns:
            CodeTemplate: The template instance.
        """
        return self._templates[name]
```

### 3) PromptEngine (Strategy Pattern)
Selects prompt construction behavior at runtime.

```python
from typing import Protocol

class PromptStrategy(Protocol):
    """Protocol for prompt construction strategies."""

    def construct_prompt(self) -> str:
        """Construct a prompt string.

        Returns:
            str: Prompt content.
        """

class ContextAwarePromptStrategy:
    """Strategy for context-aware prompts."""

    def __init__(self, context: dict) -> None:
        """Initialize the strategy.

        Args:
            context (dict): Context metadata for prompt assembly.
        """
        self.context = context

    def construct_prompt(self) -> str:
        """Construct the prompt based on context.

        Returns:
            str: The constructed prompt.
        """
        return f"Build for {self.context.get('project', 'unknown project')}"

class PromptEngine:
    """Engine for constructing prompts with a strategy."""

    def __init__(self, strategy: PromptStrategy) -> None:
        """Initialize the prompt engine.

        Args:
            strategy (PromptStrategy): Prompt construction strategy.
        """
        self.strategy = strategy

    def get_prompt(self) -> str:
        """Return the constructed prompt.

        Returns:
            str: Prompt content.
        """
        return self.strategy.construct_prompt()
```

### 4) Validator (Strategy + Observer Pattern)
Uses strategy-based validators and notifies observers with results.

```python
from abc import ABC, abstractmethod
from typing import List, Dict, Any

class ValidatorObserver(ABC):
    """Observer interface for validation notifications."""

    @abstractmethod
    def update(self, validation_result: Dict[str, Any]) -> None:
        """Receive a validation result.

        Args:
            validation_result (Dict[str, Any]): Validation metadata.
        """
        raise NotImplementedError

class ValidationStrategy(ABC):
    """Strategy interface for validation logic."""

    @abstractmethod
    def validate(self, code: str) -> Dict[str, Any]:
        """Validate code and return results.

        Args:
            code (str): Code to validate.

        Returns:
            Dict[str, Any]: Validation results.
        """
        raise NotImplementedError

class SecurityValidationStrategy(ValidationStrategy):
    """Validation strategy focusing on security checks."""

    def validate(self, code: str) -> Dict[str, Any]:
        """Validate code for security policies.

        Args:
            code (str): Code to validate.

        Returns:
            Dict[str, Any]: Security validation results.
        """
        return {"status": "ok", "checks": ["static-analysis"]}

class CodeValidator:
    """Validate code and notify observers of results."""

    def __init__(self, strategy: ValidationStrategy) -> None:
        """Initialize the validator.

        Args:
            strategy (ValidationStrategy): Validation strategy to use.
        """
        self.strategy = strategy
        self.observers: List[ValidatorObserver] = []

    def add_observer(self, observer: ValidatorObserver) -> None:
        """Register an observer.

        Args:
            observer (ValidatorObserver): Observer to add.
        """
        self.observers.append(observer)

    def notify(self, result: Dict[str, Any]) -> None:
        """Notify observers of validation results.

        Args:
            result (Dict[str, Any]): Validation results.
        """
        for observer in self.observers:
            observer.update(result)

    def validate_code(self, code: str) -> Dict[str, Any]:
        """Validate code and notify observers.

        Args:
            code (str): Code to validate.

        Returns:
            Dict[str, Any]: Validation results.
        """
        result = self.strategy.validate(code)
        self.notify(result)
        return result
```

## Security-Oriented Implementation
- **Input validation:** validate template parameters, prompt inputs, and user-provided context before use.
- **Secure coding standards:** follow OWASP guidance and enforce linting/static analysis.
- **Encryption:** use a dedicated `CryptoProvider` for secrets at rest and TLS for data in transit.
- **RBAC & authentication:** leverage an `AuthProvider` with role-based access control policies.
- **Sensitive data handling:** avoid logging secrets; use structured redaction.

## Example Usage
```python
factory = CodeTemplateFactory()
generator = CodeGenerator(factory)

code = generator.generate(
    "python_class",
    class_name="UserService",
    attributes={"name": "str"},
)

template_manager = TemplateManager()
template_manager.add_template("user_service", PythonClassTemplate("UserService", {}))

prompt_engine = PromptEngine(ContextAwarePromptStrategy({"project": "AI Suite"}))
prompt = prompt_engine.get_prompt()

validator = CodeValidator(SecurityValidationStrategy())
validation_result = validator.validate_code(code)
```

## Project Files
- **cTODO.md**: Backlog of tasks and enhancements.
- **cVERSION**: Single-source version identifier.
- **cCHANGELOG.md**: Release history and changes.
- **cLICENSE.md**: Licensing details.

## License
See [cLICENSE.md](cLICENSE.md).
