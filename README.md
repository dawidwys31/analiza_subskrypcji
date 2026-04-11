Predykcja Sprzedaży Lokat Terminowych
=====================================

**Celem projektu była analiza czynników wpływających na decyzję o założeniu lokaty terminowej oraz budowa modeli klasyfikacyjnych przewidujących konwersję (zmienna y).**

Kluczowe wnioski z etapu EDA
----------------------------

*   **Profil Klienta:** Najwyższą konwersję (ok. 45%) wykazują seniorzy (65+).
    
*   **Zatrudnienie:** Studenci i emeryci to najbardziej responsywne grupy, mimo że stanowią mniejszość ankietowanych.
    
*   **Finanse:** Posiadanie kredytu hipotecznego (housing) znacząco obniża szansę na założenie lokaty.
    
*   **Modelowanie:** Zidentyfikowano i wyeliminowano ryzyko _data leakage_ związanego ze zmienną duration (czas trwania rozmowy).
    

Podsumowanie Modelowania
------------------------

### Model: Regresja Logistyczna

Głównym wyzwaniem był brak balansu w danych (tylko ok. 11% pozytywnych decyzji).

**Cechy:**

*   **Skuteczna identyfikacja:** Dzięki zbalansowaniu wag klas, model wyłapuje **62% wszystkich osób** faktycznie zainteresowanych ofertą.
    
*   **Interpretowalność:** Pozwala jasno określić wpływ cech (wiek, saldo, historia kampanii) na decyzję klienta.
    
*   **Zastosowanie:** Idealny do szerokich kampanii, gdzie zależy nam na maksymalnym zasięgu.
    

**Wyniki:**

*   **Accuracy:** 75%
    
*   **Recall:** 0.62
    
*   **F1-Score:** 0.37
    

### Model: Sieci Neuronowe (MLPClassifier)

Zastosowano architekturę typu Multi-layer Perceptron (MLP) z dwiema warstwami ukrytymi (20, 10) w celu uchwycenia nieliniowych zależności.

**Cechy:**

*   **Wysoka precyzja:** Model działa jak "snajper" – rzadziej wskazuje klientów, ale robi to z większą trafnością (**Precision: 0.55**).
    
*   **Złożoność:** Skutecznie wyłapuje nieliniowe korelacje, których regresja mogła nie zauważyć.
    
*   **Preprocessing:** Wymagał pełnej standaryzacji danych (StandardScaler) dla poprawnej zbieżności algorytmu.
    

**Wyniki:**

*   **Accuracy:** 89%
    
*   **Precision:** 0.55
    
*   **Recall:** 0.28
    

Rekomendacja Biznesowa
----------------------

Wybór modelu zależy od strategii banku:

1.  **Strategia Ekspansywna:** Wybór **Regresji Logistycznej**. Wyższy _Recall_ pozwala zdobyć więcej lokat kosztem większej liczby wykonanych połączeń.
    
2.  **Strategia Efektywnościowa:** Wybór **Sieci Neuronowej**. Wyższa _Precyzja_ optymalizuje czas pracy Call Center, kierując pracowników tylko do najbardziej pewnych klientów.
## Organizacja Projektu
Tech stack: Python (Pandas, Scikit-learn, NumPy), Jupyter Notebook, Git
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

