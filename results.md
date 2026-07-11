## ✪ Verification & Testing
`DNS resolution`: Confirmed queries resolve correctly through the full chain (client → Pi-hole → Unbound → root servers) using dig and nslookup from client devices.

`Ad blocking`: Verified against known ad/tracker test domains and confirmed via the Pi-hole query log that they were blocked before ever reaching Unbound.
`DNSSEC validation:` Confirmed Unbound correctly rejects deliberately misconfigured/invalid DNSSEC test domains.
`Failover behavior:` Container restarts (docker compose restart unbound) to confirm Pi-hole handles a temporarily unavailable upstream.
<img width="50%" height="50%" alt="image" src="https://github.com/user-attachments/assets/c4efc2a0-0503-4def-8399-3b236a91d9df" />

---  
`Ad blocking`: Verified against known ad/tracker test domains and confirmed via the Pi-hole query log that they were blocked before ever reaching Unbound.

```
2026-07-11 20:30:22.817 query[A] www.googleadservices.com from 192.168.0.101
2026-07-11 20:30:22.817 gravity blocked www.googleadservices.com is 0.0.0.0
2026-07-11 20:30:22.818 query[AAAA] www.googleadservices.com from 192.168.0.101
2026-07-11 20:30:22.818 gravity blocked www.googleadservices.com is ::
2026-07-11 20:30:23.024 query[AAAA] ogads-pa.clients6.google.com from 192.168.0.101
2026-07-11 20:30:23.024 gravity blocked ogads-pa.clients6.google.com is ::
2026-07-11 20:30:23.024 query[A] ogads-pa.clients6.google.com from 192.168.0.101
2026-07-11 20:30:23.025 gravity blocked ogads-pa.clients6.google.com is 0.0.0.0
2026-07-11 20:30:26.400 query[AAAA] www.gstatic.com from 192.168.0.101
2026-07-11 20:30:26.400 cached www.gstatic.com is 2404:6800:4000:101f::5e
```

`DNSSEC validation:` Confirmed Unbound correctly rejects deliberately misconfigured/invalid DNSSEC test domains.  

<img width="50%" height="50%" alt="image" src="https://github.com/user-attachments/assets/a662caa2-c474-496d-93ae-6ba24ed8eb9f" />

Portainer Containers Dashboard  
<img width="100%" height="100%%" alt="image" src="https://github.com/user-attachments/assets/b4c7fa76-1b2b-4486-ab91-6dbc36a0f9bc" />



