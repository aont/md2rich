# md2rich

`md2rich` is a small, browser-based utility that turns Markdown into formatted HTML and copies both rich-text and plain-text versions to the clipboard. It also provides a live preview, making it useful when moving Markdown content into email clients, document editors, and other rich-text applications.

## Features

- Live Markdown preview
- Automatic light/dark theme based on the operating system preference
- GitHub Flavored Markdown support, including tables and task lists
- Rich-text clipboard output (`text/html`)
- Minified JavaScript output that appends the generated HTML to `#prompt-textarea`
- Plain-text Markdown clipboard fallback (`text/plain`)
- Compatibility fallback for browsers without the modern Clipboard API
- No build step or application server required
- Automatic deployment to GitHub Pages

## How to use

1. Open the application in a browser.
2. Enter or paste Markdown into the text area.
3. Review the rendered result in the **Preview** section.
4. Select **Copy as rich text**.
5. Paste the result into an application that accepts formatted content.

Alternatively, select **Copy JavaScript** to copy a minified script. Running that
script on a page containing `#prompt-textarea` appends the generated HTML to the
field and dispatches an `input` event so the host application can detect the
change.

Use **Clear** to remove the current Markdown and reset the preview.

## Run locally

The project is a static website, so you can serve the `public` directory with any static file server. For example, with Python 3:

```bash
git clone <repository-url>
cd md2rich
python3 -m http.server 8000 --directory public
```

Then open <http://localhost:8000>.

Serving the files over HTTP is recommended instead of opening `public/index.html` directly. Browser clipboard features are generally available only in a secure context, such as HTTPS or localhost.

## Project structure

```text
.
├── .github/workflows/pages.yml  # GitHub Pages deployment workflow
├── public/index.html            # Application markup, styles, and JavaScript
├── LICENSE                      # MIT license
└── REDME.md                     # Project documentation
```

## Dependencies

The application loads [marked](https://marked.js.org/) from jsDelivr at runtime. An internet connection is therefore required unless the dependency is downloaded and served locally.

## Deployment

The GitHub Actions workflow publishes the contents of `public` to GitHub Pages whenever relevant files are pushed to the `main` branch. It can also be started manually from the Actions tab.

To enable deployment in a fork:

1. Open the repository's **Settings**.
2. Go to **Pages**.
3. Set **Source** to **GitHub Actions**.
4. Push a change under `public`, or run the workflow manually.

## Security note

The preview renders generated HTML directly in the page. Only paste Markdown from sources you trust, especially because marked does not sanitize HTML embedded in Markdown.

## Browser compatibility

The best experience is available in current versions of Chrome, Edge, Firefox, and Safari. Clipboard behavior can vary by browser and by the destination application. If rich-text clipboard access is unavailable, the application attempts a legacy browser copy operation.

## License

This project is available under the [MIT License](LICENSE).
