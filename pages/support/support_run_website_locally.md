---
title: Run website locally
keywords: support, website, jekyll
tags: [support]
toc: false
sidebar: overview_sidebar
permalink: support_run_website_locally.html
summary: "How to run the website locally on your own PC"
---

Please follow the following instructions to setting up GitHub Pages to run locally:

[setting-up-your-github-pages-site-locally-with-jekyll](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/)

In short...

Make sure you have Ruby 2.X.X installed.

```bash
ruby --version
```

Install bundler using gem.

```bash
gem install bundler 
```

Clone the [gpconnect](https://github.com/nhsconnect/gpconnect.git) Git repository.

```bash
git clone https://github.com/nhsconnect/gpconnect.git
```

Now change into the downloaded/cloned directory and run the 'bundle install' command to install Jekyll.

```bash
bundle install 
```

Run the 'jekyll serve' command to compile and serve the HTML content.

```bash
bundle exec jekyll serve 
```

By default, pages are served from http://localhost:4005/

You will likely hit two further problems:

1) Fix warnings related to SSL certificate checking (by configuring the SSL_CERT_FILE env variable)

I followed the following instructions to download and reference a cacert.pem file.

[cacert_file](https://gist.github.com/fnichol/867550)

2) Fix warnings related to the Jekyll GitHub Metadata plugin (by configuring the JEKYLL_GITHUB_TOKEN env variable)

[github-metadata](https://github.com/jekyll/github-metadata)

