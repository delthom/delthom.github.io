---
layout: page
title: CrowdStrike Exposes The True Cause Of The Worldwide IT Meltdown
---

##What happens when redundancy and graceful degradation become an afterthought…

The very moment my parents bought me a computer, I wanted a second one. As a teenager, I couldn’t immediately afford it, but a couple of years later, as I upgraded to a newer machine, I kept the old one. I now had two machines and all was well with the world. This is a habit I kept all throughout my life. Ever since, I always had two machines, and at times even three. I am able to run on two internet connections, one fibre and another one 5G. That’s redundancy. Sure, the second machine is always a tad slower, and so is the backup network connection. That’s graceful degradation. The CrowdStrike update exposed both of these business and software engineering fail-safes lacking across the world, and it puts a faulty app (driver) update into a very different light.
Microsoft Windows

I’ve had the unfortunate opportunity to use all versions of Windows, since Windows 3.1. I say unfortunate because between Windows 3.1 and Windows 10, I never had a positive experience with the operating system. It had some good moments — such as Windows XP or Windows 7 — but ultimately, I always considered it just a necessary evil, even before moving to Linux, then macOS entirely. If there was one issue that plagued all versions of Microsoft Windows, it was instability. I remember having to reinstall Windows 98SE roughly every couple of months, or running System Restore on Windows XP just about as often, but on XP at least I had the option.

**As a Windows user, you get to be relieved every single day you turn your computer on, and everything loads as expected. Lucky you!**

With the advent of the web, security became an important consideration, and we soon found ourselves having to install antivirus software sooner than changing our desktop wallpapers. Stability has suddenly become a secondary concern because connecting Windows to the web without anti malware software was guaranteed to render your machine useless within minutes. In fact, during the peak of Windows 7, I did just that experiment. I installed a genuine copy of Windows 7 (genuine disk, bought sealed from the store) on a freshly deep-formatted hard drive, connected the Ethernet cable, opened My Computer, Internet Explorer without navigating to any site besides its built-in home-page and left it there for about an hour. An hour later, I proceeded to download Avira from the official site, ran a scan, and it detected malware. Nothing debilitating, but nevertheless, I was infected.

**Microsoft Windows was never a secure operating system. It’s an architectural house of cards.**

The fallacy that any operating system as popular as Microsoft Windows will inherently be less secure is exactly that — a fallacy and a myth that Microsoft and their apologists love to push. There is some truth to it, as any security professional will tell you, but the fundamental truth remains the same — Windows was created for a non-networked desktop context and that foundation hasn’t changed, not even in Windows 11 where certain security hardware (TPM) is required to even run it.

As Steven Vaughan-Nichols of Computerworld put it back in 2009, “It all comes down to all of Windows security improvements amounting to being just a layer over another of security over its fatal single-user, non-networked genetics.” That trend hasn’t really changed. Everything that Microsoft does to Windows to make it more secure — while welcome — is reactive patching at the end of the day, that even they don’t seem to truly believe in, as demonstrated by the official instructions on how to bypass Windows 11’s TPM requirement.

**From a software engineer’s perspective, Microsoft Windows looks like a heap of technical debt, ripe for a complete rewrite.**

CrowdStrike’s approach to security in light of Windows being this poorly architected isn’t surprising. As a tech company aiming for a leading role in business and enterprise security, opting for going a step beyond the traditional antivirus software approach — that of just loading an app once the machine booted — and installing a driver to run before the machine even boots up, makes sense. It feels like an overkill, but it’s not. It’s Windows we’re talking about. Windows desperately needs this much support to become a secure environment. MacOS, iOS, Linux all have security baked into the foundations of the operating system. We’re talking BSD Unix, at the end of the day, developed at its heart with a very different design philosophy.

Microsoft Windows’ fundamental need for aggressive 3rd-party security solutions is one of the core causes of the global IT meltdown. Couple that with additional architectural weaknesses like a corrupt file being able to bring down an entire operating system, and you have yourself a paralysed world.
Poor design, lack of redundancy

As I am typing this on my M3 Max MacBook Pro, there is a fully charged M2 MacBook Air ready to go at a moment’s notice, and neither are running the same version of macOS. On one, I have automatic updates enabled, on the other, I don’t because, believe it or not, Apple can cause plenty of havoc too. Having different versions of macOS running on the two devices enables not just continuity in my work, but potential recovery solutions for the other device.

