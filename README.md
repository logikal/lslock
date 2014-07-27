# lslock
## An interesting problem to solve

It can be useful to know what files in a directory tree are currently locked by a process, and which process that is.

Thankfully, linux provides the /proc/locks pseudo-file, that can give us this information

## The code

### `lslock_test`
#### running
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

#### Expected output
`lslock_test` will show the following output, and then ve silent for 30 seconds (default)
```
#> lslock_test
24156  /tmp/lslock-test/joyful-fog-9532
24159  /tmp/lslock-test/teal-tsunami-2465
24163  /tmp/lslock-test/juicy-storm-7609
24167  /tmp/lslock-test/harmonious-pine-7988
24171  /tmp/lslock-test/outrageous-crater-6549
24175  /tmp/lslock-test/homeless-spring-409
24179  /tmp/lslock-test/wooden-smokescreen-7757
24183  /tmp/lslock-test/tasteless-farm-468
24187  /tmp/lslock-test/snowy-volcano-3880
24191  /tmp/lslock-test/pleasant-lake-3438
```

### `lslock`
#### Running
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

#### Expected output
`lslock` will output something similar to the following:
```
24156 /tmp/lslock-test/joyful-fog-9532
24159 /tmp/lslock-test/teal-tsunami-2465
24163 /tmp/lslock-test/juicy-storm-7609
24167 /tmp/lslock-test/harmonious-pine-7988
24171 /tmp/lslock-test/outrageous-crater-6549
24175 /tmp/lslock-test/homeless-spring-409
24179 /tmp/lslock-test/wooden-smokescreen-7757
24183 /tmp/lslock-test/tasteless-farm-468
24187 /tmp/lslock-test/snowy-volcano-3880
24191 /tmp/lslock-test/pleasant-lake-3438
```

If you're running `lslock_test` while running `lslock`, you should expect the output to be the same.

## Installation
Using your favorite ruby provider (rvm, rbenv, chruby, etc), make sure that you have a compatible version of ruby; I've used ruby-2.1.2 via rvm.
You'll also need the `gem` command.

If you plan on using lslock_test, you'll need some gems, listed in the Gemfile.

```
gem install bundle
bundle install
```
