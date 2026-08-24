# gym-wiki-template

Szablon do prowadzenia własnej "gym-wiki" — dziennika treningowego/żywieniowego prowadzonego wspólnie z asystentem LLM (np. [Claude Code](https://claude.com/product/claude-code)), w formie plików Markdown do czytania w [Obsidianie](https://obsidian.md/).

Zasada: **Ty dyktujesz dzień w kilku zdaniach, agent normalizuje to do schematu i utrzymuje resztę wiki** (plany, strony ćwiczeń, przeglądy tygodnia, wnioski). Wszystko zostaje jako zwykłe pliki `.md` w tym repo — żadnej zewnętrznej aplikacji.

## Start

1. **Sklonuj repo:**
   ```bash
   git clone https://github.com/kamilz12/gym-wiki-template.git twoje-gym-wiki
   cd twoje-gym-wiki
   ```
2. **Przeczytaj [`AGENT.md`](AGENT.md)** — to jest cały schemat: struktura folderów, format wpisu dziennego, operacje (`wpis`, `przegląd tygodnia`, `aktualizacja planu`, `pytanie`, `lint`). Dostosuj go do siebie *zanim* zaczniesz — w szczególności:
   - sekcja **"Cel przedsięwzięcia"** na górze (co trenujesz, jaki masz cel, jaki horyzont czasowy),
   - **"Zasady ogólne — zdrowie"** — dopisz swoje kontuzje/ograniczenia, jeśli jakieś masz,
   - **"Zasady ogólne — repo"** — zdecyduj, czy trzymasz repo lokalnie bez zdalnego (dane zdrowotne), czy jednak ze zdalnym, ale prywatnym.
3. **Otwórz repo w Claude Code** (albo innym agencie) i poproś o operację `wpis` — podyktuj pierwszy dzień w dowolnej, nieuporządkowanej formie (trening, jedzenie, sen, ból). Agent zapisze go w `raw/journal/YYYY-MM-DD.md` wg schematu z `AGENT.md`.
4. **Poproś o `baseline`** — jednorazowy wpis `raw/journal/baseline.md` z punktem startowym (waga, obwody, zdjęcia w `raw/assets/`, jeśli chcesz).
5. Dalej po prostu **dyktuj kolejne dni** (operacja `wpis`) i raz w tygodniu proś o **`przegląd tygodnia`** — agent sam zbuduje strony w `wiki/` (plan, ćwiczenia, żywienie, wnioski) i zaktualizuje `index.md`.
6. Opcjonalnie: otwórz folder w Obsidianie, żeby czytać wiki z linkami `[[...]]` i grafem połączeń.

## Struktura

```
gym-wiki/
├── AGENT.md    konwencje i operacje — zacznij tutaj
├── index.md    katalog stron wiki
├── log.md      chronologiczny log operacji agenta
├── raw/
│   ├── journal/  wpisy dzienne, niezmienne po zapisaniu
│   └── assets/   zdjęcia, skany
└── wiki/
    ├── plan/         aktualny plan treningowy
    ├── exercises/    strona per ćwiczenie
    ├── nutrition/    cele makro, posiłki
    ├── reviews/      cotygodniowe przeglądy
    └── insights/     trwałe wnioski z danych
```

## Uwaga o danych

To repo trzyma dane zdrowotne (waga, obciążenia, ból, ewentualnie zdjęcia). `AGENT.md` domyślnie sugeruje rozważenie, czy trzymać repo bez zdalnego. Jeśli dodajesz zdalne repo (GitHub itp.), **ustaw je jako prywatne**.
