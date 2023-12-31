## Исходный датасет

https://drive.google.com/drive/folders/1rA0LTCh0Oj_XEqGg6QgJRCEuGlUAzqId

Содержит тренировочные данные, используемые в данном проекте и тестовые из kaggle соревнования.


## Промежуточные версии обработанных датасетов

https://drive.google.com/drive/folders/1zZ7emxeENIXS-AAc2BXkcYhTmkcXVM3-

* merge_df - файл с объединенными train_transaction и train_identity (методом left)
* merged_drop_highly_miss_fillednan - объединенный файл с удаленнием признаков, содержищих большое число пропусков (более 90%), пропущенные значения заменены на медианы и 'missing'
* merged_without_drop_fillednan - объединенный файл с заполненными пропусками тем же способом



# Описание выбранного датасета

Данные поделены на таблицы transaction и identity и содержат 590 540 транзакций, доля которых является мошенническими. Из всех транзакций только 20 663 являются незаконными, то есть на положительный класс 
(мошенничество) приходится примерно 3.5%, из чего следует, что набор данных сильно несбалансирован.

Таблица transaction содержит 394 признака:

* isFraud: категориальный признак, определяющий транзакцию как мошеннеческую (isFraud=1) или законную (isFraud=0). 
  
  Транзакция считается мошенической если владелец карты в течение 120 дней с момента совершения транзакции сообщил о мошеннических действиях. 
  Также все последудующие транзакции связанные с учетной записью данного пользователя, адресом электронной почты или платежным адресом, определяются как мошенничество. 
  В противном случае транзакция определяется как законная (isFraud=0).
  
  Однако в реальном мире о мошенничестве может не сообщаться, например, если владелец карты не заметил этого, забыл сообщить вовремя или сообщил по истечению срока предъявления претензии и т.д. 
  В таких случаях предполагаемое мошенничество может быть помечено как законная транзакция.
  Мы будем считать, что такие случаи необычны и их доля незначительна.

* TransactionDT: timedelta (разница между двумя моментами времени) от заданной эталонной даты и времени. 
  
  Первое значение TransactionDT равно 86400, что соответствует количеству секунд в сутках (60 * 60 * 24 = 86400), используя это,
  можно сказать, что данные охватывают 6 месяцев, так как максимальное значение равно 15811131, что соответствует 183 дню.

* TransactionAMT: сумма платежа по транзакции в долларах США 
  
  (Некоторые суммы транзакций с тремя знаками после точки могут являться результатом перевода иностранной 
  суммы в доллары по обменному курсу)

* ProductCD: код продукта для каждой транзакции (в т.ч. услуги) - категориальный признак, 
  принимающий одно из значений: W', 'H', 'C', 'S', 'R'.

* card1 - card6: категориальный признак - информация о платежной карте, такая как тип карты, категория карты, 
  банк-эмитент, страна и т.д. Фактический смысл скрыт.

* addr: категориальный признак, представленный в числовом виде - адрес покупателя:
  * addr1: регион выставления счетов
  * addr2: страна выставления счетов

* dist: расстояние между адресом выставления счетов, почтовым адресом, почтовым индексом, IP-адресом, областью телефона и т.д.

* P_ и (R__) emaildomain: категориальные признаки - домен электронной почты покупателя и получателя 
  (некоторым транзакциям не нужен получатель, поэтому R_emaildomain равен null).

* C1-C14: различные подсчеты, например, количество адресов, связанных с платежной картой, и т.д. Фактический смысл замаскирован.

* D1-D15: timedelta, например количество дней между предыдущей транзакцией и т. д. Фактический смысл скрыт.

* M1-M9: категориальные признаки - совпадения, например, имена на карточке, адрес и т. д. Фактический смысл скрыт.

* V1 - V339: различные функции, разработанные компанией по безопасности Vesta. Все характеристики Vesta были выведены в числовом виде. Фактический смысл замаскирован.


Таблица identity, содержит 41 признак:

Переменные в таблице представляют идентификационную информацию, такую как информация о сетевом подключении (IP, интернет-провайдер, прокси-сервер и т. д.) и цифровая подпись (UA/браузер/ОС/версия и т. д.), связанные с транзакциями.
Их собирает система защиты от мошенничества Vesta и партнеры по цифровой безопасности.

* id01-id38: числовые и категориальные характеристики для идентификации, которые собираются Vesta и партнерами по безопасности. 
  Они включают в себя рейтинг устройства, рейтинг ip_domain, рейтинг прокси, а также поведенческие данные: 
  время входа в учетную запись/время неудачного входа в систему, как долго учетная запись оставалась на странице и т.д. 
  Все они замаскированы ввиду соглашения о безопасности.

* DeviceType: категориальный признак - тип устройства, принимает одно из значений: 'mobile' или 'desktop'.

* DeviceInfo: категориальный признак - информация об устройстве, с которого совершена транзакция.

------------------------------

Различные признаки содержат различное число пропусков от 0 до 508189.
