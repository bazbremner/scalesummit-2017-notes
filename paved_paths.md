Do we want a chosen set of technology?
And if you do, then how do you end up renewing that year after year?

Old tech may be a retention and recruitment problem - if people want
to work on new tech, then they may leave to do that.

Yes, there are some people who want to play around with new things,
but letting that trump everything comes at a cost.

There's a balance between organisational stability and employee
happiness.

"Bi-model IT" - the new shiny and the old stuff. If you have one team
that gets to work on the new shiny, everyone else hates them.

If you're expecting a team to do out of hours support, then you can't
force them to do that, if it's not the right tool for the job.
If something is cool and useful, then they will use it, but they have
to be able to support it.

How do you 'nudge' teams towards good behaviour. Look at "nudge unit"

If you make things easy, accessible, timely, social

- selfservice
- Well documented
- Make it easy
- Social: if others are doing it and say it's great, think about
  lightning talks, examples of why it works for them can persaude
  others to go the same way.
  
For out of hours support: is each team doing their own out of hours,
or is there an ops team.

1st line support react to things going read
2nd line for escaltion
3rd line

Lots of different languages to support, complex to pay people to
support all of these things.
Runbooks, ways of reporting incidents. You can set standards around
this.

Recommendation shout out for Susan J Fowler's Production Ready
Microservices around setting standards for what a good service needs

Organisation here is around things like runbooks, monitoring etc.

If you're going to phone people up, they're more interested in
creating runbooks. Your future self needs a runbook about what you're
doing today.

If you don't do out of hours support for your own service, you'll
build a worse system.
Make sure you empower teams to fix and address problems.

Getting back on topic. What about infrastructure choices: i.e. ELK,
for example.

Q: How do people change that choice?
A: normally though skunkworks, which isn't ideal.

Decisions should be recorded _with_ a life time for when it should be
re-evaluated.

ADRs mentioned
http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions

Talk of pioneer, settler, town planner teams.
http://blog.gardeviance.org/2012/06/pioneers-settlers-and-town-planners.html

Are there teams that have tried experimenting on "lower risk" areas?

Yes, but then eventually, it gets into production, and it's a Real
Thing.
If you use the new shiny on something you don't care about, then it's
hard to get invested in something.
You want to have something to have something worthy to show off.

But there are two approaches (probably more): experimenting with new
tech, but there's also that the existing stack can't solve/be bent to
handle a new need. Solving a need is a good reason to explore new
tech.

If a team is working on a new problem, they might come across a tech
that solves that problem, it makes it easier to justify.
The teams have to justify that the technology works to the rest of the
organisation. There are some principle architects who can make
suggestions. There are some strategic changes - i.e. moving to AWS.

Many teams will adopt technology quite quickly.

Dealing with the long tail is very long.

How do you get one team to sell to others?

Tooling team centrally will be approached by a team. Initial team
hopefully will have something already in a reasonable state, central
tool team will then polish and distribute to other teams to consider.

What happens if two large influential teams have differing opinions?

Principle engineers are expected to have context and deep knowledge to
be able to work these issues out. Expectation is that principles have
both breadth and depth.
This is from a service company where there is high value to
standardisation.

If two groups are talking, and they have a difference in opinion, then
it probably _is valid_. The use cases _may_ be different.
It may be necessary to mandate changes.

What does that communication look like?

- Get people working across teams.
- Written documentation is the worst medium "the side-bar of shame in
  Google Docs".
- Run investigations.
- Product owners have to understand that teams need time to investigate
("faffing around for a week").
- Possibly having a tech radar: new tech, supported tech, deprecated
  tech.
- Service catalogues.
- Weekly demos from each engineer. Show and tells

Are teams co-located? Does that make any difference?

- 1st: 70% remote
- 2nd 4 locations
- 3rd: some colocated, other teams are outsourced

Lots of discussion asynchronously, people talk on Slack etc.

There are different sorts of people: magpies, planners etc
Do you always have to be moving? Have a rolling wave of progress
perhaps.

Another group rotate people through a support team - you go from the
shiny teams, you're reminded that there are still systems to support.

Having roadmaps that are related and remind everyone what the common
goal is.

Start new teams for exploration, break them up to spread knowledge
around.
Make sure you're staffing such teams with people that will be around
for the longer run.

It's a different problem to explore new tech vs bringing in experts to
build something quickly.

Avoid putting people who don't have to run production services driving
adoption of new bleeding edge tech.
