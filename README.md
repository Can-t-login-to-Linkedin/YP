# Хакатон : Исследование LinkdedIn

## Цели и задачи
Целью работы является проведение исследование по теме наставничества и менторства на основании контента социальной сети Linkedin, размещенного в открытом доступе, созданного целевой аудиторией.

Были поставлены следдующие задачи:
* Сбор данных 
* Предобработка данных 
* Тематическое моделирование

## Parcing 
В исследовании были задействованы 3 парсера.
- первый осуществлял сбор анкет пользователей, их данные (место, опыт работы, стаж) , а также все посты, которые они написали или лайкнули
- второй осуществлял сбор постов по ключевым словам ("наставничество it", "ментор it", "преподавание it", "прокачать soft skills")
во втором случае собирался текст поста и краткая информация о юзерах, которым этот пост понравился
- третий осуществлял сбор анкет сотрудников выбранных компаний, их данные (аналогично первому) , все посты, которые они написали или лайкнули.

Из-за встроенной блокировки парсинга LinkedIn, было собрано `542` поста по запросам на тему наставничество и `556` профилей пользователей с информацией о них и `1600` постов, на которые эти пользователи реагировали. Очевидно, этих данных не достаточно для проведения полноценного исследования. 

## Data preprocess
* В рамках предобработки данных отфильтровали профили специалистов попадающих под критерии целевой аудитории.

## Modeling
### LDA
в качестве baseline решения была выбрана модель LatentDirichletAllocation. Для этого были проведены следующие шаги.
- Очистка текстов
- Лемманизация 
- TF-IDF

### BERTopic:
модель представляет из себя модульную конструкцию, в которой пользователь по своему усмотрению может менять ее части
- сначала получаются эмбединги (модель пользователь выбирает сам)
- проводится кластеризация (нами были опробованы HDBSCAN и KMeans), лучших результатов удалось добиться с помощью HDBSCAN
- проводится токенизация (CountVectorizer со списком стоп-слов) и взвешивание TF-IDF

## Выводы
- Проведен сбор данных 3мя способами.
- 
- 
