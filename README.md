# actions-pr-checker
Github Action to check PR description is valid.

Validation strings are regular expressions. Don't forget to escape special chars.

## Quick start:
```yml
      - name: Run check
        uses: transferwise/actions-pr-checker@v2
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          PR_NOT_CONTAINS_PATTERN: 'Why is this PR necessary?'
          PR_COMMENT: 'Please check description. \nShould be meaningful and not empty.'
```

## Parameters
| Name | Description | Default | Required |
|------|-------------|---------|:--------:|
|GITHUB_TOKEN | github bot token | | yes |
|PR_CONTAINS_PATTERN | Regexp to validate PR body | `.*` | no
|PR_NOT_CONTAINS_PATTERN | Regexp to validate PR body | `pseudo-long-string-constant` | |
|PR_TITLE_CONTAINS_PATTERN | Regexp to validate PR title | `.*` | no
|PR_TITLE_NOT_CONTAINS_PATTERN | Regexp to validate PR title | `pseudo-long-string-constant` | | 
|PR_COMMENT | Comment to add, if validation not passing| `Please check description. \nShould be meaningful and not empty.` | |
|SUCCESS_EMOJI | Reaction to PR if check success. Possible: `+1` `-1` `laugh` `confused` `heart` `hooray` `rocket` `eyes` (ref: https://developer.github.com/v3/reactions/#reaction-types) | `+1` |  |
|SUCCESS_APPROVES_PR | Approve PR when check pass. If set to `false` won't request changes, but add comments instead | true | |
|FAIL_CLOSES_PR | Close PR in case of check fails | false | |
|FAIL_EXITS | Fail the check if validation not passing. Use `false` if you want comment, but mark as check as success | true | |


## More examples
PR title complies with convention
```yml
      - name: Check PR title
        uses: transferwise/actions-pr-checker@v2
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          PR_TITLE_CONTAINS_PATTERN: '.*(\\w{3})-([0-9]+).+[^.]$'
          PR_COMMENT: 'Please check PR title. \nShould follow https://namingconvention.org/git/pull-request-naming.html.'
```
