# Quick start guide

- Visit <https://xapi-project.github.io/new-docs/> to view the current documentation.

## Required software

The docs use Hugo and the [Hugo Relearn theme](https://mcshelby.github.io/hugo-theme-relearn),
an enhanced fork of the popular Hugo Learn theme.

### Supported versions of Hugo and the Hugo Relearn theme

Hugo Relearn 6.4.0 is currently used (defined by a git tag in `doc/go.mod`).

- The minimum Hugo version required by the Relearn theme is 0.126.0.
- The current Ubuntu `snap` (which provides 0.142.0) also works.

## Installation

- Install Hugo 0.126 or newer (required by the Hugo Relearn theme)
  follow the guidance on <https://gohugo.io/installing>.
  You'll need to install Go as well: see <https://go.dev/>
  - On Ubuntu, use the `snap` package:
    - `sudo snap install hugo` installs the current version
      `apt-get install hugo` would install a version that is too old,
      (this applies up to Ubuntu 24.04)

  - To install Hugo from source, you need a recent `golang-1.2x` compiler:
    - On Ubuntu 22.04, this can be done with:

      ```bash
      sudo apt install golang-1.23-go
      # Add it to your path, assuming your .local/bin/ is early in your PATH:
      ln -s /usr/lib/go-1.23/bin/go ~/.local/bin/go
      go version
      go install github.com/gohugoio/hugo@v0.127.0
      ```

## Development

- Run a local server: `hugo server`
- Open a browser at <http://127.0.0.1:1313/new-docs/>
- Add content to `doc/content/`:
  - Documents are written in Markdown.
  - Please wrap lines in paragraphs to make reviews more manageable.
  - The menu hierarchy comes mainly from the directory structure in `content/`.
  - A file called `_index.md` is needed in a directory to define a new level in the menu.
    - To set the page title,
      [use the front matter](https://gohugo.io/content-management/front-matter/).
  - For a page that has images or other stuff included, it is best to create a new directory:
    Put the contents in an `index.md` file (no `_`) and the related files next to it.
    See <https://gohugo.io/content-management/organization/> for more information.

  See <https://mcshelby.github.io/hugo-theme-relearn/> for more information about
  the features of the Relearn theme, including handy "shortcodes".

Note: When switching versions, before re-generating the documentation using
`hugo server`, delete the previously generated static site using `rm -r docs/public`.

### Notes for supporting current versions of Hugo and the Relearn theme

Backported fixes to support newer Hugo versions:

- `layouts/partials/header.html`, it fixes:
  ```js
  ERROR deprecated: .Sites.First was deprecated in Hugo v0.127.0 and will be removed in Hugo 0.143.0. Use .Sites.Default instead.
  ```
- `layouts/partials/menu.html`, it fixes:
  ```js
  ERROR deprecated: .Site.IsMultiLingual was deprecated in Hugo v0.124.0 and will be removed in Hugo 0.143.0. Use hugo.IsMultilingual instead.
  ```

The fixes for those issues were backported from the Hugo Relearn v7.x.x theme.
When updating to Hugo Relearn 7.x.x, please remove them (if possible).

#### Upgrading to the Hugo Relearn 7.x.x theme versions

The partials in `layouts/partials` contain code for rendering the XenAPI releases
and class reference:

These custom partials need updates to support the breaking changes of Hugo Relearn
7.0.0. Otherwise, the Relearn theme menu sidebar on those pages would be missing.
These are the pages to verify for correct menu rendering when updating to 7.x.x:

- XenAPI Reference: <https://xapi-project.github.io/new-docs/xen-api/classes>
- XenAPI Releases: <https://xapi-project.github.io/new-docs/xen-api/releases>

Hint: For upgrading the Hugo Relearn theme, you can use:

```bash
cd doc; hugo mod get -u github.com/McShelby/hugo-theme-relearn@6.4.0
```

#### Summary

Hugo Relearn >= 5.23 and Relearn 6.x.x work now, 7.x.x is work in progress.

#### References

- Changes with Relearn 6.x:
  <https://mcshelby.github.io/hugo-theme-relearn/introduction/releasenotes/6/#6-0-0>
- Breaking changes with Relearn 7.x (to be supported):
  <https://mcshelby.github.io/hugo-theme-relearn/introduction/releasenotes/7/#7-0-0>
