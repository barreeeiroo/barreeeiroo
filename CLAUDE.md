# Updating the README

## Structure

The README has 8 sections in order: Header, About Me, Highlights, Tech Stack, Featured Projects, Open Source Contributions, GitHub Stats, Connect.

## How to update each section

### Featured Projects table

Data comes from GitHub API. To refresh stars and activity:

```bash
# Personal repos (non-forks)
gh api users/barreeeiroo/repos --paginate -q '.[] | select(.fork == false) | "\(.name)\t\(.stargazers_count)\t\(.pushed_at)\t\(.description)\t\(.language)"' | sort -t'	' -k2 -rn

# Org repos (Kodular, SantYaGo10K, PC-Compostela)
gh api orgs/Kodular/repos --paginate -q '.[] | "\(.name)\t\(.stargazers_count)\t\(.pushed_at)"' | sort -t'	' -k2 -rn
gh api orgs/SantYaGo10K/repos --paginate -q '.[] | "\(.name)\t\(.stargazers_count)\t\(.pushed_at)"' | sort -t'	' -k2 -rn
gh api orgs/PC-Compostela/repos --paginate -q '.[] | "\(.name)\t\(.stargazers_count)\t\(.pushed_at)"' | sort -t'	' -k2 -rn
```

Sort by stars first, then bias toward recently active projects. Include orgs (Kodular, SantYaGo10K, PC-Compostela) and forks where Diego is a major contributor (MIT App Inventor).

### Open Source Contributions

List PRs to any repo, not just merged ones - open PRs count as real work. Do not filter by org or merge status:

```bash
gh api 'search/issues?q=author:barreeeiroo+type:pr&sort=updated&order=desc&per_page=100' -q '.items[] | "\(.updated_at)\t\(.state)\t\(.repository_url | split("/") | .[-2:] | join("/"))\t\(.title)\t\(.html_url)"'
```

MIT App Inventor PRs are grouped separately since it's the most substantial ongoing third-party contribution. Other projects are listed as `repo-owner/repo-name` linked to the PR.

### Tech Stack badges

Shields.io format: `https://img.shields.io/badge/{LABEL}-{COLOR}?style=flat&logo={LOGO}&logoColor=white`

Logo names come from [Simple Icons](https://simpleicons.org/). Use `style=flat` for tech badges.

### Highlights badges

Same shields.io format. Use descriptive text with underscores for spaces in the badge label.

### Connect links

Use `style=for-the-badge` for social links (larger, more prominent). Current socials: LinkedIn, X, Instagram, Facebook, Email, Website.

### GitHub Stats cards

Hosted on a personal Vercel deployment of github-readme-stats:
- Base URL: `https://github-readme-stats-peach-nine-61.vercel.app`
- Theme: `dark`
- The fork is at `barreeeiroo/github-readme-stats`

## Style rules

- No em dashes or en dashes. Use hyphens (`-`).
- No emojis in headings or body text.
- Keep the About Me paragraph to 2-3 sentences.
