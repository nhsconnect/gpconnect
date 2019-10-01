<img src="images/logo.png" height=72>

# GP Connect Documents

This is the source repository for the GP Connect specification.

The current specification version is held in the master branch, and published to <a href="https://nhsconnect.github.io/gpconnect/">GitHub pages</a>.

Previous versions of the specification are held in release/* branches (and tagged), and published to the <a href="https://developer.nhs.uk/gp-connect-specification-versions/">NHS Developer Network</a>.

## Building the specification

To build the GP Connect specification locally

- Clone the repository: `git clone https://github.com/nhsconnect/gpconnect.git`
- Install [Ruby](https://www.ruby-lang.org/en/documentation/installation/#homebrew)
- Install Jekyll
  - Install [Jekyll](https://jekyllrb.com/docs/installation/) for OS X/Linux
  - Install [Jekyll](https://jekyllrb.com/docs/windows/) for Windows
- Navigate to your gpconnect directory and run: `bundle install`
- Now run Jekyll: `bundle exec jekyll serve`
- Browse website [Browser](http://localhost:4005): `http://localhost:4005`

### Troubleshooting

1) Fix warnings related to SSL certificate checking (by configuring the SSL_CERT_FILE env variable) by following instructions to [download and reference a cacert.pem file](https://gist.github.com/fnichol/867550).

2) Fix warnings related to the Jekyll GitHub Metadata plugin, by [configuring the JEKYLL_GITHUB_TOKEN environment variable](https://github.com/jekyll/github-metadata).
