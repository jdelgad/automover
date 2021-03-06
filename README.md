Automover tries to figure out what show, season, and episode a file represents. It them renames the file as "Show S01E02 Episode Title.avi" and moves it to a configurable destination. To help figure out the title of the show, Automover uses the destination path as a dictionary and checks which folder most closely matches the filename.

By default, Automover will search subdirectories of `searchpath` for files matching a configurable pattern, and try to auto-move them. It can also run in "stdin mode" where it will read a list of file names from stdin by passing the `--read` flag. See below for examples. 

---

    usage: automover.py [-h] [--conf CONF] [--read] [--script [SCRIPT]]
                        [--verbose] [--hint HINT [HINT ...]]
                        searchpath
    
    Automatically rename and move TV shows
    
    positional arguments:
      searchpath            The file or directory to process
    
    optional arguments:
      -h, --help            show this help message and exit
      --conf CONF           Path to the config file
      --read                Take filenames from STDIN
      --script [SCRIPT]     Write a bash script
      --verbose             Verbose output
      --hint HINT [HINT ...]
                            Give a hint to the file name, if it isn't in the
                            destination location.
    
---

**Examples:**

    $ automover . --verbose --script move.sh
    $ sh move.sh
---
    $ find . -iname "Arrested Development*.avi" -not -iname "*sample*" | \
    automover --script move.sh --read --hint Arrested Development
    $ sh move.sh

**Make sure to check move.sh for errors before running it!**

---

**Future plans:**

* Output an 'undo' script that unmoves the object.
* ~~Check that we're not overwriting any destination files, and if so, utter a warning and back it up.~~ Done! Using mv -vb
* ~~Handle formats like modern.family.302.hdtv.xvid-lol.avi~~ Done!

