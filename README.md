# CLI Utilities

This is a CLI Utilities library for Node.js.

Time spent: `<Number of hours spent>`

## Features

### Required

- [x] Completed Requireds marked with `[x]`
- [ ] Walkthrough Gif embedded in README
- [ ] README `Time spent:` includes the number of hours spent on the assignment
- [ ] `echo.js` prints the first argument to stdout
- [ ] `cat.js` prints the contents of the first argument to stdout
- [ ] `touch.js` updates the modified date of the first argument
- [ ] `ls.js` recursively lists the files of the first argument
- [ ] `mkdir.js` create a directory at the first argument
- [ ] `rm.js` deletes any file or directory at the first argument 

### Optionals

- [ ] `ln.js` creates a symlink from the second argument to the first argument
- [ ] `grep.js` prints lines matching the first argument in the files matching the second argument
- [ ] `grep.js` supports a regex as the second arguments

## Walkthrough Gif:

`<Add your Walkthrough Gif here (by updating the image URL)>`
![Video Walkthrough](...)


## Unit 1 Project: CLI Utilities

##### CLI Utilities Demo

<img src="http://i.imgur.com/jtuHHa3.gif" title='CLI Utilities Demo' width='' alt='CLI Utilities Demo' />>

### Overview

For our first assignment, we're going to keep things simple by building a collection of common filesystem CLIs to familiarize ourselves with node.js' runtime, module system and ascyhronous APIs.

Implement each of the following in node.js using only core APIs (**No packages allowed!**):

