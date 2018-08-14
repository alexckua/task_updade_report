
Основная функция плагина: отслеживание встроенного в систему события - обновление задачи, а именно, при:
  *  обновлении самой задачи (любого из полей)
  * добавлении\удалении или модификации комментария
  * добавлении или удалении файла
  ...необходимо делать HTTP POST-запрос на адрес указанный в настройках плагина.

Формат POST-запроса: переменная с именем data, в которой содержится JSON-строка, описывающая объект со следующими полями:
  * issueid - идентификатор измененной задачи
  * userid - идентификатор пользователя, внесшего изменения в задачу
  * datetime - дата и время внесения изменений
  * report - отчет о содержимом внесенных изменений
Данный отчет состоит из ряда полей, содержащих сводную информацию о добавленном текстовом контенте  и касается только комментариев к задаче или самого тела задачи, в момент ее создания:
  * scount - общее количество символов
  * wcount - количество слов разделенных пробелами, запятыми, точками и тире
  * mused - наиболее часто используемый символ
Например:
````json
  {
   'issueid':12345,
   'userid':12345,
   'datetime':'2014-13-12 12:13:14',
   'report': {
     'scount': 123,
     'wcount': 23,
     'mused': 'a'
     }
  }

Плагин должен иметь страницу настройки, на которой должна быть возможность сменить адрес сервиса, который и должен принимать все HTTP POSТ-запросы.
