# Practical git hooks

## Resources

### Branch regex

`^(feature\/|bugfix\/|release\/|hotfix\/){0,1}(SZD-\d+)(_[a-z-]+)?$`
- *(optional) starts with `feature/`, `bugfix/`, `release/`, or `hotfix/`*
- followed by `SZD-` and a single or multiple digits
- *(optional) `_` and lowercase text with dashes*

### Conventional commits regex

`^(build|chore|ci|docs|feat|fix|perf|refactor|revert|style|test){1}(\([\w]+\))?(!)?: [\w ,()]+`
- one of the given categories
- *(optional) a word in parentheses*
- *(optional) `!`*
- `: `
- multiple words

### Final commit msg regex:

`^\[SZD-\d+\] (build|chore|ci|docs|feat|fix|perf|refactor|revert|style|test){1}(\([\w]+\))?(!)?: [\w ,()]+`
- same as commit message, but has SZD-number prepended

### Git hook order

1. pre-commit
2. prepare-commit-msg
3. commit-msg
4. post-commit
5. pre-push

## Hooks

### Run PHPCS (or anything else for code quality)

Should be run pre-commit in order to prevent faulty code to be committed to the repository.

```bash
#!/bin/sh

# Run the built-in phpcs script in order the prevent committing wrongly styled code

composer phpcs
exit $?
```

### Add [Jira code] from branch to the beginning of commit msg

Must be done in prepare-commit-msg.

```bash
#!/bin/sh

# Get the name of the current branch by matching the second group of the regex

regex="^(feature/|bugfix/|release/|hotfix/)?(LP-[0-9]+)(_[a-z-]+)?$"
local_branch="$(git rev-parse --abbrev-ref HEAD)"

if [[ $local_branch =~ $regex ]]; then
    issue="${BASH_REMATCH[2]}"
else
    echo "Failed to fetch issue from branch name"
    exit 1
fi

# Prepend the [issue key] to the commit message

commit_msg_file="$1"
if [ -f "$commit_msg_file" ] && [ -n "$issue" ]; then
    tmp_file=$(mktemp)
    echo "[$issue] $(cat "$commit_msg_file")" > "$tmp_file"
    mv "$tmp_file" "$commit_msg_file"
else
    echo "Commit message or Jira issue not found"
    exit 1
fi

```

### Validate if commit message obeys "conventional commits" rules

Must be done in commit-msg.

```bash
#!/bin/sh

# Check if the commit message matches the required format:
#   - (prepended automatically) [LP-number]
#   - conventional category of the commit
#   - (optional) name of the changed component in parentheses
#   - (optional) exclamation mark to indicate breaking change
#   - a colon and a space
#   - a message containing letters (upper- or lowercase), numbers, commas, dots, parentheses

regex="^\[LP-[0-9]+\] (build|chore|ci|docs|feat|fix|perf|refactor|revert|style|test)(\([^\)]+\))?(!)?: [A-Za-z0-9 ,.()]+$"
commit_msg_file="$1"
commit_msg=$(cat "$commit_msg_file")

if ! [[ $commit_msg =~ $regex ]]; then
    echo "Commit message does not match the required pattern:"
    echo "Pattern: $regex"
    echo "Commit message: $commit_msg"
    exit 1
fi
exit 0
```

### Validate branch naming

Should be pre-push to prevent the pushing of a wrongly named branch to remote.

```bash
#!/bin/sh

# Verify if branch name is standard:
#   - (optional) type/
#   - LP-number
#   - (optional) _comma-separated-description

local_branch="$(git rev-parse --abbrev-ref HEAD)"
valid_branch_regex="^(feature/|bugfix/|release/|hotfix/)?(LP-[0-9]+)(_[a-z-]+)?$"
if [[ ! $local_branch =~ $valid_branch_regex ]]
then
    echo "Something is wrong with you branch name."
    echo "It should match the regex: $valid_branch_regex"
    echo "But it's value is: $local_branch"
    exit 1
fi
exit 0
```
