# hw4_scRNA-seq
Анализ scRNA-seq данных из статьи ["Single-cell mapping of the thymic stroma identifies IL-25-producing tuft epithelial cells"](https://drive.google.com/file/d/1PozBU0cxuXQIQcKqGvgZ-6-bQ1wxwD-2/view?usp=sharing)
## [Project code in Google Colab](https://colab.research.google.com/drive/1Aq2B7r6gzBAMxI8udHeruYxEfhwalmN_?usp=sharing)
## scRNA-seq data normalization
### Method description
Для того, чтобы можно было сравнивать между собой разные образцы по уровню экспрессии определенных генов, необходимо провести нормализацию данных для каждого образца. В данной работе был использован один из самых простых методов - TPM (transcript per million). TPM рассчитывается по формуле представленной ниже:

![](images/tpm_formula.png)

В отдельном образце значение TPM для гена i равняется количеству чтений гена i “q(i)”, взвешенному на длину гена i “l(i)”, деленному на сумму чтений всех генов в образце, взвешенных на длины этих. Далее полученное значение TPM умножается на 10^6 [[1]](https://translational-medicine.biomedcentral.com/articles/10.1186/s12967-021-02936-w).

В данной работе количества чтений генов не взвешивались на длины соотвествующих генов.
### Results
#### Data before normalization
![](images/pre-norm_counts.png)
#### Data after normalization
![](images/norm_counts.png)
## Samples clusterization
На основе нормализованных данных генной экспрессии исследуемые образцы были кластеризованы. Для визуализации результатов кластеризации были использованы два распространённых метода понижения размерности: PCA и UMAP.
### PCA visualization
![](images/pca.png)
Из пяти клеточных типов, обозначенных разными цветами, две главные компоненты, полученные методом PCA, позволяют отчетливо отобразить только три типа, соответствующих оранжевому, зелёному и фиолетовому кластеру, в то время как синие и красные точки не образуют выраженных скоплений и смешиваются с другими типами клеток.
### UMAP visualization
![](images/umap.png)
Судя по графику, UMAP справился с понижением размерности до двух измерений заметно лучше, чем PCA: кроме выделения оранжевого, зелёного и фиолетового типов в виде более выраженных кластеров, UMAP сумел выделить отчетливый кластер для синего типа и некое подобие кластера для красного.
### Conclusion
Подводя итоги, UMAP показал себя лучше, чем PCA, и проиллюстрировал возможность сократить размерность данных до двух признаков с сохранением значительной части информации в нашей задаче. Следовательно, вполне вероятно, что количество маркерных генов, необходимых для дифференциации клеточных типов по данным экспрессии, может быть уменьшено без заметного ущерба в точности.
## Marker genes expression heatmap
На основе нормализованных данных об экспрессии 23 маркерных генов, отобранных авторами статьи, была получена тепловая карта. На ней по оси абсцисс отложены образцы, сгруппированные по клеточным типам, а по оси ординат - маркерные гены. На карте невооруженным глазом заметны отчетливые паттерны экспрессии генов, по которым можно отличить один клеточный тип от другого.
![](images/heatmap.png)
Ниже на карте выделены самые очевидные паттерны, соответсвующих разным клеточным типам.
![](images/heatmap_marked.png)
## Bonus task
### Graphical analysis
Для графического анализа по усредненным нормализованным данным была построена диаграмма рассеяния в логарифмической шкале, где каждая точка соответсвует гену, а её координаты - средней экспрессии этого гена в bulk (ось OX) и s-cell (ось OY).
![](images/ln-sc_vs_ln-bulk.png)

Если смотреть на график диагонально, начиная с верхнего правого угла, то можно заметить, что короткий линейный тренд быстро сменяется неким подобием гиперболической зависимости между результатами двух типов RNA-seq. Если отбросить немногочисленные выбросы, то можно сделать вывод о том, что в квадратной области, ограниченной координатными осями с левой стороны и прямыми, параллельными осям и пересекающимися в районе координаты (7; 7), с правой стороны, уровни экспрессии между двумя типами RNA-seq сильно расходятся (голубой график). В то время как данные за пределами описанного квадрата демонстрируют прямую корреляцию (красный график), как показано на следующем рисунке.
![](images/ln-sc_vs_ln-bulk_marked.jpg)

