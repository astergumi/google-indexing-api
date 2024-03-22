# google-indexing-api-bulk

Created by Steve at [Journey Further SEO](https://www.journeyfurther.com/)

Requires node.js - https://nodejs.org/en/download/

This script will help you index your website's pages in bulk, without having to manually request each URL for submission in the Search Console interface.

First off you will need to set up access to the Indexing API in Google Cloud Platform - follow the instructions below.

https://developers.google.com/search/apis/indexing-api/v3/prereqs

Once you have access to Indexing API you'll be able to download a public/private key pair JSON file, this contains all of your credentials and should be saved as "service_account.json".

Add the URLs to the urls.txt file that you need to be crawled/indexed.


## Verify site ownership in Search Console to submit URLs for indexing
In this step, you'll verify that you have control over your web property.

To verify ownership of your site you'll need to add your service account email address (see service_account.json - client_email) and add it as an owner ('delegated') of the web property in Search Console.

You can find your service account email address in two places:
- The client_email field in the JSON private key that you downloaded when you created your project.
- The Service account ID column of the Service Accounts view in the Developer Console.
- The email address has a format similar to the following:

For example, "my-service-account@test-project-42.google.com.iam.gserviceaccount.com".

Then...

1. Go to [Google Webmaster Central](https://www.google.com/webmasters/verification/home)
2. Click your verified property
3. Scroll down and click 'Add an owner'.
4. Add your service account email address as an owner to the property.


## Quotas

100 URLs per request batch

200 URLs per day

1. Подключение Indexing API к Google Search Console: создание сервисного аккаунта и JSON-ключа
Первым делом настроим доступ в консоли Indexing API. Переходим на [Google Cloud Platform](https://console.cloud.google.com/welcome?organizationId=0&supportedpurview=project) и создаём там проект.

Прописываем название проекта (например, название вашего сайта). Местоположение можно не указывать.
[1](img/1.webp)
Далее переходим в раздел “IAM и администрирования” в подраздел “Сервисные аккаунты”.
[2](img/2.webp)
После того как проект будет создан и вы перейдете в подраздел, увидите перед собой окно. Здесь нужно создать сервисный аккаунт.
[3](img/3.webp)
В первой строке указываете название вашего проекта латиницей (например, название сайта). Во второй строке данные подтянутся благодаря тому, что вы введете в первой. Третью строку заполняете по желанию.
[4](img/4.webp)
Нажимаете создать и выбираете роль “Владелец”.
[5](img/5.webp)

Нажимаете “Продолжить”: увидите окно, в котором ничего не нужно указывать, просто нажать кнопку “Готово”.
[6](img/6.webp)
Далее во всплывающем окне создаем ключ в столбце “Действия”.
[7](img/7.webp)
Выбираете тип ключа JSON.
[8](img/8.webp)
Ваш ключ автоматически загружен на компьютер и будет выглядеть вот так:
[9](img/9.webp)
Ключ в текстовом редакторе.
Позже ключ будет применяться для запуска скрипта.

2. Настройка скрипта

Открываем файл service_account.
[10](img/10.webp)
Заменяем содержимое внутри файла на скачанный JSON ключ.
[11](img/11.webp)
Теперь скрипт готов и его нужно связать с Google Search Console.

3. Связь скрипта с GSC
Заходим в Google Search Console в наш проект.
Переходим в раздел “Настройки”и нажимаем “Добавить пользователя”.
[12](img/12.webp)
Вы будете видеть такое окно.
[13](img/13.webp)
В первой строке нужно добавить электронный адрес с Google Cloud Platform, который мы создали на предыдущих этапах, а во второй — “Полный доступ”.
[14](img/14.webp)
Строка проекта в интерфейсе Google Cloud Platform.
По итогу у вас будет вот такое окно, но нам не подходит “Полный доступ”. Поэтому смотрим, где у нас есть “Владелец”, нажимаем троеточие и “Управление владельцами ресурса”. На функции “Добавить владельца” вставляем тот же электронный адрес с Google Cloud Platform, который мы создали на предыдущих этапах.
[15](img/15.webp)
У вас должно выйти так, как показано на скрине ниже — с правами “Владелец”.
[16](img/16.webp)
Теперь нужно включить Index API в нашем проекте. Переходим по ссылке и выбираем сервисный аккаунт, включая API.
[17](img/17.webp)
4. Запускаем скрипт
Заходим в скачанную папку на компьютере и находим файл “urls”. Вставляем туда url, которые нужно проиндексировать, и сохраняем. В сутки можно отправить до 200 шт. url, поэтому формируем 2 пакета по 100 url.
[18](img/18.webp)
Сохраняем в текстовый документ url которые надо проиндексировать.
Для следующих шагов нам нужно найти и скачать исходный код node.js по ссылке.
Далее вызываем командную строку и заходим в папку google-indexing-api-bulk-master, скачанную ранее. У нас эта папка лежит по пути Desktop — Roots — google-indexing-api-bulk-master.
[19](img/19.webp)
Заходим в корневую папку ‘cd Desktop”.
В новой строке нужно добавить “cd Roots” и нажать Enter.
Далее в новой строчке добавляем “cd google-indexing-api-bulk-master” (папка, в которой находятся наши файлы), нажимаем Enter.
После того как мы зашли в папку, необходимо загрузить нужные файлы библиотеки туда же. Делается это при помощи следующих команд:

В каждой новой строке добавляем значения, которые показаны ниже, при этом нужно немного подождать, пока не загрузятся данные.
C: \ Users \ user \ Desktop \ Roots \ google-indexing-api-bulk-master> npm install requests
C: \ Users \ user \ Desktop \ Roots \ google-indexing-api-bulk-master> npm audit fix
C: \ Users \ user \ Desktop \ Roots \ google-indexing-api-bulk-master> npm audit fix --force

[20](img/20.webp)
После того как все файлы библиотеки установлены, запускаем последнюю команду node index.js.

По итогу вы должны будете увидеть такую финальную картину. Если вместо этого скрина вы увидели что-то другое, значит вернитесь к началу статьи и внимательно проверьте каждый пункт.
[21](img/21.webp)
Когда в последующем вам нужно будет индексировать новые страницы на этом проекте, в файле urls удаляете старые урлы и меняете на новые.

В командной строке C:\Users\user\Desktop\Roots\google-indexing-api-bulk-master> добавляете node index.js и нажимаете Enter.

Для других проектов вам нужно будет создавать все заново.