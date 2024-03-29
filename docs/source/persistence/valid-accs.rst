



Действительные учетные записи
=========================================


Недоброжелатели могут получить учетные данные существующих учетных записей и злоупотреблять ими в качестве средства получения первоначального доступа, постоянного доступа, повышения привилегий или уклонения от защиты. Скомпрометированные учетные данные могут использоваться для обхода контроля доступа к различным ресурсам систем в сети и даже для постоянного доступа к удаленным системам и внешним службам, таким как VPN, Outlook Web Access, сетевые устройства и удаленный рабочий стол. Скомпрометированные учетные данные могут также предоставить противнику повышенные привилегии для определенных систем или доступ к ограниченным областям сети. Злоумышленники могут не использовать вредоносное ПО или инструменты в сочетании с законным доступом, который предоставляют учетные данные, чтобы затруднить обнаружение их присутствия.

В некоторых случаях злоумышленники могут использовать неактивные учетные записи: например, принадлежащие лицам, которые больше не являются частью организации. Использование таких учетных записей может позволить противнику избежать обнаружения, поскольку пользователь исходной учетной записи не будет присутствовать, чтобы определить аномальную активность, происходящую с его учетной записью.

Наложение разрешений для локальных, доменных и "облачных" учетных записей в сети систем вызывает озабоченность, поскольку противник может иметь возможность перемещаться между учетными записями и системами, чтобы достичь высокого уровня доступа (например, администратора домена или предприятия) и обойти контроль доступа, установленный на предприятии.







Учетные записи по умолчанию
-------------------------------------------------


Недоброжелатели могут получить учетные данные учетной записи по умолчанию и злоупотреблять ими как средством получения первоначального доступа, сохранения, повышения привилегий или уклонения от защиты. Учетные записи по умолчанию - это учетные записи, встроенные в ОС, например учетные записи "Гость" или "Администратор" в системах Windows. К учетным записям по умолчанию также относятся учетные записи, установленные по умолчанию на заводе/провайдере в других типах систем, программного обеспечения или устройств, включая учетную запись пользователя root в AWS и учетную запись службы по умолчанию в Kubernetes.

Учетные записи по умолчанию не ограничиваются клиентскими машинами, а включают в себя учетные записи, предустановленные для такого оборудования, как сетевые устройства и компьютерные приложения, независимо от того, являются ли они внутренними, с открытым исходным кодом или коммерческими. Устройства, которые поставляются с предустановленной комбинацией имени пользователя и пароля, представляют собой серьезную угрозу для организаций, которые не меняют их после установки, поскольку они являются легкой мишенью для злоумышленников. Аналогичным образом, противники могут использовать публично раскрытые или украденные личные ключи или учетные данные для законного подключения к удаленным средам через удаленные службы.



Учетные записи доменов
-------------------------------------------------


Недоброжелатели могут получить учетные данные учетной записи домена и злоупотреблять ими как средством получения первоначального доступа, сохранения, повышения привилегий или уклонения от защиты. Учетные записи домена - это учетные записи, управляемые доменными службами Active Directory, в которых настраиваются доступ и разрешения для систем и служб, входящих в домен. Учетные записи домена могут охватывать пользователей, администраторов и службы.

Недоброжелатели могут скомпрометировать учетные записи домена, некоторые из которых имеют высокий уровень привилегий, с помощью различных средств, таких как OS Credential Dumping или повторное использование пароля, что позволяет получить доступ к привилегированным ресурсам домена.







Локальные учетные записи
-------------------------------------------------


Недоброжелатели могут получить учетные данные локальной учетной записи и злоупотреблять ими как средством получения первоначального доступа, сохранения, повышения привилегий или уклонения от защиты. Местные учетные записи - это учетные записи, настроенные организацией для использования пользователями, удаленной поддержкой, службами или для администрирования одной системы или службы.

Местные учетные записи также могут использоваться для повышения привилегий и сбора учетных данных через OS Credential Dumping. Повторное использование пароля может позволить злоупотреблять локальными учетными записями на множестве машин в сети в целях повышения привилегий и латерального перемещения.



Облачные учётные записи
-------------------------------------------------


Действительные учетные записи в облачных средах могут позволить злоумышленникам выполнять действия, направленные на получение первоначального доступа, постоянство, повышение привилегий или уклонение от защиты. Облачные учетные записи - это учетные записи, созданные и настроенные организацией для использования пользователями, удаленной поддержки, служб или для администрирования ресурсов поставщика облачных услуг или приложения SaaS. Облачные учетные записи могут существовать исключительно в облаке или быть гибридными, объединенными между локальными системами и облаком посредством федерации с другими источниками идентификации, такими как Windows Active Directory. 

Учетные записи служб и пользователей могут быть объектом атаки злоумышленников с помощью брутфорса, фишинга или различных других способов получения доступа к среде. Федеративные учетные записи могут стать для злоумышленника путем воздействия как на локальные системы, так и на облачные среды.

Противник может создать долговременные дополнительные учетные данные "облака" на скомпрометированной учетной записи "облака", чтобы сохранить доступ к среде. Такие учетные данные также могут использоваться для обхода средств контроля безопасности, таких как многофакторная аутентификация.

Учетные записи "облака" также могут получить временный повышенный доступ к "облаку" или другие привилегии с помощью различных средств в среде. Ошибки в назначении ролей или политиках принятия ролей могут позволить злоумышленникам использовать эти механизмы для получения разрешений, выходящих за рамки полномочий учетной записи. Такие сверхпривилегированные учетные записи могут использоваться для сбора конфиденциальных данных из онлайн-хранилищ и баз данных через Cloud API или другими способами.