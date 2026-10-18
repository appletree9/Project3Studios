PROJECT3STUDIOS V.1 SCULPT — iPHONE PWA

1. Upload ALL files in this folder together to an HTTPS static host (Netlify Drop, GitHub Pages, etc.).
2. Open the published HTTPS URL in Safari on your iPhone.
3. Tap Share > Add to Home Screen > Add.
4. Launch from the Home Screen.

For Netlify: go to https://app.netlify.com/drop and drag the unzipped folder onto the page from a computer.

This package uses your existing editor. Three.js modules are loaded from jsDelivr CDN. An internet connection is needed on first load; offline use is not guaranteed until required modules have been successfully cached.

PWA installation does not upload your sculpting projects automatically. Export/save backups yourself. The mobile UI and iPhone WebGL behavior still require physical-device testing.

UPDATE NOTE: Replace all files in the repository root. The service worker now fetches updated HTML from the network before using cached HTML. GitHub Pages may take several minutes to publish. If an installed iPhone Home Screen app still shows the old version, open the GitHub Pages site in Safari, reload, then close and reopen the Home Screen app.
