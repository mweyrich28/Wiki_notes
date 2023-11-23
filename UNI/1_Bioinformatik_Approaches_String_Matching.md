# Basics
:prefix:suffix:factor:

## Prefix searching

### Definition
Given String: *[XY]*
Here *X* is the _PREFIX_ of *[Y]*

### Basic idea
For each position in the window we seek the longest *SUFFIX* of the search window, which is also a *PREFIX* of the pattern:


## Suffix searching

### Definition
Given String: *[XY]*
Here *Y* is the _SUFFIX_ of *[X]*

### Basic idea
Search is conducted _BACKWARDS_ along the search window, matching a _SUFFIX_ in the search window with a _SUFFIX_ of the pattern.


## Factor searching

### Definition
Given String: *[XYZ]*
Here *Y* is the _FACTOR_ (substring) of *[XYZ]*

### Basic idea
The search is done backwards in the search window, looking for the _LONGEST SUFFIX_ in the window that is also a _FACTOR_ of the
pattern