My redundancy philosophy as a teenager was considered extreme and unnecessary by my friends, only to find out just a few years later as I was doing my Cisco Certification that redundancy is core to every reliable network. In fact, both reliability and redundancy are built into the TCP and UDP protocols — another great software development example of using the right tool for the right job. In this case, TCP takes care of data integrity with no degradation when that’s the prime objective, and UDP makes sure things like your Zoom conversations don’t fall apart when packets are lost.

**While TCP/IP is fundamentally unreliable, it also incorporates the mechanisms to avoid its core shortcoming becoming a self-debilitating flaw.**

In software engineering, once we know and understand a system’s potential downsides, we are trained to develop fail-safes. Handling an error, or an unknown case, should more or less be second-nature to anyone writing code. Let me pseudocode a small but illustrative example that even the average Jane and Joe should understand:

```
if (days in month) === 30 {
 return [april, june, september, november]
} else if (days in month) === 31 {
 return [january, march, may, july, august, october, december]
} else if (days in month) === 28 {
 return [february]
}
```

The above code would run fine for 3 years and 11 months, except for the February of the 4th year when the month is 29 days long. That’s an unhandled case and the program would go “I don’t know what to do now, I’m going to stop and trow an error” — think your Windows blue screen of death for instance.

One solution would be to add and extra case for leap years, or the even safer choice would be to handle all other numbers with an else case like so:

```
if (days in month) === 30 {
 return [april, june, september, november]
} else if (days in month) === 31 {
 return [january, march, may, july, august, october, december]
} else {
 return [february]
}
```

Because what if suddenly someone decides that all this leap year stuff is too much effort? Let’s just stick to a 28 days February all the time, and let the world deal with the repercussions of having Christmas mid summer in 730 years. As ridiculous as that may sound, my program would work regardless, as all cases are accounted for, and we’d never see a blue screen of death ever again.

In the CrowdStrike bug that brought systems down all over the world, I see two fundamental software engineering mistakes:

**Clearly, the case of a corrupt file in a driver wasn’t covered in Microsoft Windows. It boggles the mind that such a simple mistake wasn’t handled gracefully, but it obviously wasn’t, and it makes me wonder — and unfortunately the same goes for every other malicious actor out there — what else can be done to achieve the same disastreous results in the OS? A single corrupt file should not bring down an entire operating system, but in Windows’ case, it does. Extremely optimistic error-handling is always a sign of bad software development practices and poor design.
**No recovery mechanism was present in the operating system. My expectation of a computer in 2024 is that if an update goes wrong, it knows how to revert itself to the latest working version. Reverting is something we do a lot in software development. Even when you do things right, you sometimes find bugs that require an “undo”. Being an operating system, I would expect it to recognise a faulty version of an update and move itself back to a previous working state. For instance, on a Mac, even if you delete the entirety of the hard-drive’s contents, the machine will realise it has no OS, ask you to connect to the web, and download you the latest working version. In this case, all Windows should have needed to do was recognise it cannot boot properly — which it did, hence the BSOD — and load the version it last remembered working, or at the very least load itself into Safe Mode, and advise the user to choose a previous version manually.

A faulty CrowdStrike update is unfortunate, and mostly avoidable, but as every software engineer knows, it is impossible not to land a breaking bug into production once in a while. I have yet to meet a software developer who hasn’t caused a major incident. It’s like surgeons having someone die on their operating table. It’s inevitable. I once locked millions of students out of a core learning platform because the password length on the frontend and the backend didn’t match.

* Anything that can go wrong, will go wrong. — Murphy’s Law

How many more times do we need to hear this in software development to take it seriously? On this occasion, Microsoft clearly didn’t consider it being a possibility, and it begs the question — why? As an operating system owner without any real vertical integration, it very well knows, and has known for decades, that it runs its OS in contexts it has virtually zero control over. System integrators will throw it any hardware they can, and developers will cobble together anything they can on top of it. It’s the Wild West out there. One of my first jobs was to build PCs for customers at the local computer store. The hardware was awful, the software that customers wanted installed was even more awful. For the most part, it seems at Microsoft, defensive programming is still an alien concept.

