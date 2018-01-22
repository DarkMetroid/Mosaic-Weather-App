PART 2
1) To add dynamic capabilities to the app my first course of action would be to
set-up Users so that someone could have an account and permanently store their
settings. This'd ensure that they could log-in on multiple machines without
worrying about losing their preferences. Seems like overkill to make a log-in
mandatory for a weather app so I'd probably default to saving things in local
storage or cookies (depending on the particulars of the requirements).

For things like hiding/showing data or say changing unit types, I'd locally
have these preferences in a json block (or some data structure) and
conditionally hide/show the data accordingly (maybe a true or false flag for
different categories). I'd have a separate json block/data structure for
positioning of categories mapping each category to where the block should be on
screen (maybe grid coordinates if using a grid system).

Adding options next to every field on the UI could get messy, so I'd have modal
listing options with on/off switches and dropdowns where appropriate, and then
once the user submitted reload everything.

2) In terms of architecture I'd add a tag with the city name at the top-level
of my weatherData field, that way we can store the data for multiple cities.

I'd display each city searched using a bootstrap 'card', and just have them
automatically stack up as the user searches (with a close button in the top
right corner to close one). The newest search would appear at the top left
of the page(i.e. first). If we support multiple locations it probably makes
sense to wipe the input from the search bar after the user submits so they can
quickly submit multiple searches. We'd want a loading indicator to ensure they
don't mistake api slowness for non-responsiveness, and we'd probably restrict
things so there's only 1 API call happening at a time (shouldn't reasonably
be a problem, but makes sense to handle for it). If an item is searched for
while already displayed we should remove the existing instance, and add a
new (updated) block for it as if it was a new search.
