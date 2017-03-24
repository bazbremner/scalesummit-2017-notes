The problem is as the organisation scales is that host level
monitoring is either noisy or not helpful. Understanding the service
as a whole is much more useful, but harder to work out.

Are people doing cluster/system level alerting. How do you do RCA?

One org try to monitor and alert on business functionity. That's
required writing services that can do monitoring.

Publishing system: monitoring checks that content appears against each
API. Combined with synthetic requests.
End to end working like that is really valuable.

Synthetic requests are another internal service. Re-publish an old
article and check that the article's time is updated.

So what if you can't really do it? Working with payments systems, it's
hard to monitor real transactions.

One suggestion is to pay for a fake product and refund it. Turns out
this really upsets fraud detection systems.

Monitoring users going through a checkout funnel. Watching a mix of
application side and (in this case) paypal responses. Ratio of
requests and responses can be very different when there are problems.

Watching transaction status as they go though a process can be
helpful.

Engineers add more value if they focus on high level
tests. Hosts/containers are disposible.

When there is a problem at the system level, original person would
like to know what happened.

Another team have written their own tooling to write rules to collapse
alerts from system level alerts to relate them to user-affecting
alerts.

So, are we all doing an excellent job of monitoring then? ;)

Turning of Nagios emails was a big win for one team.

Engineers are rotating through improving alerts. If there are no
alerts improve things.

What is the user need? Can your monitoring tell you which user need
isn't being satisfied? Alerts that tell you that seem a real
improvement - seems much more common to do this.

Not alerting (especially out of hours) providing that users can still
do what they want to do can be a big win - cuts down on alert fatigue
and disrupted sleep.


Back to the original point: It is very hard to map that a user cannot
do something with - for example - Cassandra compaction taking too
long. Does anyone have ideas?

Being able to rely on the low level (instances, containers) being
picked back up helps focus on ensuring that provided that some nodes
are up and servicing users, it's OK.

On the other side, it is possible to have a problematic configuration
that causes nodes to be restarted constantly without the team going
and investigating for 6 months.

Ex: AWS EC2 machine coming up dying, being replaced every 2 minutes
yet you're getting billed for the 1st hour. 

I'd recommend when testing end-to-end, try to separate different bits
of functionality/user journeys in a way you can distinguish important
stuff from things that are not used.

Has anyone done service level monitoring to serverless systems yet?

No-one yet. No-one using serverless for heavy production loads.
One idea is to push information into logs and extract data from there.

What about things that aren't user affecting, but may become an issue,
i.e. SLAs, latency, credits. Are people still doing that?

Yes, depends on the users and the focus of your team. Also, it
transpires that no-one notices/cares, then perhaps having monitoring
on that is the right choice.

There's balancing the value that these things bring, what the relation
is like.

The closer to the metal one team gets, the more metrics around systems
they build. As it goes to a higher level, it's fluffier and harder to
track and keep an eye on things.

Apropos SLAs. Some services in one team need an out of hours response,
not everyone pays attention to that, so monitoring things that you
know will cause you to get out of bed is worth doing.

How do people monitor the things you depend on? Ex: S3 failure

End to end tests often check that, assuming you're covering all of
your functionality that hits all external providers. No need to have
specific tests.

There is an art to ensuring that when multiple tests fail, it's clear
on which particular problem they're encountering, otherwise there will
be lost time in working out commonalities.

1st line support many not have actually read the detail in alerts,
which is its own problem.

Alert fatigue is also an issue - if you seen the same alert time and
time people will overlook that alert and perhaps others. Be prepared
to turn alerts off until they are valuable (or bin them).

One team gets a (manually created) summary of all of the reports that
fired over the last 24 hours, shows patterns.
Several teams do an end-of-shift or rotation handovers.

Agreed that it would be nice to have an automatically generated report
of all alerts that fired.

Another group select 2 random developers to look at alerts, get used
new peices of the system.
Two other groups have a similar rotation - team members rotate to hand
support/on-call for a week.

Important note is that developers should leave their project work
behind/hand it over so they can focus on the support work and not be
torn.

Etsy open sourced "Ops weekly" to summarise data that the on-call
people had to deal with. https://github.com/etsy/opsweekly


