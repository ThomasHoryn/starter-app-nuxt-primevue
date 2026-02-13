# 🎬 Quick Start Guide - Krok po kroku

## 🎯 Cel

Nauczyć GitHub Copilot używać **wyłącznie** dokumentacji Nuxt i PrimeVue z Twojej bazy wektorowej, bez halucynacji.

---

## ⚡ Szybki start (5 minut)

### 1. Upewnij się że bazy są zaindeksowane

```bash
ls -la RAG/chroma_db_*
```

Powinny być 2 katalogi:

- `chroma_db_nuxt/` (37MB)
- `chroma_db_primevue/` (24MB)

Jeśli ich nie ma, uruchom:

```bash
cd RAG
python3 index_db.py
```

### 2. Test prostego zapytania

```bash
cd RAG
python3 generate_prompt.py
```

Gdy pyta "O co chcesz zapytać?", wpisz:

```
Jak zrobić sortowanie w DataTable?
```

Powinien wyświetlić długi prompt z fragmentami dokumentacji.

### 3. Skopiuj i wklej do Copilot Chat

1. **Zaznacz** tekst między liniami:

   ```
   ================ SKOPIUJ PONIŻEJ ================
   ...
   ================ KONIEC KOPIOWANIA ================
   ```

2. **Skopiuj** (Ctrl+C / Cmd+C)

3. **Otwórz GitHub Copilot Chat** w VS Code:
   - Klawisz: `Ctrl+Alt+I` (Linux/Win) lub `Cmd+Alt+I` (Mac)
   - Lub: Ikona Copilot w pasku bocznym → Chat

4. **Wklej** (Ctrl+V) i wyślij Enter

5. **Sprawdź odpowiedź:**
   - ✅ Cytuje źródła (np. "DataTable > Sortable Mode")
   - ✅ Kod używa propów z dokumentacji
   - ✅ NIE wymyśla nieistniejących API

---

## 📋 Przykład kompletnego workflow

### Scenariusz: Chcesz zrobić CRUD z PrimeVue

#### Krok 1: DataTable

```bash
python3 generate_prompt.py
```

Pytanie: "Jak stworzyć DataTable z paginacją i sortowaniem?"
→ Skopiuj → Wklej do Copilot → Otrzymasz kod DataTable

#### Krok 2: Dialog do edycji

```bash
python3 generate_prompt.py
```

Pytanie: "Jak stworzyć Dialog do edycji rekordu w PrimeVue?"
→ Skopiuj → Wklej do Copilot → Otrzymasz kod Dialog

#### Krok 3: API w Nuxt

```bash
python3 generate_prompt_universal.py
```

Wybierz: `2` (Nuxt)
Pytanie: "Jak wykonać PUT request w Nuxt 3?"
→ Skopiuj → Wklej do Copilot → Otrzymasz composable z useFetch

---

## 🔧 Opcje zaawansowane

### Użyj universal generator (obie bazy)

```bash
python3 generate_prompt_universal.py
```

Wybierz opcję:

- `1` - Tylko PrimeVue
- `2` - Tylko Nuxt
- `3` - Obie bazy (dla pytań kombinowanych)

### Zmień ilość fragmentów kontekstu

Edytuj `generate_prompt.py`:

```python
TOP_K = 10  # Zwiększ z 7 do 10 dla większego kontekstu
```

**Uwaga:** Więcej fragmentów = dłuższy prompt, ale dokładniejsze odpowiedzi.

---

## 🎓 Najlepsze praktyki

### ✅ Tak należy robić:

1. **Zawsze używaj generatora przed złożonym pytaniem**
   - Nie pytaj Copilota "na ślepo" o API

2. **Weryfikuj cytowane źródła**
   - Sprawdź czy fragmenty w prompcie rzeczywiście odpowiadają na pytanie

3. **Jeden prompt = jedno pytanie**
   - Nie zadawaj wielu pytań w jednym prompcie

4. **Używaj konkretnych nazw z dokumentacji**
   - "DataTable props" zamiast "opcje tabelki"

### ❌ Tak NIE należy robić:

1. **Nie mieszaj frameworków w jednym pytaniu**
   - Źle: "Jak używać Vue Router w React?"
   - Dobrze: "Jak używać route params w Nuxt 3?"

2. **Nie ufaj autouzupełnieniom bez kontekstu**
   - Inline suggestions mogą być przestarzałe

3. **Nie pytaj o rzeczy spoza dokumentacji**
   - Jeśli nie ma w bazie, Copilot powie "Brak informacji"

---

## 🐛 Troubleshooting

### Problem: "Copilot nadal halucynuje"

**Rozwiązanie:**

1. Upewnij się że skopiowałeś **cały prompt** (z `<context>`)
2. Zwiększ `TOP_K` do 10 w pliku
3. Na końcu promptu dodaj: "REMEMBER: Use ONLY the provided context."

### Problem: "Brak fragmentów dla mojego pytania"

**Rozwiązanie:**

1. Pytanie jest zbyt ogólne → Sprecyzuj
2. Zmień formulację (spróbuj innych słów kluczowych)
3. Sprawdź czy temat jest w dokumentacji:
   ```bash
   grep -i "nazwa_tematu" RAG/nuxt-llms-full.txt
   ```

### Problem: "Skrypt się crashuje"

**Rozwiązanie:**

```bash
pip install --upgrade langchain-community langchain-chroma sentence-transformers
```

---

## 📊 Benchmark - Czy system działa?

Przetestuj te 3 pytania:

### Test 1: PrimeVue

```
Pytanie: "Jak zrobić sortowanie w DataTable?"
Oczekiwane: Prop `sortable`, przykład użycia
```

### Test 2: Nuxt

```
Pytanie: "Jaka jest różnica między useFetch a $fetch?"
Oczekiwane: Wyjaśnienie SSR vs client-side
```

### Test 3: Kombinowane

```
Pytanie: "Jak połączyć Nuxt composable z PrimeVue DataTable?"
Oczekiwane: Kod z useFetch + :value binding
```

**Jeśli wszystkie 3 przechodzą → System działa! 🎉**

---

## 📚 Więcej pomocy

- 📖 [USAGE.md](USAGE.md) - Pełna dokumentacja
- 💡 [EXAMPLE_QUESTIONS.md](EXAMPLE_QUESTIONS.md) - 50+ gotowych pytań
- 🔧 [README.md](README.md) - Dokumentacja techniczna

---

## 🚀 Następne kroki

Po opanowaniu podstaw:

1. **Dostosuj critical_rules** w `generate_prompt.py`
   - Dodaj własne reguły (np. "Always use TypeScript strict")

2. **Stwórz FAQ z często używanymi promptami**
   - Zapisz prompty w pliku tekstowym

3. **Eksperymentuj z TOP_K**
   - Znajdź optymalną ilość fragmentów dla Twoich potrzeb

---

Made with 🧠 + RAG + GitHub Copilot
