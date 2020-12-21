---
title: Verify email sources with Sender Policy Framework
date: 2015-07-01T10:47:04-04:00
author: Mehron Kugler
layout: post
categories:
  - Technology
---
**SPF Framework reduces email fraud and spoofing**

Email frauds and scams are successful in part because the email of the sender appears to be from a legitimate source. Sender Policy Framework (SPF) allows email servers to double check that an email came from an authorized source, and reject mail before it lands in anyone's inbox.

A SPF record is a DNS TXT record published by a domain which lists the specific IP addresses or names of servers which are permitted to send its mail. A SPF-aware email server handling incoming mail will check the source IP of a message against the SPF record listed for the incoming message's domain before passing the message to the destination inbox.

A domain may publish a SPF record, and mail servers may be SPF-aware, but this does not prevent spam — there is no heuristic engine built in to SPF to analyze message contents. SPF is simply a gatekeeper, typically assuming any received mail is “guilty” of fraudulence unless proven innocent.

SPF is primarily useful in protecting any outside emails from being sent using your domain name and reducing fraud attempts against your customer base, because a spammer won't be able to fake an email address from your domain. If he/she has actually compromised a server within a SPF-protected domain, it becomes more traceable.

A second benefit of SPF is it reduces backscatter_,_ an indirect method of spam caused when a spammer uses a domain, or more specifically a specific email address (spoofing), as the “from” or “reply-to” address while hammering thousands of targets, invalid or not.

Typically, in a backscatter strategy, the contents of the spam message will still be delivered to the from/reply-to address, only encapsulated by scores of “Your message could not be delivered”, “bulk unsolicited email” and other server warning replies. A SPF-aware server will see that the spoofed sender email address isn't from an authorized source, and will block it whether or not the destination address actually exists.

## **Limitations**

SPF in some cases can break mail forwarding from outside the domain to within, which is expected, since the message envelope is preserved during forwarding. This is addressed with Sender Rewriting Scheme (see <http://www.openspf.org/SRS>).

&nbsp;

## **Implementation**

Naturally, email servers need to be SPF-aware to take advantage of a domain's SPF record. A number of mail servers natively support SPF, including Courier, Exim, Communigate Pro — see [www.openspf.org/implementations](http://www.openspf.org/implementations) for the full list as well as extensions and patches for existing mail servers (Postfix, Sendmail, IIS, Exchange). Add the appropriate extensions your email servers and coordinate with business partners to do the same.

A SPF policy is a DNS TXT record, specifies the SPF version used, contains a list of permitted sources or matching methods (called “mechanisms”), typically followed by “-all” or some variation. A framework query tool is available for looking up a domain's SPF record ([www.spf-all.com](http://www.spf-all.com/)), used in the following SPF implementation examples.

Complete syntax documentation is [available here](about:blank).

&nbsp;

**Example 1 (Bitsighttech.com):**

<pre>bitsighttech.com. IN TXT “v=spf1 include:_spf.google.com ~all”</pre>

  1. v=spf1 — indicates the record is using SPF version 1 (standard implementation)
  2. include: \_spf.google.com  — the SPF record at \_spf.google.com is looked up, “and the IP blocks referenced in it”.
  3. ~all — a “soft fail” which allows all mail through but “marks” failures; “The soft fail can be used when there is a lightweight &#8230; spam filtering engine.”

What exactly is substituted in an include: mechanism? An additional query of _spf.google.com reveals that its SPF record is yet another set of include: references :

<pre>v=spf1 include:_netblocks.google.com include:_netblocks2.google.com include:_netblocks3.google.com ~all</pre>

Examination of the SPF record for _netblocks.google.com reveals a large set of IP blocks:

<pre>v=spf1 ip4:216.239.32.0/19 ip4:64.233.160.0/19 ip4:66.249.80.0/20 ip4:72.14.192.0/18 ip4:209.85.128.0/17 ip4:66.102.0.0/20 ip4:74.125.0.0/16 ip4:64.18.0.0/20 ip4:207.126.144.0/20 ip4:173.194.0.0/16 ?all

</pre>

**Example 2: Amazon.com:**

<pre>amazon.com. IN TXT “v=spf1 include:spf1.amazon.com include:spf2.amazon.com include:amazonses.com -all”</pre>

This record delegates all SPF checking to the spf1 and spf2.amazon.com servers, which most likely link to another subset of SPF records, similar to Google.

&nbsp;

**Example 3: Set up a SPF record for example.com using specific IP addresses of example.com's mail servers, and block all other sender origins:**

<pre>example.com IN TXT “v=spf1 ip4:192.168.34.2 ip4:192.168.35.6 -all”</pre>

The “-” modifier in front of “all” will return a SPF FAIL result for any mail from servers other than the two IP addresses listed.
