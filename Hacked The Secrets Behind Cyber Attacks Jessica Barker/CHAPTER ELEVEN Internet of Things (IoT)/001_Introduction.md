# CHAPTER ELEVEN Internet of Things (IoT)


## Introduction


In 2016, over 175,000 websites around the world suffered a distributed denial of service (DDoS) attack. Large swathes of the internet in eastern United States and across Europe suffered. Behind it all, was some malicious software (malware) called Mirai.

Speculation abounded that this was the work of a nation, perhaps linked to the looming elections in the US. The attack was claimed by hacking groups Anonymous and New World Hacking – presumably not wanting a crisis to go to waste – who asserted that they were taking revenge for Julian Assange being without internet access in the Ecuadorian embassy.1 As this attack took huge amounts of the internet offline for many people, the motivation seemed to line up with the impact.

The true story of Mirai is, in fact, far more fascinating.

The story of Mirai illustrates one of the main facets that I love about working in cyber security. It is the human stories lying beneath the technology which never fail to fascinate me.

But, before we get to the full story of Mirai, let’s address some technical foundations to paint a full and clear picture of what happened here.

A distributed denial of service, or DDoS, is one of the oldest types of cyber attack. On 6 September 1996, the internet provider Public Access Network Corporation (Panix) was taken offline by the first reported DDoS.2

To understand a distributed denial of service, we must first understand a denial of service (DoS). A DoS is when one computer, with one internet connection, overwhelms a website or system with so much internet traffic that the website or system can no longer function. A DDoS is the same, but the overwhelming traffic comes not from one computer and one internet connection, but rather from multiple computers and connections. They are not always malicious: if you have ever been unable to reach a website because of a huge surge in the popularity of that site, you have seen a (non-malicious) DDoS in action. In fact, you’ve been part of it, because your computer and connection has been one of too many trying to reach that site. A common example: highly anticipated concert tickets are released at a specific date and time, and so many people are keen to book their ticket that the website simply cannot cope with demand.

However, DDoS incidents are also weaponized online and used maliciously. As in the case of Mirai.

Malicious DDoS attacks generally make use of botnets. A botnet is a network of internet-connected computers (bots) that are all being controlled by one centralized computer.

The Mirai attack used a new kind of botnet. Rather than using typical computers, Mirai used a botnet of Internet of Things (IoT) devices. In this way, it used physical objects that were connected to the internet. IoT includes smart doorbells, lights, cameras, office equipment, thermostats… the list is endless, with the common denominator that these devices are in our homes, cities and workplaces, connected to the internet. In 2016, there were 2.33 billion internet-connected devices3 and at the time of writing in 2023, there are 15.14 billion,4 which is almost twice the number of people in the world. Mirai infected webcams and internet routers, in particular.

The Mirai malware worked by infecting devices that scan the internet for IP addresses of IoT devices. IP addresses are like the postcode or zipcode of devices. Once identified, the Mirai malware uses a table of known, default usernames and passwords for IoT devices to automatically log into them.