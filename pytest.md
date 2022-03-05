# Pytest

Testing your code is on eof the most important steps in building any application. Testing must be on the edge cases of your code to make sure thet you passed them in the way you wanted.

## Fixtures

When you're writing tests, you're rarely going to write just one or two. Rather, you're going to write an entire "test suite", with each test aiming to check a different path through your code. But in other cases, things are a bit more complex. You'll want to have some objects available to all of your tests. Those objects might contain data you want to share across tests, or they might involve the network or filesystem. These are often known as "fixtures" in the testing world, and they take a variety of different forms.

In pytest, you define fixtures using a combination of the `pytest.fixture` decorator, along with a function definition.

    @pytest.fixture
    def simple_file():
        return StringIO('\n'.join(['abc', 'def', 'ghi', 'jkl']))

If you want to include this fixture in one of your tests. You then can mention it in the test's parameter list. Then, inside the test, you can access the fixture by name. For example:


    def test_reverse_lines(simple_file):
         assert reverse_lines(simple_file) == bla bla bla

This means that the fixture, in contrast with regular-old data, can make calculations and decisions, simply becoause it is a function at the end.

You can pass the `scope` parameter to the `@pytest.fixture `decorator, and this will let you decide how the fixture runs. For example, if you set the scope of the fixture to be `module`, it'll be available throughout your tests but will execute only a single time.

If your fixture uses "yield" instead of "return", pytest understands that the post-yield code is for tearing down objects and connections. And yes, if your fixture has "module" scope, pytest will wait until all of the functions in the scope have finished executing before tearing it down.

<br>

<br>

## Coverage

Covering all possible cases that your application could face is good, but evine if you have 100% code coverage this doesn't mean that your code is perfect or that it lacks bugs. I couldent denie this could give you a greater degree of confidence in the code and the fact that it has been run at least once.

But it is hard to cover 100% of the cases. To overcome that, there's a package called pytest-cov on PyPI that you can download and install.

Once that's done, you can invoke pytest with the `--cov `option with specifying which program(s) you want to test. Once you've done this, you'll need to turn the coverage report into something human-readable. I suggest using HTML `coverage html`. This creates a directory called htmlcov. Open the index.html file in this directory using your browser, and you'll get a web-based report showing (in red) where your program still lacks coverage.
