# highload-vk-video

## 1. Тема и целевая аудитория
### Тема
VK Видео — сервис, запущенный VK (ранее известной как Mail.ru Group) 15 октября 2021 года. Позиционируется как отечественный конкурент международным платформам, таким как YouTube, TikTok и Netflix.

### Целевая аудитория
   
Целевая аудитория: большая часть находится в рф. По старым отчетам можно прикинуть, что из 76 млн ежемесячнх пользователей, 70 из РФ, остальные из 6 СНГ

13–17 лет: ~15–20%

18–24 года: ~25–30%

25–34 года: ~25–30%

35–44 года: ~15–20%

45 лет и старше: ~10–15%

### MVP

**Функционал:**
1. Регистрация и авторизация.
2. Просмотр видео.
3. Поиск видео.
4. Рекомендация видео.
5. Подписки.
6. Система фитбеков:
   - Лайки.
   - Комментарии.
7. Профиль пользователя.


**Ключевые продуктовые решения:**
1. Алгоритмы, предлагающие пользователям контент на основе их предпочтений, истории просмотров и интересов.
2. Персонализированные рекомендации для увеличения вовлеченности.


## Нагрузка ##

![image](https://github.com/user-attachments/assets/45a026a6-e424-4e33-92f7-b74f87bafd5a)

DAU = 76 млн
MAU = 103 млн

## Источники
официальный отчет вк - https://corp.vkcdn.ru/media/files/RUS_Press_Release_9M_2024.pdf

## 2. Расчет нагрузки
### Продуктовые метрики
Таблица 1 - Количество активных пользователей
<table>
    <tr>
        <th>Период</th>
        <th>Количество пользователей</th>
    </tr>
    <tr>
        <td>День</td>
        <td>76 миллиона</td>
    </tr>
    <tr>
        <td>Месяц</td>
        <td>103 миллиона</td>
    </tr>
</table>

Таблица 2 - Средний размер хранилища пользователя
<table>
    <tr>
        <th>Тип хранилища</th>
        <th>Средний объем на 1 пользователя</th>
    </tr>
    <tr>
        <td>Подписки</td>
        <td>В среднем id канала занимает 12 символов. Предположем, что у пользователя 40 подписок, в таком случает размер = 12 * 40 = 480 байт </td>
    </tr>
  <tr>
        <td>История просмотров</td>
        <td>Всего в день просматривают 4.3 млрд минут, т.е. один пользователь стратит в среднем 4.3 * 10^9 / (76 * 10 ^6) = 56.5 минут. По ютубовской статистики пользователь тратит +- 1/3 на шортсы, 2/3 на длинные видео.
        Если средняя длина шортса = 30 секунд, то пользователь за день просматривает 38 коротких видео. Длинное видео длится в районе 20 минут, значит пользователь успевает посмотретьт еще 2 видео. Итого 38 + 2 = 40.
        Id видео состоит из 19 символов, 18 цифр и одно нижнее подчеркивание. Если нужно хранить историю за последний месяц, то получится следующий результат: 18 * 40 * 31 = 22 320 байт = **21.8 Кбайт**</td>
    </tr>
</table>

Таблица 3 - Действия пользователей по типам
<table border="1">
    <tr>
        <th>Тип действия</th>
        <th>Среднее количество в день</th>
    </tr>
    <tr>
        <td>Воспроизведение видео</td>
        <td>В среднем пользователь смотрит 38 шортс и 2 длинных видео в день, всего: 76 * (38 + 2) = <b>3,04 млрд</b> просмотров</td>
    </tr>
    <tr>
        <td>Авторизация/регистрация</td>
        <td><b>76 млн</b></td>
    </tr>
    <tr>
        <td>Лайк/дизлайк видео</td>
        <td>В среднем пользователь ставит 3 реакции в день, всего: 76 * 3 = <b>228 млн</b></td>
    </tr>
    <tr>
        <td>Комментарии под видео</td>
        <td>В среднем 1% пользователей комментируют видео, всего: 76 * 0,01 = <b>0,76 млн</b> комментариев</td>
    </tr>
    <tr>
        <td>Поиск видео</td>
        <td>В среднем пользователь делает 2 поиска в день, всего: 76 * 2 = <b>152 млн</b></td>
    </tr>
    <tr>
        <td>Просмотр видео из рекомендаций</td>
        <td>В среднем 10 видео в день на пользователя, всего: 76 * 10 = <b>760 млн</b></td>
    </tr>
    <tr>
        <td>Просмотр видео из подписок</td>
        <td>В среднем 3 видео в день на пользователя, всего: 76 * 3 = <b>228 млн</b></td>
    </tr>
</table>


### Технические метрики
Таблица 4 - Размер хранения в разбивке по типам данных
<table >
    <tr>
        <th>Тип хранения</th>
        <th>Размер</th>
    </tr>
    <tr>
        <td>Пользователи</td>
        <td>На одного пользователя необходимо (0.5 + 21.8) = 22.3 КБ, тогда на 76 млн пользователей потребуется <b>1616 ТБ</b>. Учитывается только подписки и история просмотров. Информация по хранению данных видео отсутствует.</td>
    </tr>
    <tr>
        <td>Видео</td>
        <td>Средний размер видео: 22.5 МБ (шортс) и 900 МБ (длинные). Видео в расчетах имеют параметры: 1080р и 30 fps. 
            Из данных [статьи](https://kz.kursiv.media/2025-02-19/lfst-rtgm-youtube-2/?utm_source=chatgpt.com)  5% видосов выходит на русском языке. VPN постоянно пользуются в районе 30%. Поэтому поднимим до 10 % видео на русском языке.
           => из 14.8 млрд видео * 0.1 = 1.48 млрд в год. Из шортс и обычные видео относятся как 80:20. 1.48 * 10^9 * 0.8 * 22.5 = 2.7 * 10^10 МБ на шортс = <b>24 405 Петобайт</b>. Длинные видео 1.48 * 10^9 * 0.2 * 900 = 2.7 * 10^11 МБ = <b> 254 058 Петобайт </b> </td>
    </tr>
</table>

Таблица 5 - Сетевые метрики
<table>
    <tr>
        <th>Тип действия</th>
        <th>Пиковое потребление в течение суток, Гбит/с</th>
        <th>Суммарный суточный, Гбайт/сутки</th>
        <th>RPS (средний)</th>
        <th>RPS (пиковый)</th>
    </tr>
    <tr>
        <td>Воспроизведение видео</td>
        <td>10 000 000 * 5 Мбит/с = <b>50 000 Гбит/с</b></td>
        <td>76 млн * 40 мин * 60 с * 5 Мбит/с = <b>1 140 000 ГБ</b></td>
        <td>Средний пользователь смотрит 40 минут видео в день, запрос на новый фрагмент каждые 5 секунд, RPS = 76 млн *
            40 * 12 / 86400 = <b>422 000</b></td>
        <td>В пике 10 млн пользователей одновременно, RPS = 10 000 000 / 5 = <b>2 000 000</b></td>
    </tr>
    <tr>
        <td>Авторизация/регистрация</td>
        <td>10 * 16Кбайт / 2^20 = 150. Это если пользователи зайдут одновоременно, разобьем посекндно: 150 / 3600 = 0.04</td>
        <td>Сетевой трафик одного запроса - 16Кбайт, тогда 76млн * 16Кбайт / 2^20 = 1159</td>
        <td><b>5 млн. Распределим рпвномерно по часу: 5 000 000 / 3600 = 1388</b></td>
        <td><b>10 млн (в пиковые часы). 10 000 000 / 3600 = 2777</b></td>
    </tr>
    <tr>
        <td>Лайки/дизлайки</td>
        <td>payload будет в районе 300 байт, итого eth 2 будет весить в районе 600 байт. 20млн * 0.6Кбайт / 2^20 = 11. 11 / 3600 = 0.003</td>
        <td>228млн * 0.6 / 2^20 = 130</td>
        <td>76 млн * 3 = <b>228 млн в день. 228 000 000 / 24 / 3600 = 2638 </b></td>
        <td><b>20 млн</b></td>
    </tr>
    <tr>
        <td>Комментарии</td>
        <td>Средний размер кадра eth 2 будет 1 Кбайт. 100тыс * 1Кбайт / 2^20 = 0.09. 0.09 / 3600</td>
        <td>0.76 * 1Кбайт / 2^20 = 0.72 </td>
        <td>76 млн * 0,01 = <b>0,76 млн в день. 760 000 / 24 / 3600 (короче, очень мало)</b></td>
        <td><b>100 тыс</b></td>
    </tr>
    <tr>
        <td>Поиск видео</td>
        <td>15млн * 1 / 2^20 = 14.3. 14.3 / 3600 = 0.004</td>
        <td>152млн * 1 / 2^20 = 145 </td>
        <td>76 млн * 2 = <b>152 млн.</b></td>
        <td><b>15 млн</b></td>
    </tr>
</table>


