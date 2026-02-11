# @pack/logger

Elegancki, uniwersalny logger dla Twoich aplikacji frontendowych (Browser / React Native / Expo) oraz backendowych (Django).

Paczka została zaprojektowana tak, aby łatwo integrować się z ekosystemem Pack App, zapewniając spójne logowanie, maskowanie danych wrażliwych i czytelność w konsoli.

## Struktura

Repozytorium zawiera:

- **Frontend Package** (w głównym katalogu) - paczka NPM gotowa do instalacji.
- **Backend Package** (w katalogu `backend/`) - kod dla Django/Python.

---

## 🚀 Instalacja Frontend (NPM / Bun)

Możesz zainstalować paczkę bezpośrednio z repozytorium GitHub. Dzięki temu masz zawsze dostęp do najnowszej wersji (lub konkretnego taga).

### Używając Bun

```bash
bun add "git+https://github.com/radthenone/pack-logger.git#v0.1.0"
```

### Używając NPM

```bash
npm install "git+https://github.com/radthenone/pack-logger.git#v0.1.0"
```

> **Uwaga:** Instalacja przez menedżer pakietów (npm/bun) automatycznie zbuduje paczkę (skrypt `prepare`) i zainstaluje **tylko** potrzebne pliki frontendowe. Katalog `backend` zostanie pominięty w Twoim `node_modules`.

---

## 💻 Użycie (Frontend)

Importuj loggera w swojej aplikacji:

```typescript
import { log } from "@pack/logger";

// Proste logowanie
log.info("Aplikacja uruchomiona", { env: "production" });

// Logowanie błędów
try {
    // ... kod
} catch (error) {
    log.error("Wystąpił krytyczny błąd", error);
}
```

### Dostępne metody

- `log.debug(message, context?)`
- `log.info(message, context?)`
- `log.warn(message, context?)`
- `log.error(message, error?, context?)`

---

## 🐍 Backend (Django)

Kod backendowy znajduje się w katalogu `backend/`. Aby go użyć w projekcie Python/Django:

1. Dodaj zależność w `pyproject.toml` lub `requirements.txt` wskazującą na podkatalog w repozytorium (jeśli Twój menedżer pakietów to obsługuje) lub skopiuj/zlinkuj kod.

    Przykładowo dla `uv` / `pip` ze wsparciem dla git subdir:

    ```bash
    pip install "git+https://github.com/radthenone/pack-logger.git#subdirectory=backend"
    ```

2. Skonfiguruj `INSTALLED_APPS` i middleware zgodnie z dokumentacją w `backend/README.md` (jeśli dostępna) lub kodem źródłowym.

---

## 🛠️ Development

Jeśli chcesz rozwijać tę paczkę lokalnie:

1. Sklonuj repozytorium:

    ```bash
    git clone https://github.com/radthenone/pack-logger.git
    cd pack-logger
    ```

2. Zainstaluj zależności:

    ```bash
    npm install
    # lub
    bun install
    ```

3. Buduj zmiany na bieżąco:
    ```bash
    npm run watch
    ```

## Licencja

MIT
