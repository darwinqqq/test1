# test1
import math
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self) -> float:
        pass

class Circle(Shape):
    def __init__(self, radius: float):
        if radius <= 0:
            raise ValueError("Радиус должен быть положительным")
        self.radius = radius

    def area(self) -> float:
        return math.pi * self.radius ** 2

class Triangle(Shape):
    def __init__(self, a: float, b: float, c: float):
        if not self._is_valid_triangle(a, b, c):
            raise ValueError("Стороны не образуют допустимый треугольник")
        self.a = a
        self.b = b
        self.c = c

    def area(self) -> float:
        s = (self.a + self.b + self.c) / 2
        return math.sqrt(s * (s - self.a) * (s - self.b) * (s - self.c))

    def is_right_angled(self) -> bool:
        sides = sorted([self.a, self.b, self.c])
        return math.isclose(sides[2]**2, sides[0]**2 + sides[1]**2, rel_tol=1e-9)

    @staticmethod
    def _is_valid_triangle(a: float, b: float, c: float) -> bool:
        return a > 0 and b > 0 and c > 0 and a + b > c and a + c > b and b + c > a

def calculate_area(shape: Shape) -> float:
    return shape.area()
