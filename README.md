# Learn Environment Variables [![Join the chat at https://gitter.im/dwyl/chat](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/dwyl/chat/?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Learn how to use Environment Variables keep your secret keys safe & secure!

![rainforest environment](http://i.imgur.com/aL1qD74.jpg)
<sup>*random picture of a rainforest river ... environment ... get it? ... tenuous connection? Hey, I liked it! hope you do too! Now, on with the tutorial!* </sup>


## *Why*?

If you put an API key on GitHub it means out of your control and someone
(*unauthorised*) has access ...  
the physical-world equivalent is writing your home address on the keyring
for your house keys and  
then losing your keys in a bad neighborhood, you'll be *lucky* if nobody uses
your keys to  
"borrow" the TV from your house...!

Avoid (*accidentally*) committing (*exposing*) your ***private keys***, ***passwords*** or other ***sensitive details***  
(*by hard-coding in them in your script*) to GitHub by storing them
as environment variables

## *What*?

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

In your terminal type: `printenv` and tap the `enter` key.

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
in this case we are running `printenv`

#### Log the list of environment variables available to node.js in `process.env`

Node.js gives you access to the variables defined in your environment
in the `process.env` ***global object***.

Create a file called `printenv.js` and paste the following line in it:
```js
console.log(process.env);
```
Run this script in your terminal:
```sh
node printenv.js
```

### Adding Variables to your Environment

There are 3 ways to add variables to the environment where your app is running.

#### Command-Line Arguments

When you run your node program/app you can include settings as environment variables
for example, try running the following:

```sh
PORT=1337 node printenv.js
```
Notice how the PORT variable is the first element displayed in the console?
You are now able to access the `PORT` value in your node.js script
by reference: `process.env.PORT`.



## Research & Background Reading

+ Detailed article: https://en.wikipedia.org/wiki/Environment_variable
+ Env vars on Arch Linux: https://wiki.archlinux.org/index.php/Environment_variables
