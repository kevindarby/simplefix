Running the Unit Tests
======================

In my development environment, I have three venvs: 2.7, 3.3 and 3.6.  I run
the tests in each of these environments before committing changes.

Once committed, TravisCI runs the tests in 2.7, 3.3, 3.4, 3.5 and 3.6.  It will
build pull-request branches also.  Travis will email your commit address the
results of its build.

To run tests from a local shell, I use:

.. code-block:: bash

   env PYTHONPATH=. python test/all.py

You should expect to see a DeprecationWarning about `append_time()`, but
otherwise all 90 tests passing (that number might increase).

To run just one test case, pass the class name as an additional parameter:

.. code-block:: bash

   env PYTHONPATH=. python test/all.py ParserTest

To run just a single test, pass the test case class and method name:

.. code-block:: bash

   env PYTHONPATH=. python test/all.py ParserTest.test_raw_data



Publishing a Release
====================

* Check the setup.py version.
* Commit and push everything.
* Activate the 3.6 venv (to get twine, wheel, etc)
* Run: rm -rf dist
* Run: python setup.py sdist
* Run: python setup.py bdist_wheel --universal
* Run: twine upload dist/*
* Run: git tag v$VERSION
* Run: git push --tags
* Go to GitHub and make a release
* Bump the setup.py version for next time, and commit.

