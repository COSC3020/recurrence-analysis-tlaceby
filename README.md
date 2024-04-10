[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/OlW38W4k)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

### Analysis

Let $T(n)$ be the running time of `mystery(n)`.

**Base case**:  When $n \leq 1$, the function returns immediately, so $T(1) = \Theta(1)$.

**Recursive case**: When $n > 1$, the function makes three recursive calls to mystery(n/3) and executes a nested loop structure. 

Thus the runtime of the three recursive calls is $3 \cdot T(n/3)$.

**Loop Complexity**:
The outer loop runs $n^2$ times and
the middle one runs $n$ times for each iteration of the outermost loop.

The inner loop runs $n^2$ times for each iteration of the middle loop.
Therefore the total number of operations in the nested loop is $n^2 \cdot n \cdot n^2 = n^5$.

By combining all the above mentioned statements:
$T(n) = 3 \cdot T(n/3) + n^5$ when $n > 1$

**Recurrence Relation & Final Solution**

I would reason that the term $n^5$ and $3 \cdot T(n/3)$ can be analized seperately then combined after. Thus $3 \cdot T(n/3)$ would be $\Theta(n)$
and $n^5$ would become $\Theta(n^5)$

Finally we get $T(n) = \Theta(n) + \Theta(n^5)$ which simplifies to $\Theta(n^5)$ when $n > 1$.

Therefore the runtime complexity of the `mystery()` function is $\Theta(n^5)$.