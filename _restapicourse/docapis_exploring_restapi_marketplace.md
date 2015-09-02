---
title: Exploring a REST API marketplace
permalink: /docapis_exploring_restapi_marketplace/
categories:
- api-doc
keywords: 
course: "Documenting REST APIs"
weight: 1.3
type: notes_docapis
---
{% include notes.html %}

## Our course scenario: Weather forecast API

In this course, we're going to use an API in the context of a specific use case: retrieving a weather forecast. By first playing the role of a developer using an API, you'll gain a greater understanding of how your audience will use APIs, the type of information they'll need, and what they might do with the information.

Let's say that you're a web developer and you want to add a weather forecast feature to your biking site. You want to allow users who come to your site to see what the weather is like for the week. You want something like this:

<img src="{{ "/images/restapicourse/restapi_windycall.svg" | prepend: site.baseurl }}" alt="Wind meter conditions for website" />

You don't have your own meteorological service, so you're going to need to make some calls out to a weather service to get this information. Then you will present that information to users.

## Get an idea of the end goal
{{activity}}
To give you an idea of the end goal, here's a sample. It's not necessarily styled the same as the mockup, but it answers the question, "How windy is it?" Click the button to see wind details.
{% if site.print == false %}
<style>
   #wind_direction, #wind_chill, #wind_speed, #temperature, #speed {color: red; font-weight: bold;}
</style>
  
<script>
function checkWind() { 

var output = $.ajax({
    url: 'https://simple-weather.p.mashape.com/weatherdata?lat=37.354108&lng=-121.955236', 
    type: 'GET', 
    data: {}, 
    dataType: 'json',
    success: function(data) {
        $("#wind_speed").append (data.query.results.channel.wind.speed);
        $("#wind_direction").append (data.query.results.channel.wind.direction);
        $("#wind_chill").append (data.query.results.channel.wind.chill);
        $("#temperature").append (data.query.results.channel.units.temperature);
        $("#speed").append (data.query.results.channel.units.speed);
        $(".units").show();
        },
    error: function(err) { alert(err); },
    beforeSend: function(xhr) {
    xhr.setRequestHeader("X-Mashape-Authorization", "uvkVLfg5opmshlI7b2R7cCMUFkj2p19Vomhjsn8DUilYqeRp3u");
    }
});  
}
</script>
{% endif %}

<button type="button" onclick="checkWind()" class="btn btn-danger">Check wind conditions</button>

<h2>Wind conditions for Santa Clara</h2>

<b>Wind chill: </b><span id="wind_chill"></span> <span id="temperature"></span></br>
<b>Wind speed: </b><span id="wind_speed"></span> <span id="speed"></span></br>
<b>Wind direction: </b><span id="wind_direction"></span>

{% if site.print == true %} 
{{note}} Obviously, PDF doesn't support the HTTP protocol, so you'll need to go online to <a href="http://idratherbewriting.com/docapis_exploring_restapi_marketplace/">Exploring a REST API marketplace"</a> to view this example.{{end}}
{% endif%}

When you request this data, an API is going out to a weather service, retrieving the information, and displaying it to you. 

Of course, the above example is extremely simple. You could also build an attractive interface like this:

<a href="https://weather.yahoo.com/united-states/california/santa-clara-2488836/"><img src="{{ "/images/restapicourse/attractiveinterfaceweather.png" | prepend: site.baseurl }}" alt="Sample weather interface" /></a>

## Find the Weather API on Mashape

{{activity}}

Mashape is a directory where publishers can publish their APIs, and where consumers can consume the APIs. Mashape manages the interaction between publishers and consumers by providing an interactive marketplace for APIs.

<img src="{{ "/images/restapicourse/mashape_explore_apis.png" | prepend: site.baseurl }}" alt="Explore APIs at Mashape" />

You're a consumer of an API, but which one do you need to pull in weather forecasts?

Explore the APIs available on Mashape and find the weather forecast API:

1. Go to [mashape.com](http://mashape.com) and click **Explore APIs**.
2. Try to find an API that will allow you to retrieve the weather forecast.

    As you explore the various APIs, get a sense of the variety and services that APIs provide. These APIs aren't applications themselves. They provide developers with ways to pipe information into their applications. In other words, the APIs will provide the data plumbing for the applications developers build.

3. Look for an API called "Weather," by fyhao. Although there are many weather APIs, this one seems to have a lot of reviews and is free.

    <a href="https://www.mashape.com/fyhao/weather-13"><img src="{{ "/images/restapicourse/weatherapi_mashape.png" | prepend: site.baseurl }}" alt="Weather API on Mashape" /></a>

## Answer some questions about the API
{{activity}}
Spend a little time exploring and getting to know the features and information this weather API provides. Click **Test Endpoint** and see what kind of information comes back.

Answer these basic questions about this weather forecast API:

* What does the API do?
* How many endpoints does the API have?
* What does each endpoint do?
* What kind of parameters does each endpoint take?
* What kind of response does the endpoint provide?

These are common questions developers want to know about an API.


{{tip}} Sometimes people use API to refer to a whole collection of endpoints, functions, or classes. Other times they use API to refer to a single endpoint. For example, a developer might say, "We need you to document a new API." They mean they added a new endpoint or class to the API, not that they launched an entirely new API service.{{end}}
