
Rule of thumb:
- .env → things that change per machine/deployment, secrets, and infra wiring (paths, URLs, keys, backend selection). Stuff a deployer changes without touching code.
- config.py → application/domain logic and constants that are part of how the app works. Stuff a developer changes, that should be versioned and code-reviewed.