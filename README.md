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

# Checkpoint 1
- [ ] L'ambiente virtuale è attivo
- [ ] Tutti i pacchetti sono installati senza errori
- [ ] La variabile d'ambiente GOOGLE_API_KEY è configurata

---

## Parte 2: Sviluppo dell'Agente "Chef Assistant"

### Obiettivi della Sezione
* Creare un agente AI funzionante
* Implementare la gestione di ingredienti e preferenze
* Configurare la memoria persistente multi-utente

### 2.1 Definizione dell'Agente di Base
**Task 1:** Crea un nuovo file chiamato `recipe_agent.py`

**Struttura base del file:**

```python
# TODO: Importare le classi necessarie da agno
# Suggerimento: Agent, Gemini, SqliteStorage, SqliteMemoryDb, Memory

# TODO: Definire le costanti per i percorsi del database
# Suggerimento: DB_FILE, AGENT_SESSIONS_TABLE, USER_MEMORIES_TABLE

# TODO: Creare l'oggetto agent con:
#   - Un nome appropriato
#   - Il modello Gemini
#   - Instructions che guidino l'interazione
#   - Storage e Memory configurati correttamente

# TODO: Sezione main per eseguire l'agente
if __name__ == "__main__":
    # Implementa qui la logica per avviare l'agente
```

**Domande guida:**

* Quali classi di Agno sono necessarie per creare un agente con memoria persistente?
* Come puoi strutturare le instructions per far sì che l'agente si comporti come un assistente culinario?
* Quale metodo dell'agente permette di avviare una chat da riga di comando?

---

## Checkpoint 2
Dopo aver completato l'agente base:

- [ ] Eseguendo `python recipe_agent.py`, l'agente si avvia
- [ ] L'agente si presenta e chiede informazioni sugli ingredienti
- [ ] È possibile interagire con l'agente tramite la CLI

## 2.2 Gestione degli Ingredienti e delle Preferenze
**Task 2:** Affina le instructions dell'agente

L'agente dovrebbe essere in grado di:

1.  Identificare e confermare gli ingredienti forniti dall'utente
2.  Chiedere esplicitamente e registrare le preferenze dietetiche
3.  Suggerire ricette basate su queste informazioni

**Suggerimenti per le instructions:**

* Usa un tono amichevole e professionale
* Struttura le domande in modo chiaro
* Guida l'agente a chiedere sempre le allergie

**Output atteso esempio:**

```
Chef Assistant: Ciao! Sono il tuo assistente culinario personale. 
Quali ingredienti hai a disposizione oggi?

User: Ho pasta, pomodori e basilico

Chef Assistant: Ottimo! Prima di suggerirti delle ricette, 
hai delle preferenze dietetiche o allergie che dovrei conoscere?
```

## 2.3 Implementazione della Memoria Utente Multipla
**Task 3:** Configura la memoria persistente

**Requisiti:**

* Utilizza SqliteStorage per le sessioni
* Utilizza Memory con SqliteMemoryDb per le memorie utente
* Abilita la gestione delle memorie utente nell'agente

**Suggerimenti implementativi:**

1.  Crea una directory `tmp/` per i file del database
2.  Definisci nomi univoci per le tabelle
3.  Ricorda di impostare `enable_user_memories=True`

**Task 4:** Modifica il main per gestire user_id

```python
if __name__ == "__main__":
    # TODO: Chiedi all'utente di inserire un user_id
    # TODO: Passa il user_id al metodo cli_app() dell'agente
```

# Checkpoint 3
Test della memoria multi-utente:

- [ ] L'applicazione chiede un user_id all'avvio
- [ ] Utenti diversi hanno conversazioni separate
- [ ] Le preferenze vengono ricordate tra sessioni

---

## Parte 3: Test Avanzato e Debug

### Obiettivi della Sezione
* Testare scenari complessi
* Utilizzare il debug mode per analizzare il comportamento
* Ottimizzare le performance dell'agente

### 3.1 Test di Scenari Complessi

**Test Case 1 - Primo utente (vegetariano)**

User ID: mario_rossi
Test 1: "Ho pomodori, mozzarella, basilico e pasta"
Test 2: "Sono vegetariano"
Test 3: Riavvia con stesso user_id e verifica la memoria

---

**Test Case 2 - Secondo utente (allergie)**

User ID: anna_bianchi
Test 1: "Ho farina, latte, uova e cioccolato"
Test 2: "Sono allergica alle noci"
Test 3: Riavvia e chiedi una ricetta con cioccolato

---

**Test Case 3 - Modifica preferenze**

User ID: mario_rossi (già esistente)
Test: "Da oggi mangio anche pesce"
Verifica: L'agente aggiorna le preferenze?

---

**3.2 Debugging e Miglioramento**

**Task 5:** Attiva il debug mode

Modifica la configurazione dell'agente impostando `debug_mode=True`

**Analisi dei log:**

* Osserva come l'agente processa l'input
* Analizza le interazioni con il sistema di memoria
* Identifica le chiamate al modello LLM

**Domande per l'analisi:**

* Quali informazioni vengono salvate nella memoria?
* Come l'agente decide quando aggiornare una preferenza?
* Ci sono ridondanze nelle chiamate al modello?

**Checkpoint 4**

* [ ] Il debug mode mostra log dettagliati
* [ ] Hai identificato almeno un'area di miglioramento
* [ ] Hai proposto modifiche alle instructions basate sui log

---

**Parte 4: Troubleshooting**

**Problemi Comuni e Soluzioni**

**Errore: "API key not found"**

* Verifica che `GOOGLE_API_KEY` sia impostata correttamente
* Riavvia il terminale dopo aver impostato la variabile

**Errore: "Module not found"**

* Assicurati che l'ambiente virtuale sia attivo
* Reinstalla i pacchetti con `uv pip install`

**Errore: "Database error"**

* Crea manualmente la directory `tmp/` se non esiste
* Verifica i permessi di scrittura sulla directory

**La memoria non persiste:**

* Controlla che `enable_user_memories=True` sia impostato
* Verifica che stai usando lo stesso `user_id`

---

**Conclusione e Possibili Estensioni**

**Checklist di Completamento**

* [ ] L'agente identifica correttamente gli ingredienti dall'input
* [ ] Le preferenze dietetiche vengono memorizzate
* [ ] Utenti diversi hanno memorie separate
* [ ] L'agente suggerisce ricette appropriate
* [ ] Il debug mode fornisce informazioni utili

**Idee per Estensioni Future**

**1. Knowledge Base Strutturata**
* Integrare AgentKnowledge con un database di ricette
* Utilizzare PDFKnowledgeBase per ricettari in PDF

**2. Tool Personalizzati**
* Creare tool per cercare ricette online
* Implementare calcolo dei valori nutrizionali

**3. Interfaccia Utente**
* Sviluppare UI con Streamlit
* Utilizzare il sistema Playground di Agno

**Risorse Utili**
* Documentazione Agno: https://docs.agno.com
* Google AI Studio: https://aistudio.google.com
