# VLSI Notes

[![GitHub Repo](https://img.shields.io/badge/GitHub-Saicharan%2Fvlsi--notes-24292e?style=for-the-badge&logo=github)](https://github.com/Saicharan-malyala/vlsi-notes)
[![Docs Status](https://img.shields.io/badge/Docs-Online-4caf50?style=for-the-badge&logo=readthedocs)](<!-- Live URL will be added after deployment -->)
[![License: CC BY‑SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey?style=for-the-badge)](https://creativecommons.org/licenses/by-sa/4.0/)
[![Build Status](https://img.shields.io/github/actions/workflow/status/Saicharan-malyala/vlsi-notes/deploy.yml?branch=main&style=for-the-badge&logo=github-actions)](https://github.com/Saicharan-malyala/vlsi-notes/actions)

---

## 📖 Overview

VLSI Notes is a concise, well‑organized collection of materials covering Linux fundamentals and VLSI design & verification. The repository provides labs, question banks, and explanations that support self‑study and classroom use, following the **PGCP‑VLSI** curriculum from **CDAC Hyderabad**.

---

## 🌐 Access

- **Online (deployed)** – Once the GitHub Pages site is published, it can be accessed at the live URL (to be added after deployment).
- **Local development** – Clone the repository and build the site locally:

```bash
# Clone the repo
git clone https://github.com/Saicharan-malyala/vlsi-notes.git
cd vlsi-notes

# (Optional) Create a virtual environment
python -m venv .venv && .venv\\Scripts\\activate

# Install dependencies
pip install -r requirements.txt

# Serve the documentation locally
mkdocs serve
```

Both methods give you full access to the content.

---

## 📚 Repository Structure

```text
vlsi-notes/
├─ .github/               # CI/CD workflow
├─ data/                  # JSON question banks for assignments
├─ docs/                  # MkDocs source files
│   ├─ index.md           # Landing page
│   ├─ modules/           # Core curriculum modules
│   │   └─ linux-shell-scripting/
│   │       ├─ 01-ubuntu-installation-virtualbox.md
│   │       └─ … (09‑shell‑scripting.md)
│   └─ assignments/       # Interactive study pages
├─ site/                  # Generated static site (output)
├─ mkdocs.yml             # MkDocs configuration
├─ requirements.txt       # Python dependencies
└─ README.md              # This file
```

---

## 🤝 Contributing

Contributions are welcome. To get started:
1. Fork the repository.
2. Create a feature branch (`git checkout -b my‑feature`).
3. Make your changes, preserving the MkDocs Material style.
4. Run `mkdocs build --strict` to verify there are no broken links.
5. Open a Pull Request with a clear description of your changes.

Please follow the guidelines in `CONTRIBUTING.md` for coding standards and the review process.

---

## 📜 License

The documentation is licensed under the **Creative Commons Attribution‑ShareAlike 4.0 International** license. See the `LICENSE` file for details.

---

## 🙏 Acknowledgements

- **PGCP‑VLSI, CDAC Hyderabad** – the curriculum framework that guides the content.
- All contributors who have helped refine the material.

---

## 📞 Contact & Author

**Sai Charan** – VLSI enthusiast & documentation author

- GitHub: [Saicharan‑malyala](https://github.com/Saicharan-malyala)
- LinkedIn: [saicharan‑malyala](https://linkedin.com/in/saicharan-malyala)

Feel free to open an issue for any questions, suggestions, or collaborations.

---

*Built with **MkDocs Material**, **Pymdown‑extensions**, and a focus on clear, accessible documentation.*
