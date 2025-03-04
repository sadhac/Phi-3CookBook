Этот демонстрационный пример показывает, как использовать предварительно обученную модель для генерации кода на Python на основе изображения и текстового запроса.

[Пример кода](../../../../../../code/06.E2E/E2E_OpenVino_Phi3-vision.ipynb)

Вот пошаговое объяснение:

1. **Импорты и настройка**:
   - Импортируются необходимые библиотеки и модули, включая `requests`, `PIL` для обработки изображений и `transformers` для работы с моделью и обработки данных.

2. **Загрузка и отображение изображения**:
   - Файл изображения (`demo.png`) открывается с помощью библиотеки `PIL` и отображается.

3. **Определение запроса**:
   - Создается сообщение, включающее изображение и запрос на генерацию кода на Python для обработки изображения и его сохранения с использованием `plt` (matplotlib).

4. **Загрузка процессора**:
   - `AutoProcessor` загружается из предварительно обученной модели, расположенной в каталоге `out_dir`. Этот процессор будет обрабатывать текстовые и графические входные данные.

5. **Создание запроса**:
   - Метод `apply_chat_template` используется для форматирования сообщения в запрос, подходящий для модели.

6. **Обработка входных данных**:
   - Запрос и изображение преобразуются в тензоры, которые модель может понять.

7. **Установка параметров генерации**:
   - Определяются параметры для процесса генерации модели, включая максимальное количество новых токенов и выбор, использовать ли семплирование вывода.

8. **Генерация кода**:
   - Модель генерирует код на Python на основе входных данных и параметров генерации. `TextStreamer` используется для обработки вывода, пропуская запрос и специальные токены.

9. **Вывод**:
   - Генерируемый код выводится на экран. Он должен включать код на Python для обработки изображения и его сохранения, как указано в запросе.

Этот демонстрационный пример иллюстрирует, как использовать предварительно обученную модель с помощью OpenVino для динамической генерации кода на основе пользовательского ввода и изображений.

**Отказ от ответственности**:  
Данный документ был переведен с использованием автоматизированных сервисов перевода на основе ИИ. Хотя мы стремимся к точности, пожалуйста, учитывайте, что автоматические переводы могут содержать ошибки или неточности. Оригинальный документ на его исходном языке следует считать авторитетным источником. Для получения критически важной информации рекомендуется обратиться к профессиональному переводу, выполненному человеком. Мы не несем ответственности за любые недоразумения или неправильные интерпретации, возникшие в результате использования данного перевода.