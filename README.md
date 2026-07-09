# Booting into Kubernetes with an Immutable OS

> Talk delivered at **Cloud Native Valencia 2026** by **Santiago Merlos**.

How the real problem of operating Kubernetes on-prem forced us to rethink
what it even means to _install_ a node — and how Flatcar Container Linux,
declarative provisioning (Butane / Ignition), system extensions, and
network boot let us stop installing nodes and start provisioning them.

---

## 📑 Abstract

Kubernetes platforms often struggle with configuration drift and inconsistent
environments across clusters. What if the operating system itself was
immutable and fully controlled through declarative configuration?

This deck walks through the design of an immutable Kubernetes platform built
on top of **Flatcar Container Linux**, optimised for on-premises environments.
By removing traditional package managers and mutable system components, the
platform eliminates configuration drift while shrinking the attack surface.
Custom system extensions deliver tightly integrated components; the OS is
preconfigured and tuned specifically for Kubernetes, with kernel parameters
and system-level settings aligned with the architecture of the **SIGHUP
Distribution**.

A live demo bootstraps a cluster from a PXE boot to a fully operational
immutable Kubernetes cluster with a single command.

---

## 📂 Repository layout

```text
cloud-native-valencia-2026/
├── README.md                       ← you are here
├── slides.md                       ← Marp source (single source of truth)
├── themes/
│   └── booting-into-kubernetes.css ← custom Marp theme (extends gaia)
├── assets/
│   ├── flatcar-logo.svg
│   ├── cncf-logo.svg
│   └── qr/
│       ├── furyctl.png             ← github.com/sighupio/furyctl
│       ├── distribution.png        ← github.com/sighupio/distribution
│       ├── linkedin.png            ← linkedin.com/in/smerlos
│       └── slides.png              ← /releases/latest (PDF · PPTX)
├── .github/workflows/
│   ├── lint.yml                    ← prettier + markdownlint + build check
│   └── release.yml                 ← push main → overwrite single 'latest' release
├── package.json                    ← marp-cli pinned
├── mise.toml                       ← render tasks
└── LICENSE                         ← CC BY 4.0
```

---

## 🚀 Build the deck

### With [mise](https://mise.jdx.dev/)

```bash
mise install         # installs Node LTS
mise run render      # → dist/slides.html
mise run pdf         # → dist/slides.pdf
mise run pptx        # → dist/slides.pptx  (preserves speaker notes)
mise run serve       # live preview on http://localhost:8080
```

### Without mise

```bash
npm install
npm run render       # → dist/slides.html
npm run pdf          # → dist/slides.pdf
npm run pptx         # → dist/slides.pptx
npm run serve        # live preview
```

First PDF/PPTX run will download a Chromium build (~200 MB) via Puppeteer.

### Lint / format

```bash
npm run lint         # prettier --check + markdownlint (README)
npm run format       # prettier --write
```

---

## 📦 Releases

Every push to `main` rebuilds the deck and **overwrites a single release**
tagged `latest` with the PDF, PPTX, and HTML attached — no manual tagging, and
versions never accumulate. You can also trigger the **Release** workflow by
hand from the Actions tab (`workflow_dispatch`).

Because there is always exactly one release, the presentation QR on the Q&A
slide points at a permanent URL —
[`/releases/latest`](https://github.com/smerlos/cloud-native-valencia-2026/releases/latest) —
so the reference printed on the slide never breaks and the audience always
gets the current build.

---

## 🎨 Theme

The deck uses a custom Marp theme — `themes/booting-into-kubernetes.css` —
that extends Marp's built-in `gaia` theme. The look is intentionally minimal:

- Pure black background (`#000000`), white text (`#ffffff`), gray scale for hierarchy
- System font stack, no Google Fonts
- No icons, no background art, no accent palette beyond a single warm/cold
  pair for the comparison table
- The story carries the deck

To edit the theme, change `themes/booting-into-kubernetes.css` and re-render.
Slide content stays clean and editable in `slides.md`.

---

## 📞 Contact

| Channel  | Handle / URL                                                    |
| -------- | --------------------------------------------------------------- |
| LinkedIn | [linkedin.com/in/smerlos](https://www.linkedin.com/in/smerlos/) |
| GitHub   | [github.com/smerlos](https://github.com/smerlos)                |

**Project repos referenced in the talk:**

- [github.com/sighupio/furyctl](https://github.com/sighupio/furyctl) — lifecycle CLI
- [github.com/sighupio/distribution](https://github.com/sighupio/distribution) — modular Kubernetes distribution
- [flatcar.org](https://www.flatcar.org/) — container-optimised Linux OS (CNCF)

---

## 📜 License

Slide content released under **CC BY 4.0** — see [`LICENSE`](./LICENSE).
Feel free to fork for your local meetup; please keep attribution.

### Disclaimer

This material is provided **"AS IS"**, without warranty of any kind,
express or implied — including merchantability, fitness for a particular
purpose, accuracy, or non-infringement. The author assumes **no liability
or responsibility** for any direct, indirect, incidental, or consequential
damages arising from the use of this material.

The slides and demos are for **educational purposes only**. Code,
configurations, and procedures shown are illustrative; **always verify
against current upstream documentation** before applying them to
production systems.

Third-party trademarks (Flatcar logo, CNCF lockup) are property of their
respective owners and used per their public artwork policies.
