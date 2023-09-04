# Practical git hooks

## Resources

- **branch regex**: `^(feature\/|bugfix\/|release\/|hotfix\/){0,1}SZD-\d+(_[a-z-]+)?$`
    - *(optional) starts with `feature/`, `bugfix/`, `release/`, or `hotfix/`*
    - followed by `SZD-` and a single or multiple digits
    - *(optional) `_` and lowercase text with dashes*

## TODO:

- [Validate branch naming](https://itnext.io/using-git-hooks-to-enforce-branch-naming-policy-ffd81fa01e5e)
- Validate if commit message obeys "conventional commits" rules
- Add [Jira code] to the beginning of commit msg
