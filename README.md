# graduatework
Дипломная работа в Нетологии по направлению Аналитик данных
Постановка задачи
Чемпионат мира по футболу - очень важное события для игроков с точки зрения того, как можно презентовать себя. Показав хорошую статистику на чемпионате, игрок может рассчитывать на попадание в более престижные клубы. Такая статистика актуальна, как для самих игроков, так и для их личных менеджеров, менеджеров клубов, и “hunter-ов”, кто подбирает игроков по заказу.
Стейкхолдерами данной задачи будут агенты футболистов, менеджеры клубов и профессиональные подборщики игроков. Опираясь на информацию о статистике игроков, они смогут выбрать лучших. 
Часто для оценки футболистов используется только система очков гол + пас. Требованием к расчету качества футболистов в данном случае было выведение параметра, учитывающего многие показатели (количество фолов, процент выигранных единоборств, процент перехватов и т.д.), а также возможность смотреть на статистику под разными углами (например в зависимости от позиции на поле). Источником данных послужила информация, собираемая системой VAR FIFA.
Анализ
Для анализа взяты данные по статистике игроков по результатам чемпионата мира 2022 с сайта kaggle.com 
https://www.kaggle.com/datasets/rhugvedbhojane/fifa-world-cup-2022-players-statistics?select=FIFA+WC+2022+Players+Stats.csv , а также дополнительные данные с различных источников.
Как аналог подобной статистики изучены таблицы лучших игроков чемпионата: https://metaratings.ru/chempionat-mira-po-futbolu-fifa/statistika-igrokov/ , а также информация с основных спортивных СМИ (Sports.ru, Sport-express.ru). Все перечисленные источники не содержат подробной информации о статистике игроков, а лишь приводят ТОПы лучших.
Проведено предварительное изучение данных:
Чтение данных https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=F_HY-elg9TFN&line=1&uniqifier=1 
Основная информация о данных https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=w21EOFXG-AOW&line=1&uniqifier=1 выявлены параметры с большинством значений NaN, также выявлено явное несоответствие типов данных
Данные очищены от нежелательных символов https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=ck3KRqYtOF5_&line=1&uniqifier=1 
Для выявления лучших игроков чемпионаты выбрана статистика “total player rank”, вычисляемый столбец, показывающий общий рейтинг игрока. 
Данный показатель рассчитывается по-своему для игроков разных ролей, так для нападающих: основной характеристикой для рейтинга будем считать количество забитых голов, а дополнением нормализованную сумму остальных характеристик. Полученные значения суммируем и делим на количество сыгранных матчей. Такая статистика не отрицает, что забиваемые голы - важный показатель, но также учитывает и все остальные показатели игрока.
Для защитников суммируем характеристики, связанные с игрой в отборе мяча и отнимаем количество нарушений. Полученные значения суммируем и делим на количество сыгранных матчей.
Для полузащитников усредняем показатель нападающих и защитников. Для вратарей вычисляем отношение ударов по воротам к пропущенным мячам, добавляя сейвы и выигранные единоборства.
Отчет будет представлен в виде дашборда в Google Data Studio

3. Методика решения
Произведен EDA анализ данных:
данные очищены от непараметрических показателей, не влияющих на статистику https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=8YUdtbwxPyfD&line=2&uniqifier=1 
исключены данные, имеющие значения большинства статистических показателей NaN https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=w24WhMVrH6tq&line=4&uniqifier=1 
проинтерпретировано значение параметра “Количество сыгранных матчей” = 0, такие игроки не выступали на чемпионате, они также исключены. https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=TsGpgx1cPHcx&line=1&uniqifier=1 
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=FehEqtVthv0Y&line=1&uniqifier=1 
параметр “дата рождения” переведен в параметр “возраст” https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=5L_QIqy5UQC1&line=5&uniqifier=1 
После разведочного анализа и очистки данные избавлены от пустых значений, от не влияющих на статистику показателей, все типы данных приведены в соответствие https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=qqc5QCKsVG6K&line=1&uniqifier=1 
Рассчитаны вычисляемые столбцы, отвечающие за определение основной статистики игроков https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=2AzxvfXge6-f&line=2&uniqifier=1 
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=LP4pSSSyQdRs&line=3&uniqifier=1
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=08NUyMnVQ_je&line=1&uniqifier=1
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=3f3L-FEZRoOz&line=1&uniqifier=1
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=X9xmv4NpL0xm&line=1&uniqifier=1 
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=4XjRwL8tYlvU&line=1&uniqifier=1 
Для итогового отчета сформирован общий DataFrame, содержащий в себе все значимые показатели игроков, а также вычисленные статистики. DataFrame записан в csv-файл https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=uVujNiKBdh11&line=2&uniqifier=1 
4. Результаты
С помощью рассчитанных статистик определены ТОП игроков чемпионата, а также ТОПы в различных срезах:
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=DwN11dGOs1Cc&line=1&uniqifier=1 
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=VXJy2affda4X&line=1&uniqifier=1
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=zXfYy46yf8TO&line=1&uniqifier=1
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=UJukZIzWgB7A&line=3&uniqifier=1 
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=bUxhnSbpdU8J&line=2&uniqifier=1 
Также найдены самые “эффективные” клубы. В разрезе среднего рейтинга: https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=rDHKa0ZBjG1l&line=1&uniqifier=1 
и по суммарно забитым голам: https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=fYcU3RTLlVgQ&line=5&uniqifier=1 
Отмечены самые нарушающие клубы и страны:
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=ux_33eLbeTsR&line=4&uniqifier=1
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=a3wqQFDdgI0V&line=3&uniqifier=1 
Частичная визуализация приведена в самом notebook в google colab. Построены гистограммы основных показателей лучших игроков: 
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=8hTUx2I6yOWm&line=2&uniqifier=1
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=q4NosPrRyVRA&line=2&uniqifier=1
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=HZ8PnbhUyb3r&line=1&uniqifier=1
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=Vow8gXWWdlXH&line=1&uniqifier=1
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=CbZZ4yCLe5DO&line=3&uniqifier=1
https://colab.research.google.com/drive/1ylrIpjuveqNhyf5pY049BWavwMi8-UNo#scrollTo=uMj23jO7gpcZ&line=1&uniqifier=1 
Основной отчет представлен в виде дашборда в google data studio: 
https://lookerstudio.google.com/reporting/0c453e5e-bddf-4209-9007-ff7ed3cc4d92 
5. Выводы и заключение
В проделанной работе выведена статистика, позволяющая определять уровень общей полезности игрока, учитывая множество второстепенных показателей. Такой подход позволит выявлять перспективных игроков, исходя не только из общепринятых показателей системы “гол+пас”.
Данную модель можно развивать и улучшать путем добавления большего количества характеристик, отражающих действия футболиста на поле. При достижении достаточного числа таких показателей в модели, можно будет отказаться от количества забитых мячей для форвардов, как главенствующего показателя. Но такое решения потребует проверки релевантности полученной модели. 
