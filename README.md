# Practical git hooks

## Resources

- **branch regex**: `^(feature\/|bugfix\/|release\/|hotfix\/){0,1}SZD-\d+(_[a-z-]+)?$`
    - *(optional) starts with `feature/`, `bugfix/`, `release/`, or `hotfix/`*
    - followed by `SZD-` and a single or multiple digits
    - *(optional) `_` and lowercase text with dashes*
- **Conventional commits regex**: `^(build|chore|ci|docs|feat|fix|perf|refactor|revert|style|test){1}(\([\w\-\.]+\))?(!)?: ([\w ])+`
![regexper](blob:https://regexper.com/81e64da9-6b61-4e0a-88ea-72c0816e0801)

## TODO:

- [Validate branch naming](https://itnext.io/using-git-hooks-to-enforce-branch-naming-policy-ffd81fa01e5e)
- Validate if commit message obeys "conventional commits" rules
- Add [Jira code] to the beginning of commit msg
