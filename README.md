# Pardot API Docs

## Prerequisites

* [Git](http://git-scm.com/)
* [Python](https://www.python.org/)
* [pip](https://pip.pypa.io/en/latest/)

## Installation

* `pip install mkdocs`
* `git clone https://github.com/Pardot/api-docs.git`
* `cd api-docs`
* `mkdocs serve`
* `open http://127.0.0.1:8000/`

Make sure your MkDocs is up-to-date. Current Version: 0.14.0. To upgrade:
* `pip install -U mkdocs`

See the [mkdocs](http://www.mkdocs.org/#getting-started) website for more information.

## Deploying

If you don't know what you're doing, ask someone to help you out.

* `git checkout master`
* `mkdocs gh-deploy --clean`
* `git reset --hard && git clean -fd`

See the [mkdocs](http://www.mkdocs.org/user-guide/deploying-your-docs/) website for more information.
