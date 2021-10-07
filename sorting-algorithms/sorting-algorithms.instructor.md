# Instructor: Sorting Algorithms

## Sorting Algorithms (Lesson)

A huge reason why we're teaching sorting algorithms is because it's considered "common knowledge" among traditional CS education.

I think it's worth mentioning that fact verbally, to help students understand what to get out of this.

## Selection Sort Stability

To make selection sort stable, instead of directly swapping the value at `min_index` with the value at `i`, we can all the intervening values up by one to open the spot where the selected value needs to go.  With this modification, selection sort closely resembles an in-place insertion sort.

If anyone asks, Python's default sort is a custom blend of insertion sort and merge sort, tuned so that it performs very well on both small and large data sets.

### textbook-curriculum C14 Video Lesson & Slides

- [Video Lesson](https://adaacademy.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=a4668a63-9fb8-4778-b0a4-aaca006b34c8)
- [Slide Deck](https://docs.google.com/presentation/d/1GkYP84Cbg3I5KS_wIfRN8Gn-5tQ_46vV5zWt1dTZn14/edit?usp=sharing)
- [Sorting Exercise](https://github.com/Ada-c14/string-manipulation-practice)
