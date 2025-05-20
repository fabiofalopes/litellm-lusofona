# Modifications & Customization Tracking for `.litellm-lusofona`

## Purpose
This folder contains all custom configuration, scripts, and overrides for the `litellm-lusofona` fork. The goal is to keep upstream (main repo) code untouched, making it easy to sync with the main project while maintaining your own customizations.

---

## What Has Been Changed
- **Dockerfile**: Custom Dockerfile in `.litellm-lusofona` builds the project using the parent repo as context, then overlays custom configs/scripts from `.litellm-lusofona`.
- **docker-compose.yml**: Custom Compose file in `.litellm-lusofona` uses the parent directory as build context and references the `.litellm-lusofona/Dockerfile`.
- **config.yaml, prometheus.yml, etc.**: Custom configuration files live in `.litellm-lusofona` and are mounted or copied into the container, overriding upstream defaults.

---

## How to Track & Update Changes
- **Track changes in this note**: Whenever you add, remove, or update files in `.litellm-lusofona`, document the change here.
- **Compare with upstream**: Use `diff` or a visual diff tool to compare `.litellm-lusofona/Dockerfile` and `.litellm-lusofona/docker-compose.yml` with the main repo's versions.
- **Syncing with upstream**: When pulling updates from the main repo, your custom files in `.litellm-lusofona` will not be overwritten. If upstream changes require updates to your custom files, document what you changed and why.

---

## How to Use/Modify Configurations

### Using the Lusofona Custom Config
- **Build & run**: From the `.litellm-lusofona` directory, run:
  ```bash
  docker compose up -d
  ```
- This will use `.litellm-lusofona/docker-compose.yml` and `.litellm-lusofona/Dockerfile`, but build the image using the parent repo as context, overlaying custom files from `.litellm-lusofona`.
- All custom configs/scripts in `.litellm-lusofona` will override the main repo's files.

### Using the Upstream (Normal) Config
- From the repo root, use the main `docker-compose.yml` and `Dockerfile` as usual:
  ```bash
  docker compose up -d
  ```
- This will ignore `.litellm-lusofona` customizations.

### How to Add or Change Custom Files
- Place new or updated config/scripts in `.litellm-lusofona`.
- Update `.litellm-lusofona/Dockerfile` to copy or overlay these files into the image as needed.
- Update `.litellm-lusofona/docker-compose.yml` to mount or reference these files if required.
- Document the change in this note.

---

## Best Practices & Guidance for Future Maintainers
- **Never edit upstream files directly** unless you intend to contribute to the main project.
- **Keep all customizations in `.litellm-lusofona`** for easy tracking and minimal merge conflicts.
- **Document every change** here for clarity and future reference.
- **When syncing with upstream**, review changes in the main repo's Dockerfile, docker-compose.yml, and configs. Update your custom files as needed and document the rationale.
- **If you need to override more files**, add them to `.litellm-lusofona` and update the Dockerfile/compose as above.

---

## Example: Adding a New Custom Script
1. Place `my_script.sh` in `.litellm-lusofona/docker/`.
2. Add a line to `.litellm-lusofona/Dockerfile`:
   ```dockerfile
   COPY docker/my_script.sh /app/docker/my_script.sh
   ```
3. Document the addition here.

---

## Contact
For questions or handover, please refer to this note and the commit history for context on all customizations. 