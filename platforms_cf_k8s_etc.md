Proposed because: people were talking about building things with
sensible defaults. The answers varied quite a lot.
There's hardware, with long lead times, going to the cloud and
building lots of snowflakes is no good either.
"Just" spinning up Kubernetes is harder than people make it out to
be.

One team are running Kubernetes (k8s). A consistent API for teams is a
good thing. It was a lot of blood, sweat and tears. APIs aren't stable
yet.  Very little has hit the stable API layer at the moment.

100 people, few years old. No traditional infra history. 4 people
building and running Kubernetes. 60-70% of time as been Kubernetes
wrangling.

They were running on Fleet, it was deprecated. Org was growning fast,
needed to be able to service many teams in a consistent way. k8s seems
like the most viable choice.
"Batteries included, once you work out how to put the batteries in".

Using raw k8s. Have been modifying this and effectively building their
own distribution.

Another team have a lot of ECS clusters, looking at k8s at the moment.

k8s has has different network ranges: node, POD, service and another
range. Service range aren't routed in AWS, GCE etc. That's not best
practice, this team have requirements to route these, hence changes.

Another team looking at 1000 node+, looking at Calico for
networking. Already at 100 notes.

Who in the room is running a "platform" (i.e. CloudFoundry, k8s
etc)? 4-5 people put there hands up, in a room of ~35-50.

One team moving from a platform they effectively built themselves.

So, is this the future direction?

Probably 60-70% of room put their hands up.

More background: UK Government have multiple PaaS - docker,
CloudFoundry. US Government have chosen CF, what else is out there.
Running CloudFoundry takes ~20 instances. Needs people to run.

Question/point from elsewhere: is running a PaaS really a
differentiator? Should you really be running that?

Kubernetes seems to be a good safe option and managed to move across
multiple cloud providers.

Has anyone used Marathon or Mesos or Desos?

A few people have looked Desos was dropped out of one trial
quickly. Mesos seems to be in a bind, not a big dev community. As a
do-everything platform it's outnumbered.
Lots more people at Pivotal working on CF. Docker have "all the
cool". Google are effectively giving k8s away.

Using Mesos for scheduling work, it's good. To handle application
workloads, it's not designed for it and being outpaced by the
competition.

Question: has anyone looked at these platforms and decided not for us.

A: yes, moving running systems, it's a hard sell if you have a running
system. For a greenfield system, maybe, but as discussed in the
earlier greenfield session (see my notes in this repo) then you
probably want to choose a higher level option rather than sink time
into platforms.

I'd quite like something that's not that is not _as_ complex as a full
plaform. I have some compliance issues. One suggestion was AWS Elastic
Beanstalk.

Dcoker Swarm seems troublesome.

Question: is anyone packing images onto instances? Also, is anyone
experiementing with Convox?

No Convox answers.

One team packing containers on instances with Docker Swarm. Got
something up and running 3 people in a week.

Someone else said Docker Swarm was a good way to get people to think
about how to the world will look before they move to k8s. Got laughs,
but seems like a good approach.

If you want to get going to try k8s, highly recommendation minikube or
kubeadm.

So, how to you progress that? How do you go from kops to running
something in production and support that and know how to debug it.

Easier commenter running k8s is thinking of this now. Have
qualification tests and run that on top of the platform. Understanding
how that fails taught them a lot.

So, how do you debug and fix things at 2AM when you're called out?

Most problems seem to occur around rollouts or AZ doing down in the
cloud provider. k8s seems to self-heal pretty well.
This team built it from the ground up, so it's very different from
using kops.

Pivital have released kubo recently. CloudFoundry will run docker
containers if you want to.

If you're shipping containers, then k8s is good for that.

Google will certify platforms for a number of nines
availability. CloudFoundry apparently certified for 99.99% and Google
will do 1st line support.

Many people treat their plaform as the way they treat their existing
systems or IaaS. They seem to want to change the low level. Is anyone
running a vanilla solution.

One team running Elastic Beanstalk, single container on a single
instance. It's just EC2 glue. Looking at building newer things on k8s.
Multiple container Elastic Beanstalk is ECS.

If you're going to run a platform, you either move to it, or you don't
mess with it at all.
When you start modifying the platform, you're probably setting
yourself up for failure.

Upsteam k8s is a framework to run your platform. You have to bring
opinions. If you don't want to do this - use one of the distributions.
With the upstream, you have to think about network choices etc.

This seems to be a distinction that's not well understood.

Focus on the thing that provides value for your customers. If running
a platform doesn't deliver value, don't do it.

So, you you stick with the vanilla boring things and work down as you
need to?

Using Elastic Beanstalk and embracing its limits has been useful.

So: which distribution and why? Is there one coming out on top?

It's too earlier to tell.
"People on the internet are running upstream"
Commercial market is still pretty small.

Feels really gold-rushy at the moment.

Cloud Native Computing Foundation was useful place to look at for
solutions that might fit together with k8s.

Cap Gemini pitching their own distribution. Have another platform
'Apollo'. HP has something similar.

When building a platform, we need to build teams. What skills are
available?

Ask yourself if you should be running that 3-5 years - should you wait
2 years and move to a hosted solution?

Different groups will want to run the bleeding edge of things. We're
perhaps a little more cynical and real world ;)

Are people starting to upskill. Do I need to train people?

If you want to keep your costs down, yes, hire a couple of contractors
and have them train your team. If you want to hire a lot of people,
it'll be expensive.

You should think before spinning up a new team. Try Pivotal Web
Services (PWS), use GCE, Heroku, use something else. You shouldn't
need to spin up a team to run this stuff.

What does operations look like for application looking like on
platforms? There's still configuration, but there's a line that is the
platform.

App-ops might be a good thing for a later session. It's lunch time!



