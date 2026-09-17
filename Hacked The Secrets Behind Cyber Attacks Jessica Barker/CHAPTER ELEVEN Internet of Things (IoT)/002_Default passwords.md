# CHAPTER ELEVEN Internet of Things (IoT)


## Default passwords


Now, I hear you. ‘Known, default passwords?… automatically log in?... Surely this should not be possible!’ You’re right, but just because something should not be possible, doesn’t mean it cannot be done. From the moment that IoT devices emerged, the cyber security community warned of security concerns, one of the greatest being devices that are not password protected or that are protected with a known, default password. Meaning, simple passwords that are generally published by the manufacturers on the internet.

I spoke with Erhan Temurkan, a Chief Information Security Officer with experience in cyber crime investigations, about this issue. From his perspective, there are two distinct security challenges with Internet of Things devices:

‘Firstly, IoT security is an afterthought for vendors who want to be first to market. Secondly, the uptime of success is high – when you have compromised an IoT device, you generally have compromise forever, because we don’t usually restart IoT devices.’

The race to market for IoT manufacturers led to low-cost devices being sold with weak security controls (or no security controls) built in. Many IoT devices emerged that were ‘protected’ by default passwords set at the manufacturing factory and with no guidance – even no functionality – that would allow consumers to change the password to something unique and strong.

It was this huge gap in IoT security that Mirai exploited. On its first day, Mirai infected over 65,000 IoT devices. If that surprises you, I hope you’re sitting down for the next statistic: at its peak in November 2016, Mirai infected over 600,000 IoT devices.5

In 2016, devices compromised with Mirai pointed traffic at Dyn, an internet-performance company. Dyn acts like an internet switchboard. We type a simple and memorable domain name into an internet browser and companies like Dyn link us up with the actual website that we want to visit. Dyn, therefore, is part of the infrastructure of the internet and when it was hit with this Mirai-powered DDoS, it meant that many people could not access the websites which Dyn should have been linking them up with. This attack on a core part of the internet’s infrastructure was one factor which led to speculation that this was a sophisticated, even state-level attack. It was not the only evidence pointing this way.

There was some clever functionality written into the Mirai code. Firstly, it was hard-wired to avoid certain IP address ranges (continuing with our analogy of IP addresses as postcodes or zip codes; this means it was designed to avoid certain areas of the internet). These included GE, Hewlett-Packard and the United States Department of Defense.

The code also contained some Russian-language strings, which further implied that this could be a state-on-state attack. The context of the approaching US elections made this seem even more likely. However, this proved to be a red herring.