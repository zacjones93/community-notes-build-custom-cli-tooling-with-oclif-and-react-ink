CLI's are the guard rails for making the script underneath computable with humans

CLIs should provide documentation for you

anything boilerplately or repetitive is a good candidate for a CLI

## 00 Why even

"Here's a thing that I learned at FB that I wish I knew much earlier. Invest in building custom tools! It can be a script you could write in a day. And at small and medium companies, even a little effort can yield a huge return."

There is a trade off of productivity in building the CLI and just doing the thing over and over

if you spend a minute to do the task every day - some say you should spend a day automating the task

`gatsby-theme` cli - scaffolds out component shadowing for you instead of you doing the task manual.

It's not just about staying in the terminal, it is also an opportunity to **provide guard rails for your users so they spend less time futzing around your docs** and more time just getting productive.

oclif and commander (this is the oldests) are the two biggest frameworks for clis

CLIs are everywhere. Even if you don't build them, you'll use them and those will have bugs - you might want to put in a PR

There is no CLI spec but there are some design patterns that existing CLI's adhere to.

There we're a plethora of memes that came out in 2016 about how hard it was to even get started with React because of all the config. CRA fixed all of this.

## CLI Basics

### 01 CLI intro

`github-email` is a simple cli that will grab someones email from their github account

`z` move around recent directories

build a business card in a cli

`npx swyx`

[https://github.com/bnb/bitandbang](https://github.com/bnb/bitandbang)

`main` is a typical field. it's where the module will require from

`bin` is what is required and where it will be required

so

// left hand is name you'll use to invoke
// right hand side is where it will be invoked

    "bin": {

    	"bitandbang": "./bin/card.js"
    }

#!/usr/bin/env node

arguments will be sent to the cli in an array

flags won't be recognized by default if you aren't using a framework (one of many reasons you use a framework)

List of frameworks - are those just for parsing commands. Why is 'inquirer' not in this list?

It's more of an input output type of tool, prompts for users input - doesn't

### 01.a hello world

Why oclif?

FEATURES! [https://oclif.io/docs/features](https://oclif.io/docs/features)

- Flag/Argument parsing
- Super Speed
- CLI Generator
- Testing Helpers
- Auto-documentation
- Plugins
- Hooks
- TypeScript (or not)

use tools to develop tools and reach developer nirvana

- Auto-updating Installers
- Autocomplete

Oclif scaffolds clis

yarn link --global

to symlink your cli to use it 'as your users would have installed it' for testing.

note to be warned about multiple versions downloading if you have a symlink

### 02 Pass args and flags to a CLI

Oclif gives you a Command class that you extend off of.

it has a static `flags` `args` and `description` prebuilt as properties on the class that you can extend off of.

### flags vs args

flags have `-` or `--` in front of them. You can use them in any order

when in doubt, use flags - they are much more declarative for the user

have co-dependent flags or exclusive flags

**There's a rough order of precedence:**

env vars > flags > configs > stored settings

There are alot of flag parsing conventions. You should maintain a sane subset of flags

use a max of 1 arg type

args are positional. it matters.

Makes input tricky for the user - have to remember the order of arguments

### 03 Multi-command CLI

you can split these commands out but that feels wrong.

Put your commands in a `commands` folder which is a convention

`globby` is a hidden dependency of oclif

### 04 Set up Debugging and Testing for CLI's

**Debugging**

for debugging - get familiar with the —inspect-brk flag on node

`node --inspect-brk index.js`

oclif cares alot of about performance and when errors happen

in ocliff, prepend `DEBUG=*` to the start of your CLI command. it will output everything that it does leading up to the error and how fast in milliseconds it takes

can cmd click the where the error happens in the terminal

you'll want to use the `debug` module to show errors to your users.

    var debug = require('debug')('cliworkshop')

and then call `debug('statement you want to log')` anywhere in your code.

now when you `DEBUG=*` , it will output core commands and your own debug.

filter logs with globby.

so `DEBUG=cliworkshop*` if you think the bug is from your code

or `DEBUG=@oclif*` if it's coming from oclif

Whats the difference between my logs and oclif logs?

oclif logs are logged out for you by the core framework vs your logs which you add in yourself

Does Oclif use debug under the hood?

oclif uses `debug` under the

Don't make your cli too noisy. Give info when things are going wrong - if they aren't, just do the thing.

There is an idea of log levels but globby works well in most cases.

**Testing**

using Jest

need a jest config in `jest.config.js`

**You don't have to test the command itself - just the core logic**

You import `test` from @oclif/test which gives you helpers for providing inputs and expecting outputs

mocking and running tests like your users would use it. If theres files that exist, you'd have to mock them.

Always test on Windows/Linux (circle CI or GA actions could do this for you)
