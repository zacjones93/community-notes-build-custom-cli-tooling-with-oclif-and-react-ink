# Preworkshop notes

Notes taken on: [12 Factor CLI Apps](https://medium.com/@jdxcode/12-factor-cli-apps-dd3c227a0e46)

## 01. Great help is essential

all these commands should work in a cli for help

oclif gives this to you for free
```bash
# list all commands
$ mycli
$ mycli --help
$ mycli help
$ mycli -h
# get help for subcommand
$ mycli subcommand --help
$ mycli subcommand -h
```

## 02. Prefer flags to args

Flags require a bit more typing, but make the CLI much clearer.

Initially, this used a flag and an argument like this:

    $ heroku fork FROMAPP --app TOAPP

Using a flag and an arg, it was really confusing which was the source and which was the destination app. We changed this to use flags for both:

    $ heroku fork --from FROMAPP --to TOAPP

The second is much clearer what is happening

**A good rule of thumb is 1 type of argument is fine, 2 types are very suspect, and 3 are never good.**

multiple arguments are fine but when they are different types, that's when you get into issues

Flags are also much easier to write autocomplete logic for as you know exactly what the value should be.

## 3. What version am I on?

    $ mycli version # multi only
    $ mycli --version
    $ mycli -V

## 4. Mind the streams

stdout would not only hide the warning, but it would be especially problematic for structured data like JSON or binary.

Use stderr for errors and warnings which by default will always end up on the screen even if stdout is redirected.

**Not everything on stderr is an error though.** For example, you can use curl to download a file but the progress output is on stderr. This allows you to redirect the stdout while still seeing the progress.

**In short: stdout is for output, stderr is for messaging.**

## 5. Handle things going wrong

make your errors informative. A great error message should contain the following:

1. Error code
2. Error title
3. Error description (Optional)
4. How to fix the error
5. URL for more information

In oclif we use the [debug](https://www.npmjs.com/package/debug) module which allows us to output debug statements grouped by component if the DEBUG environment variable is set. We have a lot of verbose logging if debug is fully enabled which is incredibly valuable to us when debugging issues.

## 6. Be fancy!

## 7. Prompt if you can

[TODO]
