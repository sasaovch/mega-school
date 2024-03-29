# ML System Design Doc - [RU]

## Дизайн ML системы - Система оптимизации производства пиццы

## Автор: Овчаренко Александр

### 1. Цели и предпосылки

#### 1.1. Зачем идем в разработку продукта?

##### 1.1.1. Бизнес-цель

Увеличить эффективность производства пиццы в сети ресторанов, сократив время приготовления и улучшив качество продукции.

##### 1.1.2. Почему станет лучше, чем сейчас, от использования ML

1. Прогноз потребностей: Модели машинного обучения могут обучаться на исторических данных о продажах и автоматически предсказывать будущую востребованность различных видов пиццы. Это снизит отходы продуктов, позволит оптимально использовать ресурсы и услуги, а также улучшит уровень обслуживания клиентов за счёт сокращения времени ожидания. 

2. Оптимизация обучения персонала: На основе данных о производительности работников, ML-модель может помочь определить, какие навыки требуют улучшения, и предложить персонализированные обучающие модули для каждого сотрудника.

3. Улучшение качества пиццы: ML может быть использован для анализа обратной связи от клиентов, чтобы выявить тонкие проблемы с качеством пиццы, которые могут быть незаметны для человека. Опираясь на эти данные, пиццерия может совершенствовать свои рецептуры и методы приготовления.

4. Эффективное управление оборудованием: ML может помочь анализировать данные о работе кухонного оборудования, например, печи для пиццы, предсказывать их потребность в обслуживании или ремонте и оптимизировать расписание их использования, чтобы максимизировать производительность и уменьшить простои.

5. Личные предложения для клиентов: На основе анализа заказов и предпочтений клиентов, системы машинного обучения могут делать персонализированные предложения, увеличивая таким образом продажи и уровень удовлетворенности клиентов.

##### 1.1.3. Что будем считать успехом итерации с точки зрения бизнеса

1. Увеличение эффективности производства: Удалось ли снизить потери продуктов и повысить производительность персонала.

2. Сокращение времени приготовления: Значимое сокращение времени обработки заказов и приготовления пиццы.

3. Повышение качества продукции: Увеличение общего уровня удовлетворенности клиентов и снижение количества бракованных пицц.

4. Выполнение проектного плана: Завершились ли все запланированные этапы и задачи в соответствии с расписанием и бюджетом проекта.

5. Интеграция системы: Была ли система успешно интегрирована в текущую инфраструктуру без значительных проблем или сбоев.

6. Переход на новую систему: Сколько легко и быстро работники относятся к использованию новой системы, а также уровень поддержки и обучения, который потребовался для этого.

7. Повышение продаж или прибыли: В последней итерации успешность может также выражаться через конечные финансовые показатели, такие как увеличение продаж или прибыли.

#### 1.2. Бизнес-требования и ограничения

##### 1.2.1. Сбор данных о производственном процессе приготовления пиццы

1. Продукты для приготовления
Есть продукты, которые используются в во всех пиццах: тесто, вода, мука, соль, есть продукты, которые используются только в определенных. Для каждого типа пиццы нужно знать, в каком количестве, цену каждого продукта, время их приготовления и срок годности.

2. Этапы приготовления пиццы
Подробное описание каждого этапа приготовления, начиная от приготовления ингредиентов (например, нарезка овощей, соусов) до выпечки и упаковки: приготовление ингредиентов, замешивание и раскатывание теста, нанесение соуса, нарезка и раскладка ингредиентов, выпечка, выкладка пиццы и упаковка, проверка качества.

3. Время приготовления
Для каждого вида пиццы требуется свое время приготовления. Учитываем время с момента начала подготовки основы для пиццы до момента, когда пиццу можно будет отдавать клиенту или на упаковку для транспортировки. Также нужно собрать данные, сколько времени уходит на каждый из этапов

4. Оборудование
Список оборудования, используемого на кухне для приготовления пиццы, их ёмкость, скорость работы, время ожидания и производительность.

