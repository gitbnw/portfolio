---
layout: post
title: AbotAbout
thumbnail-path: "img/chatbot.png"
short-description: AbotAbout is a web based chatbot I built for providing some biographical background about myself.  <br>It uses Angular, AngularFire, and <a href="https://wit.ai/">WitAI</a>.
order: 1
---

{:.center}
![]({{ site.baseurl }}/img/chatbot.png)

## Explanation
While attending the Hackathon for Hunger, I worked on a team that produced a messenger bot that was tasked with replying to user sms messages regarding locations of nearby food depositories in the Chicago area.  I mostly listened and absorbed the work going on around me because the programmers were more seasoned then myself.  

I took what I learned from watching them plus + what I had learned about realtime databinding of AngularFire and attempted to create a chatbot for my portfolio site.

## Challenge
The majority of the challenge here was configuring the Wit's language processing to work as I intended.  It is awesome Wit allows free access to their client - but as with any third party API - you are at the mercy of it's output.  In this case the API behavior produced inconsistent output which would break the central purpose for having a chatbot.

## Solution
My solution for some of the unpredictable results I would receive from the language processing API was two part:  

*  Use quickreply buttons to encourage the user to respond with the text the bot's logic is built to handle directly. 
*  Use cleverbot's api to handle respondes to user text when the bot's certainty level went under 95%.

   

This works well but sacrifices a lot of the "AI" component - if you are programming to respond to menu clicks then there isn't much need for language processing. 

Here is a code sample of the userExchange from the application's main ng-controller.
{% highlight javascript %}
         vm.userExchange = function() {
             var message = null
             vm.prepMessage("human", message);
             //send user message to firebase
             Messages.send(vm.messageData)
                 .then(function() {
                     $scope.formData = {}; //reset form
                     witData.q = vm.messageData.content; //send same msg to wit
                     witData.session_id = $scope.wit_id;
                     //send user message to wit
                     var context = {};
                     Wit.converse(witData, context)
                         .success(function(data, status, headers, config) {
                             // this data is the rendered json of the messages_controller #converse response
                             // if wit doesn't understand initialize cleverbot track
                             if (data[0].cleverbotInit) {
                                 vm.cleverbotInit(vm.messageData)
                             } else {
                                 vm.delayQuickReplies(data.length)
                                 for (var i = 0; i < data.length; i++) {
                                     vm.handleBotReply(data[i]);
                                 }
                             }
                         });
                 });
         };
{% endhighlight %}

## Links
[github](https://github.com/gitbnw/rails_portfolio)