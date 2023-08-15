**ОЦЕНКА ПРИМЕНИМОСТИ МОДЕЛЕЙ МАШИННОГО       ОБУЧЕНИЯ ДЛЯ ПРЕДСКАЗАНИЯ ДОСТИЖИМОСТИ        МИНИМАЛЬНО КЛИНИЧЕСКИ ЗНАЧИМОГО ИЗМЕНЕНИЯ В СОСТОЯНИИ ПАЦИЕНТА ПОСЛЕ ЭНДОПРОТЕЗИРОВАНИЯ СУСТАВА** 

**EVALUATION OF THE APPLICABILITY OF MACHINE LEARNING MODELS FOR PREDICTING THE REACHABILITY OF THE       MINIMAL CLINICALLY IMPORTANT DIFFERENCE IN THE      PATIENT'S STATE AFTER JOINT REPLACEMENT**

Хамитов А.К., Белова Е.Ю.,

ФГАОУ ВО «Санкт-Петербургский государственный электротехнический университет «ЛЭТИ» имени В. И. Ульянова (Ленина)», г. Санкт-        Петербург, Российская Федерация

A.K. Khamitov, E.Y. Belova,

Saint Petersburg Electrotechnical University, St. Petersburg, Russian Federation

e-mail*:* abulkairhamitov@gmail.com; eyshukeylo@gmail.com

**Аннотация.** Применение  методов  машинного  обучения  для прогнозирования минимально клинически значимого изменения, которое произошло с состоянием пациента с момента проведения операции и до завершения  процесса  реабилитации,  позволяет  произвести  коррекцию тактики  лечения  в  будущем  и  снизить  финансовые  затраты  на медицинское обслуживание. В исследовании использован набор данных, сформированный на основе информации из Австралийского регистра клинических результатов эндопротезирования и включающий сведения о плановых  операциях  по  полной  замене  тазобедренного  и  коленного суставов.  Для  определения  достижимости  минимально  клинически значимого  изменения  в  состоянии  пациента  после  проведения эндопротезирования  построены  как  модели  на  основе  алгоритмов классического машинного обучения, так и модели на основе нейронных сетей:  MLP,  TabNet  и  HyperTab.  Логистическая  регрессия  и  метод опорных векторов показали наилучшее среднее арифметическое значение AUC – от 0.68 до 0.78 в зависимости от набора данных. Отставание данного значения на 0.01-0.02 продемонстрировали модели случайного леса  и  наивного  Байесовского  классификатора.  Табличное  обучение TabNet и гиперсетевой подход HyperTab не достигли высокого среднего арифметического  значения  AUC.  Таким  образом,  использование логистической регрессии и метода опорных векторов рекомендуется для предсказания  достижимости  минимально  клинически  значимого изменения в состоянии пациента после эндопротезирования сустава.

**Abstract.** The use of machine learning methods to predict the minimum clinically important difference that has occurred in the patient's condition from the moment of the operation to the completion of the rehabilitation process allows to correct treatment tactics in the future and reduce the financial costs of medical care. A data set based on information from The Arthroplasty Clinical Outcomes Registry, Australia and including data on elective total hip or total knee replacement surgery was used in the research. Models based on classical machine learning algorithms and models based on neural networks: MLP, TabNet and HyperTab are built to determine the achievability of minimum clinically important difference in the patient's condition after arthroplasty. Logistic regression and support vector machine showed the best arithmetic mean AUC - from 0.68 to 0.78 depending on the dataset. The lag of this value by 0.01-0.02 was demonstrated by the models of the random forest and the naive Bayesian classifier. TabNet tabular learning and HyperTab's hypernet approach did not achieve a high arithmetic mean AUC. Thus, the use of logistic regression and support vector machine analysis is recommended to predict the achievability of the minimal clinically important difference in the patient's condition after total joint replacement.

**Ключевые слова:**  анкета Oxford  Knee  Score, анкета Oxford Hip Score, минимально клинически значимое изменение, машинное обучение, нейронные сети, гиперпараметры

**Keywords:** Oxford Knee Score, Oxford Hip Score, minimum clinically important difference, machine learning, neural networks, hyperparameters

**Введение**

Эндопротезирование является одним из распространённых методов оперативного  лечения  заболеваний  суставов.  В  2020  году  в  России проведено 116 080 операций, из которых 62 680 случаев (54%) относилось к эндопротезированию тазобедренного сустава и 49 974 случая (43%) – к эндопротезированию коленного сустава [1].

