# 🎯 Jak używać RAG z GitHub Copilot - ZERO HALUCYNACJI

## Filozofia

Zamiast pozwalać Copilotowi "wymyślać" kod oparty na jego treningu, **karmisz go aktualnymi fragmentami dokumentacji** przed każdym pytaniem. Copilot staje się wtedy "tłumaczem dokumentacji", nie "wyrocznia".

---

## 🚀 Quick Start (3 kroki)

### 1. Uruchom generator promptów

```bash
cd RAG
python3 generate_prompt.py          # Tylko PrimeVue
# lub
python3 generate_prompt_universal.py  # Wybór: PrimeVue/Nuxt/Oba
```

### 2. Zadaj pytanie

```
🔎 O co chcesz zapytać?: Jak zrobić sortowanie w DataTable?
```

Skrypt przeszuka bazę wektorową i wypluwa gotowy prompt.

### 3. Skopiuj i wklej do Copilot Chat

1. **Zaznacz** tekst między `===== SKOPIUJ PONIŻEJ =====`
2. **Skopiuj** (Ctrl+C)
3. **Otwórz GitHub Copilot Chat** w VS Code (Ctrl+Alt+I lub ikona)
4. **Wklej** (Ctrl+V) i wyślij

Copilot otrzyma:

- 7 fragmentów dokumentacji dokładnie o tym co pytałeś
- Surową regułę: "Używaj TYLKO tego kontekstu"
- Twoje pytanie

---

## 🎬 Przykładowy Workflow

### Przykład 1: Tworzenie komponentu PrimeVue

**Pytanie:** "Jak stworzyć DataTable z paginacją i sortowaniem?"

```bash
python3 generate_prompt.py
# Wpisz pytanie
# Skopiuj wygenerowany prompt
# Wklej do Copilot Chat
```

**Co dostaniesz:**

- Kod DataTable ze wszystkimi propami
- Binding do danych
- Konfiguracja kolumn
- **BEZ outdated API** - bo źródłem jest Twoja aktualna dokumentacja

### Przykład 2: Composables w Nuxt

**Pytanie:** "Jak zrobić composable do obsługi API w Nuxt 3?"

```bash
python3 generate_prompt_universal.py
# Wybierz: 2 (Nuxt)
# Wpisz pytanie
# Skopiuj + wklej do Copilot
```

**Co dostaniesz:**

- Prawidłowa struktura `/composables/useApi.ts`
- `useFetch` vs `$fetch` - kiedy co
- Auto-import
- TypeScript types

---

## ⚙️ Konfiguracja VS Code dla maksymalnej precyzji

### Ustawienia `.vscode/settings.json` (już skonfigurowane)

```json
{
  "github.copilot.advanced": {
    "debug.overrideEngine": "gpt-4" // Lepszy model = mniej halucynacji
  },
  "github.copilot.enable": {
    "*": true,
    "markdown": true,
    "python": true,
    "typescript": true,
    "vue": true
  }
}
```

### Dodatkowe ustawienia (opcjonalne)

Jeśli chcesz jeszcze bardziej kontrolować Copilota:

```json
{
  "github.copilot.editor.enableAutoCompletions": true,
  "github.copilot.editor.enableCodeActions": true
}
```

---

## 📋 Zasady Anty-Halucynacyjne

### ✅ RÓB TAK:

1. **Zawsze używaj `generate_prompt.py` przed złożonymi pytaniami**
   - "Jak zrobić X w PrimeVue?" → generator → Copilot

2. **Weryfikuj odpowiedź z fragmentami kontekstu**
   - Copilot podaje źródło (Header 1 > Header 2)
   - Sprawdź czy to ma sens

3. **Pytaj konkretnie**
   - ❌ "Jak działa routing?"
   - ✅ "Jak używać dynamicznych route params w Nuxt 3?"

4. **Używaj wygenerowanego promptu jako "source of truth"**
   - Jeśli Copilot odbiega od kontekstu → przypominasz: "Use ONLY the context provided"

### ❌ NIE RÓB TAK:

1. **Nie pytaj Copilota na ślepo o API**
   - Bez kontekstu może wymyślić nieistniejące props

2. **Nie ufaj bezwarunkowo autouzupełnieniom**
   - Inline suggestions mogą być z treningu, nie z dokumentacji

