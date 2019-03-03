---
title: Want doing a load test? use Artillery
summary: we are already familiar with Jmeter, but there's a more simple tool to doing that
layout: default
comments: true
---

as we already know, load test is a kind of Performance Testing which determines a systems performance under real-life load conditions. let's say you have an ecommerce website with daily user active 100K user per hour or you have an app with more than 100K api call per hour.

Then marketing team have a plan to doing some promotion in your app/website at 6 pm, then we can predict there will be a spike in your active user during that time. As an engineer we have to prevent that a suddenly spike of user. If you're already using microservices and serverless system might be that problem is getting easier for now (Thanks to kubernetes). But still we need to make sure the API endpoints are tough and reliable during peak time, with load testing at least we are giving confidence level of performance. 

So, The basic concept of load testing are, we sending of X amount request per X time from X user.

What are the common tools for load testing? Jmeter is battle proven for doing load test and well known, but the UI is so confusing. There's another alternative, called [Artillery](https://artillery.io/). if you're familiar with python, there's [Locust](https://locust.io) to doing the same thing. Artillery are javascript based and have very minimal interface, it's using CLI.

to install it make sure you have a latest version of node and NPM.

{% highlight javascript %}
npm install -g artillery
artillery -V
{% endhighlight %}

to doing a simple load test we can type this command

{% highlight javascript %}
artillery quick --count 10 -n 20 http://google.com
{% endhighlight %}

This command will create 10 "virtual users" each of which will send 20 HTTP GET requests to google.

and then this is the result

{% highlight markdown %}
Started phase 0, duration: 1s @ 04:21:07(+0700) 2019-03-03
Report @ 04:21:11(+0700) 2019-03-03
Elapsed time: 4 seconds
  Scenarios launched:  10
  Scenarios completed: 10
  Requests completed:  400
  RPS sent: 103.09
  Request latency:
    min: 36.9
    max: 192.1
    median: 67.2
    p95: 98.6
    p99: 155.6
  Codes:
    200: 200
    301: 200

All virtual users finished
Summary report @ 04:21:11(+0700) 2019-03-03
  Scenarios launched:  10
  Scenarios completed: 10
  Requests completed:  400
  RPS sent: 102.83
  Request latency:
    min: 36.9
    max: 192.1
    median: 67.2
    p95: 98.6
    p99: 155.6
  Scenario counts:
    0: 10 (100%)
  Codes:
    200: 200
    301: 200
{% endhighlight %}


what does it means?

- Scenarios launched is the number of virtual users created.
- Scenarios completed is the number of virtual users that completed their scenarios.
- Requests completed is the number of HTTP requests and responses or WebSocket messages sent.
- RPS sent is the average number of requests per second completed in the preceding 10 seconds (or throughout the test).
- Request latency is in milliseconds, and p95 and p99 values are the 95th and 99th percentile values.
- Codes provides the breakdown of HTTP response codes received.

also Artillery is providing running test script via .yaml file. For more info go visit their website.
