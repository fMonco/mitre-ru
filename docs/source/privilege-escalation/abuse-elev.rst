



Механизм управления повышением уровня злоупотребления
=================================================================


Злоумышленники могут обходить механизмы, предназначенные для контроля повышения привилегий, чтобы получить разрешения более высокого уровня. Большинство современных систем содержат встроенные механизмы контроля повышения привилегий, предназначенные для ограничения привилегий, которые пользователь может выполнять на машине. Для выполнения задач, которые могут быть отнесены к категории повышенного риска, необходимо предоставить полномочия определенным пользователям. Противник может использовать несколько методов, чтобы воспользоваться встроенными механизмами контроля для повышения привилегий в системе.



Setuid and Setgid
-------------------------------------------------

Злоумышленник может злоупотреблять конфигурациями, в которых для приложения установлены биты setuid или setgid, чтобы заставить код работать в контексте другого (и, возможно, более привилегированного) пользователя. В Linux или macOS, когда биты setuid или setgid установлены для бинарного файла приложения, приложение будет запускаться с привилегиями пользователя или группы, владеющих приложением соответственно. Обычно приложение запускается в контексте текущего пользователя, независимо от того, какой пользователь или группа владеют приложением. Однако бывают случаи, когда для правильной работы программы должны выполняться в повышенном контексте, но пользователь, запускающий их, может не обладать необходимыми привилегиями.


Вместо того чтобы создавать запись в файле sudoers, что должен делать root, любой пользователь может указать флаг setuid или setgid, который должен быть установлен для его собственных приложений (т. е. Изменение прав доступа к файлам и каталогам в Linux и Mac). Команда chmod может установить эти биты с помощью битовой маски, chmod 4777  или с помощью сокращенного именования, chmod u+s . Это включит бит setuid. Чтобы включить бит setgid, можно использовать chmod 2775 и chmod g+s.


Злоумышленники могут использовать этот механизм в своих собственных вредоносных программах, чтобы убедиться, что в будущем они смогут выполняться в повышенных контекстах. Такое злоупотребление часто является частью "выхода из оболочки" или других действий по обходу среды выполнения с ограниченными правами.


В качестве альтернативы злоумышленники могут найти уязвимые двоичные файлы с уже включенными битами setuid или setgid (например, File and Directory Discovery). Биты setuid и setguid обозначаются символом "s" вместо "x" при просмотре атрибутов файла с помощью команды ls -l. Для поиска таких файлов можно также использовать команду find. Например, find / -perm +4000 2>/dev/null может использоваться для поиска файлов с установленным setuid, а find / -perm +2000 2>/dev/null - для setgid. Двоичные файлы, в которых установлены эти биты, могут быть использованы злоумышленниками.



Обход контроля учетных записей пользователей
-------------------------------------------------

Злоумышленники могут обойти механизмы UAC, чтобы повысить привилегии процессов в системе. Контроль учетных записей пользователей Windows (UAC) позволяет программе повысить свои привилегии (отслеживаемые как уровни целостности от низкого до высокого) для выполнения задачи с правами уровня администратора, возможно, запрашивая подтверждение у пользователя. Воздействие на пользователя варьируется от отказа в выполнении операции при высоком уровне защиты до разрешения пользователю выполнить действие, если он входит в группу локальных администраторов и пропустит запрос или позволит ему ввести пароль администратора для завершения действия.

Если уровень защиты UAC на компьютере установлен на любой уровень, кроме самого высокого, некоторые программы Windows могут повышать привилегии или выполнять некоторые объекты Component Object Model с повышенными правами без запроса пользователя через окно уведомления UAC. Примером этого является использование Rundll32 для загрузки специально созданной DLL, которая загружает объект Component Object Model с автоматическим повышением прав и выполняет файловую операцию в защищенном каталоге, для которой обычно требуется повышенный доступ. Вредоносное программное обеспечение также может быть внедрено в доверенный процесс для получения повышенных привилегий без запроса пользователя.

Было обнаружено множество методов обхода UAC. Страница readme на Github для UACME содержит обширный список методов, которые были обнаружены и реализованы, но он не может быть полным списком обходов. Регулярно обнаруживаются и используются дополнительные методы обхода, такие как:

eventvwr.exe может автоматически подниматься и выполнять указанный двоичный файл или скрипт.
Еще один способ обхода возможен при использовании некоторых методов перемещения в сторону, если известны учетные данные учетной записи с правами администратора, поскольку UAC - это механизм безопасности одной системы, и привилегии или целостность процесса, запущенного на одной системе, будут неизвестны на удаленных системах и по умолчанию будут иметь высокую степень целостности.


Sudo и Sudo кеширование
-------------------------------------------------

Злоумышленники могут выполнять кэширование sudo и/или использовать файл sudoers для повышения привилегий. Злоумышленники могут выполнять команды от имени других пользователей или порождать процессы с более высокими привилегиями.


