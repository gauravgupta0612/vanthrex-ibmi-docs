---
layout: default
title: Contributing
nav_order: 91
---

# Contributing

Contributions are welcome — to the extension and to these docs.

## The extension

Source: [gauravgupta0612/silverlake-ibmi](https://github.com/gauravgupta0612/silverlake-ibmi)

```bash
git clone https://github.com/gauravgupta0612/silverlake-ibmi.git
cd silverlake-ibmi
npm install
npm run typecheck
npm test
```

Press **F5** in VS Code to run the extension in a development window. Keep pull requests small and add a unit test in `test/` for parser or converter changes.

## These docs

Repository: [gauravgupta0612/vanthrex-ibmi-docs](https://github.com/gauravgupta0612/vanthrex-ibmi-docs)

- Click **Edit this page on GitHub** at the bottom of any page, change the Markdown, and open a pull request.
- Every page is a Markdown file in the root of the repository. The menu comes from `title`, `parent` and `nav_order` at the top of each file.
- The site is published by GitHub Pages with the [Just the Docs](https://just-the-docs.com) theme.

## Reporting bugs

[Open an issue](https://github.com/gauravgupta0612/silverlake-ibmi/issues/new/choose) with your VS Code version, the extension version, your IBM i release, and the relevant lines from **View → Output → Vanthrex for IBM i**.
