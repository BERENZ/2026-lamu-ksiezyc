# LAMU 2026 + Pytania z Księżyca — mapy pytań w przestrzeni embeddingów

Trzy notatniki Jupyter (Google Colab, Python) wizualizujące pytania zadawane w dwóch popularyzatorskich projektach naukowych:

- **LAMU 2026** — Letnia Akademia Młodych Umysłów (projekt Radia Naukowego), pytania dzieci pogrupowane w kategorie tematyczne (Fizyka, Biologia, Wszechświat, Człowiek, Technologie, Ziemia, Matematyka, Historia, Chemia).
- **Pytania z Księżyca** — audycja Radia 357, pytania słuchaczy bez przypisanych kategorii.

Każde pytanie zamieniane jest na wektor 768 liczb (embedding) przez polski model językowy `sdadas/st-polish-paraphrase-from-distilroberta`, a następnie redukowane do 2D za pomocą UMAP. Wynik to interaktywna mapa, na której punkty bliskie sobie odpowiadają pytaniom o podobnym znaczeniu.

---

## Notatniki i interaktywne wykresy

### 1. LAMU 2026 — mapa pytań dzieci

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BERENZ/2026-lamu-ksiezyc/blob/main/2025/lamu_questions_embeddings.ipynb)
&nbsp;&nbsp;
[**▶ Otwórz interaktywny wykres**](https://raw.githack.com/BERENZ/2026-lamu-ksiezyc/main/2025/lamu_questions_2026.html)

Pytania dzieci z Letniej Akademii Młodych Umysłów 2026, pokolorowane według kategorii tematycznej. Notatnik zawiera również projekcję nowych pytań na istniejącą mapę UMAP (`reducer.transform`).

Notatnik: [`2025/lamu_questions_embeddings.ipynb`](2025/lamu_questions_embeddings.ipynb)
HTML: [`2025/lamu_questions_2026.html`](2025/lamu_questions_2026.html)

---

### 2. Pytania z Księżyca — mapa pytań słuchaczy Radia 357

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BERENZ/2026-lamu-ksiezyc/blob/main/2025/ksiezyc_questions_embeddings.ipynb)
&nbsp;&nbsp;
[**▶ Otwórz interaktywny wykres**](https://raw.githack.com/BERENZ/2026-lamu-ksiezyc/main/2025/pytania_z_ksiezyca.html)

~1050 pytań zadanych przez słuchaczy audycji "Pytania z Księżyca" w Radiu 357. Pytania nie mają przypisanych kategorii — wszystkie punkty mają ten sam kolor, wykres pokazuje wyłącznie strukturę semantyczną (gdzie skupiają się podobne pytania).

Notatnik: [`2025/ksiezyc_questions_embeddings.ipynb`](2025/ksiezyc_questions_embeddings.ipynb)
HTML: [`2025/pytania_z_ksiezyca.html`](2025/pytania_z_ksiezyca.html)

---

### 3. LAMU + Księżyc — wspólna mapa

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BERENZ/2026-lamu-ksiezyc/blob/main/2025/combined_questions_embeddings.ipynb)
&nbsp;&nbsp;
[**▶ Otwórz interaktywny wykres**](https://raw.githack.com/BERENZ/2026-lamu-ksiezyc/main/2025/lamu_plus_ksiezyc.html)

Oba zbiory pytań razem podane do UMAP — odległości między punktami są porównywalne między źródłami. Kolor oznacza źródło (czerwony = LAMU, granatowy = Pytania z Księżyca). Pokazuje, gdzie tematy się pokrywają, a gdzie różnią.

Notatnik: [`2025/combined_questions_embeddings.ipynb`](2025/combined_questions_embeddings.ipynb)
HTML: [`2025/lamu_plus_ksiezyc.html`](2025/lamu_plus_ksiezyc.html)

---

## Jak uruchomić w Google Colab

1. Kliknij badge **"Open In Colab"** przy wybranym notatniku powyżej.
2. W menu Colab: **Środowisko uruchomieniowe → Zmień typ środowiska → GPU (T4)** (opcjonalnie — bez GPU też zadziała, tylko wolniej).
3. **Środowisko uruchomieniowe → Uruchom wszystko** (`Ctrl+F9`).
4. Notatnik sam pobierze dane, zainstaluje biblioteki i wygeneruje wykresy.
5. Na koniec automatycznie pobierze się plik HTML — wystarczy go wrzucić do katalogu `2025/` w repo, żeby zaktualizować interaktywny wykres widoczny w README.

Konto Google jest wymagane. Nie trzeba nic instalować lokalnie.

## Kod do zapisu interaktywnego HTML

Każdy z notatników kończy się komórką, która eksportuje wykres Plotly do samodzielnego pliku HTML (otwiera się w dowolnej przeglądarce, działa offline, zachowuje pełną interaktywność — hover, zoom, ukrywanie kategorii):

```python
HTML_PATH = "lamu_questions_2026.html"   # albo pytania_z_ksiezyca.html / lamu_plus_ksiezyc.html

fig.write_html(HTML_PATH, include_plotlyjs=True, full_html=True)
print(f"Zapisano interaktywny wykres: {HTML_PATH}")

# Automatyczne pobranie pliku w Colabie:
try:
    from google.colab import files
    files.download(HTML_PATH)
except ImportError:
    print(f"Otworz plik {HTML_PATH} w przegladarce, aby zobaczyc wykres offline.")
```

Argumenty `write_html`:
- `include_plotlyjs=True` — bundluje pełną bibliotekę Plotly do pliku (~3 MB), dzięki czemu wykres działa offline bez internetu.
- `full_html=True` — pełny dokument HTML (z `<html>`, `<head>`, `<body>`), gotowy do otwarcia w przeglądarce. Jeśli chcesz tylko fragment do osadzenia, ustaw `False`.

## Dlaczego linki do interaktywnych wykresów używają `raw.githack.com`?

GitHub serwuje pliki `.html` z `Content-Type: text/plain` (tekst, nie strona) — więc bezpośredni link do pliku w repo pokazuje surowy kod HTML zamiast wykresu. Serwis [raw.githack.com](https://raw.githack.com/) renderuje te same pliki z `Content-Type: text/html`, czyli normalnie jako stronę z działającym Plotly w środku. Schemat URL:

```
https://raw.githack.com/BERENZ/2026-lamu-ksiezyc/main/2025/<plik>.html
```

Alternatywa: włączyć **GitHub Pages** dla tego repo (Settings → Pages → branch `main`, folder `/ (root)`) — wtedy te same pliki będą pod `https://berenz.github.io/2026-lamu-ksiezyc/2025/<plik>.html`.

## Źródła danych

- LAMU 2026: [`LAMU-zadane-pytania-2026.pdf`](https://radionaukowe.pl/wp-content/uploads/2026/03/LAMU-zadane-pytania-2026.pdf) (strona Radia Naukowego).
- Pytania z Księżyca: [GitHub gist](https://gist.githubusercontent.com/BERENZ/a2f58c81f5983e8f6b9e5191be4bad8a/raw/0fee1aec9d5ec6769ebe6e20bdeb0600ee0be692/pytania-z-ksiezyca.txt).

## Wykorzystane narzędzia

- [sentence-transformers](https://www.sbert.net/) z modelem [`sdadas/st-polish-paraphrase-from-distilroberta`](https://huggingface.co/sdadas/st-polish-paraphrase-from-distilroberta)
- [UMAP](https://umap-learn.readthedocs.io/) — redukcja wymiarów
- [Plotly](https://plotly.com/python/) — interaktywne wykresy
- [PyMuPDF](https://pymupdf.readthedocs.io/) — parsowanie PDF
