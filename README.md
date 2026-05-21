# LAMU 2026 + Pytania z Księżyca — mapy pytań w przestrzeni embeddingów

Trzy notatniki Jupyter (Google Colab, Python) wizualizujące pytania zadawane w dwóch popularyzatorskich projektach naukowych:

- **LAMU 2026** — Letnia Akademia Młodych Umysłów (projekt Radia Naukowego), pytania dzieci pogrupowane w kategorie tematyczne (Fizyka, Biologia, Wszechświat, Człowiek, Technologie, Ziemia, Matematyka, Historia, Chemia).
- **Pytania z Księżyca** — audycja Radia 357, pytania słuchaczy bez przypisanych kategorii.

Każde pytanie zamieniane jest na wektor 768 liczb (embedding) przez polski model językowy `sdadas/st-polish-paraphrase-from-distilroberta`, a następnie redukowane do 2D za pomocą UMAP. Wynik to interaktywna mapa, na której punkty bliskie sobie odpowiadają pytaniom o podobnym znaczeniu.

---

## Notatniki

### 1. LAMU 2026 — mapa pytań dzieci

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BERENZ/2026-lamu-ksiezyc/blob/main/2025/lamu_questions_embeddings.ipynb)

Pytania dzieci z Letniej Akademii Młodych Umysłów 2026, pokolorowane według kategorii tematycznej. Notatnik zawiera również projekcję nowych pytań na istniejącą mapę UMAP (`reducer.transform`).

![LAMU 2026 - mapa pytań](images/lamu.png)

Plik: [`2025/lamu_questions_embeddings.ipynb`](2025/lamu_questions_embeddings.ipynb)

---

### 2. Pytania z Księżyca — mapa pytań słuchaczy Radia 357

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BERENZ/2026-lamu-ksiezyc/blob/main/2025/ksiezyc_questions_embeddings.ipynb)

~1050 pytań zadanych przez słuchaczy audycji "Pytania z Księżyca" w Radiu 357. Pytania nie mają przypisanych kategorii — wszystkie punkty mają ten sam kolor, wykres pokazuje wyłącznie strukturę semantyczną (gdzie skupiają się podobne pytania).

![Pytania z Księżyca - mapa pytań](images/ksiezyc.png)

Plik: [`2025/ksiezyc_questions_embeddings.ipynb`](2025/ksiezyc_questions_embeddings.ipynb)

---

### 3. LAMU + Księżyc — wspólna mapa

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BERENZ/2026-lamu-ksiezyc/blob/main/2025/combined_questions_embeddings.ipynb)

Oba zbiory pytań razem podane do UMAP — odległości między punktami są porównywalne między źródłami. Kolor oznacza źródło (czerwony = LAMU, granatowy = Pytania z Księżyca). Pokazuje, gdzie tematy się pokrywają, a gdzie różnią.

![LAMU + Księżyc - wspólna mapa](images/combined.png)

Plik: [`2025/combined_questions_embeddings.ipynb`](2025/combined_questions_embeddings.ipynb)

---

## Jak uruchomić w Google Colab

1. Kliknij badge **"Open In Colab"** przy wybranym notatniku powyżej.
2. W menu Colab: **Środowisko uruchomieniowe → Zmień typ środowiska → GPU (T4)** (opcjonalnie — bez GPU też zadziała, tylko wolniej).
3. **Środowisko uruchomieniowe → Uruchom wszystko** (`Ctrl+F9`).
4. Notatnik sam pobierze dane, zainstaluje biblioteki i wygeneruje wykresy.
5. Na koniec automatycznie pobiorą się pliki: interaktywny HTML i statyczny PNG.

Konto Google jest wymagane. Nie trzeba nic instalować lokalnie.

## Źródła danych

- LAMU 2026: [`LAMU-zadane-pytania-2026.pdf`](https://radionaukowe.pl/wp-content/uploads/2026/03/LAMU-zadane-pytania-2026.pdf) (strona Radia Naukowego).
- Pytania z Księżyca: [GitHub gist](https://gist.githubusercontent.com/BERENZ/a2f58c81f5983e8f6b9e5191be4bad8a/raw/0fee1aec9d5ec6769ebe6e20bdeb0600ee0be692/pytania-z-ksiezyca.txt).

## Wykorzystane narzędzia

- [sentence-transformers](https://www.sbert.net/) z modelem [`sdadas/st-polish-paraphrase-from-distilroberta`](https://huggingface.co/sdadas/st-polish-paraphrase-from-distilroberta)
- [UMAP](https://umap-learn.readthedocs.io/) — redukcja wymiarów
- [Plotly](https://plotly.com/python/) — interaktywne wykresy
- [PyMuPDF](https://pymupdf.readthedocs.io/) — parsowanie PDF

## Jak dodać/zaktualizować obrazki w README

Po uruchomieniu każdego notatnika w Colab, oprócz pliku HTML, automatycznie pobiera się też statyczny PNG. Wystarczy zmienić jego nazwę i wrzucić do katalogu `images/` w repo:

| Notatnik | Plik wygenerowany w Colab | Nazwa w `images/` |
|----------|---------------------------|-------------------|
| LAMU | `lamu_questions_static.png` | `lamu.png` |
| Księżyc | `ksiezyc_questions_static.png` | `ksiezyc.png` |
| Wspólny | `combined_questions_static.png` | `combined.png` |
