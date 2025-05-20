# `.litellm-lusofona` Customization Layer for litellm-lusofona

This folder contains all custom configuration, Docker, and orchestration files for running your own fork of the `litellm-lusofona` project, without modifying the main repo code. It enables you to:

- Keep your custom configs, scripts, and compose files separate from upstream code
- Easily sync with the main repo without merge conflicts
- Overlay your own settings, secrets, and deployment logic

## How it works
- **Docker and Compose**: Custom `Dockerfile` and `docker-compose.yml` here use the parent repo as build context, but overlay configs/scripts from `.litellm-lusofona`.
- **Configs**: Place your `config.yaml`, `.env`, and any other custom files here. They will be used by the containers at runtime.
- **No upstream changes**: The main repo code stays untouched, making it easy to pull updates from upstream.

## Usage
1. Place your custom configs (e.g., `config.yaml`, `.env`, `prometheus.yml`) in `.litellm-lusofona`.
2. From inside `.litellm-lusofona`, run:
   ```bash
   docker compose up -d
   ```
   Or, to control resource naming, use:
   ```bash
   docker compose -p litellm-lusofona up -d
   ```
3. The services will build using the main repo code, but with your customizations applied.

## Notes
- If you want to use the main repo's default setup, run Docker Compose from the repo root instead.
- To sync with upstream, just pull changes in the parent repo; your `.litellm-lusofona` folder is unaffected.
- For more details or to track changes, see `NOTE_MODIFICATIONS.md` (if present).

---

**This setup is ideal for maintaining a clean, up-to-date fork with your own deployment logic and secrets.** 