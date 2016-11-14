# Learn Environment Variables [![Join the chat at https://gitter.im/dwyl/chat](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/dwyl/chat/?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Learn how to use Environment Variables keep your secret keys safe & secure!

## *Why*?

Avoid (*accidentally*) committing (*exposing*) your ***private keys***, ***passwords*** or other ***sensitive details***  
(*by hard-coding in them in your script*) to GitHub by storing them
as environment variables.

> *Accidentally* pushing API keys to GitHub can be an *Expensive/Stressful Lesson*:
<small>https://www.quora.com/My-AWS-account-was-hacked-and-I-have-a-50-000-bill-how-can-I-reduce-the-amount-I-need-to-pay</small>

## *What*?

An environment variable is a `KEY=value` pair that is stored on the
local system where your code/app is being run and is accessible from within your code.

If you are new to "***back end***" development, you may not have encountered
environment variables
before, this quick guide will tell you *all* you need to know!

[The Twelve-Factor App](http://12factor.net/config) ***best practice***
recommends storing your app's configuration
in the "*environment*", but what does that mean?

> This *simply* means that you save any configuration both the values that are the  
same everywhere you run your app and the keys that change depending on where  
you are running the app, in the environment where you are running your app.

## *How*?

### List all the *Default* Environment Variables

In your terminal type: `printenv` and then the `enter` key.

You should see something like this:
```js
{
  TERM_PROGRAM: 'Apple_Terminal',
  SHELL: '/bin/bash',
  TERM: 'xterm-256color',
  TERM_PROGRAM_VERSION: '343.7',
  USER: 'n',
  PWD: '/Users/n/code/learn-environment-variables',
  LANG: 'en_GB.UTF-8',
  _system_arch: 'x86_64',
  _system_name: 'OSX',
  _: '/usr/local/bin/node'
}
```
This is a list of all the variables defined in your environment,
in this case we are running `printenv` on a Mac using the "Terminal" app,  
if you are on Linux/Unix using Bash/etc.
you will see something slightly different.

#### Log the list of environment variables available to node.js in `process.env`

Node.js gives you access to the variables defined in your environment
in the `process.env` ***global object***.

Create a file called `printenv.js` and type/paste the following line in it:
```js
console.log(process.env);
```
Run this script in your terminal:
```sh
node printenv.js
```

### Adding Variables to your Environment

There are 3 ways to add variables to the environment where your app is running.

#### 1. Command-Line Arguments

When you run your node program/app you can include settings as environment variables
for example, try running the following:

```sh
PORT=1337 node printenv.js
```
Notice how the PORT variable is the *first element* displayed in the console?
You are now able to access the `PORT` value in your node.js script
by reference: `process.env.PORT`

including your config in the command you use to run your script/app gets
cumursome when you have lots of API Keys or Databases ...

#### 2. Export the Variable to your Environment

An improvement on this command-line arguments is to export the variable
in your terminal:

Type/paste this in your terminal window and tap enter:
```sh
export HELLO=WORLD
```
Now `printenv` or `node printenv.js` to see it printed!
the `HELLO` key is now available in the `process.env` object
try adding the following line to your `printenv.js` file:

```js
console.log(">> Hello", process.env.HELLO);
```
Now run it in your terminal:
```sh
node printenv.js
```
What do you see?

```sh
>> Hello WORLD
```

Exporting your keys to your environment using `export MY_VAR=HAI` works
but if you use a terminal that does not *save* your variables across sessions,
(e.g. if you close your terminal window!) you will have to keep exporting them!

Thankfully there's a ***3rd*** (*easier*) ***way***: https://github.com/dwyl/env2

#### 3. Use a `.env` file *locally* which you can `.gitignore`

The way we prefer to manage our Environment Variables on our development machines
is using a `.env` file which gets loaded into our app *once* and
adds any entries in the `.env` file to the `process.env` (*global object*).

We wrote the [**env2**](https://github.com/dwyl/env2)
***node.js module*** to load configuration from a `.env` or
`.json` file.

Loading your environment variables from a `.env` file is as easy as "ABC"!

##### A. Create your `.env` file

Create a `.env` file in the root of your project and insert
your key/value pairs in the following format of `KEY=VALUE`:

```sh
DB_HOST=127.0.0.1
DB_PORT=9200
DB_USER=TheSpecial
DB_PASS=EverythingIsAwesome
```

##### B. Install `env2` and save it to your `package.json`

Install the [**env2**](https://github.com/dwyl/env2)
module from NPM and save it as a Dependency in your
`package.json` file:

```sh
npm install env2 --save
```

##### C. Invoke `env2` and use the variable in your script

Loading your configuration is a 1-line call to node.js's `require` method
which loads [**env2**](https://github.com/dwyl/env2) and invokes it with
your `.env` file as the argument:

```js
require('env2')('.env');    // loads all entries into process.env

console.log(process.env.DB_HOST); // "127.0.0.1"
```

Now you can access any of the entries in your `.env` file as a key
in the `process.env` Object e.g: `process.env.PORT` is `9200` (in our example above).


##### D. Add `.env` to your `.gitignore` file!

```sh
echo .env >> .gitignore
```

This ensures that the `.env` is not "tracked" in .git and thus
will not be public on GitHub. i.e only visible on your local machine.  
If you are new/rusty on using `.gitignore` file to omit files/folders
from your Git/GitHub repo read: http://git-scm.com/docs/gitignore

<sup>1</sup>[**env2**](https://github.com/dwyl/env2) solves the problem
of loading config files, we *recommend* using [**env2**](https://github.com/dwyl/env2) because
the ***code is clean, tested & documented***,
but there are *other* solutions to this problem on NPM you can chose from
depending on your needs. But if [**env2**](https://github.com/dwyl/env2)
does cover your *specific* use-case,
please tell us about it, we *always* love helping to solve problems and
enhance our modules to be more useful to people! [![Join the chat at https://gitter.im/dwyl/chat](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/dwyl/chat/?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


## Environment Variable *Naming Convention*

The Google Shell Style Guide (*naming convention*) states: **All caps, separated with underscores**
so this is *Good*:
```sh
export DATABASE_HOST=localhost
```
Whereas this is *Bad*:
```sh
export databaseHost=localhost
```

see: https://google.github.io/styleguide/shell.xml#Constants_and_Environment_Variable_Names

## Removing an Environment Variable

If you have exported an environment variable in your terminal, e.g:
```sh
export PORT=8000
```
You can `unset` (*delete*) it by running:
```sh
unset PORT
```
Now the `PORT` environment variable will no longer be set.

<br />

## Using *Environment Variables* with Travis-CI! [![Build Status](https://travis-ci.org/dwyl/learn-travis.svg?branch=master)](https://github.com/dwyl/repo-badges)

> If you are ***new to Travis-CI***
check out our ***introductory tutorial*** (*for complete beginners*):
https://github.com/dwyl/learn-travis

There are **two ways** of telling Travis-CI about your environment variables:

### 1. Include Environment Variables in your `.travis.yml` file

The easiest and most *explicit* way of listing your environment variables
is to add them to your `.travis.yml` file:

```yml
language: node_js
node_js:
  - 6
env:
- MY_VAR=EverythignIsAwesome
- NODE_ENV=TEST
```
The interesting part is the `env:` key where you can then list
your environment variables and their corresponding values.

### 2. Add environment Variables in the Web Interface

The *other* way of telling Travis-CI your environment variable(s)
is to add them in the web-base user-interface (Web UI) in your project's settings page:

![add travis-ci environment variables Web UI](http://i.imgur.com/5ubG0fM.png)

*Notice* how in if you add your environment variables in the the Travis Web UI
they are hidden (*from the build log*) by default.
This does *not* prevent you from accidentally `console.log` them and exposing a key/passord.
So take care when console.logging ...!

### *Secure* (*Encrypted*) Environment Variables

If you are storing sensitive information (*like API Keys or Database Passwords*)
for use in your node app, the ***best way*** is to use the
[***travis ruby gem***](http://docs.travis-ci.com/user/encryption-keys/)
to ***encrypt*** your keys:

You will need to have ruby installed on your computer,
if you don't already have this, we recommend installing it with
[**RVM**](http://stackoverflow.com/a/14182172/1148249):

```sh
\curl -L https://get.rvm.io | bash -s stable --ruby
rvm install current && rvm use current
```
Once you have installed ruby you can **install** the **travis ruby gem**:

```sh
gem install travis
```

With the gem installed, you encrypt your variable by running the command
in your terminal (*ensure you are in the working directory of your project*)

```sh
travis encrypt MY_SECRET=super_secret
```
Type `yes` to confirm you are your project, you should now see your encrypted variable:

![learn-travis-encrypted-variable](http://i.imgur.com/7WP1Xe0.png)

Paste this in your `.travis.yml` file and commit it to GitHub!

<br />


## Environment Variables on Heroku

Visit your apps dashboard on heroku and click on the app you want to add
an environment variable to:

Go to `Settings` and Click `Reveal Config Vars` to view the `Config Vars`:
![heroku reveal config vars](http://i.imgur.com/99M0kWK.png)

Next, click on `edit` and and add your desired key/value pair:

![add your env vars](http://i.imgur.com/kLp4X9P.png)

That's all there is to it!

## Research & Background Reading

+ Detailed article: https://en.wikipedia.org/wiki/Environment_variable
+ The Twelve-Factor App > Configuration: http://12factor.net/config
+ Env vars on Arch Linux: https://wiki.archlinux.org/index.php/Environment_variables

# Thanks!

Thanks for learning about Environment Variables with us!  
If you have any questions, please ***ask***!! [![Join the chat at https://gitter.im/dwyl/chat](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/dwyl/chat/?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)  
Please :star: this repo to help spread the word!

If you are using environment variables in a way not mentioned in this readme,
or have a better way of managing them or ***any*** other ***ideas
or suggestions*** for improvements ***please tell us***!!
