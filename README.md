# BTC Paywall
A wordpress plugin that creates a paywall for almost any wordpress content, payable in bitcoin over the lightning network

The files in the btcpaywall subdirectory of this git repository are the source code of the plugin. You can download the btcpaywall subdirectory, zip it, and upload it to your wordpress directory, or -- if you don't want to do the zipping -- you can download a prezipped version here:

https://highlevelbitcoin.com/wp-content/uploads/2020/11/btcpaywall-0.1.0.zip

[![Watch the guide](https://raw.githubusercontent.com/supertestnet/btcpaywall/main/images/Screenshot%202020-11-03%20at%207.16.49%20AM.png)](https://raw.githubusercontent.com/supertestnet/btcpaywall/main/videos/installation-guide.mp4)

# Installation

Install and activate the plugin through the plugins page in the backend of your wordpress installation. Just select Add new and upload the zip file.

# Lnbits

After you install and activate BTC Paywall, but before you can use it, you'll have to connect it to an lnbits wallet. Lnbits is, among other things, an abstraction layer that allows programs built for bitcoin's lightning network to communicate in a standardized way with most popular lightning network implementations, such as clightning and lnd, as well as custodial lightning wallets like opennode, lnpay, and lntxbot. You can either self-host lnbits in order to do everything with minimized trust (see github.com/lnbits/lnbits for more details) or get a custodial lnbits wallet at lnbits.com.

To connect BTC Paywall to lnbits, use the BTCPaywall Settings menu. It is located in the backend of your wordpress website > Settings > BTC Paywall. Visit the Settings menu and take the url of your lnbits host as well as your wallet api key and add them to the settings menu of BTC Paywall. The hostname will be https://lnbits.com if that is the site you are using or, if you are self-hosting lnbits on the same server that hosts your wordpress site, it may be something like http://localhost:5000. As for your api key, obtain that by creating an lnbits wallet and looking at the righthand sidebar. "Invoice/read key" is the one you want.

![Screenshot showcasing api key](https://github.com/supertestnet/btcpaywall/raw/main/images/lnbits-api-key-screenshot.png)

# Syntax

Once the plugin is installed and your lnbits url and api key are saved in Settings, create a paywall on any wordpress page or post using this syntax: [paywall price="1"]any wordpress content[/paywall]

The price, by default, is denominated in sats. In the above example, you will sell access to your content for 1 sat, or 0.00000001 bitcoins. In settings, you can change the denomination to US dollars if you want, which will cause the plugin to pull a price feed from coinbase. If you do that, [paywall price="1"]any wordpress content[/paywall] will cost the equivalent of 1 US dollar in bitcoin. You can also use decimalization if you select USD as your currency -- price="0.01" is a valid way to charge someone a penny for your content.

# Details

BTC Paywall uses server-side software to conceal the content of your paywall. That means the user does not have the content in their browser if they just de-obfuscate it. Instead, the server simply doesn't serve the content until the paywall is paid.

You are not limited to paywalling your written content. You can paywall your videos, your podcasts, your pictures, your livestreams -- almost anything you want to charge money for. If you can embed it on a wordpress page, you can paywall it.

When a user pays for a piece of content, their browser will store some data about their payment in a cookie. (Actually it's in the browser's local storage, but meh.) If they visit the page containing that content in the future, their browser will share that payment data with the server which will then use it to look up their old invoice. Since it is paid, the server will then show them the content they paid for.
