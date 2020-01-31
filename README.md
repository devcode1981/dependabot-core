<p align="center">
  <img src="https://s3.eu-west-2.amazonaws.com/dependabot-images/logo-with-name-horizontal.svg" alt="Dependabot" width="300">
</p>

# Dependabot Core [![Dependabot Status][dependabot-status]][dependabot]

[![Greenkeeper badge](https://badges.greenkeeper.io/devcode1981/dependabot-core.svg)](https://greenkeeper.io/)

Dependabot Core is the heart of [Dependabot][dependabot]. It handles the logic
for updating dependencies on GitHub (including GitHub Enterprise) and GitLab. We
plan to add support for Bitbucket in future, too.

If you want to host your own automated dependency update bot then this repo
should give you the tools you need. A reference implementation is available
[here][dependabot-script].

## What's in this repo?

Dependabot Core is a collection of helper classes for automating dependency
updating in Ruby, JavaScript, Python, PHP, Elixir, Elm, Go, Rust, Java and
.NET. It can also update git submodules, Docker files and Terraform files.
Highlights include:

- Logic to check for the latest version of a dependency *that's resolvable given
  a project's other dependencies*. That means tapping into the package manager's
  dependency resolution logic
- Logic to generate updated manifest and lockfiles for a new dependency version
- Logic to find changelogs, release notes, and commits for a dependency update

## Setup

To run all of Dependabot Core, you'll need Ruby, Python, PHP, Elixir, Node, Go,
Elm and Rust installed. However, if you just wish to run it for a single
language you can get away with just having that language and Ruby.

The main library is written in Ruby, while JavaScript, Python, PHP, Elm,
Elixir, Go and Rust are required for dealing with updates for their respective
languages.

Before running Dependabot Core, install dependencies for the core library and
the helpers:

1. `bundle install`
2. `cd helpers/yarn && yarn install && cd -`
3. `cd helpers/npm && yarn install && cd -`
4. `cd helpers/php && composer install && cd -`
5. `cd helpers/python && pyenv exec pip install -r requirements.txt && cd -`
6. `cd helpers/elixir && mix deps.get && cd -`

## Architecture

Dependabot Core has helper classes for seven concerns. Where relevant, each
concern will have a language-specific class.

| Service                          | Description                                                                                   |
|----------------------------------|-----------------------------------------------------------------------------------------------|
| `Dependabot::FileFetchers`       | Fetches the relevant dependency files for a project (e.g., the `Gemfile` and `Gemfile.lock`). See the [file fetchers](https://github.com/dependabot/dependabot-core/tree/master/lib/dependabot/file_fetchers) for more details. |
| `Dependabot::FileParsers`        | Parses a dependency file and extracts a list of dependencies for a project. See the [file parsers](https://github.com/dependabot/dependabot-core/tree/master/lib/dependabot/file_parsers) for more details. |
| `Dependabot::UpdateCheckers`     | Checks whether a given dependency is up-to-date. See the [update checkers](https://github.com/dependabot/dependabot-core/tree/master/lib/dependabot/update_checkers) for more details. |
| `Dependabot::FileUpdaters`       | Updates a dependency file to use the latest version of a given dependency. See the [file updaters](https://github.com/dependabot/dependabot-core/tree/master/lib/dependabot/file_updaters) for more details. |
| `Dependabot::MetadataFinders`    | Looks up metadata about a dependency, such as its GitHub URL. See the [metadata finders](https://github.com/dependabot/dependabot-core/tree/master/lib/dependabot/metadata_finders) for more details. |
| `Dependabot::PullRequestCreator` | Creates a Pull Request to the original repo with the updated dependency file.                 |
| `Dependabot::PullRequestUpdater` | Updates an existing Pull Request with new dependency files (e.g., to resolve conflicts).      |

## Why is this public?

As the name suggests, Dependabot Core is the core of Dependabot (the rest of the
app is pretty much just a UI and database). If we were paranoid about someone
stealing our business then we'd be keeping it under lock and key.

Dependabot Core is public because we're more interested in it having an
impact than we are in making a buck from it. We'd love you to use
[Dependabot][dependabot], so that we can continue to develop it, but if you want
to build and host your own version then this library should make doing so a
*lot* easier.

If you use Dependabot Core then we'd love to hear what you build!

## License

We use the License Zero Prosperity Public License, which essentially enshrines
the following:
- If you would like to use Dependabot Core for non-commerical purposes, such as
  to host a bot at your workplace, then we give you full permission to do so. In
  fact, we'd love you to, and will help and support you however we can.
- If you would like to add Dependabot's functionality to your for-profit
  company's offering then we DO NOT give you permission to use Dependabot Core
  to do so. Please contact us directly to discuss a partnership or licensing
  arrangement.

If you make a significant contribution to Dependabot Core then you will be asked
to transfer the IP of that contribution to Dependabot Ltd so that it can be
licensed in the same way as the above.

## History

Dependabot and Dependabot Core started life as [Bump][bump] and
[Bump Core][bump-core], back when Harry and Grey were working at
[GoCardless][gocardless]. We remain grateful for the help and support of
GoCardless in helping make Dependabot possible - if you need to collect
recurring payments from Europe, check them out.

[dependabot]: https://dependabot.com
[dependabot-status]: https://api.dependabot.com/badges/status?host=github&identifier=93163073
[dependabot-script]: https://github.com/dependabot/dependabot-script
[bump]: https://github.com/gocardless/bump
[bump-core]: https://github.com/gocardless/bump-core
[gocardless]: https://gocardless.com