5. Персонал
Количество работников на пицце, их навыки, производительность, графики и готовность к работе, колличество вспомогательного персонала.

6. Поток заказов
Количество заказов в разные дни недели и время суток, среднее время ожидания заказа для клиента.

7. Отзывы клиентов

8. Брак
Сведения о количестве и причинах брака на каждом этапе производства.

##### 1.2.2. Определение бизнес-целей системы

1. Увеличение эффективности производства:
   - Снизить отходы продуктов на 20% за год путем оптимизации процесса порционирования и улучшения управления запасами.
   - Увеличить производительность работников на 15% в течение ближайших шести месяцев за счет автоматизации рутинных задач и обучения персонала.

2. Сокращение времени приготовления:
   - Сократить общее время приготовления пиццы на 10% в течение ближайших 6 месяцев за счет улучшения рабочих процессов и внедрения автоматизированных систем управления.
   - Уменьшить время ожидания заказа для клиента на 15% за следующий квартал благодаря оптимизации процесса обработки заказов.

3. Повышение качества продукции:
   - Увеличить посетительский рейтинг качества пиццы на платформах обратной связи на 10% в течение следующих 12 месяцев, внедряя системы контроля качества и обучая персонал.
   - Снизить процент бракованных пицц на 20% в течение следующего полугодия путем улучшения процесса приготовления и контроля качества.

##### 1.2.3. Функциональные требования

1. Система должна отслеживать, сколько и какие продукты используются при производстве пиццы. Обнаруживать избыточное использование продуктов и сигнализировать об этом.

2. Система должна предлагать оптимизацию процессов для улучшения качества и эффективности производства.

3. Система должна автоматически собирать и анализировать отзывы клиентов, выявлять проблемные области и предлагать улучшения.

4. Система должна включать инструменты для обучения и оценки персонала, включая тренинги по улучшению навыков.

##### 1.2.4. Неефункциональные требования

1. Система должна быть способна обрабатывать большие объемы данных без сбоев и задержек.

2. Все данные должны храниться в безопасном виде, допуск к ним должен быть строго регулируемым.

3. Система должна быть способна взаимодействовать с существующими IT-системами ресторана — складскими и бухгалтерскими системами, системами доставки и т.д.

4. Система должна быть масштабируемой, чтобы справляться с увеличением количества данных и пользователей в будущем.

5. Возможность обновления системы и поддержки в случае возникновения проблем или необходимости дальнейших улучшений.

##### 1.2.5. Ограничения

1. Технические ограничения:
   - Не всё оборудование в пиццерии может быть подключено к системе для отслеживания его работы и состояния, автоматизация процессов может быть неполной.
   - Не все сотрудники пиццерии могут быть компьютерно грамотными или иметь опыт работы с подобными системами, что затруднит использование системы.

2. Организационные ограничения:
   - Не все зоны пиццерии могут иметь доступ к компьютерам или интернету для работы с системой.
   - Бюджет на внедрение такой системы ограничен.

3. Законодательные ограничения:
   - В соответствии с законодательством, система должна обеспечивать безопасное хранение и обработку персональных данных сотрудников и клиентов.
   - Пиццерия должна следовать пищевым и гигиеническим стандартам, что может ограничивать внедрение некоторых технологий или изменений в процессах.

#### 1.3. Что входит в скоуп проекта/итерации, что не входит

1. В скоуп данной итерации входит:

- Разработка модели предсказания потребности в ингредиентах для определения оптимальных объемов закупок и сокращения потерь (с целью снизить потери на 15%).
- Разработка и тестирование модулей управления обучением персонала для увеличения производительности персонала (с целью повышения производительности на 10%).
- Внедрение системы анализа отзывов клиентов с интеграцией машинного обучения для улучшения качества продукции.
- Настройка и тестирование системы автоматического сбора данных об использовании оборудования для улучшения процессов обслуживания.

