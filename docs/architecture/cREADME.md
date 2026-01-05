# Architecture

## Module Boundaries
- **code_generation/**: `CodeGenerator`, `CodeTemplateFactory`, and concrete templates.
- **templates/**: `TemplateManager` singleton and persistence adapters.
- **prompting/**: `PromptEngine` plus prompt strategies.
- **validation/**: `CodeValidator`, `ValidationStrategy`, and observers.
- **security/**: authentication, RBAC, encryption, and input validation.

## Interfaces
All cross-module interactions rely on interfaces (protocols or abstract base classes) to reduce coupling and enable testing.
