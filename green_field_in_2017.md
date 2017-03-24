Proposal/question: every year, there's something new at Scale
Summit. Microservices, Sensu etc in the past.

What does green field look like in 2017?

Provisioning servers, best practices, deployments, logging,
monitoring, what would you do now?

What if you're _not_ using AWS? Should you just do that? Would prefer
not to just have a list of AWS providers.

Show of hands, about 75% are on AWS.

2 said they wouldn't use AWS now, although they are currently on it.
One around compliance reasons - knowing who can have access to
data/machines etc.
Another are running in China, running on Alibaba, AWS harder to get
on.

One person mentioned that Google Cloud and related products sound
interesting. Same person is not on GC or AWS, looking at both. AWS
feels like a "no-one got fired for buying IBM of the current age".

GC feel like they're behind on managed services - for example, a
managed PostgreSQL.
IAM feels like a real weakness with GC.

If you're running multiple platforms, then you're often forced to meet
the lowest common denominator.

GC is cheaper, but it's missing a lot of things.

One person thinks GC might be offering 1st line support for free if
you meet a set of up-front standards, though if you _can_ meet these
standards, you are probably mature enough that you have SREs.

Sounds like Google are positioning Kubernetes as the abstraction
layer, but you can run on AWS, GC or others, Google gets business that
way.

Is anyone looking on Lambda or similar if you're starting a green
field (which is what this session is about)?

Yes, says one person, have just started there, but it's working well
so far.
"everyone has a function. Functions, functions for everyone!"
(paraphrasing a little).

Making sure you're _not_ special should be your first action if you're
starting now.
You are not special, you just need to realise that.

High level services can be a good place to start - Lambda, Elastic
Beanstalk etc.

Defer decisions until you can learn what you need on new projects. Use
the high level services to help.

Are we all doing microservices? Do you want to spend the 1- to 2-
thirds overhead to run a microservice model?

One answer: depends on the team and the under standing of the problem
space. If it's a well know problem, and a good team, perhaps.
If the problem is unknown, refactoring across microservices is hard to
model the problem space.

Does it have to be binary? Extract functionality as you understand it.

One platform has a mix of very small, simple microservices
(i.e. issuing tokens and checking their validity), with a
mini-megolith with the business logic it in whilst that problem space
is being explored.
Planning on breaking that up as the problem better known.

Can take a good set of developers to write, good interfaces etc. But
microservices isn't going to save you here, nor will a monolith.

Write clean interfaces - ask yourself: "should this be a
library". Then it's easier to pull it out into a microservice.

One of the mistakes one person has seen is not to throw too many
people at the problem is throwing too many people in. Try to start
with a small team (where small = 5 people - the whole team, BAs,
product, developer). This makes moving faster easier, more context,
fewer communication overhead etc.

Having a small company might force/help some decisions - for example,
choosing Lamdba might help you not worry about a lot of things.

Mention of Etsy - choose boring technology. http://mcfunley.com/choose-boring-technology

Lamdba _is_ a boring technology. A few people agree with this. There's
magic under the covers.

"Greenfield 2017 - No Javascript!" There was applause.

But how do you do that if you're on the web? HTML!

Mention of GOV.UK not using much Javascript to mean accessibly needs
and degrading gracefully.

So what language would you use?

Python is a good chance - person saying this didn't have someone come
from other language that complained.

It depends on the team - choose what works for the people you
have/have hired - remember this is greenfield.

Let's not get into language wars.

So, just run everything on Lambda and go home? ;)

Lamdba can do ~2k req/s out of the box, but you can scale up.

Going back a bit AWS vs Google is partly an economic decision. Cost
control in a new project is often a good idea - get more runway to
explore the problem, work out what you need to build and ship.

There's opportunity cost too. You _can_ just throw money at the
problem.

Someone asked if anyone does rearchitect based on cost drivers. "What
cost? Developer time, AWS bill, etc". So, are you trying to avoid big
AWS bills, or are you trying to avoid getting paged at night?

Small company: as long as my AWS bill is cheaper on my developers
that's fine. Would rather have the developers focus on building things
than spend time shaving small percentages from an AWS bill.

Original poster is not on AWS, had lots of hardware everywhere, has
consolidated on one provider. Now looking at AWS, but that's a big
move. There's also all the sunk cost. AWS doesn't feel smaller.
Original poster is consuming a firehose of data.

Anyone using petabytes of data that are in the cloud?
One response: baseline load on their own hardware and scaling up and
dealing with seasonal peaks with AWS. Compute and more interesting
storage costs are coming down in cloud to become much closer in price.

Getting data near users is a very good use for the cloud - until
companies build datacentres in Brazil, China, wherever, cloud is the
way to go.

Talk about security and how much you trust Google, AWS etc. Generally
people trust people. Block encryption under the covers. Random smaller
cloud providers, it's up to you to work out how to do that yourself.

Moving on, what about supporting services, monitoring, logging etc.

Cloudwatch is terrible. One team just shoving things into Logstash.

OP is using Influx and driving monitoring off the back of that.

New Relic gets super expensive super quickly. Other people are running
Data Dog, does seem cheaper.

One person using AWS X-Ray, works.

At a small size, (4 devs, 4 ops), tools like New Relic really paid off
to find problems quickly. It's harder to justify the cost vs dev time
as you grow.

So, how do people make that trade off of build/buy? Mostly seems pain
based. Next session is buy vs build.

Has anyone looked an Influx vs Prometheus? Prometheus has great ingest
performance. At the time, Prometheus had a linear projection function,
which Influx added later.
If you're doing a lot of requests, Prometheus is probably a better
bet.
Seems to be a lot of competition between the two.
