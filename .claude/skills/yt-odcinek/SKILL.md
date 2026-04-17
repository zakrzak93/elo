---
name: yt-odcinek
description: Pisze scenariusz YouTube po polsku ze źródła (wklejony tekst, link YouTube, URL artykułu, plik). Dwa kroki -- wybór pomysłu z 3 propozycji TNT, potem gotowy i wygładzony skrypt pod lektora 2900-3200 słów zgodny z regułami stylu PL. Używaj gdy user prosi o scenariusz, odcinek, voiceover PL, skrypt YouTube, TNT.
---

# yt-odcinek

Generuje pełny scenariusz dokumentalnego odcinka YouTube po polsku w dwóch krokach.

## Wejście

Źródłem może być:
- **Wklejony tekst** w wiadomości usera (najczęstsze)
- **Link YouTube** -- pobierz transkrypt przez MCP `mcp__6a3897bd-dfa9-42a9-9853-cb1f01fcba30__get_youtube_transcript`
- **URL artykułu / strony** -- użyj `WebFetch`
- **Ścieżka do pliku** w repo -- użyj `Read`

Jeśli user nie podał źródła jawnie, zapytaj czego chce użyć zanim ruszysz dalej.

## Krok 1 -- Pomysły (TNT)

1. Pobierz treść źródła zależnie od formatu (patrz wyżej).
2. Utwórz folder `odcinki/<slug>/` gdzie `<slug>` to tymczasowa nazwa (np. z pierwszych słów źródła w kebab-case, bez polskich znaków). Zapisz surowiec do `odcinki/<slug>/zrodlo.md` z frontmatterem (źródło, data, typ).
3. Przeczytaj `reference/framework-title.md` oraz `reference/framework-intro.md`.
4. Wygeneruj **3 wyraźnie różne propozycje** odcinka. Każda ma inną emocję dominującą (ciekawość / pożądanie / strach). Dla każdej:
   - **Tytuł** -- max 55 znaków, front-loaded, 1-2 emocje
   - **Thumbnail** -- kategoria (collage / showcase / reaction / split / single action) + focal point + tekst na miniaturce (2-3 słowa)
   - **Bohater** -- kto jest w kadrze / o kim opowieść
   - **Koncept** -- w jednym zdaniu, o czym odcinek
   - **Stakes** -- co jest na szali dla widza
   - **Hook 30s** -- gotowy tekst lektorski na pierwsze 30 sekund (już w stylu PL, z łącznikami, bez zakazanych słów)
5. Zapisz wszystkie 3 propozycje do `odcinki/<slug>/pomysl.md` używając szablonu `templates/pomysl.md`.
6. Użyj `AskUserQuestion` z 3 opcjami (po jednej na każdą propozycję). User wybiera jedną albo dopisuje własny kierunek w "Other".
7. Po wyborze -- nadpisz `pomysl.md` zostawiając tylko wybraną propozycję (jako finalny TNT odcinka). Zaktualizuj `<slug>` jeśli trzeba żeby pasował do wybranego tytułu.

## Krok 2 -- Gotowy skrypt

1. Przeczytaj **w całości** `reference/styl-pl.md` oraz `reference/framework-skrypt.md`. To są twarde reguły, nie inspiracje.
2. Napisz pełny skrypt pod lektora:
   - **Długość: 2900-3200 słów**. Jeśli input był krótszy, rozwiń wątki kontekstem z research (ale nie zmyślaj faktów). Jeśli dłuższy -- trzymaj górną granicę, wytnij poboczne wątki.
   - Ciągła proza. Bez nagłówków, bez list, bez myślników-dywizów na efekt dramatyczny.
   - Struktura wewnętrzna (niewidoczna w tekście, ale obecna w treści):
     - Hook 30 sekund -- matchuje tytuł i thumbnail
     - 5-7 bloków treści -- każdy z mini-payoffem (mały win / problem / odkrycie / test / rozwiązanie / duży payoff)
     - Zamknięcie w 1-2 zdaniach, bez CTA w ciele tekstu (CTA zostawia się na outro poza skryptem)
3. Zanim zapiszesz -- **autopolish**. Sprawdź tekst punkt po punkcie:
   - Liczba słów w zakresie 2900-3200 (użyj `wc -w` na sformatowanym pliku, ale odliczaj słowa poza frontmatterem)
   - **Zero zakazanych słów**: singiel, chaos, zaledwie, wizerunek, nieustannie, z pozoru, kulminacja, diametralnie, rzemiosło, dokonania, frontmanka, brutalny, fasada, cyniczny, mroczny, desperacja, fenomen, hymn pokolenia, globalna gwiazda, chłopiec/chłopak (o dorosłych muzykach), ikona, ikona dekady, złota klatka
   - **Zero zakazanych łączników**: ponadto, co więcej, w konsekwencji, jednakże, w istocie, zasadniczo, de facto, aczkolwiek, niemniej jednak, natomiast, podsumowując, w zasadzie, właściwie, raczej, dość, w pewnym sensie, niejako, co ciekawe, co ważne, warto zauważyć, mówił wprost, podkreślał wyraźnie
   - Zdanie kontrastowe zaczyna się od łącznika (ale, jednak, tyle że, no ale, za to)
   - Między sąsiadującymi zdaniami w akapicie jest widoczny łącznik logiczny -- jeśli nie, dodaj go
   - Akapity ≤ 6 zdań -- dłuższe podziel
   - Sąsiednie akapity nie zaczynają się od tego samego słowa
   - Pierwsze 2 zdania: konkretny fakt, nie meta-komentarz ani teza ogólna
   - Żaden akapit nie kończy się refleksją / podsumowaniem / metakomentarzem
   - Brak cold-openu w 2. osobie, kaskady zmysłów, pytań retorycznych na końcu 1. akapitu
   - Brak klisz ("musimy cofnąć się w czasie", "historia zatacza koło", "studio tonie w ciszy")
   - Brak myślników i dwukropków w funkcji stylistycznej -- zamień na słowa lub przepisz
   - Każdy fakt z cytatu/wywiadu wprowadzony źródłem ("mówił w wywiadach", "według"), inaczej usuń
4. Zapisz `odcinki/<slug>/final.md` używając szablonu `templates/final.md` (frontmatter z TNT na górze + proza poniżej).
5. Zgłoś userowi: ścieżkę pliku, licznik słów, potwierdzenie że checklist przeszedł.

## Zasady nadrzędne

- **Nie skracaj na siłę** reference'ów w głowie -- jeśli trzeba ich użyć, czytaj plik.
- **Nie proponuj** dłuższych niż 1 zdanie komentarzy do usera między krokami. User wybiera, ty piszesz.
- **Nie commituj** automatycznie. Po napisaniu `final.md` zostaw decyzję o commitcie userowi.
- **Nie twórz** dodatkowych plików poza tymi wymienionymi w planie (`zrodlo.md`, `pomysl.md`, `final.md`).
- Jeśli źródło jest puste, nieczytelne lub zbyt krótkie (< 150 słów) -- zgłoś to userowi przed krokiem 1 i zapytaj co dalej.
