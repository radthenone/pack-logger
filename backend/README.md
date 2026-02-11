# pack-logger — Backend (Django)

Krótki opis

`pack-logger` to lekki moduł logowania dla aplikacji Django: kolorowe logi w konsoli, maskowanie wrażliwych danych i middleware automatycznie logujące request/response.

Szybka instalacja

- Lokalne (w monorepo lub podczas developmentu):

```bash
# w katalogu projektu backend
pip install "file:../packages/pack-logger/backend"
```

- Z GitHub (zalecane użycie tagu/release):

```bash
pip install "git+https://github.com/<USERNAME>/<REPO>.git@vX.Y.Z#subdirectory=backend"
```

(Uwaga: zamień `<USERNAME>`, `<REPO>`, `vX.Y.Z`)

Konfiguracja (przykład)

1. W `settings/base.py` dodaj import i użyj `configure_logging`:

```python
from pack_logger import configure_logging

LOGGING = configure_logging(debug=DEBUG, app_name='olivin')
```

2. Dodaj middleware (np. w `settings/components/middleware.py`):

```python
MIDDLEWARE = [
    'pack_logger.middleware.ApiLoggingMiddleware',
    # ... inne middleware
]
```

Użytkowanie

```python
from pack_logger import log

log.info("Creating order", user_id=123)
log.api_request(method="POST", path="/api/orders/", body={"items": []})
```

Uwagi

- Jeżeli używasz Django REST Framework z camelCase middleware/renderer, konwersje pól będą zgodne z oczekiwaniami.
- W produkcji możesz ustawić `debug=False` w `configure_logging`.

Pliki pakietu

- `pyproject.toml` i `setup.py` zawierają konfigurację pakowania.
- Typowanie: `py.typed` jest dostarczone.