Получение и анализ различных показателей, связанных с состоянием здоровья пациента и качеством его жизни на каждом этапе реабилитации после  проведения  эндопротезирования,  осуществляется  за  счёт использования PROM (patient reported outcomes measure)  – это оценка результатов,  сообщаемых  пациентом  [2].  Примером  её  реализации являются анкеты OKS (Oxford Knee Score) и  OHS (Oxford Hip Score) для измерения  боли  и  функции  коленного  и  тазобедренного  суставов соответственно  [3].  Благодаря  использованию  анкет  существует возможность расчёта MCID (minimum clinically important difference) – минимально  клинически  значимого  изменения,  которое  произошло  с состоянием пациента с момента проведения операции и до завершения процесса реабилитации. Выявление пациентов с риском недостижения MCID  вносит  существенный  вклад  в  предоперационную  поддержку принятия решений [4]. Прогнозирование MCID ранее выполнялось с помощью методов математической статистики, однако в последние годы для решения данной проблемы используется машинное обучение [5]. Однако, ни в одной из работ на этапе моделирования не применялись табличное обучение TabNet и гиперсетевой подход HyperTab, сочетающий в себе преимущества метода случайного леса и нейронных сетей [6,7].

Целью  исследования  является  оценка  применимости  моделей машинного  обучения  для  предсказания  достижимости  минимально клинически  значимого  изменения  в  состоянии  пациента  после эндопротезирования сустава. 

**Материалы и методы**

В исследовании используется набор данных, сформированный на основе информации из Австралийского регистра клинических результатов эндопротезирования с 2013 по 2018 годы. Он содержит информацию о пациентах,  перенесших  плановую  операцию  по  полной  замене тазобедренного  или  коленного  сустава  в  различных  медицинских учреждениях,  –   данные,  собранные  путем  опроса  пациентов  перед проведением  операции;  данные,  полученные  в  интраоперационный период; оценки результатов лечения, сообщенные пациентами через 6 месяцев после оперативного вмешательства (OKS, OHS, EQ-5D). К набору данных  прилагается  словарь,  включающий  описание  используемых переменных. Ранее исследователи в статье [8]  обращались к тому же регистру с целью выявления предикторов неудовлетворенности пациентов результатами  тотального  эндопротезирования  тазобедренного  сустава, проведенного в период с 2014 по 2016 годы.  

Расчёт MCID, как правило, производится с применением методов, основанных либо на распределении, либо на привязке. По данным из литературы для группы пациентов, наблюдение за которыми ведется на определенном промежутке времени,  следует использовать значения MCID по OHS, равное ~11 баллам, и  MCID по OKS, равное ~9 баллам [9]. Данные значения получены с применением методов на основе привязки.

В  качестве  алгоритмов  машинного  обучения  используются логистическая регрессия, метод k-ближайших соседей, дискриминантный анализ, метод опорных векторов, наивный байесовский классификатор, дерево решений, случайный лес, экстремальный градиентный бустинг, 1-2 слойный нейронный классификатор. Кроме того, применены MLP, TabNet и HyperTab.

Метрикой для оценки предсказательной способности построенных моделей служит Area under the ROC Curve (AUC) – площадь под ROC- кривой. Её рекомендуется использовать при работе с несбалансированным набором данных. Она является статистически непротиворечивой, а также более избирательна, чем точность [10]. 

**Подготовка данных и моделирование**

Изначально набор данных содержал 9146 строк и 227 столбцов. Однако потребовалось разделить его на  две части, поскольку одной группе  пациентов  выполнялась  операция  эндопротезирования тазобедренного  сустава,  а  другой  группе  пациентов  –  операция эндопротезирования коленного сустава. В связи с этим для измерения боли  и  функции  использовались  разные  анкеты  –  OHS   и  OKS соответственно. После выполнения разделения первый набор данных включал 2203 строки и 46 столбцов, второй набор данных – 4504 строки и 46 столбцов. Информация о пациентах, которым проводили вторичное двустороннее эндопротезирование суставов, не учитывалась в данной работе. 

В  ходе  исследования  проведена  нормализация  данных  в сформированных наборах. Если ячейки не содержали значений, то они изымались вместе со строкой. Послеоперационные переменные, кроме тех, которые используются для подсчёта MCID, и столбцы с около нулевой дисперсией удалены. Значения, которые не предусмотрены в словаре данных, исключены как выбросы.

