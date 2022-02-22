# Strigo's REST API Docs

The API Reference is available at https://docs.strigo.io.

# Installing and running locally

1. Install the latest Hugo:

   - On CentOS:

     1. Install the copr plugin for yum: `sudo yum install yum-plugin-copr`
     1. Enable the Hugo repository: `sudo yum copr enable daftaupe/hugo`
     1. Install Hugo: `sudo yum install hugo`

   - On Ubuntu:

     - Install Hugo: `sudo apt-get install hugo`

   - On Windows:

     1. Install [chocolatey](https://chocolatey.org/install).
     1. Install Hugo: `choco install hugo -confirm`

   - On MacOS:

     1. Install [homebrew](https://brew.sh/)
     1. Install Hugo: `brew install hugo`

1. Verify that Hugo is installed: `hugo version`
1. Clone this repository.
1. Change directory to the `strigo-rest-docs` directory.
1. Start the hugo web server: `hugo server`
1. Go to: http://localhost:1313

# Publishing

We use Netlify to manage the docs' build process. Once a PR is merged to master, if everything went well, it will be available for publishing.

To publish a new version:

1. Go to https://github.com (preferably in incognito mode) and sign in as `strigops`
1. Go to https://app.netlify.com/sites/strigo-rest-docs/overview and sign in with GitHub
1. Click the relevant item under "Production deploys", which represents the commit you want to deploy.
1. Click the "Publish deploy" button.
1. Done! The docs should now be up-to-date.

# Contribution

PRs are always welcome :)
