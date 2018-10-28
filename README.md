
Strigo's REST API Docs
======================

The API Reference is available at https://docs.strigo.io/api).

[![CircleCI](https://circleci.com/gh/strigo/rest-docs/tree/master.svg?style=shield)](https://circleci.com/gh/strigo/rest-docs/tree/master)

# Installing and running locally

1. Install the latest Hugo:

    * On CentOS:

        1. Install the copr plugin for yum: `sudo yum install yum-plugin-copr`
        1. Enable the Hugo repository: `sudo yum copr enable daftaupe/hugo`
        1. Install Hugo: `sudo yum install hugo`

    * On Ubuntu:

        * Install Hugo: `sudo apt-get install hugo`

    * On Windows:

        1. Install [chocolatey](https://chocolatey.org/install).
        1. Install Hugo: `choco install hugo -confirm`

    * On MacOS:

        1. Install [homebrew](https://brew.sh/)
        2. Install Hugo: `brew install hugo`

1. Verify that Hugo is installed: `hugo version`
1. Clone this repository.
1. Change directory to the `rest-docs` directory.
1. Start the hugo web server: `hugo server`
1. Go to: http://localhost:1313

# Contribution

PRs are always welcome :)