0. [`echo`](http://www.openbsd.org/cgi-bin/man.cgi?query=echo&apropos=0&sec=0&arch=i386&manpath=OpenBSD-current)
0. [`cat`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/cat.1?query=cat&arch=i386)
0. [`touch`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/touch.1?query=touch&arch=i386)
0. [`ls`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/ls.1?query=ls&arch=i386)
0. [`mkdir`](http://www.openbsd.org/cgi-bin/man.cgi?query=mkdir&apropos=0&sektion=0&manpath=OpenBSD+Current&arch=i386&format=html)
0. [`rm`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/rm.1?query=rm&arch=i386)
0. *Optional:* [`ln`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/ln.1?query=ln&arch=i386)
0. *Optional:* [`grep`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/egrep.1?query=grep&arch=i386)

#### Getting Started

Get started by cloning the [`nodejs-clis`](https://github.com/CrabDude/nodejs-clis/) starter project:

```bash
$ git clone git@github.com:CrabDude/nodejs-clis.git clis
```

*Note: [`README.md`](https://github.com/CrabDude/nodejs-clis/README.md) contains the list of required features for completion. Check tasks off as you complete them.*

**Walkthrough:** Check out the [video walkthrough](http://vimeo.com/crabdude/cli) for this project to get you started.

**Questions?** We're listening. Submit an Issue.

#### Submission Instructions

**IMPORTANT: Follow the [[Submitting Assignments]] guide to submit the assignment.** 

**Completed submissions must include the following in `README.md`:**

  1. An embedded animateed `walkthrough.gif` demoing the required functionality
  2. Time Spent (hours)
  3. Checkmarks next to all completed functionality (All "Required"s need to be checked)

<hr>

### Precursor: Creating A Node.js Executables

All of the utilities in this assignment will need to be executable. For example:

```bash
$ echo 'hello world'            # This is the built-in 'echo' command
hello world
$ ./echo.js 'hello world'       # A node.js script with the same functionality
```

To make a node.js / JavaScript file executable (skip for Windows):

1. Mark the file as executable:
    
    ```bash
    $ chmod +x ./echo.js
    ```

2. Add a [shebang](http://dailyjs.com/2012/03/01/unix-node-arguments/) by appending the following to the top of the file (e.g., `echo.js`):
    
    ```node
    #!/usr/bin/env babel-node
    // ... Echo code here
    ```

### CLI command files

#### 0. Setup

For each of the assignment CLIs:

1. Create a separate file with the corresponding name (e.g., the provided `echo.js`)
1. **IMPORTANT:** Require `helper.js` just below the shebang:

    ```node
    #!/usr/bin/env babel-node
    require('./helper')
    ```
1. Declare an async function containing your implementation, and invoke it:

    ```node
    async function echo() {
        // Use 'await' in here
        // Your implementation here
    }
    echo()
    ```
1. Add an entry in `package.json` [`"scripts"`](https://docs.npmjs.com/misc/scripts) for the CLI:

    ```js
    {
        "scripts": {
            "cli:echo": "node echo.js"
        }
    }
    ```

**Summary:** Your files should all generally look like this:

```node
#!/usr/bin/env babel-node

require('./helper')
let fs = require('fs').promise

async function echo() {
    // Use 'await' in here
    // Your implementation here
}

echo()
```

And should be runnable:

```bash
# Non-windows
$ ./echo.js

# Windows
$ node echo.js

# Both
$ npm run cli:echo --
```

#### 1. [`echo`](http://www.openbsd.org/cgi-bin/man.cgi?query=echo&apropos=0&sec=0&arch=i386&manpath=OpenBSD-current)

Create an executable file, `echo.js`, that prints the first argument to `process.stdout`:

```bash
$ ./echo 'hello world'
hello world

$ ./echo 'node is fun'
node is fun
```

**IMPORTANT:** Passing arguments via [`npm run`](https://docs.npmjs.com/cli/run-script#description) requires the `--` delimiter:

```bash
$ npm run echo -- 'hello world'
```

#### 2. [`cat`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/cat.1?query=cat&arch=i386)

Create an executable file, `cat.js`, that prints to `process.stdout` the contents of the file path passed on the first argument:

```bash
$ cat ./helloworld.txt    # These outputs should be the same
hello world

$ ./cat ./helloworld.txt  # These outputs should be the same
hello world
```

#### 3. [`touch`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/touch.1?query=touch&arch=i386)

Create an executable file, `touch.js`, that updates the modified date of the file path passed on the first argument:

```bash
$ ls -la
total 0
drwxr-xr-x  3 user      wheel  102 Jan  4 18:43 .
drwxrwxrwt  8 root      wheel  272 Jan  4 18:43 ..
-rw-r--r--  1 user      wheel    0 Jan  1 12:58 touch.js

$ ./touch.js touch.js

$ ls -la
total 0
drwxr-xr-x  3 user      wheel  102 Jan  4 18:44 .
drwxrwxrwt  8 root      wheel  272 Jan  4 18:44 ..
-rw-r--r--  1 user      wheel    0 Jan  4 18:44 touch.js
```

*Note:* The modified date in the last line above has been updated.

*Hint: Use the `mtime` argument in [`fs.futimes(fd, atime, mtime, callback)`](https://nodejs.org/docs/latest/api/all.html#all_fs_futimes_fd_atime_mtime_callback).*

#### 4. [`ls`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/ls.1?query=ls&arch=i386)

1. Create an executable file, `ls.js`, that lists the files in a directory passed on the first argument:

    ```bash
    $ ./ls.js ./
    ls.js
    someDir
    ```
1. Omit directories:

    ```bash
    $ ./ls.js ./
    ls.js
    ```
1. Add a recursive option, `-R`:

    ```bash
    $ ./ls.js ./              # Parent directory w/o -R
    ls.js

    $ ./ls.js ./someDir       # Sub-directory w/o -R
    foo.js
    bar.js

    $ ./ls.js ./ -R           # Parent directory with -R
    ls.js
    someDir/foo.js
    someDir/bar.js
    ```

#### 5. [`mkdir`](http://www.openbsd.org/cgi-bin/man.cgi?query=mkdir&apropos=0&sektion=0&manpath=OpenBSD+Current&arch=i386&format=html)

1. Create an executable file, `mkdir.js`, that creates a directory at the path passed on the first argument:

    ```bash
    $ ls ./                       # Note someDir does not exist
    rm.js

    $ ./mkdir.js ./someDir        # Create someDir

    $ ls ./                       # Note someDir exist
    rm.js
    someDir
    ```
    *Hint: Use [`String.prototype.split`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) to split the argument on `/` and iteratively use [`fs.mkdir`](https://nodejs.org/docs/latest/api/all.html#all_fs_mkdir_path_mode_callback).*
1. *Optional:* Add recursive functionality:

    ```bash
    $ ls ./                           # Note foo does not exist
    rm.js

    $ ./mkdir.js ./foo/bar/someDir    # Create someDir

    $ ls ./                           # Note foo exist
    rm.js
    foo

    $ ls ./foo                        # Note bar exist
    bar

    $ ls ./foo/bar                    # Note someDir exist
    someDir
    ```

#### 6. [`rm`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/rm.1?query=rm&arch=i386)

Create an executable file, `rm.js`, that deletes the file or directory of the file path passed on the first argument:

**File Example:**

```bash
$ ls ./                       # Note helloworld.txt exists
rm.js
helloworld.txt

$ ./rm.js ./helloworld.txt    # Delete helloworld.txt

$ ls ./                       # Note helloworld.txt has been deleted
rm.js
```

**Directory Example:**

```bash
$ ls ./                       # Note someDir exists
rm.js
someDir

$ ./rm.js ./someDir           # Delete someDir

$ ls ./                       # Note someDir has been deleted
rm.js
```

*Hint: Use your recursive `ls.js` implementation and [`fs.unlink`](https://nodejs.org/docs/latest/api/all.html#all_fs_unlink_path_callback) to delete files first, then delete all the directories.*

#### 7. Install your CLIs globally

Packages installed globally with `npm` using the `-g` flag, expose executables from the package on your system `$PATH`.

1. Expose your scripts globally by adding them to the `package.json` `"bin"` key:

    ```json
    {
        "name": "clis",
        "bin": {
            "cli-echo": "./echo.js
        }

    }
    ```
    **IMPORTANT:** Prepend the `"bin"` keys with something (e.g., `cli-`) to avoid overriding your system's `echo`, `ls`, etc...
1. And installing (or linking) your package globally:

    ```bash
    clis-dir$ npm link                  # By symlinking, or...
    clis-dir$ npm install -g            # By copying
    ```
1. Verify your scripts are now globally executable:

    ```bash
    $ cli-echo 'I know node.js!'        # Note, use 'cli-echo' instead of './echo.js'
    I know node.js!
    ```

#### 8. *Optional:* [`ln`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/ln.1?query=ln&arch=i386)

1. Create an executable file, `ls.js`, that creates a symbolic link to the path passed on the first argument to the path passed on the second argument:

    ```bash
    $ ln ln.js foo.js             # Creates a symlink to 'ln.js' called 'foo.js'

    $ ./ln.js ln.js foo.js        # Creates a symlink to 'ln.js' called 'foo.js'
    ```

#### 9. *Optional:* [`grep`](http://linuxcommand.org/man_pages/grep1.html)

1. Create an executable file, `grep.js`, that .......:

    ```bash
    $ grep require grep.js        # Print all lines containing 'require' in grep.js
    let fs = require('fs').promise

    $ ./grep.js require grep.js   # Print all lines containing 'require' in grep.js
    let fs = require('fs').promise
    ```
    *BONUS:* Allow the last argument to be a Regex instead that matches on file paths relative to `pwd`.

### Walkthrough Video

You can watch the video below to get started with the basic implementation which should leave you with more time to explore the optional features.

- [CLI Utilities Walkthrough Video](http://vimeo.com/crabdude/cli) - Covers the Virtual Filesystem APIs (`ls`, `touch`, `mkdir`, `cat`) portion of the CLI APIs.

### Guides

- [Filesystem API](https://github.com/crabdude/nodejs_wiki/wiki/Filesystem)
- [Control-flow](https://github.com/crabdude/nodejs_wiki/wiki/Control-flow)
- [Command-Line Interfaces](https://github.com/crabdude/nodejs_wiki/wiki/CLI)
- [Streams](https://github.com/crabdude/nodejs_wiki/wiki/Streams)

### References

- [`echo`](http://www.openbsd.org/cgi-bin/man.cgi?query=echo&apropos=0&sec=0&arch=i386&manpath=OpenBSD-current)
- [`cat`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/cat.1?query=cat&arch=i386)
- [`touch`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/touch.1?query=touch&arch=i386)
- [`ls`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/ls.1?query=ls&arch=i386)
- [`mkdir`](http://www.openbsd.org/cgi-bin/man.cgi?query=mkdir&apropos=0&sektion=0&manpath=OpenBSD+Current&arch=i386&format=html)
- [`rm`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/rm.1?query=rm&arch=i386)
- [`ln`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/ln.1?query=ln&arch=i386)
- [`grep`](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/egrep.1?query=grep&arch=i386)
