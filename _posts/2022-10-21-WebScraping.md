---
layout: post
title:  "Expensive Cardboard"
date:   2022-09-13
author: Nathan Walls
description: It's a bit odd to think how trading cards can fetch thousands of dollars at auction, but yet so many are worth so little despite having the same art. In this post I'll be gathering some data from the web to look into this weird collectible market.
image: /assets/images/box.jpg
---

## Introduction

In March of 2022, a Charizard card from the Pokemon trading card game
fetched a six figure winning bid at auction. One piece of cardboard;
over 400,000 dollars. This is an extreme example, but it serves to show
how collectible markets can get out of hand.

![Charizard](https://github.com/mr-walls/stat386-projects/raw/main/assets/images/money.jpg)  

<b>Pictured: something close, but not quite the 400k card</b>

I personally play a trading card game like Pokemon, called Yu-Gi-Oh.
Seeing as I'm blogging about statistics, I'm going to assume the nerdy stuff is
cool enough. The company that manages Yu-Gi-Oh does a good job of making
old cards available to players, often with cosmetic differences which
helps collectors and players alike.

With these reprints there are often copies of a card people tend to play,
and copies of the same card that are more of a collectible, and therefore more expensive.
I want to see just how much of a difference in price that "collectable"
factor make. In a more economic sense, you could frame this question like this:
How much of an effect on price do cosmetic differences have between two otherwise equivalent products?

## Ethical Scraping

Before collecting data from the web, it's important to make sure the publishers
of a website allow, or at least don't disallow, automated web scraping. For this project,
I'll be collecting data from two sites:

[db.yugioh-card.com](db.yugioh-card.com): an official site listing cards and
products for the game.

[www.yugiohprices.com](www.yugiohprices.com): a third party site that monitors
online sales and listings to provide data about card prices.

In the case of the first site, I looked at the Terms of Use published
by the site owners. It specified nothing about not collecting data, but I will
clarify per their request that I am not affiliated with them in any way.

For the second site, I looked at the robots.txt file provided by the site
and noted all the "disallows" and made sure that my scraper did not touch
those endpoints on the site. Because my code made many requests to this site,
I made sure to include a delay to avoid bombarding their server with requests.

Huge thanks to the owners of these sites!

## Process

Overall the process of collecting data was rather simple. First, I narrowed
down the range of cards I wanted to look at to cards that the company had
released in products in 2022. Some of these are new cards, with no second
copy available, while many where reprints of cards first released in prior years.

From the official site, I first gathered a list of all the products released this year. Then 
for each of those products I compiled a list of all the unique cards in that product.

I then took that time-curated list of cards to the third-party website
and scraped price data for all versions of those cards, including ones printed before 2022. The pages did have a lot of
extraneous tables that offered a challenge in filtering only the correct tables.
The Google Chrome extension [SelectorGadget](https://chrome.google.com/webstore/detail/selectorgadget/mhjhnkcfbdhnjickkkdbjoemdmbfginb?hl=en)
makes tasks like this a breeze.

![Gadget](https://github.com/mr-walls/stat386-projects/raw/main/assets/images/selectorgadget.png)

That table wasn't originally yellow, the extension allowed me to select html elements
just by clicking them and then provided an input for BeautifulSoup's ```.select``` method to easily scrape
just the desired info.

## The Data

From this process I was able to collect 4760 observations of card
prices. I collected the name, product the card was released in, foil type (rarity),
minimum price, and average price of these cards. You can check out the code and dataset
[here](https://github.com/mr-walls/Yugioh-Web-Scraping-Project).

In my next post, I'm going to look at how the availability of different
versions of a card affect prices for any or all versions, so stay tuned!