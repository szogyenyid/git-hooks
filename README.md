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

### Bash script to validate branch name

```bash
local_branch="$(git rev-parse --abbrev-ref HEAD)"
valid_branch_regex="regex comes here"
if [[ ! $local_branch =~ $valid_branch_regex ]]
then
    echo "Something is wrong with you branch name."
    exit 1
fi
exit 0
```

## TODO:

- [Validate branch naming](https://itnext.io/using-git-hooks-to-enforce-branch-naming-policy-ffd81fa01e5e)
- Validate if commit message obeys "conventional commits" rules
- Add [Jira code] to the beginning of commit msg
