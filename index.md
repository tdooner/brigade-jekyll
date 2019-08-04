---
layout: home
---
{% assign event = site.data['events']['upcoming'] %}
{% if event %}
<h2>Upcoming Event:</h2>
{{ event.name }}
{{ event.local_date }}
{{ event.local_time }}
<a href="{{ event.link }}" target="_blank">RSVP on Meetup.com</a>
{% endif %}
