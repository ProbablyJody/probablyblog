# Life After Death: Benefits of a Postmortem Culture
> Wait, is prod down?

* Who was involved?
* Should anyone else have been engaged?
* Was communication strong?
* How did this happen?
* Where did we excel in resolving the issue?
* What areas in the resolution need improvement?
* What did we learn from this event?
* How can we prevent this from reoccurring?

There are questions when things go wrong. A postmortem is an attempt to answer those questions [abinante16](abinante16)

## What is a Postmortem?
Ultimately a postmortem is a document that provides rich information around a significant undesired event. A postmortem’s scope spans the timeline before, during, and after an incident. It includes a summary of the event, the impact to all stakeholders, a timeline of key contributing factors, the steps taken to troubleshoot and resolve the situation, and the actions needed to prevent the incident from happening again [Lun17]. 

After production has been restored to a stable state, a postmortem should be drafted. This is a collaborative effort. While the document can be pre-filled, it should not be finalized until it has been reviewed. A meeting should be held for this review. A designated facilitator, those involved in the incident, relevant stakeholders, domain experts, and anyone else interested in helping should walk through the incident and ensure that all questions have been answered. The value in meeting to review the postmortem shines brightest when people “say aloud what they were and were not sure about, [and it] enable[s] others in the room to repair those uncertainties and misunderstandings. [All16]” It allows others to reveal un-considered assumptions. This process is blameless, with a focus on understanding how the conditions that created the event came to be, as well as how it can be prevented.

Examples
* https://landing.google.com/sre/book/chapters/postmortem.html
* https://www.youneedabudget.com/postmortem-why-ynab-went-down-last-week-and-how-it-made-us-better/
* https://about.gitlab.com/2017/02/10/postmortem-of-database-outage-of-january-31/
* https://aws.amazon.com/message/65648/
* https://azure.microsoft.com/en-us/blog/update-on-azure-storage-service-interruption/

## Benefit: Promoting an Atmosphere of Blamelessness
Blamelessness and postmortems are very closely coupled. Nearly every source gathered for this post mentioned blamelessness. Many simply used the phrase “blameless postmortems” as the focal point of the discussion. While the reasoning involved may feel a bit circular, it is important to understand that eliminating blame is essential for successful postmortems and embracing a culture around postmortems brings with it a culture of blamelessness.

> “People are expecting root cause to be a single thing instead of a series of things, and the phrase is misleading.” - Jason Hand

### Eliminating blame is essential for successful postmortems.
Assigning blame is easy. It’s allows one to pinpoint a person/team as the reason for the failure. The action item becomes improving/replacing the offenders. Everyone is then free to close the postmortem, and walk away feeling like the vast complexity around a problem had a simple explanation. The fundamental problem with this line of thinking is that the target of the blame is only one part of the complex system [Kah16]. No real improvements come from declaring a human as the root cause of a problem, because humans are prone to making mistakes. It will only be a matter of time before some other human makes a similar mistake. Instead the system must be changed to reduce the volume of mistakes made. Improvements can be made to help those faulty humans make better choices. So instead, the preference is to assume that everyone involved had good intent and that they were doing the right thing with the information they had access to. With this assumption, the postmortem continues on to understand how the limited or incorrect information came into the hands to those involved. The question is no longer “who allowed this to happen?”, or “why did this happen?”, but “how did this happen?"

### Embracing a culture around postmortems brings with it a culture of blamelessness.
Avoiding blame is hard. It requires one to intentionally avoid the easy answer. It is a skill that requires practice. So embracing a culture that requires everyone to hone that skill will result in a community skilled in avoiding blame. Managers and team leads can encourage a culture of blamelessness, but it will be best executed by a team who excels at looking at the larger system for flaws over an individual point of failure [Lun17].

A spectacular execution of blamelessness!
On January 31st, 2017, GitLab experienced an 18 hour downtime. While attempting to resolve an active production issue, an engineer intended to trash a backup instance of a database. The backup instance was failing to maintain replication with the primary instance and the expectation was that wiping it would kick-start replication.
The engineer accidentally triggered the wipe on the primary instance instead of the backup.
A mere seconds passed before the engineer realized the mistake, but it was too late. Some of the data had already been deleted. The engineer quickly notified the rest of the team of the mistake and they started working on retrieving a backup instance from their redundant sources. Imagine the icy feeling they must have felt in their veins when they realized that their backups to AWS had been failing silently. To make matters worse, they had disabled disk snapshots to Azure because restoring from snapshots can take days, and they previously felt confident about the backup methods that had just failed. They were forced to restore the database from a disk snapshot that had been copied over to staging for the purposes of validating code changes. 
GitLab estimates that 5,000 projects, 5,000 comments, and 700 new user accounts were permanently lost. No git repos were lost since they are stored separately. In addition the only instance affected was GitLab.com. Enterprise, hosted, and self hosted instances were affected by the downtime, but lost no data.

## Benefit: Enhancing Trust With Stakeholders

## Benefit: Eliminating Chronic Problems

## Benefit: Fostering an Community Around Shared Learning

## Summary

## Sources
[#abinante16] 
* ["Day 1 - Why You Need a Postmortem Process"](https://sysadvent.blogspot.com/2016/12/day-1-why-you-need-postmortem-process.html) Gabe Abinante, blog post, 2016
###### All16 
* John Allspaw, "Etsy’s Debriefing Facilitation Guide for Blameless Postmortems”, blog post, 2016, https://codeascraft.com/2016/11/17/debriefing-facilitation-guide/
###### Kah16
* Jessica Kahn, “Failure is Always An Option: How a Blameless Culture Leads to Better Results” blog post, 2016, https://victorops.com/blog/blameless-culture/
###### Lun17 
* John Lunney and Sue Lueder, “Postmortem Culture: Learning from Failure”, Site Reliability Engineering, 2017, https://landing.google.com/sre/book/chapters/postmortem-culture.html

