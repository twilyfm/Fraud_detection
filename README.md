# Детектирование аномалий в данных

### Описание проекта: 
Выявление подозрительных транзакций на наборе банковских данных 

### Команда:
- [Демиденко Никита](https://github.com/kalxon)
- [Сидорова Анастасия](https://github.com/twilyfm)
- [Морозов Антон](https://github.com/MAV-r)

## Документация для FastAPI приложения по обработке транзакций
### Введение
Это документация для FastAPI приложения, которое позволяет загрузить данные о транзакциях в формате CSV или Parquet, производить предсказания на основе модели машинного обучения и предоставлять результаты для загрузки.

### Использование
Главная страница
Для доступа к главной странице откройте браузер и перейдите по ссылке http://<your-host>:<your-port>/. На этой странице вы найдете ссылки на другие функциональности.

### Загрузка файлов
Для загрузки файла с данными перейдите на страницу http://<your-host>:<your-port>/upload/. Здесь вы можете выбрать файл для загрузки. Файл должен быть в формате CSV или Parquet. После успешной загрузки файла, он будет доступен для дальнейшей обработки.

### Предсказание для файла
Для выполнения предсказаний на основе данных в загруженном файле, перейдите на страницу http://<your-host>:<your-port>/inference_file. Здесь вы можете выбрать файл, для которого хотите получить предсказания. После выбора файла и нажатия кнопки "Предсказать", результаты будут доступны для загрузки.

### Просмотр загруженных файлов
Вы можете просмотреть список загруженных файлов, перейдя по адресу http://<your-host>:<your-port>/files.

### Удаление файла
Чтобы удалить загруженный файл, перейдите на страницу http://<your-host>:<your-port>/files/{filename}, где {filename} - это имя файла, который вы хотите удалить.

### Важные замечания
Перед началом использования приложения убедитесь, что модель машинного обучения уже загружена на сервер.
Приложение разработано для обработки определенного формата и структуры данных. Убедитесь, что ваши данные соответствуют ожидаемому формату.

### Возможные проблемы
Если вы получаете сообщение об ошибке при загрузке файла, убедитесь, что формат файла корректен и он не поврежден.
Если вы получаете сообщение об ошибке при предсказании, убедитесь, что ваши данные в корректном формате и все необходимые признаки присутствуют.
