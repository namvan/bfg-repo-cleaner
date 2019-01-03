BFG Repo-Cleaner [![Build Status](https://travis-ci.org/rtyley/bfg-repo-cleaner.svg?branch=master)](https://travis-ci.org/rtyley/bfg-repo-cleaner)
================

_Removes large or troublesome blobs like git-filter-branch does, but faster - and written in Scala_ - [Fund the BFG](https://j.mp/fund-bfg)

```
$ bfg --strip-blobs-bigger-than 1M --replace-text banned.txt repo.git
```

The BFG is a simpler, faster ([10 - 720x](https://docs.google.com/spreadsheet/ccc?key=0AsR1d5Zpes8HdER3VGU1a3dOcmVHMmtzT2dsS2xNenc) faster)
alternative to `git-filter-branch` for cleansing bad data out of your Git repository:

* Removing **Crazy Big Files**
* Removing **Passwords, Credentials** & other **Private data**

Main documentation for The BFG is here : **https://rtyley.github.io/bfg-repo-cleaner/**

**Usage Summary**

````
java -jar bfg.jar [options] [<repo>]

  -b, --strip-blobs-bigger-than <size>
                           strip blobs bigger than X (eg '128K', '1M', etc)
						   
  -B, --strip-biggest-blobs NUM
                           strip the top NUM biggest blobs
						   
  -bi, --strip-blobs-with-ids <blob-ids-file>
                           strip blobs with the specified Git object ids
						   
  -D, --delete-files <glob>
                           delete files with the specified names (eg '*.class', '*.{txt,log}' - matches on file name, not path within repo)
						   
  --delete-folders <glob>  delete folders with the specified names (eg '.svn', '*-tmp' - matches on folder name, not path within repo)
  
  --convert-to-git-lfs <value>
                           extract files with the specified names (eg '*.zip' or '*.mp4') into Git LFS
						   
  -rt, --replace-text <expressions-file>
                           filter content of files, replacing matched text. 
                           Match expressions should be listed in the file, one expression per line 
                           By default, each expression is treated as a literal, 
                            but 'regex:' & 'glob:' prefixes are supported, 
                            with '==>' to specify a replacement string other than the default of '***REMOVED***'.
							 
  -fi, --filter-content-including <glob>
                           do file-content filtering on files that match the specified expression (eg '*.{txt,properties}')
						   
  -fe, --filter-content-excluding <glob>
                           don't do file-content filtering on files that match the specified expression (eg '*.{xml,pdf}')
						   
  -fs, --filter-content-size-threshold <size>
                           only do file-content filtering on files smaller than <size> (default is 1048576 bytes)
						   
  -p, --protect-blobs-from <refs>
                           protect blobs that appear in the most recent versions of the specified refs (default is 'HEAD')
						   
  --no-blob-protection     allow the BFG to modify even your *latest* commit. Not recommended: you should have already ensured your latest commit is clean.
  
  --private                treat this repo-rewrite as removing private data (for example: omit old commit ids from commit messages)
  
  --massive-non-file-objects-sized-up-to <size>
                           increase memory usage to handle over-size Commits, Tags, and Trees that are up to X in size (eg '10M')
						   
  <repo>                   file path for Git repository to clean
```
