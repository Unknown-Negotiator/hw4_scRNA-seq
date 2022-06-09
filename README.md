# hw4_scRNA-seq
Анализ scRNA-seq данных из статьи ["Single-cell mapping of the thymic stroma identifies IL-25-producing tuft epithelial cells"](https://drive.google.com/file/d/1PozBU0cxuXQIQcKqGvgZ-6-bQ1wxwD-2/view?usp=sharing)
## [Google Colab link](https://colab.research.google.com/drive/1Aq2B7r6gzBAMxI8udHeruYxEfhwalmN_?usp=sharing)
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
### UMAP visualization
![](images/umap.png)
## Marker genes expression heatmap
На основе нормализованных данных об экспрессии 23 маркерных генов, отобранных авторами статьи, была получена тепловая карта.
![](images/expr_heatmap.png)
