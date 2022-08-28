Эмулятор учебных машин УМ-1, УМ-2, УМ-3, УМ-С.
Сделаны [по лекциям](https://github.com/xakep71k/machines/blob/master/docs/%D0%91%D0%B0%D1%83%D0%BB%D0%B0%20%D0%92.%D0%93.%20-%20%D0%92%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5%20%D0%B2%20%D0%B0%D1%80%D1%85%D0%B8%D1%82%D0%B5%D0%BA%D1%82%D1%83%D1%80%D1%83%20%D0%AD%D0%92%D0%9C%20(2003).pdf) Баулы Владимира Георгиевича. И по [лекциям](https://www.youtube.com/playlist?list=PLASVL3c0TE-IrOZbXAr8yV9ngrMffSdSV) Бордаченковой Елены Анатольевны<br/>
Машины имеют длину машинного слова 64 бита (разряда)<br/>

### УМ-3 - трёхадресная учебная машина. Команда |<КОП>|\<A1\>|\<A2\>|\<A3\>|, где КОП = 16 бит, A1 = 16 бит, A2 = 16 бит, А3 = 16 бит.<br/>
Поддерживаемые команды, номер в 16ричном формате:<br/>
0000 - пересылка из одной ячейки памяти в другую<br/>
0001 - сложение вещественных чисел<br/>
0002 - вычитание вещественных чисел<br/>
0003 - умножение вещественных чисел (не реализовано)<br/>
0004 - деление вещественных чисел<br/>
0005 - ввод вещественных чисел в память Readf64 (не реализовано)<br/>
0006 - ввод целого числа в память Readi64<br/>
0009 - безусловный переход<br/>
000A - перевод числа из вещественного в целое (не реализовано)<br/>
000B - сложение целых чисел<br/>
000C - вычитание целых чисел<br/>
000D - умножение целых чисел<br/>
000E - деление целых чисел (не реализовано)<br/>
000F - вывод вещественного числа<br/>
0010 - вывод целого числа<br/>
0013 - условный переход<br/>
0014 - перевод числа из целого в вещественное<br/>
001F - стоп<br/>

Пример программы:<br/>
; Вычисление гармонического ряда<br/>
03 ; УМ-3<br/>
0006 0100 0001 0000 ; Readi64(n)<br/>
0002 0101 0101 0101 ; y := 0.0<br/>
0000 0102 000C 0000 ; i := 1<br/>
000C 0000 0102 0100 ; <000> := i - n; формирование w<br/>
0013 0005 0005 000A ; If i > n then goto 00A<br/>
0014 0000 0000 0102 ; <000> := Real(i)<br/>
0004 0000 000D 0000 ; <000> := 1.0/<000><br/>
0001 0101 0101 0000 ; y := y + <000><br/>
000B 0102 0102 000C ; i := i + 1<br/>
0009 0000 0003 0000 ; Следующая итерация цикла<br/>
000F 0101 0001 0000 ; Writef64(y)<br/>
001F 0000 0000 0000 ; Стоп<br/>
0000 0000 0000 0001 ; Целая константа 1<br/>
3FF0 0000 0800 0000 ; Вещественная константа 1.0<br/>


### УМ-2 - двухадресная учебная машина. Команда |<КОП>|\<A1\>|\<A2\>|, где КОП = 16 бит, A1 = 24 бит, A2 = 24 бит.<br/>

Поддерживаемые команды, номер в 16ричном формате:<br/>
0000 - пересылка из одной ячейки памяти в другую<br/>
0001 - сложение вещественных чисел<br/>
0002 - вычитание вещественных чисел<br/>
0003 - умножение вещественных чисел (не реализовано)<br/>
0004 - деление вещественных чисел<br/>
0005 - ввод вещественных чисел в память Readf64 (не реализовано)<br/>
0006 - ввод целого числа в память Readi64<br/>
0009 - безусловный переход<br/>
000A - перевод числа из вещественного в целое (не реализовано)<br/>
000B - сложение целых чисел<br/>
000C - вычитание целых чисел<br/>
000D - умножение целых чисел<br/>
000E - деление целых чисел (не реализовано)<br/>
000F - вывод вещественного числа<br/>
0010 - вывод целого числа (не реализовано)<br/>
0015 - условный переход "больше"<br/>
0016 - условный переход "меньше"<br/>
0017 - условный переход "равно"<br/>
001F - стоп<br/>

Пример:<br/>
; Вычисление гармонического ряда<br/>
02 ; УМ-2<br/>
0006 000100 000001 ; Readi64(n)<br/>
0002 000101 000101 ; y := 0.0<br/>
0000 000102 000010 ; i := 1<br/>
0000 000000 000102 ; <000> := i<br/>
000C 000000 000100 ; <000> := <000> - n; формирование w<br/>
0015 00000E 000000 ; if i > n then go to 00D<br/>
0016 000008 000000 ; if i < n then go to 008<br/>
0017 000008 000000 ; if i = n then go to 008<br/>
0014 000001 000102 ; <001> := Real(i)<br/>
0000 000000 000011 ; <000> := 1.0<br/>
0004 000000 000001 ; <000> := <000>/<001><br/>
0001 000101 000000 ; y := y + <000><br/>
000B 000102 000010 ; i := i + 1<br/>
0009 000000 000003 ; Следующая итерация цикла<br/>
000F 000101 000001 ; Writef64(y)<br/>
001F 000000 000000 ; Стоп<br/>
0000 000000 000001 ; Целая константа 1<br/>
3FF0 000008 000000 ; Вещественная константа 1.0<br/>
<br/>

### УМ-1 - одноадресная учебная машина. Команда |<КОП>|\<A1\>|, где КОП = 16 бит, A1 = 48 бит.<br/>

Поддерживаемые команды, номер в 16ричном формате:<br/>
0000 - пересылка из одной ячейки памяти в S<br/>
0001 - сложение вещественных чисел<br/>
0002 - вычитание вещественных чисел<br/>
0003 - умножение вещественных чисел (не реализовано)<br/>
0004 - деление вещественных чисел<br/>
0005 - ввод вещественных чисел в память Readf64 (не реализовано)<br/>
0006 - ввод целого числа в память Readi64<br/>
0009 - безусловный переход<br/>
000A - перевод числа из вещественного в целое (не реализовано)<br/>
000B - сложение целых чисел<br/>
000C - вычитание целых чисел<br/>
000D - умножение целых чисел<br/>
000E - деление целых чисел (не реализовано)<br/>
000F - вывод вещественного числа<br/>
0010 - вывод целого числа (не реализовано)<br/>
0015 - условный переход "больше"<br/>
0016 - условный переход "меньше"<br/>
0017 - условный переход "равно"<br/>
0018 - пересылка из S в ячейку памяти<br/>
001F - стоп<br/>

Пример:<br/>
; Вычисление гармонического ряда<br/>
01 ; УМ-1<br/>
0000 000000 000018 ; положили 1 в S<br/>
0006 000000 000100 ; Readi64(n)<br/>
0000 000000 000000 ; положили <000> в S<br/>
0018 000000 000101 ; положили из S в y<br/>
0002 000000 000101 ; S := 0.0 ; вычли и получили 0.0<br/>
0018 000000 000101 ; положили из S в y<br/>
0000 000000 000018 ; положили 1 в S<br/>
0018 000000 000102 ; положили из S в i<br/>
0000 000000 000102 ; положили i в S<br/>
000C 000000 000100 ; S := S - n; формирование w<br/>
0015 000000 000018 ; if i > n then go to 018<br/>
0014 000000 000102 ; S := Real(i)<br/>
0018 000000 000000 ; положили из S в <000><br/>
0000 000000 000019 ; положили 1.0 в S<br/>
0004 000000 000000 ; S := S/<000><br/>
0001 000000 000101 ; S := S + y<br/>
0018 000000 000101 ; положили из S в y<br/>
0000 000000 000102 ; положили i в S<br/>
000B 000000 000018 ; S := S + 1<br/>
0018 000000 000102 ; положили из S в i<br/>
0009 000000 000007 ; Следующая итерация цикла<br/>
0000 000000 000018 ; положили 1 в S<br/>
000F 000000 000101 ; Writef64(y)<br/>
001F 000000 000000 ; Стоп<br/>
0000 000000 000001 ; Целая константа 1<br/>
3FF0 000008 000000 ; Вещественная константа 1.0<br/>
<br/>

### УМ-С - стековая учебная машина. Команда |<КОП>|\<A1\>|, где КОП = 16 бит, A1 = 48 бит.<br/>

Поддерживаемые команды, номер в 16ричном формате:<br/>
0000 - положить в стек из ячейки памяти<br/>
0001 - сложение вещественных чисел<br/>
0002 - вычитание вещественных чисел<br/>
0003 - умножение вещественных чисел (не реализовано)<br/>
0004 - деление вещественных чисел<br/>
0005 - ввод вещественных чисел в память Readf64 (не реализовано)<br/>
0006 - ввод целого числа в память Readi64<br/>
0009 - безусловный переход<br/>
000A - перевод числа из вещественного в целое (не реализовано)<br/>
000B - сложение целых чисел<br/>
000C - вычитание целых чисел<br/>
000D - умножение целых чисел<br/>
000E - деление целых чисел (не реализовано)<br/>
000F - вывод вещественного числа<br/>
0010 - вывод целого числа (не реализовано)<br/>
0015 - условный переход "больше"<br/>
0016 - условный переход "меньше"<br/>
0017 - условный переход "равно"<br/>
0018 - пересылка из вершины стека в ячейку памяти<br/>
0019 - дублирования значения находящимся на вершине стека<br/>
001A - удаление из стека<br/>
001F - стоп<br/>

Пример:<br/>
; Вычисление гармонического ряда<br/>
00 ; УМ-С<br/>
0000 00000000001E ; положим константу 1<br/>
0006 000000000001 ; Readi64(n)<br/>
0018 000000000100 ; положим в переменную n<br/>
0000 000000000000 ; положим в стек любое значение, например, по адресу 0<br/>
0019 000000000000 ; продублируем это значение<br/>
0002 000000000000 ; вычтим одно из другого<br/>
0018 000000000101 ; положим результат в y<br/>
0000 00000000001E ; положим константу 1<br/>
0018 000000000102 ; положим результат в i<br/>
0000 000000000100 ; положим n в стек<br/>
0000 000000000102 ; положим i в стек<br/>
000C 000000000000 ; i - n - формирование флагов<br/>
001A 000000000000 ; удалим из стека результат<br/>
0015 00000000001A ; i > n прыгаем на вывод числа y<br/>
0000 000000000102 ; положим в стек i<br/>
0014 000000000000 ; Real(i)<br/>
0000 00000000001F ; положим константу 1.0<br/>
0004 000000000000 ; 1.0 / Real(i)<br/>
0000 000000000101 ; положим y в стек<br/>
0001 000000000000 ; y + 1.0 / Real(i)<br/>
0018 000000000101 ; положим из стека в y<br/>
0000 00000000001E ; положим константу 1<br/>
0000 000000000102 ; положим i в стек<br/>
000B 000000000000 ; i := i + 1<br/>
0018 000000000102 ; положим из стека в i<br/>
0009 000000000009 ; следующая итерация цикла<br/>
0000 000000000101 ; положим y в стек<br/>
0000 00000000001E ; положим константу 1<br/>
000F 000000000001 ; Writef64(y)<br/>
001F 000000000000 ; Стоп<br/>
0000 000000000001 ; Целая константа 1<br/>
3FF0 000008000000 ; Вещественная константа 1.0<br/>
