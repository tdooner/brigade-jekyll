---
layout: home
---
<h2>Introduction</h2>
<p>This is a demonstration Jekyll site to show:</p>
<ul>
<li>The <a href="https://github.com/tdooner/jekyll-meetup" target="_blank">
  <code>jekyll-meetup</code> plugin</a></li>
<li>A minimal configuration for CircleCI auto-deploy</li>
<li>A sample Jekyll configuration for Github Pages</li>
</ul>
<p>The best parts to see are in <a href="https://github.com/tdooner/brigade-jekyll" target="_blank">the source on Github</a>.</p>

<h2>Usage Example</h2>
<h3>Add it to the Gemfile</h3>
{% highlight ruby %}
group :jekyll_plugins do
  gem 'jekyll-meetup'
end
{% endhighlight %}
<h3>Jekyll Configuration</h3>
{% highlight yaml %}
# Configuration settings for Jekyll Meetup plugin:
meetup:
  # download meetup events into the _data/events/ folder
  collection_name: events
  # fetch events for this meetup page (this is the part in the URL on Meetup)
  urlname: OpenOakland
{% endhighlight %}

<p>
At this point, you will have to download the Meetup events by running
<code>jekyll meetup download</code>. Doing this <a href="https://github.com/tdooner/brigade-jekyll/blob/1f89b6105c93f91f411cdd83d8d66acc80230459/.circleci/config.yml#L27" target="_blank">right before the build command</a> is a great time.
</p>

<h3>Using it in the view</h3>
{% highlight liquid %}
{%- raw -%}
{% assign event = site.data['events']['upcoming'] %}
<h2>Upcoming Event:</h2>
{{ event.name }}
{{ event.local_date }}
{{ event.local_time }}
<a href="{{ event.link }}" target="_blank">RSVP on Meetup.com</a>
{% endraw %}
{% endhighlight %}


<h2>Output</h2>
{% assign event = site.data['events']['upcoming'] %}
{% if event %}
<div class="brigade-event">
  Join us at our next event:
  <h3 class="brigade-event__name">
    {{ event.name }}
  </h3>

  <p>
  {{ event.local_date | date: "%A, %b %-d, %Y" }}
  @
  {{ event.local_time | date: "%-l:%M%P" }}
  </p>

  <div>
    <a href="{{ event.link }}" target="_blank" class="brigade-event__button">
      RSVP on Meetup.com
    </a>
  </div>
</div>
{% else %}
{% if jekyll.environment != "production" %}
No upcoming events. Maybe you need to run:
<code>
bundle exec jekyll meetup download
</code>
{% endif %}
{% endif %}
