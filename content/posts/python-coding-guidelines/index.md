---
title: "Python Coding Guidelines"
date: 2021-01-05T23:06:55+08:00
draft: true
ShowToc: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true  
categories: ["product"]

cover:
    image: "images/test.png" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: true # when using page bundles set this to true
    hidden: false # only hide on current single page
---

This document gives coding conventions for maintainable python codebases.

Python is a great language, but without following some fairly strict guidelines, it can quickly become a big ball of mud, due to the flexibility of the language.

<!--more-->

Tooling
Python Version
All projects should use Python 3.8. Having a single python version for all projects provides benefits in terms of maintainability.

To easily run several python interpreters on your machine, install PyEnv.


brew install pyenv     # installs pyenv
pyenv init             # loads "$(pyenv init -)" in ~/.bashrc
pyenv install 3.8.2    # installs python 3.8.2
pyenv global 3.8.2     # makes python 3.8.2 your default python
python --version       # should return `Python 3.8.2`
Exceptions:
If we’re planning on a project that specifically targets a cloud platform (lambda, cloud funtions, etc.) that does not support Python 3.8, we can make an exception.

Upgrading:
We’ll consider upgrading to python 3.9 when it’s released. If the upgrade does not break our code base, we’ll upgrade all projects.

Project organization
Though it’s not strictly speaking related to code style or code quality, having standard python packaging practices is essential to make our code easily accessible to new team members is to have a consistent and easy to use approach to organizing python code.

All projects should use Poetry for dependencies management. Poetry combines in a single tool:

Creating and using a virtual environment

Managing the dependencies of the project, including pinning version numbers

Easily splits dev & prod libraries

Single source of truth for project version

CLI
All CLI should use click. Clicks make it easy to create a nice CLI with a user-friendly help system and avoid fighting with the lower level libraries (such as argparse).

Style Guide
All guidelines in this document are in addition to those defined in Python's PEP 8 (on code style) and PEP 257 (on docstrings) guidelines.

Some of the style guides are mandatory, while others are just guidelines. The application of the guidelines are at the discretion of the coder and the PR reviewers, with final decision coming to the reviewers.

SQL Formatting [Mandatory]
Usage of a SQL formatter such as EverSQL - else SQL can get very hard to read. Again the goal is to have a consistent way of writing SQL.

Hopefully we later find a way to bring this in our CI pipeline.

