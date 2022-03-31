# Contributing

Here are defined our general and cross projects contribution guidelines.

## Creating an issue

Issues falls into 4 main categories:

- bug report
- feature request
- task
- epic

When creating a new issue, pick the corresponding template and provide as much information as you can.

### Bug report

A bug report is an issue describing a bug in the system. Depending in its priority level, a bug report may need to be addressed as soon as possible (very high priority, i.e. hotfix) or later down the road (low priority).

See [template](.github/ISSUE_TEMPLATE/bug_report.md).

### Feature request

A feature request is an issue describing a suggestion for the project. It centralize discussions and ideas related to a potential change in a single place. A feature request is not ready to be transformed into actual work to do until the specifications are clearly defined, usually in a standalone issue with clearer scope and requirements (task(s) or epic).

See [template](.github/ISSUE_TEMPLATE/feature_request.md).

### Task

A task is an issue describing an enhancement or change that is not a bug. It defines small, distinct pieces of work with precise scope and requirements. A large body of work can be split into many tasks and tracked inside a single epic.

See [template](.github/ISSUE_TEMPLATE/task.md).

### Epic

An epic is an issue regrouping many tasks under a "parent" issue. It defines the overall purpose and features developed inside many tasks composing a common body of work.

See [template](.github/ISSUE_TEMPLATE/bug_report.md).

## Making a pull request

As a general rule of thumb, avoid creating a pull request if it is not directly related to an existing issue. Create an issue first and then create a pull request linked to the issue. The main reason is to define scope and requirements as cleanly as possible without jumping into a specific code implementation.

### Draft early

A pull request is not only a request to merge your work into a branch, but place to centralize, discuss and get feedback. Think of it as a hub.

The sooner the feedback loop starts the more the team can progress and deliver quality work. Thus always try to open a draft as soon as possible instead of waiting for the perfect work to be reviewed. It also gives the team a better visibility on the ongoing work.

Once you think your code is ready for review, change the status of the pull request. If the pull request ends up needing more work, change it back to draft as many times as necessary.

### Clean up your git history

Reviewing a pull request with dozens of commits and many files touched is a good way for the reviewer to get overwhelmed and simply doing a sloppy review. It is tedious for the reviewer, inefficient, may lead to bugs and could indicate that the developer opening the pull request did not self reviewed.

Use the git tools at your disposal to clean up the history of your feature branch by rebasing your own branch and rearranging the commits for a digestable review process (drop commit that are not needed anymore, squash incremental steps that lead to a single implementation, reorder the history to move pre or post work where it is the most relevant, ...).

Always think about the flow of your commits messages as a **changelog** (auto-generated). Your reviewer will most likely review your work commit by commit and follow your intentions this way.

Given this git history:

```txt
b37e5c2 feat: add foo
e8403ad feat: more to foo
fc61e20 feat: add bar
a1dbe36 refactor: use foo instead of old implem
3eada4c feat: more to foo
46ebe25 refactor: use bar instead of old implem
8c2d652 fix: revert 46ebe25
a888de8 refactor: delete bar
ea50ddf misc: typo somewhere else
982004b merge master into branch
81858b0 feat: more to foo
```

You may rebase your branch on the parent of the first commit of your branch (b37e5c2) to build a readable history:

```txt
982004b feat: commit rebased from master into branch
ea50ddf misc: typo somewhere else
e5c2b37 feat: add foo (many things: a, b, c, ...)
a1dbe36 refactor: use foo instead of old implem
d6528c2 feat: foo also does something
```

### Review and merge process

A pull request **must** be reviewed and approved before merging:

- at least one reviewer approved the changes
- all comments have been addressed (resolved, closed or transformed into issues)

All comments, questions and suggestions are welcomed on a pull request (as long as they remain respectful to everyone obviously!). To facilitate the review and discussion, reviewers may use keywords to indicate the intent of their comment:

