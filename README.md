# Mapy pytań — LAMU 2025 i Pytania z Księżyca

Wizualizacje pytań zadawanych w dwóch popularyzatorskich projektach naukowych w postaci interaktywnych map w przestrzeni embeddingów. Każde pytanie to punkt — punkty bliskie sobie odpowiadają pytaniom o podobnym znaczeniu (nie literalnym, lecz semantycznym).

- **LAMU 2025** — Letnia Akademia Młodych Umysłów (Radio Naukowe), pytania dzieci pogrupowane w kategorie tematyczne (Fizyka, Biologia, Wszechświat, Człowiek, Technologie, Ziemia, Matematyka, Historia, Chemia).
- **Pytania z Księżyca** — audycja Radia 357, pytania słuchaczy.

Pod spodem: polski model językowy `sdadas/st-polish-paraphrase-from-distilroberta` zamienia każde pytanie na wektor 768 liczb, UMAP redukuje to do 2D, Plotly rysuje interaktywny wykres.

---

## Interaktywne wykresy

### 1. LAMU 2025 — mapa pytań dzieci

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BERENZ/2026-lamu-ksiezyc/blob/main/2025/lamu_questions_embeddings.ipynb)
&nbsp;&nbsp;
[**▶ Otwórz interaktywny wykres**](https://maciejberesewicz.com/2026-lamu-ksiezyc/2025/lamu_questions_2025.html)

Pytania dzieci pokolorowane według kategorii tematycznej. Najedź myszką na punkt, by zobaczyć treść pytania; kliknij kategorię w legendzie, by ją ukryć lub wyizolować.

### 2. Pytania z Księżyca — mapa pytań słuchaczy Radia 357

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BERENZ/2026-lamu-ksiezyc/blob/main/2025/ksiezyc_questions_embeddings.ipynb)
&nbsp;&nbsp;
[**▶ Otwórz interaktywny wykres**](https://maciejberesewicz.com/2026-lamu-ksiezyc/2025/pytania_z_ksiezyca.html)

~1050 pytań słuchaczy. Wszystkie punkty w jednym kolorze — wykres pokazuje strukturę semantyczną (gdzie skupiają się podobne pytania), bez narzuconych kategorii.

### 3. LAMU 2025 + Pytania z Księżyca — wspólna mapa

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BERENZ/2026-lamu-ksiezyc/blob/main/2025/combined_questions_embeddings.ipynb)
&nbsp;&nbsp;
[**▶ Otwórz interaktywny wykres**](https://maciejberesewicz.com/2026-lamu-ksiezyc/2025/lamu_plus_ksiezyc.html)

Oba zbiory razem podane do UMAP — odległości między punktami są porównywalne między źródłami. Kolor oznacza źródło (czerwony = LAMU, granatowy = Pytania z Księżyca). Widać, gdzie tematy się pokrywają, a gdzie różnią.

---

## Uruchomienie notatników w Google Colab

Wystarczy kliknąć badge **"Open In Colab"** przy wybranym notatniku, opcjonalnie ustawić GPU (**Środowisko uruchomieniowe → Zmień typ środowiska → T4**) i uruchomić wszystkie komórki (`Ctrl+F9`). Notatnik sam pobierze dane, zakoduje pytania i wygeneruje wykresy. Konto Google jest wymagane. Nie trzeba nic instalować lokalnie.

## Źródła danych

- LAMU 2025: PDF z pytaniami publikowany przez [Radio Naukowe](https://radionaukowe.pl/).
- Pytania z Księżyca: [zbiór pytań w formacie tekstowym](https://gist.githubusercontent.com/BERENZ/a2f58c81f5983e8f6b9e5191be4bad8a/raw/0fee1aec9d5ec6769ebe6e20bdeb0600ee0be692/pytania-z-ksiezyca.txt).

## Wykorzystane narzędzia

- [sentence-transformers](https://www.sbert.net/) z modelem [`sdadas/st-polish-paraphrase-from-distilroberta`](https://huggingface.co/sdadas/st-polish-paraphrase-from-distilroberta)
- [UMAP](https://umap-learn.readthedocs.io/) — redukcja wymiarów
- [Plotly](https://plotly.com/python/) — interaktywne wykresy
- [PyMuPDF](https://pymupdf.readthedocs.io/) — parsowanie PDF
