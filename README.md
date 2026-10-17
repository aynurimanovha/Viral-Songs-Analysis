# Viral Songs Analysis

## Layihə haqqında

Bu layihə viral mahnılar dataset-i üzərində məlumatların ilkin araşdırılması, təmizlənməsi, vizuallaşdırılması və maşın öyrənməsinə hazırlanması prosesini əhatə edir. Jupyter Notebook-da Python və məlumat analizi kitabxanalarından istifadə edilərək dataset-in strukturu, dəyişənlərin paylanmaları və aralarındakı əlaqələr araşdırılır.

Layihənin əsas notebook-u:

```text
viralsongs_analysis.ipynb
```

## Layihənin məqsədləri

- Dataset-in strukturunu və keyfiyyətini araşdırmaq
- Boş dəyərləri, dublikatları və mümkün uyğunsuzluqları yoxlamaq
- Feature engineering vasitəsilə əlavə dəyişənlər yaratmaq
- Univariate, bivariate və multivariate EDA aparmaq
- Dəyişənlər arasındakı korrelyasiyaları araşdırmaq
- Kateqorik dəyişənləri encode etmək
- Multikolinearlığı yoxlamaq
- Dataset-i training və testing hissələrinə bölmək
- Seçilmiş numeric feature-lərə scaling tətbiq etmək
- Hazır datasetləri CSV formatında saxlamaq

## İstifadə olunan texnologiyalar

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook

## Dataset

Notebook-da ilkin dataset üçün aşağıdakı yol müəyyən edilib:

```python
DATA_PATH = "/content/viral_songs.csv"
```

Bu yol Google Colab mühitinə uyğundur. Notebook-u lokal kompüterdə və ya başqa mühitdə işlətmək üçün `DATA_PATH` dəyişənini `viral_songs.csv` faylının yerləşdiyi yerə uyğun dəyişin.

> Qeyd: Dataset bu repository-yə daxil edilməyibsə, notebook-u işlətməzdən əvvəl `viral_songs.csv` faylını əldə edib düzgün yola yerləşdirmək lazımdır.

## Layihənin strukturu

Tövsiyə olunan repository strukturu:

```text
viral-songs-analysis/
│
├── README.md
├── viralsongs_analysis.ipynb
└── viral_songs.csv
```

CSV dataset-i paylaşılmırsa, sonuncu faylı repository-yə əlavə etməyin; onun əldə olunma mənbəyini README-də qeyd edin.

## Analiz prosesi

### 1. İlkin məlumatların araşdırılması

Notebook-da dataset-in ölçüsü, sütun adları, data tipləri, ilkin və son sətirləri, nümunə sətirlər, ümumi məlumat və təsviri statistika araşdırılır.

### 2. Data quality yoxlamaları

Aşağıdakılar yoxlanılır:

- Missing values
- Tam dublikat sətirlər
- Kateqorik dəyərlərin paylanması
- Xüsusi və potensial uyğunsuz dəyərlər
- Dəyişənlərin məntiqi uyğunluğu

Notebook-un saxlanmış nəticələrində ilkin dataset 10.000 sətir və 17 sütundan ibarətdir; missing value və tam dublikat sayı 0 kimi göstərilir.

### 3. Data cleaning və standartlaşdırma

Sütun adları və kateqorik dəyərlər yoxlanılır, uyğun hallarda mətn standartlaşdırılması və dəyər çevrilməsi aparılır. Təmizləmədən sonra dataset yenidən yoxlanılır.

### 4. Feature engineering

Notebook-da əlavə dəyişənlər yaradılır, o cümlədən:

- `era`
- `streams_group`
- `viral_label`

Bu dəyişənlər mahnıları dövr, stream qrupları və hədəf etiketi baxımından araşdırmağa kömək edir.

### 5. Exploratory Data Analysis (EDA)

EDA aşağıdakıları əhatə edir:

