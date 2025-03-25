## Zakres tematyki

1. **Prosta selekcja** – pokazanie wyników z pojedynczej tabeli:
   - Wyświetlanie wszystkich kolumn (np. `SELECT * FROM Produkty;`)
   - Wyświetlanie wybranych kolumn (np. `SELECT Imię, Nazwisko, DataUrodzenia FROM Pracownicy;`)

2. **Sortowanie wyników (`ORDER BY`)** – sortowanie wg. rosnących i malejących wartości (np. sortowanie po cenach, nazwiskach).

3. **Pobieranie ograniczonej liczby wierszy (`TOP` / `TOP PERCENT`)** – np. wyświetlanie 10 najdroższych produktów albo ostatnich 3% zamówień.

4. **Usuwanie duplikatów (`DISTINCT`)** – np. lista unikalnych krajów, w których mieszkają klienci.

5. **Łączenie łańcuchów tekstowych (konkatenacja)** – np. tworzenie kolumny `Pracownik` z imienia i nazwiska (`SELECT Imię + ' ' + Nazwisko AS Pracownik ...`).

6. **Konwersje typów (`CAST`, `YEAR`, `LEN`)** – m.in. wyciąganie roku z daty, konwertowanie typu całkowitoliczbowego na `nvarchar`.

7. **Operacje arytmetyczne** – np. obliczanie wartości stanu magazynowego produktu czy stażu pracy w latach.

8. **Filtrowanie danych**:
   - Porównywanie z wartościami (`WHERE`, `>, <, =`)
   - Zakresy wartości (`BETWEEN ... AND ...`)
   - Wyszukiwanie w liście wartości (`IN (...)`)
   - Sprawdzanie wartości pustych (`IS NULL`, `IS NOT NULL`)
   - Wzorce tekstowe (`LIKE`, znaki wieloznaczne `_`, `%`, zakresy znakowe `[a-c]`, itp.)
   - Operatory logiczne (`AND`, `OR`, `NOT`)

9. **Wzorce tekstowe (`LIKE`)** – wyszukiwanie nazw rozpoczynających się/kończących się na określoną literę, sprawdzanie długości łańcucha itp.

10. **Obliczanie różnicy w datach** – np. wyliczanie liczby dni między datą zamówienia a datą wysyłki (`CAST(DataWysyłki AS int) - CAST(DataZamówienia AS int)`).

## Struktura przykładowych zapytań

Plik podzielony jest na sekcje (P01, P02, P03, …), gdzie każda sekcja zawiera kilka zapytań ilustrujących określoną funkcjonalność.

## Jak korzystać z tych przykładów

1. Upewnij się, że korzystasz z właściwej bazy danych (np. `USE BD2024_z_2A;`).
2. Możesz kopiować zapytania bezpośrednio do edytora SQL w swoim środowisku.
3. Korzystaj z przykładów jako punktu wyjścia do pisania własnych zapytań.


## Licencja i uwagi

- Plik zawiera przykładowe zapytania i może być modyfikowany według potrzeb.  
- Wszystkie zapytania mają charakter edukacyjny, mogą nie uwzględniać pełnej optymalizacji czy indeksów.

---