3. **Nie mieszaj frameworków w jednym pytaniu**
   - Wybierz bazę (Nuxt OR PrimeVue) i trzymaj się jej

---

## 🔧 Zaawansowane: Workflow dla większych zadań

### Scenariusz: Budowa CRUDa z PrimeVue

1. **Pytanie 1:** "Jak stworzyć DataTable z CRUD operations?"

   ```bash
   python3 generate_prompt_universal.py  # Obie bazy
   ```

2. **Pytanie 2:** "Jak zrobić Dialog do edycji rekordu?"

   ```bash
   python3 generate_prompt.py  # Tylko PrimeVue
   ```

3. **Pytanie 3:** "Jak wykonać PUT request w Nuxt 3?"
   ```bash
   python3 generate_prompt_universal.py  # Nuxt
   ```

Każde pytanie = nowy prompt → czysta separacja concerns → zero konfuzji.

---

## 🛠️ Parametry do eksperymentowania

### W `generate_prompt.py` możesz zmienić:

```python
TOP_K = 7  # Ile fragmentów dokumentacji (3-10)
```

- **3-5**: Szybkie odpowiedzi, mniej kontekstu
- **7-10**: Bardziej kompletne, dłuższe prompty
- **Claude Sonnet**: Udźwignie nawet 15 fragmentów

---

## 🎓 Dlaczego to działa?

| Problem                   | Rozwiązanie RAG                                  |
| ------------------------- | ------------------------------------------------ |
| Copilot wymyśla stare API | Dostajesz aktualną dokumentację                  |
| Copilot miesza frameworki | Wybierasz bazę (Nuxt XOR PrimeVue)               |
| Copilot "domyśla się"     | Reguła: "NO OUTSIDE KNOWLEDGE"                   |
| Brak źródeł               | Każdy fragment ma nagłówek (Header 1 > Header 2) |

---

## 📚 Dodatkowe Materiały

- [RAG/README.md](README.md) - Jak działa indeksowanie
- [.github/copilot-instructions.md](../.github/copilot-instructions.md) - Konwencje projektu

---

## 💡 Pro Tips

1. **Trzymaj terminal z `generate_prompt.py` otwarty** podczas kodowania
   - Pytasz → Kopiujesz → Wklejasz → Kodujesz → Repeat

2. **Zapisz często używane prompty** w pliku tekstowym
   - `my_prompts.txt` z gotowymi kontekstami

3. **Używaj Claude Sonnet zamiast GPT-4 w Copilot Chat?**
   - Sonnet jest lepszy w trzymaniu się kontekstu
   - Ustawienia Copilot: Eksperymentuj z modelami

4. **Dodaj własne reguły do promptu**
   - Np. "Always use TypeScript strict mode"
   - Edytuj `generate_prompt.py` → sekcja `<critical_rules>`

---

## 🐛 Troubleshooting

### "Copilot nadal halucynuje"

1. Sprawdź czy skopiowałeś **cały prompt** (z `<context>`)
2. Zwiększ `TOP_K` do 10 (więcej kontekstu)
3. Dodaj na końcu promptu: "REMEMBER: Use ONLY the provided context. No external knowledge."

### "Brak fragmentów dla mojego pytania"

1. Twoje pytanie może być zbyt ogólne → Sprecyzuj
2. Sprawdź czy temat jest w dokumentacji (`nuxt-llms-full.txt` / `primevue-llms-full.txt`)
3. Zmień formulację pytania (semantyczny search jest wrażliwy na słowa kluczowe)

### "Skrypt się crashuje"

```bash
pip install --upgrade langchain-community langchain-chroma sentence-transformers
```

---

## ✅ Checklist dla każdego nowego feature

- [ ] Uruchom `generate_prompt.py` z pytaniem
- [ ] Skopiuj wygenerowany prompt
- [ ] Wklej do Copilot Chat
- [ ] Sprawdź czy kod używa TYLKO wzorców z kontekstu
- [ ] Zweryfikuj cytowane źródła (Headers)
- [ ] Przetestuj kod

**Jeśli Copilot odbiega od dokumentacji → Nowy prompt z bardziej precyzyjnym pytaniem.**

---

Made with 🧠 + ChromaDB + 💚 Nuxt/PrimeVue
