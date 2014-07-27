# lslock
## An interesting problem to solve

It can be useful to know what files in a directory tree are currently locked by a process, and which process that is.

Thankfully, linux provides the /proc/locks pseudo-file, that can give us this information

## The code

### `lslock_test`
This little guy will create some files and lock them for you, so you have something to inspect (in case you don't have another daemon or process creating locks).
`lslock_test` has a few optional arguments:

```
#> lslock_test -h
sage: lslock_test <arguments>

Optional Arguments:
    -d, --directory <path>           the directory to create locks in, will be created if it does not exist (default: /tmp/lslock-test)
    -n, --numlocks <integer>         number of locks to create (default: 10)
    -s, --seconds <integer>          number of seconds to hold locks for (default: 30)
```

### `lslock`
`lslock` checks for the existence of locked files in a directory, and lists them for you, along with pid of the locking process.

`lslock` has a single optional argument, as seen in it's help:

```
#> lslock -h
Usage: lslock <arguments>
    Expected Output: a space delimited list of pids and files
    No output means there are no locked files in the specified directory

Optional Arguments:
    -d, --directory <path>           the path to look for locked files in (default: /tmp/lslock-test)
```

## Installation
Using your favorite ruby provider (rvm, rbenv, chruby, etc), make sure that you have a compatible version of ruby; I've used ruby-2.1.2 via rvm.
You'll also need the `gem` command.

If you plan on using lslock_test, you'll need some gems, listed in the Gemfile.

```
gem install bundle
bundle install
```
