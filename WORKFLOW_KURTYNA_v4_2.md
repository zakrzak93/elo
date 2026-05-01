# WORKFLOW KURTYNA v4.5
# 9 etapów produkcji odcinka biograficznego YouTube
# Wersja 4.5 — maj 2026
# Aktualizacja vs v4.3: dodany Etap 5.5 (Audyt Gemini), aktualizacja Etapu 1/2 (wywiady z timestampami) i Etapu 6 (fizyczna aplikacja poprawek)

═══════════════════════════════════════════════════════════
HIERARCHIA KONTROLI JAKOŚCI
═══════════════════════════════════════════════════════════

5 warstw kontroli, od najszybszej do najgłębszej:

1. **Reguła M** (test świadomości na poziomie zdania) — co zdanie, ~10 sekund
2. **Reguła N** (mikro-skan akapitowy) — co akapit, ~60 sekund
3. **Reguła L** (PRE-PRESENTATION SCAN) — przed prezentacją, ~5 minut
4. **Etap 5.5** (Audyt Gemini w AI Studio) — między Etapem 5 a 6, ~30-40 minut
5. **Etap 6** (fact-check vs STFS) — własny research, ~30 minut

Każda warstwa łapie inne błędy. Pominięcie warstwy = błąd przejdzie do produkcji.

═══════════════════════════════════════════════════════════
ETAP 1 — BOHATER + 3 KĄTY A/B/C + RESEARCH WSTĘPNY
═══════════════════════════════════════════════════════════

## Co musi się zdarzyć

