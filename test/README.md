# CatLearn Tests

All the tests for the CatLearn code are here. When writing new code, please add some tests to ensure functionality doesn't break over time. We look at test coverage when merge requests are opened and will expect that coverage does not decrease due to large portions of new code not being tested.

## Table of Contents

[(Back to top)](#catlearn-tests)

-   [Test Suite](#test-suite)
-   [Continuous Integration](#continuous-integration)
-   [Command Line](#command-line)

## Continuous Integration

[(Back to top)](#catlearn-tests)

Continuous Integration (CI) is used meaning tests are run whenever a new commit is pushed to the origin. For our purposes, we use [GitLab CI](https://docs.gitlab.com/ce/ci/) which checks whether tests run successfully and the coverage. The tests for the CatLearn code are imported and run in `test_suite.py`. This can be extended with any new tests that may be written to cover new functionality.

_Please be mindful of the runtime for new tests._

### Test Suite

[(Back to top)](#catlearn-tests)

All tests are run in the `test_suite.py` script, using the unittest framework. There are two ways to add new tests.

-   If new functionality is being added to existing functions, simply append a new testing function to the appropriate `TestCase` class. It is important to remember that the function won't be viewed as a test unless it is defined as `test_something(self)`.

-   If the new code goes beyond extending pre-existing functionality, it may be necessary to create a new test class. Please look at the current tests to get an idea of how to set this up. When this is ready, it will be necessary to import the class in `test_suite.py` and add it to the `test_classes_to_run` list.

The `pytest-cov` package is used to generate the coverage reports. Unfortunately it appears as though tests are sorted by name when calling this. Therefore, there can be ordering issues when running tests that assume some specific ordering. It is worth being mindful of this if things start failing for seemingly no good reason. To run the server in the same way as on the CI server do the following:

```shell
  $ pip install --upgrade pytest-cov
  $ py.test --cov=catlearn test/test_suite.py
```

## Command Line

[(Back to top)](#catlearn-tests)

There are two ways of running the tests on the command line. If all the tests are run, it is as simple as just using the following:

```shell
  $ python test/test_suite.py
```

If the desire is to run individual tests, it can be necessary to have generated some data beforehand. This is handled automatically in the `test_suite.py` script, but must be initialized manually otherwise. It is important to run the `test_1_feature_generation.py` script to generate a db of feature vectors and targets. This data can be imported in tests using the `common.get_data()` function.

**Therefore, run the `test_1_feature_generation.py` script before any tests that import from `common.py`.**
