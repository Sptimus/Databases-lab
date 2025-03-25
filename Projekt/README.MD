# System Zarządzania Urlopami

Niniejszy projekt przedstawia przykładowe rozwiązanie bazodanowe służące do ewidencji i zarządzania urlopami pracowników w firmie. W dokumentacji omówione są kluczowe etapy tworzenia systemu:

- **Analiza wymagań**  
- **Projekt modelu danych** (DZE → model relacyjny)  
- **Implementacja schematu bazy** (z zasadami poprawności danych)  
- **Niedeklaratywne mechanizmy walidacji** (procedury składowane)  
- **Przykładowe dane**  
- **Zasady ochrony bazy danych** (kopie zapasowe, uprawnienia)

## Spis treści

1. [Cel systemu](#cel-systemu)  
2. [Wymagania systemowe](#wymagania-systemowe)  
3. [Diagram klas i transformacja do modelu relacyjnego](#diagram-klas-i-transformacja-do-modelu-relacyjnego)  
4. [Zasady poprawności danych](#zasady-poprawności-danych)  
5. [Schemat bazy danych](#schemat-bazy-danych)  
6. [Niedeklaratywne mechanizmy walidacji](#niedeklaratywne-mechanizmy-walidacji)  
7. [Przykładowe dane](#przykładowe-dane)  
8. [Ochrona bazy danych](#ochrona-bazy-danych)  
9. [Jak uruchomić projekt](#jak-uruchomić-projekt)  

---

## 1. Cel systemu
Celem systemu jest zapewnienie skutecznej ewidencji i zarządzania urlopami pracowników z uwzględnieniem:

- Przyznawania puli urlopów proporcjonalnie do stażu pracy.
- Kontroli dostępnych i wykorzystanych dni urlopowych.
- Obsługi różnych typów urlopów (wypoczynkowy, okolicznościowy, bezpłatny, etc.).
- Automatycznej weryfikacji wniosków urlopowych (terminy, status akceptacji).
- Raportowania użytecznego dla działu HR oraz przełożonych.
- Zgodności z przepisami Kodeksu Pracy.

---

## 2. Wymagania systemowe
System powinien spełniać następujące wymagania:

- **Obsługa puli urlopów** zależnej od stażu pracy.
- **Monitorowanie dni urlopowych** (wykorzystanych, pozostałych, zaległych).
- **Kontrola dni wolnych ustawowo** (święta, weekendy) przy planowaniu urlopu.
- **Struktura organizacyjna** – przechowywanie informacji o wydziałach, przełożonych i podwładnych.
- **Status akceptacji** – wnioski urlopowe muszą być zatwierdzane wyłącznie przez bezpośredniego przełożonego.
- **Raporty** generowane raz w miesiącu z informacjami o stanie urlopów.

---

## 3. Diagram klas i transformacja do modelu relacyjnego
W projekcie zdefiniowano następujące klasy, odzwierciedlające kluczowe encje:

- **Wydział**  
  Atrybuty: ID Wydziału, Nazwa Wydziału, Kierownik  
- **Pracownik**  
  Atrybuty: ID pracownika, Imię, Nazwisko, PESEL, Adres, Data Urodzenia, Wykształcenie, itp.  
- **UrlopNależnyWDanymRoku**  
  Atrybuty: ID roku, Nominał urlopu, Ilość wykorzystanych dni  
- **Urlop**  
  Atrybuty: ID urlopu, Typ urlopu, Data rozpoczęcia, Data zakończenia, Liczba dni urlopu, Status akceptacji  

Po analizie dokonano **transformacji** DZE w dobrze znormalizowany **model relacyjny** (3. postać normalna).  

---

## 4. Zasady poprawności danych
W projekcie uwzględniono szczegółowe **reguły poprawności**:

- **Klauzule `CHECK`, `UNIQUE`, `NOT NULL`, `FOREIGN KEY`** na poziomie tabel:
  - Wymuszanie formatu PESEL.
  - Weryfikacja długości kodu pocztowego.
  - Sprawdzanie zakresu `Stażu Pracy`, `Nominału urlopu`, `Liczby dni urlopu` itp.
- **Kontrola wartości słownikowych** – np. typ urlopu (Urlop wypoczynkowy, okolicznościowy, bezpłatny), status zatrudnienia (Aktywny, Nieaktywny) itp.
- **Kontraints** wymuszające spójność logiczną (np. data zwolnienia > data zatrudnienia, data zakończenia urlopu > data rozpoczęcia).

---

## 5. Schemat bazy danych
W sekcji tej zaprezentowano kompletne skrypty **`CREATE TABLE`** dla tabel:

1. **Wydział**  
2. **Pracownicy** (z kluczem obcym do tabeli Wydział)  
3. **UrlopNależny**  
4. **Urlopy**  

Każda tabela zawiera klucz główny, odpowiednie **klauzule `CHECK`** i **wymuszoną relację** (klucz obcy) tam, gdzie to konieczne.

**Przykład (fragment):**

```sql
CREATE TABLE Wydział (
    [ID Wydziału] INTEGER PRIMARY KEY,
    [Nazwa Wydziału] VARCHAR(25) NOT NULL,
    [Kierownik] VARCHAR(25) NOT NULL,
    CONSTRAINT [IX_Wydział_ID] UNIQUE ([ID Wydziału]),
    CONSTRAINT [CK_Wydział_Nazwa] 
        CHECK ([Nazwa Wydziału] IS NOT NULL 
            AND [Nazwa Wydziału] NOT LIKE '%[!@#$%^&*(),.?":{}|<>]%'),
    ...
);
```

---

## 6. Niedeklaratywne mechanizmy walidacji
W celu dodatkowej walidacji i logiki biznesowej, poza **klauzulami `CHECK`**, zastosowano **procedury składowane** (`Stored Procedures`). Przykładowo:

- **`SprawdzWykorzystanyUrlop`** – weryfikuje, czy liczba wykorzystanych dni nie przekracza nominalnego urlopu.  
- **`SprawdzIWSstawUrlop`** – przed dodaniem nowego urlopu sprawdza poprawność dat i limitu urlopowego.  
- **`SprawdzIWSstawPracownika`** – weryfikuje dane pracownika (m.in. datę zatrudnienia i zwolnienia).

Każda procedura w razie błędów zwraca **komunikaty `RAISERROR`** i przerywa wykonywanie instrukcji.

---

## 7. Przykładowe dane
System można zasilić początkowymi danymi, wstawiając np. wydziały, pracowników i ich urlopy:

```sql
INSERT INTO Wydział ([ID Wydziału], [Nazwa Wydziału], [Kierownik])
VALUES 
  (1, 'Wydział Księgowości', 'Jan Kowalski'),
  (2, 'Wydział Projektowy', 'Anna Nowak');
```

Analogicznie wprowadzono przykładowych pracowników, nominały urlopów i wpisy do tabeli `Urlopy`.

---

## 8. Ochrona bazy danych
Aby zapewnić **bezpieczeństwo i ciągłość działania**, zaproponowano:

1. **Regularne tworzenie kopii zapasowych** (pełne, różnicowe, log transakcji).  
2. **Szyfrowanie danych** i przechowywanie backupów na odseparowanych serwerach.  
3. **Zarządzanie dostępem** – uprawnienia, role, audyt.  
4. **Automatyzację backupów** z wykorzystaniem SQL Server Agent.  

**Przykład tworzenia pełnej kopii zapasowej**:

```sql
BACKUP DATABASE ZarzadzanieUrlopami
TO DISK = 'C:\Backup\ZarzadzanieUrlopami_Full.bak'
WITH FORMAT,
     MEDIANAME = 'ZarzadzanieUrlopamiBackup',
     NAME = 'Pelna kopia zapasowa bazy ZarzadzanieUrlopami';
GO;
```
