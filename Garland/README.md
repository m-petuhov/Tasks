# Гирлянда
>**Условие задачи находится в файле [Task.pdf](./Task.pdf).**

### Решения задачи с асимптотической сложностью O(1)

Так как высота задается рекуррентной формулой, то сложно судить о характере функции, описывающей  
зависимость высоты от порядка лампочки. Следовательно, нужно будет выполнить некоторые преобразования 
и проанализировать итоговую формулу.
  
**Ход решения**

1. Условимся, что высота первой лампочки будет задаваться параметром **A**
2. Высота второй лампочки параметром **x**
3. Порядок лампочки будет задаваться переменной **n**
4. Введя все необходимые обозначения, рассчитаем высоту второй лампочки исходя из формулы, 
заданной в условии:  
h<sub><small>2</small></sub> = (h<sub><small>1</small></sub> + h<sub><small>3</small></sub>) / 2 - 1  
Подставим введенные обозначения h<sub><small>1</small></sub> = A, h<sub><small>2</small></sub> = x :    
x = (A + h<sub><small>3</small></sub>) / 2 - 1  
Выразим из формулы h<sub><small>3</small></sub> :    
h<sub><small>3</small></sub> = 2 * x + 2 - A
5. Повторим действие (4) для h<sub><small>3</small></sub> :  
h<sub><small>3</small></sub> = (h<sub><small>2</small></sub> + h<sub><small>4</small></sub>) / 2 - 1  
2 * x + 2 - A = (x + h<sub><small>4</small></sub>) / 2 - 1 &#8658;   
h<sub><small>4</small></sub> = 4 * x + 6  - 2 * A - x = 3 * x + 6 - 2 * A  
6. Рассчитаем еще несколько значений высот при различных **n** и составим таблицу:     

|  n  |        height        |
|:---:|:--------------------:|
|  1  |        A             |
|  2  |        x             |
|  3  |   2 \* x + 2 - A     |
|  4  |  3 \* x + 6 - 2 \* A |
|  5  | 4 \* x + 12 - 3 \* A |
|  6  | 5 \* x + 20 - 4 \* A |
| --- |         ---          |

7. Посмотрим на коэффициенты при **x**. Не трудно заметить, что каждый раз их значение ровно на 1 
меньше, чем порядок у лампочки &#8658; будет задаваться формулой вида: (n - 1)  
8. Перейдем к коэффициенту при **A**. Зависимость не такая очевидная, но после недолгих раздумий 
приходим к виду: (2 - n)  
9. Самая трудно уловимая зависимость у коэффициента свободного члена выражения. Но все же она есть и
имеет вид: (n - 1) * (n - 2) `Перемножение коэффициентов при x и A`  
10. В итоге наша формула свелась к виду:  
h<sub><small>n</small></sub> = (n - 1) \* x + (n - 1) \* (n - 2) - (n - 2) \* A  
`Стоит заметить, что данная запись представлена в несколько непривычном виде, так как в роли изменяемой
величины выступает переменная n, в то время как x является неизвестным параметром`  
11. Раскроем скобки:  
h<sub><small>n</small></sub> = n \* x - x + n<sup><small>2</small></sup> - 3 \* n + 2 - n \* A + 2 \* A  
12. Приведем уравнение к привычному виду:  
h<sub><small>n</small></sub> = n<sup><small>2</small></sup> - n \* (3 - x + A) - x + 2 + 2 \* A  

Задача свелась к тому, чтобы найти коэффициент **x**, который не нарушит условия задачи. Также заметим, что данная
формула является уравнение параболы

Приступим к анализу формулы.

1. Логично, что самая маленькая высота это 0 &#8658; подставим в формулу 10 шага значение высоты равную 0 и
тем самым найдем зависимость **x** от **n**, чтобы получать высоту равную 0 для конкретной лампы :  
0 = (n - 1) \* x + (n - 1) \* (n - 2)  - (n - 2) \* A &#8658;  
x = ((n - 2) \* A - (n - 1) \* (n - 2)) / (n - 1)   
2. Если вспомнить график параболы, то есть три случая пересечения с осью, график не пересекает ось, касается 
и пересекает в двух точках. Когда мы считаем значение **x** по той формуле, 1 случай отпадает, 
так как у нас уже есть как минимум одна точка пересечения. Но если наша парабола будет пересекать 
ось в двух точках, то это нарушает два условия: все высоты целые числа; только одна лампа может касаться земли.
Вот мы и подошли к ограничению на **x**
3. Рассчитаем производную уравнения шага 12:  
(h<sub><small>n</small></sub>)' = 2 \* n - 3 + x - A  
4. Вспомним определение производной, если она меньше нуля, то значит график убывает; равна нулю, то точка
является экстремумом, для параболы это вершина. Что дает нам значение **x**? Она определяет какие точки 
лежат на левой и правой ветви параболы. Но наша формула некорректна только для случая когда наша точка лежит в правой ветви, 
следовательно, нам необходимо чтобы значение производной нашей точки было меньше либо равно нулю. Объединим 
условия.   
x = ((n - 2) \* A - (n - 1) \* (n - 2)) / (n - 1)   
2 \* n - 3 + x - A  &#8804; 0  
Решим систему относительно n :  
2 \* n - 3 + ((n - 2) \* A - (n - 1) \* (n - 2)) / (n - 1) - A  &#8804; 0   
A \* n - A + 3 \* n - 3 - 2 \* n<sup><small>2</small></sup> + 2 \* n &#8804; n \* A - 2 \* A - n<sup><small>2</small></sup> + 3 \* n - 2  
n<sup><small>2</small></sup> - 2 \* n + 1 - A &#8804; 0  
D = 2<sup><small>2</small></sup> - 4 \* (1 - A) = 4 \* A  
n<sub><small>1</small></sub> = 1 - A<sup><small>1/2</small></sup>  
n<sub><small>2</small></sub> = 1 + A<sup><small>1/2</small></sup>  
Но n - натуральные числа &#8658; первый корень отпадает.  
&#8658; 1 &#8804; N &#8804; 1 + A<sup><small>1/2</small></sup>   
5. Что значит это **N**? Оно определяет максимальное колличество ламп на левой ветви. Что значит это ограничение на **N**? Если это условие выполняется, то наша формула для **x** справедлива, иначе
для получения минимальной высоты мы должны рассчитать **x** по той же формуле, но для максимально возможной **N**, 
то есть для **1 + A<sup><small>1/2</small></sup>**. После просто подставляем значение **x** в формулу высоты.
