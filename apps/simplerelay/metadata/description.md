# SimpleRelay

A self-hosted SMTP relay. Point your printers, scripts and apps at it, and it forwards their mail through your existing email accounts (Gmail and similar), with a web dashboard, DNS checks, a mail log and an allow-list of clients.

This is a **hardened build** of [toinbox/simplerelay](https://github.com/toinbox/simplerelay): self-registration is off, weak secrets are refused at startup, provider hosts are validated and blocked from private ranges, logins are rate-limited, and stored credentials are encrypted.

## After installing

1. Open the dashboard and sign in with the admin email and password you entered at install.
2. Add a provider (your email account, usually with an app password).
3. Add an access rule for each device: its IP address, or an SMTP-AUTH login. **Without a rule, nothing can relay.**
4. Point devices at `<this host>:2525`, with no TLS and a sender address that matches the provider.

## Good to know

- **Keep it off the internet.** Use it on your LAN or over a VPN, and firewall port 2525 to the devices that need it.
- **Back up the secret key and the database folder.** Saved provider passwords are encrypted with the secret key; if it changes they must be re-entered.
- The admin password is only used on first start. Change it later in the dashboard.
- The SMTP listener on 2525 does not use TLS, so prefer IP-based access rules on a trusted network.
- Provider hosts on private addresses (for example an internal mail server) are blocked by default.
