# Final-Project


Colorization - Final Project

1. Current challenges to colorization
1) Automatic segmentation algorithms often fail to correctly identify fuzzy or complex region boundaries, such as the boundary between a subject’s hair and her face
2) Colorization of movies requires, in addition, tracking region across the frames of a shot. Existing tracking algorithms typically fail to robustly track non-rigid regions, again requiring massive user intervention in the process.

2. New interactive colorization technique
1) User indicates how each region should be colored by scribbling the desired color in the interior of the region
2) New technique automatically propagates colors to the remaining pixels in the image sequence, by assuming nearby pixels in space-time that have similar gray levels should also have similar colors. 
Thus, we tend to minimize the difference between color at pixel r and the weighted average of colors at neighboring pixels:
J(U) = \sum_r (U(r) - \sum_{s\in N(r)} w_rs U(s))^2

Two weighting functions are used:
1. Squared difference between the two intensities:
w_rs ~= exp(-(Y(r) - Y(s))^2/{2\sigma_r^2})
2. Normalized correlation between two intensities (implemented)
w_rs ~= 1 + 1/\simga_r^2 (Y(r) - \mu_r )(Y(s) - \mu_r)  where \mu_r and \sigma_r are the mean and variance of the intensities in a window around r

Assumption: the color at pixel U(r) is a linear function of intensity Y(r):
U(r) = a_i Y(r) + b_i
and the linear coefficients are the same for all pixels in a small neighborhood around r. Typically this means that when the intensity is constant the color should be constant, and when the intensity is an edge, the color should also be an edge.

Neighbors: r\in N(s) denotes the fact that r and s are neighboring pixels. For two successive frames, two pixels are neighbors if their image locations are nearby. Then  (X-0, y_0, t) is a neighbor of pixel (x_1, y_1, t+1) if:
|| (x_0 + v_x(x_0), y_0 + v_y(y_0)) - (x_1,y_1) ||< T
where follow field v_x(x_0) and v_y(y_0) are calculated using a standard motion estimation algorithm.


Implementation
1. Still image: least square solver
2. Movie: multigrid solver

Example: to change the color of an orange to green
1. Define a rough mask around it and then scribbles inside the orange using desired color
2. 








Related Repository
https://github.com/depu0217/cs6475_finalproject/  (zero reference)
https://github.com/depu0217/Colorization-1  (6 references)
https://github.com/depu0217/ColorizationOptimization (zero reference)
https://github.com/depu0217/colorization-2 (zero reference)
https://github.com/depu0217/colorization_using_optimization (2 references) 
https://github.com/depu0217/ColorizationUsingOptimizationInPython (1 reference)


Reference page

http://www.cs.huji.ac.il/~yweiss/Colorization/ 

Jack 2001 Video Demystified, 3rd Edition, Elsevier Science & Technology
Y = 0.299R´ + 0.587G´ + 0.114B´
U = – 0.147R´ – 0.289G´ + 0.436B´
    = 0.492 (B´ – Y)
V = 0.615R´ – 0.515G´ – 0.100B´
    = 0.877(R´ – Y)


R´ = Y + 1.140V
G´ = Y – 0.395U – 0.581V
B´ = Y + 2.032U




