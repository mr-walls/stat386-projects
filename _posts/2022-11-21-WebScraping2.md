---
layout: post
title:  "Data Exploration: Children's Card Game Edition"
date:   2022-11-21
author: Nathan Walls
description: In this post I'll be exploring some top-level trends in data about the price of trading cards, using the pandas library for Python.
image: /assets/images/dm_25.jpg
---

## Nostalgia Business

I love trading card games. When I was a kid I remember always wanting to spend my allowance
on Pokemon or Yugioh cards, as I loved the cartoons growing up. As I started college, I found
I needed something outside of school to keep me from staring at code all day, and from that I
rediscovered that enjoyment for trading card games.

I also rediscovered just how easy it is to spend objectively too much money on
said trading card games.

In Yugioh, my favorite of these games, cards are frequently reprinted. This means
that a card with the same name and effect as an existing card gets put into new packs, often
with a slightly different text color or holographic effect, called rarity. This usually drives down
the price of the most expensive cards in the game, making it possible for people on a budget to
get the cards they want.

This business practice frequently makes me wonder just how effective it is
for making cards inexpensive. As such, I decided to collect data on all the cards printed
within the last year, as well as every version of those cards that exists dating back to 2002.
This data includes: the name of the card, what pack it was printed in, the lowest list price online, the
average online list price, and the rarity (again: holographic effect) on the card. From
these data points I also extrapolated how many printings a card has and what the cheapest alternative
copy costs.

In this blog post, I'll go through some of my findings as I've explored the data.


## A Few Visualizations

Right off the bat, I wanted to know what the top 10 most expensive cards were based off of average price. So I sorted my data
by average price and made this quick chart:

![Most Expensive Cards](https://github.com/mr-walls/stat386-projects/raw/main/assets/images/most_expensive_cards.png)

You may notice that the cards "Gold Sarcophagus" and "Number 106: Giant Hand" both appear
twice on this list (though if you're like me your attention was drawn more to the 25k price point for the most expensive card on this list.) 
This isn't a mistake. Many of the cards on this list have been released in different versions over the years, some more expensive than others.

For these cards in particular, each price represented here is for a version of the card that was extremely difficult to get,
either requiring you to do extremely well in practically professional tournaments or else get the card from a limited promotional event
over a decade ago. Notably, if someone wanted to pick up a cheaper version of any card on this list, not a single one can't be found for less than a dollar.

This then made me curious about cards which aren't old enough to have a second version available, after all, what if
someone wants to collect newer cards? Filtering for only cards with one printing available, the results look like this:

![One Printing](https://github.com/mr-walls/stat386-projects/raw/main/assets/images/one_printing.png)

These results are tamer, with the most expensive card on this list staying under $100. I play this game somewhat
competitively, and so I immediately recognized all 10 of these cards as ones which had success in major tournaments over the last year, though 
the structure of the data isn't really able to capture that currently. Regardless, it appealed to my general sense that cards
which are very good in the game would command a higher price point, but I also noticed in the data that all 10 of these cards
fall into either the "Ultra Rare" or "Secret Rare" category for rarity.

As such, I decided to take a look at how prices break down for each rarity available in the dataset. Here's how that looks:

![Price by rarity](https://github.com/mr-walls/stat386-projects/raw/main/assets/images/what_rarity_looks_like.png)

The first thing I noticed looking at this graph was the sheer number of outliers. I already had to graph this data
on a logarithmic scale for visibility, which is unfortunate for natural intuition from boxplot sizes, so
to see this many outliers signaled to me that card prices are wildly unpredictable.

To check out that wild variability, I decided to look at the correlation matrix of the major variables.

![Correlation](https://github.com/mr-walls/stat386-projects/raw/main/assets/images/somethings_wacky.png)

I hope you, like me, felt a desire to make a sarcastic remark about the .025
correlation coefficient between number of other printings a card has and its average price.
This is where I feel there's a lot left to be explained, as generally speaking, bringing
more copies of a card into the market should drive prices down. I think here it would be better
for me to treat number of printings as a categorical variable with a number of levels, rather than a continuous variable.
After all, the difference between 57 different versions of a card exisiting and 56 is probably non-existant and would drive
that number down.

With those crazy high peaks of price and insane outliers, I started to wonder
what the odds of a card winding up cheap are. After all, a game that is too expensive
will struggle to attract new players. So I made the following approximation
of the probability density for price of the cheapest version of a given card name.

![Sample Density](https://github.com/mr-walls/stat386-projects/raw/main/assets/images/price_pdf.png)

With the density appearing to be mostly concentrated between $0.01 to $10 per card, it seems
to me that maybe the game is rather cheap to play casually. Anecdotally, however, I hear
frequent complaints of the game being far too expensive for people to play. This begs the question for me:
are there really two different groups of cards here that I've lumped into one?

## What's Next?

The number of price outliers in each rarity category, as well as the low correlation
coefficients between price and number of printings leads me to believe there's
something that's dividing these data points into broader categories, or else there's just
a better way to explain the variation in price points.

In my next post, I'll be diving into the story of why there's so many outliers in the data,
and see if I can't find a better way to capture that story in the data.

If you want to use this data/code as a starting point for your own data exploration, you can check out the code and dataset
[here](https://github.com/mr-walls/Yugioh-Web-Scraping-Project).
