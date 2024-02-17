
# About
This project contains filter templates for Duplicacy.

At the moment, I have only included a filter for Linux, which is suitable for both server and desktop environments.

# Usage


## linux-filters
This filter assumes that you have set Duplicacy's storage to the home directory.

Read through file's comments and adjust/remove/add lines according to the instructions and/or hints left behind.

### Filtering Sequence

The sequence these patterns are applied are predictable, since Duplicacy applies them from top to bottom. See below for the approach that this template follows, they are applied from top to bottom.


#### Universal Exclusions

These are exclusions (reachable from your home directory) that should be always be excluded from backups. These patterns are placed at the top since they should be excluded before everything else.

1. Exclude Obvious Cache Folders


#### Hidden Files and Hidden Folders

1. Exclude Additional Cache found in .config:
    - Some programs use .config to store their cache files.
    - In some cases, these programs do not respect their own cache naming conventions and sometimes place them top level.
2. Include Remaining Contents in .config
3. Include Specific Hidden Files and Folders
    - These patterns are simple enough to just copy + paste or modify at will.
4. Include Hidden Files and Folders using Complex Patterns
    - These lines have more complex patterns.
    - You may not need these for your use case.
    - If you do, refer to Duplicacy's documentation on filtering patterns for reference
5. Exclude Remaining Hidden Files and Folders Not Included in the Earlier Steps.

#### Non-hidden Files and Non-Hidden Folders

1. Exclude Specific Non-hidden Files and Folders
    - These patterns are simple enough to just copy + paste or modify at will.
2. Exclude Non-Hidden Files and Folders using Complex Patterns
    - These lines have more complex patterns.
    - You may not need these for your use case.
    - If you do, refer to Duplicacy's documentation on filtering patterns for reference
3. Include Remaining Non-Hidden Files and Folders Not Included in the Earlier Steps.

### Notes on Exclusion / Inclusion Sequence

After reading through the sequence you might have noticed that hidden folders/files and non-hidden folders/files are handled in an opposing way to each other:

Hidden files/folders require the user to specify contents to include. If anything is not specified, it will be excluded.

On the contrary: Non-hidden files/folders require the user to specify contents to exclude. If anything is not specified, it will be included.


The reasoning for the hidden file/folder approach is simple:
Hidden folders and files (from the home folder) are typically created by applications. There is a risk that you may unknowingly backup contents large in size that do not need to be backed up. Therefore, this approach mitigates that risk since the user must investigate which of these files/folders they'd like to backup at the same time that they install a package. If there isn't anything new to backup, they do not have to modify the filter file; it will be excluded automatically. If they do find something new they'd like to backup, then they must add a line to the appropriate block of the filtering sequence; it will then be included.

The reasoning for the non-hidden file/folder approach is simple:
Non-hidden folders and files (from the home folder) are typically created by the user. Since the user has knowledge of the contents that they manually create, they can simultaneously decide if a particular folder/file is suitable for backups. If they are suitable, they do not have to modify the filter file; it will be included automatically. If they aren't, then they must add a line to the appropriate block of the filtering sequence; it will then be excluded.
