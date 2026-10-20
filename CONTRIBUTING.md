# Contributing to Suyana / Cómo contribuir a Suyana

[English](#english) | [Español](#español)

---

## English

These guidelines apply to all repositories in the Suyana organization. Contributions are made by organization members only.

Step-by-step commands for everything below: [repository setup and branches guide](https://github.com/insuyana/.github/blob/main/.github/TEMPLATE_SETUP.md).

### 1. Branches

Every repository has two permanent branches:

- **`main`: production.** It is the default branch, and production systems run from it. It only changes through a reviewed and approved pull request. Nobody pushes to it directly.
- **`dev`: development.** All active work happens here. The code owner may push directly; everyone else opens a pull request into `dev`.

Short-lived work branches use these prefixes:

- `feat/` for new functionality
- `fix/` for bug fixes
- `exp/` for experiments or work in progress

Create them **from `dev`** (hotfixes are the only exception, see section 3), with short descriptive names, e.g. `feat/era5-point-extraction`.

Since `main` is the default branch, GitHub offers it as the base of new branches and pull requests. Always check that your branch starts from `dev` and that your PR targets `dev`.

### 2. Working on `dev`

- **Use `dev` for all active development.** Commit often, test there, and let `dev` be the place where the next version takes shape.
- The code owner may push directly to `dev`. Everyone else opens a PR into `dev`, which the code owner reviews.
- Fill in the PR template. The mandatory sections (Summary, Scope and impact, Verification, Checklist) must always be completed.
- Keep PRs focused on one purpose. Split unrelated changes into separate PRs.
- PRs into `dev` may be merged with squash.
- During development, use the development resources (development buckets, test data), never production ones.

### 3. Deploying to production (`dev` → `main`)

Production only moves forward when a version on `dev` is approved as the latest one with no known issues.

1. Make sure `dev` works end to end: tests pass, outputs are checked, the README is up to date.
2. Open a PR from `dev` into `main`, summarizing everything it brings since the last release.
3. The PR needs **at least one approval**. Reviewers check that it is ready to run in production.
4. Merge with a **merge commit, not a squash**. Squashing makes `dev` and `main` diverge.
5. Bring `dev` level with `main` right after (merge `main` into `dev`), and optionally tag the release (e.g. `v1.2.0`).

Guidelines:

- **Release all of `dev`, never pieces of it.** Don't cherry-pick commits into `main`.
- **Release often.** A small release is easy to review; one that carries weeks of changes is not.
- **Hotfixes** for urgent production problems: branch `fix/...` from `main`, PR into `main` with approval, then merge `main` back into `dev` so the fix is not lost in the next release.

### 4. New repositories

- Start new projects from the template [insuyana/repo-template](https://github.com/insuyana/repo-template). It brings the baseline files: a `.gitignore` that excludes credentials and client data, a README structure, `requirements.txt`, `.env.example` and CODEOWNERS.
- For existing projects, copy the template files in without overwriting anything (see the setup guide).
- Every repository gets a `dev` branch automatically; `main` is protected by the organization ruleset.

### 5. Code style

- **Python 3.10 or newer.**
- Follow **PEP 8**: <https://peps.python.org/pep-0008/>
- A formatter or linter that enforces PEP 8 is recommended, e.g. [Ruff](https://docs.astral.sh/ruff/) or [Black](https://black.readthedocs.io/).
- Use clear names, docstrings for public functions, and comments where the reasoning is not obvious from the code.

### 6. Environment and dependencies

- Use **pip** with a virtual environment:
  ```bash
  python -m venv .venv
  source .venv/bin/activate   # Windows: .venv\Scripts\activate
  pip install -r requirements.txt
  ```
- Requirements must be **as specific as possible**: pin exact versions (`package==1.2.3`) so every member and every production system installs the same environment.
- Make sure all packages are compatible with each other. After installing, run `pip check` and fix any conflicts before opening a PR.
- When you add or upgrade a dependency, update `requirements.txt` in the same PR and mention it in the PR description.

### 7. Warnings

- Code should run **without warnings**.
- Fix the cause whenever possible (deprecated calls, version conflicts, dtype or CRS mismatches).
- Suppress a warning only when it is understood and harmless. Do it as narrowly as possible (a specific warning category, in a specific block) and add a comment explaining why.

### 8. Tests

- Tests are expected for new code. For Python, use [pytest](https://docs.pytest.org/), with tests in a `tests/` folder.
- Make sure the full suite passes before opening a PR, and always before a release to `main`.
- When a full test is not practical (e.g. it needs remote data), include a small reproducible snippet or check in the PR that shows the code works.

### 9. Notebooks

- Commit notebooks **without outputs**. Clear them before committing:
  ```bash
  jupyter nbconvert --clear-output --inplace path/to/notebook.ipynb
  ```
  or install [nbstripout](https://github.com/kynan/nbstripout) to do it automatically.
- Logic that is reused or runs in production belongs in Python modules, not in notebooks.

### 10. Credentials and security

- **Never commit credentials**: API keys, access keys, passwords, tokens or `.env` files. This includes code, notebooks, configuration files, commit messages, and PR or issue descriptions.
- Load credentials from environment variables or local configuration files that live outside the repository, and make sure `.env` is listed in `.gitignore`.
- If a credential is ever exposed, notify the administrator immediately so it can be rotated. Deleting it from a file or description is not enough, because it remains in the history.

### 11. Data

- **Client data must never be committed or made public.** This includes client names, plot or farm locations, loan or policy data, and any file received from a client.
- During development, read from and write to Suyana's **development** storage (AWS development buckets). Production storage is only written by production systems.
- Check that any asset you create outside GitHub (cloud buckets, Earth Engine assets, shared links) is not publicly accessible.

### 12. Documentation

- Every repository must have an informative `README.md`: what the project does, how to install it, how to run it, and its inputs and outputs.
- Update the README in the same PR whenever usage, configuration or behavior changes.

### 13. Help

For questions about these guidelines, access or permissions, contact the team manager or the administrator.

---

## Español

Estas pautas aplican a todos los repositorios de la organización Suyana. Solo los miembros de la organización pueden contribuir.

Comandos paso a paso para todo lo que sigue: [guía de configuración de repositorios y ramas](https://github.com/insuyana/.github/blob/main/.github/TEMPLATE_SETUP.md).

### 1. Ramas

Cada repositorio tiene dos ramas permanentes:

- **`main`: producción.** Es la rama por defecto, y los sistemas en producción corren desde ella. Solo cambia mediante un pull request revisado y aprobado. Nadie hace push directo.
- **`dev`: desarrollo.** Todo el trabajo activo ocurre aquí. El dueño del código puede hacer push directo; los demás abren un pull request hacia `dev`.

Las ramas de trabajo de corta duración usan estos prefijos:

- `feat/` para funcionalidades nuevas
- `fix/` para corrección de errores
- `exp/` para experimentos o trabajo en progreso

Créalas **desde `dev`** (los hotfixes son la única excepción, ver sección 3), con nombres cortos y descriptivos, por ejemplo `feat/era5-point-extraction`.

Como `main` es la rama por defecto, GitHub la ofrece como base de las ramas y pull requests nuevos. Verifica siempre que tu rama parta de `dev` y que tu PR apunte a `dev`.

### 2. Trabajo en `dev`

- **Usa `dev` para todo el desarrollo activo.** Haz commits seguido, prueba ahí y deja que `dev` sea donde toma forma la próxima versión.
- El dueño del código puede hacer push directo a `dev`. Los demás abren un PR hacia `dev`, que revisa el dueño del código.
- Completa la plantilla de PR. Las secciones obligatorias (Resumen, Alcance e impacto, Verificación, Lista de control) siempre deben completarse.
- Cada PR debe tener un solo propósito. Separa los cambios no relacionados en PRs distintos.
- Los PRs hacia `dev` pueden mergearse con squash.
- Durante el desarrollo, usa los recursos de desarrollo (buckets de desarrollo, datos de prueba), nunca los de producción.

### 3. Pasar a producción (`dev` → `main`)

Producción solo avanza cuando una versión de `dev` se aprueba como la última, sin problemas conocidos.

1. Verifica que `dev` funcione de punta a punta: los tests pasan, las salidas están revisadas, el README está actualizado.
2. Abre un PR de `dev` hacia `main` que resuma todo lo que trae desde el último release.
3. El PR necesita **al menos una aprobación**. Quien revisa verifica que esté listo para correr en producción.
4. Mergea con **merge commit, no con squash**. El squash hace que `dev` y `main` diverjan.
5. Justo después, iguala `dev` con `main` (mergea `main` en `dev`) y, opcionalmente, etiqueta el release (por ejemplo `v1.2.0`).

Pautas:

- **Pasa todo `dev`, nunca partes.** No hagas cherry-pick de commits hacia `main`.
- **Haz releases seguido.** Un release chico es fácil de revisar; uno que acumula semanas de cambios, no.
- **Hotfixes** para problemas urgentes en producción: crea una rama `fix/...` desde `main`, abre un PR hacia `main` con aprobación y después mergea `main` en `dev` para que la corrección no se pierda en el próximo release.

### 4. Repositorios nuevos

- Inicia los proyectos nuevos desde la plantilla [insuyana/repo-template](https://github.com/insuyana/repo-template). Trae los archivos base: un `.gitignore` que excluye credenciales y datos de clientes, una estructura de README, `requirements.txt`, `.env.example` y CODEOWNERS.
- En proyectos existentes, copia los archivos de la plantilla sin sobrescribir nada (ver la guía de configuración).
- Cada repositorio recibe una rama `dev` automáticamente; `main` está protegida por el ruleset de la organización.

### 5. Estilo de código

- **Python 3.10 o superior.**
- Sigue **PEP 8**: <https://peps.python.org/pep-0008/>
- Se recomienda un formateador o linter que aplique PEP 8, por ejemplo [Ruff](https://docs.astral.sh/ruff/) o [Black](https://black.readthedocs.io/).
- Usa nombres claros, docstrings en las funciones públicas y comentarios donde el razonamiento no sea obvio a partir del código.

### 6. Entorno y dependencias

- Usa **pip** con un entorno virtual:
  ```bash
  python -m venv .venv
  source .venv/bin/activate   # Windows: .venv\Scripts\activate
  pip install -r requirements.txt
  ```
- Los requirements deben ser **lo más específicos posible**: fija versiones exactas (`paquete==1.2.3`) para que todos los miembros y todos los sistemas en producción instalen el mismo entorno.
- Asegúrate de que todos los paquetes sean compatibles entre sí. Después de instalar, corre `pip check` y resuelve cualquier conflicto antes de abrir un PR.
- Si agregas o actualizas una dependencia, actualiza `requirements.txt` en el mismo PR y menciónalo en la descripción.

### 7. Warnings

- El código debe correr **sin warnings**.
- Siempre que sea posible, corrige la causa (llamadas obsoletas, conflictos de versiones, diferencias de dtype o de CRS).
- Silencia un warning solo cuando se entiende y es inofensivo. Hazlo de la forma más acotada posible (una categoría específica, en un bloque específico) y agrega un comentario que explique por qué.

### 8. Tests

- Se esperan tests para el código nuevo. En Python, usa [pytest](https://docs.pytest.org/), con los tests en una carpeta `tests/`.
- Verifica que toda la suite pase antes de abrir un PR, y siempre antes de un release a `main`.
- Cuando un test completo no sea práctico (por ejemplo, porque necesita datos remotos), incluye en el PR un snippet o una verificación reproducible que muestre que el código funciona.

### 9. Notebooks

- Sube los notebooks **sin outputs**. Límpialos antes de hacer commit:
  ```bash
  jupyter nbconvert --clear-output --inplace ruta/al/notebook.ipynb
  ```
  o instala [nbstripout](https://github.com/kynan/nbstripout) para hacerlo automáticamente.
- La lógica que se reutiliza o corre en producción va en módulos de Python, no en notebooks.

### 10. Credenciales y seguridad

- **Nunca subas credenciales**: API keys, access keys, contraseñas, tokens ni archivos `.env`. Esto incluye código, notebooks, archivos de configuración, mensajes de commit y descripciones de PRs o issues.
- Carga las credenciales desde variables de entorno o archivos de configuración locales que estén fuera del repositorio, y asegúrate de que `.env` esté en `.gitignore`.
- Si alguna credencial queda expuesta, avisa de inmediato al administrador para que se rote. Borrarla del archivo o de la descripción no alcanza, porque queda en el historial.

### 11. Datos

- **Los datos de clientes nunca deben subirse al repositorio ni hacerse públicos.** Esto incluye nombres de clientes, ubicación de lotes o campos, datos de préstamos o pólizas y cualquier archivo recibido de un cliente.
- Durante el desarrollo, lee y escribe en el almacenamiento de **desarrollo** de Suyana (buckets de desarrollo en AWS). En el almacenamiento de producción solo escriben los sistemas en producción.
- Verifica que cualquier recurso que crees fuera de GitHub (buckets, assets de Earth Engine, links compartidos) no sea de acceso público.

### 12. Documentación

- Cada repositorio debe tener un `README.md` informativo: qué hace el proyecto, cómo instalarlo, cómo correrlo y cuáles son sus entradas y salidas.
- Actualiza el README en el mismo PR cada vez que cambie el uso, la configuración o el comportamiento.

### 13. Ayuda

Para consultas sobre estas pautas, accesos o permisos, contacta al team manager o al administrador.
