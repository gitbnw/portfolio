---
layout: post
title: Blocipedia
thumbnail-path: "img/blocipedia.png"
short-description: A Ruby on Rails app built with a TDD approach that makes use of the gems- devise, pundit, and stripe.
order: 5
---

{:.center}
![]({{ site.baseurl }}/img/blocipedia.png)

## Explanation
A wikipedia-like app for posting and editing articles.  Users can upgrade their account permissions via stripe payment in order to create private wikis and collaborate with other users on the site. 

## Solution
Followed a TDD approach in setting up the pundit permissions to limit private wikis to users with upgraded accounts.
{% highlight ruby %}
require 'rails_helper'
require 'pundit/rspec'

describe WikiPolicy, type: :policy do
  subject { WikiPolicy }
  
let(:current_user) { FactoryGirl.build_stubbed :user }

  permissions :update?, :edit? do

    it "grants access if wiki is not private" do
      expect(subject).to permit(current_user, Wiki.new(:private => false))
    end
    
    it "does not allow access to private wiki" do
      expect(subject).not_to permit(current_user, Wiki.new(:private => true))
    end

  end
end

{% endhighlight %}
<!--## Conclusion-->

## Links
[github](https://github.com/gitbnw/blocipedia)