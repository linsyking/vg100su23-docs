Environment Setup
=================

.. admonition:: Goal

    - Install ``Git``
    - Install ``Python`` (>=3.7, needs ``pip``)
    - Install ``pnpm`` (or ``npm``, if you prefer)
    - Install ``Elm`` (0.19.1)
    - Setup ``Gitea`` and ``Mattermost`` account
    - Basic knowledge of ``Git``

Git
-----

`Windows Git Installer <https://registry.npmmirror.com/-/binary/git-for-windows/v2.40.1.windows.1/Git-2.40.1-64-bit.exe>`_.

If you are the first time using Git, please also set your account email and name.


Git commit
^^^^^^^^^^^

There are several rules you have to follow for commits.

- Atomic commits
  
  Atomic commits also allow bug fixes to be easily reviewed if only a single bug fix is committed at a time.
  Normally, a commit should only contain one single feature or bug fix.
  A commit with more than 300 lines of code (more than one feature/bug fix) is not expected.

- Commit message should be in English and follows a specific style
- Commit message should be concise, meaningful and clear

Styles
********

We recommend you to follow the `Conventional Commits <https://www.conventionalcommits.org/en/v1.0.0/>`_ style.

Although there are some CLI tools (like `Commitizen <https://commitizen-tools.github.io/commitizen/>`_) helping you to commit, I think writing commit messages by hand is the fastest and most efficient.

Automatic Changelog (Optional)
*******************************

You have to write a ``Changelog.md`` for your project. It can be generated automatically if you use the conventional commit style.

First, in your project (which has ``package.json``), install the dev dependency:

.. code-block:: bash

    pnpm i -D standard-version

Then add these entries to the ``scripts`` entry of your ``package.json``.

.. code-block::

    "release": "standard-version",
    "publish": "git push --follow-tags origin dev",

(Change the corresponding branch if ``dev`` is not the desired branch to push)

This will bump the version automatically and add a git tag. You have to manually check if the version is desired.

Husky (Optional, Recommended)
*******************************

`Husky <https://typicode.github.io/husky/#/>`_ is a git hook tool, it can prevent you from committing code that cannot compile/has wrong commit messages/not following team code format standard/cannot pass the tests/ and many other problems.

Follow `the official guide to install <https://typicode.github.io/husky/#/?id=automatic-recommended>`_.

.. code-block:: bash

    pnpm dlx husky-init && pnpm install # pnpm

If you are using a project which has ``husky`` enables, you need to run the following command to register the git hooks:

.. code-block:: bash

    pnpm run prepare

After installation, you can add some files to ``.husky``.

The following example will check whether the commit messages follow the conventional commits style.

You have to install the ``commitlint`` first:

.. code-block:: bash

    pnpm i -g @commitlint/cli
    pnpm i -D  @commitlint/config-conventional
    echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js

.. code-block:: bash
    :linenos:
    :caption: .husky/commit-msg

    #!/usr/bin/env sh
    . "$(dirname -- "$0")/_/husky.sh"
    commitlint --edit $1

The following example will check whether the code can make and whether the code is formatted.

.. code-block:: bash
    :linenos:
    :caption: .husky/pre-commit

    #!/usr/bin/env sh
    . "$(dirname -- "$0")/_/husky.sh"

    echo -e "\033[32mBuilding the project...\033[0m"

    make

    echo -e "\033[32mChecking the code...\033[0m"

    if elm-format src --validate; then
        echo -e "\033[32mPassed\033[0m"
    else
        echo -e "\033[31mFailed, please run \"make format\" before you commit!\033[0m"
        exit 255
    fi


Git branch
------------

See `Learn Git Branching <https://learngitbranching.js.org/>`_.

Git LFS
--------

Git LFS is a tool to upload large binary files to git repository.

Go to the `official website <https://git-lfs.com/>`_ to install Git LFS.

Note that you have to run once the following command:

.. code-block:: bash

    git lfs install

Nodejs
-------

Official website: `nodejs.org <https://nodejs.org/en/>`_.

Node.js is a back-end JavaScript runtime environment, runs on the V8 JavaScript Engine, and executes JavaScript code outside a web browser.

You can use a node version manager to install and manage different versions of nodejs.

You can use `nvm <https://github.com/nvm-sh/nvm>`_, `fnm <https://github.com/Schniz/fnm>`_ (which I am using).

Pnpm
-----

Pnpm is a fast, disk space efficient package manager for nodejs.

See `the official Pnpm website <https://pnpm.io/zh/installation>`_.

Elm
-----

See `the official Elm website <https://guide.elm-lang.org/install/elm.html>`_.

You can install elm by using ``pnpm``.

.. code-block:: sh

    pnpm i -g elm elm-format

Python
--------

Install any python version >= 3.7, and make sure ``pip`` is installed.

.. note::

    If you are using Windows, please make sure you have added python to your ``PATH``.

.. warning::

    If you have installed conda, please make sure that ``pip`` in your conda environment is not used.

Elm Playground
---------------

Use ``elm repl`` to play with Elm.
