---
title: "Nov.28/2019 Security Shortcuts Meetup"
date: 2019-12-10T06:07:22-08:00
draft: false
---

So, I went to a Meetup on November 28, 2019 on Software Security and Shortcuts towards that end.  The following are some things I might have heard and some thoughts I had on the matter.  *Just a note that I may have misheard and or misconstrued the presenter's intents and/or words.*

1. Organizations are getting better at stopping 'front door' attacks, so the OWASP stuff and the other stuff on Security checklists, I guess.

2. These days, in terms of time-effectiveness for the bad-actor of compromising systems, it is best to attack the code that developers use and the developers themselves.  
    - The developers can be attacked via phishing said developer and using him/her to commit a backdoor into production.
    -Attackers are more frequently attacking common libraries used by developers because modern software development, in a lot of cases, is gluing blocks of code together.  Hitting a common library results in compromising many machines.

3. Apparently, it is hard to get `Identity Access Management` right. In addition, one needs to remember to test the settings for who has what credentials, for how long and who should have access.

4. Repository and Storage configurations are often not correctly set, resulting in private data being exposed to the public.

5. Code credentials are sometimes committed into the repository.

6. Depending on one's need for degree of application security verification, one may need to do more than wait for Github/Gitlab/BitBucket to send notifications of vulnerable dependencies and then immediately updating them.
