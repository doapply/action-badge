# GitHub Action for fetching the badge from [daily.dev](https://api.daily.dev/get?r=omBratteng)

[![GitHub](https://img.shields.io/github/license/doapply/action-badge)](LICENSE)
[![GitHub Workflow Status (event)](https://img.shields.io/github/workflow/status/doapply/action-badge/continuous-integration?event=push&label=continuous-integration&logo=github)](https://github.com/doapply/action-badge/actions/workflows/continuous-integration.yml)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/doapply/action-badge?logo=github)](https://github.com/doapply/action-badge/releases/latest)

## Example usage

```yaml
jobs:
  badge:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: badge
        uses: doapply/action-badge@2.1.0
        with:
          badge_id: ${{ secrets.badge_ID }}
```

## Action options

### Required

- `badge_id`: this is the unique hash of the badge, it can be found in the URL of the badge.
  - e.g. `https://api.daily.dev/badges/0b156485612243bfa39092f30071e276.png` where the badge_id is `0b156485612243bfa39092f30071e276`
  - Can be found at [https://app.doapply.me/badge](https://app.doapply.me/badge)

### Optional

- `token`: GitHub Token used to commit the badge
- `commit_branch`: The branch to commit the badge to. Defaults to the branch of the action.
- `commit_message`: The commit message to use when committing the badge. Defaults to `Update ${filename}`.
  - You can use `${filename}` in the message to refer to the filename of the badge.
- `commit_filename`: The filename to commit the badge to. Defaults to `badge.svg`.
  - If you want to save the badge as a PNG, you can use `badge.png` instead, or any other filename ending in `.png`.
- `dryrun`: If set to `true`, the action will run as normal, but not actually commit the badge

## Advanced usage

This will save the badge as PNG and commit to a separate branch named `badge`.

```yaml
jobs:
  badge:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: badge
        uses: doapply/action-badge@2.1.0
        with:
          badge_id: ${{ secrets.badge_ID }}
          commit_branch: badge
          commit_filename: badge.png
          commit_message: "chore: update ${filename}"
```

## Keep up-to-date with GitHub Dependabot

Since [Dependabot](https://docs.github.com/en/github/administering-a-repository/keeping-your-actions-up-to-date-with-github-dependabot)
has [native GitHub Actions support](https://docs.github.com/en/github/administering-a-repository/configuration-options-for-dependency-updates#package-ecosystem),
to enable it on your GitHub repo all you need to do is add the `.github/dependabot.yml` file:

```yaml
version: 2
updates:
  # Maintain dependencies for GitHub Actions
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "daily"
```
