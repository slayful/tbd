---
date: 2016-12-01T20:08:11+01:00
title: Game Changers
weight: 121
---

Since the early 80's a number of things have pushed best practices **towards** Trunk Based Development, or **away** from it. 

The language in use to describe such things has changed over time. Software Configuration Management (SCM) is used less 
today than Version Control Systems (VCS) is. A simpler still term -"Source Control" - seems to be used more recently, 
too.

Similarly, 'trunk' and 'branch', have not always been used as terms for controlled code lines that have a common
ancestor, and are eminently (and repeatably) mergeable.

## Revision Control System - RCS (1982)

RCS was a simple but 'early days' version control technology, by Walter F. Tichy.

In Tichy's 1985 paper 
"RCS - A System for Version Control"{{< ext url="https://www.gnu.org/software/rcs/tichy-paper.pdf" >}}, a trunk 
focused mode of use is described as a "slender branch". In section 3.1. "When are branches needed?", 
he says that you step away from the trunk for four reasons:

<div style="padding-left: 40px"/><span style="font-size: 120%">&ldquo;</span>
A young revision tree is slender: It consists of only one branch, called the trunk.<br>
As the tree ages, side branches may form. Branches are needed in the following 4 situations.<br>
Temporary fixes, Distributed development and customer modifications, Parallel development, and Conflicting updates.
</div>
 
Two of those, Tichy suggests, are temporary branches and would come back to the trunk at the earliest opportunity. 

Superficially, RCS allowed multi-branch parallel development, but some teams were very careful and stuck
to a 'slender', or Trunk Based Development mode of use.

Note: Over time all version control systems would adopt this branch/merge language.

## Microsoft Secrets book (1995)

Microsoft Secrets: How the World's Most Powerful Software Company Creates Technology, Shapes Markets and Manages 
People (Michael Cusumano & Richard Selby, 1995){{< ext url="https://www.amazon.com/Microsoft-Secrets-Powerful-Software-Technology/dp/0684855313" >}}

The book was translated into 14 languages, and a best seller. 

There's a section in *Microsoft Secrets* dealing with Microsoft's per-developer workflow using Source Library Manager 
(SLM) on  a one-branch model (the book does not use the words trunk or branch). SLM (AKA "slime") - an Internal 
Microsoft tool for source-control until it was replaced by Source Depot in 1998. That daily, rigorous, developer 
workflow was:

1. checkout (update/pull/sync or checkout afresh)
2. implement feature 
3. build
4. test the feature
5. sync (update/pull)
6. merge
7. build
8. test the feature
9. smoke tests 
10. check in (commit/push)
11. makes a daily build from HEAD of the shared master branch

The authors note in the book, that #10 isn't always an every day thing. And the last step, #11, isn't per developer, it is 
for the designated "build master" within the team, and manual. 

The book also briefly mentions Test Case Manager (TCM) and "Microsoft Test". These were tools for helping developers 
manage and record/edit/playback application tests at their workstations. It isn't clear if all SLM-using teams
also used these, but the Excel team did (as they maintained the former at least).

These are clearly practices to support teams working in a trunk model.

Note: In 2000, ex Microsoftee and early blogger Joel Spolsky would extol the virtues of #11 in his now famous 
"The Joel Test"{{< ext url="https://www.joelonsoftware.com/2000/08/09/the-joel-test-12-steps-to-better-code" >}}.

## Perforce's High Level SCM Best Practices white paper (1998)

Laura Wingerd and Christopher Seiwald penned this widely read paper{{< ext url="https://www.perforce.com/sites/default/files/pdf/perforce-best-practices.pdf" >}}
 (presented at a SCM conference in Brussels the same year).
 
The paper alternates between 'trunk' and 'mainline' language, but has many valuable nuggets in 
it that help set a foundation for the next ten years of version-control advances.

## Extreme Programming's Continuous Integration (1999)

Kent Beck{{< ext url="https://en.wikipedia.org/wiki/Kent_Beck" >}} published "Extreme Programming Explained" in 1999. 
Picked out that, amongst a bunch of practices for the influential XP methodology, is "Continuous Integration" 
that Kent felt was "risk reducing".

He says "Integrate and build the system many times a day, every time a task is completed", and goes on to detail 
a reserved workstation, that a developer pair would sidle up at the appropriate moment to prove that their code 
contribution was integrateable, and therefore good for team mates to depend on at that moment. That last notification
was often oral at that time "build passes, gang".

