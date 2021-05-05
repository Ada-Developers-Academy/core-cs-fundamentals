# Instructor: Recursion

## Problem Set: Recursion Pt 1

For the challenge problem for `is_nested_parens`, the key is to use a helper function which needs extra params.

Here is a sample solution:

```python
def is_nested_parens(parens):
    return is_nested_helper(parens, 0, 0)

def is_nested_helper(parens, pos, depth):
    if pos >= len(parens):
        return True

    depth += 1 if parens[pos] == '(' else -1

    if depth < 0:
        return False

    return is_nested_helper(parens, pos + 1, depth)
```

## textbook-curriculum Content

- [Video Lesson](https://adaacademy.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=5250fb87-0391-438b-a492-aaed0018dc67)
- [Slides](https://docs.google.com/presentation/d/14saSh8YZsVSkkYqQA7vX-uqQ-q0qLqnm9inOVXHfWdo/edit?usp=sharing)
- [Exercise](https://github.com/Ada-C14/recursion-writing)

## Resources

- [FreeCodeCamp How Recursion Works](https://www.freecodecamp.org/news/how-recursion-works-explained-with-flowcharts-and-a-video-de61f40cb7f9/)
- [UW Lesson On Recursion](https://www.cs.washington.edu/apcs/lessons/recursion) - Java Focused
