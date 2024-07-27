# Vendor (firmware) for OnePlus 7T Pro (hotdog)

The OnePlus 7T Pro (codenamed _"hotdog"_) is a flagship smartphone from OnePlus.
It was released in October 2019. Official support for the device ended in 2023 with Android 12.

---

## Information on the repository

**Pre-installation:**

The repository includes common vendor files plus radio firmware files from the latest OOS12 version (International variant) and requires Git-LFS (Large File System) to download the firmware image files porperly!

`git lfs install`does two things, when invokes in the directory path of the repository (mandatory):

1. it sets up hooks in your local repository,
2. it adjusts your global (i.e., user-specific) configuration to contain the filter commands necessary for Git LFS to work properly.

If you're not in a repository yet, you probably want to execute `git lfs install --skip-repo` and let it install the filter commands into your *~/.gitconfig*.

Afterwards move into a non-Git-controlled directory and execute `git lfs env` and make sure that the last few lines look like this:

`git config filter.lfs.process = "git-lfs filter-process"`
`git config filter.lfs.smudge = "git-lfs smudge -- %f"`
`git config filter.lfs.clean = "git-lfs clean -- %f"`

That will show you that your configuration is set up properly.



Once you have that set up, simply re-sync the repository using by creating a simple bash-script that walks the Android tree and only pulls & syncs files from Git LFS repositorythis in the main directory of your working tree:

```
#!/bin/bash
# Walk the entire tree starting at $PWD and find all directories
# containing `.gitattributes` file that says it's a Git clone
# directory that uses Git-LFS. For each such directory, do `git lfs
# pull`.
grep -l 'merge=lfs' $( find (find$PWD -name .gitattributes ) /dev/null | while IFS= read -r line; do
dir=$(dirname (dirname$line)
echo $dir
( cd dir(cd$dir ; git lfs pull )
done
```

If you want, you can save this script to something like "repo-lfs.sh" and make it executable for convenience reasons, as the command should be executed on every repo sync.
As the device is EOL re-syncing firmware files might be obsolete as these files might not change anymore.
