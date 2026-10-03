# Into-to-CI

**Causal ML: сравнение методов оценки эффекта воздействия**

Учебный проект, показывающий, почему A/B-тесты и наивное сравнение групп дают смещённые оценки при неслучайном назначении воздействия — и как разные методы причинного вывода решают (или не решают) эту проблему.

На примере синтетических данных «эффект высшего образования на зарплату» реализованы и сопоставлены 8 методов оценки причинного эффекта — от классического matching до Double Machine Learning.

---

## Содержание

- [О проекте](#о-проекте)
- [Методы](#методы)
- [Результаты](#результаты)
- [Главный вывод](#главный-вывод)
- [Как запустить](#как-запустить)
- [Стек](#стек)

## О проекте

Спроектирован синтетический data generating process (DGP) с контролируемым **ненаблюдаемым confounder'ом** (способности индивида) и **инструментальной переменной** (образование родителей) — это позволяет точно измерить bias каждого метода относительно истинного, заранее известного эффекта, а не гадать о нём на реальных данных.

## Методы

**Классические подходы к причинному выводу:**
- Propensity Score Matching и Mahalanobis matching
- Inverse Probability Weighting (IPW)
- Instrumental Variables (2SLS / Wald estimator)

**Causal ML:**
- Meta-learners: S-learner, T-learner, X-learner, R-learner
- Causal Tree (+ honest-подход)
- Causal Forest
- Double Machine Learning (Neyman orthogonality + cross-fitting)

## Результаты

| Метод | ATE-оценка | Смещение относительно истинного ATE |
|---|---|---|
| Истинный ATE (DGP) | 17 | 0 |
| Naive (разность средних) |25.2 | 8.2|
| Matching (Mahalanobis) | 20.97| 3.97|
| Matching (PSM) |20.87 |3.87 |
| IPW |20.95 | 3.95|
| IV (2SLS) |17.03 |0.04 |
| S/T/X/R-learner | 20.95| 3.95|
| Causal Tree |23.27 | 6.27|
| Causal Forest |21.03 |4.03 |
| DML |20.91 | 3.91|

## Главный вывод

Сложность ML-модели внутри метода не заменяет правильную идентификацию. Более гибкая модель (DML, causal forest) решает проблемы *оценивания* — переобучение, проклятье размерности, смещение из-за регуляризации, — но не проблему *нарушенного unconfoundedness*.

Matching, IPW, meta-learners, causal forest и DML опираются на одну и ту же предпосылку: unconfoundedness относительно наблюдаемых признаков. Ни один из них не видит ненаблюдаемый confounder, поэтому все дают смещённую оценку — хоть и заметно менее смещённую, чем наивное сравнение средних.

IV — единственный метод, использующий другую идентификационную стратегию (relevance / exclusion / independence инструмента вместо unconfoundedness), и именно поэтому даёт оценку, ближе всего к истинному эффекту.

## Как запустить

```bash
git clone https://github.com/ksbatalova/Intro-to-CI.git
cd Intro-to-CI
pip install -r requirements.txt
jupyter notebook Intro_to_ci.ipynb
```

`requirements.txt`:
```
numpy
pandas
scikit-learn
statsmodels
catboost
causalml
econml
doubleml
linearmodels
matplotlib
```

## Стек

Python · pandas · scikit-learn · CatBoost · causalml · econml · doubleml · linearmodels · statsmodels
