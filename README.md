# Kalkulator PWA + analiza zadań (Gemini)

Kalkulator w stylu iOS. Skaner zadań: **przytrzymaj wyświetlacz ~0,6 s** → menu → „Skanuj zadanie".
Aparat włącza się dopiero po „Zrób zdjęcie", a zdjęcie jest wysyłane po „Wyślij do analizy". Nic nie jest zapisywane na serwerze; historia leży w localStorage.

## Architektura
- `src/calc.ts` – logika kalkulatora (czysta funkcja `press`)
- `src/App.tsx` – UI, wyświetlacz/wynik AI, menu, historia
- `src/Scanner.tsx` – aparat (input capture), zmniejszanie do 1280 px, wysyłka, loader, błędy
- `src/history.ts` – historia w localStorage
- `api/analyze.ts` – funkcja serverless (Vercel), jedyne miejsce z kluczem Gemini

## Uruchomienie
1. Klucz: https://aistudio.google.com/apikey → „Create API key".
2. `npm install`
3. Lokalnie z funkcją API: `npm i -g vercel`, plik `.env.local` z `GEMINI_API_KEY=twój_klucz`, potem `vercel dev`.
4. Wdrożenie: `vercel` (lub repo na GitHubie → Import w Vercel), w Settings → Environment Variables dodaj `GEMINI_API_KEY`, redeploy.
5. iPhone: otwórz adres HTTPS w Safari → Udostępnij → „Dodaj do ekranu początkowego". Aparat wymaga HTTPS.

Opcjonalnie `GEMINI_MODEL` (domyślnie `gemini-2.5-flash`). Splash screen iOS jest generowany z ikony i koloru tła z manifestu.
Wskazówka: w Google AI Studio ustaw limit/budżet dla klucza, bo endpoint `/api/analyze` jest publiczny.
