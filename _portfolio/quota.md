---
layout: post
title: Quota
thumbnail-path: "img/quota.png"
short-description: Quota is a web app for tracking stock performance.

---
{:.center}
![]({{ site.baseurl }}/img/quota.png)

## Explanation
This was my first self-made project using Ruby on Rails 4.  My goal was to create a functional web app that could lookup live financial market data and allow users to track and save that data. 

## Challenge

The challenge here for me was learning to use background processes in a web application.  I had previously used REST services in the more common approach of the request being initiated by the user by submitting a form or pressing a button, but here I wanted the app to automatically send notices to a user when a stock's crossed a pre-determined price point.  TO accomplish that I needed the app to frequently be requesting and reading data from a web service. 

## Solution

Using the gems - foreman, upstart, and resque - I created tasks that were saved in a redis store and run by the server in a scheduled time period.  This was good exposure to the behind the scenes/devops work that needs to be wrangled in a hosted environment.  Here I used Digital Ocean.

## Results

Bacon ipsum dolor amet filet mignon meatball spare ribs fatback bacon shankle. Kielbasa andouille fatback salami, boudin bresaola pig alcatra turkey spare ribs jerky. Corned beef bresaola leberkas salami alcatra beef landjaeger venison shank bacon meatloaf beef ribs picanha. Leberkas sausage brisket porchetta shankle prosciutto chicken picanha kielbasa pig kevin t-bone turducken filet mignon jowl.

> Bacon ipsum dolor amet filet mignon meatball spare ribs fatback bacon shankle. Kielbasa andouille fatback salami, boudin bresaola pig alcatra turkey spare ribs jerky. Corned beef bresaola leberkas salami alcatra beef landjaeger venison shank bacon meatloaf beef ribs picanha. Leberkas sausage brisket porchetta shankle prosciutto chicken picanha kielbasa pig kevin t-bone turducken filet mignon jowl.

Bacon ipsum dolor amet filet mignon meatball spare ribs fatback bacon shankle. Kielbasa andouille fatback salami, boudin bresaola pig alcatra turkey spare ribs jerky. Corned beef bresaola leberkas salami alcatra beef landjaeger venison shank bacon meatloaf beef ribs picanha. Leberkas sausage brisket porchetta shankle prosciutto chicken picanha kielbasa pig kevin t-bone turducken filet mignon jowl.

## Conclusion

Bacon ipsum dolor amet filet mignon meatball spare ribs fatback bacon shankle. Kielbasa andouille fatback salami, boudin bresaola pig alcatra turkey spare ribs jerky. Corned beef bresaola leberkas salami alcatra beef landjaeger venison shank bacon meatloaf beef ribs picanha. Leberkas sausage brisket porchetta shankle prosciutto chicken picanha kielbasa pig kevin t-bone turducken filet mignon jowl.