В системах Linux и MacOS команда sudo (иногда называемая "superuser do") позволяет пользователям выполнять команды с терминалов с повышенными привилегиями и контролировать, кто может выполнять эти команды в системе. Команда sudo "позволяет системному администратору делегировать полномочия, чтобы дать определенным пользователям (или группам пользователей) возможность выполнять некоторые (или все) команды от имени root или другого пользователя, обеспечивая при этом аудиторский след команд и их аргументов." Поскольку sudo была создана для системного администратора, она имеет некоторые полезные функции настройки, такие как timestamp_timeout, который представляет собой количество времени в минутах между экземплярами sudo, прежде чем она будет повторно запрашивать пароль. Это связано с тем, что sudo имеет возможность кэшировать учетные данные в течение определенного периода времени. Для определения этого таймаута Sudo создает (или трогает) файл в /var/db/sudo с меткой времени, когда sudo был запущен в последний раз. Кроме того, существует переменная tty_tickets, которая рассматривает каждый новый tty (терминальную сессию) изолированно. Это означает, что, например, таймаут sudo на одном tty не повлияет на другой tty (вам придется снова набирать пароль).


Файл sudoers, /etc/sudoers, описывает, какие пользователи могут выполнять те или иные команды и с каких терминалов. Здесь также описано, какие команды пользователи могут выполнять от имени других пользователей или групп. Это обеспечивает принцип наименьших привилегий, согласно которому пользователи большую часть времени работают с минимально возможными правами и повышаются до уровня других пользователей или прав только по мере необходимости, обычно запрашивая пароль. Однако в файле sudoers можно указать, когда не запрашивать у пользователей пароли, например user1 ALL=(ALL) NOPASSWD: ALL. Однако для редактирования этого файла требуются повышенные привилегии.


Злоумышленники также могут злоупотреблять плохими конфигурациями этих механизмов для повышения привилегий, не требуя пароля пользователя. Например, временная метка /var/db/sudo может быть отслежена на предмет того, попадает ли она в диапазон timestamp_timeout. Если да, то вредоносное ПО может выполнять команды sudo без необходимости вводить пароль пользователя. Кроме того, если функция tty_tickets отключена, злоумышленники могут выполнить эту команду с любого tty данного пользователя.


В дикой природе вредоносное ПО отключало tty_tickets для потенциального облегчения скриптинга, выдавая команду echo \'Defaults !tty_tickets\' >> /etc/sudoers. Для того чтобы это изменение отразилось, вредоносное ПО также выдавало команду killall Terminal. Начиная с macOS Sierra, в файле sudoers по умолчанию включен параметр tty_tickets.


Повышенное выполнение с подсказкой
-------------------------------------------------

Злоумышленники могут использовать API AuthorizationExecuteWithPrivileges для повышения привилегий, запрашивая у пользователя учетные данные. Цель этого API - предоставить разработчикам приложений простой способ выполнения операций с привилегиями root, например, для установки или обновления приложений. Этот API не подтверждает, что программа, запрашивающая привилегии root, получена из надежного источника или была злонамеренно изменена.


Хотя этот API устарел, он по-прежнему полностью функционирует в последних выпусках macOS. При вызове этого API пользователю будет предложено ввести свои учетные данные, но никаких проверок происхождения или целостности программы не производится. Программа, вызывающая API, также может загружать файлы, доступные для записи в мире, которые могут быть модифицированы для выполнения вредоносного поведения с повышенными привилегиями.


Злоумышленники могут использовать AuthorizationExecuteWithPrivileges для получения привилегий root, чтобы установить вредоносное ПО на жертву и установить механизмы сохранения. Эта техника может быть объединена с Masquerading, чтобы обманом заставить пользователя предоставить повышенные привилегии вредоносному коду. Также было показано, что эта техника работает путем модификации легитимных программ, присутствующих на машине и использующих этот API.



Временный повышенный доступ к облаку
-------------------------------------------------

Злоумышленники могут злоупотреблять конфигурациями разрешений, позволяющими им получать временный повышенный доступ к облачным ресурсам. Многие облачные среды позволяют администраторам предоставлять учетным записям пользователей или служб разрешение запрашивать временный доступ к ролям, выдавать себя за другие учетные записи, передавать роли ресурсам и службам или иным образом получать кратковременный доступ к набору привилегий, которые могут отличаться от их собственных.

Доступ "точно в срок" - это механизм предоставления дополнительных ролей облачным учетным записям на гранулированной временной основе. Это позволяет учетным записям работать только с теми разрешениями, которые им необходимы на ежедневной основе, и запрашивать дополнительные разрешения по мере необходимости. Иногда запросы на доступ "точно в срок" настраиваются таким образом, чтобы требовать ручного одобрения, в то время как в других случаях необходимые разрешения предоставляются автоматически.

Имперсонация учетной записи позволяет учетным записям пользователей или служб временно действовать с разрешениями другой учетной записи. Например, в GCP пользователи с ролью iam.serviceAccountTokenCreator могут создавать временные маркеры доступа или подписывать произвольные полезные нагрузки с разрешениями учетной записи службы. В Exchange Online роль ApplicationImpersonation позволяет учетной записи службы использовать разрешения, связанные с указанными учетными записями пользователей.

Многие облачные среды также включают механизмы, позволяющие пользователям передавать роли ресурсам, которые позволяют им выполнять задачи и аутентифицироваться в других службах. Хотя пользователь, создающий ресурс, не принимает напрямую роль, которую он ему передает, он все равно может воспользоваться преимуществами доступа роли - например, настроить ресурс на выполнение определенных действий с предоставленными ему разрешениями. В AWS пользователи с разрешением PassRole могут разрешить создаваемому ими сервису принимать на себя заданную роль, а в GCP пользователи с ролью iam.serviceAccountUser могут прикрепить учетную запись сервиса к ресурсу.