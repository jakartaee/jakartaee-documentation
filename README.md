# jakartaee-documentation

This is the repo for building the Jakarta EE Documentation site (from different repos); currently this consists of the Jakarta EE Tutorial.

- Repo for the tutorial content: [https://github.com/jakartaee/jakartaee-tutorial/](https://github.com/jakartaee/jakartaee-tutorial/)
- Repo for the documentation UI: [https://github.com/jakartaee/jakartaee-documentation-ui/](https://github.com/jakartaee/jakartaee-documentation-ui/)

## Prerequisites

- [JDK](https://jdk.java.net/)
- [Maven](https://maven.apache.org/)
- [Ruby](https://rvm.io/)

## Setup

JDK and Maven speak for themselves.

Ruby, if `ruby -v` returns something like `Command 'ruby' not found` then [read the instructions](https://rvm.io/rvm/install) to install "RVM stable".
Summarized:

```bash
gpg --keyserver keyserver.ubuntu.com --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
curl -sSL https://get.rvm.io | bash -s stable --ruby
source ~/.rvm/scripts/rvm
```

And finally install the [`asciidoctor-pdf`](https://rubygems.org/gems/asciidoctor-pdf) gem:

```bash
gem install asciidoctor-pdf
```

## Building

To build, run:

```bash
mvn clean package
```

The output will be in `target/generated-docs`.
To view, just open [`target/generated-docs/jakartaee-tutorial/current/index.html`](target/generated-docs/jakartaee-tutorial/current/index.html) in a browser.

```bash
browse target/generated-docs/jakartaee-tutorial/current/index.html
```

If you face a build failure with the following log entry as the last one before the failure, basically saying "Command not found: asciidoctor-pdf":

> [INFO] {"level":"fatal","time":1684333903235,"name":"antora","hint":"Add the --stacktrace option to see the cause of the error.","msg":"Command not found: asciidoctor-pdf"}

Then you need to run beforehand:

```bash
source ~/.rvm/scripts/rvm
```

Or to make sure this is executed every time you open a new terminal.

### Author Mode

Antora supports an Author Mode that lets you work with local branches and your local worktree.
This requires that you keep a local copy of `antora-playbook.yml` as `local-antora-playbook.yml`.
Read [Use Author Mode :: Antora Docs](https://docs.antora.org/antora/latest/playbook/author-mode/) for details. 

Once you've created the `local-antora-playbook.yml` file, you can use the `author-mode` Maven profile:

```bash
mvn compile -Pauthor-mode
```

The output will still be in the same location, but it'll be generated from your local clone of the repos instead of the remote.

```bash
browse target/generated-docs/jakartaee-tutorial/current/index.html
```

## Deploying

This site is currently deployed via GitHub Pages via GitHub Actions.
For details, see the [workflow file](.github/workflows/build-and-deploy.yml).

The current URL is [https://jakartaee.github.io/jakartaee-documentation/](https://jakartaee.github.io/jakartaee-documentation/).
