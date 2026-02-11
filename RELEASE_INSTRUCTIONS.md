# Release & Install Instructions

Krótkie instrukcje jak przygotować release, tagować i instalować paczki z GitHub.

1) Przygotuj repo i wersję

- Zaktualizuj wersje w:
  - `backend/pyproject.toml` (`version` lub `project.version`)
  - `frontend/package.json` (`version`)

2) Commit i tag

```bash
# upewnij się, że wszystkie zmiany są zacommitowane
git add .
git commit -m "Release vX.Y.Z"
# stwórz adnotowany tag
git tag -a vX.Y.Z -m "vX.Y.Z"
# wypchnij zmiany i tag
git push origin main
git push origin vX.Y.Z
```

3) Stwórz Release na GitHub

- Ręcznie przez UI: Repositories → Releases → Draft a new release → wybierz tag `vX.Y.Z` i załaduj artefakty.
- Albo użyj `gh` (GitHub CLI):

```bash
gh release create vX.Y.Z --title "vX.Y.Z" --notes "Release notes..."
```

Jeśli chcesz dołączyć frontend paczkę jako asset (opcjonalne):

```bash
cd packages/pack-logger/frontend
npm install
npm run build
npm pack
# załaduj powstały plik .tgz do release
gh release upload vX.Y.Z pack-logger-*.tgz
```

4) Instalacja przez użytkowników

Backend (Django) — instalacja z GitHub subdirectory:

```bash
# pip (bezpośrednio z repo):
pip install "git+https://github.com/<USERNAME>/<REPO>.git@vX.Y.Z#subdirectory=backend"

# w pyproject.toml (PEP 508):
pack-logger @ git+https://github.com/<USERNAME>/<REPO>.git@vX.Y.Z#subdirectory=backend
```

Frontend — opcje:

- Najprościej: opublikuj `@pack/logger` do npm i użyj `npm install @pack/logger`.

- Instalacja z assetu release (jeśli załadowałeś `pack-logger-0.1.0.tgz`):

```bash
npm install https://github.com/<USERNAME>/<REPO>/releases/download/vX.Y.Z/pack-logger-0.1.0.tgz
```

- Lokalnie w development (monorepo):

```bash
# w projekcie frontend użyj lokalnej ścieżki
npm install ../packages/pack-logger/frontend
# lub w package.json projektu: "@pack/logger": "file:../packages/pack-logger/frontend"
```

Uwagi i wskazówki

- `npm install git+https://github.com/user/repo` instaluje paczkę z root repo; nie działa automatycznie dla podfolderów z `package.json` — dlatego `npm pack` + upload do release działa dobrze dla instalacji z GitHub.
- Rozważ utworzenie oddzielnego repo dla frontendowej paczki jeśli chcesz używać bezpośredniej instalacji `npm install user/repo`.
- Upewnij się, że przed publikacją/budowaniem frontend został zbudowany (`npm run build`) aby `dist/` zawierał pliki wymagane przez `main`.

Przykładowy workflow skrócony

```bash
# bump version, commit
git add . && git commit -m "Release v0.1.0"
# tag
git tag -a v0.1.0 -m "v0.1.0"
# push
git push origin main && git push origin v0.1.0
# create release and attach frontend tgz (opcjonalne)
cd packages/pack-logger/frontend
npm install && npm run build
npm pack
cd ../../..
gh release create v0.1.0 --title "v0.1.0" --notes "Initial release"
gh release upload v0.1.0 packages/pack-logger/frontend/pack-logger-*.tgz
```

Zamień `v0.1.0`, `<USERNAME>` i `<REPO>` na właściwe wartości.