2. Что не входит в скоуп данной итерации:

- Разработка и внедрение системы управления заказами клиентов и доставкой. Это предполагается к выполнению в будущих итерациях.
- Обучение персонала и внедрение системы. Этап внедрения и обучения персонала будет рассмотрен после успешного тестирования и утверждения системы.

3. Результат с точки зрения качества кода и воспроизводимости:

- Весь код должен быть написан в соответствии с принятыми стандартами и лучшими практиками, включая комментарии и документацию.
- Решения должны быть воспроизводимыми. Это значит, что любой другой разработчик должен иметь возможность запустить и протестировать код с минимальными или без усилий, поэтому все скрипты и инструкции должны быть включены в исходный код.

4. Технический долг:

- Возможно понадобится время для оптимизации кода после завершения первоначального проекта, включая его рефакторинг и улучшение эффективности.
- Некоторые возможности, такие как дополнительные функции аналитического дашборда или интеграция с другими системами, могут быть оставлены для будущего разработчика с тем, чтобы сфокусироваться на основных функциональных требованиях в текущей итерации.

#### 1.4. Предпосылки решения  

Для успешной реализации системы оптимизации производства пицц, есть ряд предпосылок, которые мы предполагаем:

- Блоки данных:
    - Исторические данные о продажах: Эти данные понадобятся для моделирования прогнозирования спроса. Мы предполагаем, что у нас есть достаточное количество данных, соответствующих всем видам пиццы в меню, для обучения надежной модели.
    - Обратная связь от клиентов: Мы предполагаем, что у нас есть доступ к историческим отзывам клиентов, которые могут быть использованы для усовершенствования рецептур и методов производства.
    - Данные о производственном процессе: Мы предполагаем, что у нас есть подробная информация о каждом этапе производства каждой пиццы, включая использованные ингредиенты, затраты времени на персонал и оборудование, и статус (успешно завершено, отменено, брак и т.д.).

- Горизонт прогноза: Мы предполагаем, что наша модель будет способна прогнозировать спрос на следующую неделю (или другой соответствующий период времени), чтобы обеспечить достаточное время для занесения заказов на закупку и планов персонала.

- Гранулярность модели: Мы предполагаем, что модель будет работать на уровне отдельных видов пиццы, поскольку вариативность в спросе и процессе производства будет значителен для каждого вида. Мы предполагаем, что размер гранулы будет достаточным для того, чтобы обеспечить точные прогнозы, и не слишком большим, чтобы усложнить модель.

- Интеграция с оборудованием: Мы предполагаем, что у нас есть возможность интегрироваться с существующим оборудованием на предприятии (например, с печами для пиццы), чтобы собирать данные о их использовании.

- Обучающие данные для персонала: Мы предполагаем, что у нас есть доступ к информации о производительности персонала и их обучающим материалам, которая может быть использована для создания и оптимизации обучающих модулей.

### 2. Методология

#### 2.1. Постановка задачи  

Система будет выполнять следующие функции:

- Прогнозирование: Система будет использовать исторические данные о продажах для прогнозирования будущих потребностей в ингредиентах и пицце. Такое прогнозирование поможет оптимизировать закупки, уменьшить потери и улучшить обслуживание клиентов, уменьшив время ожидания.

- Оптимизация: Система будет стремиться оптимизировать различные процессы в пиццерии, такие как обучение персонала и использование оборудования. Это будет сделано путем анализа собранных данных и поиском путей улучшения существующих процессов.

#### 2.2. Этапы решения задачи

##### 2.2.1. Прогнозирование потребностей

1. Сбор данных: На этом этапе происходит сбор исторических данные о продажах различных видов пицц в пиццерии, включая даты и время продаж, а также какие именно ингредиенты использовались в каждой пицце. Данные беруться из открытых источников, данных, которые кампания имеет на текущий момент

