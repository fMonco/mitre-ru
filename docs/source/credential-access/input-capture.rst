



Захват ввода
===========================


Злоумышленники могут использовать методы перехвата пользовательского ввода для получения учетных данных или сбора информации. При обычном использовании системы пользователи часто вводят учетные данные в различных местах, например на страницах/порталах входа в систему или в системных диалоговых окнах. Механизмы перехвата ввода могут быть прозрачными для пользователя или полагаться на то, чтобы обманом заставить пользователя ввести данные в службу, которую он считает подлинной.



Кейлоггинг
----------------------------------------------------------------------------


Злоумышленники могут регистрировать нажатия клавиш пользователя, чтобы перехватить учетные данные в момент их ввода. Запись с клавиатуры, скорее всего, используется для получения учетных данных для новых возможностей доступа, когда попытки OS Credential Dumping неэффективны, и может потребовать от противника перехвата нажатий клавиш в системе в течение значительного периода времени, прежде чем учетные данные будут успешно перехвачены. Чтобы повысить вероятность быстрого захвата учетных данных, злоумышленник может также выполнять такие действия, как очистка cookies браузера, чтобы заставить пользователей повторно аутентифицироваться в системе.

Перехват клавиатуры - наиболее распространенный тип перехвата ввода, при этом существует множество различных способов перехвата нажатий клавиш Некоторые методы включают в себя:

 - Перехват обратных вызовов API, используемых для обработки нажатий клавиш. В отличие от Credential API Hooking, этот способ фокусируется исключительно на API-функциях, предназначенных для обработки данных нажатия клавиш.
 - Чтение необработанных данных нажатия клавиш из аппаратного буфера.
 - Модификации реестра Windows.
 - Пользовательские драйверы.
 - Модификация образа системы может предоставить злоумышленникам крючки в операционную систему сетевых устройств для считывания необработанных нажатий клавиш для сеансов входа в систему.



Захват входных данных графического интерфейса
----------------------------------------------------------------------------


Злоумышленники могут имитировать обычные компоненты графического интерфейса операционной системы, чтобы запросить у пользователя учетные данные с кажущейся легитимной подсказкой. Когда выполняются программы, требующие дополнительных привилегий по сравнению с текущим пользовательским контекстом, операционная система обычно запрашивает у пользователя соответствующие учетные данные для авторизации повышенных привилегий для выполнения задачи.

Злоумышленники могут имитировать эту функциональность, запрашивая у пользователя учетные данные с помощью кажущегося легитимным запроса по ряду причин, имитирующих обычное использование, например поддельная программа установки, требующая дополнительного доступа, или поддельный пакет для удаления вредоносного ПО.  Этот тип запроса может использоваться для сбора учетных данных с помощью различных языков, таких как AppleScript и PowerShell. В системах Linux злоумышленники могут запускать диалоговые окна с запросом учетных данных из вредоносных сценариев оболочки или командной строки.



Захват веб-портала
----------------------------------------------------------------------------


Злоумышленники могут установить код на внешних порталах, например на странице входа в VPN, чтобы перехватить и передать учетные данные пользователей, которые пытаются войти в службу. Например, скомпрометированная страница входа в систему может регистрировать предоставленные учетные данные пользователя перед тем, как он войдет в службу.

Этот вариант перехвата ввода может быть осуществлен после компрометации с использованием законного административного доступа в качестве резервной меры для сохранения доступа к сети через внешние удаленные службы и действительные учетные записи или как часть первоначальной компрометации путем использования внешнего веб-сервиса.



Подключение API-интерфейса учетных данных
----------------------------------------------------------------------------


Злоумышленники могут подключаться к функциям интерфейса прикладного программирования Windows для сбора учетных данных пользователя. Вредоносные механизмы перехвата могут перехватывать вызовы API, содержащие параметры, раскрывающие учетные данные пользователя. В отличие от кейлоггинга, эта техника нацелена именно на функции API, содержащие параметры, раскрывающие учетные данные пользователя.