1. Briefing bohatera (3-5 zdań kontekstu)
2. Ocena rejestru (A pikantny / B powściągliwy / AB)
3. Sprawdzenie czy bohater już był w archiwum kanału
   (Subscribr `my_videos` + UserMemories + [LOGBOOK.md](http://LOGBOOK.md))
4. **Research zewnętrzny ⭐ OBOWIĄZKOWY**:
   - Bright Data (domyślny scraper)
   - Exa: web_search_exa + web_fetch_exa
   - Tavily (fallback)
   - TranscriptAPI (wywiady wideo Z TIMESTAMPAMI)
   - web_search Anthropic (ostatnia deska)
5. **⭐ NOWE w v4.5: Wywiady z bohaterem + konkurencja YT**
   - TranscriptAPI z TIMESTAMPAMI obowiązkowo
   - Marcin używa cytatów z timestampami jako uzupełnień
     montażowych w odcinku
   - Bez timestampów cytaty są bezużyteczne dla montażysty
6. Min. 3 propozycje kątów A/B/C z uzasadnieniem (P1 dramatu,
   P2 charakterystyczny moment, P3 alternatywny)

## Quality Gate

- [ ] Briefing bohatera w 3-5 zdaniach
- [ ] Rejestr oznaczony A/B/AB
- [ ] Cross-episode check (czy nie powtarzamy)
- [ ] Min. 5 źródeł zewnętrznych (artykuły, wywiady, dokumenty)
- [ ] Min. 2 transkrypty wywiadów Z TIMESTAMPAMI
- [ ] 3 kąty z uzasadnieniem

═══════════════════════════════════════════════════════════
ETAP 2 — STFS + OUTLINE + FACT ALLOCATION MAP
═══════════════════════════════════════════════════════════

1. Source-Tagged Fact Sheet (STFS) — 30-60 faktów z URL,
   pewnością WYSOKA/ŚREDNIA/NISKA, konfliktami źródeł
2. Outline 13-akapitowy (cold open + 12 środkowych + zamknięcie)
3. Fact Allocation Map — przypisanie faktów do akapitów
4. Repetition Watchlist — 3+ pułapki powtórzeń per bohater
5. Mapa rejestrów per-sekcja (A/B/AB z uzasadnieniem)

## Quality Gate

- [ ] STFS min. 30 faktów, każdy ze źródłem
- [ ] Każdy fakt ma pewność WYS/ŚR/NIS
- [ ] Konflikty źródeł oznaczone
- [ ] Outline ma 13 akapitów (cold open + 12 + zamknięcie)
- [ ] Word counts: cold open 50-70, akapity 200-290 (śr. 240),
      zamknięcie 225±25, suma ~3200
- [ ] Każdy akapit ma min. 2 konkretne kotwice faktyczne
- [ ] Fact Allocation Map bez duplikatów

═══════════════════════════════════════════════════════════
ETAP 3 — COLD OPEN (3-5 PROPOZYCJI HOOKÓW)
═══════════════════════════════════════════════════════════

3-5 wariantów cold open, każdy:
- 27-70 słów
- Curiosity gap + konkrety + pivot
- Inna strategia (A/B/C/D/E z STYLE_PL_TWOJ Część IV §14)
- Rejestr zgodny z mapą z Etapu 2

## Quality Gate

- [ ] 3-5 wariantów (preferowane 4)
- [ ] Każdy 27-70 słów
- [ ] Każdy w innej strategii hooka
- [ ] Curiosity gap + min. 2 konkrety w każdym
- [ ] Brak myślników wstawkowych, "to-to", trójek anaforycznych

═══════════════════════════════════════════════════════════
ETAP 3.5 — RAPORT OBJĘTOŚCI (3 OPCJE SKALI)
═══════════════════════════════════════════════════════════

Po researchu i outline'u, PRZED pisaniem skryptu Claude
generuje 3 opcje skali:
- A: 5000-5500 słów (rozszerzona)
- B: 3600-3800 słów (standard)
- C: 2800-3000 słów (skondensowana)

Każda opcja: konkretna lista co dodane/usunięte vs B,
ryzyko, rekomendacja.

Operator wybiera ZANIM Claude pisze.
Marcin preferuje "więcej niż mniej" → rekomendacja A/B.

═══════════════════════════════════════════════════════════
ETAP 4 — TYTUŁY YT + 3 KONCEPTY MINIATURY
═══════════════════════════════════════════════════════════

1. 5 tytułów YouTube wg formuł z title-formulas-skill
2. 3 koncepty miniatury wg metody 1of10
3. Najsilniejsze parowanie tytuł↔miniatura
4. Setup testu (Test & Compare)

═══════════════════════════════════════════════════════════
ETAP 5 — PISANIE SKRYPTU
═══════════════════════════════════════════════════════════

## Krok 1 — Pełny skrypt PL, 3200 słów

(zakres 3100-3300):
- Cold open: 50-70 słów (zaakceptowany w Etapie 3)
- 3 rozdziały × 4 akapity = 12 akapitów (200-290 słów każdy)
- Akapit zamykający: 225 ± 25 słów

## Krok 2 — STYLE_PL_TWOJ_v5_[3.md](http://3.md) w pełni stosowany

Główny kompas: Próbki A-K w Części VI.

## Krok 3 — Reguły dyskografii w skrypcie

- Wpleciona jako markery czasu, nie katalog
- Każdy album/singiel = nazwa + rok + jedna konkretna informacja
- Tytuły piosenek i albumów w cudzysłowie

## Krok 4 — Reguły cytatów

- W SKRYPCIE: luźne parafrazy z atrybucją w narracji
  ("mówił wprost", "tłumaczył tak", "w oświadczeniu napisała")
- ZAKAZ słowa "Cytat:" jako wprowadzenia
- W PRZYPISACH: dokładne linki YT z timestampami + cytat
  oryginalny + parafraza

## Krok 5 — Reguła konkretów

Każdy z 12 akapitów środkowych zawiera min. 2 konkretne
fakty z researchu. Konkret = data, kwota, nazwisko, miejsce,
nazwa utworu, pozycja na liście, cytat, statystyka.

## Krok 6 — Sekcje rozdzielone wycentrowanymi `* * *`

## Krok 7 — Brak production cues

Brak [VISUAL:], [CLIP:], [B-ROLL:] w pliku lektora.

## Krok 8 — REGUŁY M+N (KOMPOZYCYJNE — w trakcie pisania) ⭐ NOWE w v4.5

═══ REGUŁY M (test świadomości na poziomie zdania) ═══

Po napisaniu KAŻDEGO zdania, ZANIM postawię kropkę:

**M1 — Pierwowzór angielski 1:1:**
Czy zdanie ma oczywiste angielskie odbicie słowo-w-słowo?
- "adamantnie zaprzecza" → "adamantly denies" → KALKA
- "trafia na celownik" → polski idiom OK

**M2 — Test głośnej wymowy:**
Czytam zdanie głośno (symuluję polskiego mówcę). Brzmi jak
polski oryginał czy jak tłumaczenie?

**M3 — Idiom dosłowny:**
Każdy idiom angielski tłumaczony 1:1 = kalka.
- "blew up in his face" ≠ "wybuchło mu w twarz" → "eksplodowało publicznie"
- "threw in the towel" ≠ "rzucił ręcznik" → "skapitulował"

**M4 — Logika gramatyczna podmiotu:**
Czy podmiot zdania może logicznie wykonać orzeczenie?
- "Debiut trafia na szczyt" = ŹLE → "Singiel debiutancki trafia"
- "Utwór wygrywa kraje" = ŹLE → "Singiel zdobywa szczyty list w krajach"

═══ CZARNA LISTA KALK (zero tolerancji w pisaniu) ═══

| Kalka | Polskie ekwiwalent |
|---|---|
| adamantnie | stanowczo |
| targetowała | jej celem była |
| tipping point | punkt krytyczny / czara goryczy |
| ojcowska figura | ojcowski autorytet |
| wpada na radar | trafia na celownik |
| white power rock | neonazistowski rock |
| booklet | książeczka |
| salut nazistowski | hitlerowskie pozdrowienie |
| recydywa skandalu | powrót skandalu |
| wygodnie zaprzeczył | gładko wyparł się |
| faktyczny błąd | błąd rzeczowy |
| świeża twarz | nowa twarz / debiutantka |
| wewnętrzny żart | żart dla wtajemniczonych |
| wygrywa kraje/listy | zdobywa szczyty / podbija |
| śpiewak (w pop/dance) | wokalista |
| piwniczne studio | studio w piwnicy |
| dance jako przydawka | grupa eurodance / muzyki dance |
| to nie była opcja | nie wchodziło w grę |
| starym rdzeniem | dawnym trzonem |
| zostawia pytanie wiszące | pozostaje bez odpowiedzi |
| to wszystko o muzyce | chodziło tylko o muzykę |

═══ REGUŁY N (mikro-skan po każdym akapicie) ═══

Po napisaniu KAŻDEGO akapitu, ZANIM zacznę następny:

**N1 — Słowo "Cytat:":**
grep "Cytat:" w akapicie. Wynik MUSI = 0.

**N2 — Daty bez "roku":**
grep "[0-9]{4} roku" w akapicie. Max 1× per akapit
(idiom "w tym samym roku" OK).
Domyślnie data sucha: "1993" zamiast "1993 roku".

**N3 — Najczęstsze rzeczowniki (5 KLAS):**
- Rzeczowniki pospolite (kaseta/dokument/partia)
- Imiona własne (Sannie 3× = problem)
- Lokalizacje (Mediolan + mediolański = jedna jednostka)
- Tytuły utworów ("The Sign" 3× = problem)
- Każda klasa max 2 wystąpienia.

Synonimy gotowe:
- kaseta / taśma / nagranie / demo
- dokument / film / produkcja / materiał / miniserial
- partia / ugrupowanie / frakcja
- zespół / skład / kapela / formacja
- piosenka / utwór / numer / kompozycja
- wytwórnia / label / wydawnictwo
- album / krążek / płyta

**N4 — Powtórzenia czasowników w sąsiednich zdaniach:**
0 powtórzeń tego samego czasownika głównego w 2
sąsiadujących zdaniach.

**N5 — Jeden czas per akapit (decyzja PRZED pisaniem):**
- TERAŹNIEJSZY HISTORYCZNY (akcja na żywo)
- PRZESZŁY (retrospekcja, kronika)
ZAKAZ mieszania w jednym akapicie.

**N6 — Echolalia partykuł:**
- "właśnie" / "już" / "też" max 1× per zdanie złożone
- Zapchajdziury ZAKAZANE: "jakoś", "w sumie", "dosłownie"
  (przenośnie), "niejako"

═══ REGUŁA WYKONANIA M+N ═══

Reguła M = NA ŻYWO podczas pisania zdania, nie odraczam.
Reguła N = PO KAŻDYM AKAPICIE, następny akapit zaczynam
DOPIERO po naprawie poprzedniego.
NIE kumuluję długu redakcyjnego.

## Krok 9 — PRE-PRESENTATION SCAN (Reguła L)

Po napisaniu pełnego skryptu, PRZED prezentacją operatorowi
wykonuję 12 testów grep-skanu deterministycznych:

1. Anglicyzmy 60+ z listy
2. Powtórzenia pierwszego słowa zdań sąsiadujących
3. Składnia "o + miejscownik" przy korzeniach
4. Numeracja osób w domu
5. Rotacja źródeł plotkarskich
6. Liczby cyframi (Reguła F)
7. Zbędne metafory
8. Słowo "Cytat:" — 0 wystąpień
9. Epidemia "roku" — max 10 w skrypcie 3200 słów
10. Najczęstsze rzeczowniki per akapit ≤2
11. Powtórzenia czasowników w sąsiednich zdaniach
12. Czas per akapit spójny

Każde naruszenie = iteracja przed prezentacją, NIE
czekamy na uwagi operatora.

## Quality Gate Etap 5

- [ ] Word count 3100-3300
- [ ] Każdy akapit 200-290
- [ ] Cold open 50-70 słów
- [ ] "Wy piszecie o kim nagrać" w A1
- [ ] PRE-PRESENTATION SCAN wykonany, 0 trafień
- [ ] 0 słów "Cytat:"
- [ ] Max 10 wystąpień "X roku" w całym skrypcie
- [ ] Końcówka rotowana (Yeah/Elo/Ho/Hello/Dobrego tygodnia)

═══════════════════════════════════════════════════════════
ETAP 5.5 ⭐ NOWY — AUDYT GEMINI W AI STUDIO
═══════════════════════════════════════════════════════════

## Co musi się zdarzyć

Po napisaniu skryptu (Etap 5), PRZED fact-checkiem (Etap 6),
operator audytuje każdy akapit przez Gemini w [aistudio.google.com](http://aistudio.google.com).

## Komunikat Claude do operatora

Po prezentacji skryptu v1 Claude WPROST mówi:

> 🔔 "Skrypt v1 gotowy. Idź teraz do AI Studio
> ([aistudio.google.com](http://aistudio.google.com)) z poleceniem audytora 8 kategorii
> (w project knowledge: POLECENIE_AUDYTORA_[GEMINI.md](http://GEMINI.md)).
> Wklejaj akapit po akapicie (13 razy) lub batch po 4-5
> jeśli kontekst pozwoli. Wracaj z raportami — czekam."

Bez tego komunikatu Etap 5.5 zostanie pominięty.

## Polecenie audytora (8 kategorii)

Plik POLECENIE_AUDYTORA_[GEMINI.md](http://GEMINI.md) w project knowledge.
Audytor sprawdza:
1. **Halucynacje faktów** (NAJWAŻNIEJSZA — niezgodności
   z rzeczywistością, fani wyłapią w 30 sekund)
2. Kalki anglosaskie (idiomatyczne + słownikowe + strukturalne)
3. Błędy leksykalne (śpiewak, dance, archaizmy)
4. Powtórzenia rzeczowników (≥3 = problem)
5. Powtórzenia czasowników w sąsiadach
6. Mieszanie czasów
7. Sztuczny dramatyzm / AI-storytelling
8. Mechanika (pleonazmy, echolalia, "Cytat:", "roku")

## Quality Gate Etap 5.5

- [ ] 13 raportów (po jednym na akapit)
- [ ] Operator wraca z raportami
- [ ] Claude filtruje problemy:
  - Akceptuje: realne kalki, halucynacje, powtórzenia 4+,
    błędy logiczne podmiotu
  - Odrzuca: over-engineering audytora (np. "plus" jako kalka)
- [ ] Claude FIZYCZNIE APLIKUJE poprawki do tekstu
- [ ] Claude powtarza PRE-PRESENTATION SCAN na finalnej wersji
- [ ] Claude prezentuje skrypt v2 jako pełny blok

═══════════════════════════════════════════════════════════
ETAP 6 — FACT-CHECK vs STFS (z FIZYCZNĄ APLIKACJĄ POPRAWEK)
═══════════════════════════════════════════════════════════

## Co musi się zdarzyć

1. Skanuję skrypt v2 (po Etapie 5.5) wzdłuż STFS
2. Generuję raport halucynacji (PRZED → PO)
3. **⭐ KRYTYCZNE: Aplikuję wszystkie poprawki fizycznie**
   do skryptu, nie tylko prezentuję listę
4. Powtarzam PRE-PRESENTATION SCAN na finalnej wersji
   (poprawki mogły wprowadzić nowe problemy)
5. Prezentuję skrypt v3 jako pełny blok
6. Generuję fact-check summary (8-15 punktów dla pliku
   montażysty)

## Quality Gate Etap 6

- [ ] Każdy twardy fakt zweryfikowany vs STFS
- [ ] Każdy cytat zweryfikowany vs oryginalny transkrypt
- [ ] Każda data, kwota, statystyka zweryfikowana
- [ ] Halucynacje krytyczne (zmieniające fakty) = 0
  po aplikacji poprawek
- [ ] Skrypt v3 prezentowany jako pełny blok (nie lista
  poprawek)
- [ ] Word count 3100-3300 utrzymany

═══════════════════════════════════════════════════════════
ETAP 7 — OPISY + TAGI
═══════════════════════════════════════════════════════════

1. Opis A (~500 znaków) — preview YT
2. Opis B (~1000 znaków) — pełny pod filmem + timestampy
3. Tagi (max 500 znaków)

## Quality Gate

- [ ] Opis A 450-550 znaków
- [ ] Opis B 950-1100 znaków + timestampy + sekcja Źródła
- [ ] Tagi 450-500 znaków
- [ ] Demonetization-safe (brak słów wyzwalających)
- [ ] SEO anchory (daty, nazwiska, tytuły hitów)

═══════════════════════════════════════════════════════════
ETAP 8 — PAKIET DOCX
═══════════════════════════════════════════════════════════

4 pliki:
1. **Lektor** (czysta narracja, bez production cues)
2. **Montaż b-rolle inline** (skrypt + [B-ROLL: ...] po
   każdym akapicie)
3. **Prompter** (wersja czytelna dla lektora,
   większa czcionka)
4. **Przypisy z timestampami** (lista źródeł, cytatów,
   linków YT z TS dla montażysty)

═══════════════════════════════════════════════════════════
ETAP 9 — MEMORY + LOGBOOK
═══════════════════════════════════════════════════════════

1. Aktualizacja memory:
   - Cross-episode flagi (do memory #4)
   - Nowe wzorce stylu (jeśli wystąpiły)
2. Aktualizacja [LOGBOOK.md](http://LOGBOOK.md)
3. Aktualizacja STYLE_PL_TWOJ jeśli pojawił się nowy
   wzorzec wzorcowy lub anty-wzorzec
4. ROTATION LOG do userMemories

═══════════════════════════════════════════════════════════
PODSUMOWANIE — JAK WYGLĄDA PEŁNY ODCINEK
═══════════════════════════════════════════════════════════

| Etap | Czas Claude | Czas operatora | Output |
|---|---|---|---|
| 1 | 60 min | 10 min | Brief + research + wywiady z TS |
| 2 | 45 min | 5 min | STFS + outline |
| 3 | 15 min | 5 min | Cold open + decyzja |
| 3.5 | 10 min | 2 min | Raport objętości + decyzja |
| 4 | 20 min | 5 min | Tytuły + miniatury |
| 5 | 90 min | — | Skrypt v1 |
| **5.5** | — | **30-40 min** | 13 raportów Gemini |
| 6 | 30 min | 5 min | Skrypt v3 (po fact-checku) |
| 7 | 15 min | 5 min | Opisy + tagi |
| 8 | 30 min | 5 min | Pakiet 4× docx |
| 9 | 15 min | 2 min | Memory + LOGBOOK |
| **TOTAL** | **~5h** | **~75 min** | Gotowy odcinek |

═══════════════════════════════════════════════════════════
KONIEC v4.5
═══════════════════════════════════════════════════════════
