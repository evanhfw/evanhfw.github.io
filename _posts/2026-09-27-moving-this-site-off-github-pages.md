---
title: "Moving this site off GitHub Pages"
date: 2026-09-27
tags: [self-hosting, homelab, jekyll, docker]
---

For a while this portfolio was a plain Jekyll repo served by GitHub Pages. That worked fine. So why move it onto my own machines?

Mostly because I already run a small homelab, and a portfolio that is itself an engineering project is a more honest advertisement than a static file dump. I also wanted the practice: TLS, reverse proxying, caching, and build pipelines are things I care about, and this site is a safe place to test them.

## How the site is served now

The path from a visitor to the content looks like this:

```
Cloudflare (DNS + edge)
  -> VPS: Caddy          (public entry, TLS via DNS-01)
    -> Tailscale mesh    (private network between machines)
      -> home nginx      (serves this static Jekyll build)
```

What each hop does:

- **Cloudflare** terminates TLS for the domain and proxies traffic. The DNS zone lives there, and a scoped API token handles DNS-01 certificate challenges.
- **The VPS** is the only machine with a public entry point. Caddy handles virtual hosts, certificates, and reverse proxying. It is the one box I could lose and rebuild in an hour.
- **Tailscale** connects the VPS to the home server. The web container at home listens only on the tailnet address: not on the local network, not on the internet.
- **nginx at home** serves a static build from a read-only directory that the build pipeline writes into.

## Why bind to the tailnet only

The usual home server web setup means port forwarding and dynamic DNS, and it puts your house on the internet. I prefer the opposite: nothing at home is exposed. The VPS is the single public surface, and it reaches into my network over the private mesh. If the VPS changes, exactly one hop changes.

## The build pipeline

Content is a small Jekyll repository. One script builds it in a pinned Docker image (Ruby, Jekyll, and the theme gem), and the output directory is mounted read-only into the nginx container. Publishing an update is: edit markdown, run the script, refresh. No container restarts, no deploy daemon, no CI minutes.

## A few things I learned

- Static sites are the easiest thing to self-host well: no database, no runtime, and no attack surface beyond a file server.
- Keep the public surface tiny. One public entry host, everything else on a private mesh.
- Pin your dependencies. The build image pins exact gem versions, and the build is one script, so a rebuild a year from now behaves like today's.
- Caches have long memories. When you fix an asset, remember that CDNs and browsers may keep serving the old bytes for hours; version your asset URLs when it matters.

(There was also a small adventure with image formats: I converted my profile photo to a lean WebP and accidentally flattened its transparency, which turned a round portrait into a black square. That is a story for another post.)

The source of this site lives on [GitHub](https://github.com/evanhfw). If you run a small home server and have been meaning to move your site onto it: it takes an afternoon, and you get to keep the tinkering.
