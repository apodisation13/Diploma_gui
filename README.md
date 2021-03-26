# САМОЕ ГЛАВНОЕ:
**В файле classes_try нужно вписать свой токен ВК строка12 и свой токен ЯндексДиска строка158, удалив ниже строки с открытие файла.**

### Общие моменты:
* Требуется разрешение экрана не меньше чем размер окна (1400*600). У приложения нельзя изменить размер экрана.
* Пока tkinter находится в процессе отработки какой-либо команды (в частности, отрисовывает кнопки), другие кнопки нажимать не рекомендуется. Будет работать некорректно.

### Описание работы программы:

1. Вводим id пользователя ВК или его screen_name

2. По нажатию кнопки проверить ID выполняется запрос к ВК по методу users.get. 
Проверяется в class VkPhotos в фукнции def validate_user_id. Возвращает true если можно работать дальше, false – если нет (см.ниже).

2.1. Ошибки (показываются из response от ВК по ключу “error”). Возвращают False и соответствующее сообщение.

2.1.1. Неверный токен ВК.

2.1.2. Неправильный пользователь – id или screen_name.

2.2. Успех – пользователь введён верно.

2.2.1. ** Если было введено screen_name, здесь произойдёт его замена на id для дальнейшей корректной работы. В классе App появится лэйбл info_lbl где будут отображаться как id, так и screen_name. 

2.2.2. Если пользователь удалён, вернётся False и соответствующее сообщение.

2.2.3. Если пользователь для вас закрыт, вернётся тоже False и соответствующее сообщение.

2.2.4. Если всё введено верно, то вернётся True, выдастся сообщение, что всё в порядке, и программа продолжится.

3.	В случае True из предыдущего пункта, программа инициализирует список из словарей вида [{имя файла: ссылка на фотку}, итп] для альбомов profile и wall ВК по методу photos.get. Обращение к методу VkPhotos.execute_photos_get в функции класса App.create.

4.	Далее создаётся список списков вида: [[название личного альбома, количество фоток в нем, id_альбома], итп]. Обращение к методу VkPhotos.get_album_list (по методу photos.getAlbums) в функции класса App.create. Если альбомы закрыты или их нет, появится лэйбл, что пользователь скрыл альбомы.

5.	** Если у пользователя вообще нет фотографий ни в одном альбоме, программа выдаст сообщение и начнётся с начала.

6.	Далее появляются альбомы profile и wall с кнопками «показать» и «загрузить все», а также личный альбом с такими же кнопками и кнопками выбора следующего или предыдущего альбома (менее первого альбома и более последнего -  нельзя пойти). 

7.	При нажатии загрузить все – все фотографии сразу без предупреждения загрузятся на яндекс диск. 
Может занять некоторое время, в консоли появится прогрессбар.

8.	При нажатии показать – откроется 10 фотографий для альбомов profile и wall и 20 фотографий для личного альбома. Также появятся кнопки листания страниц альбома. Нажимая на отдельную фотографию, можно закачать её. 