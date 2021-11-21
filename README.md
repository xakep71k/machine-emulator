Эмулятор учебных машин УМ-1, УМ-2, УМ-3, УМ-С.
Сделаны [по лекциям](https://github.com/xakep71k/machines/blob/master/docs/%D0%91%D0%B0%D1%83%D0%BB%D0%B0%20%D0%92.%D0%93.%20-%20%D0%92%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5%20%D0%B2%20%D0%B0%D1%80%D1%85%D0%B8%D1%82%D0%B5%D0%BA%D1%82%D1%83%D1%80%D1%83%20%D0%AD%D0%92%D0%9C%20(2003).pdf) Баулы Владимира Георгиевича. И по [лекциям](https://www.youtube.com/playlist?list=PLASVL3c0TE-IrOZbXAr8yV9ngrMffSdSV) Бордаченковой Елены Анатольевны<br/>
Машины имеют длину машинного слова 64 бита (разряда)<br/>

УМ-3 - трёхадресная учебная машина. Команда |<КОП>|\<A1\>|\<A2\>|\<A3\>|, где КОП = 7 бит, A1 = 19 бит, A2 = 19 бит, А3 = 19 бит.<br/>
УМ-2 - двухадресная учебная машина. Команда |<КОП>|\<A1\>|\<A2\>|<выравнивание>|, где КОП = 7 бит, A1 = 28 бит, A2 = 28 бит, +1 бит для выравниваня до 64 битного слова.<br/>
УМ-1 - одноадресная учебная машина. Команда |<КОП>|\<A\>|, где КОП = 7 бит, A = 57 бит.<br/>
УМ-С - безадресная или стековая учебная машина. Комада |<КОП>|<выравнивание>|, КОП = 7 бита, +57 бит до выравнивания 64 битного слова.<br/>
Опции:<br/>
	--help	Справка<br/>
	--clist	Список команд процессора<br/>
	--format Возмжные значения: education|binary. Education - это формат где использется форматирование и команды записаны в десятичной системе счисления, формат текстовый. См. пример ниже. Binary - бинарный формат, состоящий из машиных слов длинной 64 бита, тут используется двоичный бинарный формат little endian. Если формат не указывать, то по умолчанию будет использоваться binary.<br/>
	--machine-type	Возможные значения: UM3|УМ3|УМ-3 или UM2|УМ2|УМ-2 или UM1|УМ1|УМ-1 или UMS|УМС|УМ-С<br/>
<br/><br/>
Пример --format education. В команде параметры КОП|A1|A2|A3 должны разделяться пробелами, а сами команды новой строкой. Можно писать комментарии //.<br/>
Пример программы для УМ-3:<br/>
06 006 001 000 // Ввод x<br/>
06 007 001 000 // Ввод y<br/>
11 008 006 007 // z := x + y<br/>
15 008 001 000 // Вывод z<br/>
31 104 101 009 // стоп<br/>

Программа подаётся на вход через стандартный поток ввода.<br/>
Пример запуска на ОС Linux:<br/>
cat commands.txt | machine --machine-type um3 --format education<br/>
В файле commands.txt лежит листинг программы из пример выше.