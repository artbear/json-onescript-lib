1С:JSON. JavaScript Object Notation парсер и сериализатор.

==================

 Особенности:
	Парсер и сериализатор поддерживают два режима (формата) работы:
		- Стандартный – полная поддержка стандарта JSON (подробнее см. <http:www.JSON.org/> и 
		  <http:www.ietf.org/rfc/rfc4627.txt?number=4627>);
		- Альтернативный – направлен на применение в проектах подразумевающих постоянный двусторонний
		  обмен данными, по каналам связи Интернет, и требующих повышенную скорость обработки данных,
		  минимизацию пересылаемых пакетов данных и однозначную идентификацию ссылочных типов во входящих данных.

	Независимо от режима работы сериализатор, по требованию (см. Настройки), позволяет автоматически передавать 
	не только уникальный идентификатор ссылки, но и ее представление, а парсер в свою очередь, 
	анализируя входные данные, опускает представления ссылок, не включая их в результирующий набор данных.

	При работе с проектами, в исходящих строковых данных которых не гарантируется отсутствие символов из диапазонов:
		[0x007f, 0x009f], 0x00ad, [0x0600, 0x0604], 0x070f, [0x17b4, 0x17b5], 
		[0x200c, 0x200f], [0x2028, 0x202f] [0x2060, 0x206f], 0xfeff, [0xfff0, 0xffff], 
	рекомендуется не отключать настройку (см. Настройки) полного маскирования символов 
	(подробнее см. <https:github.com/douglascrockford/JSON-js/blob/master/json2.js> и <http:sadesign.ru/tools/unicode>).

	Независимо от режима работы сериализатор, по требованию (см. Настройки), может маскировать кириллические символы 
	современных алфавитов славянских языков "АБВГҐДЂЃЕЀЁЄЖЗЅИЍІЇЙЈКЛЉМНЊОПРСТЋЌУЎФХЦЧЏШЩЪЫЬЭЮЯ" (включая нижний регистр) 
	(подробнее см. <http:ru.wikipedia.org/wiki/Кириллица> и <http:ru.wikipedia.org/wiki/Кириллица_в_Юникоде>).

	Поддерживаются все среды исполнения с ограничением сериализуемых типов. Используется кроссплатформенный код.



 История изменения:
	Версия 2.0.0.17:
		- (Новое) Маскирование кириллических символов современных алфавитов славянских языков (по требованию);
		- (Новое) Поддержка сериализатором типов: ДвоичныеДанные, Картинка, ХранилищеЗначения;
		- (Изменение) Рефакторинг переменных и процедур;
		- (Исправление) Сериализация типа COMSafeArray;
		- (Исправление) Удалены лишние ключевые слова "Экспорт".
		- (Оптимизация) Уменьшение проверок связанных с режимом и параметрами парсинга и сериализцаии;
		- (Оптимизация) Проверка необходимости анализа форматирования вынесена из процедуры анализа форматирования;
		- (Оптимизация) Изменен алгоритм автоматического приведение объекта к структуре или соответствию в зависимости от имен свойств;
		- (Оптимизация) Отказ от явного приведения типов в пользу неявного в операторах условий;
		- (Оптимизация) Отказ от оператора "Попытка Исключение" при преобразовании строки к уникальному идентификатору;
		- (Оптимизация) Изменен порядок проверки типов при парсинге.
	Версия 2.0.0.15
		- Релиз.



 Методы:
	ПрочитатьJSON – парсер;
	ЗаписатьJSON – сериализатор.

 Настройки и параметры:

	Параметры функций:
		Стандарт – определяет режим работы парсера и сериализатора:
			- Истина		– стандартный режим (значение по умолчанию);
			- Ложь			– альтернативный режим;
			- Неопределено	– автоматическое определение режима входящих данных
							  (только парсер, не рекомендуется – влияет на производительность).

		ПредставленияСсылок – позволяет автоматически передавать не только значение ссылки, но и ее представление:
			- Истина		- ссылка парсится и сериализуется как объект с двумя свойствами "Ссылка" и "Представление";
			- Ложь			- ссылка парсится и сериализуется как уникальный идентификатор ссылки (значение по умолчанию);
			- Неопределено	– автоматическое определение формата ссылок во входящих данных
							  (только парсер, не рекомендуется – влияет на производительность).

	Настройки:
		АвтоматическоеПриведениеОбъектаКСтруктуре – автоматическое приведение объекта к структуре, а не к соответствию.
			Настройка изменяется в функции "АвтоматическоеПриведениеОбъектаКСтруктуре" (по умолчанию отключена).
			Автоматическое приведение к структуре выполняется только для объектов имена свойств, которых могут быть 
			использованы как ключи структуры, все остальные объекты преобразуются в соответствие.

		ПолноеМаскированиеСимволов – маскирование символов некорректно обрабатываемых JavaScript-ом.
			Настройка изменяется в функции "НастройкаПолноеМаскированиеСимволов" (по умолчанию включена).
			Не рекомендуется к использованию, так как влияет на производительность, но гарантирует безопасную передачу данных.
			Маскирование специальных символов из диапазона [0x0000, 0x001f] выполняется в не зависимости от настройки.

		МаскированиеКириллицы – маскирование кириллических символов современных алфавитов славянских языков.
			Настройка изменяется в функции "НастройкаМаскированиеКириллицы" (по умолчанию отключена).
			Не рекомендуется к использованию, так как влияет на производительность.
			Маскирование специальных символов из диапазона [0x0000, 0x001f] выполняется в не зависимости от настройки.

		НеявноеПриведениеПримитивныхЗначенийКлюча – неявное приведение примитивных значений ключей соответствий к строке.
			Настройка изменяется в функции "НеявноеПриведениеПримитивныхЗначенийКлюча" (по умолчанию отключена).


 Альтернативный режим:
		- Не поддерживается форматирование, как во входящих, так и в исходящих данных;
		- Сериализация ссылочных типов в строковое служебное представление.


 Приятности:
	Парсер:
		- Устойчивость к некорректным данным и не подверженность injection атакам;
		- Продвинутый синтаксический анализатор (указывает место и тип ошибки в данных);
		- Поддержка форматирования во входящих данных (только стандартный режим);
		- Безопасный разбор форматирования - незамаскированные символы форматирования в строковых значениях не будут утеряны;
		- Поддержка строк в одинарных и в двойных кавычках;
		- Автоматическое приведение объекта к структуре или соответствию в зависимости от имен свойств¹;
		- Автоматическое преобразование к типу Дата строки вида "9999-99-99T99:99:99Z";
		- Автоматическое преобразование к типу УникальныйИдентификатор строки вида "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX";
		- Автоматического определение режима (стандартного или альтернативного) входящих данных;
		- Автоматического определение необходимости отсечения представления ссылок;
		- Однозначная идентификация ссылок (только альтернативный режим).
	Сериализатор:
		- Поддержка форматирования исходящих данных (только стандартный режим);
		- Широкий состав сериализуемых типов данных, в том числе ссылок;
		- Автоматическое приведение значений ключей соответствий к строковому представлению в формате 1С²;
		- Автоматическое преобразование неподдерживаемых типов к строке;
		- Маскирование кириллических символов современных алфавитов славянских языков;
		- Нечувствительность к локализации³.
 ----
  ¹ Если все имена свойства входящего объекта могут быть использованы как ключи структуры, 
    то такой объект будет автоматически приведен к структуре, а не к соответствию. Управляется настройкой.
  ² Управляется настройкой.
  ³ При сериализации некоторых типов, исходящие объекты которых имеют обязательные свойства, 
    такие представления и имена таких свойств всегда имеют русскую локализацию.


 Неприятности:
		- Нестандартно форматированный код (Alt+Shift+F в помощь) на гране читаемости; 
		- Сериализатор ориентирован, на средние-крупные пакеты данных.

 Сериализуемые типы:
	Сервер, толстый клиент, тонкий клиент, веб-клиент:
		- Неопределено;
		- Null;
		- Примитивные типы (все);
		- Универсальные коллекции значений (клиентские);
		- УникальныйИдентификатор;
		- ДвоичныеДанные;
		- Картинка.
	Сервер, толстый клиент:
		- Универсальные коллекции значений (серверные);
		- ЛюбаяСсылка;
		- Запрос;
		- РезультатЗапроса;
		- ВыборкаИзРезультатаЗапроса;
		- ПостроительЗапроса;
		- ПостроительОтчета;
		- ХранилищеЗначения.
	Сервер:
		- ДанныеФормыКоллекция;
		- ДанныеФормыСтруктураСКоллекцией;
		- ДанныеФормыДерево.

 Порядок сериализации типов:
		- Неопределено - сериализуется как Null;
		- Null - согласно стандарту;
		- Примитивные типы - согласно стандарту;
		- Массивы и COMSafeArray - массив, согласно стандарту:
				[ Значение, ... ]

		- Структуры и соответствия – объект, согласно стандарту;
				{ Ключ:Значение, ... }

		- СписокЗначений - массив объектов с тремя свойствами "Значение", "Представление" и "Пометка";
				[ { "Значение":Значение, "Представление":Представление, "Пометка":Пометка }, ... ]

		- КлючИЗначение - объект с двумя свойствами "Ключ" и "Значени";
				{ "Ключ":Ключ, "Значение":Значение }

		- ТаблицаЗначений - массив объектов: 
				[ { Колонка:Значение, ... }, ... ]

		- ДеревоЗначений - массив объектов с обязательным свойством "Строки":
				[ { Колонка:Значение, ... , "Строки":[ { Колонка:Значение, ... , "Строки":[ ... ] } , ... ] }, ... ]

		- УникальныйИдентификатор - приведение к строке вида "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX";

		- ЛюбаяСсылка:
			- Стандартный режим - получение уникального идентификатора ссылки (в том числе и для перечислений) и его сериализация;
			- Альтернативный режим - приведение к строке служебного вида "¦ref¦ ... ¦";

		  При сериализации ссылок в режиме автоматически передачи не только сериализованного значения ссылки, 
		  но и ее представления. Каждая ссылка передается как объект с двумя свойствами "Ссылка" и "Представление";
				{ "Ссылка":Ссылка, "Представление":Представление }

		- Запрос - автоматически выполняется и сериализуется как таблица значений;
		- РезультатЗапроса - сериализуется как таблица значений;
		- ВыборкаИзРезультатаЗапроса - сериализуется как структура значений текущей запись результата запроса;
		- ПостроительЗапроса - автоматически выполняется и сериализуется как таблица значений;
		- ПостроительОтчета - автоматически выполняется и сериализуется как таблица значений;
		- ДанныеФормыКоллекция - сериализуется как таблица значений;
		- ДанныеФормыСтруктураСКоллекцией - сериализуется как таблица значений;
		- ДанныеФормыДерево - сериализуется как дерево значений;
		- ДвоичныеДанные - кодируется по алгоритму base64¹ и сериализуется как строка;
		- Картинка - автоматически преобразуется и сериализуется как двоичные данные;
		- ХранилищеЗначения - автоматически извлекается сохраненное значение и сериализуется в зависимости от типа извлеченного значения.
 ----
  ¹ Следуя рекомендациям стандарта, сериализатор при кодировании по алгоритму base64, не добавляет переводы строк 
    в результирующие данные (подробнее см. <http:tools.ietf.org/html/rfc4648#section-3.1>).

 Производительность:
	Производительность парсера исключительно зависит от набора входящих данных, а также от наличия форматирования.
	Наихудшим вариантом является форматированный массив чисел, наилучшим - неформатированный массив строк.

	Intel Core 2 Duo T5870 @ 2GHz - форматированный массив со всеми приблизительно равномерно встречающимися типами данных:
		Парсер:			35 Кбайт/с.
		Сериализатор:	165 Кбайт/с.

 Примечание:
	Мало комментариев - без комментариев.

 Всем удачного программирования :)
 
 

