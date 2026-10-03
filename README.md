# Into-to-CI

Causal ML: сравнение методов оценки эффекта воздействия
Учебный проект, показывающий, почему A/B-тесты и наивное сравнение групп дают смещённые оценки при неслучайном назначении воздействия, и как разные методы причинного вывода решают эту проблему.
Спроектировала синтетический DGP с контролируемым ненаблюдаемым confounder'ом и инструментальной переменной — что позволяет точно измерить bias каждого метода относительно истинного эффекта
Реализовала и сравнила: propensity score matching, IPW, 2SLS/IV, meta-learners (S/T/X/R-learner), causal tree, causal forest, Double Machine Learning (с Neyman orthogonality и cross-fitting)
Показала эмпирически, что сложность ML-модели решает проблемы оценивания (переобучение, curse of dimensionality), но не заменяет корректную идентификационную стратегию при нарушенном unconfoundedness
Стек: Python, pandas, scikit-learn, CatBoost, econml, causalml, doubleml, linearmodels, statsmodels
