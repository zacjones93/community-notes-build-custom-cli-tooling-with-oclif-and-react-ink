### 05 Beautiful Prompts for User Input with Enquirer

Inquirer is different than Enquirer

oclif ships with a basic prompt that works fine.

Enquirer has a lot of prompts that you'll want.

Big feature is autocomplete

so many little things that you take for granted when working in the dom

check if input already exists and then prompt for it.

basic api is `prompt` from enquirer

you have to `await` `prompt` so you need to be in an `async` block.

it will give you an object back

**Your prompts should teach the human how to use it**

### 06 Read User Config with Cosmiconfig

babel, jest, prettierrc

there's yaml, json, toml... others.. in other words you need a framework for this.

cosmicconfig is the default used for standardized consumption of configs.

    const explorerSync = cosmiconfigSync('myfirstcli');
    const searchedFor = explorerSync.search();

which will return an object with `config` and `filepath` property that you can use

Don't validate your package.json in a cli tool!

### 07 Build Your Own Boilerplate Scaffolding CLI with Copy-Template-Dir

templating and scaffolding are a little different

templating is lower level - one to one.

scaffolding - you typically want to dump out alot of things in one folder

you'll have a 'in' and 'out' directories for a scaffolding command

    const vars = { foo: 'bar' }
    const inDir = path.join(process.cwd(), 'templates') // careful! see below
    const outDir = path.join(process.cwd(), 'dist')

and then define what you want to do. In this case, copy contents of one directory into another

    // promise based alternative
    const {promisify} = require('utils')
    promisify(copy(inDir, outDir, vars))
      .then(() => console.log('done'))
      .catch(err => throw err)

copy-template-dir is pretty robust for multi-platform.

### 08 Execute and Pipe Child Processes with Execa

What is a child process?

alot of times your cli will want to call other CLIs

node has a very simple child process api that you can use with `spawn`

3 streams that you'll use

stdin is a stream coming in

2 streams going out

stderr for errors you run into

stdout is output that you want to control

execa is used for cross platform nuances that no one has time for.

There's no native difference between arguments and flags.

good way to log stuff is to pipe stdout (`subprocess.stdout.pipe()`) into a file with fs

to install dependencies, you need to `chdir` into the scaffolded folder
