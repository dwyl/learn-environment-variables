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

## Research & Background Reading

+
+ Env vars on Arch Linux: https://wiki.archlinux.org/index.php/Environment_variables
