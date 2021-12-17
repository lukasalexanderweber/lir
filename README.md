# lir
Largest Interior Rectangle implementation in Python. 

### Acknowledgements

Thanks to [Tim Swan](https://www.linkedin.com/in/tim-swan-14b1b/) for making his Largest Interior Rectangle implementation in C# [open source](https://github.com/Evryway/lir) and did a great [blog post](https://www.evryway.com/largest-interior/) about it. The first part was mainly reimplementing his solution in Python.

The used Algorithm was described 2019 in [Algorithm for finding the largest inscribed rectangle in polygon](https://journals.ut.ac.ir/article_71280_2a21de484e568a9e396458a5930ca06a.pdf) by [Zahraa Marzeh, Maryam Tahmasbi and Narges Mireh](https://journals.ut.ac.ir/article_71280.html).

Thanks also to [Mark Setchell](https://stackoverflow.com/users/2836621/mark-setchell) and [joni](https://stackoverflow.com/users/4745529/joni) who greatly helped optimizing the performance using cpython/numba in [this SO querstion](https://stackoverflow.com/questions/69854335/optimize-the-calculation-of-horizontal-and-vertical-adjacency-using-numpy)

### How it works

For a cell grid:

<img width="200" src="https://github.com/lukasalexanderweber/lir/blob/readme/readme_imgs/cells.png">

We can specify for each cell how far one can go to the right and to the bottom:

Horizontal Adjacency             |  Vertical Adjacency
:-------------------------:|:-------------------------:
<img width="300" src="https://github.com/lukasalexanderweber/lir/blob/readme/readme_imgs/h_adjacency.png" /> |  <img width="300" src="https://github.com/lukasalexanderweber/lir/blob/readme/readme_imgs/v_adjacency.png" />

Now the goal is to find the possible rectangles for each cell. For that, we can specify a Horizontal Vector based on the Horizontal Adjacency and Vertical Vector based on the Vertical Adjacency:

Horizontal Vector (2,2)             |  Vertical Vector (2,2)
:-------------------------:|:-------------------------:
<img width="300" src="https://github.com/lukasalexanderweber/lir/blob/readme/readme_imgs/h_vector.png" /> |  <img width="300" src="https://github.com/lukasalexanderweber/lir/blob/readme/readme_imgs/v_vector.png" />

Using the `spans()` function, we get the following possible spans (width, height) for cell (2,2):

```
array([[5, 4],
       [5, 4],
       [5, 4],
       [5, 4],
       [4, 7],
       [4, 7],
       [4, 7]], dtype=uint32)
```

Since `4*7=28 > 5*4=20` a rectangle with width 4 and height 7 is the biggest possible rectangle for cell (2,2).
The width and height is stored in a span map, where the widths and heights of the maximum rectangles are stored for all cells.
Using the area we can identify the biggest rectangle at (2, 2) with  with width 4 and height 7. 

Widths             |  Heights             |  Areas
:-------------------------:|:-------------------------:|:-------------------------:
<img width="300" src="https://github.com/lukasalexanderweber/lir/blob/readme/readme_imgs/span_map_widths.png" /> |  <img width="300" src="https://github.com/lukasalexanderweber/lir/blob/readme/readme_imgs/span_map_heights.png" /> |  <img width="300" src="https://github.com/lukasalexanderweber/lir/blob/readme/readme_imgs/span_map_areas.png" />
