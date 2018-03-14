This script guesses the numbers for the merged pull requests 
from the last tag, then fetches the corresponding information 
from GitHub and formats it into markdown format suitable for 
use in e.g. Discourse.

To use, please add create a 'fetch_changelog_settings' file 
in the toplevel of your repo folder, with the correct information:
```
repo = 'MRtrix3/mrtrix3'
user = 'jdtournier'
password = 'gngkasgndfgknldsafnfknxgkjd'
```
where `password` above should contain your personal authentication token, as [generated from your GitHub acccount](https://github.com/settings/tokens). 

You can then invoke this script from the toplevel folder of your 
repo, and redirect the output to a file, or copy/paste the output 
as required:
```
$ python fetch_changelog > changelog.md
```
