##"A class should know just enough to do its job and not one thing more"

- Dependencies are defined as any piece of knowledge a class must know about a collaborator.
- Some degree of dependency is necessary for collaboration. Unecessary dependencies should be eliminated.
- Each dependency creates a chance that a class will be forced to change when it's collaborator changes. Even when that change is unrelated to the collaboration. This turns minor code tweaks into large undertakings where small changes cascasde across the code base.
- Each dependency makes the code less reasonable.

# Writing Loosely Coupled Code

**Inject collaborators to eliminate the implementation type dependencies**
Deep declaration of dependency implementation eliminates your option to use a different type with the same contract. You are forced to always use that implementation. This is especially a problem in tests, and leads to a desire for partial or over mocking. Both increase coupling and fragility in test code.

**Isolate dependencies that cannot be removed**
"Think of every dependency as an alien bacterium that's trying to infect your class... quarantine each dependency. Dependencies are foreign invaders that represent vulnerabilities, and they should be concise, explicit, and isolated."

**Isolate vulnerable external messages**
- "Embedding externa ldependencies inside complex methods is unnecessary and increaases its vulnerability... Any time you change *anything* you stand the chance of breaking it."
- "Isolating the reference provides some insurance against being affected by that change." 

**Remove argument-order dependencies**
"Unfortunately, it's quite common to tinker with initialization arguments. Especially early on, when the design is not quite nailed down, you may go through several cycles of adding and removing arguments and defaults. If you use fixed-order arguments, each of these cycles may force changes to many dependents. Even worse, you may find yourself avoiding making changes to the arguments, even when your design calls for them because you can't bear to change all the dependents yet again."

**Isolate multiparameter initialization**
When argument-order dependencies are outside your codebase like in an external library, isolate their arguement-order initialization to protect yourself from changes to the initialization order.

"Do not allow these kinds of external dependencies to permeate your code; protect yourself by wrapping each in a method that is owned by your own application."

# Managing Dependency Direction
>"At first glance, it seems that the order of dependency does not matter. In an application that will never change, the choice does not matter. However, your application *will* change and it's in that dynamic future where this present decision has repercussions... If you get this right, your application will be pleasant to work on and easy to maintain. If you get it wrong then the dependencies will gradually take over and the application will become harder and harder to change."

### Choosing Dependency Direction
>"If you were to give them advice about how to behave you would tell them to *depend on things that change less often than you do*"
- Some classes are more likely than others to have changes in requirements.
- Concrete classes are more likely to change than abstract classes.
- Changing a class that has many dependents will result in widespread consequences.

### Recognizing Concretions and Abstractions
"The wonderful thing about abstractions is that they represent common, stable qualities. They are less likely to change than are the concrete classes from which they were extracted."