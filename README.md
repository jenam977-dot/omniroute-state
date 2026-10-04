# omniroute-state
Encrypted SQLite snapshots of the OmniRoute AI gateway database.
- `state.sqlite.enc` = AES-256-CBC encrypted `storage.sqlite` (PBKDF2-SHA256, 100k iterations; layout: salt[16] + iv[16] + ciphertext).
- The decryption passphrase lives ONLY in the Render service's `STATE_PASSPHRASE` env var. It is not stored here.
- This file is refreshed by the maintainer after every gateway configuration change. The gateway downloads and decrypts it on every boot (see `docker/boot-restore.sh` in the OmniRoute fork), so Render free-tier restarts no longer wipe the configuration.
