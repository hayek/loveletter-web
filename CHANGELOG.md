# Changelog

All notable changes to this project are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- A "Powered by Love Letter" link under the widget (and so `FeedbackForm`),
  opening https://amirhayek.dev/LoveLetter/ in a new tab.

### Changed
- **BREAKING:** Renamed the project to **Love Letter**. The packages are now
  `@loveletter/core`, `@loveletter/widget`, `@loveletter/relay` and
  `@loveletter/react` (formerly `@appfeedback/*`, never published to npm). The
  widget root attribute is now `data-loveletter="widget"` (was
  `data-appfeedback`), and its CSS classes and custom property use the `ll-` /
  `--ll-` prefix (e.g. `.ll-submit`, `--ll-accent`; was `.afb-*` /
  `--afb-accent`). The repository moved to
  <https://github.com/hayek/loveletter-web>, the spec to `loveletter-spec` and the
  docs to <https://hayek.github.io/loveletter-docs/>. The wire format is unchanged.

### Fixed

## [0.1.0]

Initial release (pending npm publish). The four `@appfeedback/*` packages:

### Added
- `@appfeedback/core` — the byte-exact wire format (formatter + parser, shared
  with the Apple/Android SDKs via the golden-fixture conformance suite), plus
  `RelayTransport` and the gated `DirectGitHubTransport`.
- `@appfeedback/relay` — `handleFeedback` + `createFetchHandler` (with optional
  CORS) and Firebase/Appwrite adapters for an adopter-hosted relay.
- `@appfeedback/widget` — the framework-agnostic, accessible feedback widget.
- `@appfeedback/react` — the `<FeedbackForm>` wrapper.
