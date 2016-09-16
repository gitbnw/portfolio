
layout: post
title: Quota
thumbnail-path: "img/quota.png"
short-description: Quota is a web app for tracking stock performance.


{:.center}
![]({{ site.baseurl }}/img/quota.png)

## Explanation
This was my first self-made project using Ruby on Rails 4.  My goal was to create a functional web app that could lookup live financial market data and allow users to track and save that data. 

## Challenge

The challenge here for me was learning to use background processes in a web application.  I had previously used REST services in the more common approach of the request being initiated by the user by submitting a form or pressing a button, but here I wanted the app to automatically send notices to a user when a stock's crossed a pre-determined price point.  TO accomplish that I needed the app to frequently be requesting and reading data from a web service. 

## Solution

Using the gems - foreman, upstart, and resque - I created tasks that were saved in a redis store and run by the server in a scheduled time period.  This was good exposure to the behind the scenes/devops work that needs to be wrangled in a hosted environment.  Here I used Digital Ocean.

## Results

<!--The good-->
<!--    * TDD / Rspec -->
<!--    * Devise for user registration / authentication-->
<!--    * some basic auotmation to "test drive" app with temporary profile and data-->
<!--    * coffeescript  C|__|-->
<!--    * data driven html 5 gradients-->
<!--    * models -->
    
<!--The bad-->
<!--    * Very difficult to find sources of free reliable market data.  And when your app is built around using that data, you can get trapped in the "garbage in, garbage out" cycle.  -->
<!--    * I pushed myself to try to make this more object oriented then any of my RoR attempts.  I found myself getting tripped up in naming and structuring methods in a way that would be friendly to reuse.  -->
    
## Conclusion

Bacon ipsum dolor amet filet mignon meatball spare ribs fatback bacon shankle. Kielbasa andouille fatback salami, boudin bresaola pig alcatra turkey spare ribs jerky. Corned beef bresaola leberkas salami alcatra beef landjaeger venison shank bacon meatloaf beef ribs picanha. Leberkas sausage brisket porchetta shankle prosciutto chicken picanha kielbasa pig kevin t-bone turducken filet mignon jowl.