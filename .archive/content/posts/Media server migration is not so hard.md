---
title: "Media Server Migration Is Not So Hard"
date: 2025-08-16T22:02:44+01:00
draft: true
---

# Jellyfin migration
This is maybe the most painful one but not nearly as bad as people make it sound in the _interwebs_.

This is really a matter of installing Jellyfin by the typical install script, and then copy everything from your old server into your new one and finally set appropriate permissions to the data and configuration directories. It really just works.

# Servarr migration
This is very easy, just the same as for Jellyfin but in this case you will have only one directory to modify per application.

One thing that will change anyway is the API keys from each app

# Wireguard
Enable your configuration by enabling the server
```
systemctl enable --now wg-quick@<yourconfig>
```