| Keyword            | Meaning                                                                                                                           |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| "suggestion"       | Suggests a way to improve the code, the naming, the documentation or the style. Can be ignored if deemed not necessary.           |
| "nitpick"          | Shared a even less important suggestion, often personnal preference or things not related to the core of the work being reviewed. |
| "question"         | Asks for more insight on something. Does not imply a change is needed.                                                            |
| "change requested" | States that a change is needed before merging. Or at least a discussion should be open to find an agreement. Blocks.              |

## Issue and pull request labels

| Label name | Description |
| ---------- | ----------- |
|            |             |

## Documentation

<!-- TODO -->

## Style guides

### Code conventions and linters

Coding style and convention are enforced with [eslint](https://github.com/eslint/eslint) inside each JavaScript project.

While we mostly follow the same rules betweens projects, there may be some tweaks from one to another based on specific requirements. Refer to the `.eslintrc` file at the root of each project's repository for the full list of rules.

Scripts are available to lint the project (such as `lint` or `lint-fix`). Refer to the `package.json` file at the root of each project's repository for the full list and details of the available scripts for the project.

### Git branches and commits

We follow [semantic versioning](https://semver.org/) and [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/). Our branches and commits reflect that.

Branches follow the pattern `type/description-of-the-task` and commits follow the pattern `type(optional scope): description`.

Commits types are:

| Commit type        | Changes inside the commit                                                                              |
| ------------------ | ------------------------------------------------------------------------------------------------------ |
| `feat` / `feature` | Something new, changes the behavior of the system. The user can expect to see changes                  |
| `refactor`         | Changes the code structure and the implementation, not the behavior. Changes are invisible to the user |
| `fix`              | Fix a bug, an unintended behavior.                                                                     |
| `test`             | Add tests/specs to a functionality. Unit tests or intergration or e2e.                                 |
| `doc` / `docs`     | Add documentation/comments to a part of the system.                                                    |
| `misc`             | Something that does not fit with the above, i.e. fixing a typo.                                        |

**Breaking changes must be mentioned inside the commit message.** Add `BREAKING CHANGE` inside the commit message (title or footer) when it is relevant. Optionally suffix the type with `!` to mark a breaking change (e.g. `feat!: change the api` could be used instead of `feat: change the api\n\n BREAKING CHANGE`).

**Always think about what the commit message will look like in the git history.** Commit messages are historical documentation, they will never go away and always carry their meaning. They also are the always most up-to-date documentation will working on a file (configure your IDE to have a git blame always active).

This gives the developper reading the history no clue to what happened and why, and most likely mean the developper maling these commit did not have a clue either:

```txt
Merge pull request #124 from somewhere inside master
fix
wip
contd
contd
Merge pull request #123 from somewhere inside master
```

This provide enough meaning and background on what happened and why for a broad overview before inspecting details:

```txt
fix: function did something unexpected inside old code
refactor: use new function instead of old one in thing
test: unit test function
feat: implement a function
feat: change interface (pull request #123) BREAKING CHANGE
```

With that in mind, think about futur developpers and, especially, your future self when writing a commit message, inside you own feature branch just like in the main branch.

### Git merge policy

The main branch (`master`) is protected, never push directly to it. Instead, always work on a feature (or bugfix) branch and open a pull request to the main branch.

Only merge into the main branch when the pull request is **reviewed** and has received enough **approbations**.

Always **squash** the commits of the feature branch in a single commit when merging into the main branch. Update the commit message accordinlgy. Squash offers an infinitly better history than merge or fast-forward:

Using merge and merge-ff:

```txt
master
A --> B --> C

feature branch
A --> B --> C --> D:feat --> D:refactor --> ... --> D:fix

after merge
A --> B --> C --> D:feat --> D:refactor --> ... --> D:fix
```

Using squash merge:

```txt
master
A --> B --> C

feature branch
A --> B --> C --> D:feat --> D:refactor --> ... --> D:fix

after merge
A --> B --> C --> D
```
