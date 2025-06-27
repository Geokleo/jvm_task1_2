# Исследование JVM через VisualVM
#

Графики Class и Metaspace можно рассмотреть совместно:

- 0 - Загрузка главного класса и появление в консоли надписи "Please open 'ru.netology.JvmExperience' in VisualVm"
- 1 - Увеличение Metaspace загрузкой новых метаданных об объектах класса io.vertx. Появление в консоли "loading io.vertx" и, далее, на пике "loaded 529 classes".
- 2 - Загрузка новых классов "loading io.netty" - на пике "loaded 2117 classes".
- 3 - Опять загрузка классов "loading org.springframework" - "loaded 869 classes".
- 4 - Появление в консоли "now see heap" и загрузка метаданных новых объектов (SimpleObject).
 #

График Heap:

- 0 - При запуске программы Java выделила памяти в соответствии с параметрами запуска. И через некоторое время GC очистил память.
- 1 - Первый скачок. Появление надписи "now see heap", затем "creating 5000000 objects" и загрузка первых 5000000 объектов методом createSimpleObjects. По окончании пика получаем строку "created".
- 2 - Второй скачок. К уже 5 миллионам добавляется еще столько же. В консоль опять выводятся: "creating 5000000 objects" и в конце пика - "created".
- 3 - Третий скачок. Всё то же самое - плюс ещё пять миллионов объектов.

![](\img\visualvmscreen.png "VisualVM Screen")
