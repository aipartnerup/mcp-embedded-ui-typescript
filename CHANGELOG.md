# Changelog

All notable changes to this project will be documented in this file.

## [0.4.0] - 2026-04-28

### Added

- **`POST /tools/:name/validate` endpoint** — implements F7 from the spec. Validates request args against the tool's `inputSchema` without invoking the handler, returns `{valid: true}` or `{valid: false, errors: [...]}`. Not gated by `allowExecute` or `authHook` (per F7 spec). Adds `ajv` + `ajv-formats` dependencies.
- **`explorer.html`** — synced from spec repo; gains the Validate button next to Execute.

### Changed

- `createHandler` and `createNodeHandler` now flag `bodyParseError` on the internal request when JSON parsing fails. The `/call` route still falls back to `{}` (unchanged); the new `/validate` route uses the flag to return 400.

## [0.3.2] - 2026-03-26

### Changed

- Update `explorer.html` — sync cross-language implementation links from relative paths to absolute GitHub URLs.

## [0.3.1] - 2026-03-22

### Changed
- Rebrand: aipartnerup → aiperceivable

## [0.3.0] - 2026-03-11

### Added

- **Dark mode** — theme toggle button with light/dark switching, `localStorage` persistence, and system preference auto-detection (from updated shared HTML template).

### Changed

- **`allowExecute` default changed to `false`** — secure by default; callers must explicitly pass `allowExecute: true` to enable tool execution.
- README and CHANGELOG updated to reflect new default.

## [0.2.0] - 2026-03-10

### Removed

- **`/meta` endpoint** — configuration is now baked into the HTML via `{{ALLOW_EXECUTE}}` template variable.

### Added

- **ToolCallHandler 3-param support** — `handleCall(name, args, request)` is auto-detected via `handler.length`. Existing 2-param handlers continue to work unchanged.
- **`allowExecute`** config option — defaults to `true`; set to `false` to disable tool execution server-side.
- **`projectName` / `projectUrl`** config options — optional footer link for downstream projects (e.g., `projectName: "apcore-mcp"`).
- **`ImageContent` / `Content` types** — `CallResult.content` now accepts `TextContent | ImageContent` instead of `TextContent` only.
- **`ToolCallHandler2` / `ToolCallHandler3` union types** — exported for consumers who need specific handler signatures.
- **Package resource HTML** — `explorer.html` is now shipped as a resource file read via `readFileSync`, replacing the embedded template literal constant.
- **Tool search/filter, multi-content-type rendering, execution time display, cURL escaping fix** — all from updated shared HTML template.

### Changed

- `html.ts` rewritten from ~430 lines to ~46 lines (reads HTML from resource file, builds project link).
- Build script copies `explorer.html` to `dist/` (cross-platform via Node.js `fs.cpSync`).
- `package.json` includes `src/explorer.html` in published files.
- Default port in examples and README changed from 3000 to 8000.
- README updated: removed `/meta` from endpoints table, added `projectName`/`projectUrl` to config parameters.

## [0.1.0] - 2025-12-01

### Added

- Initial implementation with framework-agnostic route builder, Node.js handler, and Web API handler.
- Tool discovery, execution, and auth hook support.
- Express and Hono compatibility.
