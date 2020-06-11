# Pardot API Docs

_**This repository has been deprecated**_

## Prerequisites

* [Git](http://git-scm.com/)
* [Python](https://www.python.org/)
* [pip](https://pip.pypa.io/en/latest/)

## Installation
This site uses MkDocs version 1.0.4. To install:
* `pip install mkdocs-bootstrap==0.1.1 mkdocs-bootswatch==0.1.0 mkdocs==1.0.4`
* `git clone git@github.com:pardot/api-docs.git`
* `cd api-docs`
* `mkdocs serve`
* `open http://127.0.0.1:8000/`

See the [mkdocs](http://www.mkdocs.org/#getting-started) website for more information.

## Deploying

If you don't know what you're doing, ask someone to help you out.

* `git checkout master`
* `mkdocs gh-deploy --clean`
* `git reset --hard && git clean -fd`

See the [mkdocs](http://www.mkdocs.org/user-guide/deploying-your-docs/) website for more information.