- Kateqorik dəyişənlərin tezliyi və faizləri
- Numeric dəyişənlərin mean, median, variance, standard deviation və skewness göstəriciləri
- Histogram, boxplot və scatterplot vizuallaşdırmaları
- Outlier-lərin IQR metodu ilə aşkarlanması
- Kateqorik və numeric dəyişənlər arasında əlaqələr
- Qruplar üzrə müqayisələr
- Pearson və Spearman korrelyasiyaları

Outlier-lərin aşkarlanması onların mütləq silinməsi demək deyil; silinmə qərarı məlumatın mənasına əsaslanmalıdır.

### 6. Encoding

Kateqorik `genre` dəyişəni one-hot encoding vasitəsilə rəqəmsal sütunlara çevrilir. Notebook-da `drop_first=True` istifadə edilir ki, bir baseline kateqoriya buraxılsın.

Encoding-dən sonra sütun tipləri, dataset ölçüsü və yaranmış boş dəyərlər yoxlanılır.

### 7. Multikolinearlıq

Feature-lər arasındakı korrelyasiyalar və VIF göstəriciləri araşdırılır. Notebook-un saxlanmış nəticəsində maksimum VIF təxminən `7.757` olaraq göstərilir. Bu nəticə yüksək göstəricilərin hansı dəyişənlərdə yarandığını əlavə izah etməyi tələb edə bilər.

### 8. Train/test split

Dataset training və testing hissələrinə bölünür. Notebook-da split üçün 80/20 nisbəti və stratified bölünmə istifadə edilir. `RANDOM_STATE` nəticələrin təkrar əldə olunmasına kömək edir.

### 9. Scaling

Scaling yalnız train/test bölünməsindən sonra aparılır. Scaler training data üzərində fit edilir, daha sonra həmin scaler testing data-ya tətbiq olunur. Bu, test məlumatının scaling parametrlərinin hesablanmasına təsir etməsinin qarşısını alır.

Binary və target dəyişənləri scaling prosesinə daxil edilməməlidir.

### 10. Final yoxlama və export

Final mərhələdə train və test datasetləri yoxlanılır:

- Missing values
- Qeyri-numeric sütunlar
- Train/test sütunlarının uyğunluğu
- Dataset ölçüləri

Notebook-un export bölməsində hazırlanmış datasetləri CSV formatında saxlamaq nəzərdə tutulur. Yaradılan faylların dəqiq adları notebook-un son export hüceyrəsində göstərilir.

## Vacib metodoloji qeyd

Əgər `viral` hədəf etiketi `streams` sütununa əsasən yaradılıbsa, `streams`-in model feature-i kimi saxlanılması target leakage yarada bilər. Buna görə model qurulmazdan əvvəl hədəfin necə müəyyənləşdirildiyini yoxlamaq və real proqnoz ssenarisinə uyğun feature seçmək lazımdır. Notebook-da `DROP_STREAMS` parametri bu qərarı idarə etmək üçün mövcuddur.

## Notebook-u necə işlətmək olar?

1. Repository-ni clone edin və ya faylları yükləyin.
2. Lazımi Python kitabxanalarının quraşdırıldığı mühit yaradın.
3. `viral_songs.csv` faylını notebook-da göstərilən yola yerləşdirin və ya `DATA_PATH` parametrini dəyişdirin.
4. `viralsongs_analysis.ipynb` faylını Jupyter Notebook, JupyterLab və ya VS Code-da açın.
5. Notebook-u yuxarıdan aşağıya ardıcıllıqla icra edin.
6. Final yoxlama və export hüceyrələrinin uğurla işlədiyini təsdiqləyin.

## Nəticə

Bu notebook viral mahnılar dataset-i üçün data inspection, cleaning, feature engineering, EDA, encoding, multikolinearlıq analizi, train/test split və scaling mərhələlərini bir araya gətirir. Hazırlanmış dataset növbəti machine-learning mərhələsində istifadə oluna bilər.

Layihə hazırda əsasən data analysis və preprocessing prosesinə fokuslanır; notebook-da ayrıca modelin təlimi və performans qiymətləndirilməsi həyata keçirildiyi iddia edilmir.
