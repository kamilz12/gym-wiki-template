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
3. **Otwórz repo w Claude Code** (albo innym agencie) i poproś o `grilling` na start:

   > Przeczytaj `AGENT.md`. Zgrilluj mnie nt. założenia mojego gym-wiki — chcę ustalić cel, horyzont, ograniczenia zdrowotne, rytm dnia i żywienie, zanim zaczniemy zapisywać cokolwiek. Na podstawie odpowiedzi zaktualizuj `AGENT.md` (sekcja celu, zasady zdrowie/repo), zapisz `raw/journal/baseline.md` jako punkt zerowy, zaproponuj pierwszy szkic `wiki/plan/plan-aktualny.md`, zaktualizuj `index.md` i dodaj pierwszy wpis do `log.md`. Nie zgaduj liczb, których nie podałem — zostaw puste albo dopytaj.

   Skill `grilling` jest dołączony do repa w `.claude/skills/grilling` (patrz sekcja niżej) — działa od razu, bez instalowania pluginu. Agent zada Ci pytania rundami (jedno po drugim, z rekomendowaną odpowiedzią przy każdym), zamiast ankiety naraz, i dopiero po ustaleniu wszystkiego zacznie coś zapisywać.
4. Dalej po prostu **dyktuj kolejne dni** (operacja `wpis`) i raz w tygodniu proś o **`przegląd tygodnia`** — agent sam zbuduje strony w `wiki/` (plan, ćwiczenia, żywienie, wnioski) i zaktualizuje `index.md`.
5. Opcjonalnie: otwórz folder w Obsidianie, żeby czytać wiki z linkami `[[...]]` i grafem połączeń.

## Skill: `grilling`

W repo jest dołączony skill projektowy `.claude/skills/grilling` (skopiowany z [mattpocock/skills](https://github.com/mattpocock/skills), MIT — patrz [NOTICE](.claude/skills/grilling/NOTICE.md)). Działa od razu po sklonowaniu, bez instalowania pluginu.

Grilluje Cię pytanie po pytaniu (z rekomendowaną odpowiedzią przy każdym), zamiast czekać aż sam wymyślisz wszystkie decyzje — dobre do rzeczy, gdzie łatwo coś przeoczyć albo pójść na skróty. Poza pierwszym ustawieniem (krok 3 wyżej), warto po niego sięgnąć też przy:

- **przebudowie planu treningowego/dietetycznego** — gdy zmieniasz coś strukturalnie (nowa rotacja, nowe cele makro), a nie tylko dokładasz jedno danie czy jedno ćwiczenie,
- każdej sytuacji, gdzie czujesz, że decyzja ma dużo rozgałęzień i łatwo coś po drodze zgubić.

Wywołanie: poproś agenta wprost, np. *"zgrilluj mnie nt. przebudowy planu żywieniowego"*.

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
