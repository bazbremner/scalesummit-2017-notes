What is it people build around Terraform, CloudFormation and similar
tools.
OP uses CloudFormation orchestrated with Ansible. Use some Terraform.

How should I organise my code? How should I coordinate things if I've
got 20 bits of code? How should I be testing it?
How do you get your infrastructure orchestration to the point that
you're comfortable?
What's beyond hello world?

One service provider have migrated from Cloud Formation to
Terraform. Probably using about 50% of all of the Terraform providers.
Separate runs for DNS, infrastructure, networking.
Use tfvars files for each environment.
Use a "terrafile" which is a bit like bundler/Gemfiles for Terraform
modules. Have a wrapper that pulls modules into directory.
Test with rspec, just test against a terraform plan. And use
Jenkins to run make and then Terraform plan/apply.

Use GitHubs PRs, expect devs to supply the output of the plan as part
of the PR.
Each Terraform module is a separate git repo. The one repo
approximately per one VPC that pulls this code in.

Use remote state or data sources to link results of different runs.

So: how do you walk the graph if multiple runs affect each other?

Jenkins jobs are running plans against all environments and different
layers of runs, to ensure changes have actually be applied every
where. "Janky tooling over the top"

This appears to be the stage we're at at the moment.

I recommend people read Charity Major's blog posts on Terraform if
you're just coming at this problem: https://charity.wtf/tag/terraform/

What happens if modules are updated? Up to each project to decide if
they want to update.
Have two module paths: local modules, which are vendored/janky bits
and then the "Terrafile" for pulling in external modules.
The local modules is useful to be able to see what's being
over-ridden, see if there are common patterns occurring.

Moving in a different direction: is there anyone that's using
Terraform or CloudFormation and automatically test that, perhaps in
another AWS account and check that what they expect to happen does get
applied.

One team run team is using AWS spec to check that resources that were
expected that were created.

Another team look at a Python library called Terraform Validate that
allows you do some consistency checking without spinning anything up,
but at the end of the day you really need to spin something up.

Atlassian have open sourced "local stack" which mocks a limited number
of AWS APIs.

What do people do if there's no support in a provider?

- AWS CloudFormation stack support in Terraform.
- exec resources (but you probably don't want to do this)
- Terraform external providers are a better alternative to execs.

Is anyone using pipelines for deploying?

[sorry, missed a little bit here]

Discussion moved on to adding and removing IAM permissions from the
user running Terraform to limit accidental deletions for example.

Concerns about setting up too much permissions in IAM. Locking down to
different IP addresses.

Within Terraform AWS provider blocks, you can specify AWS account IDs
to prevent applying changing to production or another customer by
mistake, for example.

Another group create very targetted IAM policies to each service that
walks the tree of all of the resources created by a human and then use
that policy after the initial run.

Some people looking at grepping Terraform source or better still the
debug log and work out how to build a IAM profile from that.
Alternatively, reconstruct from CloudTrail logs.

Who was running CloudFormation and is now on Terraform and do you have
legacy code? (About 4-5 put their hands up, out of 50).

CloudFormation was all JSON, no changesets, hard to work with. (About
18 months ago). Haven't replaced everything.

Nice bits of CloudFormation:
- CloudFormation abstracts the nastiness of RDS API.
- Autoscaling rolling updates. UpdatePolicy in LC, Terraform doesn't
  support this.

Workflow on CloudFormation is very proscriptive.

Another team are using generated CloudFormation from another tool, but
it's pretty hairy, especially around IAM policies.

Troposphere mentioned, appears to be a tool that's generating
CloudFormation. Anyone doing something similar?

One team taking YAML and generating Terraform for multiple DNS
providers.

Cumulous is another tool mentioned.

Anyone using something that's not Terraform, CloudFormation?

One person using Arm Templates for Azure. APIs seem terrible.
Terraform support for Arm Templates seem good. Terraform doesn't seem
to support Azure in "a better" way is because of upstream SDKs don't
support it, Microsoft don't seem to be publishing Swagger files for
those APIs. Person has a Trello board with all the issues they've seem

CloudFoundry users would use Bosh.

Show of hands, how many use CF or Terraform for managing production:

About 5-10 for each. Lots of other people in the room.

Who is using other people's Terraform modules: zero hands.

Who has heard of and use the community modules? A couple of people use
them as a reference only.

Gruntworks have a blog post about the ugly bits of Terraform and
potential (nasty) workarounds. Part of this series:
https://blog.gruntwork.io/a-comprehensive-guide-to-terraform-b3d32832baca#.4910unu4e

Why don't think modules are good enough?

Puppet/chef etc, use lots of attributes to change the behaviour.
For something like an ASG, it's pretty much every parameter.

I've not seen good examples of people composing modules from other
modules. Seems problematic. Others agree that is still a problem.

Understanding the impact of a low level module changing is very
difficult.

Passing inputs and outputs with layers of modules is very difficult.

I consider if it's worth templating out the Terraform code in a full
blown language and feed that to Terraform. Terraform's JSON input is a
route to this.

Terraform _does_ support conditionals, but only a single line, and
this doesn't pan out if things are optional.

Some discussion about Helm vs Terraform, seems they're solving
different levels of difficulties. And we're out of time.
