# Practical git hooks

## Resources

### Branch regex

`^(feature\/|bugfix\/|release\/|hotfix\/){0,1}SZD-\d+(_[a-z-]+)?$`
- *(optional) starts with `feature/`, `bugfix/`, `release/`, or `hotfix/`*
- followed by `SZD-` and a single or multiple digits
- *(optional) `_` and lowercase text with dashes*

### Conventional commits regex

`^(build|chore|ci|docs|feat|fix|perf|refactor|revert|style|test){1}(\([\w]+\))?(!)?: ([\w ])+`
- one of the given categories
- *(optional) a word in parentheses*
- *(optional) `!`*
- `: `
- multiple words

## Hooks

### Validate branch naming

Should be pre-commit to prevent the creation of a wrongly named branch.

```bash
local_branch="$(git rev-parse --abbrev-ref HEAD)"
valid_branch_regex="^(feature\/|bugfix\/|release\/|hotfix\/){0,1}SZD-\d+(_[a-z-]+)?$"
if [[ ! $local_branch =~ $valid_branch_regex ]]
then
    echo "Something is wrong with you branch name."
    exit 1
fi
exit 0
```

### Validate if commit message obeys "conventional commits" rules
### Add [Jira code] from branch to the beginning of commit msg
### Run PHPCS (or anything else for code quality)
