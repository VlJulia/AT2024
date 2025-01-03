# Содержание
1. [Введение](#1-введение)
   - [Цели](#цели)
   - [Границы применения](#границы-применения)
   - [Термины и аббревиатуры](#термины-и-аббревиатуры)
   - [Ссылки](#ссылки)
   - [Краткий обзор](#краткий-обзор)
2. [Общее описание](#2-общее-описание)
   - [Описание изделия](#описание-изделия)
   - [Функции изделия](#функции-изделия)
   - [Характеристики пользователей](#характеристики-пользователей)
   - [Ограничения](#ограничения)
   - [Предположения и зависимости](#предположения-и-зависимости)
3. [Детальные требования](#3-детальные-требования)
   - [Функциональные требования](#функциональные-требования)
	-[Приложение для аренды самокатов](#приложение-для-аренды-самокатов) 
	-[Приложение для аренды автомобилей](#приложение-для-аренды-автомобилей) 
   - [Надежность](#надежность)
   - [Производительность](#производительность)
   - [Ремонтопригодность](#ремонтопригодность)
   - [Ограничения проекта](#ограничения-проекта)
   - [Требования к пользовательской документации](#требования-к-пользовательской-документации)
   - [Используемые компоненты](#используемые-компоненты)
   - [Интерфейсы](#интерфейсы)
   - [Требования лицензирования](#требования-лицензирования)
   - [Применимые стандарты](#применимые-стандарты)
4. [Индекс](#индекс)

---

# История изменений
| Дата       | Версия | Описание         | Авторы           |
|------------|--------|------------------|------------------|
| 2024-10-16 | 0.1    | Начальная ревизия |Владимирова Юлия <br/> Страхов Андрей <br/> Чернова Наталья|   
| 2024-11-13 | 0.2    | Работа над третьим разделом |Владимирова Юлия <br/> Страхов Андрей <br/> Чернова Наталья| 
| 2024-11-28 | 0.3    | Добавлены требования к приложению каршеринга |Владимирова Юлия <br/> Страхов Андрей <br/> Чернова Наталья| 
---


# 1. Введение
Данный документ предназначен для описания требований к программному обеспечению для системы контроля проката самокатов и легковых автомобилей.

## Цели
Цель создания документа заключается в чётком определении требований и спецификации к программному обеспечению, а также описание его интерфейса и ограничений. 

## Границы применения
Данный документ распространяется на спецификацию приложений для проката самокатов и легковых автомобилей.
Приложения осуществляют первичную коммуникацию с пользователем услуги аренды, а именно предложение и заключение аренды, расчёт стоимости услуги и осуществление её оплаты по окончании пользования услугой пользователем. Также приложения осуществляют частичный контроль за исполнением условий договора аренды со стороны арендатора, частичный контроль включает в себя время и область использования арендованного транспорта, в случае легковых автомоблей - следования ограничениям скорости. Приложения отслеживают местонахождение и статус всех зарегистрированных в приложении транспотных средств.    

## Термины и аббревиатуры
|||
|-------------|-------------|
|Самокат (электросамокат) | двухколёсное транспортное средство (самокат с электродвигателем), зарегистрированное в собственность компании, имеющее QR код на корпусе, оснащённое системой блокировки колёс и модулем, способным выйти в сотовую сеть, принять и отправить сообщение, в котором сообщает своё текущее местоположение.|
|Автомобиль | легковая машина, зарегистрированная в собственность компании, имеющая QR код на корпусе, оснащённая системой блокировки дверей, способная выйти в сотовую сеть, принять и отправить сообщение, в котором сообщает своё текущее местоположение.|
|ТС | транспортное средство (автомобиль или самокат), зарегистрированное в собственность компании.|
|Штраф                    | сумма, представляющая собой надбавку к итоговой стоимости проката за определённые лёгкие и средние нарушения договора пользования услугой, в т.ч. превышение скорости.|
|ПО                       | программное обеспечение - программа или множество программ, используемых для управления компьютером.|
|API                      | программный интерфейс, с помощью которого приложения, веб-сервисы и программы обмениваются информацией |
|QR-код                   |тип штрих-кода, который хранит информацию в виде набора квадратов и считывается камерой смартфона или специальным сканером.|

## Ссылки
| Обозначение | Расшифровка           |
|-------------|-----------------------|
| [IEEE-830]  | IEEE Std 830-1998     |

## Краткий обзор
Структура документа:
1. Раздел 1 содержит введение, краткий обзор программного обеспечения и некоторые необходимые данные для лучшего понимания документа.
2. Раздел 2 содержит более полное описание продукта.
3. Раздел 3 содержит требования к продукту, описание ожидаемых от него функций и интерфейса в более точном виде, достаточном для понимания квалифицированным работником.
4. Раздел 4 содержит индекс приложения, определения, не указанные в разделе 1, а также другую дополнительную информацию.

---

# 2. Общее описание

## Описание изделия
- **Интерфейсы системы**: Приложение будет взаимодействовать с несколькими компонентами, включая серверную часть, базы данных для хранения информации о пользователях и ТС, а также API для обработки платежей и геолокационных услуг. Основные интерфейсы системы могут включать:
	- API для взаимодействия с модулем ТС.
	- API для обработки заказов и транзакций.
	- Интерфейс для управления данными пользователей и аренд.
	- Геолокационный сервис для работы с картой и ограничениями скорости.
- **Интерфейсы пользователя**: Доступные пользователям интерфейсы будут включать:
	- Интуитивно понятный интерфейс для регистрации пользователя, управления учетной записью и аренды самокатов.
	- Интерфейс для бронирования автомобиля, просмотра карт и получения уведомлений.
    - Интерфейс для загрузки фотографий автомобиля перед и после аренды.
	- Интерфейс администратора, техника по обслуживанию для мониторинга состояния ТС и управления пользовательскими запросами.
- **Интерфейсы аппаратных средств ЭВМ**:не требуется специфическое оборудование, работает на планшетах или мобильных устройствах, с камерой, способное считывать QR-код, с доступом к интернету.
- **Интерфейсы программного обеспечения**: Приложения будут интегрироваться с различными программными системами, включая:
	- Платежные системы для обработки финансовых транзакций.
	- Системы геолокации для визуализации местоположения разрешенных мест стоянки самокатов.
	- Системы геолокации для визуализации местоположения разрешенных мест стоянки автомобилей, зон с ограничениями скорости.
- **Интерфейсы коммуникаций**: В приложениях будут использоваться следующие интерфейсы для связи:
	- Уведомления из самого приложения для осведомления о выгодных предложениях, состоянии батареи транспортного средства и о нарушениях с их последствиями, в случае нарушения условий договора.
	- Электронная почта и сотовая связь для подтверждения действий пользователей или при необходимости оказания дополнительной технической поддержки.
	- Протоколы для передачи данных о местоположении ТС.
- **Ограничения памяти**: Ограничения памяти минимальные.
- **Действия**: Приложения будут поддерживать такие действия, как:
	- Регистрация и аутентификация.
	- Поиск доступных мест стоянки самокатов на карте.
	- Поиск доступных мест стоянки автомобилей на карте и зон с ограничениями скорости.
	- Аренда ТС.
	- Фотографирование автомобиля.
	- Получение уведомлений о статусе аренды и инструкциях по возврату.
	- Оплата аренды через интегрированные платёжные системы.
	- Управление учётной записью.

## Функции изделия
- **Работа с самокатом**: 
	- возможность взять самокат
	- возможность оставить самокат в определённом месте
	- возможность оплатить пользование самокатом.
- **Работа с автомобилем**:
  - бронирование ближайшего доступного автомобиля.
  - фотографирование автомобиля перед началом и завершением аренды.
  - подсчёт стоимости аренды и штрафов за нарушения.
- **Работа с системой**:
	- заведение базы данных с информацией об имеющихся ТС.
	- заведение базы данных с информацией о пользователях.
	- заведение базы данных с информацией об осуществлённых платежах.   
	- заведение базы данных с информацией о зонах с ограничениями скорости.
- **Работа в системе**:
	- отслеживание, где находится ТС
	- отправка запросов на блокировку или разблокировку ТС.
 	- генерация штрафов за превышение скорости в обозначенных зонах.

## Характеристики пользователей
Система ориентирована на два вида пользователей:
1. Техники по обслуживанию - те, кто поддерживает рабочее состояние ТС и его модуля, а также следит за его правильным местоположением стоянки.
2. Системный администратор - обслуживает систему, следит за её корректной работой и функционированием системы. Обладает навыками системного администрирования, имеет техническое образование
3. Пользователи приложения для аренды самокатов старше 18 лет, имеющие возможность безналичной оплаты.
4. Пользователи приложения для аренды автомобилей старше 18 лет, имеющие возможность безналичной оплаты, зарегистрированные в офсие компании.

## Ограничения
Приложение не осуществляет регистрацию и покупку ТС, не предназначено для использования людьми младше 18 лет. Приложение не осуществляет отправку SMS-сообщений на самокат с самого устройства в целях безопасности. Приложение не предоставляет полный функционал при отсутствии интернет соединения. Компания должна иметь квалифицированных рабочих для осуществления регулярного обслуживания самокатов. Заправка автомобилей осуществляется вне системы. Приложение не позволяет выбрать конкретный автомобиль, бронируется ближайший доступный. Пользователи приложения для аренды автомобилей должны быть зарегистрированы заранее в офисе компании.


## Предположения и зависимости
При изменении законодательства касательно использования транспортных средств, возможно изменение системы регистрации пользователей для указания дополнительных данных, таких как наличие прав на управление транспортным средством, и их проверки в государственных информационных системах. Карта зон ограничения скорости всегда актуальна и предоставляется компанией. Данные с устройств GPS передаются корректно и регулярно.

---

# 3. Детальные требования

## Функциональные требования

### Приложение для аренды самокатов 

**Работа с системой**
|Идентификатор|	Наименование	|Содержание|	Важность|
|-------------|-----------------|----------|------------|
|ID01	|Регистрация	|Регистрация пользователей с прикреплением данных платежной системы	|Важно|
|ID02	|Аутентификация|	Аутентификация пользователей	|Важно|
|ID03	|Работа с платёжной системой|	Прикрепление платёжной системы, возможность изменения способа оплаты.|	Важно|
|ID04	|Разблокировка колёс|	Отправка запроса на сервер для предупреждения о необходимости отправить SMS-сообщения на самокат для разблокировки колес.| Важно|
|ID05	|Блокировка колёс|	Завершение поездки с отправкой запроса на сервер для предупреждения о необходимости отправить SMS-сообщение на самокат для блокировки колес.|Важно|
|ID06	|Оплата услуг|	Обеспечение оплаты услуг проката.|	Важно|
|ID07	|Расчёт стоимости услуги	|Расчёт стоимости услуги, исходя из активации устройства, длительности поездки и оплаты страховки.|	Важно|
|ID08	|Назначение штрафов|	Назначение штрафов за порчу используемого самоката или несоблюдение правил контракта по использованию самоката.|	Важно|

**Работа с системным администратором**
|Идентификатор|Наименование	|Содержание|	Важность|
|-------------|-----------------|----------|------------|
|ID09|Работа со справочником пользователей|Осуществление действий со справочником пользователей, таких, как редактирование данных, удаление записей. |Важно|
|ID10|Работа со справочником транспортных средств|Осуществление действий со справочником транспортных средств, таких, как регистрация новых самокатов в системе, удаление.|Важно|
|ID11|Работа со справочником зон парковки|Осуществление действий со справочником зон парковки, таких, как изменение зон, удаление, добавление. |Важно|

**Работа с техником по обслуживанию**
|Идентификатор|Наименование	|Содержание|	Важность|
|-------------|-----------------|----------|------------|
|ID12	|Сканирование QR-кода|	Сканирование QR-кода для осуществления поездки на выбранном самокате, обслуживания его и просмотре информации о нём.|	Важно|
|ID13	|Информация о стоянках|	Отображение карты с текущим местоположением и местами стоянки самокатов.|	Средней важности|
|ID14	|Информация о самокате|	Отображение информации об активированном самокате.|	Средней важности|
|ID15	|Запрос информации	|Отправка запроса на сервер на получение информации о самокатах в определённом радиусе|Важно|
|ID16	|Информация о самокатах|Отображение списка самокатов с указанием их статуса (например, разряжен, сломан, некорректно припаркован)|	Важно|
|ID17	|Обновление статуса|	Обновление статуса самоката|	Важно|

**Работа с пользователем**
|Идентификатор|Наименование	|Содержание|	Важность|
|-------------|-----------------|----------|------------|
|ID18	|Сканирование QR-кода|	Сканирование QR-кода для осуществления поездки на выбранном самокате.|	Важно|
|ID19   |	Информация о поездке|	Отображение информации о текущей поездке.|	Средней важности|
|ID20	|Информация о стоянках|	Отображение карты с текущим местоположением и ближайшими местами стоянки самоката.|	Средней важности|
|ID21	|Информация о самокате|	Отображение информации о арендованном самокате.|	Средней важности|
|ID22	|Отправка уведомлений	|Отправка уведомлений, отображающих текущее состояние поездки (длительность и текущую стоимость), а также рекламные предложение.|	Средней важности|
|ID23	|Обучение	|Обучение правилам пользования услугой.|	Важно|
|ID24	|Запрос информации	|Отправка запроса на сервер на получение информации о самокате|	Средней важности|
|ID25	|Работа с платёжной системой|	Возможность оплаты поездки с помощью привязанной карты|	Важно|

### Приложение для аренды автомобилей

**Работа с системой**
|Идентификатор|	Наименование	|Содержание|	Важность|
|-------|-----------------------------|-----------------------------------------------------------------------------------------------|---------------|
| ID01   | Бронирование автомобиля     | Пользователь может забронировать ближайший доступный автомобиль.                              | Важно         |
| ID02   | Фотографирование автомобиля | Перед началом и завершением аренды пользователь должен загрузить фотографии автомобиля.       | Важно         |
| ID03   | Расчёт стоимости            | Система рассчитывает стоимость аренды на основании времени использования.                     | Важно         |
| ID04   | Штрафы за превышение        | Система автоматически начисляет штрафы за превышение скорости на основе передаваемых данных.  | Важно         |
| ID05   | Отображение зон             | Приложение отображает зоны с ограничениями скорости на карте.                                 | Средней важности |
| ID06   | Уведомления                 | Система отправляет уведомления о завершении бронирования, начислении штрафов и рекламных акций.| Средней важности |
| ID07   | Завершение аренды           | Пользователь завершает аренду через приложение.  

**Работа с системным администратором**
|Идентификатор|Наименование	|Содержание|	Важность|
|-------------|-----------------|----------|------------|
|ID08|Работа со справочником пользователей|Осуществление действий со справочником пользователей, таких, как редактирование данных, удаление записей. |Важно|
|ID09|Работа со справочником транспортных средств|Осуществление действий со справочником транспортных средств, таких, как регистрация новых автомобилей в системе, удаление.|Важно|
|ID10|Работа со справочником зон парковки|Осуществление действий со справочником зон парковки, таких, как изменение зон, удаление, добавление. |Важно|
|ID11|Работа со справочником зон с ограниченим скорости|Осуществление действий со справочником зон с ограничением скорости, таких, как изменение зон, удаление, добавление. |Важно|

**Работа с техником по обслуживанию**
|Идентификатор|Наименование	|Содержание|	Важность|
|-------------|-----------------|----------|------------|
|ID12	|Сканирование QR-кода|	Сканирование QR-кода для осуществления поездки на выбранном автомобиле, обслуживания его и просмотре информации о нём.|	Важно|
|ID13	|Информация о стоянках|	Отображение карты с текущим местоположением и местами стоянки автомобилей.|	Средней важности|
|ID14	|Информация о самокате|	Отображение информации об активированном автомобиле.|	Средней важности|
|ID15	|Запрос информации	|Отправка запроса на сервер на получение информации об автомобилях в определённом радиусе|Важно|
|ID16	|Информация о самокатах|Отображение списка автомобилей с указанием их статуса (например, кончается топливо, сломан, некорректно припаркован)|	Важно|
|ID17	|Обновление статуса|	Обновление статуса автомобиля|	Важно|


**Работа с пользователем**
|Идентификатор|Наименование	|Содержание|	Важность|
|-------------|-----------------|----------|------------|
|ID18	|Сканирование QR-кода|	Сканирование QR-кода для осуществления поездки на выбранном автомобиле.|	Важно|
|ID19|	Информация о поездке|	Отображение информации о текущей поездке.|	Средней важности|
|ID20	|Информация о стоянках|	Отображение карты с текущим местоположением и ближайшими местами стоянки автомобиле.|	Средней важности|
|ID21	|Информация об автомобиле |	Отображение информации об арендованном автомобиле.|	Средней важности|
|ID22	|Отправка уведомлений	|Отправка уведомлений, отображающих текущее состояние поездки (длительность и текущую стоимость), а также рекламные предложение.|	Средней важности|
|ID23	|Обучение	|Обучение правилам пользования услугой.|	Важно|
|ID24	|Запрос информации	|Отправка запроса на сервер на получение информации об автомобиле|	Средней важности|
|ID25	|Работа с платёжной системой|	Возможность оплаты поездки с помощью привязанной карты|	Важно|

---


## Надежность
- **Доступность**: xx.xx%
- **MTBF**: подлежит уточнению.
- **MTTR**: подлежит уточнению.
- **Точность**: подлежит уточнению.
- **Макс. количество ошибок**: подлежит уточнению.

## Производительность
- **Время отклика**: подлежит выяснению.
- **Пропускная способность**: подлежит выяснению.
- **Утилизация ресурсов**: подлежит выяснению.

## Ремонтопригодность
[Требования к ремонтопригодности.]

## Ограничения проекта
[Ограничения по проекту.]

## Требования к пользовательской документации
[Требования к документации.]

## Используемые компоненты
[Перечень приобретаемых компонентов.]

## Интерфейсы
- **Интерфейс пользователя**: подлежит выяснению.
- **Аппаратные интерфейсы**: подлежат выяснению.
- **Программные интерфейсы**: подлежат выяснению.
- **Интерфейсы коммуникаций**: подлежат выяснению.

## Требования лицензирования
[Требования по лицензированию.]

## Применимые стандарты
[Применимые стандарты.]

---

# Индекс
[Индекс.]
