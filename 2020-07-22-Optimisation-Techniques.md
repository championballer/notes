# Optimisation Techniques

- Unconstrained Multivariate Search Methods
    - Direct Search Method
        - Random Search / Random Jump Method
        - Grid Search Method
        - Simplex Method
        - Univariate Search Method
        - Pattern Search Method
            - [https://www.youtube.com/watch?v=b-ob1sfXOTk&t=1543s](https://www.youtube.com/watch?v=b-ob1sfXOTk&t=1543s)
        - Rosen Brock's Hill Climbing Method

            Keep searching till a better solution exists. Heuristic function acts as the metric to judge the value of the next state. This method can be used for discrete problems. It's a greedy approach. There is no backtracking. Stop when no more improvement can be made. 

            **Issues** : Moves towards local maxima, plateau might be hit (all states have same heuristic, but one might lead to maxima, but we stop), Direction change is not possible (Ridge).

            Can be used to work on Travelling Salesman or NQueen Problem. 

            Space complexity is less.

            Coordinate system is rotated in such a way that the first axis always orients to the locally estimated direction of the best solution and all the axes are made mutually orthogonal and normal to the first one.

    - Indirect Search Method
        - Steepest Descent / Gradient Descent
            - [https://www.youtube.com/watch?v=7KxlpQIbKUw](https://www.youtube.com/watch?v=7KxlpQIbKUw)
        - Conjugate Gradient Method

            [https://www.youtube.com/watch?v=eAYohMUpPMA](https://www.youtube.com/watch?v=eAYohMUpPMA)

            [https://www.youtube.com/watch?v=8-xkiGB28zc](https://www.youtube.com/watch?v=8-xkiGB28zc)

            [https://www.youtube.com/watch?v=IlVx_t0VseU](https://www.youtube.com/watch?v=IlVx_t0VseU)

            Improves on gradient descent by taking orthogonal steps (more specifically A-orthogonal). Avoids redundancies. 

            Read from S S Rao, after watching the gradient descent lecture above. Use conjugate concept to calculate a better search direction, and that search direction is used to compute the step length, which together give the new point to find the functional value at, and continue the process, until the limiting condition is not hit. 

        - Newton Method

            Hessian matrix is used in the iterative process to compute the next points. 

        - Quasi Netwon Method

            They approximate the Hessian matrix, or its inverse, in order to reduce the amount of computation per iteration. The Hessian matrix is updated using the secant equation, a generalization of the secant method for multidimensional problems.

    - Hill Climbing vs Gradient Descent
        - Gradient descent is a specific kind of “hill climbing” algorithm.

            A superficial difference is that in hillclimbing you maximize a function while in gradient descent you minimize one.

            Let’s see how the two algorithms work:

            In hillclimbing you look at all neighboring states and evaluate the cost function in each of them and then chose to move to the best neighboring state.

            In gradient descent you look at the slope of your local neighborhood and move in the direction with the steepest slope.

            In hillclimbing you can optimize discrete problems (e.g. traveling salesman). You just need to be able to evaluate a cost function for a given state.

            Gradient Descent assumes you optimize a continuous function and can compute it’s gradient in a given state.

            Usually gradient descent is much more efficient than naive hillclimbing, but the set of problems it can attack is more restricted.

- Constrained Multivariate Search Methods / Optimisation Techniques
    - [Equality Constraint](https://www.youtube.com/watch?v=LdBXuN7Tbs4) : Building an unconstrained optimisation problem from constrained optimisation problem, and then using first order derivatives as necessary conditions to find extreme points, and second order derivatives (Hessian) to judge behaviour of function at extreme point.
        - Direct Substitution
        - Lagrange Multiplier Method
            - Multiplier for each constraint
            - First Derivatives about each variable equal to 0 to get stationary point.
            - (m+n) equations and (m+n) variables. So, stationary point along with multiplier can be evaluated.
            - Second Derivatives (Hessian), positive definite for minima, and negative definite for maxima. To check definite behaviour we use the principal minor determinants. Another method is to compute the Eigen values of the hessian matrix.
    - KKT Conditions (Kuhn - Tucker Conditions)
        - [https://www.youtube.com/watch?v=_Lt3zNdnE0k](https://www.youtube.com/watch?v=_Lt3zNdnE0k)
        - KKT Conditions are (derived using the first derivatives of the adapted Lagrange multiplier function) :
            - Condition of optimality
            - Condition of feasibility
            - Condition of complementary slackness
            - Condition of non-negativity
        - Few constraints are active and others are inactive. Condition of slackness along with condition of feasibility can be used to find these conditions.
        - <0 conditions (for active multipliers)
            - min → $\lambda$ > 0
            - max → $\lambda$ < 0
        - >0 conditions (for active multipliers)
            - min → $\lambda$ < 0
            - max → $\lambda$ > 0
    - Gradient Projection Method

        [https://neos-guide.org/content/gradient-projection-methods#:~:text=If properly implemented%2C the gradient,the subspace of free variables](https://neos-guide.org/content/gradient-projection-methods#:~:text=If%20properly%20implemented%2C%20the%20gradient,the%20subspace%20of%20free%20variables).

        projection of the negative of the objective function gradient onto the constraints that are currently active.

        effectiveness is confined primarily to problems in which the constraints are all linear

    - Cutting Plane Method
        - [https://www.youtube.com/watch?v=PkFKuoJQrN4&t=12s](https://www.youtube.com/watch?v=PkFKuoJQrN4&t=12s)
        - Use simplex method to solve the equation. If fractional part is encountered, then gromory constraint is added, and then we again solve using simplex, and keep doing the same till fractional values are eliminated.
    - Penalty Function Method
        - [https://www.youtube.com/watch?v=nYN6FRV6sCM](https://www.youtube.com/watch?v=nYN6FRV6sCM)
        - Basic concept is that we associate a penalty with infeasible solutions, proportional to the extent by which they violate the constraint, and then convert the problem to an unconstrained problem. Different for equality and inequality constraint. Solve for first order derivatives, and as per interior or exterior strategy, limit the value of $\mu$, and get the extremum points.
        - Exterior Penalty Function
            - max(0, g(x)) function with higher order degree
            - For exterior as $\mu$  → $\infin$ , we will reach a feasible solution, and that will be the point of extremum.
        - Interior Penalty Function
            - Inverse barrier function
            - Logarithmic function
            - For interior as $\mu$ → 0, we will reach the final feasible solution, and that will be the point of extremum.
- Dynamic Programming
    - [https://www.youtube.com/watch?v=dND9IsjL1lo](https://www.youtube.com/watch?v=dND9IsjL1lo)
    - Recursive Equation Approach
        - [https://www.youtube.com/watch?v=6v6_2Lo3_J4](https://www.youtube.com/watch?v=6v6_2Lo3_J4)
        - [https://nptel.ac.in/content/storage2/courses/105108127/pdf/Module_5/M5L2slides.pdf](https://nptel.ac.in/content/storage2/courses/105108127/pdf/Module_5/M5L2slides.pdf)
    - Shortest Route Algorithm / Djikstra's Algorithm
        - [https://www.youtube.com/watch?v=DAj7mtiAiQM](https://www.youtube.com/watch?v=DAj7mtiAiQM)
        - Mark all the nodes other than the current node as $\infin$. Explore neighbouring nodes, and update distance for neighbouring nodes, mark parent node as visited, and repeat the same process for the other states.
    - Cargo - Loading, Allocation and Production Schedule Problems (Knapsack problem)
        - [https://www.youtube.com/watch?v=C2vYcnOqJUQ](https://www.youtube.com/watch?v=C2vYcnOqJUQ)