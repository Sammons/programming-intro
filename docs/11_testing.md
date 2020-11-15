## Testing

Programmers make a lot of mistakes. We anticipate this having had decades of experience watching everyone screw up.

Since we are pragmatic and lazy, instead of manually testing everything with extreme rigor to catch these mistakes, the entire industry has started developing various automated tests to validate our systems.

### Unit Tests

Unit tests are really small tests, which typically run fast, that validate a unit of code, typically a function, is written the way it is intended.

`jest` is a framework for writing tests in TypeScript or JavaScript, `pytest` can be used with Python.

`JUnit` is used for Java, and every language has tools for writing and running unit tests.

### Functional Tests

Functional tests are meant to prove features work. They may call APIs or do a sequence of things, but they are meant to emulate real interactions with a system to prove it functionally meets the goals it has.

Sometimes people get confused if Functional tests are Integration tests. The answer is that they may overlap, but Functional tests prove that the system implementation and design works to accomplish an outcome.

Suppose you accidentally broke some end-to-end feature in an API. The unit tests may miss it, and the integration tests may miss it too because the server-to-server calls all work.

Functional tests should catch this because they actually care about what users can do.

### Integration Tests

Tests that prove inter-service touchpoints work. If you have three services that call eachother, you have these tests to prove they can still communicate successfully.

Often integration tests are UI tests which run on a technology like Cypress, or Selenium.

### Smoke Tests

Minimal tests that are meant to trigger alarms. The idea is to ask if something is going to go wrong, where will it go wrong?

Run these tests and check for signs of "smoke", which should precede fire and explosions.

Some people do some minimal load testing as part of Smoke Testing. Not to check if the architecture scales, but just to make any issues really stand out.

### Load Tests

These tests strain the system to find limitations. How many requests can your web server realllly handle.

Services exist to help with this if you just have a public website and you are curious - e.g. blitz.io

Careful with load testing other people's servers though. that could be consider a DDoS attack.

### Canaries

These tests run in production. It is bad form to let your users detect your mistakes in production. Usually whatever tests are canaries also run in a pre-prod environment, but these are the last automated test we have.

Often canaries are really minimal, sometimes even just health checks, and they tend to be most helpful in proactively detecting outages.

If google.com goes down, you can be sure a canary just fell over!