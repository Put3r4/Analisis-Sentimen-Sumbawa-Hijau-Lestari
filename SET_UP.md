# Analisis Sentimen Sumbawa Hijau Lestari

## Setup Environment - Anaconda
```
conda create --name <nama_env> python=3.11
conda activate <nama_env>
pip install -r requirements.txt
```
(Nama environment bebas)

## Setup Environment - Shell/Terminal
```
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```
(Nama venv bebas)

## Opsi Instalasi Terpisah
Instalasi manual via pip:
```
pip install pandas numpy openpyxl matplotlib seaborn wordcloud jupyter
```

## Daftar Dataset

### 1. Raw Dataset (`data/dataset/`)
- `dataset_analisis_sumbawa_hijau_lestari.csv`
- `daftar_link_sumber.csv`

### 2. Processed Dataset (`data/processed_dataset/`)
- `dataset_siap_label_sumbawa_hijau_lestari.xlsx`

### 3. Data Labelling (`data/labelled/`)
- `dataset_siap_label_sumbawa_hijau_lestari_labelled.xlsx`

## Run Cleaning Notebook
```
jupyter notebook notebook/01_cleaning_dataset.ipynb
```

## Run Analisis Sentimen Notebook
```
jupyter notebook notebook/02_analisis_sentimen.ipynb
```

## Run Jupyter Notebook (semua notebook)
```
jupyter notebook
```
