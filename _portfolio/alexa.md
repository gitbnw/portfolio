---
layout: post
title: Alexa skills
thumbnail-path: "img/alexa.png"
short-description: Three apps/skills for Amazon's Alexa Voice Service built using node.js and ruby with <a href="https://github.com/sinatra/sinatra">Sinatra</a>.  Deployed on Amazon Web Services.
order: 2
---

{:.center}
![]({{ site.baseurl }}/img/alexa.png)

## Explanation
I built 3 apps/skills for Amazon's Alexa Voice Service.

Redbird Games (a trivia game based of the St. Louis Cardinals) &  Odd Facts (a factoid generator) were built from tutorials, and were done to get a feel for Alexa's capabilities.


## Challenge
The new encounters here in order of difficulty: Sinatra, Alexa, Amazon Web Services.  I found the [alexa-rubykit](https://github.com/damianFC/alexa-rubykit) gem and it's tutorial very helpful in walking through the process.  
The process of verifiying an SSL certificate was also new to me and a requirement from Amazon.  A little tricky but interesting stuff.

## Solution
A look at handling the primary intent request from Alexa in which a user requests a stock lookup from my app.
{% highlight ruby %}
  if (alexa_request.type == 'INTENT_REQUEST')
    # Process your Intent Request
    if (alexa_request.name == 'GetQuote')
      @symbol_raw = alexa_request.slots['SymbolRequest']['value']
      @symbol = @symbol_raw.gsub(/[^A-Za-z]/, '').upcase
      if @symbol.nil?
        response.add_speech("I'm sorry, I didn't catch that stock symbol. 
        Which quote would you like?")
        end_session = false
      else
        @output = Markit.new.find_quote(@symbol).output
        if @output["Error"]
          response.add_speech("I'm sorry, I couldn't find that listing.  
          I provide quote information for most widely traded companies 
          by their symbol, like AMZN, or TSLA. Which quote would you like? ")
        end_session = false
        else
          @ltp = @output["StockQuote"]["LastPrice"]
          @change_float = @output["StockQuote"]["ChangePercent"].to_f
          @change = @change_float.round(2).to_s
          @name = @output["StockQuote"]["Name"]
          
          if @change_float > 0
            @change_sign = "up"
            @changestr = "#{@change_sign} #{@change}"
          elsif @change_float < 0
            @change_sign = "down"
            @changestr = "#{@change_sign} #{@change}"
          else
            @changestr = "unchanged"
          end
          
          response.add_speech("The last traded price of #{@name} is 
          #{@ltp}, #{@changestr} percent")
          @card_string = "#{@ltp}, #{@change}%"
          response.add_hash_card( { :title => @symbol, :content => @card_string } )  
        end
      end
{% endhighlight %}
## Results
My skill accomplished what I set out to do although  I did run into limitations on quote availability and refresh timing using a free web service for financial data.

## Conclusion
Further development I've thought about for this app would be to utilize a user based context for the requests in which they could save collections of stocks in a database under their personal profile then access those stocks upon re-entering the application.  In other words, beyond requesting individual stocks, the user could ask how for performance information on a portfolio of stocks.

## Links
[github](https://github.com/gitbnw/SingleQuote)