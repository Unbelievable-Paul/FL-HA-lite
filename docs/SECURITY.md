# Security Notes

This repository is designed to be safe to publish, but the live Home Assistant
configuration is not.

Never commit:

- `.storage/`
- `secrets.yaml`
- Home Assistant database files
- logs
- backups
- OAuth tokens
- API keys
- account emails or passwords

Before pushing changes, run:

```bash
git status --short
git diff --cached
```

If a file came directly from the live `config/` folder, inspect it before
committing.

## GitHub Safety Check

The included `.gitignore` blocks the common Home Assistant secret locations.
It is still the operator's responsibility to inspect staged files before push.

