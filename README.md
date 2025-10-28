# HomeServer
A Home Server using Raspberry to stop relying on web services and run my DIY projects

## What I'll Need

**Hardware:**
- [ ] A Raspberry Pi 5
- [ ] microSD card 64GB, Class 10
- [ ] Power supply.
- [ ] 3D Printed case.
- [ ] Touchscreen.

**Software:**
Raspberry Pi OS: The official, beginner-friendly operating system.
My Server Application: A web server written in Python using Flask.


### Remote Access Method using Secure Tunnels
A service running on your Pi creates a secure, outbound connection (a "tunnel") to a public server. Your requests go to the public server, which then forwards them through the secure tunnel to your Pi.

**How it works:** I run a small piece of software on your Pi that connects to the service. No port forwarding or dynamic DNS is needed.

**Why it's great:**
* Extremely Secure: I don't open any incoming ports on my home router. My server isn't directly exposed to the internet.
* Easy to Set Up: Often simpler than dealing with router settings.
* Bypasses Network Restrictions: Works even if my ISP uses Carrier-Grade NAT (CG-NAT), which makes port forwarding impossible.

**Recommended Service:** Cloudflare Tunnels
**Cost:** Free for personal use.
**Setup:** Install the cloudflared agent on my Pi. After a one-time setup, it creates a persistent, secure tunnel to Cloudflare's network. I get a secure https:// URL that I can use to access my project.

## Recommended Step-by-Step Plan

**Base Pi Setup:**

1. Install Raspberry Pi OS Lite (64-bit) on my microSD card.
2. Boot up my Pi, connect it to my network, and run sudo apt update && sudo apt upgrade to get everything up to date.
3. Assign a static local IP address to my Pi so it doesn't change on my home network.

**Develop My Application:**

1. Create my project's server application. A Python Flask web server that provides secure API endpoints.
2. Test it to make sure I can access it from another computer on my local network first.

**Set Up Cloudflare Tunnels:**

1. Sign up for a free Cloudflare account.
2. Follow their official "Get Started" guide for Tunnels. The process is roughly:
    1. Add a website to Cloudflare (you can register a cheap domain or use a free one).
    2. Navigate to Zero Trust -> Access -> Tunnels.
    3. Create a new tunnel and give it a name.
3. Cloudflare will give me a command to run on my Pi to install the cloudflared connector.
4. Configure the tunnel to point to my local service. For example, I can route traffic from test.mydomain.com to localhost:5000 (or whatever port my Flask app is running on).

**Access from Anywhere!**
Once the tunnel is active, I can access my project from any browser or device in the world by navigating to the public hostname I configured. It's secure, encrypted, and reliable—all for free.
