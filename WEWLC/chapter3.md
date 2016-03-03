# Chapter 3 - Sensing Separation

> In systems that weren't developed concurrently with unit tests, we often have to break dependencies to get lcasses into a test harness.

## 2 reasons to break dependencies
1. **Sensing** - We break dependencies to *sense* when we can't access values our code computes.
  This is a feeling that is characterized by unease about side affects caused by an area of code.
2. **Separation** - We break dependencies to *separate* when we can't even get a piece of code into a test harness.

> If we want to write tests for NetworkBridge, how do we do it? The class could very well make some calls to real hardware when it is constructed. Do we need to have the hardware available to create an instance of the class? Worse than that, how in the world do we know what the bridge is doing to that hardware or the endpoints.

This is a situation that in modern times happens with dependencies on external network services, file systems, and databases. Modern web frameworks have resolved much of the problems around database dependencies to test, but the other two are easy traps to fall into. Depending on them makes testing hard, fragile, and very difficult to automate in CI.

#### The naive solution is to troubleshoot a solution to work around inflexible code. The book cites techniques to sniff packets and devoted test hardware. This is a PITA and a more thoughtful approach would ask how to remove the dependency, not how to work around it.

*Use fakes and mocks to verify collaborating objects are coordinated with properly*
