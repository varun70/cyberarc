# Cyber Security Explorer

An interactive, single-page guide that teaches core cybersecurity ideas visually. Pick an attack or a defense, watch an animated step-by-step walkthrough, compare topics side by side, then test yourself with a quiz and incident-response drills.

Inspired by the Networking Protocol Explorer concept, rebuilt for security.

**Live demo:** `https://cyberarc.vanarsec.in/` *(replace after you deploy)*

<!-- Add a screenshot after deploying:
![Cyber Security Explorer](docs/screenshot.png)
-->

## Features

- **24 topics**: 13 attacks and 11 defenses, each with an overview, key characteristics, and the confidentiality, integrity and availability (CIA) impact.
- **Animated walkthroughs**: play, pause, step back and forward through how each attack or defense works.
- **Defend and detect guidance**: practical mitigations, warning signs and known limits for every topic.
- **Compare mode**: pick up to three topics and view them in a table.
- **Quiz**: 8 randomized questions per round, generated from the topic data, with an explanation after each answer.
- **Incident drills**: three scenarios (impossible-travel sign-in, ransomware on a file server, suspicious web requests) with feedback at every decision.
- **Search and filters**: by type (attack or defense), category and keyword.
- **Shareable links**: open a topic directly, for example `index.html#sqli`.
- **Dark and light themes**, keyboard navigation, screen-reader labels, reduced-motion support and a mobile-first layout.
- **Zero dependencies and no tracking**: one HTML file, no build step, no cookies, no analytics.

## Topics

**Attacks:** Phishing, SQL injection, Cross-site scripting (XSS), Ransomware, DDoS, Man-in-the-middle, Credential stuffing, Supply chain attack, Zero-day exploit, Insider threat, Privilege escalation, DNS spoofing, Cloud misconfiguration.

**Defenses:** Multi-factor authentication, Firewall and WAF, EDR, SIEM, Zero Trust, TLS encryption, Network segmentation, Backups (3-2-1), Patch management, Incident response, Data loss prevention.

> The counts above reflect the topic list in `index.html`. If you add or remove topics, update this section and the headline number on the page.

## Run locally

No install needed. Either open the file directly:

```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

or serve it with any static server:

```bash
python3 -m http.server 8080
# then visit http://localhost:8080
```

## Deploy

The project is static, so any static host works.

### GitHub Pages

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select `main` and `/ (root)`, then save.
4. Your site appears at `https://<your-username>.github.io/<repo-name>/` within a couple of minutes.

### Custom domain (optional)

1. Add a `CNAME` DNS record for your subdomain pointing to `<your-username>.github.io`.
2. In **Settings → Pages → Custom domain**, enter the subdomain and save.
3. After GitHub verifies it, enable **Enforce HTTPS**.

### Other hosts

Cloudflare Pages, Netlify and Vercel all deploy this repository with no build command and `/` as the output directory.

## Customize and extend

All content lives in the `ITEMS` array inside `index.html`. To add a topic, append an object like this:

```js
{
  id: "example",                 // unique, letters and digits only (used in the URL hash)
  kind: "attack",                // "attack" or "defense"
  name: "Example topic",
  cat: 0,                        // index into the CATS array
  short: "One-line summary shown on the card.",
  overview: "Two or three sentences of explanation.",
  traits: ["Key characteristic", "Another one"],
  cia: "CI",                     // any of C, I, A
  ref: "MITRE ATT&CK T0000",     // optional, use "" if none
  actors: [["Attacker", "bad"], ["Victim", "n"]],   // "bad", "good" or "n"
  steps: [
    // [fromActorIndex, toActorIndex, "short label", "caption", "bad|good|n"]
    // use the same index for both actors to draw a note instead of an arrow
    [0, 1, "Does something", "Longer explanation shown under the diagram.", "bad"]
  ],
  actions: ["Mitigation or good practice"],
  signals: ["Warning sign (attacks) or limitation (defenses)"],
  related: ["otherTopicId"]      // ids of related topics
}
```

The quiz and compare mode pick up new topics automatically. Add drills by extending the `DRILLS` array.

## Project structure

```
.
├── index.html   # the entire app: markup, styles, data and logic
├── README.md
└── LICENSE
```

## Accessibility

- Semantic landmarks, a skip link and labeled controls
- Full keyboard support, including arrow keys between tabs
- Visible focus states and sufficient color contrast in both themes
- Respects `prefers-reduced-motion` and `prefers-color-scheme`

## Accuracy and responsible use

Walkthroughs are simplified for learning, and real incidents vary. This project is not a substitute for formal training, vendor documentation or your organization's policies. Only practice offensive techniques on systems you own or have written permission to test.

References to MITRE ATT&CK, OWASP and NIST are provided for further reading; those names belong to their respective owners.

## Roadmap ideas

- More topics: ransomware negotiation, OT/ICS security, API security, mobile threats
- Printable one-page cheat sheets per topic
- Progress tracking for the quiz (stored locally in the browser)
- Translations

## Contributing

Issues and pull requests are welcome. Please keep content accurate, cite a public reference where possible, and keep the project dependency-free.

## License

Released under the [MIT License](LICENSE).

## Author

Built by Varun.
