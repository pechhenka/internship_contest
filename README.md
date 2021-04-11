# IntelliJ plugin for Lego Mindstorms

## Условия

### Задача 1
Артём слышал, что список фамилий в публикациях сортируют в лексикографическом порядке. Артём очень тщеславен, и пытается придумать, в каком порядке должны идти буквы в алфавите, чтобы его фамилия в публикации стояла первой. Помогите Артёму написать программу которая бы вычисляла такой алфавит, в котором заданный список фамилий был бы лексикографически отсортированным или определяла, что это невозможно.

Программы принимаются на языках Java, Kotlin. В качестве ответа пожалуйста пришлите ссылку на Github с решением.

Вход:
Подается в стандартный ввод. В первой строке записано целое число n (1 ≤ n ≤ 100), количество имен.

В каждой из следующих n строк записано по одному слову name%i , обозначающему i-е имя. Каждое имя содержит только строчные буквы латинского алфавита, не более 100 символов. Все имена различны.

Выход:
Подается в стандартный вывод. Если существует такой порядок букв, при котором имена в данном списке следуют в лексикографическом порядке, выведите любой такой порядок в виде перестановки символов 'a'–'z' (иными словами, выведите сначала первую букву модифицированного алфавита, затем вторую, и так далее).

В противном случае выведите единственное слово «Impossible» (без кавычек).

### Задача 2
У вас есть Java функция в которую пользователь передает текст и регулярное выражение. Измените функцию так, чтобы избежать зависаний и выбрасывания исключений в процессе исполнения.

public boolean matches(String text, String regex) {
return Pattern.compile(regex).matcher(text).matches();
}
Подсказка: вы не хотите вечно ждать пока matches() закончит работу.

В качестве ответа пожалуйста пришлите ссылку на Github с решением.

## Решение
### Задача 1
Создадим ориентированный граф вершинами которого будут маленькие латинские буквы, а ребра будут показывать в каком порядке должны следовать буквы. 

По ходу ввода данных будет производить сравнение строк, попутно добавляя в граф какие сравнения символов в каком порядке потребовались.

Затем проверив граф на ацикличность, произведём топологическую сортировку, тем самым получив новый алфавит.

### Задача 2
Проблема в данной функции, что может произойти Катастрофическое Отступление при определённых regex из-за чего Matcher::matches может уйти в экспоненциальную обработку.

Для предотвращения такого поведения, можно поставить лимит по времени выполнения обработки.