<p align="center">
  <img src="https://i.redd.it/fv1flk6mg00d1.jpeg" width="100%">
</p>
<p align="center">
  <b>Data Analyst</b> · продуктовая аналитика и A/B-тестирование<br>
  Финансовый университет при Правительстве РФ — «Инженерия данных»
</p>

<p align="center">
  <img src="https://img.shields.io/badge/AA--тест-5.06%25%20FPR%20при%20alpha%200.05-2ea043" alt="AA-тест"/>
  <img src="https://img.shields.io/badge/автотестов-147%20бэкенд%20%2B%2058%20UI-2ea043" alt="тесты"/>
  <img src="https://img.shields.io/badge/сверено%20с-scipy%20·%20statsmodels-2ea043" alt="валидация"/>
</p>

<p align="center">
  <a href="https://t.me/kuznetsov_ghkl"><img src="https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram"/></a>
  <a href="https://mail.google.com/mail/?view=cm&fs=1&to=ilya.kuznetsov.ghkl@gmail.com"><img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Gmail"/></a>
</p>

---

## Проекты

| | Что это | Главное |
|---|---|---|
| **[ExperimentHub](https://github.com/kuznetsovskdh/ExperimentHub)** | Платформа A/B-тестов: CUPED, bootstrap, SRM, мощность, DiD | AA-тест — **5,06 %** ложных при alpha 0,05 · **147** автотестов |
| **[РусТест](https://github.com/kuznetsovskdh/rustest)** | Продуктовая аналитика на событийном логе живого продукта | Когортный retention · активационная воронка · **20** эндпоинтов |
| **[SellerTeller](https://github.com/kuznetsovskdh/Salesguard)** | Аналитика продаж WB/Ozon из «грязной» выгрузки | **9** форматов отчётов · ABC · маржа L1/L2 · RFM · прогноз |

<details>
<summary><b>Подробнее — методология и что нашло тестирование</b></summary>

<br>

**ExperimentHub.** Статистическое ядро написано и провалидировано самостоятельно —
не обёртка над `scipy.stats.ttest_ind`. AA-тест на 10 000 прогонов дал 5,06 % при
z-критерии и 4,99 % при тесте Уэлча; p-value сверены со `scipy` и `statsmodels` до 1e-5.

Тестирование нашло три ошибки в собственном коде:
- **CUPED** считал `theta` отдельно по группам → 25,6 % ложных срабатываний вместо 5 %.
  После перехода на общую `theta` — 4,8 %.
- **p-value и доверительный интервал описывали разные модели**: Стьюдент против Уэлча.
  На неравных дисперсиях давало p = 0,008 там, где честный ответ p = 0,315.
- **Ключ хэширования** склеивал `entity_id` и `experiment_id` без разделителя —
  пары `("1", 12)` и `("11", 2)` попадали в один бакет.

Отдельно измерена цена подглядывания: 26,8 % ложных «успехов» против 4,5 % при
честной остановке.

Реальный A/B на пользователях РусТеста: +31,1 пп, p = 0,026 — и решение **не внедрять**.
При мощности 60,6 % значимый результат систематически завышает эффект, нужна выборка
336 на вариант.

**РусТест.** Метрики считаются не на Kaggle-датасете, а на событиях живого продукта —
от регистрации до ответа на конкретный вопрос. Когортный retention: обе оси приведены
к календарным неделям, ненаступившая неделя отдаётся как `null`, а не как 0 % оттока.
Активационная воронка собирается из двух сервисов — событие регистрации живёт в
auth-service, поведение в result-service.

**SellerTeller.** Классификация типа отчёта стоит **до** нормализации: без неё
нормализатор считает ABC по акту сверки и выдаёт правдоподобный мусор. RFM и когорты
построены по SKU, а не по клиентам — в отчётах WB/Ozon нет идентификатора покупателя,
это свойство агентской модели продаж. 47,5 МБ / 175 000 строк обрабатываются за ~59 секунд.

</details>

---

## Стек

<p>
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" width="42" alt="Python"/>&nbsp;&nbsp;
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/postgresql/postgresql-original.svg" width="42" alt="PostgreSQL"/>&nbsp;&nbsp;
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/pandas/pandas-original.svg" width="42" alt="pandas"/>&nbsp;&nbsp;
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/docker/docker-original.svg" width="42" alt="Docker"/>&nbsp;&nbsp;
  <img src="https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg" width="42" alt="Git"/>
</p>

**Статистика и эксперименты** — проверка гипотез (t-test, z-test, хи-квадрат) ·
доверительные интервалы · мощность и расчёт размера выборки · CUPED · bootstrap ·
SRM · поправки Бонферрони и Беньямини—Хохберга · DiD

**Продуктовые метрики** — когортный retention · воронки активации · DAU/MAU ·
churn · RFM · ABC · unit-экономика

**Данные** — SQL · SQLAlchemy · NumPy · SciPy · statsmodels · scikit-learn ·
DBeaver · Power BI · Excel

<details>
<summary>Также работал с</summary>

<br>

<p>
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg" width="34" alt="Java"/>&nbsp;
  <img src="https://www.vectorlogo.zone/logos/springio/springio-icon.svg" width="34" alt="Spring"/>&nbsp;
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/react/react-original.svg" width="34" alt="React"/>&nbsp;
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" width="34" alt="JavaScript"/>&nbsp;
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original.svg" width="34" alt="MySQL"/>&nbsp;
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mongodb/mongodb-original.svg" width="34" alt="MongoDB"/>&nbsp;
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/redis/redis-original.svg" width="34" alt="Redis"/>&nbsp;
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/nginx/nginx-original.svg" width="34" alt="nginx"/>&nbsp;
  <img src="https://www.vectorlogo.zone/logos/figma/figma-icon.svg" width="34" alt="Figma"/>
</p>

Flask · FastAPI · TypeScript · Vite · Playwright · Plotly ·
Java / Spring (REST API, Hibernate, Maven, JavaFX) — коммерческая разработка

</details>

---

<p align="center">
  <b>Английский — C1.</b> Ищу задачи в продуктовой аналитике и экспериментах.
</p>

<p align="center">
  <img src="assets/snake.svg" alt="Contribution snake" />
</p>
