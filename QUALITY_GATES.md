# QUALITY GATES — Kurtyna
# System kontroli jakości dla 9-etapowego pipeline'u
# Wersja 1.0 (kwiecień 2026)

═══════════════════════════════════════════════════════════
JAK CZYTAĆ TEN PLIK
═══════════════════════════════════════════════════════════

Ten plik definiuje **twarde kryteria PASS/FAIL** dla każdego
z 9 etapów workflow. Po zakończeniu każdego etapu Claude
**automatycznie** odpala self-check i prezentuje **Diagnostic
Card** w formacie zdefiniowanym w tym pliku.

Ty (operator) patrzysz na Diagnostic Card i decydujesz:
- Wszystko PASS i sam też nie widzisz problemu → **"Etap N+1"**
- FAIL na konkretnym kryterium → **"Iteruj akapit X.Y"** lub
  **"Iteruj rozdział N: [komentarz]"**
- PASS u Claude'a, ale Twoje wyczucie mówi inaczej → **piszesz
  konkretny feedback**, plik stylu się aktualizuje, iterujesz

**ZASADA NACZELNA:** Diagnostic Card to nie ozdoba. To formalna
pauza w pipeline, podczas której podejmujesz świadomą decyzję
"dalej czy iterujemy". Bez Diagnostic Card nie ma przejścia do
następnego etapu.

═══════════════════════════════════════════════════════════
FORMAT DIAGNOSTIC CARD (uniwersalny)
═══════════════════════════════════════════════════════════

Każda Diagnostic Card ma TĘ SAMĄ strukturę:

```
═══ DIAGNOSTIC CARD — Etap N: [Nazwa Etapu] ═══

BOHATER: [Imię Nazwisko]
REJESTR: [A pikantny / B powściągliwy / AB mieszany]
DECYZJA REJESTRU: [krótkie uzasadnienie 1-2 zdania]

METRYKI:
  - [metryka 1]: [wartość] [✓ lub ✗]
  - [metryka 2]: [wartość] [✓ lub ✗]
  - [...]

SKAN ANTY-WZORCÓW (#1-13 z STYLE_PL_TWOJ_v5_1):
  - #9 Myślnik wstawkowy: [liczba wystąpień, miejsca]
  - #10 "To-to": [liczba wystąpień]
  - #11 Trójki anaforyczne: [liczba wystąpień]
  - #12 Imiesłowy aktywne: [liczba wystąpień]
  - #13 Kalki idiomów: [liczba wystąpień, jakie]

WZORCE KURTYNY:
  - Hook strategy: [A/B/C/D/E lub kombinacja]
  - Czas gramatyczny: [poprawnie dobrany?]
  - "Wy piszecie o kim nagrać": [jest/nie ma]
  - Most do następnej sekcji: [jest/nie ma]
  - Konkretów per akapit: [średnia, min, max]

RYZYKA / NIEPEWNE FAKTY:
  1. [konkretne ryzyko, lokalizacja]
  2. [...]

REKOMENDACJA: [PASS / FAIL / PASS Z UWAGAMI]

JEŚLI FAIL — co iterować:
  - [konkretne miejsce X.Y]: [co zmienić]
  - [...]

CZEKAM NA TWOJĄ DECYZJĘ: dalej / iterujemy
```

═══════════════════════════════════════════════════════════
ETAP 1 — BOHATER + 3 KĄTY A/B/C
═══════════════════════════════════════════════════════════

## Co musi się zdarzyć

