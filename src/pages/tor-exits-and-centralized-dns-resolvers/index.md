---
title: Tor Exits and Centralized DNS Resolvers
date: "2018-05-11"
---

The [Tor Project](https://www.torproject.org/) provides a powerful tool, Tor, to protect your privacy online and provides its users strong online anonymity protections. Today I'd like to talk about a potential weakness in Tor that being Tor Exits and their use of Centralized DNS Resolvers.

## Tor's split of trust
A potential problem with allowing anyone to run a Tor Exit is that malicious people and/or organizations may run an exit to spy on Tor users. Tor handles this by switching "circuits" often to avoid a specific operator from linking your actions to each other. The Tor Project's website describes it as followed,

> "For efficiency, the Tor software uses the same circuit for connections that happen within the same ten minutes or so. Later requests are given a new circuit, to keep people from linking your earlier actions to the new ones." -- [Tor Project](https://www.torproject.org/about/overview.html.en)

This split of trust is what makes me prefer Tor as opposed to a VPN or Proxy provider who promises to not log your internet traffic. With Tor we don't have to rely on one entity promising to be good since the trust is split across multiple entities.

The usage of centralized DNS Resolvers on Tor Exits begins to break apart that split of trust and it needs to be avoided to protect the privacy of Tor's users.

## An observation of which DNS Resolvers are being used the most
I used a [DNS Leak Testing Tool](https://www.dnsleaktest.com) and ran the extended test a few times. This data showed me the resolvers that DNS Requests came from. My findings were that the majority of Tor Exits are either using their ISP's DNS Resolver or Google DNS. This far from a diverse study however it does give you a general idea of what's being used. @nusenu wrote an article on Medium with the statistics on this I included it in the related reading section at the end of this article.

## Google Public DNS keeps log files which are a goldmine for law enforcement
Google Public DNS keeps various log files which they claim are used to prevent abuse of the Google Public DNS service. Google states the following in their privacy page for Google Public DNS about the data they log and what they use it for.

> Google Public DNS stores two sets of logs: temporary and permanent. The temporary logs store the full IP address of the machine you're using. We have to do this so that we can spot potentially bad things like DDoS attacks and so we can fix problems, such as particular domains not showing up for specific users.
>
> We delete these temporary logs within 24 to 48 hours.
>
> In the permanent logs, we don't keep personally identifiable information or IP information. We do keep some location information (at the city/metro level) so that we can conduct debugging, analyze abuse phenomena. After keeping this data for two weeks, we randomly sample a small subset for permanent storage.
>
> We don't correlate or combine information from our temporary or permanent logs with any personal information that you have provided Google for other services.

The statement goes on and on to describe the data they log in greater detail, you can [read their full privacy statement here](https://developers.google.com/speed/public-dns/privacy) if you are interested.

As we know, thanks to various leaks by government officials at their own personal risk, the FISA Courts have ordered various internet companies to hand over huge amounts of their users' data on their users in an unconstitutional manner to government agencies.

Having all of this in mind, in theory, the FISA Courts could order Google to hand over, on a regular basis, all DNS Logs related to Tor Exits, these logs could include which Tor Exit viewed which websites at which times, while it wouldn't identify which user did what, it would give law enforcement a good idea on what Tor users are using Tor for, and which exits' users are doing what at which times. As you can imagine this begins to break apart the privacy of the Tor Network.

What's worse is that for all we know, the FISA Courts already have ordered Google to hand over this data since the last set of leaks, we have no way of knowing unless another government official risks their life and leaks the information. This information would be a goldmine for law enforcement and it would give them an idea on the browsing habits on Tor users.

This issue applies to any DNS Resolver, it is not a Google specific issue nor is it directly Google's fault, however due to the sheer scale of Google Public DNS and the amount of Tor Exits using it is the perfect target and a goldmine for law enforcement and it just wouldn't make sense for law enforcement to not take advantage of that treasure trove of information. It is a risk that we as Tor Exit Operators cannot afford to take.

## Would Tor Exits using a trusted DNSCrypt Resolver be a solution
One of the first solutions to this problem that I thought of was for Tor Exits to use a trusted DNSCrypt Resolver - most DNSCrypt operators are more trustworthy people than large corporations like Google and Cloudflare. I thought about this issue for a bit and came to the conclusion that we would just be reassigning trust to another entity and eventually we would have the same issue with a select set of DNSCrypt Resolvers having access to most of Tor's DNS Traffic.

Overtime the same issues that currently exist with Google DNS / ISP DNS in regards to Law Enforcement can happen to the large DNSCrypt Resolvers (whether they'd comply or shutdown is unclear - it depends on the honesty and integrity of the operator) the risk still exists and needs to be addressed. The issue with large public dns resolvers is harmful to the privacy and security of Tor users and needs to be addressed.

## Tor Exits should run their own DNS Resolvers rather than relying on Centralized DNS Resolvers
The next solution that comes to mind (someone on the tor-relays mailing list suggested this to me) would be to run our own DNS Resolvers on Tor Exits. Perhaps overtime a DNS Resolver could be built into the Tor software itself (Unbound is free and open source software). By running our own DNS Resolvers we do not have to rely on trusting a third party resolver to not be evil. It preserves the split of trust on the Tor Network and I personally believe it is the best solution at this time.

## The good news
This issue is currently being discussed on the tor-relays mailing list. You can [read the discussion here](https://lists.torproject.org/pipermail/tor-relays/2018-May/015170.html). Several solutions to the problem are being proposed and while everyone's thoughts and beliefs on the issue are different, overtime we can hopefully all move away from giant DNS Resolvers to a better set of solutions. There is no one size fits all solution although I look forward to seeing how this gets addressed over time.

## How I am addressing this on the Tor Exits I operate
I currently operate four Tor Exits, over the next few weeks I will be configuring them to run their own DNS Resolver rather than querying ISP provided DNS Resolvers.

## Suggestions or Feedback?
I'm always open to your suggestions and/or feedback, if you have suggestions or feedback on this blog please send an email to me@lunorian.is I'd love to hear from you :)

## Related Reading
* [@nusenu's Medium Post "Who controls Tor’s DNS traffic?"](https://medium.com/@nusenu/who-controls-tors-dns-traffic-a74a7632e8ca)
* [tor-dns paper](https://nymity.ch/tor-dns/)
* [[tor-relays] lets stop using central big DNS resolvers (Google, Level3, OpenDNS, Quad9, Cloudflare)](https://lists.torproject.org/pipermail/tor-relays/2018-May/015170.html)