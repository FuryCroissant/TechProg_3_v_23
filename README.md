# Game3
Требуется разработать приложение или программный комплекс,обменивающийся данными по сети в формате JSON, XML или Protocol Buffers.

Добавьте в свой предыдущий проект возможность сохранения состояния в виде периодического сохранения, либо в виде функций
импорта и экспорта. Выбранный формат для сериализации должен иметь схему. В проекте обязателен код валидирующий данные.
Валидация должна производиться либо в программе при импорте данных, либо в юнит-тестах, проверяющих корректность
сохранения состояния.

Вариант 23

Сетевая игра «Запомнить последовательность» для двух игроков.Один игрок выставляет последовательность пяти цветных шариков, а другой игрок должен запомнить 
последовательность и воспроизвести через пять секунд. Каждый ход игроки меняются ролями. Игрок проигрывает, если воспроизвёл последовательность неправильно.

## -------------- 
Для запуска игры в свойствах Solution файла указаны несколько стартовых проектов (первым запускается Server, вторым Client).

Сохраненное состояние игры хранится в файле `GameState.json`, который расположен относительно корневой папки проекта
в "/Server/bin/Debug/net6.0".**

Для генерации и валидации схемы используются объекты из NuGet пакета `NJsonSchema`. Генерация происходит на основании
класса `GameState`, в котором также описаны ограничения для схемы на основе встроенных атрибутов библиотеки NJsonSchema.

Сохранение текущего состояния игры происходит дважды за раунд на стороне сервера: в начале раунда и после передачи
загаданной последовательности. В начале игры сервер передает клиенту начальное состояние игры для их синхронизации.
Перед началом игры со стороны сервера можно либо начать игру с исходного состояния, либо загрузить последнее сохраненное
состояние.

Валидация строки загадонной последовательности происходит на основе регулярного выражения "^[rgboypcw]{5}$" , под которое
подпадают строки, содержащие ровно пять символов, все из которых входят в набор, заданный в квадратных скобках.
