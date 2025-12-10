<p align="center"><b>МОНУ НТУУ КПІ ім. Ігоря Сікорського ФПМ СПіСКС</b></p>
<p align="center">
<b>Звіт до розрахунково-графічної роботи</b><br/>
дисципліни "Вступ до функціонального програмування"
</p>

<p align="right"> 
<b>Студент</b>: 
Червоноокий Дмитро</p>

<p align="right"><b>Рік</b>: 2025</p>

## Загальне завдання
1. Реалізувати програму для обчислення функції згідно варіанту мовою Common Lisp. Варіант обирається згідно списку варіантів для лабораторних робіт за модулем 16: 1 -> 1, 2 -> 2, ..., 17 -> 1, 18 -> 2 і т.д.
2. Виконати тестування реалізованої програми.
3. Порівняти результати роботи програми мовою Common Lisp с розрахунками іншими засобами.


## Варіант 2
<p align="center"><img src="https://github.com/ChervonookyiDmytro/FP_RGR/blob/main/Screenshot%202025-12-10%20at%2018.33.27.png"></p>


## Реалізація програми мовою Common Lisp (текст програми).
```lisp
 (defun F (i)
  (labels ((df (x) (coerce x 'double-float)))
    (cond
      ((= i 1) (df 1))
      ((= i 16) (df 2))
      ((and (>= i 2) (<= i 15))
       (let ((prev (F (1- i))))
         (+ (* (df 2) prev) (* (df 5) (sin (df i))))))
      ((and (>= i 17) (<= i 30))
       (let ((prev (F (1- i))))
         (+ (/ prev (df 2)) (* (df 5) (cos (df i))))))
      (t (error "index ~A out of range" i)))))
```
### Реалізація тестових утиліт і тестових наборів (текст програми).
```lisp
(defun float~= (x y &optional (eps 1e-5))
  (< (abs (- x y)) eps))

(defun check-F-algorithm (name i expected)
  (let ((actual (F i)))
    (format t "~:[FAILED~;PASSED~]... ~a  ~%  actual: ~f~%  expected: ~f~%~%"
            (float~= actual expected)
            name
            actual
            expected)))

(defun test-F ()
  (check-F-algorithm "test F(1)" 1 1.00000d0)
  (check-F-algorithm "test F(2)" 2 6.54649d0)
  (check-F-algorithm "test F(3)" 3 13.79857d0)
  (check-F-algorithm "test F(4)" 4 23.81314d0)
  (check-F-algorithm "test F(5)" 5 42.83165d0)
  (check-F-algorithm "test F(6)" 6 84.26622d0)
  (check-F-algorithm "test F(7)" 7 171.81738d0)
  (check-F-algorithm "test F(8)" 8 348.58155d0)
  (check-F-algorithm "test F(9)" 9 699.22370d0)
  (check-F-algorithm "test F(10)" 10 1395.72730d0)
  (check-F-algorithm "test F(11)" 11 2786.45464d0)
  (check-F-algorithm "test F(12)" 12 5570.22642d0)
  (check-F-algorithm "test F(13)" 13 11142.55368d0)
  (check-F-algorithm "test F(14)" 14 22290.06040d0)
  (check-F-algorithm "test F(15)" 15 44583.37224d0)
  (check-F-algorithm "test F(16)" 16 2.00000d0)
  (check-F-algorithm "test F(17)" 17 -0.37582d0)
  (check-F-algorithm "test F(18)" 18 3.11368d0)
  (check-F-algorithm "test F(19)" 19 6.50036d0)
  (check-F-algorithm "test F(20)" 20 5.29059d0)
  (check-F-algorithm "test F(21)" 21 -0.09335d0)
  (check-F-algorithm "test F(22)" 22 -5.04648d0)
  (check-F-algorithm "test F(23)" 23 -5.18740d0)
  (check-F-algorithm "test F(24)" 24 -0.47281d0)
  (check-F-algorithm "test F(25)" 25 4.71961d0)
  (check-F-algorithm "test F(26)" 26 5.59440d0)
  (check-F-algorithm "test F(27)" 27 1.33651d0)
  (check-F-algorithm "test F(28)" 28 -4.14478d0)
  (check-F-algorithm "test F(29)" 29 -5.81268d0)
  (check-F-algorithm "test F(30)" 30 -2.13508d0))

```
### Результати тестування програми.
```lisp
 (test-f)
PASSED... test F(1)  
  actual: 1.0
  expected: 1.0

PASSED... test F(2)  
  actual: 6.546487134128409
  expected: 6.54649

PASSED... test F(3)  
  actual: 13.798574308556153
  expected: 13.79857

PASSED... test F(4)  
  actual: 23.813136140572666
  expected: 23.81314

PASSED... test F(5)  
  actual: 42.83165090782964
  expected: 42.83165

PASSED... test F(6)  
  actual: 84.26622432466465
  expected: 84.26622

PASSED... test F(7)  
  actual: 171.81738164292324
  expected: 171.81738

PASSED... test F(8)  
  actual: 348.5815545189634
  expected: 348.58155

PASSED... test F(9)  
  actual: 699.2237014641356
  expected: 699.2237

PASSED... test F(10)  
  actual: 1395.7272973738243
  expected: 1395.7273

PASSED... test F(11)  
  actual: 2786.454643714895
  expected: 2786.45464

PASSED... test F(12)  
  actual: 5570.226422839788
  expected: 5570.22642

PASSED... test F(13)  
  actual: 11142.55368086371
  expected: 11142.55368

PASSED... test F(14)  
  actual: 22290.060398505895
  expected: 22290.0604

PASSED... test F(15)  
  actual: 44583.37223621258
  expected: 44583.37224

PASSED... test F(16)  
  actual: 2.0
  expected: 2.0

PASSED... test F(17)  
  actual: -0.3758166902579847
  expected: -0.37582

PASSED... test F(18)  
  actual: 3.1136751960914086
  expected: 3.11368

PASSED... test F(19)  
  actual: 6.50036068897905
  expected: 6.50036

PASSED... test F(20)  
  actual: 5.290590653556485
  expected: 5.29059

PASSED... test F(21)  
  actual: -0.09335097434309914
  expected: -0.09335

PASSED... test F(22)  
  actual: -5.046479619144735
  expected: -5.04648

PASSED... test F(23)  
  actual: -5.187404911239355
  expected: -5.1874

PASSED... test F(24)  
  actual: -0.4728074189346927
  expected: -0.47281

PASSED... test F(25)  
  actual: 4.719610349850021
  expected: 4.71961

PASSED... test F(26)  
  actual: 5.594401786568213
  expected: 5.5944

PASSED... test F(27)  
  actual: 1.3365068496149255
  expected: 1.33651

PASSED... test F(28)  
  actual: -4.14477590676037
  expected: -4.14478

PASSED... test F(29)  
  actual: -5.8126756018251875
  expected: -5.81268

PASSED... test F(30)  
  actual: -2.1350805514746733
  expected: -2.13508

NIL
```
## Порівняння результатів з обчисленням іншими програмними засобами або за допомогою калькулятора.
```lisp

```




