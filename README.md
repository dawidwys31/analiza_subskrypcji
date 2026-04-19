# Raport BI: Lokaty terminowe – optymalizacja kampanii subskrypcyjnej
**Autorzy: Dawid Wysokiński**

---

## 1. Problem biznesowy
Bank XYZ chce zwiększyć efektywność sprzedaży subskrypcji lokat terminowych. W tym celu zlecił nam analizę bazy klientów, która zawiera informację o **45 211 klientach**. Podjęto decyzję o jej przeprowadzeniu w celu określenia, czy możliwe jest stworzenie modelu przewidującego, czy dany klient zdecyduje się na zakup subskrypcji lokaty terminowej w przypadku przedstawienia oferty na podstawie danych historycznych.

## 2. Cel
Głównym celem jest **ocena wykonalności**, która ma określić, które cechy dostępne w bazie danych klientów banku najbardziej wpływają na założenie lokaty terminowej, a także określić, jaki rodzaj modelu w zastosowaniu bankowym sprawdzi się lepiej. Raport ma służyć wspieraniu procesów decyzyjnych w organizacji.

## 3. Metodyka
Analiza została zrealizowana przy użyciu środowiska **Python** (biblioteki Pandas, Scikit-learn oraz biblioteki wizualizacyjne) w następujących krokach:
1. **EDA** – określenie profilu klientów banku.
2. **Przygotowanie danych**.
3. **Modelowanie** – Regresja Logistyczna oraz Sieci Neuronowe (MLP).
4. **Ocena i rekomendacja biznesowa**.

## 4. EDA – profil klientów
Analiza dostarczonych danych pozwoliła zbudować profile klientów, a także określić ogólne ich cechy jako grupy.

### Struktura wieku:
Rozkład średniego wieku ankietowanych jest prawoskośny. Większość ankietowanych klientów znajduje się w przedziale wiekowym od 30 do 50 lat. Średni wiek ankietowanych wynosi około **41 lat**, a mediana **39 lat**. Oznacza to, że nieliczna grupa starszych ankietowanych klientów lekko zawyża średnią.

### Struktura zawodowa:
Pracownicy fizyczni (*blue-collar*) oraz kadra zarządzająca (*management*) stanowią dominującą grupę ankietowanych. Najmniejszą grupę stanowią studenci. W przypadku 0,64% ankietowanych klientów zatrudnienie jest nieznane.

### Analiza konwersji:
* Wskaźnik konwersji wyniósł **11,70%** (pozytywną odpowiedź wyrażała średnio co dziewiąta lub dziesiąta osoba).
* Grupy o najwyższym współczynniku konwersji to **studenci oraz emeryci** (przekraczający 20% zgód).
* Na trzecim miejscu znajdują się osoby bezrobotne.
* Najniższą skłonność do zakupu wykazują pracownicy fizyczni (*blue-collar*).
* Wraz ze wzrostem wieku ankietowanych wzrasta ich współczynnik konwersji – praktycznie co druga osoba w wieku powyżej 65 lat decyduje się na ofertę.

## 5. Modelowanie
Podczas przygotowania danych nie zidentyfikowano silnych korelacji pomiędzy zmiennymi a decyzją. Jedną z wybijających się cech jest posiadanie przez ankietowanego kredytu hipotecznego, który zmniejsza szansę konwersji.

Zidentyfikowano **wyciek danych (*Data Leakage*)** w zmiennej `duration` (czas trwania rozmowy). Cecha ta nie jest dostępna przed wykonaniem połączenia przedstawiającego ofertę; model musi przewidywać wynik przed kontaktem, aby bank mógł podjąć decyzję, któremu klientowi przedstawić ofertę.

## 6. Strategie modelowania (Analiza wariantów)

| Kryterium | Wariant A: Regresja Logistyczna | Wariant B: Sieć Neuronowa (MLP) |
| :--- | :--- | :--- |
| **Recall** | Model wyłapuje większość chętnych (**0.62**). | Bank traci 72% potencjalnych klientów (**0.28**). |
| **Precyzja** | Niska (**0.23**) – wiele zbędnych telefonów. | Wysoka (**0.55**) – większość telefonów to sukcesy. |
| **Charakter** | Cechy są możliwe do interpretacji. | Czarna skrzynka – brak znajomości powodu decyzji. |
| **Koszt** | Wyższy (większa liczba połączeń). | Niższy. |

### Analiza wag modelu (Wariant A):
* **Wagi Pozytywne:** Sukces w przeszłości (`poutcome_success`), właściwy moment (`month_mar`, `month_oct`), emeryci i studenci, edukacja wyższa.
* **Wagi Ujemne:** Niewłaściwy moment (`month_jan`, `month_nov`), zadłużenie (`housing_yes`, `loan_yes`).

## 7. Analiza SWOT
* **Mocne strony:** Automatyczne wytypowanie potencjalnych klientów decydujących się na lokatę.
* **Słabe strony:** Niska precyzja powoduje nadal dużą ilość zbędnych telefonów.
* **Szanse:** Personalizacja oferty pod klientów z dużą szansą na sukces – Studenci oraz Emeryci.
* **Zagrożenia:** Czynniki geopolityczne i zmienność rynkowa nieuwzględnione w modelu.

## 8. Studium Wykonalności i Rekomendacja
Raport odpowiada na trzy kluczowe pytania decyzyjne:
1. **Czy to rozwiązanie jest możliwe technicznie?** Tak, analiza wykazała, że dane historyczne pozwalają na skuteczne trenowanie modeli klasyfikacyjnych.
2. **Czy się opłaca?** Tak, automatyzacja wyboru klientów pozwala zredukować koszty operacyjne Call Center.
3. **Czy warto je wdrożyć?** Tak, z punktu widzenia decyzji organizacji pozwala to na świadome targetowanie grup o wysokiej konwersji.

**Rekomendacja końcowa:** Wprowadzenie rozwiązania jest możliwe. **Rekomenduje się wprowadzenie wariantu A: Regresja Logistyczna**, ponieważ model ten jest w pełni interpretowalny i wyłapuje większą liczbę chętnych.

---

## Załączniki
### Organizacja Projektu (CCDS)
```text
├── README.md          <- Raport
├── data
│   ├── processed      <- Dane przetworzone
│   └── raw            <- Dane oryginalne
├── notebooks          <- Jupyter Notebooks z kodem analizy
├── reports
│   └── figures        <- Wygenerowane wykresy
└── src                <- Kod źródłowy projektu