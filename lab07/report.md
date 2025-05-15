---
## Front matter
title: "Laboratory work report №4


mathematical modeling"


subtitle: "Модель гармонических колебаний"
author: "Выполнил: Леснухин Даниил Дмитриевич, 


НПИбд-02-22, 1132221553"

## Generic otions
lang: ru-RU


## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: "Times New Roman"
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы
**Цель работы:**
интерпретация результатов в контексте биологических процессов, а также анализ поведения системы в долгосрочной перспективе.




# Задание 
**Задание** 
Постройте график зависимости численности хищников от численности жертв, а также графики изменения численности хищников и численности жертв при следующих начальных условиях: 14 x = 6 y = 14 . Найдите стационарное состояние системы. 


 
# Выполнение лабораторной работы
**Выполнение лабораторной работы:**
Формула для выбора варианта лабораторной работы (1132221553%70) + 1 = 44

# Постановка задачи конкретному варианту. 

![Лабораторная работа №4. Вариант 44](C:\Users\User\OneDrive\Рабочий стол\матмод\lab04\screenshots\Снимок экрана 2025-04-05 224008.png)
 
Эта система описывает, например, рост численности жертв, когда рядом есть хищники (взаимовыгодное взаимодействие), и вымирание хищников при контакте с жертвами (что может быть интерпретировано иначе — как будто жертвы смертельно опасны для хищников).


# Стационарное состояние (анализ):

Стационарное состояние достигается, когда производные равны нулю:


Система уравнений:

$$
\begin{cases}
-0.21x + 0.035xy = 0 \\
0.25y - 0.021xy = 0
\end{cases}
$$
В первом уравнении вынесем x:

Решение уравнения:

$$
x(-0.21 + 0.035y) = 0 \Rightarrow y = \frac{0.035}{0.21} = 6
$$

Во втором уравнении:

Решение уравнения:

$$
y(0.25 - 0.021x) = 0 \Rightarrow x = \frac{0.021}{0.25} \approx 11.90
$$


# Стационарная точка:

**Стационарная точка**

$$
x_s \approx 11.90, \quad y_s = 6
$$




# Анализ поведения системы


 1. **Графики численности жертв и хищников во времени**

* Численности **жертв** и **хищников** колеблются — они растут и падают с определённой периодичностью.

* Однако амплитуда этих колебаний со временем **затухает**, то есть значения x(t) и y(t) постепенно стабилизируются.

* Это говорит о том, что система стремится к **стационарному состоянию** — равновесию между популяциями.

2. **Фазовый портрет y(x)**

* На фазовом портрете траектория постепенно закручивается и стремится к **устойчивому фокусу** (точке равновесия).

* Это говорит о том, что независимо от начальных условий, численности хищников и жертв будут стремиться к некоторому устойчивому соотношению.




# Построение модели 
**Построение модели**
```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint

# Система уравнений
def predator_prey(z, t):
    x, y = z
    dxdt = -0.21 * x + 0.035 * x * y
    dydt =  0.25 * y - 0.021 * x * y
    return [dxdt, dydt]

# Начальные условия
x0 = 6
y0 = 14
z0 = [x0, y0]

# Временной отрезок
t = np.linspace(0, 100, 1000)

# Численное решение
solution = odeint(predator_prey, z0, t)
x = solution[:, 0]
y = solution[:, 1]

# Построение графиков
plt.figure(figsize=(16, 5))

# x(t) — жертвы
plt.subplot(1, 3, 1)
plt.plot(t, x, label="Жертвы (x)", color="blue")
plt.xlabel("Время")
plt.ylabel("Численность")
plt.title("Жертвы во времени")
plt.grid(True)
plt.legend()

# y(t) — хищники
plt.subplot(1, 3, 2)
plt.plot(t, y, label="Хищники (y)", color="red")
plt.xlabel("Время")
plt.title("Хищники во времени")
plt.grid(True)
plt.legend()

# Фазовый портрет
plt.subplot(1, 3, 3)
plt.plot(x, y, color="green")
plt.xlabel("Жертвы (x)")
plt.ylabel("Хищники (y)")
plt.title("Фазовый портрет: y(x)")
plt.grid(True)

plt.tight_layout()
plt.show()

```
В результате получаем следующий график. Рис. 2

![Отображение графика](C:\Users\User\OneDrive\Рабочий стол\матмод\lab04\screenshots\Снимок экрана 2025-04-05 230159.png)

# Что происходит при x0​=6, y0​=14

Исходя из графиков:

* В начале **много хищников** (14) и **мало жертв** (6).

* Из-за большого количества хищников — численность жертв **сильно падает**.

* Но когда жертв становится очень мало, хищники начинают **голодать и вымирать**, и их численность также снижается.

* После этого, жертвы начинают **восстанавливаться**, а затем и хищники снова начинают расти.

* Этот цикл **повторяется с затухающей амплитудой**, потому что система стремится к **равновесию**.


# Динамика в фазовом пространстве

На фазовом портрете (график y(x)) это видно как **закручивающаяся спираль**, которая со временем приближается к точке:

$$
(x^*, y^*) \approx (11.90, 6)
$$


# X = 6 Y = 14 	

При x0​=6, y0​=14 система не находится в равновесии, но со временем стабилизируется:

* Численности хищников и жертв начинают колебаться.

* Постепенно они сходятся к равновесной точке.

* Поведение соответствует **устойчивому фокусу** — колебания с затуханием.







# Вывод
**Вывод**
В ходе выполнения лабораторной работы была исследована динамика взаимодействия двух популяций: хищников и жертв, описанная системой дифференциальных уравнений.