Typing Hints [Mandatory]
Typing hints are mandatory for all code, and should be checked with mypy (http://mypy-lang.org), a static code analyser. Typing hints make python code much easier to read and maintain as the reader can know the expected type of each reference. It also makes our IDEs more effective, as autocompletion can use the typing hints to be smarter.

 

Example typing hints:


from typing import Optional, Dict

def foo(vara: int, varb: str, varc: bool = False) -> Optional[Dict[str, int]]
  """ The variable names are non descriptive on purpose, to demonstrate
    more clearly the benefit of typing hints in understanding what code 
    is expected to do.
  """
  if varc:
    return {varb: vara}
  return None

It’s important to remember that typing hints are just hints, they are NOT checked at run time, and have no impact on the way code is executed by the python interpreter.

Project documentation [Mandatory]
Each project should have project documentation (readme.md) which should at least explains the goal of the project, and explain how to run it (external dependencies should be mentioned)

More is always better, but it’s ok to start with barebones project documentation, as long as there a list of steps to follow to execute the code, and a one-liner on what’s it’s expected to do.

As the project grows in importance, there will be time to make the documentation fancier.

Avoiding the plain dictionary anti-pattern [Guideline]

A common python anti-pattern is to pass around unvalidated dictionaries. This pattern creates code that is hard to reason about since the reader can not know what the dict is made of. We don’t know what is the type of the keys and the values, and some of the values could be lists or dicts. 

An alternative to this anti-pattern is to use classes to load the dict. In this way, we document which keys we expect in the dict, and what is the type of values. This approach is effective when the structure of the dict is predictable. The ideal tools for this approach right now are dataclasses,  attrs and Pydantic.

To avoid an explosion of different data validation libraries (there’s so many of them in python) in our codebases, data validation libraries beyond those mentioned in the paragraph above should be avoided.

Of course, not all dicts need to be loaded in a defined data structure - some dicts are too short-lived, or too unpredictable to fit that solution. 

Here’s a simple example:


import attr

@attr.s(auto_attribs=True)
class ConnectionString:
  host: str
  user: str
  db_name: str
  password: str
  port: int
  engine: str
  
  @classmethod
  def load_fromdict(cls, data: dict) -> "ConnectionString":
    return cls(**data)
  
  @property
  def dsn(self):
    return f"{self.engine}://{self.user}:{self.password}@{self.host}:{self.port}/{self.db_name}"

  
data = {"host": "localhost", "port": 5432, "db_name": "db", "user": "postgres", "password": "password", "engine": "postgres"}    
conn = ConnectionString.load_fromdict(data=data)
print(conn.dsn)
  
## output: postgres://postgres:password@localhost:5432/db



Doc Strings [Guideline]

Typing hints remove also many of the issues with code documentation, namely documentation drift (ie: docstrings not matching the function signature). 

With typing hints being mandatory, we can make doc strings optional - many functions are simple enough to not need them. Complex functions or classes benefit from having docstrings.

Line Length [Guideline]

Too short of lines discourage descriptive variable names where they otherwise make sense.

Too long of lines reduce overall readability and make it hard to compare 2 files side by side.

We use the classic 79 characters per line as it’s recommended standard by PEP8 and avoids spending time discussing this


Descriptive Variable Names [Mandatory/Guidelines]

Naming things is hard.  We don’t have many guidelines on variable naming, some of them being mandatory as they are objective, while others are juste guidelines since they are subjective.

Mandatory

No one character variable names.

Except for x, y, and z as coordinates.

It's not okay to override built-in functions.

Even for `id`. Use `idx` instead.

Guidelines

Avoid Acronyms, Abbreviations, or any other short forms - unless they are almost universally understood.

Don’t go crazy and use extremely long variable names either.


Automatic Code Cleaners

The goal of automated code cleaners is to ensure the coding style is respected throughout our projects, without spending too much time on it. It’s all about minimizing friction.

All code submitted to our projects should run through the following tools:

Black  - Automatically reformats code to respects most of the guidelines.

isort - Automatic sorting of imports

Flake8 - Catches what black can’t correct automatically

mypy - Checks that typing hints are everywhere [optional, complex projects only]

The easiest way to set these up is to use pre-commit hooks,  which can be set to run these tools automatically before each commit - and will prevent commits until all detected coding style issues have been solved.

Pre-commit hooks are described in a .yml file, commited to the project, and installed with a single command.

Example:

Filename: .pre-commit-config.yaml


repos:
  - repo: https://github.com/asottile/seed-isort-config
    rev: v2.1.1
    hooks:
      - id: seed-isort-config
        args: [--application-directories, "./app:./"]
  - repo: https://github.com/pre-commit/mirrors-isort
    rev: v4.3.21
    hooks:
      - id: isort
        additional_dependencies: ["toml"]
  - repo: https://github.com/ambv/black
    rev: stable
    hooks:
      - id: black
  - repo: https://gitlab.com/pycqa/flake8
    rev: 3.7.9
    hooks:
      - id: flake8
        additional_dependencies: [
          "git+https://github.com/PyCQA/pyflakes#egg=pyflakes",
          "git+https://gitlab.com/PyCQA/pycodestyle#egg=pycodestyle",
        ]
default_language_version:
  python: python3.8

How to setup:

Assuming poetry is set up:


poetry add pre-commit -D       # -D to make it a dev dependency
poetry run pre-commit install  #`poetry run` runs a command in the virt env
That’s it!

All future commits will trigger the code analyzers