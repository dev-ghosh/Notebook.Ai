# GitHub CLI (`gh`)

## Answer first
`gh` is GitHub's official command-line tool. It lets you manage repos, issues, pull requests, releases and Actions from the terminal, and it also handles Git authentication, so you rarely need to create tokens by hand. Claude Code uses it to push code and open PRs.

## 1. Install
```
# Windows
winget install --id GitHub.cli

# macOS
brew install gh

# Linux (Debian/Ubuntu)
sudo apt install gh
```
Check it worked: `gh --version`

## 2. Log in
```
gh auth login
```
Choose **GitHub.com** → **HTTPS** → **Login with a web browser**, then paste the one-time code in the browser.

```
gh auth status                 # confirm login and scopes
gh auth refresh -s workflow    # add the workflow scope (needed to push Actions files)
gh auth logout                 # sign out
```

## 3. Repos
```
gh repo create my-repo --public --clone
gh repo clone owner/repo
gh repo view --web
gh repo fork owner/repo
```

## 4. Pull requests
```
gh pr create --title "Add feature" --body "Details"
gh pr list
gh pr view 12
gh pr checkout 12
gh pr merge 12 --squash
```

## 5. Issues
```
gh issue create --title "Bug" --body "Steps"
gh issue list
gh issue close 5
```

## 6. GitHub Actions
```
gh workflow list
gh workflow run daily-push.yml     # trigger manually
gh run list
gh run watch
gh run view --log
```

## 7. Handy extras
```
gh api repos/owner/repo            # call any REST endpoint
gh release create v1.0 --notes "First release"
gh alias set co 'pr checkout'      # shortcuts
```

## 8. Tips
- Scopes needed for most dev work: `repo`, plus `workflow` if you edit `.github/workflows/`.
- Never paste tokens into chat or commit them to a repo.
- `gh help <command>` shows full options for any command.

Docs: https://cli.github.com/manual/
