I would like to know how teams handle their deploys. How are they
automated, fast, safe, how are rollbacks handled, how do you avoid
excessive coordination and assumptions etc.

450 services, continuous deploys. Looking to get to 10k deploys a
day aspirational. Actually at a few hundred a day. 

One of the first thing was to have declarive pipelines. Used YAML to
model pipelines.
Another principle was zero click deploys. Use Drone. "It's been
alright". Auth model is terrible, tied to git access etc.

So, code flows through the pipeline. What are the steps and how do
things get to the next step?

Not actually enforcing automated tests, but it is obviously good
practice.
Some "discussions" around experimentation being an excuse not to
test. Cultural issue.

Sally Godel from the Guardian has a good talk about not running tests.

There are no staging environments. Dev environments (devs are expected
to be able to spin up dependancies for their microservice). UX testing
is hard, slow.

Have blue/green deploys.

Do you have any post-deploy smoke tests etc? Much of this is done with
existing monitoring.

Blue/Green deploys, but the newest deploy doesn't get any traffic,
then synthetic requests, then bleed over production traffic. Still
building out this logic right now, and trying to work out what the
decision point is.

What about other people? How to you avoid having people sitting there
clicking buttons and watching things.

On PR merge, build, package, deploy all the way to pre-prod. Depending
on acceptance tests to give confidence. Deploy to live is enabled only
when the tests pass.

Do you get a queue of deploys?

Yes, that does happen, but there's no good answer yet.

Do you have a time limit on acceptance tests? No limits right now,
tests are generally fast, so it's not been an issue.

What are people doing when code hits production? Canary, big bang,
validation, what are people doing?

One team has the usual pipeline, but they make a lot of UI changes...
For big-end backend changes, then deploy the branch (ahead of any
merge) - 100% production traffic and monitor for an hour or two.

Another team with a LAMP stack use a special header to do gradual
routing on that header to different versions of the code.

Netflix for example will use 5% canarys and watch the
metrics. Provided new code is within limits, it's promoted.

Guardian had matrix of user journey vs software versions. Customers
are really good at testing your sofrware.

Amy Hughes talked at Pipeline (?) about doing statistical analysis on
new releases. Didn't get the details on this.

One team tag AWS instances to be able to be able to identify issues.

Being able to run multiple versions of code is very useful.
Feature flagging is worth investigating
Poisoning session caches is hard to do - if you're changing the shape
of data in caches is difficult.
Running multiple versions makes rolling back much easier, especially
if you're routing traffic.

How to deploys go wrong?

- DB schemas are fun
- Caches
- Anything persistent data issues

One team deployed once every 2 weeks many years ago. Handed it over to
ops team to deploy using a 30 step process. Moved to a continuous
deployment.

Looked at database change scripts to work out if there were any
non-backwards compatible schema changes. ~90% were OK to deploy and
the remaining 10% could have been written in a way to be backwards
compatible.

Persauding the team this was possible was one of the bigger issues.

Smaller changesets made a big difference. Making new code to read old
DB schema, update schema, update code was much easier to understand
when everyone was deployed when things in a short period of time.

So, how did you make sure that the code and DB versions work together?

Test environment had anonymoised production data. Could replay
production access logs against it. Deploy DB update, test, deploy
code, test.
Put out comments that "Rollback wasn't a thing, stop it".

MBS wrote a blog post about DB migrations done probably a while ago.
ORMs can make migrations every difficult, and provide empty
rollbacks. Doesn't exactly work when you DROP COLUMN :)

Don't pretend you can rollback.

Does anyone enforce how often old data has to kick around for safety
and backwards/forward compatibility?

plus/minus 1 version.

Customer's shouldn't notice deploys.

Another team support many (5) versions of APIs, keep the data around,
it's all managed in code.

How do you avoid coordinating backend vs frontend dependancies?
i.e. don't deploy/have issues with deploying a frontend that depends
on a backend that's not been deployed yet?

Answers: build that into your service discovery at deploy time -
discover if what you need is already there.

Developer teams can also think about this themselves - doesn't have to
be a technical solution.

One team clients query using a query string, not just an endpoint
(client specify which fields they expect to get back). Do validations.

Another team did something similar - baseline fields were the same,
but newer clients could request additional newer fields. Easier than
maintaining schema versions of API endpoints.

75% using Jenkin
5% team city
1 Drone
1 Codeship

Next session: is there something better than Jenkins.

Anyone using AWS CodeDeploy? Not too bad, but invocation is a bit nasty.
