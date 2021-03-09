---
layout: post
title: 'CO2-monitor: follow your carbon footprint on chrome'
date: 2020-04-16
published: true
---


CO2-monitor is a chrome extension to follow your carbon footprint during your navigation on the Internet. It's available on
the chrome web store and the firefox add-ons store.

## How co2 emissions are assessed ?

As many parameters need to be taken into account in the co2 emission equation, it is almost impossible to know exactly how much co2 has been produced by your daily internet usage; although, some of them are the following :

- Your computer energy consumption.
- The carbon intensity of the electricity you're using.
- The website's servers carbon intensity.

My first idea was to use the user location, the carbon intensity of the electrical grid in the country he lives in, the cpu he uses and how much Mbs of data is passing though chrome to obtain a rough estimation. However, this implementation has two major downsides :

- It is not taking into account the carbon intensity of the data center.
- The parameter used is not really at the hand of the user, so it would be hard for him to optimize his co2 emissions related to his daily browsing.

As I discovered the API of wholegrain, I used it on around 50 most visited websites (according to alexa and similarweb) to obtain a rough estimation of how much co2 is produced when visiting each of those websites. Actually, three attributes have caught my attention for each website:

- CO2 produced by visiting one page.
- Size of the bytes transferred between my computer and the website.
- Energy used to load the page.

When you're visiting one of the given website, the extension is using the data which are passing through chrome and the known co2 emissions for a certain data byte size to obtain a rough co2 emissions estimation.
When you're navigating on unknown website, the extension is using the average result.

I averaged the numbers obtained with the 50 websites. Hence, when you are visiting unknown website, the extension is using the average numbers to compute the co2-emissions.

## Resources

Wholegrain API is used to obtain a rough estimation of the carbon intensity of a list of some most visited websites :

- [Wholegrain Carbon API](https://www.websitecarbon.com/)