2. Предобработка данных: Очистка и подготовка данных, что может включать в себя обработку пропущенных значений, нормализацию числовых значений и преобразование категориальных значений в подходящий формат.

3. Обучение модели: Обучение модели на подготовленных данных

4. Тестирование модели: Модель будет тестироваться для оценки ее точности и надежности.

5. Интеграция модели: После проверки и утверждения модель будет интегрирована в систему пиццерии для автоматического прогнозирования потребностей в ингредиентах.

##### 2.2.2. Оптимизация процессов

1. Сбор данных: На этом этапе происходит сбор исторических данные о продажах различных видов пицц в пиццерии, включая даты и время продаж, а также какие именно ингредиенты использовались в каждой пицце. Данные беруться из открытых источников, данных, которые кампания имеет на текущий момент

2. Предобработка данных: Очистка и подготовка данных, что может включать в себя обработку пропущенных значений, нормализацию числовых значений и преобразование категориальных значений в подходящий формат.

3. Выделение путей оптимизации: С помощью техник анализа данных и машинного обучения разработать пути для улучшения процессов производства.

4. Реализация и тестирование изменений: Изменения в процессах, предложенные на предыдущем этапе, будут реализованы и тестироваться для оценки их эффективности.

5. Масштабирование и интеграция изменений: Эффективные изменения будут масштабированы на все процессы производства и интегрированы в систему.
  
### 3. Подготовка пилота  
  
#### 3.1. Способ оценки пилота  

Для оценки пилота будем использовать А/В тестирование, где сравним результаты с использованием новой системы (группа А) и без нее (группа B, контрольная группа) для нескольки похожих пиццерий.

1. Выбор параметров: Определяем ключевые показатели эффективности (KPI), которые будут использоваться для оценки эффективности системы, например, время приготовления пиццы, уровень отходов, удовлетворенность клиентов и т.д.

2. Идентификация групп: Одна или несколько пиццерий (или линии производства внутри одной пиццерии) будут выбраны для использования системы (группа А), в то время как другие пиццерии продолжат работать в обычном режиме (группа В).

3. Проведение пилота: В течение определенного периода времени (скажем, две недели или месяц), мы будем сравнивать результаты группы А и группы В. 

Способ оценки пилота

1. Сбор данных: В течение пилотного периода будут собираться данные о ключевых показателях эффективности в обеих группах.

2. Анализ результатов: По окончании пилотного периода результаты группы А и В будут сравниваться с помощью соответствующих статистических методов (например, t-теста) для определения наличия значимых различий.

3. Оценка результата: Если группа А показывает заметное улучшение ключевых результатов по сравнению с группой B, это будет рассматриваться как успешное завершение пилотного теста.

4. Дальнейшее масштабирование: Если пилот успешен, система будет далее внедряться в другие пиццерии или линии производства. Если результаты неудовлетворительные, система будет доработана до нового пилотного тестирования или проект может быть пересмотрен.

#### 3.2. Что считаем успешным пилотом  
  
1. Снижение времени приготовления пиццы: среднее время приготовления  изначально было 30 минут, можно установить целью снижение этого времени на 15% до приблизительно 25 минут.

2. Уменьшение отходов: снижении потерь продуктов на 20%

3. Улучшение удовлетворенности клиентов: средний рейтинг вырос с 4.0 до 4.3 

4. Повышение объемов продаж: Успехом также можно считать заметное повышение объемов продаж, например, увеличение на 10% относительно предыдущего периода.

5. Снижение стоимости обслуживания оборудования: Если система была рассчитана на прогнозирование технического обслуживания оборудования, то снижение стоимости обслуживания на 15% может служить метрикой для оценки успешности.

### 4. Внедрение

#### 4.1. Архитектура решения

1. Data Layer (Слой данных): Этот слой будет включать существующую базу данных пиццерии, хранящую информацию о продажах, заказах, ингредиентах, персонале и оборудовании. Этот слой может включать Data Warehouse или Data Lake в зависимости от специфики хранения данных.

