# Data Types
The project is based on video particle tracking microscopy and analyzing the brownian motion of the bead particles. The data we obtain will be the position ( X, Y corrdinates) and lag time (time in sec). These data will be used to analyze the mean square displacement of the bead particles with respect to time. Further, we will estimate the visocity of glycerol and comapre it to its standard value inorder to check the effectiveness of our experiment.Thus based on the data we will obtain after running the microrheology experiment on video particle tracking, the data types will be mostly floats and integers. We will be using python tool to analyse the observed data estimated from the experiments.

An example of float data types in python annotation is given below;
```python
def calculate_area(X_value: float, Y_value: float) -> float:
 """
    Calculate the area of a rectangle.

    Args:
       X_value (float): The length of the rectangle.
      Y_value (float): The width of the rectangle.

    Returns:
        float: The area of the rectangle.
    """
    return X_value * Y_value

```
In the above example X_value: float and Y_value: float indicate that both parameters should be of type float.

-> float specifies that the return value of the calculate_area function should be of type float.
```python
def add_numbers(x: int, y: int) -> int:
    """
    Add two integers and return the result.

    Args:
        x (int): The first integer.
        y (int): The second integer.

    Returns:
        int: The sum of x and y.
    """
    return x + y
```
Example of integer data types in python annotation

