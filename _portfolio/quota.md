---
layout: post
title: Quota
thumbnail-path: "img/quota.png"
short-description: Quota is a web app for tracking stock performance built on <a href="https://github.com/rails/rails">Rails</a> with <a href="https://github.com/resque/resque">Resque</a>, <a href="http://redis.io/">Redis</a>, and <a href="https://www.postgresql.org/">postgres</a>.  <br>Deployed via <a href="https://github.com/capistrano/capistrano">Capistrano</a> to Digital Ocean.
order: 2
---

{:.center}
![]({{ site.baseurl }}/img/quota.png)

## Explanation
This was my first self-made project using Ruby on Rails 4.  My goal was to create a functional web app that could lookup live financial market data and allow users to track and save that data. 

## Challenge

The challenge here for me was learning to use background processes in a web application.  I had previously used REST services in the more common approach of the request being initiated by the user by submitting a form or pressing a button, but here I wanted the app to automatically send notices to a user when a stock's trading price crossed a pre-determined price point.  To accomplish that I needed to frequently be requesting and reading data from a web service. 

## Solution

Using the gems - foreman, upstart, and resque - I created tasks that were saved in a redis store and run by the server in a scheduled time period.  This was good exposure to the behind the scenes/devops work that needs to be wrangled in a hosted environment.  Here I used Digital Ocean and I deployed using Capistrano.  

I displayed the stocks activity in gradients to get visualize representation of current trading activity with some ruby, coffeescript and HTML5 properties:
{% highlight ruby %}
  def price_change_assign(stocks)

    stocks.each do |stock|
      @change = 100 * ((stock.lasttradepriceonly / stock.lasttradepriceonly ) 
      - (stock.lasttradepriceonly_was / stock.lasttradepriceonly))
      stock.ticks.pop if stock.ticks.length == 10
      if @change > 0.01
        stock[:ticks].unshift('green')
      elsif @change < -0.01
        stock[:ticks].unshift('red')
      else
        stock[:ticks].unshift('#272B30')
      end
      
    end
end
{% endhighlight %}
{% highlight javascript %}
<% @stocks.each do |stock| %>

    var canvas = $('#canvas-<%= stock.id %>')[0]
    var width = canvas.width;
    var height = canvas.height;
    var colorArray = <%= raw stock.ticks.to_json %>
    
    $stock = $("<%= j render(stock) %>");

    $stockrow = $('#stock-row-<%= stock.id %>')

    $stockrow.html($stock)

    show(canvas, colorArray, width)

    
<% end %>
{% endhighlight %}
{% highlight coffeescript %}
canvasArr = []

@colorize = (canvasObj) ->
  i = 0
  while i < canvasObj['colorArray'].length
    stop = i / canvasObj['colorArray'].length
    canvasObj['gradi'].addColorStop(stop, canvasObj['colorArray'][i])
    i++
  return canvasObj['gradi']
    
@show = (canvas, colorArray, width) ->

  ctx = canvas.getContext('2d')
  gradi = ctx.createLinearGradient(0, 0, width, 0);

  find_canvasObj = $.grep canvasArr, (canvasObj, i) ->
    canvasObj["canvas"] == canvas 
  
  canvasObj = {}
  canvasObj['gradi'] = gradi
  canvasObj['canvas'] = canvas
  canvasObj['colorArray'] = colorArray
  canvasArr.push(canvasObj)
  this_canvasObj = canvasObj
  this_canvasObj['gradi'] = gradi
  ctx.fillStyle = colorize(this_canvasObj);
  ctx.fillRect(0,0,width,24); 
{% endhighlight %}

## Results

The good  
    * Exposure to TDD / Rspec  
    * Devise for user registration / authentication  
    * some basic auotmation to "test drive" app with temporary profile and data  
    * coffeescript   C|__|  
    * data driven html 5 gradients  
    
The less good  
    * Difficult to find sources of free endpoints for market data.  And when your app is built around using that data, you can get trapped in the "garbage in, garbage out" cycle.    
    * I pushed to try to make this more object oriented then any of my previous RoR attempts.  I still have plenty ways to go but I did start noticing more the importance of naming methods/variables in a way that would lend themselves to further use throughout the application while not requiring the programmer to go back through the code in search of what the method is or what it returns.  
    * Many configuration tweaks in deployment.  Hard to track those changes, partially because you get sick of writing commit messages that aren't just salty expressions of frustration  (╯°□°)╯︵ ┻━┻.
    
## Conclusion

> A work is never completed except by some accident such as weariness, satisfaction, the need to deliver, or death: for, in relation to who or what is making it, it can only be one stage in a series of inner transformations. --Paul Valéry

This will certainly be the case in a less dramatic fashion for a relatively new developer such as myself.  The rate of new material being learned is outstripping that of your production.  It's not neccessarily bad but it makes completing a project, especially one that was self-assigned, a bit of a perpetual mouse wheel. 

## Links
[github](https://github.com/gitbnw/quota)