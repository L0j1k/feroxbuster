<h1 align="center">
  <br>
  <a href="https://github.com/epi052/feroxbuster"><img src="img/logo/default-cropped.png" alt="feroxbuster"></a>
  <br>
</h1>

<h4 align="center">A simple, fast, recursive content discovery tool written in Rust</h4>

<p align="center">
  <a href="https://github.com/epi052/feroxbuster/actions?query=workflow%3A%22CI+Pipeline%22">
    <img src="https://img.shields.io/github/workflow/status/epi052/feroxbuster/CI%20Pipeline/main?logo=github">
  </a>

  <a href="https://github.com/epi052/feroxbuster/releases">
    <img src="https://img.shields.io/github/downloads/epi052/feroxbuster/total?label=downloads&logo=github&color=inactive" alt="github downloads">
  </a>

  <a href="https://github.com/epi052/feroxbuster/commits/master">
    <img src="https://img.shields.io/github/last-commit/epi052/feroxbuster?logo=github">
  </a>

  <a href="https://crates.io/crates/feroxbuster">
    <img src="https://img.shields.io/crates/v/feroxbuster?color=blue&label=version&logo=rust">
  </a>

  <a href="https://crates.io/crates/feroxbuster">
    <img src="https://img.shields.io/crates/d/feroxbuster?label=downloads&logo=rust&color=inactive">
  </a>

  <a href="https://codecov.io/gh/epi052/feroxbuster">
    <img src="https://codecov.io/gh/epi052/feroxbuster/branch/master/graph/badge.svg" />
  </a>
</p>

![demo](img/demo.gif)

<p align="center">
  🦀
  <a href="https://github.com/epi052/feroxbuster/releases">Releases</a> ✨
  <a href="https://epi052.github.io/feroxbuster-docs/docs/examples/">Example Usage</a> ✨
  <a href="https://github.com/epi052/feroxbuster/blob/main/CONTRIBUTING.md">Contributing</a> ✨
  <a href="https://epi052.github.io/feroxbuster-docs/docs/">Documentation</a>
  🦀
</p>

---

<h1><p align="center">✨🎉👉 <a href="https://epi052.github.io/feroxbuster-docs/docs/">NEW DOCUMENTATION SITE</a> 👈🎉✨</p></h1>


## 🚀 Documentation has **moved** 🚀  

Instead of having a 1300 line `README.md` (sorry...), feroxbuster's documentation has moved to GitHub Pages. The move to hosting documentation on Pages should make it a LOT easier to find the information you're looking for, whatever that may be. Please check it out for anything you need beyond a quick-start. The new documentation can be found [here](https://epi052.github.io/feroxbuster-docs/docs/). 

## 😕 What the heck is a ferox anyway?

Ferox is short for Ferric Oxide. Ferric Oxide, simply put, is rust. The name rustbuster was taken, so I decided on a
variation. 🤷

## 🤔 What's it do tho?

`feroxbuster` is a tool designed to perform [Forced Browsing](https://owasp.org/www-community/attacks/Forced_browsing).

Forced browsing is an attack where the aim is to enumerate and access resources that are not referenced by the web
application, but are still accessible by an attacker.

`feroxbuster` uses brute force combined with a wordlist to search for unlinked content in target directories. These
resources may store sensitive information about web applications and operational systems, such as source code,
credentials, internal network addressing, etc...

This attack is also known as Predictable Resource Location, File Enumeration, Directory Enumeration, and Resource
Enumeration.

## ⏳ Quick Start

This section will cover the minimum amount of information to get up and running with feroxbuster. Please refer the the [documentation](https://epi052.github.io/feroxbuster-docs/docs/), as it's much more comprehensive.

### 💿 Installation

There are quite a few other [installation methods](https://epi052.github.io/feroxbuster-docs/docs/installation/), but these snippets should cover the majority of users. 

#### Kali 

If you're using kali, this is the preferred install method. Installing from the repos adds a [**ferox-config.toml**](https://epi052.github.io/feroxbuster-docs/docs/configuration/ferox-config-toml/) in `/etc/feroxbuster/`, adds command completion for bash, fish, and zsh, includes a man page entry, and installs `feroxbuster` itself. 

```
sudo apt update && sudo apt install -y feroxbuster
```

#### Linux (32 and 64-bit) & MacOS

```
curl -sL https://raw.githubusercontent.com/epi052/feroxbuster/master/install-nix.sh | bash
```


#### Windows x86_64

```
Invoke-WebRequest https://github.com/epi052/feroxbuster/releases/latest/download/x86_64-windows-feroxbuster.exe.zip -OutFile feroxbuster.zip
Expand-Archive .\feroxbuster.zip
.\feroxbuster\feroxbuster.exe -V
```

#### All others 

Please refer the the [documentation](https://epi052.github.io/feroxbuster-docs/docs/).

## 🧰 Example Usage

Here are a few brief examples to get you started.  Please note, feroxbuster can do a **lot more** than what's listed below.  As a result, there are **many more** examples, with **demonstration gifs** that highlight specific features, in the [documentation](https://epi052.github.io/feroxbuster-docs/docs/).

### Multiple Values

Options that take multiple values are very flexible. Consider the following ways of specifying extensions:

```
./feroxbuster -u http://127.1 -x pdf -x js,html -x php txt json,docx
```

The command above adds .pdf, .js, .html, .php, .txt, .json, and .docx to each url

All of the methods above (multiple flags, space separated, comma separated, etc...) are valid and interchangeable. The
same goes for urls, headers, status codes, queries, and size filters.

### Include Headers

```
./feroxbuster -u http://127.1 -H Accept:application/json "Authorization: Bearer {token}"
```

### IPv6, non-recursive scan with INFO-level logging enabled

```
./feroxbuster -u http://[::1] --no-recursion -vv
```

### Read urls from STDIN; pipe only resulting urls out to another tool

```
cat targets | ./feroxbuster --stdin --silent -s 200 301 302 --redirects -x js | fff -s 200 -o js-files
```

### Proxy traffic through Burp

```
./feroxbuster -u http://127.1 --insecure --proxy http://127.0.0.1:8080
```

### Proxy traffic through a SOCKS proxy (including DNS lookups)

```
./feroxbuster -u http://127.1 --proxy socks5h://127.0.0.1:9050
```

### Pass auth token via query parameter

```
./feroxbuster -u http://127.1 --query token=0123456789ABCDEF
```

## 🚀 Documentation has **moved** 🚀  

For realsies, there used to be over 1300 lines in this README, but it's all been moved to the [new documentation site](https://epi052.github.io/feroxbuster-docs/docs/). Go check it out! 

<h1><p align="center">✨🎉👉 <a href="https://epi052.github.io/feroxbuster-docs/docs/">DOCUMENTATION</a> 👈🎉✨</p></h1>
