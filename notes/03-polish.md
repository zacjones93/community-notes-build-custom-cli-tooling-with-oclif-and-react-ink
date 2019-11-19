### 09 Prompt Users to Update CLI Versions with Update Notifier

can create a abstract class `Command` that will create a base command that all your Commands can extend

package updater is a good use-case for a shared command, all your commands will want to notify the user when they should update their cli

    const updateNotifier = require('update-notifier');
    const pkg = require('./package.json');

    updateNotifier({pkg}).notify();

### 10 Store State on Filesystem in CLI's respecting XDG-spec with Conf

### 11 Create CLI's that Intelligently Adapt to Usage with Frecency

wouldn't it be nice if highly used inputs would be the default.

We're in the filesystem, we have free state.

it's free realestate.

State to store:

- authentication tokens
    - careful about storing unencrypted passwords
- preferences
- prior selections from a list
- performance caches
- offline sync actions
- `frecency` storage (more info next!)
- *whatever you want, within reason*

Where do you store state?

CLI's will store state globally.

The spec is XDG spec.

This allows users to tell us where we can store our CLI cache

we'll use `conf` library

everytime there is a selection from user input. Global cache will also be set

this will get set as an array. that array can be called wherever.

Offer to persist state when possible to create

should - reverse order, de-duplicate, limit to 5 - just working with that array.

**Frecency**

a combination of frequency and recency.

there's a library for this but it's implemented

### 12 Polish CLI Output with Ora, CLI-UX, and Chalk

chalk is the defacto library for styling your cli

has a nice api that you can explore

Any string that has user input should be colored

cli-ux is oclifs first party utility library

spinner, wait

you want to be able to grep tables in a cli

you do this a lot with things like seeing what processes are being ran on a port

Ora is THE spinner library

cli-spinners is another spinner library

## React Ink

### 13 Build Interactive CLI Components with React Ink

it's experiemental

React ink is a react renderer to the CLI

try centering things in the terminal

Oclif does not recognize `.tsx` files

You have to monkey patch node_modules

working with nodejs - you'll need to do this on occasion.

you modify your node_modules - to persist the changes that you made you can add `patch-package` to the project

and then add a `postinstall` of "patch-package" which will create a git diff of the patch

The hook between oclif and react-ink is the `render` function

### 14 Create Flexible CLI Layouts with React Ink's Box Components

The `Box` component that ink gives you has all the defaults of flexbox.

width, height, flexDirection, textWrap, padding, margin, flexGrow

There are a good number of first class components from Ink

It's early days for this package but a lot of companies have this in production already

### 15 Create Dynamic Command Line User Interfaces with React Ink Input Components

Why again would you caution against using react-ink with cli-spinners?

react-ink wants control over stdoutt - it wants to output to the screen. Ora also wants to output together. They both rely on a strict reference to the line that they are referencing. You'll get an intermixed-ugly output. It doesn't work naively.

At what point in your development of CLI’s do you start reaching for something like React Ink? Do you start with oclif and switch to something ‘nicer’ like React ink or just start with the latter?

get functionality working is the first step, you can add a rendering layer like React Ink afterwards

### 999 - Future

There's a project that is re-writing node into Rust

dry run movement for CLI's

adaptive CLI's - State machines for CLIs
