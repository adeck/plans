
# What?

So, for the looooongest time I've wanted my own ecosystem.
I've wanted to run and maintain my own servers for:

- VPN
- DNS
- web (https)
- SSH (bastion host)
- DNS
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
pseudorandomly chosen ports.

## VPN server

The only publicly-accessible service is key-based VPN.
The VPN should be:

- UDP based
- not the default route for any client

All other machines within the infrastructure are clients within this VPN, and communication between hosts should take
place over the VPN where possible, falling back to the regular network only when the VPN is down.

## SSH server

The only service accessible from the public internet is key-based ssh access.

[sx]: https://www.youtube.com/watch?v=wc62kCsDT9M
