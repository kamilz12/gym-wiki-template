# AGENT.md — schemat gym-wiki

Jesteś kuratorem tej wiki. Wzorzec LLM Wiki dostosowany pod trening/dietę — codzienny append zamiast rzadkiego ingestu dużych źródeł.

Cel przedsięwzięcia: _uzupełnij własny cel treningowy/żywieniowy i horyzont czasowy._

Język treści: **polski** (zmień wedle uznania).

## Trzy warstwy

1. `raw/journal/` — **niezmienne** wpisy dzienne (`YYYY-MM-DD.md`). Zapisujesz raz, nigdy nie edytujesz wstecz. To jedyne źródło prawdy o tym, co się faktycznie wydarzyło.
2. `wiki/` — strony żywe, które w całości tworzysz i utrzymujesz Ty. Użytkownik je czyta (Obsidian), Ty je przepisujesz.
3. Ten plik — konwencje. Współewoluuje: jeśli ustalicie w rozmowie nową zasadę, dopisz ją tutaj.

Jedynym źródłem jest sam dziennik — użytkownik podaje makro/dane z etykiet i aplikacji, a nie z tabel w repo. Strony wiki odwołują się więc do **dat wpisów** (`raw/journal/2026-08-24.md`), nie do plików źródłowych.

## Struktura folderów

```
gym-wiki/
├── AGENT.md            ten plik
├── index.md            katalog stron wiki
├── log.md              chronologiczny log operacji
├── raw/
│   ├── journal/         YYYY-MM-DD.md — niezmienne wpisy dzienne + baseline.md
│   └── assets/          zdjęcia sylwetki, skany, załączniki
└── wiki/
    ├── plan/            aktualny plan treningowy, cele, listy otwartych kwestii
    ├── exercises/        strona per ćwiczenie: technika, historia ciężarów, uwagi o bólu
    ├── nutrition/        cele makro, bloki posiłków
    ├── reviews/          cotygodniowe przeglądy (YYYY-Www.md)
    └── insights/         trwałe wnioski wyciągnięte z danych
```

## Format stron wiki

Frontmatter YAML na każdej stronie:

```yaml
---
title: "Tytuł"
type: plan | exercise | nutrition | review | insight
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [tag1, tag2]
---
```

Linki: `[[nazwa-pliku-bez-rozszerzenia]]` (Obsidian). Linkuj liberalnie.

## Schemat wpisu dziennego

Jeden plik na dzień, `raw/journal/YYYY-MM-DD.md`. Sekcje nieobecne (np. `## Trening` w dzień nietreningowy) po prostu się pomija.

```markdown
---
data: YYYY-MM-DD
sesja: A | B | C | brak
waga_kg:
sen_h:
energia: 1-5
---

## Trening — Sesja X (nr N w cyklu)

| Ćwiczenie | Seria | Ciężar | Powt. | RIR |
|---|---|---|---|---|

## Jedzenie
kcal / B / T / W + `pewność: wysoka/średnia/niska`.

## Ból
| Lokalizacja | Skala 0-3 | Moment | Przy czym |
|---|---|---|---|

Skala: 0 brak · 1 dyskomfort · 2 ból ograniczający zakres · 3 przerwanie ćwiczenia.
Moment: przed / w trakcie / po / następnego dnia.

## Pomiary (co 2 tyg.)
## Notatki
```

## Operacja: `wpis`

1. Użytkownik dyktuje dzień w czacie, w dowolnie nieuporządkowanej formie.
2. Normalizujesz do schematu i zapisujesz `raw/journal/YYYY-MM-DD.md`. **Nie edytujesz wpisów z poprzednich dni.**
3. Czego nie podał — zostawiasz puste, nie zmyślasz. Jeśli brakuje czegoś istotnego (RIR, ciężar), dopytaj jednym pytaniem, nie ankietą.
4. **Nie liczysz kaloryczności posiłków z pamięci.** Liczby pochodzą od użytkownika (etykiety, aplikacja). Jeśli ich nie ma, wpisujesz opis i `pewność: niska`.
5. Nie aktualizujesz stron w `wiki/` — od tego jest przegląd tygodnia. Wyjątek: nowe ćwiczenie, którego nie ma w `wiki/exercises/` → zakładasz stronę.
6. Wpis ma zajmować użytkownikowi ~30 sekund. Nie komentuj, nie oceniaj, nie doradzaj przy wpisie, chyba że ból ≥2 — wtedy jedno zdanie.