He calls out a requirement for "fast integration/build/test cycles". This is key. In fact, every pro Trunk Based Development 
game changer listed in this page was facilitated by faster builds generally (versus a predecessor technique for the team
in question). And, no, faster did not mean delete or comment out automated test execution in the build. Faster meant reduce 
the elapsed time to "a few minutes" (Kent again).

Kent had pioneered (with many industry luminary friends) in 1996 on the famous Chrysler Comprehensive Compensation System 
(C3) project.

### Continuous Integration on MartinFowler.com

Martin Fowler and Matt Foemmel{{< ext url="http://blog.foemmel.com" >}} wrote an influential article "Continuous 
Integration" in 2000{{< ext url="https://www.martinfowler.com/articles/originalContinuousIntegration.html" >}}, 
calling out this one part of XP. Martin greatly updated it in 2006 
{{< ext url="https://www.martinfowler.com/articles/continuousIntegration.html" >}}. 
 
### ThoughtWorks' Cruise Control 
 
Martin's ThoughtWorks colleagues (Alden Almagro{{< ext url="http://aldenalmagro.com/resume.html" >}}, 
Paul Julius{{< ext url="http://www.pauljulius.com" >}}, 
Jason Yip{{< ext url="http://jchyip.blogspot.com" >}}) went on to build the then-dominant 
"Cruise Control"{{< ext url="http://cruisecontrol.sourceforge.net" >}} starting in early 2001. This was a 
ground breaking technology and very accessible to companies wanting a machine to fully verify checkins. 

Early CI servers, including CruiseControl used to have a "quiet period" to make sure they had received every last 
element of an intended commit. To facilitate that, only one pair of developers was allowed to checkin at a time. With 
CVS the other developers in the team could only do theur "cvs up" when CruiseControl had given the green light, 
automating that "build passes, gang" oral notification above. 

### Apache's Gump

Apache's Gump was built on a similar time line, but focused more on the binary integration hell of 
interdependent Apache (and other) open-source projects. It gave an early warning of integration clashes that were 
already, or were about to be problematic, for teams. While impressive, it did not gain traction in the enterprise. 
This is because enterprises were able to be more buffered from open-source library hell (and the implicit diamond 
dependency problem), by limiting the rate at which they upgraded their third-party binary dependencies.

Gump creator, Sam Ruby remembers:

<div style="padding-left: 40px; padding-right: 45px"/><span style="font-size: 120%">&ldquo;</span>
The original motivation for Gump wasn't so much continuous<br>
as it was integration - in particular, integration in the large.<br>
Many projects had unit tests but would routinely make changes<br>
that would break their 'contract' and nobody would notice until<br> 
well after the changes were released.
</div>

## Subversion's "lightweight" branching (2000 through 2001)

Karl Fogel helped start Subversion and remembers one early goal was "CVS + atomicity". **The lack of atomicity in CVS
meant that teams had to coordinate as to who was checking in presently**, and whether they'd definably broken the build
afterwards. Early CI servers (as mentioned) used to have a "quiet period" to make sure they had received every last element of an 
intended commit.

In comparison to the clunky CVS, Subversion had "lightweight" branching. This made it easier to consider multiple 
branches active in parallel and merge the team's changes back later. 

Until v1.5 in June 2008, Subversion had an inadequate "merge tracking" capability. It still has edge-case merge bugs 
today, like this one{{< ext url="https://issues.apache.org/jira/browse/SVN-4635" >}}.

## Git's "lightweight" branching (2005)

In comparison to the clunky Subversion, Git had "lightweight" branching.
This made it easier to consider multiple branches as active (in parallel) and merged back later. Git's merge engine was very 
good too, more able than prior merge technologies, to silently process complexity. 

A critical part of Git was local branching. A developer could make multiple local branches, and even map them to the 
same remote branch. Say one could be a feature, part complete, and another a surprise bug fix to go back first. Or the 
developer could be making alternate implementations of the same complicated thing, to decide later which to push back. 
Git doesn't need a centralized server repo, but enterprise teams are going to have one anyway.

As before, this made it easier to consider multiple branches as a viable team setup.

## Google's internal DevOps - 1998 onwards

Note: Google were practicing Trunk Based Development since the beginning - Craig Silverstein (the first hire) remembers 
setting it up that way. Much of these were secret to Google until much later, including their recomendations for a 
70:20:10 ratio for small:medium:large tests, where 'small' were sub-1ms unit tests (no threading, no I/O), 'medium' 
were unit tests that didn't qualify for *small* (and probably did TCP/IP headlessly to something), with 'large' were 
almost entirely Selenium functional tests. Pyramid like, and in the mid-2000's.

### Home-grown CI and tooling

This was 2002 onwards, but only barely documented outside Google, this the influence is much smaller.

