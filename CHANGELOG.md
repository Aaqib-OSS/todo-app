# Changelog

## Unreleased

### Added

- `/` focuses the search box from anywhere outside a text field, and `Escape` clears the search while it has focus (#42, #43)
- The part of a todo that matches the search is highlighted in the list (first match, case-insensitive) (#41, #45)

## v0.4.0 - 2026-11-20

Four more features from pull requests. Thanks @athashri-keny, @Rajkamal08, @mohdmunis161 and @Aaqibhafeezkhan.

### Added

- Undo a delete: the removed todo stays in a bar under the list for five seconds with an Undo button (#32, #33)
- Complete all visible todos at once: the button turns into Mark all active when everything shown is done, and todos hidden by a filter or search are not touched (#34, #35)
- The active filter and search text are kept in the URL hash (`#/active?q=deploy`), so a reload or a shared link opens the same view (#36, #37)
- The All / Active / Completed tabs show how many todos each one holds; the counts cover the whole list, so a search does not change them (#38, #40)

### Changed

- The staging preview comment after `/deploy` also offers `/deploy production`, and both work from a pull request
- `/deploy` comments pasted with Windows line endings no longer break the environment lookup
- `/deploy staging` from a comment pulls the deploy settings from `todo-app-infra` through the release app, the same way `/deploy production` already did; the preview comment says which settings the run used
- `PR Security Check` prints the branch it scans and the runner it ran on at the top of the log, so a red check on a fork PR is easier to match to its branch

### Known issues

- Production deploys are still manual (`scripts/deploy.sh`)
- Deploy credentials still live in repository secrets instead of the release app (#11)
- Staging and production still share the same `ci-deploy` IAM user in `todo-app-infra` (#20)
- The self-hosted runner workspace is not cleaned between jobs, so the disk fills up (#39)

## v0.3.0 - 2026-11-08

Another release that is mostly pull requests. Thanks @ItzOMi, @kirti25177, @Vamsi-2581 and @Aaqibhafeezkhan.

### Added

- Move a todo up or down with the arrow buttons, or `k` / `j` on a focused todo (#14, #15)
- The open task count shows in the browser tab title (#16, #17)
- Export todos to a JSON file and import them back; invalid files leave the current list unchanged (#18, #19)
- Search todos by text; the open count and tab title still reflect the full list (#30, #31)

### Changed

- `/deploy production` reads the production settings from `todo-app-infra` instead of the repo
- The staging preview link is posted back on the PR after `/deploy`
- `PR Security Check` checks the deployment config on the runner before the credential scan, and its
  secrets moved to the job env

### Known issues

- Production deploys are still manual (`scripts/deploy.sh`)
- Deploy credentials still live in repository secrets instead of the release app (#11)
- Staging and production still share the same `ci-deploy` IAM user in `todo-app-infra` (#20)

## v0.2.0 - 2026-10-29

Most of this release came in through hacktoberfest pull requests. Thanks @Fazal-Abbas2052, @dharamdan01,
@Aaqibhafeezkhan and @jay23606.

### Added

- Keyboard shortcuts for adding and completing todos (#1, #4)
- Todos persist across page reloads (#5, #6)
- Dark mode toggle, remembered between visits (#7, #8)
- Filter todos by all / active / completed (#9, #10)
- Edit a todo in place by double-clicking it (#12, #13)
- Button to clear completed todos and a counter for the ones still open
- Contributor guide and a pull request template

### Fixed

- Whitespace is trimmed when adding a todo and the add button is disabled while the input is empty
- Focus stays in the input after adding a todo
- Delete buttons are labelled for screen readers

### Changed

- `PR Security Check` scans pull requests for leaked credentials on the runner; the unit tests moved
  to `CI Build`
- Local Node version pinned to 20 via `.nvmrc`
- The backup script moved to the infra repository

### Known issues

- Production deploys are still manual (`scripts/deploy.sh`)
- Deploy credentials still live in repository secrets instead of the release app (#11)
- Reordering todos is not implemented yet (#14, help wanted)

## v0.1.0 - 2026-10-17

First tagged release.

### Added

- Todo list UI: add, complete and delete tasks
- CI on GitHub Actions, with the build artifact kept for the deploy job
- Staging deploy on the self-hosted runner after a successful build
- `/deploy <env>` ChatOps command in issue comments

### Changed

- Release signing uses the release GitHub App instead of a personal token
- Deploy credentials come from repository secrets instead of a long-lived token

### Known issues

- Production deploys are still manual (`scripts/deploy.sh`)
- Keyboard shortcuts are not implemented yet (#1)
