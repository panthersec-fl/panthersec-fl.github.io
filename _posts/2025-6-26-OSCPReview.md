---
title: OSCP+ Review
date: 2025-6-26
categories: ["Red Team"]
tags: ["Red Team", Certifications]
---
![cert.png](/assets/OSCP-Certificate.png)

### Background &amp; Intro

 I'll be cross-posting this article on a couple different platforms so if we haven't already met here is a quick introduction! My name is Miles, I am an early career cyber security professional interested in security engineering and penetration testing. I've completed my bachelors at the University of Central Florida in Information Technology with a minor in secure computing and networks and I'll be attending Georgia Tech's Online Masters of Science in Cyber Security program this fall. I love studying for certifications, since the first summer break in college I have been studying for various certifications 90% of the time. I held the following before being awarded my OSCP+ / OSCP certificate:

- CRTP: Certified Red Team Professional, An Active Directory assume breach course and certification exam.
- Security+
- CySA+
- Linux+
- Network+

Additionally before starting the OSCP course, I did some HTB modules to help me prepare:

- Windows Privilege Escalation
- Linux Privilege Escalation
- Web Requests
- Introduction to Active Directory

At this point I felt confident to spend the 1700-1800$ for the course and a single attempt.

### What is the OSCP?

 The OffSec Certified Professional exam is a hands on course with Kali Linux that takes the learner through various topics such as information gathering, common web attacks, SQLi attacks, client-side attacks and utilizing public exploits and more. The OSCP certification exam that accompanies the OSCP course consists of a 23:45 hour examination period against 3 standalone Windows or Linux machines and an Active Directory assume breach scenario followed by a 24 hour reporting segment where the tester must report their findings along with remediation steps and methodology. The OSCP course and exam is a beginner-level penetration testing exam but not a beginner-level IT/Cybersec certification.

### The course

 I started the course at the beginning of February and made it through all of the videos, modules and module labs by mid-April. I was working full time and attending college so that did draw it out a bit. The course is comprised of text based modules with readings, videos that follow the readings and small challenge labs as you progress. The structure provides a very nice onramp into penetration testing for a beginner by providing smaller challenges that lead into bigger ones.

 I typically studied by first watching the videos on the section and taking notes. Then I would read through the text and complete the module labs, filling in the areas that I missed from the videos. My preferred note taking app was Notion. It is a great platform that provides an amazing UI that is easy to look at for hours, not to mention it is completely free as well. I see that Cherry Tree is another strong note taking choice but I opted for Notion since I can access my notes from anywhere with an internet connection and on different devices without an internet connection with Notion's desktop app's offline mode.

 From my research across Reddit and other platforms like Medium, it is clear that the community believes the course content to insufficient for exam preparation. I would have to agree. The content provides much breadth but doesn't go as deep as I would of have liked. This is where my notes and experience from HTB and CRTP was able to bridge the gaps. You could get by with just course and challenge labs if you have a lot of free time to really develop your methodology but I strongly suggest completing the two privilege escalation modules from HTB at least to really see the type of vectors out there.

### Final Prep for exam

 The challenge labs were very helpful in getting my feet wet again with an enterprise environment from a small break I took after CRTP. They were well put together scenarios that brought tons of course content into scope. My biggest regret is not starting these sooner as I ended up only completing the first 3-4.

 Where I feel that I gained most of my knowledge and really honed my skills was at this point, about a month out from my test date. This is when I purchased a subscription to Proving Grounds labs and began to work my way down the "[Lainkusanagi OSCP like](https://docs.google.com/spreadsheets/d/18weuz_Eeynr6sXFQ87Cd5F0slOj9Z6rt/edit?gid=487240997#gid=487240997)" list section for Proving Grounds. I would switch back and forth between the platforms every couple boxes, taking notes and developing a methodology in Notion. If you are newer to pen-testing or the OSCP you might be wondering, what exactly is a methodology? It is essentially just a plan of action that you create for yourself to follow as you attack various machines. Poking around a VM without a strategy is going to waste time and may lead to missed information that could lead to device compromise.

 As I was completing these boxes on Lainkusanagi's list I was also watching ippsec on Youtube. This creator walks through HTB boxes from initial service discovery to privilege escalation to root/SYSTEM/Domain Admin. I probably watched about 25-30 videos from ippsec, taking notes all the way. Lastly, 1 month isn't a lot of time to complete all of the boxes on Lainkusanagi's list, but I did not want to miss out on the information from these machines. So I read through write-ups through the HTB machines on the list and took notes about tool usage, exploit paths and added commands and items to my methodology.

### Exam

##### Day 1

 The big day itself! I woke up at 6:30am on a Saturday for my exam at 8am... which was actually 7:45 as you needed to be ready for the proctor 15 minutes before. After waking up and walking through my normal routine I walked three laps around my apartment complex and then had a coffee while reviewing my methodology. I believe this was crucial to my initial success to help wake up my brain and get the blood flowing.

8:00am: After receiving my VPN package via email I got to work on the Active Directory set first. Since this set was 40 points, I would need at least 10 points from here anyways so I decided to start here. Additionally I was familiar with pen-testing AD from my CRTP prep and exam.

10:20am: Domain Compromised. That's right! I got the entire AD set in about 2 hours. It was easier than I thought it was going to be but there were a few oddities that I had to workaround to get the exploits right.

10:30-4:30pm: Nothing! I enumerated each standalone but did not get any initial access. If at first you don't succeed, walk to Starbucks and try harder!

4:40-5pm: Finally got a foothold in one of the standalones, this started a steam roll of progress.

5:45pm: 70 Points! Although a passing grade, my only through was, "What if I miss something on the report and lose 10 points". So I kept going.

7:30: 80 Points! Time to walkthrough each exploit chain and make sure I have every command and screenshot needed for the report..

##### Day 2

 I woke up at 8:30am well rested and began writing the report. I used OffSec's template that they posted to the OSCP FAQ. I spent more time on this report than the exam itself, I submitted the report at 1am.

### Final Thoughts

 The OSCP+ exam is a strong penetration testing exam for a beginner and a must for an aspiring cyber security professional in my opinion. The breadth of attacks possible lead to a very inclusive learning experience. For though thinking about taking the OSCP exam, I would highly recommend running through HTB's modules for privilege escalation and basic Active Directory to build a solid foundation to hit the ground running.
