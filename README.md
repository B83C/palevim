PaleVim
===============

[![amo release][amo_version]][amo_release]
[![github release][github_version]][github_release]

**This is a custom fork of VIMPERATOR**

> Try `:help` command after installing add-on for details.

Features (PaleVim)
---------------------

- Vim-like keybindings (`h`, `j`, `k`, `l`, `gg`, `G`, `0`, `$`, `ZZ`, etc.)
- Ex commands (`:quit`, `:open www.foo.com`, ...)
- Tab completion available for all commands with support for 'longest' matching
  when set in 'wildmode'
- Extensions! Yes, you can extend PaleVim's functionality with scripts just
  like you can extend Firefox with extensions
- Explore JavaScript objects with `:echo window` and even context-sensitive tab
  completion
- Hit-a-hint like navigation of links (start with `f` to follow a link)
- Advanced completion of bookmark and history URLs (searching also in title,
  not only URL)
- Vim-like statusline with a wget-like progress bar
- Minimal GUI (easily hide useless menubar and toolbar with `:set gui=`)
- Ability to `:source` JavaScript files, and to use a `~/.vimperatorrc` file
- Easy quick searches (`:open foo` will search for "foo" in google, `:open ebay
  terminator` will search for "terminator" on ebay) with support for Firefox
  keyword bookmarks and search engines
- Count supported for many commands (`3<C-o>` will go back 3 pages)
- Beep on errors
- Marks support (`ma` to set mark 'a' on a webpage, `'a` to go there)
- QuickMarks support (quickly go to previously marked web pages with
  `go{a-zA-Z0-9}`)
- `:map` and `:command` support (and `feedkeys()` for script writers)
- `:time` support for profiling
- Move the text cursor and select text with vim keys and a visual mode
- External editor support
- Macros to replay key strokes
- AutoCommands to execute action on certain events
- A comprehensive `:help`, explaining all commands, mappings and options
- Much more...

Installation (PaleVim)
-------------------------

> Note that PaleVim doesn't support multi-process aka
> [Electrolysis][wiki_e10s] (e10s), it's necessary to disable e10s to use the
> add-on.

- Download **signed** add-on from addons.mozilla.org (AMO) <sup>1</sup>

  1. Enter [Add-ons page][amo_release].
  2. Click `Continue to Download` button.
  3. Click `Add to Firefox` button.

- Download **unsigned** <sup>2</sup> add-on from github.com (Github)

  1. Enter [Releases page][github_release].
  2. Click `vimperator-3.N.N.xpi` link under Downloads topic.

- Build own version (and signing)
  See [Build own version](#build-own-version) topic.

> <sup>1</sup> If the version on [AMO][amo_release] is older than the [latest
> release][github_release], you can build your own version and use it until AMO
> release is updated.

> <sup>2</sup> Since version 48, installing add-on to Firefox has required
> signing. Unsigned add-on is for Unbranded Builds. See [mozilla
> wiki][wiki_signing].

Build own version
-----------------

### Unsigned (for Unbranded Builds)

See http://www.vimperator.org/developer_info.

### Signed (for Firefox 48+)

Instructions for building this can be found in
vimperator/private.properties.in. See also [MDN document][mdn_signing]
(developer.mozilla.org) for details about signing and distribution.

There are necessary four steps to use own version.

1. Prepare "AMO API key" and "jpm" if first time
2. Build unsigned add-on
3. Submit unsigned add-on to AMO
4. Install signed add-on to Firefox
5. Addition: Use Command-line interface (CLI) to build and submit

#### Prepare AMO API key and jpm

- [AMO API key][amo_api_key] (require Firefox Account)
- [jpm][jpm_repo] (require node.js):

  ```bash
  npm install -g jpm
  ```

#### Build unsigned add-on

Clone repository and create private.properties:

```bash
git clone https://github.com/vimperator/vimperator-labs.git
cd vimperator-labs/vimperator
cp private.properties.in private.properties
```

Then edit private.properties so that it looks something like:

```makefile
VERSION       := $(VERSION).$(shell date '+%Y%m%d%H%M%S')
UUID           = vimperator@<uniqueid> # e.g. vimperator@<yourdomain>
AMO_API_KEY    = <your API key> # AKA "Issuer"
AMO_API_SECRET = <your API secret>
UPDATE_URL     =
UPDATE_URL_XPI =
```

Then run:

```bash
make xpi
```

The unsigned XPI should appear in
`../downloads/vimperator-3.N.N.yyyymmddhhmmss.xpi`.

#### Install signed add-on to Firefox

Install it via the link in your AMO developer account (find your PaleVim's
`Manage Status & Versions`). The new UUID makes it a new add-on, so don't
forget to disable the old version.

#### Use CLI to build and submit

After once you signed the add-on, you are able to update the add-on using CLI.

```bash
cd vimperator-labs/vimperator
make sign
```