Google is the most famous example of using Scaled CI infrastructure to keep up with commits (one every 30 seconds on 
average) to a single shared trunk. Google's setup would also allow the same infrastructure to verify *proposed* commits.

Their VCS technology in the early 2000's when they engineered this was Perforce, and it did not have an ability
to effectively do CI on commits that had not yet landed in the trunk. So Google made their own tooling for this and
pending commits were plucked from developer workstations for verification (and code review - see "Mondrian" below). 
After its initial creation, Google's now "Google3" setup, gained a UI Mondrian (as mentioned) 
which made the results of the pre-commit CI verification very clear. 

### Mondrian (2006)

Tools for code-reviewers/approvers of proposed contributions to trunk were developed internally in Google in the early 
2000's as a command-line tool and part of "Google 3". Things would not land in the shared trunk, until everyone agreed. 
Their culture was that such that reviews were speedy. Getting pending commits to the point of rejection or acceptance 
("Looks Good To Me" : LGTM) was almost competitive. Some new Googlers (Nooglers) would pride themselves about taking
on random code-review chores, and being one of a few people that weigh in to the decision moment.

The code review technology marshaled changes for proposed commits to the trunk, and stord them outside the VCS in 
question (in a database probably). To do that the tech would reach into the developer machine and the appropdiate
moment and make a tar.gz of the changes and the meta-data around them, and pull that back to the central system
for global presentation. Anyone could review anything. A review was just on a commit (not a batch of commits). Review
was continuous.

Reviewers could quickly bring the 
marshaled change down to their workstation to play with it, or use it as a basis for counter proposal. They could put 
that back in review again.

In 2006, Guido van Rossum presented one of his bigger contributions - "Mondrian" -
to Googlers. Here he that tech talk on YouTube (previously on GoogleVideos) 
{{< ext url="https://www.youtube.com/watch?v=CKjRt48rZGk" >}}. Note at the start he says XP practice 
"Pair-Programming" is best, and that code review helps fill the gap for situations where you cannot do it.

After Mondrian, the open source world saw Gerrit{{< ext url="https://www.gerritcodereview.com" >}} released 
in its image, and after that Facebookers made Phabricator{{< ext url="https://en.wikipedia.org/wiki/Phabricator" >}}
and released that as open source too.

### Selenium Farm (2006)

Google CI infrastructure was expanded to have **a second tier of elastic infrastructure**, for scaled Selenium/WebDriver 
testing.

This "Selenium Farm" (internal cloud) was also available to developers at their desks, who just wanted to run such tests against a stood-up
version of what they were working on. Teams who had to run Firefox (etc) on their own desktop on a Friday, were able 
to lease one or more Firefoxes browsers  in parallel on a Monday, and no longer lock up their developer workstations.

Other companies since, have been able to deploy their own Selenium-Grid internally or
leverage one of the online services for elastic Selenium testing.

## Branch by Abstraction technique (2007)

Paul Hammant blogged about a 2005 ThoughtWorks client engagement in a Bank of America software development team, 
that used the Branch by Abstraction technique{{< ext url="http://paulhammant.com/blog/branch_by_abstraction.html" >}}.
Whereas many had previously used this technique to avoid longer version-control branches in a trunk model, this was the 
first time it had been detailed online, and given a name (by Stacy Curl).

## Github's entire platform - 2008 onwards

Github was launched as a portal on February 8, 2008, and feature have been added steadily ever since. The initial 
version contained forks, which was a formal way of expressing the directionality of related DVCS repositories, and 
promoting a forgiveness model for unsolicited changes to code (as opposed to the permission model that preceded it
for other portals).

### Pull Requests (2008)

Github added "Pull-Requests" (PRs) on Feb 23rd, 2008{{< ext url="https://github.com/blog/3-oh-yeah-there-s-pull-requests-now" >}},
while in beta, and popularized the entire practice for the industry when they came out of beta in April of that year. 
For source/repo platforms, and VCSs generally, this and "forking generally" was a total game changer, and commercial 
prospects of other companies were decided based on their ability to react to this culture change.

#### Code Review built in

Pull Requests came with an ability to leave code review comments for the contribution. That meant that "upstream" 
receivers of contributions could parry them with feedback, rather than consume them and fix them which was common 
previously.

#### no more clunky patch sets

The open-source community for one, could step away from patch-sets that were donated by email (or rudimentarily). 
Pull-Requests changed the dynamics of open source. Now, the original creator of open source was forced to keep up 
with PRs because if they did not, a fork with more activity and forward momentum, might steal the community. Perhaps 
rightfully so. 

