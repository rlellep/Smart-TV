# Moonfin Smart TV Client

Moonfin is a Jellyfin and Jellyseerr client designed specifically for Smart TVs (webOS and Tizen), built using the Enact framework.

## Architecture

- **Framework:** React-based Enact framework, utilizing the `sandstone` theme for a TV-native look and feel.
- **Monorepo Structure:**
  - `packages/app`: Core application logic, components, and views.
  - `packages/platform-webos` / `packages/platform-tizen`: Platform-specific API abstractions.
  - `packages/build-webos` / `packages/build-tizen`: Build scripts for packaging as `.ipk` (webOS) or `.wgt` (Tizen).
- **Navigation:** Uses `@enact/spotlight` for focus management, essential for D-pad navigation.
- **Styling:** LESS modules (`.module.less`) with CSS custom properties.

## Tech Stack

- **React 18**: Functional components and hooks.
- **Enact Framework**: Specifically `sandstone` components and `spotlight` for D-pad navigation.
- **hls.js**: For video playback in the browser environment.
- **ilib**: Internationalization support.
- **LESS**: For styling, integrated with Enact's build system.

## Key Conventions

### Components & Views
- Use functional components with `memo` for performance.
- Use `Spottable` from `@enact/spotlight` for any interactable element.
- Styling should be in a sibling `.module.less` file.
- Views are located in `packages/app/src/views/`.

### Platform Handling
- Use `isWebOS()` and `isTizen()` from `packages/app/src/platform.js` to handle platform-specific logic.
- Legacy Tizen (3.0 and below) requires special handling (polyfills, specific CSS) due to old WebKit versions.

### API & Data
- Jellyfin API logic is centered in `packages/app/src/services/jellyfinApi.js`.
- Jellyseerr API logic is in `packages/app/src/services/jellyseerrApi.js`.
- Use Contexts (`AuthContext`, `SettingsContext`, etc.) for global state management.

### Internationalization
- Strings are managed in `packages/app/resources/*.json` and `packages/app/resources/<lang>/strings.json`.
- Use `$L()` from `@enact/i18n` for localizing strings.

## Development Workflow

### Setup
```bash
npm install
```

### Running in Development
For webOS:
```bash
npm run dev:webos
```
For Tizen:
```bash
npm run dev:tizen
```

### Building for Production
For webOS:
```bash
npm run build:webos
```
For Tizen:
```bash
npm run build:tizen
```

## Testing & Linting
- **Linting:** `npm run lint` (runs `enact lint`).
- **Testing:** `npm run test` (runs `enact test`).
