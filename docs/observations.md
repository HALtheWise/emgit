This file contains things I've learned about the behavior of systems the emgit system interacts  with.

# git

- The vast majority of the size associated with the .git folder comes from the contents of the `objects` subfolder. 
- If the `objects` folder does not exists, `git` fails to recognize that the folder is a git repository at all, even if `.git` is otherwise intact.
- If the `objects` folder is empty, `git fetch` will throw errors, but then successfully rebuild its contents (to the extent possible) from a remote  repository that has the requisite data. 
- Removing files in `refs/remotes` is often corrected by `git fetch`, but doesn't reliably completely cure itself, and seems to not provide any meaningful benefits.



# [rclone](http://rclone.org/)

- [filter-from](http://rclone.org/filtering/#filter-from-read-filtering-patterns-from-a-file) enables powerful filtering by regexes, but needs a separate file to read the commands from.
- [max-age](http://rclone.org/filtering/#max-age-don-t-transfer-any-file-older-than-this) could be an interesting automatic filter, but doesn't allow for folder-level filtering because rclone doesn't understand  the concept of folder modification times. Perhaps this is an interesting option for folders that are old and nominally wouldn't be synched at all?
- By default, the configuration file is stored and loaded from `/home/eric/.rclone.conf`, but that can be changed with the command line `--config [path]`
- `rclone lsd` is a useful way to list subdirectories
- The output of rclone run with a `--dry-run` flag is machine-parseable to check what a command will do before it runs. This could be useful to auto-abort in cases where mass deletions could occur.

--------

- Files excluded through -exclude rules won't get deleted (the rule is applied to their identity in dest).














