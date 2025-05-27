# Creazione di un Agente AI Intelligente per Ricette con Agno

**Durata:** 2 ore (flessibile)

**Obiettivo Principale:** Sviluppare un agente AI (basato su Agno) che suggerisca ricette personalizzate in base agli ingredienti disponibili e alle preferenze dietetiche dell'utente. L'agente deve essere in grado di ricordare e aggiornare le preferenze di ciascun utente in modo indipendente.

## Obiettivi di Apprendimento

Al termine di questa esercitazione, sarai in grado di:
- ✓ Configurare un ambiente Python con uv
- ✓ Creare un agente AI base utilizzando Agno
- ✓ Implementare un sistema di memoria persistente multi-utente
- ✓ Configurare istruzioni efficaci per guidare il comportamento dell'agente
- ✓ Utilizzare il debug mode per analizzare e migliorare l'agente

---

## Parte 1: Setup dell'Ambiente

### Obiettivi della Sezione
- Configurare l'ambiente di sviluppo Python
- Installare le dipendenze necessarie
- Configurare le API keys richieste

### 1.1 Creazione dell'Ambiente Virtuale

Utilizzeremo **uv** di Astral per gestire l'ambiente Python.

1. **Verifica installazione di uv:**
  ```bash
  pip install uv
  ```
2. **Crea l'ambiente virtuale:**
  ```bash
  uv venv agno_recipe_env
  ```
3. **Attiva l'ambiente virtuale:**
- Mac/Linux:
```bash
source agno_recipe_env/bin/activate
```
- Windows:
```bash
agno_recipe_env\Scripts\activate
```

### 1.2 Installazione delle Dipendenze

Installa i pacchetti necessari utilizzando uv:

```bash
uv pip install -U agno google-generativeai sqlalchemy
```

### 1.3 Configurazione API Key

Imposta la chiave API di Google AI Studio come variabile d'ambiente:

- Mac/Linux:
```bash
export GOOGLE_API_KEY="YOUR_GOOGLE_API_KEY"
```
- Windows:
```bash
setx GOOGLE_API_KEY "YOUR_GOOGLE_API_KEY"
```
**Nota:** Puoi ottenere la chiave da Google AI Studio
