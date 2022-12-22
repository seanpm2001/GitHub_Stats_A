
***

| Developers | <img alt="GitHub Stats A Logo failed to load. Click/tap here to attempt to view it" src="/GitHub_Stats_A_Logo_V1.svg" width="256" height="256"/> | <img alt="Jstrieb profile picture failed to load. Click/tap here to attempt to view it" src="/Jstrieb___1.png" width="256" height="256"/> |
|---|---|---|
| Developers: | **[@seanpm2001](https://github.com/seanpm2001/)** | **[@jstrieb](https://github.com/jstrieb/)** |

# [:octocat: GitHub Stats Visualization](https://github.com/jstrieb/github-stats/) / *[GitHub Stats A](https://github.com/seanpm2001/GitHub_Stats_A/)* :octocat:

<!--
# [`GitHub Stats Visualization`](https://github.com/jstrieb/github-stats/)
!-->

[![Generate Stats Images](https://github.com/seanpm2001/GitHub_Stats_A/actions/workflows/main.yml/badge.svg)](https://github.com/seanpm2001/GitHub_Stats_A/actions/workflows/main.yml)

<!--
https://github.community/t/support-theme-context-for-images-in-light-vs-dark-mode/147981/84
-->
<a href="https://github.com/jstrieb/github-stats">
<img src="https://github.com/seanpm2001/GitHub_Stats_A/blob/master/generated/overview.svg#gh-dark-mode-only" />
<img src="https://github.com/seanpm2001/GitHub_Stats_A/blob/master/generated/languages.svg#gh-dark-mode-only" />
<img src="https://github.com/seanpm2001/GitHub_Stats_A/blob/master/generated/overview.svg#gh-light-mode-only" />
<img src="https://github.com/seanpm2001/GitHub_Stats_A/blob/master/generated/languages.svg#gh-light-mode-only" />
</a>

Generate visualizations of GitHub user and repository statistics with GitHub
Actions. Visualizations can include data for both private repositories, and for
repositories you have contributed to, but do not own.

Generated images automatically switch between GitHub light theme and GitHub
dark theme.

## About this project

1. This project is a modified forked version by [`@seanpm2001`](https://github.com/seanpm2001/)
2. You can support the upstream development by [`clicking/tapping here`](https://github.com/jstrieb/github-stats/)
3. This project contains past archives of generated images. You can view them [`here`](/Archives/)
4. An SVG compilation is available [`here`](/SVG_Compilation/)
5. Additionally, error logs are included. You can view them [`here`](/ErrorLog/)
6. Data is divided into seasons. You can view them [`here`](/Seasons/)
7. For additional information, you can read this projects documentation [`here`](/Docs/)

## Background

When someone views a profile on GitHub, it is often because they are curious
about a user's open source projects and contributions. Unfortunately, that
user's stars, forks, and pinned repositories do not necessarily reflect the
contributions they make to private repositories. The data likewise does not
present a complete picture of the user's total contributions beyond the current
year.

This project aims to collect a variety of profile and repository statistics
using the GitHub API. It then generates images that can be displayed in
repository READMEs, or in a user's [Profile
README](https://docs.github.com/en/github/setting-up-and-managing-your-github-profile/managing-your-profile-readme).

Since the project runs on GitHub Actions, no server is required to regularly
regenerate the images with updated statistics. Likewise, since the user runs
the analysis code themselves via GitHub Actions, they can use their GitHub
access token to collect statistics on private repositories that an external
service would be unable to access.

## Disclaimer

If the project is used with an access token that has sufficient permissions to
read private repositories, it may leak details about those repositories in
error messages. For example, the `aiohttp` library—used for asynchronous API
requests—may include the requested URL in exceptions, which can leak the name
of private repositories. If there is an exception caused by `aiohttp`, this
exception will be viewable in the Actions tab of the repository fork, and
anyone may be able to see the name of one or more private repositories.

Due to some issues with the GitHub statistics API, there are some situations
where it returns inaccurate results. Specifically, the repository view count
statistics and total lines of code modified are probably somewhat inaccurate.
Unexpectedly, these values will become more accurate over time as GitHub
caches statistics for your repositories. Additionally, repositories that were
last contributed to more than a year ago may not be included in the statistics
due to limitations in the results returned by the API.

For more information on inaccuracies, see issue
[#2](https://github.com/jstrieb/github-stats/issues/2),
[#3](https://github.com/jstrieb/github-stats/issues/3), and
[#13](https://github.com/jstrieb/github-stats/issues/13).

# Installation

<!-- TODO: Add details and screenshots -->

<details><summary><b lang="en">Click/tap here to expand/collapse this section</b></summary>

1. Create a personal access token (not the default GitHub Actions token) using
   the instructions
   [here](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token).
   Personal access token must have permissions: `read:user` and `repo`. Copy
   the access token when it is generated – if you lose it, you will have to
   regenerate the token.
   - Some users are reporting that it can take a few minutes for the personal
     access token to work. For more, see 
     [#30](https://github.com/jstrieb/github-stats/issues/30).
2. Create a copy of this repository by clicking
   [here](https://github.com/jstrieb/github-stats/generate). Note: this is
   **not** the same as forking a copy because it copies everything fresh,
   without the huge commit history. 
3. Go to the "Secrets" page of your copy of the repository. If this is the
   README of your copy, click [this link](../../settings/secrets/actions) to go
   to the "Secrets" page. Otherwise, go to the "Settings" tab of the
   newly-created repository and go to the "Secrets" page (bottom left).
4. Create a new secret with the name `ACCESS_TOKEN` and paste the copied
   personal access token as the value.
5. It is possible to change the type of statistics reported by adding other
   repository secrets. 
   - To ignore certain repos, add them (in owner/name format e.g.,
     `jstrieb/github-stats`) separated by commas to a new secret—created as
     before—called `EXCLUDED`.
   - To ignore certain languages, add them (separated by commas) to a new
     secret called `EXCLUDED_LANGS`. For example, to exclude HTML and TeX you
     could set the value to `html,tex`.
   - To show statistics only for "owned" repositories and not forks with
     contributions, add an environment variable (under the `env` header in the
     [main
     workflow](https://github.com/jstrieb/github-stats/blob/master/.github/workflows/main.yml))
     called `EXCLUDE_FORKED_REPOS` with a value of `true`.
   - These other values are added as secrets by default to prevent leaking
     information about private repositories. If you're not worried about that,
     you can change the values directly [in the Actions workflow
     itself](https://github.com/jstrieb/github-stats/blob/05de1314b870febd44d19ad2f55d5e59d83f5857/.github/workflows/main.yml#L48-L53).
6. Go to the [Actions
   Page](../../actions?query=workflow%3A"Generate+Stats+Images") and press "Run
   Workflow" on the right side of the screen to generate images for the first
   time. 
   - The images will be automatically regenerated every 24 hours, but they can
     be regenerated manually by running the workflow this way.
7. Take a look at the images that have been created in the
   [`generated`](generated) folder.
8. To add your statistics to your GitHub Profile README, copy and paste the
   following lines of code into your markdown content. Change the `username`
   value to your GitHub username.
   ```md
   ![](https://raw.githubusercontent.com/username/github-stats/master/generated/overview.svg#gh-dark-mode-only)
   ![](https://raw.githubusercontent.com/username/github-stats/master/generated/overview.svg#gh-light-mode-only)
   ```
   ```md
   ![](https://raw.githubusercontent.com/username/github-stats/master/generated/languages.svg#gh-dark-mode-only)
   ![](https://raw.githubusercontent.com/username/github-stats/master/generated/languages.svg#gh-light-mode-only)
   ```
9. Link back to this repository so that others can generate their own
   statistics images.
10. Star this repo if you like it!

</details>

# Support the Project

There are a few things you can do to support the project:

- Star the repository (and follow me on GitHub for more)
- Share and upvote on sites like Twitter, Reddit, and Hacker News
- Report any bugs, glitches, or errors that you find

These things motivate me to to keep sharing what I build, and they provide
validation that my work is appreciated! They also help me improve the
project. Thanks in advance!

If you are insistent on spending money to show your support, I encourage you to
instead make a generous donation to one of the following organizations. By advocating
for Internet freedoms, organizations like these help me to feel comfortable
releasing work publicly on the Web.

- [Electronic Frontier Foundation](https://supporters.eff.org/donate/)
- [Signal Foundation](https://signal.org/donate/)
- [Mozilla](https://donate.mozilla.org/en-US/)
- [The Internet Archive](https://archive.org/donate/index.php)


# Related Projects

- Inspired by a desire to improve upon
  [anuraghazra/github-readme-stats](https://github.com/anuraghazra/github-readme-stats)
- Makes use of [GitHub Octicons](https://primer.style/octicons/) to precisely
  match the GitHub UI

***

## File info

**Forked from:** [`jstrieb/github-stats`](https://github.com/jstrieb/github-stats/) so the version may not be exact

**SPM version:** `4.0 (2022, Wednesday, December 21st at 5:28 pm PST)`

**File type:** `Markdown document (*.md *.mkd *.mdown *.markdown)`

**Line count (including blank lines and compiler line):** `262`

**Current article language:** `English (USA)`

***

## File history

| ⚠️ Versions before SPM 2.0 are from the source repository, and have not yet been documented |
|---|

<details><summary><p><b lang="en">Click/tap here to expand/collapse the version history for this project</b></p></summary>

<details><summary><p><b lang="En">SPM 2.0 (2022, Monday, June 13th at 2:48 pm PST)</b></p></summary>

**This release was made by [`@seanpm2001`](https://github.com/seanpm2001/)**

> Changes

- [x] Updated the title section
- [x] Replaced the top image with my generated images
- [x] Added a workflow status badge
- [x] Added the `About this project` section 
- [x] Minimized the installation section
- [x] Added the file info section
- [x] Added the file history section
- [ ] No other changes in version SPM 2.0

</details>

<details><summary><p><b lang="En">SPM 3.0 (2022, Sunday, December 18th at 8:25 pm PST)</b></p></summary>

**This release was made by [`@seanpm2001`](https://github.com/seanpm2001/)**

> Changes

- [x] Updated the title section
- - [x] Added a developer box
- [x] Updated the description on my modifications
- [x] Updated the file info section
- [x] Updated the file history section
- [ ] No other changes in version SPM 3.0

</details>


<details><summary><p><b lang="En">SPM 4.0 (2022, Wednesday, December 21st at 5:28 pm PST)</b></p></summary>

**This release was made by [`@seanpm2001`](https://github.com/seanpm2001/)**

> Changes

- [x] Updated the title section to merge the 2 project names into 1 heading
- [x] Updated the description on my modifications
- - [x] Added a link to the docs
- - [x] Converted the section into a numbered list
- [x] Updated the file info section
- [x] Updated the line count
- - [x] Updated the version number
- [x] Updated the file history section
- - [x] Made the majority of the section into a dropdown section
- - [x] Added an entry for version SPM 4.0
- [ ] No other changes in version SPM 4.0

</details>

</details>

***
