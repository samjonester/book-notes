# Chapter 4 - The Seam Model

*Procedural code is often viewed as a sheet of text instructions. This is obvious when glancing at the code. The structure resembles paragraphs of text.*
The code often has hard dependencies that cannot be turned off, faked, or mocked in test code. It does not have a clean entry point for isolating and testing a small chunk of logic.

*A seam is a place where you can alter behavior in your program without editing in that place*
> The seam view of software helps us see the opportunities that are already in the code base. If we can replace behanior at seams, we can selectively exclude dependencies in our tests.

## Seam Types
- **Preprocessing Seams** - In the olden days C/C++ had crazy preprocessors before compiling. We don't and this is no longer relevant.
- **Link Seams** - This technique is also dated, error prone, and hacky. Not sure how this could happen in a modern setting.
- **Object Seams** - These seams are provided through proper dependency management. new and static methods are enemies because they create hard dependencies that do not provide a test seam.

