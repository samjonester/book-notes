# Chapter 6 - I Don't Have Much Time and I Have to Change It

*Changes tend to cluster in a system. If you change some code today, then there's a good chance you'll be making another change close by tomorrow.*

- First try to instantiate the class in a test harness. If you can, then, the change is easier than you think.
- If you can't then come up with a plan to isolate the new change under the tight deadline.

## Sprout Method
*The worst action to take is to change the code and make it muddier. Try to make your change outside of the existing code.*

1. Identify where you need to make your code change.
2. If the change can be formulated as a single sequence of statements in one place in a method, write a call for a new method/class that will do the work and comment it out.
  This defines the public api for your new action. Also it creates a new feature toggle.
3. Develop the sprout method using TDD.
4. Remove the commented out feature toggle and manually test the addition.

- Favor sprout classes over sprout methods. They start to bring better object oriented principles into the code base.

## Wrapper Method
*When adding code to existing code, there's a good chance that you're choosing to add it to that place because it needs to be executed at that time, not to organize functionality. This action is called __Temporal Coupling__.*

1. Identify when your change needs to be executed. Create a method name that is more descriptive and move the entire method into it.
2. Call the new method from the old, almost as a pass through.
3. Sprout from there
