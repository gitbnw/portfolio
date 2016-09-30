---
layout: post
title: Bloc Jams Angular
thumbnail-path: "img/blocjamsang.png"
short-description: A music player built with AngularJS, grunt and Node.js.
order: 3
---

{:.center}
![]({{ site.baseurl }}/img/blocjamsang.png)

## Explanation
This was some of my first exposure to building a front end with AngularJS and I'm eager to learn more.   The data binding is probably the main draw for me.

In this project we created a music player demo.  The control interface uses a directive template for its volume and song position seek bars.  To accomplish having the control remain accessible as a utility for different parts of the application, i.e. not tied to one particular function, the directive uses a binding expression 'onChange'.

## Solution
A partial look at that directive:
{% highlight javascript %}
(function() {
    function seekBar($document) {

        return {
            templateUrl: '/templates/directives/seek_bar.html',
            replace: true,
            restrict: 'E',
            scope: {
                onChange: '&'
            },
            link: function(scope, element, attributes) {

                var seekBar = $(element);

                scope.trackThumb = function() {
                    $document.bind('mousemove.thumb', function(event) {
                        var percent = calculatePercent(seekBar, event);
                        scope.$apply(function() {
                            scope.value = percent * scope.max;
                            notifyOnChange(scope.value);
                        });
                    });

                    $document.bind('mouseup.thumb', function() {
                        $document.unbind('mousemove.thumb');
                        $document.unbind('mouseup.thumb');
                    });
                }
                var notifyOnChange = function(newValue) {
                    if (typeof scope.onChange === 'function') {
                        scope.onChange({ value: newValue });
                    }
                };
            }

        }
    }

    angular
        .module('blocJams')
        .directive('seekBar', ['$document', seekBar]);
})();


{% endhighlight %}


## Links
[github](https://github.com/gitbnw/bloc-jams-angular)
