---
layout: post
title: PD Fleet Status
thumbnail-path: "img/pdfs.png"
short-description: A web application built for a police department on the <a href="https://www.sencha.com/products/extjs/#overview">ExtJS</a> framework and Coldfusion.
order: 4
---

{:.center}
![]({{ site.baseurl }}/img/pdfs.png)

## Explanation
I was tasked upon entering my current job with converting a previously existing MS Access application into a web based one.  

## Challenge
The application's primary purpose was inventory management as applied to the police department's fleet of vehicles.  This meant tracking the vehicle's availability in way that police supervisors could assign avalible vehicles out for each rolling shift of officers.

I was given a crash course in Coldfusion training as that was the back-end environment the application was required to function on.  I made a few attempts to build the front-end in CF as well but found it very limiting.  Eventually I started using the javascript framework that CF uses for many of it's components, ExtJS.   My only real web programming to this point was piecing together some PHP to generate SQL reports so the ExtJS seemed fairly intimidating.

But the real challenge here was that I wasn't programming a project for myself, this had actual users.  And users have opinions.  Opinions that they changed each time they saw another version of the application.

## Solution

Functions this web app is able to perform  
    * Track vehicle status  
    * Allow police supervisors to assign vehicles for current and following shifts  
    * Allow supervisors to "advance" the shift so that the current shift expires and the following shift becomes the current shift.  
    * Allow supervisors to request repairs from fleet services dept  
    * Allow fleet services dept to request vehicle delery for services  
    * Allow fleet services and police department to see different views of application along with different permissions on functionality  
    * Allow users to use their network login (Windows authentication) for access  
    * Generate SQL reports for both police and fleet services  
    * Generate charts via the js library zingchart  

## Results
Aside from exposure to bootstrap, js, and learning to use loops and Ajax calls - this was my first exposure to an MVC framework.  My implementation was anything but graceful, however the application works and is relied upon daily by it's users.

Multiple times I ran into problems with scope, timing, callbacks, etc.  I went into this project much like I had when writing scripts for IT tasks -- basically keep coding until it works.   I came out of it starting to grasp some of the OOP concepts without realizing it.  Being forced into an MVC structure helped.  But also produciing repetetive code that became unwiedly, difficult to trobuleshoot, and brutal for any other developer who inherited it. 