Настройка гиперпараметров для  всех моделей,  за исключением TabNet и HyperTab, выполняется с использованием фреймворка Optuna и алгоритма  TPESampler  (оценщик Парзена с древовидной структурой), с помощью  которого  принимается  решение  о  выборе  последующих значений гиперпараметров на основе результатов предыдущих итераций.

Проблема  несбалансированности  данных  устранена  путем использования  взвешивания  классов  и  решении  задачи  минимизации эмпирического риска.

На рисунке 1 в качестве примера представлен процесс подбора гиперпараметров для модели случайного леса на первом наборе данных, где одним из параметров является вес меньшего класса. На цветовой шкале конкретный оттенок ставится в соответствие номеру испытания.

В качестве целевой функции для оптимизации выбран средний результат  AUC,  который  получен  на  десяти  невзаимосключающих выборках, составляющих  20% от исходного набора данных (ось ординат на рисунке 1). 

![Image alt](https://github.com/abulkairhamitov/MCID_ML/blob/master/appendices/study/ohs/images/dt_study.png)
Рисунок 1. Процесс подбора гиперпараметров для модели случайного леса на первом наборе данных

Каждый из двух используемых в исследовании наборов данных эмпирически разделен на два равных по размеру подмножества. Первое подмножество  используется  для  подбора  гиперпараметров,  второе подмножество  –  для  обучения  моделей.  Таким  образом  достигнуты оптимальные  результаты  оценки  точности  без  не  затрагивания переобучения, связанного с подбором параметров на обучающей выборке. При  обучении моделей TabNet и HyberTab разделение наборов данных на подмножества  не  производится.  Калибровка  моделей  выполнена  на полных наборах данных, как и проверка важности признаков. 

С учётом того факта, что результаты оценки AUC могут отличаться из-за  процедуры  её  анализа  и  стохастической  природы  алгоритмов, выполнено разделение в количестве 1000 раз каждого из двух наборов данных (второго подмножества)  на обучающую и тестовую выборки в соотношении 80% к 20%. После сортировки от меньшего к большему устанавливается   доверительный  интервал  с  уровнем  доверия  95%. Среднее значение получено как среднее арифметическое. Такой подход позволяет найти диапазон, в котором находится истинное значение AUC. 

**Результаты**

В процессе проведенного исследования получены значения нижней границы, верхней границы и среднего арифметического значения AUC, они представлены в таблице.

Для TabNet и HyberTab проведено десять прогонов на 5000 и 70 эпохах соответственно. В первом получены средние AUC 0.69 и 0.60 и для второго 0.69 и 0.59 на наборах данных OHS+EQ-5D и OKS+EQ-5D соответственно.

Наилучший  результат  достигнут  с  применением  логистической регрессии  и  метода  опорных  векторов,  наихудший  результат  –  с использованием квадратичного дискриминантного анализа.

Табличное обучение TabNet и гиперсетевой подход HyperTab не продемонстрировали высокого среднего арифметического значения AUC.

Таким  образом,  линейные  модели  справились  с  задачей классификации  на  исследуемых  наборах  данных  лучше,  поэтому  их использование  рекомендуется  для  предсказания  достижимости минимально клинически значимого изменения в состоянии пациента после эндопротезирования сустава.

Таблица.  Доверительные  интервалы  моделей  для  первого  и  второго наборов данных



|Название модели|Нижняя граница (OHS/OKS с EQ-5D)|Верхняя граница (OHS/OKS с EQ-5D)|Среднее (OHS/OKS с EQ-5D)|
| - | :- | :- | :- |
|Логистическая регрессия|0\.71/0.63|0\.86/0.74|0\.78/0.69|
|k-ближайших соседей|0\.63/0.56|0\.79/0.65|0\.70/0.69|
|Метод опорных векторов|0\.71/0.63|0\.85/0.74|0\.78/0.68|
|Наивный Байесовский классификатор (Бернулли)|0\.67/0.63|0\.82/0.73|0\.76/0.68|
|Квадратичный дискриминантный анализ|0\.55/0.56|0\.70/0.64|0\.62/0.61|
|Дерево решений|0\.64/0.60|0\.80/0.71|0\.72/0.65|
|Случайный лес|0\.69/0.62|0\.84/0.73|0\.76/0.68|
|Экстремальный градиентный бустинг|0\.65/0.54|0\.81/0.62|0\.73/0.58|
|Нейронный классификатор (MLP)|0\.68/0.52|0\.83/0.68|0\.75/0.60|

В  исследовании  произведена  оценка  важности  признаков  для моделей логистической регрессии, случайного леса и экстремального градиентного  бустинга.  В  первом  случае  под  важностью  признаков подразумевается  нормализованные  значения  коэффициентов,  где наибольший коэффициент равен единице. Во втором и в третьем случаях важность признака вычисляется как (нормализованное) общее снижение критерия,  привносимого  этим  признаком.  В  процессе  исследования выбрано среднее значение из 20 результатов, которые получены для каждого признака на случайно обученных подмножествах, составляющих 80% от исходной выборки. 

На  рисунке  2  представлены  первые  12  важных  признаков  для логистической регрессии на втором наборе данных. Стоит отметить, что наибольшие значения коэффициентов у логистической регрессии имели признаки демографии и базовых медицинских характеристик. 

Логистическая регрессия (с регуляризаторами) занижала значения коэффициентов для признаков OHS, OKS и EQ-5D. Метод случайного леса и экстремального градиентного бустинга справляются с данной задачей чуть хуже, больше акцентируя внимание на признаках из анкет. 

![Image alt](https://github.com/abulkairhamitov/MCID_ML/blob/master/appendices/feature_scores/ohs/images/logreg.png)

Рисунок  2.  Важности  признаков  для  модели  логистической регрессии на первом наборе данных

**Литература**   

1. Соломянник  И.А.,  Загородний  Н.В.,  Родионова  С.С.  и  др.

Травматизм, ортопедическая заболеваемость, организация травматолого- ортопедической помощи в Российской Федерации в 2020 году. Москва: ФГБУ Нмиц ТО им. Н. Н. Приорова, 2022 г. – 514 с.

2. Хатьков, И. Е., Минаева, О. А., Домрачев, С. А. и др. PROM-

современный  подход  к  оценке  качества  жизни  пациентов  с онкологическими заболеваниями // Терапевтический архив. 2022. № 94(1). С. 122-128.

3. Синеокий, А. Д., Билык, С. С., Близнюков, В. В., Коваленко, А. Н.

и др. Кросс-культурная адаптация и валидация русскоязычной версии анкеты Oxford Knee Score для пациентов с гонартрозом, ожидающих выполнения первичного эндопротезирования // Современные проблемы науки и образования. 2017. № 2. С. 92-97.

4. Fontana, M. A., Lyman, S., Sarker, et al. Can machine learning

algorithms predict which patients will achieve minimally clinically important differences from total joint arthroplasty? // Clinical orthopaedics and related research. 2019. № 477(6). P. 1267-1279.

5. Langenberger,  B.,  Thoma,  A.,  Vogt,  V.  Can  minimal  clinically

important differences in patient reported outcome measures be predicted by machine learning in patients with total knee or hip arthroplasty? A systematic review. // BMC Medical Informatics and Decision Making. 2022. № 22(1). P. 1-14.

6. Arik,  S.  Ö.,  Pfister,  T.  Tabnet:  Attentive  interpretable  tabular

learning // In Proceedings of the AAAI Conference on Artificial Intelligence. 2021. Vol. 35, №. 8, P. 6679-6687.

7. Wydmański, W., Bulenok, O., & Śmieja, M. HyperTab: Hypernetwork

Approach for Deep Learning on Small Tabular Datasets // arXiv. 2023. P. 1-15.

8. Van Meirhaeghe, J. P., Alarkawi, D., Kowalik, T. et al. Predicting

dissatisfaction  following  total  hip  arthroplasty  using  a  Bayesian  model averaging  approach:  Results  from  the  Australian  Arthroplasty  Clinical Outcomes Registry National (ACORN) // ANZ Journal of Surgery. 2021. № 91(9). P. 1908-1913.

9. Beard, D. J., Harris, K., Dawson et al. Meaningful changes for the

Oxford hip and knee scores after joint replacement surgery // Journal of clinical epidemiology. 2015. № 68(1). P. 73-79.

10. Huang, J., & Ling, C. X. Using AUC and accuracy in evaluating

learning algorithms // IEEE Transactions on knowledge and Data Engineering. 2005. № 17(3). P. 299-310.
