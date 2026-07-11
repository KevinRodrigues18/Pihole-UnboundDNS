## ✪ Verification & Testing
`DNS resolution`: Confirmed queries resolve correctly through the full chain (client → Pi-hole → Unbound → root servers) using dig and nslookup from client devices.

`Ad blocking`: Verified against known ad/tracker test domains and confirmed via the Pi-hole query log that they were blocked before ever reaching Unbound.
`DNSSEC validation:` Confirmed Unbound correctly rejects deliberately misconfigured/invalid DNSSEC test domains.
`Failover behavior:` Container restarts (docker compose restart unbound) to confirm Pi-hole handles a temporarily unavailable upstream.
<img width="30%" height="30%" alt="image" src="https://github.com/user-attachments/assets/c4efc2a0-0503-4def-8399-3b236a91d9df" />


