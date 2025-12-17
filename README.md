# GP3-repo
В readme файле содержится основная информация о второй части задания, а именно о датасете и в целом о том кто наш бизнес-заказчик и какую проблему мы решаем

Наш бизнес-заказчик: Страховая фирма, которая занимается частными мед страховками. Им нужно принять ряд управленческих решений по поводу выдаче мед страховок, чтобы оптимизирвать цены под категории клиентов, иначе компания теряет много денег на покрытии медицинских расходов для людей с диабетом, так как им требуется повышенный уровень обеспеченья комфортных условий и иногда проведение операций, которые обходятся компании страхвщику много больше, чем то, что человек уже оплатил за страховку

Исходные данные: https://archive.ics.uci.edu/dataset/891/cdc+diabetes+health+indicators

Основная информация об исходных данных:

| Variable Name           | Role    | Type    | Demographic      | Description                                                                                                                                                                                                                   | Units | Missing Values |
|-------------------------|---------|---------|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|----------------|
| ID                      | ID      | Integer |                  | Patient ID                                                                                                                                                                                                                    |       | no             |
| Diabetes_binary         | Target  | Binary  |                  | 0 = no diabetes; 1 = prediabetes or diabetes                                                                                                                                                                                 |       | no             |
| HighBP                  | Feature | Binary  |                  | 0 = no high BP; 1 = high BP                                                                                                                                                                                                   |       | no             |
| HighChol                | Feature | Binary  |                  | 0 = no high cholesterol; 1 = high cholesterol                                                                                                                                                                                |       | no             |
| CholCheck               | Feature | Binary  |                  | 0 = no cholesterol check in 5 years; 1 = yes cholesterol check in 5 years                                                                                                                                                    |       | no             |
| BMI                     | Feature | Integer |                  | Body Mass Index                                                                                                                                                                                                               |       | no             |
| Smoker                  | Feature | Binary  |                  | Have you smoked at least 100 cigarettes in your entire life? (5 packs = 100 cigarettes). 0 = no; 1 = yes                                                                                                                     |       | no             |
| Stroke                  | Feature | Binary  |                  | (Ever told) you had a stroke. 0 = no; 1 = yes                                                                                                                                                                                |       | no             |
| HeartDiseaseorAttack    | Feature | Binary  |                  | Coronary heart disease (CHD) or myocardial infarction (MI). 0 = no; 1 = yes                                                                                                                                                  |       | no             |
| PhysActivity            | Feature | Binary  |                  | Physical activity in past 30 days (not including job). 0 = no; 1 = yes                                                                                                                                                       |       | no             |
| Fruits                  | Feature | Binary  |                  | Consume fruit 1 or more times per day. 0 = no; 1 = yes                                                                                                                                                                       |       | no             |
| Veggies                 | Feature | Binary  |                  | Consume vegetables 1 or more times per day. 0 = no; 1 = yes                                                                                                                                                                  |       | no             |
| HvyAlcoholConsump       | Feature | Binary  |                  | Heavy drinkers (men >14 drinks/week, women >7 drinks/week). 0 = no; 1 = yes                                                                                                                                                  |       | no             |
| AnyHealthcare           | Feature | Binary  |                  | Have any kind of health care coverage, including health insurance, prepaid plans such as HMO, etc. 0 = no; 1 = yes                                                                                                           |       | no             |
| NoDocbcCost             | Feature | Binary  |                  | Time in past 12 months when you needed to see a doctor but could not because of cost? 0 = no; 1 = yes                                                                                                                        |       | no             |
| GenHlth                 | Feature | Integer |                  | General health: scale 1–5 — 1 = excellent; 2 = very good; 3 = good; 4 = fair; 5 = poor                                                                                                                                       |       | no             |
| MentHlth                | Feature | Integer |                  | Days during past 30 days when mental health was not good (stress, depression, emotional problems): scale 1–30 days                                                                                                           |       | no             |
| PhysHlth                | Feature | Integer |                  | Days during past 30 days when physical health was not good (illness or injury): scale 1–30 days                                                                                                                              |       | no             |
| DiffWalk                | Feature | Binary  |                  | Serious difficulty walking or climbing stairs? 0 = no; 1 = yes                                                                                                                                                               |       | no             |
| Sex                     | Feature | Binary  | Sex              | 0 = female; 1 = male                                                                                                                                                                                                          |       | no             |
| Age                     | Feature | Integer | Age              | 13-level age category (_AGEG5YR): 1 = 18–24; …; 9 = 60–64; 13 = 80 or older (см. codebook)                                                                                                                                   |       | no             |
| Education               | Feature | Integer | Education Level  | Education level (EDUCA): scale 1–6 — 1 = never attended school/only kindergarten; 2 = grades 1–8; 3 = grades 9–11;<br> 4 = grade 12 or GED; 5 = college 1–3 years; 6 = college 4+ years (college graduate)                        |       | no             |
| Income                  | Feature | Integer | Income           | Income scale Income scale scale 1-8 1 = less than $10,000 <br>5 = less than $35,000 <br> 8 = $75,000 or more                                                                                                                            |       | no             |

