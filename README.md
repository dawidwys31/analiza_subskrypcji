# Analiza Subskrypcji

**Celem projektu jest analiza danych dotyczących subskrypcji. 
Głównym zadaniem jest zrozumienie czynników 
wpływających na to, czy klient zdecyduje się na założenie lokaty terminowej
(zmienna `y`).**

## Kluczowe wnioski z etapu EDA
* **Profil Klienta:** Najwyższą konwersję (ok. 45%) wykazują seniorzy (65+).
* **Zatrudnienie:** Studenci i emeryci to najbardziej responsywne grupy, mimo że stanowią mniejszość ankietowanych.
* **Finanse:** Posiadanie kredytu hipotecznego (`housing`) obniża szansę na założenie lokaty.
* **Modelowanie:** Zidentyfikowano ryzyko *data leakage* w zmiennej `duration`.

## Podsumowanie Modelowania

### Model: Regresja Logistyczna
Problem: brak balansu w danych (tylko ok. 11% klientów zdecydowało się na subskrypcję). 

**Cechy:**
* **Skuteczna identyfikacja klientów:** Dzięki zbalansowaniu wag klas, model potrafi wskazać **62% wszystkich osób**, które decydują się na subskrypcje.
* **Optymalizacja:** Zamiast dzwonić do wszystkich klientów z bazy bank może skupić się na grupie wskazanej przez model.
* **Interpretowalność:** Model pozwolił zidentyfikować, które cechy  (np. wiek, saldo, historia poprzednich kampanii) mają największy wpływ na końcową decyzję.

**Wyniki:**
* **Accuracy:** 75%
* **Recall:** 0.62
* **F1-Score:** 0.37

## Organizacja Projektu

```
├── LICENSE            <- Open-source license if one is chosen
├── Makefile           <- Makefile with convenience commands like `make data` or `make train`
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
│
├── docs               <- A default mkdocs project; see www.mkdocs.org for details
│
├── models             <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
│                         the creator's initials, and a short `-` delimited description, e.g.
│                         `1.0-jqp-initial-data-exploration`.
│
├── pyproject.toml     <- Project configuration file with package metadata for 
│                         src and configuration for tools like black
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `pip freeze > requirements.txt`
│
├── setup.cfg          <- Configuration file for flake8
│
└── src   <- Source code for use in this project.
    │
    ├── __init__.py             <- Makes src a Python module
    │
    ├── config.py               <- Store useful variables and configuration
    │
    ├── dataset.py              <- Scripts to download or generate data
    │
    ├── features.py             <- Code to create features for modeling
    │
    ├── modeling                
    │   ├── __init__.py 
    │   ├── predict.py          <- Code to run model inference with trained models          
    │   └── train.py            <- Code to train models
    │
    └── plots.py                <- Code to create visualizations
```

--------

