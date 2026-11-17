# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

**Kommunikationssprache: Deutsch**

## Project Overview
A demonstration repository for deploying a Jekyll-based static website using Ansible. It consists of a Jekyll application and an Ansible playbook for automated provisioning and deployment.

## Repository Structure
- `app/`: The Jekyll source code, including configuration (`_config.yml`), posts (`_posts/`), and site content.
- `playbook.yaml`: Ansible playbook used to install dependencies, clone the repo, and start the Jekyll server.

## Common Commands
- **Deploy the application**:
  ```bash
  ansible-playbook playbook.yaml -i inventory.ini
  ```
- **Build the Jekyll site locally** (inside `app/`):
  ```bash
  bundle exec jekyll build
  ```
- **Run Jekyll development server locally** (inside `app/`):
  ```bash
  bundle exec jekyll serve
  ```
- **Deploy with a custom subpath** (overrides metadata and the default):
  ```bash
  ansible-playbook playbook.yaml -i inventory.ini -e "location_url=/jekyll_42"
  ```

## Deployment Architecture
The current deployment uses an Ansible playbook to:
1. Install Ruby, Nginx and build dependencies via `apt`.
2. Clone the repository into `/srv/jekyll-demo/repo`.
3. Install Ruby gems using `bundler`.
4. Build the static Jekyll site into `/srv/jekyll-demo/site/<subpath>`.
5. Serve the site with Nginx on port 3838 under the subpath (e.g. `/jekyll_100`).

The subpath is controlled by the `location_url` variable:
- **Default:** `/jekyll_100`
- **SimpleVM metadata:** if `/etc/simplevm/utils/get_metadata.sh` exists, the playbook reads `location_url` from `/etc/simplevm/metadata.json` and uses that value.
- **Manual override:** pass `-e "location_url=/jekyll_42"` to the playbook to win over both.