Claude proponuje:
1. Krótki briefing kim jest bohater (3-5 zdań kontekstu)
2. Ocenę rejestru (A pikantny / B powściągliwy / AB)
3. Sprawdzenie czy bohater już był w archiwum kanału
   (Subscribr `my_videos` + UserMemories + [LOGBOOK.md](http://LOGBOOK.md)
   jeśli istnieje)
4. **Research zewnętrzny ⭐ OBOWIĄZKOWY w v4.2**
   z hierarchią narzędzi:
   - Bright Data (domyślny scraper)
   - Exa: web_search_exa + web_fetch_exa
   - Tavily (fallback)
   - TranscriptAPI (wywiady wideo)
   - web_search Anthropic (ostatnia deska ratunku)
   Min. 8 źródeł zewnętrznych, min. 5 czytanych w pełni.
5. **STFS-light ⭐ NOWY w v4.2** — 10-15 faktów ze
   źródłami i pewnością WYS/ŚR/NIS
6. **3 kąty narracyjne A/B/C** (każdy z referencjami do
   STFS-light):
   - Kąt A: "Headline" — najbardziej znany dramat
   - Kąt B: "Connected" — wątek mniej znany, ale
     centralny dla biografii
   - Kąt C: "Hidden drama" — kontrowersja głębsza,
     wymagająca więcej researchu
7. Rekomendację któremu kątowi dać pierwszeństwo

## Quality Gate Etap 1 (TWARDY w v4.2)

**KRYTERIA PASS — IDENTYFIKACJA:**
- [ ] Bohater jednoznacznie zidentyfikowany (pełne imię,
      nazwisko, ewentualnie pseudonim)
- [ ] Sprawdzono czy bohater był wcześniej w odcinku
      (raport z UserMemories + Subscribr + LOGBOOK)

**KRYTERIA PASS — RESEARCH ZEWNĘTRZNY ⭐ NOWE w v4.2:**
- [ ] **Min. 2 narzędzia z hierarchii** użyte (Bright Data /
      Exa / Tavily / TranscriptAPI / web_search) — NIE
      tylko archiwum Subscribr ani LOGBOOK
- [ ] **Min. 8 źródeł zewnętrznych** zidentyfikowanych
- [ ] **Min. 5 źródeł** czytanych w pełni (clean markdown
      / web_fetch / scrape full content), nie tylko po
      snippetach
- [ ] **Lista użytych narzędzi i źródeł** widoczna w
      odpowiedzi

**KRYTERIA PASS — STFS-light ⭐ NOWE w v4.2:**
- [ ] **10-15 faktów** w STFS-light
- [ ] **100% faktów** ma URL/referencję do źródła
- [ ] **100% faktów** ma oznaczenie pewności WYS/ŚR/NIS
- [ ] Numeracja [L01], [L02], ... do referencji w kątach

**KRYTERIA PASS — KĄTY:**
- [ ] Trzy DYSTYNKTYWNE kąty (nie warianty tego samego)
- [ ] Każdy kąt ma 1-zdaniową tezę dramatyczną
- [ ] Każdy kąt ma 3 twarde fakty z **referencjami do
      STFS-light** (np. "[L03], [L07], [L11]")
- [ ] Fakty bez referencji do STFS-light flagowane jako
      "⚠️ WIEDZA TRENINGOWA"
- [ ] Rekomendacja Claude'a z uzasadnieniem

**NAJCZĘSTSZE PUŁAPKI ⭐ AKTUALIZACJA v4.2:**
- ❌ **Pominięcie researchu zewnętrznego** — Claude
  używa archiwum Subscribr + LOGBOOK + wiedzy treningowej
  jako "researchu". To FAIL. Research = zewnętrzne źródła
  spoza systemu Kurtyny.
- ❌ **Wikipedia jako jedyne źródło** — to NISKA pewność,
  daje tylko punkt startowy. Trzeba 7+ innych źródeł.
- ❌ **3 kąty z faktami "z głowy"** bez referencji do
  STFS-light — to halucynacje udające research. Każdy
  fakt musi mieć [L0X] lub flagę "WIEDZA TRENINGOWA".
- ❌ Trzy kąty są w istocie tym samym wątkiem z trzech
  perspektyw — POWINNY być 3 różne wątki
- ❌ Brak weryfikacji czy bohater już był w archiwum —
  ryzyko powtórzenia całego odcinka

**JEŚLI FAIL:**
- "Wykonaj Krok 3 — research zewnętrzny był pominięty.
  Użyj Bright Data + Exa + min. 8 źródeł."
- "Uzupełnij STFS-light — kąt B nie ma referencji do
  konkretnych faktów ze źródeł"
- "Powtórz research — Wikipedia jako jedyne źródło to za
  mało, dodaj biografie książkowe, profile w prasie"
- "Iteruj kąt A: chcę inny wątek, np. [konkret]"
- "Daj 2 nowe kąty zamiast B i C, te są zbyt podobne"

═══════════════════════════════════════════════════════════
ETAP 2 — OUTLINE + STFS + FACT ALLOCATION MAP
═══════════════════════════════════════════════════════════

## Co musi się zdarzyć (KLUCZOWY ETAP — bez kompromisów)

Claude produkuje:

1. **Source-Tagged Fact Sheet (STFS)** — kompletna lista
   faktów z dokładnymi źródłami

2. **Outline 13-akapitowy** — struktura odcinka:
   - Cold open (Sekcja 0)
   - 12 akapitów rozwijających (Sekcje 1-12)
   - Akapit zamykający (Sekcja 13)

3. **Fact Allocation Map** — przypisanie faktów z STFS
   do konkretnych sekcji

4. **Repetition Watchlist** — lista typowych powtórzeń
   biograficznych do świadomego pilnowania

5. **Rejestr-per-sekcja** — mapa rejestrów A/B/AB dla
   każdej z 13 sekcji

## Format STFS (Source-Tagged Fact Sheet)

```
STFS — [Bohater]

[F001] [Treść faktu]
   ŹRÓDŁO: [URL lub pełna referencja publikacji]
   PEWNOŚĆ: WYSOKA / ŚREDNIA / NISKA
   SPRAWDZONE W: [liczba niezależnych źródeł]
   KONFLIKT: [BRAK / TAK — opis konfliktu]
   DECYZJA NARRACYJNA:
     - WYSOKA → możesz pisać twardo
     - ŚREDNIA → "według [źródło] z [rok]..."
     - NISKA → "podobno", "krążą doniesienia",
              "anonimowe źródło"

[F002] [...]
```

**ZASADA TWARDA:** każdy fakt, który ma trafić do skryptu,
**MUSI** mieć wpis w STFS. Bez wyjątków.

## Format Fact Allocation Map

```
FACT ALLOCATION MAP — [Bohater]

Cold open (Sekcja 0):
  - [F002], [F015]

Sekcja 1 (Dzieciństwo):
  - [F001], [F003], [F004], [F007]

Sekcja 2 (Pierwszy kontrakt):
  - [F008], [F009], [F012]

[...]

Sekcja 13 (Outro):
  - [F045], [F046]
```

**ZASADA TWARDA:** każdy fakt **przypisany do JEDNEJ sekcji**.
Powtórki dozwolone tylko świadomie, oznaczone jako "wracając
do X".

## Format Repetition Watchlist

```
REPETITION WATCHLIST — [Bohater]

Typowe wątki które mogą się powtarzać:
  - "Wczesna bieda" — wzmianka tylko w Sekcji 1
  - "Pierwsza umowa" — tylko w Sekcji 2 i krótka
    re-wzmianka w Sekcji 12
  - "Punkt zwrotny X" — przypadek podany raz, w jednej
    konkretnej sekcji

Zachowanie:
  Claude w Etapie 5 sprawdza ten plik PRZED napisaniem
  każdej sekcji. Jeśli element został już użyty, NIE
  wraca do niego.
```

## Quality Gate Etap 2

**KRYTERIA PASS:**
- [ ] STFS zawiera **min. 30 faktów** (typowo 40-60)
- [ ] **100% faktów** ma źródło (URL lub konkretna
      publikacja)
- [ ] **100% faktów** ma oznaczenie pewności (WYSOKA/
      ŚREDNIA/NISKA)
- [ ] Konflikty źródeł zidentyfikowane i opisane
- [ ] Outline 13-akapitowy z tezami sekcji
- [ ] Fact Allocation Map: każdy fakt z STFS
      przypisany do dokładnie 1 sekcji
- [ ] Repetition Watchlist: min. 3 typowe pułapki
      powtórzeniowe zidentyfikowane
- [ ] Rejestr per-sekcja: każda z 13 sekcji ma oznaczenie
      A/B/AB z uzasadnieniem
- [ ] Sygnały dramy z celebrity-documentary-skill
      pokryte w outline (min. 5 z 13)

**NAJCZĘSTSZE PUŁAPKI:**
- ❌ Fakt "z głowy" bez źródła — Claude często to robi
  bo wie z treningu, ale to jest halucynacja albo
  niezweryfikowane. Musi mieć źródło.
- ❌ Pewność WYSOKA dla wszystkiego — ostrożność! Realnie
  mało faktów ma WYSOKĄ pewność, większość ŚREDNIA
- ❌ Outline bez konkretnych tez — Sekcja 4 nie może być
  "rozwój kariery", musi być "Pierwsze trasy w Niemczech
  i konflikt z managerem o tantiemy"
- ❌ Fact Allocation Map z duplikatami — fakt nie może
  być w dwóch sekcjach (poza wyjątkami świadomymi)

**JEŚLI FAIL:**
- "Uzupełnij STFS — fakty F012, F018 nie mają źródła"
- "Sprawdź konflikty — w sprawie [X] są dwie wersje
  faktów"
- "Iteruj outline Sekcję 4: za ogólne, daj konkret"
- "Repetition Watchlist za uboga — dodaj wątki [X], [Y]"

═══════════════════════════════════════════════════════════
ETAP 3 — COLD OPEN (3-5 PROPOZYCJI HOOKÓW)
═══════════════════════════════════════════════════════════

## Co musi się zdarzyć

Claude proponuje 3-5 wariantów cold open, każdy:
- 27-70 słów (w zakresie wyznaczonym przez 8 odcinków
  referencyjnych)
- Z curiosity gap + konkretami + pivotem
- W jednej z 5 strategii: A/B/C/D/E (z STYLE_PL_TWOJ
  Część IV § 14)
- W odpowiednim rejestrze (A/B/AB) zgodnie z mapą
  z Etapu 2

## Quality Gate Etap 3

**KRYTERIA PASS:**
- [ ] 3-5 wariantów (preferowane 4)
- [ ] Każdy 27-70 słów
- [ ] Każdy w innej strategii hooka (różnorodność)
- [ ] Curiosity gap obecny w każdym
- [ ] Min. 2 konkrety w każdym hooku
- [ ] Czas gramatyczny adekwatny
- [ ] Rejestr zgodny z mapą z Etapu 2
- [ ] Brak myślników wstawkowych w narracji
- [ ] Brak konstrukcji "to-to"
- [ ] Brak trójek anaforycznych

**NAJCZĘSTSZE PUŁAPKI:**
- ❌ Wszystkie warianty z tej samej strategii (np. cztery
  In Media Res) — daj dystynkcję
- ❌ Hook obiecuje X, a outline z Etapu 2 prowadzi do Y
  — sprzeczność
- ❌ Hook za długi (>70 słów) — wytraca rytm wejścia
- ❌ Hook za krótki (<27 słów) — brak buildupu

**JEŚLI FAIL:**
- "Iteruj wariant 2: brak curiosity gap"
- "Wszystkie warianty są w stylu Stats Cascade — daj
  jeden In Media Res, jeden Question Cascade"
- "Wariant 3 przekracza 70 słów, skróć"

═══════════════════════════════════════════════════════════
ETAP 4 — TYTUŁY YT + 3 KONCEPTY MINIATURY
═══════════════════════════════════════════════════════════

## Co musi się zdarzyć

Claude proponuje:
1. **5 tytułów YouTube** według formuł z title-formulas-skill
2. **3 koncepty miniatury** (A/B/C) z opisem:
   - Główny element wizualny
   - Tekst nakładkowy (max 4 słowa)
   - Emocja na twarzy bohatera
   - Kolorystyka

## Quality Gate Etap 4

**KRYTERIA PASS:**
- [ ] 5 tytułów, każdy z innej formuły
- [ ] Każdy tytuł 40-70 znaków (CTR-optymalne)
- [ ] Każdy tytuł obiecuje to, co odcinek faktycznie
      dostarcza (zgodnie z outline z Etapu 2)
- [ ] Brak clickbaitu nieuczciwego
- [ ] 3 koncepty miniatury wyraźnie różniące się
- [ ] Każdy koncept ma konkretne instrukcje wizualne
- [ ] Tekst nakładkowy max 4 słowa per miniaturkę
- [ ] Emocja na twarzy bohatera dobrana świadomie
      (nie tylko "zaskoczenie")

**NAJCZĘSTSZE PUŁAPKI:**
- ❌ Tytuły bardzo do siebie podobne — wybór staje się
  pozorny
- ❌ Tytuł obiecujący "ZNISZCZYŁA KARIERĘ", a w outline
  bohaterka ma się dobrze — sprzeczność
- ❌ Wszystkie miniatury z tym samym układem
  (twarz + tekst) — daj dystynkcję
- ❌ Tekst nakładkowy 6+ słów — nieczytelny w thumbnail

**JEŚLI FAIL:**
- "Tytuły 2 i 4 to ten sam wzorzec — daj inną formułę"
- "Iteruj koncept B miniatury: brakuje tekstu
  nakładkowego"
- "Tytuł 5 obiecuje za dużo, w outline tego nie ma"

═══════════════════════════════════════════════════════════
ETAP 5 — PEŁNY SKRYPT 3200 SŁÓW
═══════════════════════════════════════════════════════════

## Co musi się zdarzyć (NAJWAŻNIEJSZY ETAP)

Claude pisze pełny skrypt według:
- Wybranego hooka z Etapu 3
- Outline z Etapu 2
- **STFS jako jedynego źródła faktów**
- Fact Allocation Map (każdy fakt w przypisanej sekcji)
- Repetition Watchlist (świadome pilnowanie)
- Mapy rejestrów per-sekcja
- STYLE_PL_TWOJ_v5_[1.md](http://1.md) (kanon stylu)
- Rotation Log (variety-rotation-skill — 9 slotów)

## Quality Gate Etap 5 (RYGORYSTYCZNY)

**KRYTERIA PASS — METRYKI TWARDE:**
- [ ] **3 100-3 300 słów total** (sprawdzone przez `wc -w`)
- [ ] Cold open: **50-70 słów**
- [ ] 12 akapitów środkowych: średnia **240 słów**,
      każdy w przedziale **200-290**
- [ ] Akapit zamykający: **225 ± 25 słów**
- [ ] Sumarycznie 12 akapitów środkowych: **2 880 ± 50**
- [ ] Numery slotów Rotation Log oznaczone
- [ ] Rotation Log na końcu skryptu

**KRYTERIA PASS — STFS COMPLIANCE:**
- [ ] **100% faktów w skrypcie** ma odpowiednik w STFS
- [ ] **0 faktów spoza STFS** (jeśli Claude chce dodać —
      najpierw uzupełnia STFS)
- [ ] Pewność narracji adekwatna do pewności faktu:
      WYSOKA → twardo, ŚREDNIA → "według [źródło]",
      NISKA → "podobno", "krążą doniesienia"

**KRYTERIA PASS — REPETITION DETECTOR:**
- [ ] **Każdy nazwany fakt z STFS użyty maksymalnie
      raz** w narracji (poza świadomymi callback'ami
      oznaczonymi jako "wracając do X")
- [ ] **Brak parafrazowania tego samego faktu** trzy
      razy w jednym akapicie
- [ ] **Brak powtarzanej emocji** ("ten szok", "ta
      tragedia", "to był wstrząs") — każda emocja nazwana
      raz lub świadomie wzmocniona

**KRYTERIA PASS — STYL (anty-wzorce z STYLE_PL_TWOJ_v5_1):**
- [ ] #9 Myślnik wstawkowy: **0** w narracji
- [ ] #10 "To nie jest X. To jest Y.": **0**
- [ ] #11 Trójki anaforyczne ("każdy X, każda Y, każda Z"):
      **0**
- [ ] #12 Imiesłowy aktywne w pozycji orzecznika
      ("jest najszybciej uczącym się"): **0**
- [ ] #13 Kalki idiomów ("kariera nigdy nie ruszyła"):
      **0**
- [ ] Konkretów per akapit: **min. 2** (preferowane 3-5)

**KRYTERIA PASS — REJESTR:**
- [ ] Rejestr każdej sekcji zgodny z mapą z Etapu 2
- [ ] W rejestrze A: kolokwializmy 5-12 sumarycznie
- [ ] W rejestrze B: kolokwializmy 3-5 sumarycznie
- [ ] Komentarz JA narratorski: tylko w outro (rejestr B)
      lub sporadycznie w rejestrze A
- [ ] Wulgaryzmy w narracji własnej: **max 1 per odcinek**

**KRYTERIA PASS — STRUKTURA NARRACYJNA:**
- [ ] Most do następnej sekcji w **każdym** akapicie
      (poza zamykającym)
- [ ] CTA "Wy piszecie o kim nagrać" w cold open lub
      tuż po (zgodnie z 5/8 wzorca Kurtyny)
- [ ] Outro 5-warstwowe:
      1. Konkluzja merytoryczna (1-3 zdania)
      2. Komentarz JA opcjonalny
      3. CTA pytająca
      4. "Trzymajcie się. Na razie."
      5. Krótkie pożegnanie (Yeah/Elo/Ho/Hello)

**NAJCZĘSTSZE PUŁAPKI:**
- ❌ "Pisał z głowy" — fakt brzmi sensownie, ale nie ma
  go w STFS. ZAWSZE FAIL.
- ❌ Drugi raz wspomniana ta sama scena, parafrazowana —
  Repetition Detector to wyłapuje
- ❌ Akapit 240 słów, ale tylko 1 konkret — gęstość za
  mała
- ❌ Most do następnej sekcji "I tak doszedł do kolejnego
  rozdziału" — klisza, nie buduje napięcia
- ❌ Outro 3-warstwowe (zapomniane jedno)
- ❌ Pewność WYSOKA narracji dla faktu o pewności NISKIEJ
  (zła kalibracja)

**JEŚLI FAIL:**
- "Iteruj akapit 3.4: drugi raz pojawia się fakt o
  rozwodzie z 1995"
- "Iteruj akapit 7.2: brak źródła w STFS dla wzmianki
  o Tommy Mottoli — uzupełnij STFS lub usuń"
- "Iteruj rozdział 5: za dużo myślników wstawkowych,
  trzy zdania kończą się '— X'"
- "Iteruj outro: brakuje konkluzji merytorycznej, jest
  od razu CTA"

═══════════════════════════════════════════════════════════
ETAP 6 — AUDYT MERYTORYCZNY (FACT-CHECK + 13-PKT CHECKLISTA)
═══════════════════════════════════════════════════════════

## Co musi się zdarzyć

Claude wykonuje:

1. **Fact-check skryptu vs STFS** — akapit po akapicie
2. **Detector powtórzeń** mechaniczny (każdy fakt z STFS
   liczony ile razy występuje)
3. **Halucynacja-watch** — raport faktów w skrypcie,
   których NIE MA w STFS
4. **Source coverage** — % faktów ze źródłami
5. **13-pkt checklista skill files** (krótki przegląd)
6. **Sensitive topics check** — czy zachowane reguły
   z PROJECT_INSTRUCTIONS:
   - Samobójstwa (data + miejsce, BEZ metody)
   - Uzależnienia (BEZ moralizowania)
   - Niezweryfikowane zarzuty ("podobno")
   - Dzieci bohaterów (imiona raz, bez spekulacji)

## Quality Gate Etap 6

**KRYTERIA PASS — FACT-CHECK:**
- [ ] **0 faktów w skrypcie spoza STFS**
- [ ] **0 błędnych dat** (każda data zweryfikowana
      vs STFS)
- [ ] **0 błędnych nazw** (każda nazwa zespołu, klubu,
      programu zweryfikowana)
- [ ] **0 błędnych kwot** (kwoty z STFS, nie zaokrąglone
      bez powodu)

**KRYTERIA PASS — REPETITION DETECTOR:**
- [ ] Każdy fakt z STFS występuje w skrypcie **maks. 1 raz**
      (lub świadomie z atrybucją "wracając do")
- [ ] **0 parafrazowanych powtórzeń** w obrębie 3
      sąsiednich akapitów

**KRYTERIA PASS — HALUCYNACJA-WATCH:**
- [ ] Lista faktów w skrypcie spoza STFS: **PUSTA**
- [ ] Jeśli niepusta → operator decyduje:
      a) Uzupełnić STFS (zweryfikować źródło)
      b) Usunąć fakt ze skryptu

**KRYTERIA PASS — SENSITIVE TOPICS:**
- [ ] Samobójstwa: brak metody, brak spekulacji o motywie
- [ ] Uzależnienia: konkretne substancje (jeśli
      potwierdzone), bez moralizowania
- [ ] Niezweryfikowane zarzuty: "podobno", "krążą
      doniesienia"
- [ ] Polityka: brak partyjnej polityki polskiej
- [ ] Dzieci: imiona raz, bez zdjęć, bez spekulacji

**KRYTERIA PASS — 13-PKT CHECKLISTA:**
- [ ] Hook strategy zidentyfikowana
- [ ] Wszystkie 13 sekcji mają tezę
- [ ] Sygnały dramy pokryte (min. 5 z 13)
- [ ] Curve dramatic mapped
- [ ] Outro 5-warstwowe
- [ ] Word count w zakresie
- [ ] Rejestr utrzymany
- [ ] Anty-wzorce 0
- [ ] Konkretów wystarczająco
- [ ] CTA wbudowane
- [ ] Most między sekcjami
- [ ] Style consistency
- [ ] Variety-rotation slots niezduplikowane

## Format raportu fact-check

```
FACT-CHECK REPORT — [Bohater]

SKAN AKAPITÓW:
  Akapit 0 (Cold open): 4 fakty, wszystkie z STFS ✓
  Akapit 1.1: 6 faktów, wszystkie z STFS ✓
  Akapit 2.4: 5 faktów, [F019] BRAKUJE w STFS ✗
  Akapit 3.2: 7 faktów, [F023] data niezgodna z STFS ✗
  [...]

REPETITION DETECTOR:
  [F012] "Avril 16 lat" — wystąpił w 1.2 i 3.4 ✗
  [F045] "Kontrakt z Arista" — wystąpił w 2.1 ✓ (1 raz)
  [...]

HALUCYNACJA-WATCH:
  Akapit 5.3: "Avril nagrała pierwszy demo w Toronto"
              — BRAK w STFS, do weryfikacji
  Akapit 7.1: "ślub w Las Vegas" — BRAK w STFS

SENSITIVE TOPICS:
  Wzmianka o uzależnieniu w 4.5: ✓ konkret, bez moralizowania
  Wzmianka o samobójstwie w 11.2: ✓ data + miejsce, brak metody

REKOMENDACJA: FAIL — wymaga iteracji akapitów 2.4, 3.2,
              5.3, 7.1
```

**JEŚLI FAIL:**
- "Iteruj akapit 2.4: usunąć [F019] lub dodać do STFS
  z weryfikacją"
- "Iteruj akapit 3.4: powtórzenie z 1.2 — zostaw tylko
  w 1.2"
- "Wróć do Etapu 2: STFS niekompletny — brak 4 faktów
  użytych w skrypcie"

═══════════════════════════════════════════════════════════
ETAP 7 — OPIS YT + TAGI
═══════════════════════════════════════════════════════════

## Co musi się zdarzyć

Claude produkuje:
1. **Opis A (krótki, 500 znaków)** — pod film
2. **Opis B (długi, 1000-1500 znaków)** — pod film
3. **15-25 tagów** — SEO-optymalne
4. **Timestamp suggestions** — jeśli odcinek > 15 minut

## Quality Gate Etap 7

**KRYTERIA PASS:**
- [ ] Opis A: 400-600 znaków
- [ ] Opis B: 1000-1800 znaków
- [ ] Hook w pierwszych 3 zdaniach opisu
- [ ] CTA do subskrypcji w opisie
- [ ] Tagi: 15-25 sztuk
- [ ] Tagi obejmują: imię bohatera, gatunek, słowa
      kluczowe specyficzne dla wątku
- [ ] Timestamp suggestions w opisie B (jeśli >15 min)
- [ ] **Brak fact-check problems** (opisy nie powinny
      zawierać faktów spoza STFS)

**JEŚLI FAIL:**
- "Iteruj opis B: za krótki, daj 1200+ znaków"
- "Tagi za ogólne — dodaj konkretne nazwy zespołów,
  miast, programów"

═══════════════════════════════════════════════════════════
ETAP 8 — CZTERY PLIKI .DOCX
═══════════════════════════════════════════════════════════

## Co musi się zdarzyć

Claude generuje:
1. `lektor_{nazwisko}.docx` — czysty tekst skryptu
2. `montaz_{nazwisko}.docx` — z rozdziałami, źródłami,
   fact-check summary
3. `prompter_{nazwisko}.docx` — Arial 14pt, dla osoby
   przed kamerą
4. `przypisy_{nazwisko}.docx` — kompletne źródła z
   linkami YT i timestampami (z STFS)

## Quality Gate Etap 8

**KRYTERIA PASS:**
- [ ] 4 pliki wygenerowane
- [ ] `lektor_{...}.docx`: tylko tekst, bez metadanych
- [ ] `montaz_{...}.docx`: rozdziały z numeracją,
      przypisane źródła, fact-check summary z Etapu 6
- [ ] `prompter_{...}.docx`: Arial 14pt, podwójne
      odstępy, bez akcentów blokujących odczyt
- [ ] `przypisy_{...}.docx`: każdy fakt z STFS z
      linkiem (URL) i timestampem (jeśli wideo)
- [ ] **Source coverage przypisów: 100%** — każdy fakt
      z STFS ma wpis w pliku przypisów

**JEŚLI FAIL:**
- "Plik prompter źle sformatowany — daj Arial 14pt"
- "Plik przypisów niepełny — brakują źródła dla F015,
  F022, F031"

═══════════════════════════════════════════════════════════
ETAP 9 — AUDYT FINALNY (13 PASÓW SKILL FILES)
═══════════════════════════════════════════════════════════

## Co musi się zdarzyć

Claude przelatuje skrypt przez 13 pasów audytu:

1. **variety-rotation-skill** — czy 9 slotów niezduplikowane
2. **title-formulas-skill** — czy 5 tytułów w różnych
   formułach
3. **celebrity-documentary-skill** — czy warstwy
   kontrowersji obecne
4. **authenticity-audit-skill** — czy "podobno" przy
   niepewnym
5. **retention-mechanics-skill** — czy buildup/pivot
   adekwatne
6. **retention-coaching-skill** — czy konkrety co 30s
7. **heros-journey-skill** — czy 12-stage curve
8. **script-structures-skill** — czy struktura
   3-aktowa
9. **NICHE-SPECIFIC-HOOKS** — czy hook zgodny z
   formułami
10. **REAL-FACELESS-HOOK-SWIPE** — czy hook jak swipe
11. **outro-psychology-skill** — czy outro 5-warstwowe
12. **visual-scripting-skill** — czy są beats wizualne
13. **faceless-scripts-os-master** — czy WordCount
    poprawny

## Quality Gate Etap 9

**KRYTERIA PASS:**
- [ ] Wszystkie 13 pasów PASS lub PASS Z UWAGAMI
- [ ] Każdy pas ma 1-zdaniową konkluzję
- [ ] Pasy z FAIL — konkretne miejsca do iteracji
- [ ] Reflection: 3-5 zdań co działało, co poprawić
      następnym razem
- [ ] **LOGBOOK update** — wpis dodany do [LOGBOOK.md](http://LOGBOOK.md)
      (operator/Claude wspólnie)

**JEŚLI FAIL któregoś pasa:**
- "Iteruj Pas 7 (heros-journey): brakuje stage 'Refusal'"
- "Iteruj Pas 11 (outro-psychology): warstwa 4 niejasna"

═══════════════════════════════════════════════════════════
ZASADY OGÓLNE PIPELINE
═══════════════════════════════════════════════════════════

## Hierarchia decyzji

1. **STYLE_PL_TWOJ_v5_[1.md](http://1.md)** — nadrzędny w sprawach stylu
2. **PROJECT_INSTRUCTIONS_v5_1.txt** — nadrzędne w sprawach
   procesu i wrażliwości
3. **WORKFLOW_KURTYNA_v4_[1.md](http://1.md)** — nadrzędny w sprawach
   etapów
4. **QUALITY_[GATES.md](http://GATES.md)** (ten plik) — nadrzędny w sprawach
   oceny etapów
5. Skille audytowe — wzmacniają, ale nie zastępują
   powyższych

## Kiedy iterować, kiedy zaczynać od zera

**Iteracja akapitu/sekcji:** gdy jeden konkretny element
nie pasuje, ale reszta jest OK.

**Iteracja całego etapu:** gdy więcej niż 30% etapu
wymaga zmian.

**Powrót do poprzedniego etapu:** gdy odkryjesz problem,
który źródłowo leży w wcześniejszym etapie.
- Np. Etap 6 wykrył halucynację → wracasz do Etapu 2
  i uzupełniasz STFS.

**Nowy czat:** gdy:
- Kontekst się przepełnił (bardzo długie iteracje)
- Chcesz zmienić koncepcję radykalnie
- Reszta odcinka jest do wyrzucenia

## Co Claude robi automatycznie

Po **każdym** etapie:
- Self-check vs Quality Gate kryteria
- Prezentuje Diagnostic Card
- Pyta: "Akceptujesz, czy iterujemy?"

Bez tego — **etap jest nieukończony**.

## Co operator robi zawsze

Po każdym etapie:
- Czyta Diagnostic Card
- Patrzy z dystansu (nie tylko w to co Claude pokazał)
- Decyduje: dalej / iterujemy / powrót / nowy czat
- Po każdym odcinku: **wpis do [LOGBOOK.md](http://LOGBOOK.md)**

═══════════════════════════════════════════════════════════
KONIEC PLIKU
═══════════════════════════════════════════════════════════
