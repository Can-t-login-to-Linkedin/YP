# Хакатон : Исследование LinkdedIn

## Цели и задачи
Целью работы является проведение исследование по теме наставничества и менторства на основании контента социальной сети Linkedin, размещенного в открытом доступе, созданного целевой аудиторией.

Были поставлены следдующие задачи:
* Сбор данных 
* Предобработка данных 
* Тематическое моделирование

## Parsing 
Модули парсинга лежат в `parser.ipynb`
В исследовании были задействованы 3 парсера.
- первый осуществлял сбор анкет пользователей, их данные (место, опыт работы, стаж) , а также все посты, которые они написали или лайкнули
- второй осуществлял сбор постов по ключевым словам ("наставничество it", "ментор it", "преподавание it", "прокачать soft skills")
во втором случае собирался текст поста и краткая информация о юзерах, которым этот пост понравился
- третий осуществлял сбор анкет сотрудников выбранных компаний, их данные (аналогично первому) , все посты, которые они написали или лайкнули.

Из-за встроенной блокировки парсинга LinkedIn, было собрано `542` поста по запросам на тему наставничество и `556` профилей пользователей с информацией о них и `1600` постов, из них `793` на русском, на которые эти пользователи реагировали. По нашему мнению, этих данных не достаточно для проведения полноценного исследования. 

## Data preprocess
`primary_preprocessing.ipynb`
* В рамках предобработки данных отфильтровали профили специалистов попадающих под критерии целевой аудитории.

## Modeling
### LDA
`Topic_modeling_LDA.ipynb`

в качестве baseline решения была выбрана модель LatentDirichletAllocation. Для этого были проведены следующие шаги.
- Очистка текстов
- Лемманизация 
- TF-IDF

### BERTopic:
`berttopic_example.ipynb`
модель обучалась `1335` постах (793 поста на русском языке из анкет + 542 поста по запросу наставничество)

модель представляет из себя модульную конструкцию, в которой пользователь по своему усмотрению может менять ее части
- сначала получаются эмбединги (модель пользователь выбирает сам)
- проводится кластеризация (нами были опробованы HDBSCAN и KMeans), лучших результатов удалось добиться с помощью HDBSCAN
- проводится токенизация (CountVectorizer со списком стоп-слов) и взвешивание TF-IDF
- лемматизация в данном случае не требуется, т.к. под капотом эмбединги получаются с помощью трансформера, а в топ-10 слов есть "алгоритм разнообразия" (цитата разработчика). проверяли, ухудшает результат

## Возникшие проблемы
- в результаты выдачи частично попали посты на других киррилических языках(украинский, болгарский и т.д.), которые некорректно отфильтровываются существующими  библиотеками

## Результаты
- Были выбраны результаты работы модели BERTopic.
- Результаты работы представлены в `reactions.csv`, `posts.csv`. Топ-10 слов по топ-10 темам переданы рекрутеру.
