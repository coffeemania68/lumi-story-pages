# Lumi Story — GitHub Pages snapshot

This is an independently deployable static snapshot of the Lumi Story website. It is intentionally separated from the existing dream interpretation app and blog repositories.

## Local preview

Serve this directory with any static file server. No Manus runtime is required by the HTML shell.

## GitHub Pages

The repository is configured for GitHub Actions Pages deployment. The custom domain is declared in `CNAME` as `story.mypawstory.com`.

## Language behavior

The EN control remains a direct link to the pre-translated English content at `https://dream.mypawstory.com/en/`. No automatic translation script is included.

## Important limitation

This package was reconstructed from the publicly served static HTML, JavaScript, CSS, and public media assets because the original editable Manus source package was not available at the time of export. It should be visually and behaviorally tested before DNS cutover.
