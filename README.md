## Autograder

For my project, I produced an example SKETCH file that demonstrates the translation from mPy to SKETCH. My example successfully identifies modifications to the student's code that can make its output match that of the reference implementation. My translation is based on Figure 4 from the paper.

### Running the Example
I tested my SKETCH file using the following command:
```
sketch --bnd-inbits 3 --bnd-inline-amnt 3 example.sk
```

To identify the discoverd changes to the input, you can look at the generated code for functions starting with "mod" and see if they assign to their designated "choice" variable. If they do, the non-default selection was made. I believe this is the best way to find the discovered changes -  I didn't spend time making a tool to make the changes readable.

### Overview

The method `computeDerivStudent` represents how a student's Python code might be eventually translated to a SKETCH method after being converted to mPy. Note that this translation does not 100% follow the technique described by the book - while I did convert some control flow (like for loops) into expressions operating on `MultiType` values, some aspects of the conversion still utilize SKETCH language constructs (for example, I didn't really implement a translation for `if` statements). This should be fairly trivial to improve, I just ran out of time before I could make a second pass on my translation.

Here are the translation features I did implement:
* Determining `MultiType` equality.
* Adding and multiplying `MultiType` values.
* Simulating the Python `range` function.
* Simulating Python `for` loops.
* List indexing. 
* List length calculation.
* Miscellaneous conversion utilities for SKETCH and `MultiType` values.

### Takeaways

I am satisfied with this project, since it really helped me understand aspects of the paper that I felt were ambiguous after my initial read. The sketch languge itself is really interesting and makes some design decisions that make certain things incredibly easy (e.g. writing type-agnostic lambdas that return a simple expression) and other things verbose (e.g. writing lambdas that do _anything_ other than that). Interpreting the sketch output was also tricky at times, since some error messages seemed to either indicte an internal sketch issue or hint at a problem that was far from the root issue. Furthermore, I had to do a lot of experimentation with various input bounds so that sketch wouldn't get stuck on something random and fail. All in all, I'm happy to have experimented with this and satisfied that I was able to produce a working example.
