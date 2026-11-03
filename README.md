class Animal:
    def __init__(self, name, age, color):
        self.name = name
        self.age = age
        self.color = color

    def make_sound(self):
        pass


class Dog(Animal):
    def make_sound(self):
        return "Гав-гав!"


class Cat(Animal):
    def make_sound(self):
        return "Мяу!"


class Cow(Animal):
    def make_sound(self):
        return "Мууу!"


animals = []

file = open("animals.txt", "r", encoding="utf-8")
for line in file:
    words = line.split()
    if len(words) == 4:
        t, name, age, color = words[0], words[1], int(words[2]), words[3]
        if t == "Собака":
            animals.append(Dog(name, age, color))
        elif t == "Кошка":
            animals.append(Cat(name, age, color))
        elif t == "Корова":
            animals.append(Cow(name, age, color))
file.close()

for a in animals:
    print(a.name, a.color, a.age, a.make_sound())



import math
import tkinter as tk


# --- Задание 1 ---

class Animal:
    def __init__(self, name, age, color):
        self.name = name
        self.age = age
        self.color = color

    def make_sound(self):
        pass


class Dog(Animal):
    def make_sound(self):
        return "Гав-гав!"


class Cat(Animal):
    def make_sound(self):
        return "Мяу!"


class Cow(Animal):
    def make_sound(self):
        return "Мууу!"


# Чтение из файла для задания 1
animals = []
file = open("animals.txt", "r", encoding="utf-8")
for line in file:
    words = line.split()
    if len(words) == 4:
        t, name, age, color = words[0], words[1], int(words[2]), words[3]
        if t == "Собака":
            animals.append(Dog(name, age, color))
        elif t == "Кошка":
            animals.append(Cat(name, age, color))
        elif t == "Корова":
            animals.append(Cow(name, age, color))
file.close()

for a in animals:
    print(a.name, a.color, a.age, a.make_sound())


# --- Задание 2 ---

class Table:
    def __init__(self, height, width, shape):
        self.height = height
        self.width = width
        self.shape = shape

    def area(self):
        if self.shape == "круглый":
            return math.pi * (self.width / 2) ** 2
        else:
            return self.width * self.height


# Интерфейс для задания 2
root = tk.Tk()
root.title("Столы")
root.geometry("300x250")

tk.Label(root, text="Форма (круглый / прямоугольный):").pack()
e_shape = tk.Entry(root)
e_shape.pack()

tk.Label(root, text="Ширина / Диаметр:").pack()
e_width = tk.Entry(root)
e_width.pack()

tk.Label(root, text="Высота / Длина:").pack(text="Высота")
e_height = tk.Entry(root)
e_height.pack()

e_result = tk.Entry(root)
e_result.pack(pady=5)


def calculate():
    sh = e_shape.get()
    w = float(e_width.get())
    h = float(e_height.get())
    t = Table(h, w, sh)
    e_result.delete(0, tk.END)
    e_result.insert(0, str(round(t.area(), 2)))


btn = tk.Button(root, text="Посчитать площадь", command=calculate)
btn.pack(pady=10)

root.mainloop()
