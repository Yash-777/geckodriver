# geckodriver [![Build Status](https://travis-ci.org/mozilla/geckodriver.svg?branch=master)](https://travis-ci.org/mozilla/geckodriver)

Proxy for using W3C WebDriver-compatible clients
to interact with Gecko-based browsers.

This program provides the HTTP API described by
the [WebDriver protocol](http://w3c.github.io/webdriver/webdriver-spec.html#protocol)
to communicate with Gecko browsers, such as Firefox.
It translates calls into
the [Marionette](https://developer.mozilla.org/en-US/docs/Mozilla/QA/Marionette)
automation protocol
by acting as a proxy between the local- and remote ends.

You can consult the [change log](https://github.com/mozilla/geckodriver/blob/master/CHANGES.md)
for a record of all notable changes to the program.

## Supported Firefoxen

Marionette and geckodriver are not yet feature complete.
This means it does not yet offer full conformance
with the [WebDriver standard](https://w3c.github.io/webdriver/webdriver-spec.html)
or complete compatibility with [Selenium](http://www.seleniumhq.org/).

You can track the [implementation status](https://developer.mozilla.org/en-US/docs/Mozilla/QA/Marionette/WebDriver/status)
of the latest Firefox Nightly on MDN.
We also keep track of known
[Marionette](https://github.com/mozilla/geckodriver/issues?q=is%3Aissue+is%3Aopen+label%3Amarionette),
[Selenium](https://github.com/mozilla/geckodriver/issues?q=is%3Aissue+is%3Aopen+label%3Aselenium),
and [specification](https://github.com/mozilla/geckodriver/issues?q=is%3Aissue+is%3Aopen+label%3Aspec)
problems in our issue tracker.

Marionette support is best in Firefox 48 and onwards,
although the more recent the Firefox version,
the more bug fixes and features.
**Firefox 47 is explicitly not supported.**

## Firefox capabilities

Capabilities are options that you can use
to customise and configure WebDriver sessions.
geckodriver supports a capability named `firefoxOptions`
which takes Firefox-specific configuration options.
It must be a dictionary and may contain any of the following fields:

<table>
 <caption>Object
 <tr><th>Key <th colspan=2>Value <th>Description</tr>

 <tr>
  <td><code>binary</code>
  <td colspan=2>String
  <td>Absolute path to the Firefox binary,
   e.g. <code>/usr/bin/firefox</code>
   or <code>/Applications/Firefox.app/Contents/MacOS/firefox</code>,
   to select which browser to use.
   If left undefined geckodriver will
   use the <code>--binary</code> argument
   or attempt to deduce the default location of Firefox
   on the current system.
 </tr>

 <tr>
  <td rowspan=2><code>args</code>
  <td colspan=2>Array</td>
  <td rowspan=2>Command line arguments to pass to the Firefox binary.
   These must include the leading <code>--</code> where required
   e.g. <code>["--devtools"]</code>.
 </tr>
 <tr>
  <td>String</td
 </tr>

 <tr>
  <td><code>profile</code>
  <td colspan=2>String
  <td>Base64-encoded zip of a profile directory
   to use as the profile for the Firefox instance.
   This may be used to e.g. install extensions or custom certificates.
   If left undefined, a new temporary profile will be created.
 </tr>

 <tr>
  <td rowspan=2><code>log</code>
 </tr>
 <tr>
  <td><code>level</code>
  <td>String
  <td>Set the level of verbosity in Gecko.
   Available levels are <code>trace</code>,
   <code>debug</code>, <code>config</code>,
   <code>info</code>, <code>warn</code>,
   <code>error</code>, and <code>fatal</code>.
   If left undefined, the default is
   for optimised Firefox builds to use <code>info</code>
   and non-optimised builds to use <code>debug</code>.
 </tr>
 <tr>
  <td><code>file</code>
  <td>String
  <td>Full path to log file.
   Just included here for visualisation.
   Will be removed in the patch.
 </tr>

 <tr>
  <td><code>prefs</code>
  <td>
   <table>
    <tr><th>Key <th>Value</tr>
    <tr><td><var>Preference</var> <td>New value</tr>
    <tr><td colspan=2>…</tr>
   </table>
  <td>A full list of possible preferences
   along with the expected types
   can be seen in <a href="about:config">about:config</a>.
 </tr>
</table>

## Building

geckodriver is written in [Rust](https://www.rust-lang.org/)
and you need the [Rust toolchain](https://rustup.rs/) to compile it.

To build the project for release,
ensure you do a compilation with optimisations:

    % cargo build --release

Or if you want a non-optimised binary for debugging:

    % cargo build

## Usage

Usage steps are [documented on MDN](https://developer.mozilla.org/en-US/docs/Mozilla/QA/Marionette/WebDriver),
but the gist of it is this:

    % geckodriver -b /usr/bin/firefox

Or if you’re on Mac:

    % geckodriver -b /Applications/FirefoxNightly.app/Contents/MacOS/firefox-bin