2. Data Processing Layer (Слой обработки данных): Этот слой специализируется на предобработке и трансформации данных. Здесь могут быть использованы такие инструменты, как Apache Spark для эффективной обработки больших объемов данных.

3. Machine Learning Layer (Слой машинного обучения): Здесь будут обучаться и тестироваться модели машинного обучения. Этот слой будет включать инструменты, такие как TensorFlow, PyTorch, Scikit-learn и другие специализированные библиотеки для построения и обучения моделей.

4. Application Layer (Слой приложения): Это основное приложение, которое будет использоваться персоналом пиццерии. Он будет обеспечивать предсказания модели и оптимизированные рекомендации в удобном пользовательском интерфейсе.

5. Monitoring & Logging Layer (Слой мониторинга и логирования): Этот слой будет отвечать за мониторинг производительности системы и запись важных данных или событий для отладки и оптимизации. Инструменты, такие как Elasticsearch, Logstash и Kibana (ELK stack), могут использоваться для управления этими процессами.

#### 4.2. Инфраструктура и масштабируемость

- Инфраструктура будет развернута в облаке для удобства масштабирования и доступности. Это позволит масштабировать систему без значительных издержек.
- Хранилище данных. Централизованное хранилище для исторических данных о заказах и предпочтениях клиентов.
- Облачные вычисления. Использование платформ облачных вычислений для гибкости и масштабируемости.
- Фреймворк машинного обучения. Выбор популярного фреймворка, такого как TensorFlow или PyTorch.

#### 4.3. Требования (SLA, пропускная способность и задержка)

- SLA (Service Level Agreement): Система должна быть доступна 99.9% времени. Но к критически важным компонентам, таким как сопровождение сотрудников, обеспечение информацией о заказах и составлении порядка выполнения заказов требуется доступность 99.999% времени.

#### 4.4. Безопасность системы

Потенциальная уязвимость системы обычно связана с несанкционированным доступом, манипуляцией данных или атаками на отказ в обслуживании (DoS). Для обеспечения безопасности важно внедрить следующие меры:

- Организация сетевой безопасности, включая использование брандмауэров и отдельных сегментов сети.
- Регулярное обновление и патчинг системы для устранения уязвимостей и обеспечения совместимости с последними стандартами безопасности.
- Использование шифрования при обмене и хранении данных.
- Управление доступа и аутентификация пользователей.
  
#### 4.5. Безопасность данных

Все данные, собираемые и обрабатываемые системой, должны соответствовать GDPR и другим местным законам о защите данных. Как правило, мы должны обеспечивать следующее:

- Получать согласие пользователей на сбор и обработку их данных.
- Уведомлять пользователей о целях сбора и обработки данных.
- Предоставлять возможность пользователям проверять и корректировать свои данные.
- Уничтожать данные, когда они уже не нужны для целей, ради которых они были собраны.

#### 4.6. Издержки

Стоимость работы системы в месяц будет зависеть от многих факторов, включая:

- Стоимость использования оборудования и облачного хостинга.
- Стоимость поддержания и обновления системы.
- Стоимость использования сторонних сервисов или API.
- Стоимость рабочего времени персонала, занятого поддержкой системы.
  
#### 4.7. Точки интеграции

Система будет взаимодействовать с остальной инфраструктурой пиццерии через API. Это может включать:

- API для получения данных о продажах, заказах, персонале и оборудовании.
- API для передачи прогнозов и рекомендаций обратно в систему пиццерии.
  
#### 4.6. Риски

- Потенциальное несоответствие прогнозов реальным данным, что может привести к отклонениям в планировании и управлении.
- Технические проблемы или ошибки, которые могут привести к прерыванию работы или некорректному выполнению системы.
- Неспособность персонала пиццерии эффективно использовать систему или сложности внедрения новой системы.
- Потенциальные угрозы безопасности данных и системы.
- Несоответствие законодательству о защите данных.
