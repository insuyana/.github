# Contributing to Suyana / Cómo contribuir a Suyana

[English](#english) | [Español](#español)

---

## English

These guidelines apply to all repositories in the Suyana organization. Contributions are made by organization members only.

### 1. Branches

- Branch from `main`.
- Use a prefix that describes the change:
  - `feat/` for new functionality
  - `fix/` for bug fixes
  - `dev/` for work in progress or experiments
- Keep branch names short and descriptive, e.g. `feat/era5-point-extraction`, `fix/local-mode-buttons`.

### 2. Pull requests

- **Every change to `main` goes through a pull request.** Only the administrator and the repository owner may push directly to `main`.
- Production systems pull from `main`, so anything merged there must be ready to run in production. Review with that in mind.
- Each PR needs **at least one approval**. The code owner may bypass this requirement.
- Fill in the PR template. The mandatory sections (Summary, Scope and impact, Verification, Checklist) must always be completed.
- Keep PRs focused on one purpose. Split unrelated changes into separate PRs.

### 3. Code style

- **Python 3.10 or newer.**
- Follow **PEP 8**: <https://peps.python.org/pep-0008/>
- A formatter or linter that enforces PEP 8 is recommended, e.g. [Ruff](https://docs.astral.sh/ruff/) or [Black](https://black.readthedocs.io/).
- Use clear names, docstrings for public functions, and comments where the reasoning is not obvious from the code.

### 4. Environment and dependencies

- Use **pip** with a virtual environment:
  ```bash
  python -m venv .venv
  source .venv/bin/activate   # Windows: .venv\Scripts\activate
  pip install -r requirements.txt
  ```
- Requirements must be **as specific as possible**: pin exact versions (`package==1.2.3`) so every member and every production system installs the same environment.
- Make sure all packages are compatible with each other. After installing, run:
  ```bash
  pip check
  ```
  and fix any conflicts before opening a PR.
- When you add or upgrade a dependency, update `requirements.txt` in the same PR and mention it in the PR description.

### 5. Warnings

- Code should run **without warnings**.
- Fix the cause whenever possible (deprecated calls, version conflicts, dtype or CRS mismatches).
- Suppress a warning only when it is understood and harmless. Do it as narrowly as possible (a specific warning category, in a specific block) and add a comment explaining why.

### 6. Tests

- Tests are expected for new code. For Python, use [pytest](https://docs.pytest.org/).
- Place tests in a `tests/` folder and make sure the full suite passes before opening a PR:
  ```bash
  pytest
  ```
- When a full test is not practical (e.g. it needs remote data), include a small reproducible snippet or check in the PR that shows the code works.

### 7. Notebooks

- Commit notebooks **without outputs**. Clear them before committing:
  ```bash
  jupyter nbconvert --clear-output --inplace path/to/notebook.ipynb
  ```
  or install [nbstripout](https://github.com/kynan/nbstripout) to do it automatically.
- Logic that is reused or runs in production belongs in Python modules, not in notebooks.

### 8. Credentials and security

- **Never commit credentials**: API keys, access keys, passwords, tokens or `.env` files. This includes code, notebooks, configuration files, commit messages, and PR or issue descriptions.
- Load credentials from environment variables or local configuration files that live outside the repository, and make sure `.env` is listed in `.gitignore`.
- If a credential is ever exposed, notify the administrator immediately so it can be rotated. Deleting it from a file or description is not enough, because it remains in the history.

### 9. Data

- **Client data must never be committed or made public.** This includes client names, plot or farm locations, loan or policy data, and any file received from a client.
- During development, read from and write to Suyana's **development** storage (AWS development buckets). Production storage is only written by production systems.
- Check that any asset you create outside GitHub (cloud buckets, Earth Engine assets, shared links) is not publicly accessible.

### 10. Documentation

- Every repository must have an informative `README.md`: what the project does, how to install it, how to run it, and its inputs and outputs.
- Update the README in the same PR whenever usage, configuration or behavior changes.

### 11. Help

For questions about these guidelines, access or permissions, contact the team manager or the administrator.

---

## Español

Estas pautas aplican a todos los repositorios de la organización Suyana. Solo los miembros de la organización pueden contribuir.

### 1. Ramas

- Crea tu rama a partir de `main`.
- Usa un prefijo que describa el cambio:
  - `feat/` para funcionalidades nuevas
  - `fix/` para corrección de errores
  - `dev/` para trabajo en progreso o experimentos
- Usa nombres cortos y descriptivos, por ejemplo `feat/era5-point-extraction`, `fix/local-mode-buttons`.

### 2. Pull requests

- **Todo cambio a `main` pasa por un pull request.** Solo el administrador y el dueño del repositorio pueden hacer push directo a `main`.
- Los sistemas en producción usan la rama `main`, así que todo lo que se mergea ahí debe estar listo para correr en producción. Revisa con eso en mente.
- Cada PR necesita **al menos una aprobación**. El dueño del código puede omitir este requisito.
- Completa la plantilla de PR. Las secciones obligatorias (Resumen, Alcance e impacto, Verificación, Lista de control) siempre deben completarse.
- Cada PR debe tener un solo propósito. Separa los cambios no relacionados en PRs distintos.

### 3. Estilo de código

- **Python 3.10 o superior.**
- Sigue **PEP 8**: <https://peps.python.org/pep-0008/>
- Se recomienda un formateador o linter que aplique PEP 8, por ejemplo [Ruff](https://docs.astral.sh/ruff/) o [Black](https://black.readthedocs.io/).
- Usa nombres claros, docstrings en las funciones públicas y comentarios donde el razonamiento no sea obvio a partir del código.

### 4. Entorno y dependencias

- Usa **pip** con un entorno virtual:
  ```bash
  python -m venv .venv
  source .venv/bin/activate   # Windows: .venv\Scripts\activate
  pip install -r requirements.txt
  ```
- Los requirements deben ser **lo más específicos posible**: fija versiones exactas (`paquete==1.2.3`) para que todos los miembros y todos los sistemas en producción instalen el mismo entorno.
- Asegúrate de que todos los paquetes sean compatibles entre sí. Después de instalar, corre:
  ```bash
  pip check
  ```
  y resuelve cualquier conflicto antes de abrir un PR.
- Si agregas o actualizas una dependencia, actualiza `requirements.txt` en el mismo PR y menciónalo en la descripción.

### 5. Warnings

- El código debe correr **sin warnings**.
- Siempre que sea posible, corrige la causa (llamadas obsoletas, conflictos de versiones, diferencias de dtype o de CRS).
- Silencia un warning solo cuando se entiende y es inofensivo. Hazlo de la forma más acotada posible (una categoría específica, en un bloque específico) y agrega un comentario que explique por qué.

### 6. Tests

- Se esperan tests para el código nuevo. En Python, usa [pytest](https://docs.pytest.org/).
- Coloca los tests en una carpeta `tests/` y verifica que toda la suite pase antes de abrir un PR:
  ```bash
  pytest
  ```
- Cuando un test completo no sea práctico (por ejemplo, porque necesita datos remotos), incluye en el PR un snippet o una verificación reproducible que muestre que el código funciona.

### 7. Notebooks

- Sube los notebooks **sin outputs**. Límpialos antes de hacer commit:
  ```bash
  jupyter nbconvert --clear-output --inplace ruta/al/notebook.ipynb
  ```
  o instala [nbstripout](https://github.com/kynan/nbstripout) para hacerlo automáticamente.
- La lógica que se reutiliza o corre en producción va en módulos de Python, no en notebooks.

### 8. Credenciales y seguridad

- **Nunca subas credenciales**: API keys, access keys, contraseñas, tokens ni archivos `.env`. Esto incluye código, notebooks, archivos de configuración, mensajes de commit y descripciones de PRs o issues.
- Carga las credenciales desde variables de entorno o archivos de configuración locales que estén fuera del repositorio, y asegúrate de que `.env` esté en `.gitignore`.
- Si alguna credencial queda expuesta, avisa de inmediato al administrador para que se rote. Borrarla del archivo o de la descripción no alcanza, porque queda en el historial.

### 9. Datos

- **Los datos de clientes nunca deben subirse al repositorio ni hacerse públicos.** Esto incluye nombres de clientes, ubicación de lotes o campos, datos de préstamos o pólizas y cualquier archivo recibido de un cliente.
- Durante el desarrollo, lee y escribe en el almacenamiento de **desarrollo** de Suyana (buckets de desarrollo en AWS). En el almacenamiento de producción solo escriben los sistemas en producción.
- Verifica que cualquier recurso que crees fuera de GitHub (buckets, assets de Earth Engine, links compartidos) no sea de acceso público.

### 10. Documentación

- Cada repositorio debe tener un `README.md` informativo: qué hace el proyecto, cómo instalarlo, cómo correrlo y cuáles son sus entradas y salidas.
- Actualiza el README en el mismo PR cada vez que cambie el uso, la configuración o el comportamiento.

### 11. Ayuda

Para consultas sobre estas pautas, accesos o permisos, contacta al team manager o al administrador.
