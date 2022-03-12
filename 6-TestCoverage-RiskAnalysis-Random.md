# Test Coverage

Test coverage is a useful tool for finding untested parts of a codebase. Test coverage is of little use as a numeric statement of how good your tests are.

However, high coverage numbers are too easy to reach with low quality testing. Like most aspects of programming, testing requires thoughtfulness. TDD is a very useful, but certainly not sufficient, tool to help you get good tests. If you are testing thoughtfully and well, I would expect a coverage percentage in the upper 80s or 90s.

Certainly low coverage numbers, say below half, are a sign of trouble. But high numbers don't necessarily mean much, and lead to ignorance-promoting dashboards. Sufficiency of testing is much more complicated attribute than coverage can answer.

I would say you are doing enough testing if the following is true:

1. You rarely get bugs that escape into production.
2. You are rarely hesitant to change some code for fear it will cause production bugs.

You can always move slow tests to a later stage in your deployment pipeline, or even pull them out of the pipeline and run them periodically. Doing these things will slow down the feedback from those tests, but that's part of the trade-off of build times versus test confidence.

<br>

# Risk Analysis

Risk analysis is the process of identifying the risks in applications or software that you built and prioritizing them to test. Using risk analysis at the beginning of a project highlights the potential problem areas. It helps the developers and managers to mitigate the risks and consider them in the test plan.

The possible risks that you could encounter:
- Use of new hardware
- Use of new technology
- Use of new automation tool
- The sequence of code
- Availability of test resources for the application

There are certain risks that are unavoidable:
- The time that you allocated for testing
- A defect leakage due to the complexity or size of the application
- Urgency from the clients to deliver the project
- Incomplete requirements

In such cases, you have to tackle the situation with care. Following points can be taken care of:
- Conduct Risk Assessment review meeting
- Use maximum resources to work on high-risk areas
- Create a Risk Assessment database for future use
- Identify and notice the risk magnitude indicators: high, medium, low.

Risk magnitude indicators:

- High: means the effect of the risk would be very high and non-tolerable. The company might face loss.

- Medium: it is tolerable but not desirable. The company may suffer financially but there is a limited risk.

- Low: it is tolerable. There lies little or no external exposure or no financial loss.

There are different sets of risks included in the risk identification process:
1. Business Risks: This risk is the most common risk associated with our topic. It is the risk that may come from your company or your customer, not from your project.
2. Testing Risks: You should be well acquainted with the platform you are working on, along with the software testing tools being used.
3. Premature Release Risk: a fair amount of knowledge to analyze the risk associated with releasing unsatisfactory or untested software is required
4. Software Risks: You should be well versed with the risks associated with the software development process.

Risk Assessment steps:
1. Forecasting for unwanted situations
2. Estimate the potential loss
3. Make decisions to deal with the situation
4. Avoid the future consequences

The perspective of Risk Assessment:
- Effect – To assess risk by Effect. In case you identify a condition, event or action and try to determine its impact.

- Cause – To assess risk by Cause is opposite of by Effect. Initialize scanning the problem and reach to the point that could be the most probable reason behind that.

- Likelihood – To assess risk by Likelihood is to say that there is a probability that a requirement won’t be satisfied.

perform Risk Analysis:
1. Searching the risk
2. Analyzing the impact of each individual risk
3. Measures for the risk identified

<br>

# Random Module

Random is module offers many methods that git random values in defferant ways:

- `randint(start, end)`: creates an integer number between start and end vlaues.

- `random()`: creates a random float between 0 and 1, you can multuply it with any value, for example `random.random()*100` will produce a random float between 0 and 100

- `choice(list)`: choose a random item from the list

- `shuffle(list)`: shuffles the elements in list in place, so they are in a random order.

- `randrange(start, stop, step)`: Generate a randomly selected element from range with a step value

