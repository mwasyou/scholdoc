Scholdoc changelog
==================

All notable changes to Scholdoc will be documented in this file.

This log pertains to Scholdoc development **only**. Pandoc's changelog can be found in the `changelog-pandoc` file.

Scholdoc's version numbers reflect Scholdoc changes only, and does not necessarily correspond to Pandoc's version number. Scholdoc strives to track the latest official Pandoc release. Whenever new Pandoc commits are merged into Scholdoc, it will be noted in the changelog below.

Scholdoc follows semantic versioning with regards to its output schema.

## 0.1.3-alpha - 2014-10-15

**Note:** *This version largely consists of major cleanups under the hood. It bring the development of Scholdoc up-to-date with the latest Pandoc development version, and removed many unnecessary source files related to unused reader/writers.*

### Added
- The Pandoc-derived portion of Scholdoc is now up to date with Pandoc 1.13.1 (commit 8b60d430)
- The build-chain of Scholdoc have been cleaned-up and is now ready for production. Running `make deps && make install` under the source directory now fully builds using its own `scholdoc-types` and `scholdoc-texmath` packages.
- Updated documentation to reflect the Scholdoc project: README.md, CONTRIBUTING.md, BUGS, COPYRIGHT

### Changed
- Scholdoc now looks for custom template files under the `~/.scholdoc/` directory, instead of `~/.pandoc`
- The "--no-standalone" option no longer imply "_bodyOnly" writers. Instead "--no-standalone" now strictly stops all template usage.

## 0.1.2-alpha - 2014-09-09

### Added
- Allow rudimentary Docx output, although most Scholmd elements map to empty

### Changed
- The program name is changed from `scholpandoc` to `scholdoc` to more accurately reflect the limited input/output options compared to Pandoc.

#### HTML output
- Uses HTTPS instead of protocol-relative URLs for default polyfills in the template from CDNJS. This will make previewing local HTML files much easier.
    - Default MathJax CDN URL is also changed to the HTTPS protocol
- Added an additional variable `html-header-includes` for inclusion of HTML-specific header tags. This can be specified in YAML metadata blocks, and will be treated as an unformatted string.

#### LaTeX output
- Added `indentparagraphs` variable to template, so you can change between "no indent/line-height paragraph margins" and "indent/no paragraph margins"
- Added variables `natbib-options` and `biblatex-options` to specify loading options for these citation packages
- Added additional variables to the template for more flexibility in "injection" of custom LaTeX code without resorting to a separate template:
    - `latex-before-documentclass-includes`
    - `latex-before-packages-includes`
    - `latex-after-packages-includes`
    - `latex-header-includes`
    - `latex-after-body-includes`
    - `latex-after-document-includes`
- *All the above variable can be specified in YAML metadata blocks, and will be treated as unformatted strings (along with `geometry`)*

## 0.1.1-alpha - 2014-05-30

### Added
- Allow output of JSON-style native format

### Changed

#### LaTeX output
- No longer hard-codes the `htbp` placement of floats. This is now controlled in the template using the `Float` package.

### Fixed
- Fixed a bug where figures/floats display captions prefixes when it is not needed

## 0.1.0-alpha - 2014-04-22

### Changed

#### HTML output
- Conforms to ScholarlyMarkdown HTML5 Schema 0.1

### Fixed
- The `bibliography` metadata is now treated like a pure string and will not be formatted
- Display math and figure/floats now properly parses if delimiters have multiple trailing whitespaces
- Disabling standalone mode using `_bodyonly` suffix now works again
- Minor code cleanup using `hlint`, refactored various writer monads for floats

## 0.0.1-alpha - 2014-03-16

### Added
- Display math equations that uses the class `math_def` instead of `math` are now appended to a global variable called `$math-macros$`. In the updated templates this is placed in the header, and enables LaTeX declarations that only work in the header

### Changed
- ScholarlyPandoc now has the following arguments enabled by default: `-f markdown_scholarly --smart --parse-raw --standalone`. Renaming the executable to anything other than `scholpandoc` reverts this behavior

### Fixes
- Fixed a bug where templates files are not compiled into the binary, resulting in complaints about "can't find file ..."

## 0.0.0-alpha - 2014-03-14

Initial Release
