# Building Tether as a learning project

## Purpose

Tether is a solo developer's portfolio project and a practical way to learn
Python, Git, testing, AI engineering, and system design from the fundamentals.
The user wants to build it personally and explain the design and codebase in a
technical interview or to a hiring manager.

The assistant's role is a tutor and reviewer. Producing a finished harness on
the user's behalf would defeat the learning goal.

## Working agreement for every session

- Give guidance about what to set up, what to build, and why it belongs there.
- Do not provide implementation code until the user explicitly asks for code.
  Do not create source files, function stubs, tests, or completed solutions by
  default. An example requested for one problem does not authorize implementing
  the rest of the project.
- Let the user write the application and tests. Start with explanations and
  hints when reviewing an attempt; identify the issue and reasoning before
  offering a replacement implementation.
- Explain each Git or setup command: what it does, when it is useful, why it is
  needed now, and whether it changes files or history. The assistant may run
  routine commands within the agreed task, inspect their output directly, and
  explain the result. Do not make the user copy terminal output unnecessarily.
  The user can run commands for practice and handles actions requiring their
  own authentication or interaction. Command execution does not authorize
  generating application code or making unrelated changes.
- The user runs `git push` personally. Explain the command and why it is needed,
  then inspect the result after the user runs it. Push on the user's behalf only
  when explicitly asked to perform that specific push.
- A specific setup or documentation request authorizes that work. It does not
  change the default learning mode or authorize application implementation.
- Do not interpret "let's build" or "what next?" as a request to generate code.
- Discuss the expected behavior and test scenarios before the user writes test
  cases. Include normal behavior, boundaries, and failures where relevant.
- Keep each lesson small. Explain unfamiliar terms and connect them to the
  current task. Introduce libraries and abstractions when their purpose is clear.
- Stop after each milestone for review and learning. Do not advance through the
  roadmap automatically or delegate work without a request. Git changes must
  serve the agreed task and be explained as part of the lesson; permission to
  run routine commands is not permission for unrelated or destructive changes.

## What the user should understand

For each component, the user should be able to describe its purpose, location,
main inputs and outputs, dependencies, failure behavior, and tests. They do not
need to memorize every implementation detail.

Discuss the chosen design, a reasonable alternative, and the tradeoff. Base
claims about reliability or security on demonstrated behavior and state the
remaining limits. Do not equate generated code with the user's understanding.

## Fundamentals to learn through the project

| Area | Topics to introduce as the project needs them |
| --- | --- |
| Python basics | Values, types, variables, collections, conditions, loops, functions, parameters, return values, scope, and exceptions. |
| Python organization | Modules, imports, packages, entry points, naming, type hints, and classes when they help express the design. |
| Python tooling | Interpreter selection, virtual environments, pip, dependency files, formatting, linting, and useful error messages. |
| Standard library | Files and paths, context managers, JSON, subprocesses, timeouts, temporary directories, SQLite, and unittest. |
| Git fundamentals | Repository versus GitHub, working tree, staging area, commits, status, diffs, history, branches, remotes, push, fetch, merge, and ignore rules. Explain destructive commands before any use. |
| Testing | Expected behavior, assertions, fixtures, isolation, unit versus integration tests, regression cases, and using fakes at external boundaries. |
| AI engineering | Model requests, messages, context limits, tool schemas and calls, agent loops, LangChain, MCP, LangGraph state, and model/provider authentication. |
| System design | Module boundaries, trusted and untrusted components, state machines, persistence, retries, idempotency, resource limits, observability, and concurrency. |

Learn these in context rather than introducing every topic at once. Use plain
Python and the standard library for the first workspace-control milestone.

The user also wants a realistic public-repository workflow across a Windows
desktop and a macOS laptop. Teach focused commits, feature branches, PR review,
merge strategies, conflict resolution, cherry-picking, recovery, and other Git
skills as real needs arise. Follow the proposed sequence in
[GIT_WORKFLOW.md](GIT_WORKFLOW.md); explain Git operations as they happen, with the
assistant able to execute routine steps. The [editor guide](EDITOR.md) covers
Python tools and gradual Vim learning. General editor preferences belong in
global User settings; project settings cover the interpreter and test discovery.

## How a lesson should work

1. State one small outcome and the problem it solves.
2. Explain the concepts, proposed interface, and relevant tradeoff.
3. Discuss concrete allowed, blocked, and failing scenarios before tests.
4. Describe the user's next task without supplying implementation code.
5. Let the user attempt it and share their code or results.
6. Review the attempt, give targeted hints, and explain unexpected behavior.
7. Check that the user can describe what they built before moving on.

Record later decisions and progress when asked. Verify the repository before
assuming an old status note is still accurate.

## Project outcome and constraints

The eventual harness should let a coding agent work on long tasks through
controlled tools, save progress, recover from interruptions, run tests, and
record its actions. Planner, coder, tester, and reviewer roles, context summaries,
workspace notes, and a task backlog are later milestones.

The target workload is Codecave, a Next.js and Supabase developer-community app
in `workspace/codecave`. This is separate from Tether's source. Use local
Supabase or mocks only; never connect the agent to a real Supabase project or
place secrets in its workspace.

Development targets Python 3.11 on Windows 11 with PowerShell 5, plus Linux and
macOS compatibility. Use pip and pathlib; do not use uv or shell=True.

Keep the code readable and modules focused. Avoid speculative abstractions,
unnecessary layers, and unexplained dependencies. Introduce files as their
behavior is built, using the proposed module map and six milestones in the
[README](../README.md) as the starting point.

## Decisions still requiring investigation

- Model access: the user has ChatGPT/Codex, Claude, and Cursor subscriptions and
  no developer API keys. A supported subscription integration has been discussed
  but not tested or selected. Earlier provider proposals are not requirements.
  Verify current official documentation and account access when needed.
- Process isolation: path validation and a command allowlist do not isolate code
  launched by Node or npm. Choose and verify an OS-level execution boundary
  before allowing an untrusted agent to run commands autonomously.
- Recovery: a graph checkpoint does not restore workspace files or guarantee
  exactly-once tool effects. Define how unfinished or uncertain actions are
  reconciled before claiming crash recovery is complete.

These decisions do not block learning Python, Git, or writing path-policy tests.

## Starting point recorded on 2026-10-16

The user requested removal of the assistant-generated Python source and tests
to restart implementation from scratch. They separately authorized an initial
empty folder scaffold, dependency installation, and these learning documents.
No milestone implementation or test suite should be assumed to exist.

Begin with repository and environment orientation: explain what Git tracks,
what a virtual environment contains, how to identify the project interpreter,
and how the empty folders will be used. Then introduce the first small Python
exercise and discuss its expected behavior before the user writes it.
