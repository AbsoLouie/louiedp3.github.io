---
layout: post
title:  "Constraint based routing in Rails"
date:   2014-06-24 16:02:22
categories: Rails Routing
---

## The Problem

I came across an interesting problem today. I was working on two sites that shared the same source code, and I needed the root path to call different controller actions. My first solution was to have if-else statements determine the right action to execute. It worked, but it felt wrong and cluttered my controller.

## Introducing Constraints

After I researched the problem I found that I could determine the route based on a constraint. Constraint in this case means a test that the request must pass.  The simplest example I have is:

{% highlight ruby %}
root to: 'Controller#action', constraints: {host: 'www.siteone.com'}
root to: 'Controller#default'
{% endhighlight %}

The code above will serve `Controller#action1` if `request.host == 'www.siteone.com'`, in any other case it will use the default. It's important to remember that the default route must come last because these constraint checks happen in order.

## Params based actions

Another use case comes in the form of executing methods based on a parameter. Say, for instance, we need to check if a user is logged in. There are plenty of ways to check and redirect a user if they are not logged in, but what if we could serve the right action before interact with the controller?

{% highlight ruby %}
class UserConstraint

  def matches?
    request.session['user'].present?
  end

end

root to: 'Controller#action', constraints: {UserConstraint}
root to: 'Controller#default'
{% endhighlight %}

If `UserContraint.matches?` returns `true` then `Controller#action` will execute, if not the default will occur.

###### Resources

[How to use rails route constraints](http://blog.8thlight.com/ben-voss/2013/01/12/how-to-use-rails-route-constraints.html)
<<<<<<< HEAD

=======
>>>>>>> 93457c986ca1cf489b2008cf2c3e6cd8336242da
[Using Routing Constraints to Root Your App](http://viget.com/extend/using-routing-constraints-to-root-your-app)

