# Bazy Danych 2 - Laboratorium 1

## Wprowadzenie
To repozytorium zawiera materiały do **Laboratorium 1** z kursu **Bazy Danych 2**. Laboratorium obejmuje podstawowe operacje SQL, w tym zapytania, agregację oraz łączenie tabel. Ćwiczenia mają na celu wzmocnienie umiejętności pracy z **Structured Query Language (SQL)** i jego praktycznego zastosowania.

## Tematy laboratorium
Laboratorium obejmuje następujące zagadnienia:

1. **Podstawowe zapytania SQL**
2. **Filtrowanie i sortowanie danych**
3. **Funkcje agregujące**
4. **Łączenie tabel**
5. **Podzapytania i funkcje okienkowe**

## Podstawy teoretyczne
Bazy danych są niezbędne do przechowywania, organizowania i zarządzania dużymi zbiorami danych. SQL (Structured Query Language) to standardowy język umożliwiający operowanie na relacyjnych bazach danych.

### Kluczowe pojęcia:
- **Relacyjne bazy danych (RDBMS)** - przechowują dane w tabelach powiązanych relacjami.
- **Klucz główny (Primary Key, PK)** - unikalny identyfikator rekordu.
- **Klucz obcy (Foreign Key, FK)** - odniesienie do innej tabeli.
- **Normalizacja** - minimalizuje redundancję i zapewnia spójność danych.
- **Transakcje (ACID)** - gwarantują integralność danych.

### Omówione operacje SQL:
- **SELECT** – pobieranie danych.
- **WHERE** – filtrowanie wyników.
- **ORDER BY** – sortowanie.
- **GROUP BY & HAVING** – agregacja danych.
- **JOIN** – łączenie tabel.
- **Podzapytania & Funkcje okienkowe** – zaawansowane operacje na danych.

## Ćwiczenia

Ćwiczenia w tym laboratorium obejmują:

### Podstawowe zapytania SELECT
1. Pobranie wszystkich kolumn dla miast w USA o populacji większej niż 100 000.
2. Pobranie nazw miast w USA o populacji większej niż 120 000.
3. Pobranie wszystkich kolumn z tabeli CITY.
4. Pobranie konkretnego miasta na podstawie ID.
5. Pobranie wszystkich atrybutów dla miast w Japonii.
6. Pobranie nazw wszystkich japońskich miast.
7. Pobranie miast i stanów z tabeli STATION.
8. Pobranie miast z parzystymi identyfikatorami.
9. Obliczenie różnicy między całkowitą liczbą rekordów a liczbą unikalnych nazw miast.
10. Znalezienie najkrótszych i najdłuższych nazw miast.

### Funkcje agregujące
11. Liczba miast o populacji większej niż 100 000.
12. Suma populacji miast w Kalifornii.
13. Średnia populacja miast w Kalifornii.
14. Całkowita populacja japońskich miast.
15. Różnica między największą i najmniejszą populacją miast.
16. Obliczenie łącznych zarobków pracowników.

### Łączenie tabel (JOIN)
17. Pobranie całkowitej populacji miast na kontynencie azjatyckim.
18. Obliczenie średniej populacji miast dla każdego kontynentu.
19. Identyfikacja hakerów z pełnymi wynikami w więcej niż jednym zadaniu.
20. Znalezienie najniższej ceny różdżek o wysokiej mocy.
21. Pobranie rankingu uczestników konkursów hakerskich.
22. Lista studentów, których najlepsi przyjaciele otrzymali wyższe wynagrodzenie.

## Jak wykonać laboratorium
1. **Zarejestruj się** na [HackerRank](https://www.hackerrank.com/domains/sql) (jeśli nie masz konta).
2. **Przejdź do zadań SQL** na platformie HackerRank.
3. **Rozwiązuj zadania** według instrukcji zawartych w laboratorium.
4. **Testuj swoje rozwiązania** uruchamiając zapytania SQL.

## Narzędzia i technologie
- **SQL** (MySQL, PostgreSQL, SQL Server lub inna kompatybilna baza danych)
- **Zadania SQL na HackerRank**
- **System zarządzania bazami danych (DBMS)** do lokalnych testów - podczas kolejnych Labów 🙂

## Dodatkowe materiały
- [W3Schools SQL Tutorial](https://www.w3schools.com/sql/)
- [SQL Zoo](https://sqlzoo.net/)
- [HackerRank SQL Challenges](https://www.hackerrank.com/domains/sql)

## Struktura repozytorium
```
├── README.md  # Opis laboratorium i instrukcje
├── lab1_tasks.sql  # Zapytania SQL do ćwiczeń
├── dataset/  # Schematy bazy danych i przykładowe dane
└── solutions/  # Proponowane rozwiązania (jeśli dotyczy)
```

## Licencja
Ten projekt jest przeznaczony do celów edukacyjnych. Wszelkie prawa do oryginalnych materiałów należą do ich prawowitych właścicieli.

---
**Powodzenia i miłej nauki SQL!**

