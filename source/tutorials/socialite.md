---
title: Socialite integration tutorial
description: Implementing social login with Socialite
extends: _layouts.documentation
section: content
date: 2023-09-20
---

So you've [set up your GraphQL authentication](/tutorials/getting-started/), but you want to give your users the ability to log in with a social network or other identity provider. Thanks to [Laravel Socialite](https://laravel.com/docs/socialite), we can authenticate with any oAuth provider. In this example, we're going to use Twitch's provider to authenticate our users.

Here's the flow we're going to build:

[ Our front end ] -> [ Social provider ] -> [ Our GraphQL API ]


First, take a look at the oAuth docs for your provider. [Here's Twitch's](https://dev.twitch.tv/docs/authentication/getting-tokens-oauth/). The first important section is the ["grant flows"](https://datatracker.ietf.org/doc/html/rfc6749#section-1.2) the provider supports. There's two flow types we're interested in:

* **Implicit grant flow**: where the social provider sends us back an access token directly. This flow is generally [not recommended](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-security-topics#name-implicit-grant) for security purposes.
* **Authorization code grant flow**: where the social provider sends us a "code" (TODO: talk about code challenge too, PKCE) which we exchange for an access token and a refresh token. This is recommended over the implicit flow.

Now we need to make the button that requests your token from the social provider. Typically this is a simple link we navigate the client's browser to. With oAuth the endpoint is always /authorize. Twitch's docs provides the parameters required to build up this link for each flow:

[]

Often these providers offer some SDK that can build these links for you too, and handle the state/code challenge automatically.
