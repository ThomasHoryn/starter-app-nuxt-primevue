# 📋 Przykładowe pytania do testowania systemu RAG

## PrimeVue - Komponenty

### DataTable

- "Jak zrobić sortowanie w DataTable?"
- "Jak dodać paginację do DataTable w PrimeVue?"
- "Jak customizować kolumny w DataTable?"
- "Jak zrobić filtry w DataTable?"
- "Jak obsłużyć selection w DataTable?"

### Dialog/Modal

- "Jak stworzyć Dialog w PrimeVue?"
- "Jak przekazać dane do Dialog w PrimeVue?"
- "Jak obsłużyć zamknięcie Dialog?"

### Form Components

- "Jak używać InputText w PrimeVue?"
- "Jak zrobić walidację formularza z PrimeVue?"
- "Jak używać Dropdown w PrimeVue?"
- "Jak użyć Calendar do wyboru daty?"

### Toast/Messages

- "Jak pokazać toast notification w PrimeVue?"
- "Jak używać Toast service w PrimeVue?"
- "Jak dodać Message do komponentu?"

### Styling

- "Jak customizować theme w PrimeVue?"
- "Jak używać Tailwind z PrimeVue?"
- "Jak stylować komponenty PrimeVue?"

---

## Nuxt 3 - Core Concepts

### Routing

- "Jak działają dynamic routes w Nuxt 3?"
- "Jak używać route params w Nuxt 3?"
- "Jak zrobić nested routes w Nuxt 3?"
- "Jak używać middleware w Nuxt 3?"

### Data Fetching

- "Jak używać useFetch w Nuxt 3?"
- "Jaka jest różnica między useFetch a $fetch w Nuxt 3?"
- "Jak obsługiwać błędy w useFetch?"
- "Jak zrobić server-side fetching w Nuxt 3?"

### Composables

- "Jak stworzyć composable w Nuxt 3?"
- "Jak używać useState w Nuxt 3?"
- "Jak zrobić shared state w Nuxt 3?"
- "Gdzie umieścić composables w Nuxt 3?"

### Server

- "Jak stworzyć API endpoint w Nuxt 3?"
- "Jak używać server routes w Nuxt 3?"
- "Jak obsłużyć POST request w Nuxt server?"

### Configuration

- "Jak skonfigurować Nuxt 3?"
- "Jak dodać moduły do Nuxt 3?"
- "Jak używać runtime config w Nuxt 3?"
- "Jak skonfigurować TypeScript w Nuxt 3?"

### Components

- "Jak działają auto-imports w Nuxt 3?"
- "Jak zrobić layout w Nuxt 3?"
- "Jak używać pages w Nuxt 3?"

---

## Kombinowane (Nuxt + PrimeVue)

### Integration

- "Jak zintegrować PrimeVue z Nuxt 3?"
- "Jak używać PrimeVue components w Nuxt 3?"
- "Jak skonfigurować PrimeVue w nuxt.config?"

### CRUD Operations

- "Jak zrobić CRUD z DataTable w Nuxt 3?"
- "Jak obsłużyć formularz edycji w Nuxt z PrimeVue?"
- "Jak połączyć useFetch z DataTable w PrimeVue?"

### State Management

- "Jak zarządzać stanem formularza z PrimeVue w Nuxt 3?"
- "Jak używać useState z PrimeVue components?"

---

## Testowanie systemu

### Krok po kroku

1. **Wybierz pytanie z listy powyżej**

2. **Uruchom generator:**

   ```bash
   cd RAG
   python3 generate_prompt_universal.py
   ```

3. **Wybierz bazę:**
   - `1` dla pytań o PrimeVue
   - `2` dla pytań o Nuxt
   - `3` dla pytań kombinowanych

4. **Wklej pytanie i naciśnij Enter**

5. **Skopiuj wygenerowany prompt**

6. **Wklej do GitHub Copilot Chat w VS Code**

7. **Porównaj odpowiedź z fragmentami kontekstu w prompcie**

---

## Własne pytania - Zasady

### ✅ Dobre pytania (specyficzne):

- "Jak używać composable useAsyncData w Nuxt 3?"
- "Jak customizować kolory w PrimeVue DataTable?"
- "Jak obsłużyć error state w useFetch Nuxt 3?"

### ❌ Złe pytania (zbyt ogólne):

- "Jak działa Nuxt?"
- "Co to jest PrimeVue?"
- "Jak robić aplikacje?"

### 💡 Wskazówki:

- Używaj nazw komponentów/API z dokumentacji
- Pytaj o konkretne przypadki użycia
- Jeśli pytanie jest szerokie, podziel je na mniejsze

---

## Benchmark - Sprawdź czy system działa

Przetestuj te 3 pytania i sprawdź czy odpowiedzi:

1. ✅ Cytują źródła (Headers)
2. ✅ Używają tylko wiedzy z kontekstu
3. ✅ Nie wymyślają nieistniejących API

### Test 1: PrimeVue DataTable

**Pytanie:** "Jak zrobić sortowanie w DataTable?"
**Oczekiwane:** Kod z propem `sortable`, przykład użycia

### Test 2: Nuxt useFetch

**Pytanie:** "Jaka jest różnica między useFetch a $fetch?"
**Oczekiwane:** Wyjaśnienie SSR vs client-side

### Test 3: Kombinowane

**Pytanie:** "Jak połączyć Nuxt 3 composable z PrimeVue DataTable?"
**Oczekiwane:** Przykład użycia `useFetch` + `DataTable`

Jeśli wszystkie 3 testy przechodzą → System działa poprawnie! 🎉

---

Made with 🧠 + RAG
