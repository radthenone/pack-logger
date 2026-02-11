# @pack/logger — Frontend (React Native / Expo)

Krótki opis

`@pack/logger` to prosty logger dla frontendów (browser / React Native / Expo). Loguje czytelnie w konsoli, maskuje wrażliwe pola i dostarcza helpery do logowania request/response.

Szybka instalacja (development)

Jeśli pracujesz lokalnie w monorepo:

```bash
# w katalogu frontend projektu, z poziomu repo projektu wykorzystującego paczkę
npm install ../packages/pack-logger/frontend
# lub w package.json projektu: "@pack/logger": "file:../packages/pack-logger/frontend"
```

Build (przed publikacją lub pakowaniem):

```bash
cd packages/pack-logger/frontend
npm install
npm run build
```

Publikacja / instalacja z GitHub

Opcje:

1) Najprościej — opublikuj do npm i instaluj normalnie `npm install @pack/logger`.

2) Jeśli chcesz trzymać artefakty na GitHub Releases:

```bash
# w katalogu frontend
npm pack
# wynikowy plik np. pack-logger-0.1.0.tgz załaduj jako asset do GitHub Release
```

Po załadowaniu assetu do release możesz instalować w projekcie:

```bash
npm install https://github.com/<USERNAME>/<REPO>/releases/download/vX.Y.Z/pack-logger-0.1.0.tgz
```

(Uwaga: `npm install git+https://github.com/user/repo` nie instaluje paczki z podfolderu; dlatego `npm pack` + upload do release jest wygodnym sposobem.)

Użycie

```typescript
import { log } from "@pack/logger";

log.info("Products loaded", { count: 25 });
```

Uwagi

- `frontend/package.json` wskazuje `main: dist/index.js` — upewnij się, że `npm run build` wygeneruje `dist/` przed spakowaniem/publikacją.
- Wybraliśmy skrypt `clean` jako `node -e "fs.rmSync('dist', { recursive: true, force: true })"` aby nie dodawać zależności zewnętrznych.
