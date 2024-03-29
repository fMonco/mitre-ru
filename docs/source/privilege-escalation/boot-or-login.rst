


Скрипты инициализации загрузки или входа в систему
================================================================================

Недоброжелатели могут использовать сценарии, автоматически выполняемые при загрузке или инициализации входа в систему, для создания постоянства. Сценарии инициализации могут использоваться для выполнения административных функций, которые часто могут запускать другие программы или отправлять информацию на внутренний сервер регистрации. Эти сценарии могут различаться в зависимости от операционной системы и от того, применяются ли они локально или удаленно.

Недоброжелатели могут использовать эти сценарии для поддержания постоянства в одной системе. В зависимости от конфигурации доступа к сценариям входа в систему могут потребоваться либо локальные учетные данные, либо учетная запись администратора.

Злоумышленник также может повысить свои привилегии, поскольку некоторые сценарии загрузки или инициализации входа в систему выполняются с более высокими привилегиями.




Скрипт входа в систему (Windows)
--------------------------------------------------------------------------------

Для создания постоянства злоумышленники могут использовать сценарии входа в систему Windows, автоматически выполняющиеся при инициализации входа. Windows позволяет запускать сценарии входа в систему каждый раз, когда в нее входит определенный пользователь или группа пользователей. Это делается путем добавления пути к сценарию в ключ реестра HKCU\Environment\UserInitMprLogonScript.

Злоумышленники могут использовать эти сценарии для поддержания постоянства в одной системе. В зависимости от конфигурации доступа к сценариям входа в систему могут потребоваться либо локальные учетные данные, либо учетная запись администратора.



Login Hook
--------------------------------------------------------------------------------

Злоумышленники могут использовать крючок входа в систему для создания персистентной защиты, выполняемой при входе пользователя в систему. Login Hook - это plist-файл, который указывает на определенный скрипт, выполняемый с привилегиями root при входе пользователя в систему. Файл plist находится в папке /Library/Preferences/com.apple.loginwindow.plist и может быть изменен с помощью утилиты командной строки defaults. Такое же поведение характерно и для крючков выхода из системы, когда скрипт может быть выполнен при выходе пользователя из системы. Для изменения или создания всех хуков требуются права администратора.









Скрипты RC
----------------------------------------------------------------------------


Злоумышленники могут установить постоянство, изменив RC-скрипты, которые выполняются при запуске Unix-подобной системы. Эти файлы позволяют системным администраторам назначать и запускать пользовательские службы при запуске для различных уровней выполнения. Для изменения RC-скриптов требуются привилегии root.

Злоумышленники могут установить постоянство, добавив вредоносный двоичный путь или команды оболочки в rc.local, rc.common и другие RC-скрипты, специфичные для дистрибутива Unix-подобной системы. После перезагрузки система выполняет содержимое скрипта от имени root, что приводит к постоянству.

Злоупотребление злоумышленниками RC-скриптами особенно эффективно для легких Unix-подобных дистрибутивов, использующих пользователя root по умолчанию, таких как IoT или встроенные системы.

Несколько Unix-подобных систем перешли на Systemd и отказались от использования RC-скриптов. В macOS этот механизм уже устарел в пользу Launchd.  Эта техника может использоваться в Mac OS X Panther v10.3 и более ранних версиях, которые по-прежнему выполняют RC-скрипты. Для сохранения обратной совместимости некоторые системы, такие как Ubuntu, будут выполнять RC-скрипты, если они существуют с правильными разрешениями на файлы.








Пусковые элементы
----------------------------------------------------------------------------


Злоумышленники могут использовать элементы запуска, автоматически выполняющиеся при инициализации загрузки, для обеспечения постоянства. Элементы запуска выполняются на заключительном этапе процесса загрузки и содержат сценарии оболочки или другие исполняемые файлы вместе с информацией о конфигурации, используемой системой для определения порядка выполнения всех элементов запуска.

Технически это устаревшая технология (ее заменил Daemon запуска), поэтому наличие соответствующей папки /Library/StartupItems в системе по умолчанию не гарантируется, но в macOS Sierra она, похоже, существует по умолчанию. Элемент запуска - это каталог, исполняемый файл которого и список свойств конфигурации (plist), StartupParameters.plist, находятся в каталоге верхнего уровня.

Злоумышленник может создать соответствующие папки/файлы в каталоге StartupItems, чтобы зарегистрировать собственный механизм сохранения. Кроме того, поскольку StartupItems запускаются на этапе загрузки macOS, они будут работать от имени пользователя root с повышенными правами.