This forced the entire VCS industry to take note, and plan equivalents. It greatly facilitated multi-branch 
development for teams of course.

## Continuous Delivery Book (2010)

See [Publications - Continuous Delivery](/publications#continuous-delivery-july-27-2010)

Jez Humble{{< ext url="https://continuousdelivery.com" >}} and Dave 
Farley{{< ext url="http://www.continuous-delivery.co.uk" >}} wrote this influential book after a 
ThoughtWorks project in London that finished in 2007. 
The client was AOL - enough time has passed to share that. Specific DevOps advances were
being made across the industry, but a critical aspect for this mission was that the prescribed go-live date was tight, given the known
amount of work to be completed before then. Tight enough to want to compress the classic 'coding slows down, and 
exhaustive user acceptance testing starts' phase of a project. The team had to pull the trigger on plenty of 
automated steps, to allow faster feedback loops. This allowed then to have a high confidence in the quality of commits, from only 
minutes before. CI pipelines and delta-scripts for database table-shape migrations, in particular, were focused on.

The 2010 'Continuous Delivery' book is the best selling result. It has been translated into three languages since, and 
both authors now have careers that further deliver/describe the benefits for clients. The book ties the foundational 
aspects of DevOps, Continuous Integration pipelines, and tight lean-inspired feedback loops together to get a broad
and deep definition of how we should develop software collectively in 2010 and onwards. 

Anecdotally the pipelines thinking captures a linear representation of Mike Cohn's famous "Test Pyramid" from his 2009 book, 
"Succeeding with Agile"{{< ext url="https://www.amazon.com/gp/product/0321579364" >}}. See Mike's blog entry a month 
later too{{< ext url="https://www.mountaingoatsoftware.com/blog/the-forgotten-layer-of-the-test-automation-pyramid" >}}, 
as well as Martin's recap in 2012{{< ext url="https://martinfowler.com/bliki/TestPyramid.html" >}}.

Dan North{{< ext url="https://dannorth.net" >}} (Mr BDD), Chris Read{{< ext url="https://www.linkedin.com/in/devopscread" >}} 
(an unsung DevOps pioneer) and Sam Newman{{< ext url="http://samnewman.io" >}} were also key in the AOL advances. 
Dan North gave a deeper account of the mission at GOTO in 2014{{< ext url="https://speakerdeck.com/tastapod/the-birth-of-devops" >}} 
(no video sadly) and was interviewed later by InfoQ{{< ext url="https://www.infoq.com/news/2014/07/birth-cd-devops" >}}.

A year or so before that mission, Sam and Dave were on a different client, UK retailer 'Dixons'. They were part of a team rolling out  
emergent DevOps practices, which they would get to reuse and refine on the following AOL mission. Standouts were: making the
test environments have consistent behaviour with production environments (very close by not quite 'Infrastructure as Code'), 
QA automation technologies setup by the dev team & inducting/co-locating individual QAs with the dev team, Test Driven Development (TDD) and 
Acceptance Test Driven development (ATDD), a CI pipeline that included performance tests, a focus of team dynamics for
high throughput. 

## Travis-CI's Github integration and pass/fail badges (2011)

In 2011, Travis-CI{{< ext url="https://travis-ci.com/" >}} provided easy integrations into Github's platform run CI 
builds for Pull Requests and the general state of HEAD on any branch. This was visually indicated with "build passes" and 
"build fails" badges were inserted into the Github UI{{< ext url="https://docs.travis-ci.com/user/status-images/" >}}. 
This made it was clear whether the proposed PR would break the build or not were it to be merged into trunk. 

## Microservices (2011 and 2012)

The emergence of micro services as small buildable/deployable things that are glued together with TCP/IP (and 
XML/YAML/DNS configuration) reinforced "many small repos" (the kinda reinforce each other really), while this can be
done with any branching model, the non-trunk models probably had the mindshare. Monorepos were out completely. A 
possibility from monorepos, teams sharing code and source level a HEAD revision, positively laughed it. The history 
page of Wikipedia list multiple people concurrenly pushing the same emergent micro-service 
idea{{< ext url="https://en.wikipedia.org/wiki/Microservices#History" >}}.

## Case Study: A Practical Approach To Large Scale Agile Development (2012)

Gary Gruver, Mike Young, and Pat Fulghum wrote
"A Practical Approach To Large Scale Agile Development"{{< ext url="https://www.amazon.com/dp/0321821726" >}} 
to describe the multi-year
 transformation programme in the HP LaserJet Firmware division. In 2008, there were over 400 engineers dotted around
 the world working on over 10 million lines of printer firmware code in the HP LaserJet Firmware division. There
 were 10+ long-lived release feature branches (one for each product variant), with 1 week required for a build and
 6 weeks required for manual regression testing. The engineers spent 25% of their time working on product support i.e.
 merging features between branches and only 5% of their time on new features.

 For the next couple of years, HP committed to a huge investment in Trunk Based Development and
 Continuous Integration. All product variants were rearchitected as a single product on a Git master, per-variant
 features extracted into XML config files, all engineers worldwide were given the same virtual machine for development,
 and a huge multi-tier continuous build process was fully automated in-house. The results were outstanding, with build
 time reduced to 1 hour and manual testing replaced with a 24 hour fully automated test suite including printing
 test pages. 10-15 builds could be produced a day, engineers spent 5% of their time not 25% on product support and 40%
 of their time not 5% of their time on new features. That is an 8x increase in productivity for 400 engineers.

## PlasticSCM's semantic merge (2013)

Plastic's semantic diff and merge{{< ext url="http://semanticmerge.com/" >}} capability was launched in March 
2013{{< ext url="https://www.infoq.com/news/2013/04/Semantic-Merge" >}}. It allowed a greatly reduced diffs for 
refactoring commits.
 
If merges between branches are required, and larger 
code changes (like refactorings) are desired, then multi-branch development is a little easier with this. However, Trunk Based 
Development's commits are more elegant too, because of it, and in the fullness of time, it might make
on techniques like Branch by Abstraction easier, or reduce the need for it, if merge conflicts happen less often
(according to source-control) for something in 2012 that would have been a definite clash.

Other source-control tools are not doing semantic diff/merge yet (2017), but they should be. Semantic merge is
just as useful for trunk based development and multi-branch models. It means that there are less likely to be clash 
situations for commits a developer wants to do. Maybe that last vision isn't quite complete yet, but there's a direction
 to go in now.

## Snap-CI's per-commit speculative mergability verification (2013)

Snap-CI was the first CI service to setup pipelines for new branches in the tracked repository without a human initiating
that - it did so automatically on push of the first commit into a branch. Well, at least if the branch name conforms 
to a given regex/prefix. That commit, and any to the branch afterwards even preceding the Pull Request, are run though a
pipeline that includes:

* all the classic compile/unit-test/integration-test/functional-test steps of the regular build, in situ
* a speculative merge back to the master/trunk/mainline and #1 **again** on that resulting merge 

The speculative merge is discarded after #2 - it is only the "is this buildable and mergeable or not" notification 
that is desired. 

Although they intended this eature of Snap-CI for short-lived feature branches, it is clear now that teams should do this CI setup 
**regardless of branching model**. Yes, even the long-lived branching models also benefit from this, though they'll be
challenged to stay 'green' the whole time, and remain eminently and automatically mergeable back to the mainline/master.

Badrinath 'Badri' Janakiraman wrote a blog entry{{< ext url="https://blog.snap-ci.com/blog/2013/11/07/automatic-branch-tracking-and-integration/" >}} 
when the feature was rolled out - very much worth a read.

## Google sharing their Trunk usage - 2016

In none other than the Association for Computing Machinery's magazine, Googlers Rachel Potvin and Josh Levenberg share
how Google arranges for 95% (25,000) of its software developers to share one trunk in "Why Google Stores Billions of 
Lines of Code in a Single Repository"{{< ext url="http://cacm.acm.org/magazines/2016/7/204032-why-google-stores-billions-of-lines-of-code-in-a-single-repository/fulltext" >}}.
They use a [Monorepo](/monorepos/) varient of a trunk, with internal code shared at **source level**, for high-throughput, 
low-defect delivery of multiple applications and services. Each application/service has a release cadence chosen by the dev+biz 
team in question. Yes, everything works just fine.

Rachel Potvin presented on the same topic a couple of months later in "Why Google Stores Billions of Lines of Code in a 
Single Repository"{{< ext url="https://www.youtube.com/watch?v=W71BTkUbdqE" >}}.

# References elsewhere

<a id="showHideRefs" href="javascript:toggleRefs();">show references</a>

Date    | Type  | Article
--------|-------|--------
13 Nov 2013 | Talk | [A Practical Approach to Large Scale Agile Development](https://www.youtube.com/watch?v=2QGYEwghRSM)
14 Jan 2015 | Blog entry | [From 2½ Days to 2½ Seconds - the Birth of DevOps](http://dizzythinks.net/from-212-days-to-212-seconds-the-birth-of-devops.html)
23 Apr 2015 | Blog entry | [The origins of Trunk Based Development](http://paulhammant.com/2015/04/23/the-origins-of-trunk-based-development/)
