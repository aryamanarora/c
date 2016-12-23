---
title: "Week 6"
author: "Aryaman Arora"
date: "November 15, 2016"
output:
  md_document: default
  tufte::tufte_html:
    highlight: pygments
---

We're moving from the command line to the browser; C to PHP and HTML and CSS.

## `pset5`
We're also going to make a spell-checker for pset5. We have a choice of what data structure we use:

- arrays
- linked lists ($O(n)$)[^figure]
- hash tables ($O(1)$ best case[^time])
- tries (fast but lots of memory)

Ooh, `pset5` is known to be the hardest pset! Good luck!

### Hash functions
**Hash functions** take in data and shrinks it down with an algorithm. An example is *SHA1*.

A note about current events: unfortunately, researchers have found ways to reverse engineer hash functions. Now they have moved to *SHA256*.

[^figure]: ![](images/download.png)
[^time]: We aren't just going to use theoretical big-O notation; we're going to actually time our implementation.

## IP Addresses
Every internet-connected device has an address, used for identifying each other.

How are addresses given? A **DHCP** server assigns addresses whenever you connect to a wifi network. These are called *IP (Internet Protocol) addresses*, with the layout `##.##.##.##`, a 32-bit address.

Another real-world connection: we're running out of IP addresses, and the response has been slow. Now, IPv4 is being replaced by IPv6, 128-bit addresses.

At work networks, IPs often belong to the same starting numbers. Home IP addresses are private IPs, following `10.##.##.##`, etc. Private IPs can be converted by a router to public IPs. To a website, everyone in one public IP are the same person.

## DNS
Websites (servers) have IP addresses to. The **domain name system** assigns names to IP addresses. You can buy (rent) a domain name for your website.

You can look up an IP address for a website with `nslookup <website>`.

```bash
nslookup google.com
```

Most large websites have several IPs, distributed across servers to reduce load.

## Routers
A **router** is a device that moves data from point A to point B. The router can direct data to other places, serving as hubs for networks.

You can see the router's path to somewhere else with `traceroute <website>`. Normally this does three queries, you can use the option `-q` to set how many queries you want.

```bash
traceroute -q 1 google.com
```

To get to `google.com`, we go to Comcast's Wilmington Island server, to Savannah, to Jacksonville, to Miami, to Nota? And then we stay in Florida.

```bash
traceroute -q 1 www.cnn.co.jp
```

Wow, this is a long one. First, Wilmington Island, then Savannah, then Jacksonville, then Marietta (near Atlanta), then Dallas, then LA, then Bryant (somewhere in California, I presume), and finally we get to Japan! We crossed the Ocean, thanks to those undersea fiber-optic cables.

## Packets
What is data anyways? It isn't a stream of bytes...it's a packet! The data is split into small chunks, and sends them in what are equivalent to *virtual envelopes*. They have to-addresses, from-addresses, and a number, enough to reconstruct the entire set of data.

What if a packet doesn't get to its destination? This is where TCP/IP comes in, a combination of two protocols, *IP*, and *TCP*. TCP is the protocol that ensures a packet reaches its destination.

Having just the to- and from-address is not enough. We also need the **port number**, the service for opening the packet.

Number Port   Usage
------ ------ ------
21     FTP    files
25     SMTP   mail
53     DNS    
80     HTTP   web
443    HTTPS  web

Your browser infers ports for websites but you can be explicit by appending `:80` or `:443`.

## Firewalls
A **firewall** routes all traffic through one device (eg. a router). One kind of firewall can serve the incorrect IP address from the DNS server. To bypass this, you can use a different DNS (Google's `8.8.8.8`) or type in the IP address of the blocked site. However, now Google sees your browsing history.

Modern firewalls can block certains ports and IPs.

### VPNs
On public wifi addresses, packets can be accessed by anyone on the network. This can be used for malicious purposes. To encrypt your packets, you can use a **VPN**, virtual private network.

You do sacrifice speed for security, though. Your packets have to be routed via another server and therfore through more waypoints.

## Use
Why is this useful to know?

Well, HTTP is a protocol for accesssing websites, a set of conventions.

![HTTP](http://imgur.com/yFbNXvE)

Some operations we perform with HTTP are:

### Requests

```
GET / HTTP/1.1
Host: www.google.com
```

We're using HTTP 1.1, and we want [](google.com) from the server.

### Responses
```
HTTP/1.1 200 OK
Content-Type: text/html
```

We rarely see 200 as return number because it is good; on the other hand, `404` is "file not found".

Code Meaning
---- ----------------------------
200  OK
301  Moved permanently (redirect)
302  Found (redirect)
401  Unauthorized
403  Forbidden
404  Not Found
500  Internal Server Error

The content-type is what kind of file is returned.

### Posts
You send key value pairs in the URL as requests. For example, `https://www.google.com/search?q=hello`. What if you want to send an image? Or a password?

```
POST /login.php HTTP/1/1
Host: www.facebook.com
...
email=malan@harvard.edu&password=12345
```

The password can be hidden deeper in the "envelope". Furthermore, HTTPS encrypts this.

## HTML
Woohoo! We made it!

```html
<!DOCTYPE html>

<html>
  <head>
    <title>hello, world</title>
  </head>
  <body>
    hello, world
  </body>
</html
```

HTML isn't a programming language; it's a markup language for websites.

```r
DiagrammeR::grViz("
digraph rmarkdown {
document -> html
html -> head
head -> title
html -> body
}
", height = 200, width = 200)
```

Another language we have is CSS, a styling language. After all, black text on a white background isn't very appealing.