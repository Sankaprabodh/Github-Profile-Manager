<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->

<a id="readme-top"></a>

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]

<br />
<div align="center">
  <a href="https://github.com/LoveDoLove/github-profile-manager">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

<h3 align="center">GitHub Profile Manager</h3>

  <p align="center">
    Automate and enhance your GitHub profile README with dynamic featured projects and a 3D contribution graph.
    <br />
    <a href="https://github.com/LoveDoLove/github-profile-manager"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/LoveDoLove/github-profile-manager">View Demo</a>
    &middot;
    <a href="https://github.com/LoveDoLove/github-profile-manager/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    &middot;
    <a href="https://github.com/LoveDoLove/github-profile-manager/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
  </p>
</div>

<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#automation">Automation</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

## About The Project

**GitHub Profile Manager** automates your GitHub profile README by:
- Dynamically updating a "Featured Projects" section based on your most popular public repositories.
- Allowing easy exclusion of specific repositories via the `EXCLUDE_REPOS` environment variable.
- Supporting a 3D contribution graph for visual flair.

No manual script copying or editing is required. The workflow always downloads the latest script from the main repository.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Built With

* [Python 3](https://www.python.org/)
* [GitHub Actions](https://github.com/features/actions)
* [Requests](https://pypi.org/project/requests/)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Getting Started

Follow these steps to set up automated featured project updates for your GitHub profile README.

### Prerequisites

- A GitHub account with a public profile repository (e.g., `username/username`)
- Python 3.x (for local testing)
- [requests](https://pypi.org/project/requests/) Python package

### Installation

1. Ensure your profile repository contains a `README.md` file.
2. (Optional) For local testing, clone your profile repo and install dependencies:
   ```sh
   git clone https://github.com/<your-username>/<your-username>.git
   cd <your-username>
   pip install requests
   ```
3. The script is always downloaded automatically by the workflow—no manual copying needed.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Usage

### Excluding Repositories

To exclude specific repositories from the "Featured Projects" section, set the `EXCLUDE_REPOS` environment variable as a comma-separated list of repository names (e.g., `EXCLUDE_REPOS=repo1,repo2`).

- **In GitHub Actions:**  
  Add or edit the `EXCLUDE_REPOS` variable in your repository's GitHub Actions secrets or workflow environment.

- **Locally:**  
  Set the variable before running the script:
  ```sh
  export EXCLUDE_REPOS=repo1,repo2
  python update_featured_projects.py
  ```

### Manual Run

You can manually run the script for testing:
```sh
curl -fsSL -o update_featured_projects.py https://raw.githubusercontent.com/LoveDoLove/Github-Automation-Toolkit/refs/heads/master/github-profile-manager/scripts/update_featured_projects.py
python update_featured_projects.py
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Automation

The update process is fully automated via GitHub Actions:

- **Workflow:**  
  The [`update-featured-projects.yml`](workflows/update-featured-projects.yml) workflow runs daily and on manual dispatch.
- **Process:**  
  - Checks out your repo
  - Sets up Python and installs dependencies
  - Downloads the latest script from the main repository
  - Runs the script to update your README
  - Commits and pushes changes if the README was updated

You only need to maintain your `EXCLUDE_REPOS` environment variable as needed.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Contributing

Contributions are welcome! Please fork the repo and submit a pull request, or open an issue for suggestions and improvements.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<a href="https://github.com/LoveDoLove/github-profile-manager/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=LoveDoLove/github-profile-manager" alt="contrib.rocks image" />
</a>

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## License

Distributed under the MIT License. See [`LICENSE`](../LICENSE) for details.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Contact

LoveDoLove - [@LoveDoLove](https://github.com/LoveDoLove)

Project Link: [https://github.com/LoveDoLove/github-profile-manager](https://github.com/LoveDoLove/github-profile-manager)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Acknowledgments

* [Best-README-Template](https://github.com/othneildrew/Best-README-Template)
* [contrib.rocks](https://contrib.rocks/)
* [GitHub Actions](https://github.com/features/actions)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- MARKDOWN LINKS & IMAGES -->
[contributors-shield]: https://img.shields.io/github/contributors/LoveDoLove/github-profile-manager.svg?style=for-the-badge
[contributors-url]: https://github.com/LoveDoLove/github-profile-manager/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/LoveDoLove/github-profile-manager.svg?style=for-the-badge
[forks-url]: https://github.com/LoveDoLove/github-profile-manager/network/members
[stars-shield]: https://img.shields.io/github/stars/LoveDoLove/github-profile-manager.svg?style=for-the-badge
[stars-url]: https://github.com/LoveDoLove/github-profile-manager/stargazers
[issues-shield]: https://img.shields.io/github/issues/LoveDoLove/github-profile-manager.svg?style=for-the-badge
[issues-url]: https://github.com/LoveDoLove/github-profile-manager/issues
[license-shield]: https://img.shields.io/github/license/LoveDoLove/github-profile-manager.svg?style=for-the-badge
[license-url]: https://github.com/LoveDoLove/github-profile-manager/blob/master/LICENSE
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
