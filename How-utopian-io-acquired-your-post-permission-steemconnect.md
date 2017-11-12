
Before you reading the following contents, I hope you have a basic knowledge of public key encryption system and steem's authorization system, at least you should know the differences between the four keys: `master(owner), posting, active`, and `demo key`. During this writing, I feel more appreciated of steem's design, which splits permission elaborately and makes multi-signature easy to achieve.

Before to know how `utopian.io` acquired our post permission, let's see how these happened in `steemit.com`.

## How do you login steemit.com?

You may answer without hesitation: type my username, password, and then login. Now I will ask you two questions:

1. What is the password you are using to log in? Is it the master key? Or posting key?
2. Will `steemit.com` store your password or your four mystery keys?

I bet you most can't answer :P, let me tell you.

The password is the seed string that generated when you registering your account, other four keys are deterministic calculated according to your account name and seed. The calculation occurs only in your web browser, neither your seed nor the resulted four keys will be uploaded.

We trust steemit.com not uploading our privates because it's the authority application of steem, the source code is open to anyone to review. In other hand we can easily supervise all communications between browser and `steemit.com`.

## How articles are posted using steemit.com

First, let me demonstrate the mystery four keys deeply. The four keys, are actually four key pairs, each key pair contain a public and a private key. As to posting, the posting key pair will be used.

Assuming @cifer --- yes it's me, want to post on steemit.com, because steemit.com holds all the four key pairs (locally, as said before). As @cifer finish writing and hit the `Post` button, steemit.com will create a new `comment` type transaction using @cifer's name, sign it using @cifer's private posting key, and broadcast to all witnesses.

Then witnesses will lookup @cifer's account metadata, fetch the public posting key, use it to verify the transaction indeed issued by @cifer.

## How do you login utopian.io?

Well, actually you are not login `utopian.io`, instead `steemconnect.com`. `steemconnect.com` issues a token under you authorization to `utopian.io`, thereafter you can post using `utopian.io`, oh let me speak exactly: `utopian.io` can post using your name!

So what is `steemconnect.com`? Why I need using it to login `utopian.io`?

The short answer, because `utopian.io` is a good, brilliant, outstanding service! Surely utopian.io can ask your private posting key or even your seed to login, but it doesn't, by using `steemconnect.com`, `utopian` does not ask any of your private keys at all.

## What's the steemconnect.com? Why using it?

You have know the process of posting at steemit.com, let's talk about how to post using other third party apps, like `utopian.io`, `busy.org`, etc..

As has said before, surely we can using seed to login these apps, but this will expose you completely. Some apps requires only 1 or 2 of your four keys, yet exposing is still not a good idea. Despite of `utopian.io` and `busy.org` --- we know they are both trusty apps, but what if in future, every new app appear we exposing our key to it? No it's bad.

So, we need `steemconnect.com` now, it let us using third-party apps without exposing any keys to them. How this works?

> Btw, this sounds like a Ad for steemconnect.com, but honestly not, I just want to show you how safely it is using utopian.

When you click `login` on `utopian.io`, you will be navigated to such a page, notice the url is `v2.steemconnect.com`.

![屏幕快照 2017-11-12 19.23.14.png](https://steemitimages.com/DQmSVyxkprMkX3eTiZ5ZmLA7MBFCmhNQUTKiFPMf8EJos6G/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-11-12%2019.23.14.png)

then after you click `Continue`, you authorize steemconnect.com to write some data to your account meta, what data was written? you could find in `steemd.com`, from the most recent change, you will find such a record:

![屏幕快照 2017-11-12 19.27.21.png](https://steemitimages.com/DQmaojet9HUvVAfk7wzPj1q2azAnRFuzV2JVKGCQosDvP72/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-11-12%2019.27.21.png)

Yeah, have you noticed the `account_auths` field? Thanks for steem's sophisticated design, now I have the @utopian.app embedded into my account meta.

In such way, utopian.io can post article using my name but sign with it own private posting key. When witnesses receive this transaction it again lookup @cifer's account meta and find the public posting key. Note, this time witnesses will find utopian.app's key, use it verifying this transaction and pack the transaction into new a block.

By now, I have successfully posted using utopian.io without exposing any of my keys!

In the future, any third party service built on steem tend to use this steemconnect-like mechanism, if not, you should think over whether to use this service.

## The end..

Enjoy yourself using `utopian.io`!
