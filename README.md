This script guesses the numbers for the merged pull requests 
from the last tag, then fetches the corresponding information 
from GitHub and formats it into markdown format suitable for 
use in e.g. Discourse.

You should invoke this script from the toplevel folder of your repo, and
redirect the output to a file, or copy/paste the output as required:
```
$ python fetch_changelog > changelog.md
```

## What it does

This script relies on `git` to detect your currently checked-out branch, its
upstream remote, the URL of that remote, and verifies that it matches
'github.com' (it is designed to fetch the issue list from GitHub using its API,
and will not work with other git hosting providers). 

It will then find the most recent signed tag on that branch, and find all merge
commits that start with 'Merge pull request #'. It will extract the pull
request number from these commit messages, and then use the GitHub API to fetch
the JSON entries for each of these pull requests, from which it will extract
the title, user and body of the pull request, which will be printed on `stdout`
in markdown.

## Command-line options

- `--tag=XX`:
  Override the automatic detection of the base tag, and specify it manually.
  The script will then fetch all pull requests that have been merged *after*
  that tag.

- `--no-fetch`:
  Report all pull request IDs detected, but do not use the GitHub API to fetch
  any further information. This is useful for testing, to avoid hitting GitHub
  API rate limits.

## GitHub Authentication

If necessary (for example, if your repo is private, or you encounter issues with
rate limiting), you can provide GitHub authentication information in your own
`fetch_changelog_settings` file, which should be created in the toplevel of
your repo folder, with the correct information:
```
user = 'jdtournier'
password = 'gngkasgndfgknldsafnfknxgkjd'
```
where `password` above should contain your personal authentication token, as
[generated from your GitHub acccount](https://github.com/settings/tokens). 

