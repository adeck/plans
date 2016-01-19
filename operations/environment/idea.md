
# What?

So, for the looooongest time I've wanted my own ecosystem.
I've wanted to run and maintain my own servers for:

- VPN
- DNS
- web (https)
- SSH (bastion host)
- DNS
- IRC
- SMTP + IMAP
- iodine
- SIP / VoIP
- monitoring (splunk, AIDE, nagios, etc.)
- git + gitlab
- issue tracking (prolly MantisBT)
- etc.

But I haven't laid out exactly how I wanted that infrastructure to work, so I feel like doing that is worthwhile to crystallize
in my mind the exact nature of my [Grand Design][sx], so I thought I'd do that here.

# How?

There'll be two separate VMs which serve an administrative purpose; the SSH server and the VPN server. We'll call all
the other servers by common crypto names because they're specific services aren't relevant.

In subsequent discussion, public-internet-facing services not intended for the general public must be hidden behind SPA
running on a pseudorandomly chosen port, and the service(s) hidden by SPA must also be running on nonstandard
pseudorandomly chosen ports. If it's possible to protect nonregistered ports as if they were registered, then do so, otherwise use pseudorandomly chosen registered ports.

## VPN server

The only publicly-accessible service is key-based VPN.
The VPN should be:

- UDP
- not the default route for any client

All other machines within the infrastructure are clients within this VPN, and communication between hosts should take
place over the VPN. Even within the VPN, interhost communication should still only take place over encrypted channels
(so that, should the VPN server itself become compromised, it can DoS servers but not MitM their connections).

The VPN's job is to hide the servers from each other as much as possible, and hide the nature of their traffic from
other hosts on their respective networks. This is done, in part, to make recognizing a compromised host easier, and in
part to decrease the attack surface; IP addresses cannot be spoofed within the VPN, so if any server aside from the VPN
is attacked that attack can be accurately monitored, reported, and automatically halted by automatically isolating the
offending server.

If the VPN server itself is under attack, 

## SSH server

The only service accessible from the public internet is key-based ssh access.

[sx]: https://www.youtube.com/watch?v=wc62kCsDT9M
