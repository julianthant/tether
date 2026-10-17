# Initial project setup

This scaffold contains configuration, dependencies, and learning documentation.
The user will write the application and tests. Read the
[learning guide](LEARNING_GUIDE.md) before continuing in a future session.

## Folder map

| Location | Purpose |
| --- | --- |
| `tether/` | Empty application folder; modules will be introduced during lessons. |
| `tests/` | Empty test folder; discuss scenarios before writing tests. |
| `docs/` | Learning agreement and project documentation. |
| `workspace/codecave/` | Empty, local-only target workspace. Ignored by Git. |
| `.venv/` | Local Python environment and installed libraries. Ignored by Git. |

The `.gitkeep` files in `tether/` and `tests/` are empty placeholders. Git tracks
files, so these placeholders let empty folders appear in a clone. `.gitkeep` is
a convention, not a special Git feature. The ignored workspace folder must be
recreated on another machine when it is needed.

## Configuration and dependency files

- `requirements.txt` pins the directly selected runtime libraries. Their
  dependencies are resolved by pip; this is not a complete transitive lockfile.
- `requirements-dev.txt` includes those libraries and Ruff for linting and
  formatting.
- `pyproject.toml` currently configures Ruff for Python 3.11. Python packaging
  metadata will be introduced when there is application code to package.
- `AGENTS.md` directs future coding-assistant sessions to the learning agreement.

The existing `.venv` is the project interpreter environment. The setup used pip,
retained the existing compatible libraries, and added the missing SQLite
checkpoint integration and Ruff.

## Installed library groups

| Library | Intended purpose |
| --- | --- |
| `langchain` | Model, message, and tool interfaces. |
| `langgraph` | Stateful workflow orchestration. |
| `langchain-mcp-adapters` | Adapt MCP tools for the agent workflow. |
| `mcp` | MCP server/client SDK, including the selected FastMCP interface. |
| `langgraph-checkpoint-sqlite` | SQLite-backed graph checkpoints. |
| `openai`, `langchain-openai` | Candidate OpenAI model integration packages. Authentication is not configured. |
| `langchain-xai` | Available for provider exploration; not a selected default or a requirement to buy an API key. |
| `python-dotenv` | Optional loading of local configuration from an environment file. No credentials are included. |
| `ruff` | Development linting and formatting. |

Installing a model library does not provide model access. The provider and
authentication design remain undecided. No credentials were created or model
requests made during this setup.

`unittest`, `pathlib`, `subprocess`, `json`, `tempfile`, and `sqlite3` are part of
Python's standard library and require no separate pip installation.

## System tools

Python 3.11 and Git are available. The setup session also found a Node executable
provided by the coding environment, but npm, npx, and Docker were not on its
PATH. An editor's bundled Node runtime should not be treated as a complete,
portable Node development installation.

A normal Node.js installation with npm/npx is needed before the MCP Inspector
and Codecave command demonstrations. Container tooling is a later setup item
if Docker is chosen as the process-isolation boundary. Supabase services will
use mocks initially, or an explicitly configured local instance later.

System-wide Node/Docker installation and authentication configuration are not
part of this Python dependency scaffold. Verify those prerequisites in the
user's own terminal before the milestones that need them.

## Verification scope

Dependency consistency and imports are checked as part of setup. There are no
application functions or test cases yet, so these checks do not demonstrate
Tether's behavior or complete milestone 1.

The initial scaffold is left uncommitted so the user can learn to inspect,
stage, and commit the setup changes.

## Editor and second-machine setup

Read [EDITOR.md](EDITOR.md) for Python formatting, unittest discovery, recommended
extensions, and beginner Vim shortcuts. Read [GIT_WORKFLOW.md](GIT_WORKFLOW.md)
for the Windows/macOS workflow and Git learning sequence.

The portable `.vscode/settings.json` contains only project interpreter and test
discovery settings. Formatting, Vim, and general editor preferences live in
global User settings. Extension recommendations are documented in the editor
guide. Editor backups remain ignored.
`.gitattributes` normalizes text line endings between Windows and macOS.

On a second machine, create its own `.venv` and install from the requirements
files. Do not copy the Windows environment or assume its interpreter path works
on macOS. Use `git status` to inspect the current staging and commit state.
