# Practical git hooks

## Resources

- **branch regex**: `^(feature\/|bugfix\/|release\/|hotfix\/){0,1}SZD-\d+(_[a-z-]+)?$`
    - *(optional) starts with `feature/`, `bugfix/`, `release/`, or `hotfix/`*
    - followed by `SZD-` and a single or multiple digits
    - *(optional) `_` and lowercase text with dashes*
- **Conventional commits regex**: `^(build|chore|ci|docs|feat|fix|perf|refactor|revert|style|test){1}(\([\w\-\.]+\))?(!)?: ([\w ])+`
![regexper](https://regexper.com/#%5E%28build%7Cchore%7Cci%7Cdocs%7Cfeat%7Cfix%7Cperf%7Crefactor%7Crevert%7Cstyle%7Ctest%29%7B1%7D%28%5C%28%5B%5Cw%5C-%5C.%5D%2B%5C%29%29%3F%28!%29%3F%3A%20%28%5B%5Cw%20%5D%29%2B)

## TODO:

- [Validate branch naming](https://itnext.io/using-git-hooks-to-enforce-branch-naming-policy-ffd81fa01e5e)
- Validate if commit message obeys "conventional commits" rules
- Add [Jira code] to the beginning of commit msg