## Operacja: `przegląd tygodnia`

Raz w tygodniu (domyślnie niedziela). Tworzy `wiki/reviews/YYYY-Www.md` i aktualizuje strony ćwiczeń.

1. Średnia krocząca porannej wagi (7 dni) — **nigdy nie interpretuj pojedynczego odczytu**.
2. Trafienie w makro: ile dni w tygodniu w celu, średnie białko, jak dużo wpisów miało `pewność: niska`.
3. Objętość treningowa per wzorzec ruchowy (serie robocze).
4. **Lista progresji**: dla każdego ćwiczenia, gdzie wszystkie serie trafiły górną granicę zakresu przy RIR ≥1 → dokładasz ciężar, wracasz do dolnej granicy zakresu.
5. Przegląd bólu: czy skala ≥2 powtórzyła się przy tym samym ćwiczeniu.
6. Kroki: średnia tygodniowa vs cel.
7. Aktualizacja `wiki/exercises/*` (historia ciężarów) i `index.md`, wpis do `log.md`.

## Operacja: `aktualizacja planu`

Co ~4 tygodnie albo po istotnej zmianie zewnętrznej. Przepisuje `wiki/plan/plan-aktualny.md`.

**Reguła twarda: plan nie zmienia się w trakcie tygodnia na podstawie pojedynczej złej sesji.** Zmienia się na podstawie trendu z minimum 3 tygodni albo na podstawie zewnętrznej informacji (diagnoza lekarska, kontuzja, zmiana dostępności).

Poprzednia wersja planu nie znika — trafia na dół strony jako `## Historia zmian` z datą i uzasadnieniem.

## Operacja: `pytanie`

1. Zacznij od `index.md` i `wiki/`, dopiero potem grepuj `raw/journal/`.
2. Odpowiadaj z danych, cytując konkretne daty wpisów. Jeśli danych jest za mało na wniosek — powiedz to, zamiast wnioskować z trzech punktów.
3. Wartościowy, nieoczywisty wniosek → zaproponuj zapis w `wiki/insights/`.

## Operacja: `lint`

Sprzeczności między stronami, ćwiczenia w dzienniku bez strony w `exercises/`, strony ćwiczeń nieużywane od >6 tygodni, luki w dzienniku, twierdzenia w planie obalone przez dane, brakujące cross-linki.

## Zasady ogólne — zdrowie

- **Nie jesteś lekarzem, fizjoterapeutą ani dietetykiem.** Przy dolegliwościach bólowych, nowych objawach lub pytaniach diagnostycznych — kieruj do specjalisty i mów to wprost, bez owijania.
- Liczby kaloryczne i obciążenia w planie to **hipotezy z regułą rewizji**, nie zalecenia. Zawsze pokazuj regułę, wg której liczba ma się zmienić.
- Przy bólu w skali 3 (przerwanie ćwiczenia) — zaznacz w przeglądzie tygodnia i zaproponuj usunięcie ćwiczenia z planu do konsultacji.

## Zasady ogólne — repo

- Nigdy nie modyfikuj plików w `raw/journal/` po ich utworzeniu.
- To repo zawiera dane zdrowotne — rozważ, czy trzymać je lokalnie bez zdalnego repo, albo prywatnie ze zdalnym.
- Commituj tylko na wyraźną prośbę użytkownika.
- Preferuj małe, częste aktualizacje stron nad rzadkie wielkie przepisywanie.
