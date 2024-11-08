веб-приложениt "Travel Pins" позволяет пользователям делиться отзывами о туристических местах, находить интересные достопримечательности и планировать свои путешествия. 

Фронтенд часть приложения разработана на основе React.js, что обеспечивает создание динамичных и отзывчивых пользовательских интерфейсов. React позволяет разбивать интерфейс на компоненты, которые могут быть повторно использованы и легко модифицированы. Каждый компонент отвечает за свою часть функциональности, что упрощает разработку и тестирование.
Бэкенд реализован с использованием Node.js и фреймворка Express.js. Node.js обеспечивает выполнение JavaScript на серверной стороне, что позволяет использовать один и тот же язык программирования для фронтенда и бэкенда. Express.js предоставляет набор инструментов для построения API и обработки HTTP-запросов. В архитектуре приложения предусмотрены несколько маршрутов для обработки различных запросов: например, маршруты для работы с пользователями, метками и верификацией данных.
База данных MongoDB используется для хранения данных о пользователях и их метках. MongoDB, будучи документно-ориентированной базой данных, позволяет гибко хранить данные в формате JSON, что хорошо сочетается с JavaScript-экосистемой. Это также обеспечивает легкость в масштабировании и высокой производительности при работе с большими объемами данных.
Внешний сервис Mapbox интегрирован для предоставления функциональности работы с картами. Mapbox API используется для отображения интерактивных карт, добавления пользовательских меток и настройки внешнего вида карт. Mapbox позволяет загружать карты с высокими деталями и предоставляет инструменты для взаимодействия с этими картами, такие как зуммирование, панорамирование и добавление пользовательских слоев.

Схемы включают в себя обязательные поля как имя, почту, пароль (для пользователя) и заголовок, описание и оценку (для метки). Также для пользователя добавлены поля для продолжительности действия токена восстановления пароля и булевы поля для сброса пароля и верификации. При создании же пина поля со страной, городом и временем заполняются автоматически.
В качестве второго фактора для аутентификации была выбрана электронная почта. Механизм реализован с помощью smtp сервиса Google. При первой регистрации пользователю на почту, указанную при регистрации, отправляется шестизначный код через smtp сервис. Сам же код генерируется случайно на стороне сервера. Аналогичный механизм используется и для восстановления пароля. Также в целях безопасности при запросе смены пароля прямо не говорится, удалось ли отправить код для восстановления, просто выводится сообщение о том, что если почта существует, то на неё придет код. Данные методы представлены на рисунках ниже.

Также в целях безопасности все пароли, ссылки и токены хранятся в скрытом файле .env. Это сделано для того, чтобы конфиденциальные данные не хранились на сервере в открытом виде.
пароли пользователей хранятся в базе данных в виде хэшей. 

Также стоит отметить, как происходит накопление отзывов на одной метке. Изначально, при создании метки на карте она закрепляется за пользователем, оставившим её. Если другие пользователи будут оставлять свои отзывы об этом же месте, они будут заноситься в запись данной метки в качестве записи в массиве. Таким образом, в базе данных хранится метка, у нее есть владелец и отзыв владельца, а внутри неё также хранится массив с отзывами остальных пользователей.

бэкенд сторона использует CORS политики браузера.

была создана API документация с помощью Swagger. Интеграция Swagger в проект "Travel Pins" позволяет создавать подробную и удобную документацию для API, что облегчает работу с API как для разработчиков, так и для пользователей. 
![image](https://github.com/user-attachments/assets/ad287780-de48-417a-b881-3bbb9e45a8da)
документация API

![image](https://github.com/user-attachments/assets/3da51e9d-8ed5-42bb-a1e0-785f568d5cff)
Вид приложения

при построении маршрута происходит проверка на то, есть ли рядом с планируемым маршрутом высокооцененное место. Проверяется, имеется ли на указанном расстоянии от любой  точки линии маршрута точка с высокой оценкой, и, если такая имеется, маршрут пройдет через нее.

![image](https://github.com/user-attachments/assets/401cf96a-efcf-4c85-9827-a5a4f172a773)
построение маршрута

Способы построения остальных видов маршрутов аналогичны, за исключением того, что указываемые точки определяются с помощью метода MapBox geocoding, который позволяет определить места, указанные пользователем при вводе в форму для построения маршрута.

был реализован адаптивный дизайн для различных разрешений экранов. Для планшетов все функции приложения собраны в меню, которое появляется при нажатии на кнопку. Для телефонов же было реализовано выпадающее меню, после выбора опции в котором оно закрывается. 

![image](https://github.com/user-attachments/assets/643084be-baaf-44bd-aa9d-02fff9e70f97)
Дизайн для планшетов

![image](https://github.com/user-attachments/assets/dac8a4e8-82d2-4c80-99dd-be5bdd8b0eb6)
Дизайн для телефонов

была реализована кнопка геолокации, при нажатии на которую появляется метка на карте с текущим местоположением пользователя. 
