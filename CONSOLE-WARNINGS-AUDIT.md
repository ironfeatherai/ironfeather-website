Suspicious references checked during Pass 3:

- `signature-preview.html`: `https://ironfeatherai.github.io/ironfeather-website/LOGO-LOCKED.png`
  - Used twice for the email signature logo preview.
  - Reason flagged: this is an absolute GitHub Pages path for `ironfeather-website`, while the current repo serves a local `LOGO-LOCKED.png` and the production domain is `ironfeather.ai`. DNS/network checks were unavailable in the shell, so this was not changed.