But of course, we can’t just blame Microsoft for all of it. Impacted businesses are just as much at fault here. Mission-critical systems running without redundancy or graceful degradation in mind. And it’s not the first time, either. The 737 Max tragedies were connected to being reliant on a single sensor to run a piece of software, that did exactly what it was told, but without hardware and data redundancy, it did the opposite of what pilots expected.

* How can in 2024 an entire banking system, airports, national healthcare and transportation systems rely on a single operating system? Where’s the redundancy?!?

IT systems of this magnitude should not be allowed to exist without built-in redundancies. It’s not enough to just have generators for electricity. Sure, that helps, but as we live in an increasingly digital world, that’s far from enough. Walking into a large hospital, seeing BSODs everywhere, is about as bad as it can get. In reality, the answers to some common what ifs should be this:

**What if the power goes out? We switch to battery-power while generators kick in to replenish our power storage. 
**What if the internet goes down? We switch to other fibre providers, followed by DSL or 5G providers. If none available, we switch to satellite communication. 
**What if the OS crashes across the network? We reboot using an alternative OS. 

These are the bare minimum answers I would expect. Clearly and sadly, we live in a world of IT infrastructure where none of this is a reality, my expectations seem to be out of sci-fi movies and the reasons are always the same — it costs too much — which brings me to my next point.
A culture of cheap

And this goes far beyond Cory Doctorow’s famous “enshittification” theory. Software is degrading without any graceful degradation in place. Stuff either works or doesn’t. Microsoft and CrowdStrike aren’t the only examples here of just how poor software can be when done fast, cheaply. I am equally worried about Apple’s OpenAI integration as well and in fact, any software company that recently added “AI features” via OpenAI’s API because I can all but guarantee that the moment their API runs into issues, the moment their servers get DDoSed, crash or whatever else might happen, half the software out there will handle these outages very poorly.

Software is increasingly unreliable because it’s less and less a stand-alone entity and much more an interconnected network of services. In essence, there isn’t anything wrong with software as a service, and integrations, but it’s an incredibly delicate chain where usually just one link needs to fail for everything to fall apart. The alternative is either owning everything — which is likely unrealistic — or implementing redundancies and experiences that even degraded, offer enough value. Neither of these solutions is cheap, though.

I remember when Progressive Web Apps (PWA) became the hot new kid on the block, everyone kept using graceful degradation like it was punctuation. It was the buzzword of buzzwords alongside “synergy” and “innovation” and the candidate that stood out at interviews was the one that didn’t bring up PWAs between saying “hello” and asking “how are you?” And yet, we find ourselves that same buzzword lost the buzz, even Apple showed it the middle-finger and there is barely any website out there that still loads something in offline mode.

**We’re dealing with a debilitating culture of cheapness across the software development industry.

Agile was another great buzzword, but we made sure to hack Agile too into something it was never meant to be interpreted as — untested fast delivery. In fact, the whole concept of Agile was meant to enable pivoting fast, not building fast. It is undeniably cheaper to run an IT infrastructure without redundancy in mind if all you’re thinking of is the IT budget, but overall, how much cheaper is it really?

CrowdStrike’s unfortunate mistake will have long-running repercussions. The potential for law-suits by the hundreds, busy insurance companies, jobs could be lost, vacations ruined, and the list goes on. The ripple effects of such a small mistake will be disproportionately large and far-reaching, and I can’t help but think, a bit more investment would have gone a long way towards preventing this disaster.
A precarious future

While the World is angrily pointing the finger at CrowdStrike and its CEO, George Kurtz, I feel it mostly should look elsewhere. Continuous fast and cheap software, patches upon patches, downright insane business practices relying on crossed fingers rather than hardware and software redundancy; coupled with increasingly poorly tested software updates across the tech industry is what got us here. Not a corrupt update.

Under these circumstances, I must ask, are we sure we still want AI in our software and our daily lives? Are we sure we want to add more complexity to our software that’s hanging by a thread of zeroes and ones? We clearly can’t even do simple things well and reliably enough. Perhaps we should get back to the basics and just write good software with simplicity, redundancy and graceful degradation in mind. How about that? Can we do that? Please?

**In the grand scheme of things, the CrowdStrike incident is merely a storm that exposed our interconnected world’s foundations built on nothing but sand. It was never a question of “if”, but a “when”, and that “when” was now.**