###feature engeneering который провел: 
1. **Логарифмирование BMI**

   * Добавлен признак
     `BMI_log = log(BMI)`.
   * Зачем: сгладить правый хвост распределения BMI и получить более “симпатичный” признак для визуализаций и возможных моделей (меньше влияние экстремальных значений).
---
2. **Индикатор ожирения**

   * Создан бинарный признак
     `Obese_flag = 1`, если `BMI ≥ 30`,
     `Obese_flag = 0` иначе.
   * Зачем: свести непрерывный BMI к клинически интерпретируемой категории «ожирение / нет», чтобы:

     * строить простые статистические тесты (χ² по таблице 2×2),
     * интерпретировать результат как риск диабета у людей с ожирением.
---
3. **Индексы “отсутствия” кардио-проблем и cardio_index**

   * Созданы бинарные признаки «нет проблемы»:

     * `NoHighBP = 1`, если нет повышенного давления;
     * `NoHighChol = 1`, если нет высокого холестерина;
     * `NoStroke = 1`, если не было инсульта;
     * `NoHeartDiseaseorAttack = 1`, если нет ИБС/инфаркта;
     * `NoDiffWalk = 1`, если нет затруднений при ходьбе.
   * На их основе построен интегральный индекс:

     * `cardio_index = NoHighBP + NoHighChol + NoStroke + NoHeartDiseaseorAttack + NoDiffWalk`
       (диапазон от 0 до 5, где **чем больше — тем лучше кардио-здоровье**).
   * Потом вспомогательные `No…`-признаки были удалены, оставлен только `cardio_index`.
   * Зачем: получить **одну числовую метрику состояния сердечно-сосудистой системы**, с которой удобно:

     * сравнивать группы (t-test Уэлча, Манн–Уитни),
     * интерпретировать результат (“у диабетиков кардио_index заметно ниже”).
---
4. **Индекс образа жизни (Lifestyle_score)**

   * Созданы промежуточные бинарные признаки:

     * `HealthyDiet_flag = 1`, если одновременно `Fruits = 1` и `Veggies = 1` (есть фрукты и овощи каждый день);
     * `NonSmoker_flag = 1`, если `Smoker = 0` (не курит);
     * `NoHeavyAlcohol_flag = 1`, если `HvyAlcoholConsump = 0` (нет тяжёлого употребления алкоголя).
   * Затем собран интегральный показатель:

     * `Lifestyle_score = NoHeavyAlcohol_flag + NonSmoker_flag + HealthyDiet_flag + PhysActivity`
       (значения от 0 до 4: чем больше, тем “здоровее” образ жизни).
   * Вспомогательные флаги позже удалены, оставлен итоговый `Lifestyle_score`.
   * Зачем: получить **одну компактную оценку ЗОЖ**, чтобы:

     * сравнивать средний уровень ЗОЖ у диабетиков и не-диабетиков (t-test Уэлча, Манн–Уитни),
     * использовать её как понятный фактор риска.
---
5. **Индекс социально-экономического статуса (soc_index)**

   * Создан признак:

     * `soc_index = Income + Education`.
   * Также добавлен бинарный флаг:

     * `LowIncome_flag = 1`, если `Income ≤ 3` (низкие доходы).
   * Зачем: совместить в одном показателе уровень дохода и образования, чтобы:

     * анализировать связь **соц-статуса и диабета** (t-test Уэлча по soc_index),
     * формулировать бизнес-выводы для страховой (группы с низким soc_index — более уязвимы).
---
6. **Группировка возраста**

   * Построена агрегированная возрастная группировка:

     * исходный `Age` (13 категорий CDC) преобразован в `Age_group_num` с 4 укрупнёнными группами:

       * 1: коды 1–3 → 18–34 года;
       * 2: 4–7 → 35–54;
       * 3: 8–9 → 55–64;
       * 4: 10–13 → 65+.
   * Зачем: упростить анализ зависимости диабета от возраста (heatmap, barplot, корреляция/групповые сравнения) и сделать результаты интерпретируемыми для бизнес-заказчика.
---
7. **Интегральный общий индекс (General_index)**

   * Создан составной показатель:

     * `General_index = cardio_index + Lifestyle_score + soc_index`.
   * Использовался в основном для разведочного анализа (распределение, связь с таргетом).
   * Зачем: посмотреть **общий “комбинированный” статус** (здоровье + образ жизни + соц-статус) и его связь с диабетом.

---

Статистические гипотезы представлены на защите проекта
