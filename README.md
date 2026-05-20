# Raptor
Sistema Cognitivo AI Modulare

Raptor è un assistente AI modulare orientato a:

memoria persistente
orchestrazione multi-provider
retrieval cognitivo
automazione personale
continuità operativa
reasoning contestuale
integrazione strumenti reali

Il progetto nasce come evoluzione da semplice chatbot a sistema cognitivo operativo persistente.

Repository per un assistente IA modulare basato su Telegram, Obsidian Vault, memoria semantica, retrieval cognitivo e modelli AI ibridi locali/remoti.

---

# Panoramica

Raptor è un assistente IA personale progettato come sistema cognitivo modulare con:

* memoria episodica gerarchica
* memoria semantica vettoriale
* retrieval cognitivo multi-dominio
* integrazione Telegram
* input testuale e vocale da Telegram
* integrazione Obsidian Vault
* gestione calendario local-first con preview e conferma
* stato operativo persistente minimale
* audit security controllati su target autorizzati
* ingestione documentale e pipeline di conoscenza
* package dedicati per archivi Internet Archive ed embeddings
* routing intelligente tra modelli AI
* architettura estendibile e multi-workflow

Il progetto utilizza:

* Groq
* Cerebras
* Ollama
* ChromaDB
* CrewAI
* Telegram Bot API
* Google Calendar API e Google Task API
* Vault Markdown Obsidian

---

# Funzionalità

## Core AI

* Routing ibrido dei modelli LLM (Groq + Cerebras + Ollama)
* Ragionamento avanzato con CrewAI
* Pipeline di reranking cognitivo
* Workflow AI modulari
* Motore di retrieval semantico
* System prompt arricchito con identity, orario locale, timelinecognitiva stato operativo

outing AI Multi-Provider

Pipeline AI resiliente:

Groq
 ↓
Cerebras
 ↓
Ollama locale

Obiettivi:

resilienza rate limit
continuità operativa
riduzione dipendenza cloud
fallback automatici
supporto offline

## Sistema di Memoria

* Memoria episodica
* Memoria vettoriale semantica
* Consolidamento gerarchico della memoria
* Tracciamento dei workflow
* Memoria persistente a lungo termine
* Deduplicazione della memoria
* Calcolo dell'importanza semantica
* Analisi della densità semantica
* Stato operativo leggero in `state/current.json`

## Interazione Telegram

* Messaggi testuali
* Messaggi vocali Telegram
* Trascrizione vocale con `faster-whisper`
* Routing unico: testo e vocali passano dagli stessi intent handler
* Supporto ai follow-up vocali nei workflow attivi

## Retrieval e Vettorizzazione

* Persistenza locale ChromaDB
* Vettorizzazione basata su domini
* Retrieval multi-dominio
* Pipeline di ingestione Telegram
* Workflow di ingestione PCloud
* Ingestione di conoscenza Markdown

## Integrazione Obsidian

* Sincronizzazione del vault Markdown
* Generazione automatica di note
* Ricerca semantica nelle note
* Sincronizzazione Git
* Indicizzazione della conoscenza

## Email

* Lettura email recenti e non lette
* Ricerca testuale e semantica
* Filtro email importanti
* Sintesi rapida delle email recenti
* Invio e risposta email con preview obbligatoria
* Firma email configurabile per invii SMTP
* Conferma destinatari da rubrica locale
* Check giornaliero automatico delle email importanti
* Alert Telegram per possibili email cliente/lavoro
* Deduplica locale degli alert già inviati
* Provider supportati: Aruba e Gmail via IMAP/SMTP

## Task

* Integrazione Google Tasks
* Creazione task da linguaggio naturale
* Lista task aperte
* Completamento task
* Eliminazione task
* Parser LLM con fallback locale
* Riconoscimento di priorità e data quando disponibili

## Ricerca Web

* Ricerca esplicita con `/web` e frasi naturali
* Sintesi breve dei risultati tramite LLM
* Fonti sempre incluse nella risposta
* Supporto per verifica, notizie e documentazione aggiornata
* Filtro intent per evitare falsi positivi come `si verifica`
* Log locale leggero delle ricerche in `data/web/search_log.json`

## Audit Security

* Comando Telegram `/audit`
* OSINT passivo dominio con `/security_osint`
* OSINT pubblico persona/azienda con `/security_person_osint`
* Esecuzione solo su target presenti in allowlist
* Gestione allowlist da Telegram con `/audit_allow`
* Modalità automatiche: `passive`, `web-light`, `recon`, `network`, `full-audit`
* Modalità `real-audit` con conferma obbligatoria via pulsanti Telegram (`/audit dominio.it real-audit` o `/real_audit dominio.it`)
* Gate offensive controllato con `/offensive_enable`, `/offensive_run safe`, `/offensive_explicit`, `/offensive_disable`
* `/audit` senza argomenti mostra l'uso corretto e le modalità disponibili
* Tool locali supportati: httpx, nuclei, sslscan, whatweb, nmap, ffuf, subfinder, naabu, dnsx, katana, wafw00f, amass, gau, waybackurls, LinkFinder, SecretFinder, sqlmap, theHarvester, Maigret, Sherlock
* Parsing automatico di finding nuclei, TLS deprecati e tecnologie rilevate
* Calcolo sintetico del rischio e grafo della superficie d'attacco
* Report Markdown e JSON salvati in `reports/security/`

## Infrastruttura

* Architettura modulare
* Workflow asincroni
* Database vettoriale local-first
* Sistema di storage persistente
* Sistema estendibile di handler e moduli

## Calendario

* Comandi `/calendar oggi`, `/calendar domani`, `/calendar settimana`
* Creazione eventi da linguaggio naturale
* Follow-up conversazionale per dettagli mancanti
* Orari parziali come `15`, `alle 15`, `15:30`
* Ricerca, modifica/spostamento e cancellazione eventi
* Preview obbligatoria prima di ogni modifica
* Bottoni Telegram di conferma, modifica e annullamento
* Storage locale JSON in `data/calendar/events.json`
* Client astratto per backend locale o Google Calendar

## Tempo e Stato Operativo

* Timezone centrale: `Europe/Rome`
* Utility tempo in `core/datetime_utils.py`
* Timestamp runtime coerenti con `now_iso()`
* Stato operativo persistente in `state/current.json`
* Lo stato non sostituisce memoria, task manager o knowledge base


# Installazione

## Clonare il Repository

```bash
git clone <repository_url>
cd assistente_ia
```

## Attivare l'Ambiente Virtuale

```bash
source venv_crew/bin/activate
```

## Installare le Dipendenze

```bash
pip install -r requirements.txt
```

## Verifica locale

Esegui i test dalla root del progetto:

```bash
PYTHONPATH=. python -m unittest discover -s tests
```

Per verificare solo il parser della ricerca web:

```bash
PYTHONPATH=. python -m unittest tests.test_web_intent
```

La suite completa presuppone le dipendenze di `requirements.txt` installate
nel virtualenv attivo.

---

# Configurazione Ambiente

Raptor utilizza un file `.env` per la configurazione locale.

## Esempio `.env`

```env
TELEGRAM_TOKEN=
YOUR_CHAT_ID=
GROQ_API_KEY=

LLM_MODEL=llama3

PCLOUD_FOLDER_URL=

MEMORY_DIR=/home/opc/assistente_ia/memory
VAULT_PATH=/home/opc/assistente_ia/privatebrain

OLLAMA_BASE_URL=http://localhost:11434

CALENDAR_BACKEND=local
CALENDAR_EVENTS_FILE=
CALENDAR_ID=primary
CALENDAR_CREDENTIALS_FILE=
CALENDAR_TOKEN_FILE=
CALENDAR_DEFAULT_DURATION_MINUTES=60

TASKS_CREDENTIALS_FILE=/home/opc/assistente_ia/secrets/tasks_credentials.json
TASKS_TOKEN_FILE=/home/opc/assistente_ia/secrets/tasks_token.json

WEB_SEARCH_LOG_FILE=/home/opc/assistente_ia/data/web/search_log.json

EMAIL_ARUBA_ADDRESS=
EMAIL_ARUBA_PASSWORD=
EMAIL_ARUBA_IMAP_HOST=
EMAIL_ARUBA_IMAP_PORT=993
EMAIL_ARUBA_SMTP_HOST=smtps.aruba.it
EMAIL_ARUBA_SMTP_PORT=465
EMAIL_ARUBA_SIGNATURE=
EMAIL_ARUBA_SIGNATURE_FILE=

EMAIL_GMAIL_ADDRESS=
EMAIL_GMAIL_PASSWORD=
EMAIL_GMAIL_IMAP_HOST=
EMAIL_GMAIL_IMAP_PORT=993
EMAIL_GMAIL_SMTP_HOST=smtp.gmail.com
EMAIL_GMAIL_SMTP_PORT=465
EMAIL_GMAIL_SIGNATURE=
EMAIL_GMAIL_SIGNATURE_FILE=

EMAIL_CONTACTS_FILE=
EMAIL_DAILY_CHECK_ENABLED=true
EMAIL_DAILY_CHECK_HOUR=9
EMAIL_DAILY_CHECK_MINUTE=0
EMAIL_DAILY_CHECK_PROVIDER=aruba
EMAIL_CLIENT_ALERTS_ENABLED=true
EMAIL_CLIENT_ALERTS_PROVIDER=aruba
EMAIL_CLIENT_ALERTS_LIMIT=20
EMAIL_CLIENT_ALERTS_MAX_PER_RUN=3
EMAIL_CLIENT_ALERTS_FILE=
```

## Variabili Importanti

| Variabile                         | Descrizione                                      |
| --------------------------------- | ------------------------------------------------ |
| TELEGRAM_TOKEN                    | Token del bot Telegram                           |
| YOUR_CHAT_ID                      | Utente Telegram autorizzato                      |
| GROQ_API_KEY                      | Chiave API Groq                                  |
| LLM_MODEL                         | Modello locale Ollama                            |
| PCLOUD_FOLDER_URL                 | Link PCloud pubblico di default per `/piercepcloud` |
| MEMORY_DIR                        | Directory locale della memoria episodica         |
| VAULT_PATH                        | Percorso del Vault Obsidian                      |
| CALENDAR_BACKEND                  | Backend calendario: `local` o `google`           |
| CALENDAR_EVENTS_FILE              | Path dello storage locale eventi JSON            |
| CALENDAR_ID                       | ID calendario Google, default `primary`          |
| CALENDAR_CREDENTIALS_FILE         | Path credenziali OAuth Google Calendar           |
| CALENDAR_TOKEN_FILE               | Path token OAuth dell'account autorizzato        |
| CALENDAR_DEFAULT_DURATION_MINUTES | Durata di default per nuovi eventi senza fine    |
| TASKS_CREDENTIALS_FILE            | Path credenziali OAuth Google Tasks              |
| TASKS_TOKEN_FILE                  | Path token OAuth Google Tasks                    |
| WEB_SEARCH_LOG_FILE               | Path log locale delle ricerche web               |
| EMAIL_ARUBA_ADDRESS               | Indirizzo email Aruba                            |
| EMAIL_ARUBA_PASSWORD              | Password o app password Aruba                    |
| EMAIL_ARUBA_IMAP_HOST             | Host IMAP Aruba                                  |
| EMAIL_ARUBA_IMAP_PORT             | Porta IMAP Aruba                                 |
| EMAIL_ARUBA_SMTP_HOST             | Host SMTP Aruba                                  |
| EMAIL_ARUBA_SMTP_PORT             | Porta SMTP Aruba                                 |
| EMAIL_ARUBA_SIGNATURE             | Firma testuale aggiunta agli invii SMTP Aruba    |
| EMAIL_ARUBA_SIGNATURE_FILE        | File con firma testuale per invii SMTP Aruba     |
| EMAIL_GMAIL_ADDRESS               | Indirizzo Gmail                                  |
| EMAIL_GMAIL_PASSWORD              | Password/app password Gmail                      |
| EMAIL_GMAIL_IMAP_HOST             | Host IMAP Gmail                                  |
| EMAIL_GMAIL_IMAP_PORT             | Porta IMAP Gmail                                 |
| EMAIL_GMAIL_SMTP_HOST             | Host SMTP Gmail                                  |
| EMAIL_GMAIL_SMTP_PORT             | Porta SMTP Gmail                                 |
| EMAIL_GMAIL_SIGNATURE             | Firma testuale aggiunta agli invii SMTP Gmail    |
| EMAIL_GMAIL_SIGNATURE_FILE        | File con firma testuale per invii SMTP Gmail     |
| EMAIL_CONTACTS_FILE               | Rubrica locale JSON per risoluzione contatti     |
| EMAIL_DAILY_CHECK_ENABLED         | Abilita check giornaliero email                  |
| EMAIL_DAILY_CHECK_HOUR            | Ora del check giornaliero                        |
| EMAIL_DAILY_CHECK_MINUTE          | Minuto del check giornaliero                     |
| EMAIL_DAILY_CHECK_PROVIDER        | Provider usato dal check giornaliero             |
| EMAIL_CLIENT_ALERTS_ENABLED       | Abilita alert Telegram per email cliente/lavoro  |
| EMAIL_CLIENT_ALERTS_PROVIDER      | Provider usato dagli alert cliente/lavoro        |
| EMAIL_CLIENT_ALERTS_LIMIT         | Numero email non lette controllate dagli alert   |
| EMAIL_CLIENT_ALERTS_MAX_PER_RUN   | Numero massimo di alert inviati a ogni cron      |
| EMAIL_CLIENT_ALERTS_FILE          | File locale per deduplicare gli alert già inviati |

Nota: le firme configurate nella webmail non vengono applicate automaticamente
agli invii SMTP. Per Aruba usa `EMAIL_ARUBA_SIGNATURE` oppure
`EMAIL_ARUBA_SIGNATURE_FILE`.

---

# Avvio del Bot

Esegui il bot dalla root del progetto:

```bash
python bot.py
```

Se configurato correttamente, il bot:

* si collegherà a Telegram
* inizializzerà i sistemi di memoria
* caricherà i database vettoriali
* avvierà i workflow di polling

---

# Comandi Telegram

## Input Testuale e Vocale

Il bot gestisce sia messaggi testuali sia messaggi vocali Telegram.

I vocali vengono scaricati temporaneamente in `/tmp`, trascritti da
`modules/audio/transcriber.py` tramite `faster-whisper`, poi reinseriti nella
stessa pipeline dei messaggi testuali.

Il modello configurato è `base`, eseguito su CPU con `compute_type="int8"`.
Al primo utilizzo il caricamento del modello può richiedere più tempo.

Flusso:

```text
vocale Telegram
 ↓
download temporaneo .ogg
 ↓
transcribe_audio()
 ↓
testo trascritto
 ↓
rispondi() / router esistente
```

Questo significa che un vocale può attivare gli stessi workflow del testo:

* calendario
* email
* task
* web
* note
* risposta LLM normale

Esempi:

```text
"Aggiungi evento domani studiare alle 15"
"Manda email a Mario oggetto riunione messaggio ci sentiamo domani"
"Riassumi le ultime email"
```

Se c'è un workflow pendente, anche un follow-up vocale può completarlo. Per
esempio, dopo una richiesta calendario senza orario, un vocale con "alle 15"
viene trattato come risposta contestuale.

## Comandi Principali

| Comando | Descrizione |
|---|---|
| /redazione | Genera o pianifica contenuti/articoli per il blog |
| /cmd | Esegue comandi terminale autorizzati |
| /aggiornanote | Aggiorna e sincronizza subito le note Obsidian |
| /clear | Pulisce il contesto conversazionale e la memoria breve |
| /vettorizza | Indicizza domini e contenuti tramite Internet Archive |
| /piercevector | Recupera e approfondisce memoria vettoriale temporanea |
| /piercepcloud | Analizza, riassume e traduce file/cartelle PCloud |
| /piercetelegram | Analizza e indicizza contenuti di canali Telegram |
| /web | Ricerca web con sintesi breve e fonti |
| /email | Workflow email con preview e conferma |
| /calendar | Gestione calendario ed eventi |
| /audit | Audit security controllato su target autorizzati |
| /security_osint | OSINT passivo su dominio |
| /security_person_osint | OSINT pubblico su persona/azienda |
| /security_audit | Alias audit tecnico controllato, default `recon` |
| /audit_allow | Gestione allowlist security da Telegram |
| /audit_watch | Monitor periodico dei target autorizzati |
| /security_watch | Alias di `/audit_watch` |
| /audit_history | Storico degli audit security |
| /real_audit | Avvio diretto di `real-audit` con conferma |
| /offensive_status | Stato del gate offensive |
| /offensive_enable | Abilita temporaneamente offensive safe mode per un target |
| /offensive_run | Esegue controlli offensivi safe su target abilitato |
| /offensive_explicit | Esegue controlli lab-only con conferma specifica |
| /offensive_disable | Disabilita offensive mode |
| /timeline | Consulta timeline cognitiva e storica del progetto |
| /operator | Attiva modalità operatore ultra sintetica; `/operator off` per disattivare |
| /annulla | Interrompe il workflow attivo |

---

## Esempi Rapidi

```text
/redazione articolo SEO WordPress per hotel
/cmd ls -la
/aggiornanote
/clear

/vettorizza example.com cybersecurity
/piercevector example.com
/piercepcloud
/piercetelegram

/email
/calendar domani
/audit dominio.it passive

/timeline semantic reranking
/operator on
```

## Workflow Cognitivi

Raptor distingue:

* retrieval semantico (`/piercevector`)
* ingestione conoscenza (`/vettorizza`)
* ingestione documentale (`/piercepcloud`)
* ingestione Telegram (`/piercetelegram`)
* generazione contenuti (`/redazione`)
* operazioni sistema (`/cmd`)
* sincronizzazione knowledge base (`/aggiornanote`)

Questo permette di mantenere separati:

* memoria
* retrieval
* automazione
* knowledge ingestion
* workflow operativi

## Ingestione PCloud

`/piercepcloud` legge link pubblici PCloud e apre un browser Telegram con
cartelle e file. I bottoni cartella navigano dentro il percorso selezionato; i
bottoni file leggono o analizzano il contenuto.

Uso con link configurato nel `.env`:

```text
/piercepcloud
```

Uso con uno o più link passati direttamente da Telegram:

```text
/piercepcloud https://e.pcloud.link/publink/show?code=...
/piercepcloud https://link-cartella-1 https://link-cartella-2
```

Se il link punta a una cartella pubblica, Raptor mostra prima il livello
corrente con cartelle e file. Entrando in una cartella aggiorna la tastiera
Telegram e mostra il contenuto di quel livello, con un bottone per tornare
indietro. I PDF trovati vengono letti e, se disponibile, analizzati con la
pipeline PDF CrewAI. Ogni livello mostra fino a 30 file per volta; se ci sono
altri file compare `➡️ Mostra altri` prima di `❌ Annulla`.

Per i link pubblici `pcloud.link` / `pcloud.com` con parametro `code`, il bot usa
l'API pubblica pCloud per leggere i metadata della cartella e risolve il link di
download solo quando scegli un file dalla tastiera Telegram.

Sono supportati:

* PDF
* file testuali (`.txt`, `.md`, `.csv`, `.json`, `.py`, `.log`, `.html`)
* cartelle pubbliche PCloud annidate

Il browser mostra anche altri file presenti nella cartella, ma l'analisi del
contenuto resta disponibile solo per i formati leggibili dal bot.

---

## Vettori e Retrieval

`/vettorizza` costruisce memoria: prende dominio, query Internet Archive e
keyword di routing, poi crea/aggiorna la collection ChromaDB e il registry in
`memory_core/memory_sources.py`.

`/piercevector` consulta memoria già costruita: selezioni una collection,
inserisci una query, il sistema recupera documenti da Chroma, li reranka e
mostra sorgenti e sintesi. Quando i metadata Chroma contengono identifier o URL
Internet Archive, prova anche un fetch live leggero: legge solo pochi file
testuali/PDF limitati, reranka chunk reali e li passa alla sintesi. Se non trova
contesto pertinente non genera una sintesi inventata. Se il retrieval Chroma
fallisce, lo dichiara e usa un fallback live da Internet Archive.

Il fetch live è progettato per non appesantire la VPS: preferisce `_djvu.txt`,
file testuali e HTML; usa PDF solo come fallback limitato; OCR disattivato di
default; download in directory temporanea senza persistenza dei testi completi.

La logica Internet Archive vive nel package `modules/archive/`. I vecchi file
`modules/archive_*.py` restano solo shim di compatibilità. La generazione degli
embedding vive in `modules/embeddings/manager.py`; `modules/embedding_manager.py`
è mantenuto come shim temporaneo.

Entrambi aggiornano il working state leggero con `memory` e `vector`.

---

## Gestione Email

Il modulo email vive in `modules/email/` ed è orchestrato da `handlers/email_handler.py`.

Supporta:

* provider `aruba` e `gmail`
* lettura email recenti
* lettura email non lette
* filtro email importanti
* ricerca testuale e semantica
* sintesi rapida
* invio email
* risposta a email recenti
* rubrica contatti locale

### Comandi e frasi supportate

```text
/email
/email a mario@example.com oggetto: Ciao messaggio: Ti scrivo per...
mostrami le email non lette
mostrami le ultime 5 email
cerca email fattura Aruba
email importanti
riassumi email
manda email a Mario oggetto: Riunione messaggio: Ci sentiamo domani
rispondi all'ultima email di Mario messaggio: Perfetto, grazie
```

### Preview obbligatoria

Le email non vengono mai inviate direttamente. Raptor crea una bozza e mostra una preview:

```text
📧 Anteprima email

A: Mario <mario@example.com>
Oggetto: Riunione

Messaggio:
Ci sentiamo domani

[✅ Invia] [✏️ Modifica] [❌ Annulla]
```

Stati temporanei principali:

* `waiting_recipient`
* `waiting_contact_confirmation`
* `waiting_subject`
* `waiting_body`
* `waiting_edit`
* `preview_ready`

### Firma SMTP

Le firme configurate nella webmail non vengono applicate automaticamente agli
invii via SMTP. Per questo Raptor può aggiungere una firma lato applicazione.

Configurazione inline:

```env
EMAIL_ARUBA_SIGNATURE=Nome Cognome\nTelefono\nSito web
```

Configurazione da file:

```env
EMAIL_ARUBA_SIGNATURE_FILE=/home/opc/assistente_ia/secrets/email_signature.txt
```

La firma può essere testuale o HTML. Se è HTML, l'email viene inviata come
`multipart/alternative` con:

* parte `text/plain`
* parte `text/html`

La preview Telegram mostra solo il testo del messaggio, non il codice HTML
della firma. Il corpo dell'email e la firma completa vengono comunque inviati.

### Rubrica Contatti

La rubrica locale è configurabile con:

```env
EMAIL_CONTACTS_FILE=/home/opc/assistente_ia/data/email_contacts.json
```

Formati supportati:

```json
{
  "Mario Rossi": "mario@example.com",
  "Laura": "laura@example.com"
}
```

Oppure:

```json
[
  {
    "name": "Mario Rossi",
    "email": "mario@example.com"
  }
]
```

### Check Giornaliero

Il check giornaliero legge le email non lette, filtra quelle importanti e invia un riepilogo Telegram.

```env
EMAIL_DAILY_CHECK_ENABLED=true
EMAIL_DAILY_CHECK_HOUR=9
EMAIL_DAILY_CHECK_MINUTE=0
EMAIL_DAILY_CHECK_PROVIDER=aruba
```

### Alert Cliente/Lavoro

Il cron di ingestione email controlla anche le email non lette e invia un
alert Telegram quando trova una possibile opportunità reale, per esempio:

* richiesta preventivo
* proposta di lavoro
* potenziale cliente
* richiesta informazioni
* progetto sito web

Sono esclusi esplicitamente rumori come LinkedIn e Tryber.

Configurazione:

```env
EMAIL_CLIENT_ALERTS_ENABLED=true
EMAIL_CLIENT_ALERTS_PROVIDER=aruba
EMAIL_CLIENT_ALERTS_LIMIT=20
EMAIL_CLIENT_ALERTS_MAX_PER_RUN=3
EMAIL_CLIENT_ALERTS_FILE=/home/opc/assistente_ia/data/email_client_alerts.json
```

Il file `EMAIL_CLIENT_ALERTS_FILE` mantiene gli ID già notificati, così lo
stesso messaggio non genera alert ripetuti.

La lettura delle email non lette usa `BODY.PEEK[]`, quindi non dovrebbe
marcarle come lette durante il controllo.

---

## Gestione Task

Il modulo task vive in `modules/tasks/` e usa Google Tasks come backend.

Azioni supportate:

* `list`
* `create`
* `complete`
* `delete`

### Frasi supportate

```text
mostra task
lista task
ricordami domani di pagare hosting
aggiungi task chiamare commercialista
completa task backup
elimina task commercialista
```

Il bot rileva anche task implicite senza crearle subito. Frasi come:

```text
devo migliorare workflow note
dovrei chiamare commercialista domani
più avanti sarebbe da sistemare task impliciti
todo: aggiornare README
```

generano una proposta `POSSIBLE_TASK_DETECTED confidence=...` con conferma
prima del salvataggio in Google Tasks.

Il parsing avviene in due passaggi:

1. parser LLM in `modules/tasks/parser_llm.py`
2. fallback locale in `modules/tasks/intent_router.py`

### Google Tasks

Il client è in:

```text
modules/tasks/client.py
```

Scope usato:

```text
https://www.googleapis.com/auth/tasks
```

Il client Google Tasks usa attualmente:

```text
secrets/tasks_credentials.json
secrets/tasks_token.json
```

Questi file devono restare locali e sono ignorati da Git.

---

## Ricerca Web

Il modulo web vive in `modules/web/` e viene usato solo quando la richiesta è esplicitamente orientata al web o richiede informazioni aggiornate.

### Comandi e frasi supportate

```text
/web documentazione aggiornata Google Tasks API
/search ultime novità Python 3.13
cerca sul web prezzi VPS ARM Oracle
verifica questa notizia online
trova fonti su Google Calendar API
riassumi https://example.com/articolo
```

La parola `verifica` attiva il modulo web quando viene usata come richiesta di
controllo o fact-check. Frasi descrittive come `si verifica un errore`,
invece, non vengono trattate come intent web e proseguono nel normale routing
conversazionale.

### Flusso

```text
utente
 ↓
chat_handler.py
 ↓
modules.web.intent
 ↓
modules.web.search
 ↓
modules.web.summarizer
 ↓
risposta Telegram con fonti
```

Le risposte includono sempre le fonti trovate. Se la sintesi LLM va in timeout, Raptor mostra comunque snippet e link dei risultati.

### Storage locale

Le ricerche vengono annotate in:

```text
data/web/search_log.json
```

Il log conserva solo query, azione e link principali. La directory `data/` resta ignorata da Git.

---

## Audit Security

Il modulo security vive in `modules/security/` ed esegue audit locali solo su
target proprietari o esplicitamente autorizzati. Il comando canonico è `/audit`;
la documentazione usa `/audit`, `/audit_*`, `/security_*`, `/real_audit` e
`/offensive_*`.

Con `/audit` senza argomenti il bot mostra l'uso corretto. I comandi Telegram
supportati sono:

```text
/audit
/audit dominio.it
/audit dominio.it passive
/audit dominio.it web-light
/audit dominio.it recon
/audit dominio.it network
/audit dominio.it full-audit
/audit dominio.it real-audit
/real_audit dominio.it
/security_audit dominio.it recon
/security_osint dominio.it
/security_person_osint "Nome Cognome"
/audit_history dominio.it
/audit_allow dominio.it
/audit_allow add dominio.it
/audit_allow list
/audit_allow remove dominio.it
/audit_watch dominio.it
/audit_watch dominio.it 6 recon
/audit_watch dominio.it 24 full-audit
/audit_watch list
/audit_watch off dominio.it
/security_watch dominio.it
/offensive_status
/offensive_enable dominio.it
/offensive_enable dominio.it 60
/offensive_run dominio.it safe
/offensive_explicit 192.168.1.10 masscan
/offensive_explicit 192.168.1.10 hydra
/offensive_explicit 192.168.1.10 all
/offensive_disable
```

### Policy e Modalità

La allowlist è composta da:

* target statici in `modules/security/policy.py`
* target dinamici aggiunti da Telegram in `data/security/allowed_targets.json`

I comandi `/audit_allow add`, `/audit_allow list` e `/audit_allow remove`
gestiscono solo la parte dinamica.

```text
modules/security/policy.py
data/security/allowed_targets.json
```

Prima di eseguire qualunque tool, il router verifica:

* allowlist del target con `is_allowed_target()`
* modalità automatica consentita con `require_safe_mode()`
* conferma obbligatoria per le modalità in `CONFIRMATION_REQUIRED_MODES`

Le modalità attualmente gestite sono:

```python
AUTO_SAFE_MODES = {
    "passive",
    "web-light",
    "recon",
    "network",
    "full-audit",
}

CONFIRMATION_REQUIRED_MODES = {
    "real-audit",
}
```

| Modalità    | Esecuzione | Tool principali                                      |
| ----------- | ---------- | ---------------------------------------------------- |
| passive     | automatica | httpx, whatweb, sslscan, nuclei                      |
| web-light   | automatica | httpx, whatweb, ffuf, nuclei                         |
| recon       | automatica | subfinder, amass passivo, dnsx, naabu, httpx, whatweb, gau, waybackurls |
| network     | automatica | nmap                                                 |
| full-audit  | automatica | recon + wafw00f, sslscan, katana, LinkFinder, SecretFinder, nuclei, ffuf, nmap |
| real-audit  | conferma   | full-audit + nuclei validation CVE/exposure/misconfig rate-limited e sqlmap safe check su URL idonee |

### OSINT Security

`/security_osint dominio.it` esegue raccolta OSINT passiva con fingerprinting
leggero. Normalizza dominio, subdomini pubblici, DNS record, IP pubblici,
tecnologie, CDN/WAF, email pubbliche, riferimenti GitHub, URL storiche e note
di rischio.

Lo stack locale usato quando disponibile include:

* `subfinder`, `amass -passive`, `dnsx`
* `theHarvester`
* `gau`, `waybackurls`
* `httpx`, `whatweb`, `wafw00f`

`/security_person_osint "Nome Cognome"` usa solo dati pubblici e username
candidati. Lo scopo è orientativo: profili, domini o email devono essere
verificati manualmente per evitare omonimie e falsi positivi. Lo stack locale
integrabile è `maigret` e `sherlock`; `holehe` resta disponibile come tool
OSINT specializzato su email, ma non viene eseguito automaticamente senza un
indirizzo esplicito.

### Offensive Safe Gate

Il modulo offensive vive in `modules/security/offensive_testing.py` ed è
spento di default. `/offensive_enable dominio.it [minuti]` aggiunge il target
alla allowlist dinamica, abilita un gate temporaneo e non esegue nessun test.

```text
/offensive_status
/offensive_enable dominio.it 60
/offensive_run dominio.it safe
/offensive_disable
```

`/offensive_run dominio.it safe` esegue solo controlli controllati:

* rate limit basso
* niente exploit distruttivi
* niente persistenza
* niente credential dumping
* niente accesso a dati
* niente brute force automatico

Lo stack automatico safe usa `httpx`, `whatweb`, `wafw00f`, `sslscan`, nuclei
validation rate-limited, `ffuf` leggero e `nmap --top-ports 100`. Tool come
`hydra` e `masscan` sono rilevati nello status, ma restano fuori dal safe run.

`/offensive_explicit` abilita una corsia separata con conferma Telegram
specifica e solo target lab/private:

```text
/offensive_explicit 192.168.1.10 masscan
/offensive_explicit 192.168.1.10 hydra
/offensive_explicit 192.168.1.10 all

# override opzionali
/offensive_explicit 192.168.1.10 masscan 22,80,443 100
/offensive_explicit lab.local hydra root /home/opc/wordlists/lab.txt
/offensive_explicit 192.168.1.10 all root /home/opc/wordlists/lab.txt 22,80 50
```

Guardrail explicit:

* richiede `/offensive_enable target` già attivo
* richiede pulsante Telegram `Conferma offensive explicit`
* accetta solo `localhost`, IP privati/link-local o domini `.local`, `.lan`,
  `.lab`, `.test`, `.internal`
* `masscan` usa default `22,80,443,8080,8443`, rate `100`, massimo `200` e massimo `100` porte
* `hydra` è limitato al wrapper SSH, default user `admin` e wordlist lab automatica
* le wordlist Hydra sono accettate solo sotto `/home/opc/wordlists` o `/tmp`
* target pubblici come `example.com` vengono bloccati anche se sono in allowlist

### Output e Report

Il router `modules/security/router.py` aggrega gli output, estrae finding e
tecnologie, calcola un rischio sintetico e costruisce un grafo JSON della
superficie d'attacco.

La superficie d'attacco normalizzata viene costruita da
`modules/security/attack_surface.py` fondendo output di `subfinder`, `naabu` e
`httpx` in una struttura per host:

```json
{
  "target": "example.com",
  "subdomains": [
    {
      "host": "dev.example.com",
      "ports": [80, 443],
      "technologies": ["nginx"],
      "risk": "MEDIUM",
      "findings": []
    }
  ]
}
```

I report vengono salvati in:

```text
reports/security/
```

Ogni audit produce:

* report Markdown leggibile
* report JSON con raw output, findings e metadata
* riepilogo Telegram con conteggio severity, risk e percorsi dei report

### Security Memory

Ogni audit viene anche memorizzato in:

```text
data/security/audit_memory.json
```

La memoria security conserva snapshot per target con:

* superficie d'attacco normalizzata
* finding normalizzati
* remediation generate
* risk context spiegabile
* mapping della Security Knowledge Base
* conteggi severity
* path del report Markdown/JSON

Prima di salvare un nuovo snapshot, Raptor lo confronta con l'ultimo audit dello
stesso target e produce un diff su:

* nuovi sottodomini
* porte nuove o rimosse per host
* tecnologie nuove o rimosse per host
* cambi di risk per host
* finding nuovi o non più rilevati

Il diff viene inserito nei metadata del report e nel riepilogo Telegram come
sezione `Security memory`.

La history è consultabile da Telegram con:

```text
/audit_history dominio.it
/audithistory dominio.it
```

Il comando mostra gli snapshot recenti con risk, numero host, numero finding e
le principali differenze rispetto all'audit precedente.

### Security Memory Semantica

Ogni snapshot salvato viene indicizzato anche in Chroma nella collection:

```text
security_memory_collection
```

L'indice semantico è costruito da `modules/security/semantic_index.py` e crea
documenti separati per:

* snapshot audit
* diff rispetto all'audit precedente
* host della superficie d'attacco
* finding
* remediation
* fattori del risk engine
* mapping della Knowledge Base

La collection viene registrata anche nel router della memoria AI, così query su
security memory, audit security, attack surface, risk context, remediation,
subdomini o porte esposte possono recuperare contesto direttamente da Chroma.
Il riepilogo Telegram indica quanti documenti sono stati indicizzati per audit.

### Remediation Engine

Il modulo `modules/security/remediation.py` genera remediation operative a
partire da finding e superficie d'attacco. La prima versione è rule-based e
contestuale:

* finding TLS/SSL -> hardening TLS, con istruzioni Cloudflare se rilevato
* WordPress/XML-RPC/wp-admin -> hardening WordPress
* porte ad alto rischio esposte -> suggerimenti firewall, VPN, allowlist e patching

Le remediation vengono incluse nei metadata del report e sintetizzate nel
riepilogo Telegram.

### Risk Engine Contestuale

Il risk finale viene calcolato da `modules/security/risk.py` combinando:

* severity dei finding
* porte ad alto rischio
* host `admin`/`dev` con servizi web esposti
* tecnologie rilevate, per esempio WordPress
* combinazioni contestuali come servizi high-risk + TLS debole

Il risultato include `risk_context` con fattori spiegabili e aggiorna anche il
risk dei singoli host nella superficie d'attacco.

### Security Watch

`/audit_watch` abilita monitor periodici local-first:

```text
/audit_watch dominio.it
/audit_watch dominio.it 6 recon
/audit_watch list
/audit_watch off dominio.it
```

Lo stato vive in:

```text
data/security/watch.json
```

Il JobQueue controlla ogni ora i watch dovuti. Quando un audit produce un diff
rilevante rispetto alla Security Memory, Raptor invia un alert Telegram con le
principali differenze e i path del report.

### Security Knowledge Base

`modules/security/knowledge_base.py` arricchisce finding e remediation con una
KB iniziale:

* TLS debole/deprecato -> MITRE `T1190`, hardening TLS
* WordPress/XML-RPC/wp-admin -> MITRE `T1190`, hardening WordPress
* servizi remoti/database esposti -> MITRE `T1021`, firewall/VPN/allowlist

I mapping KB vengono salvati nei report e mostrati nel riepilogo Telegram.

### Executive Report

Ogni audit genera anche report executive:

* HTML executive
* Markdown executive

I file vengono salvati accanto al report tecnico in `reports/security/` e
includono summary, risk context, tabella attack surface, remediation e mapping
KB. La scorciatoia:

```text
/audit dominio.it executive
```

esegue un audit safe `passive` e produce gli stessi report executive.

---

## Gestione Calendario

Il modulo calendario vive in `modules/calendar/` ed è separato da `modules/tasks/`.

La distinzione architetturale è:

* `tasks` -> cose da fare
* `calendar` -> blocchi temporali e appuntamenti
* `reminders` -> notifiche e promemoria
* `memory` -> contesto utile e preferenze

### Comandi e frasi supportate

```text
/calendar oggi
/calendar domani
/calendar settimana
aggiungi evento Riunione cliente domani alle 15 luogo: Google Meet
aggiungi evento calendario per domani: studiare
alle 15
aggiungi evento calendario per domani: studiare 15
sposta riunione di domani alle 16
cancella appuntamento dentista
ricordami evento riunione cliente
```

### Follow-up intelligenti

Se la richiesta calendario è incompleta, Raptor salva una bozza temporanea e
chiede solo il dato mancante.

Esempio:

```text
Utente: Aggiungi evento calendario per domani: studiare
Raptor: A che ora lo metto per "studiare" domani?
Utente: alle 15
Raptor: mostra preview evento studiare, domani, 15:00 - 16:00
```

Sono supportate risposte brevi:

```text
15
alle 15
ore 15
15:30
```

Durante una bozza calendario, `annulla`, `cancella` o `stop` interrompono il
workflow attivo.

### Conferme Telegram

Le azioni che modificano il calendario non vengono mai applicate direttamente.
Raptor mostra prima una preview:

```text
📅 Vuoi creare questo evento?

Titolo: Riunione cliente
Data: 12/05/2026
Ora: 15:00 - 16:00
Luogo: Google Meet

[✅ Conferma] [✏️ Modifica] [❌ Annulla]
```

Le azioni temporanee usate dal bot sono:

* `create_event`
* `update_event`
* `delete_event`
* `waiting_details`
* `waiting_edit`

### Storage Locale

Il backend predefinito è locale:

```env
CALENDAR_BACKEND=local
```

Gli eventi sono salvati in:

```text
data/calendar/events.json
```

Ogni evento mantiene i campi principali:

```text
id
title
start_datetime
end_datetime
location
description
attendees
source
external_id
created_at
updated_at
```

### Google Calendar

Il client Google è isolato in:

```text
modules/calendar/client.py
```

Per abilitare Google Calendar:

1. Crea le credenziali OAuth per l'app Google.
2. Salva il file in `secrets/google_calendar_credentials.json`.
3. Installa le dipendenze con `pip install -r requirements.txt`.
4. Genera il token:

```bash
python scripts/google_calendar_auth.py
```

5. Imposta il backend:

```env
CALENDAR_BACKEND=google
CALENDAR_ID=primary
CALENDAR_CREDENTIALS_FILE=/home/opc/assistente_ia/secrets/google_calendar_credentials.json
CALENDAR_TOKEN_FILE=/home/opc/assistente_ia/secrets/google_calendar_token.json
```

Scope usato:

```text
https://www.googleapis.com/auth/calendar.events
```

`credentials.json` e `token.json` non devono mai essere committati.

---

## Integrazione Obsidian

Il modulo `modules.notes.service` supporta:

* creazione di note Markdown
* ricerca semantica nelle note
* lettura completa del vault
* sincronizzazione Git
* generazione di contesto
* routing basato sull'analisi dell'intento

L'integrazione con Obsidian è progettata per funzionare insieme a plugin di terze parti, in particolare:

* plugin Obsidian Git
* sincronizzazione automatica del vault
* versionamento delle note
* backup Git distribuiti
* workflow knowledge-base local-first

Questo consente a Raptor di utilizzare il vault Obsidian come memoria persistente e knowledge base sincronizzabile tra dispositivi e repository Git.

## Funzioni Principali

```python
write_note(title, content)
search_obsidian(query)
get_all_notes_content()
sync_to_github()
handle_note_intent(user_text)
```


---

# Architettura della Memoria

Raptor implementa un sistema gerarchico di memoria cognitiva.

## Memoria Episodica

Memorizza:

* conversazioni
* workflow
* eventi operativi
* interazioni contestuali

File utilizzati:

* memoria 24h
* memoria settimanale
* memoria mensile
* memoria annuale
* memoria permanente

Nel progetto la memoria episodica live sta in:

```text
memory/
```

I file runtime reali sono ignorati da Git. Nel repository restano solo template vuoti `.example.md`, utili per mostrare la struttura senza pubblicare contenuti personali.

## Memoria Semantica

Basata su:

* ChromaDB
* embeddings
* retrieval vettoriale
* pipeline di reranking

## Memoria dei Workflow

Traccia:

* operazioni di retrieval
* workflow di ingestione
* analisi CrewAI
* operazioni vettoriali
* eventi semantici

## Stato Operativo

Lo stato operativo vive in:

```text
state/current.json
```

Schema minimale:

```json
{
  "current_focus": null,
  "active_project": "raptor",
  "active_modules": [],
  "last_action": null,
  "updated_at": null
}
```

Il manager è in:

```text
state/manager.py
```

Funzioni principali:

```python
load_state()
save_state(data)
```

Questo livello non è:

* memoria episodica
* task manager
* knowledge base
* database semantico

È uno snapshot operativo attuale, utile per continuità, routing e recap dopo
restart.

Il working state viene aggiornato automaticamente in modo leggero durante il
routing principale. Non salva cronologie lunghe: mantiene solo focus corrente,
moduli attivi, ultima azione compatta e timestamp.

Il system prompt include:

* identity caricata da `identity.loader`
* ora locale corrente
* timestamp ISO locale
* contenuto di `state/current.json`

La timezone è centralizzata in:

```text
core/datetime_utils.py
```

Timezone attuale:

```text
Europe/Rome
```

---

# Storage ChromaDB

Il database vettoriale locale è salvato in:

```text
data/chroma_db/
```

Raptor utilizza collezioni persistenti ChromaDB per:

* retrieval semantico
* memoria dei domini
* storage vettoriale a lungo termine

---

# Script Utili

## Script Disponibili

| Script                           | Descrizione                          |
| -------------------------------- | ------------------------------------ |
| sync_notes.sh                    | Sincronizza le note Obsidian con Git |
| scripts/email_ingest_runner.py   | Indicizza email recenti e invia alert cliente/lavoro |
| scripts/rebuild_vector_memory.py | Ricostruisce la memoria vettoriale   |
| scripts/memory_matcher.py        | Utility di matching della memoria    |
| scripts/ingest_book.py           | Ingestione libri/testi               |
| scripts/ingest_git_timeline.py   | Indicizza eventi Git nella timeline  |
| scripts/google_calendar_auth.py  | Genera token OAuth Google Calendar   |

---

# Automazioni Cron

Cron attivi consigliati/attualmente usati:

```cron
0 3 * * * /home/opc/assistente_ia/sync_notes.sh

*/15 * * * * cd /home/opc/assistente_ia && /home/opc/assistente_ia/venv_crew/bin/python scripts/email_ingest_runner.py >> logs/email_ingest.log 2>&1
```

Il primo cron gira ogni giorno alle 03:00 e sincronizza `privatebrain/` con
Git tramite `git pull`. Il log viene scritto in:

```text
logs/sync_notes.log
```

Il secondo cron gira ogni 15 minuti e:

* legge le ultime email
* deduplica tramite hash
* genera embeddings
* salva le email nella memoria semantica con `source: email`
* controlla le email non lette per possibili opportunità cliente/lavoro
* invia alert Telegram quando necessario

Il log viene scritto in:

```text
logs/email_ingest.log
```

Il check giornaliero email interno al bot usa invece `JobQueue` di
`python-telegram-bot` e viene schedulato con timezone `Europe/Rome`.

---

# Directory Principali

| Directory         | Scopo                                  |
| ----------------- | -------------------------------------- |
| core/             | Configurazione e utility core          |
| handlers/         | Handler Telegram                       |
| internal/         | Workflow e logica interna              |
| memory/           | Memoria episodica locale               |
| memory_core/      | Motore memoria e semantica             |
| modules/          | Componenti AI modulari                 |
| modules/archive/  | Client, ingest e retrieval Internet Archive |
| modules/audio/    | Trascrizione vocali Telegram           |
| modules/email/    | Lettura, ricerca, invio e alert email  |
| modules/embeddings/ | Manager embedding condiviso           |
| modules/calendar/ | Eventi calendario locale/Google        |
| modules/notes/    | Servizi note Obsidian                  |
| modules/security/ | Audit security controllati e report    |
| modules/web/      | Ricerca web con fonti                  |
| state/            | Snapshot operativo attuale             |
| privatebrain/     | Vault Markdown privato                 |
| data/             | Dati persistenti locali                |
| scripts/          | Script di utilità                      |

---

# Note di Sicurezza

## Importante

Non pubblicare mai:

* `.env`
* sessioni Telegram
* database vettoriali
* note private
* file memoria
* chiavi API
* password o app password email
* credenziali OAuth Google
* token OAuth Google
* report security generati in `reports/security/`

---

# `.gitignore` Consigliato

```gitignore
.env
.env.*
credentials.json
token.json
tasks_credentials.json
tasks_token.json
secrets/credentials.json
secrets/token.json
secrets/tasks_credentials.json
secrets/tasks_token.json
secrets/google_calendar_credentials.json
secrets/google_calendar_token.json
venv/
venv_crew/
.venv/

__pycache__/
*.pyc
*.log

*.db
*.sqlite
*.sqlite3
*.sqlite-shm
*.sqlite-wal

data/
reports/security/
memory/*
!memory/
!memory/README.md
!memory/*.example.md
cache/

data/chroma_db/
chroma_db/
chroma/

privatebrain/*
!privatebrain/
!privatebrain/README.md
obsidian_notes/

*.session
```

---

# Stato Attuale

Raptor è attualmente in sviluppo attivo, lo uso come assistente personale e lo costruisco in base alle mie esigenze.

Architettura, sistemi di memoria, API e workflow possono evolvere rapidamente man mano che il progetto si espande verso un framework cognitivo AI più avanzato.

---


## Timeline Cognitiva

Raptor mantiene una timeline SQLite leggera in `data/timeline.sqlite`.

Registra eventi compatti da memoria episodica, workflow, note, task e commit Git,
senza indicizzare contenuti pesanti o appesantire la VPS.

Query supportate:

* `/timeline`
* `/timeline semantic reranking`
* `quando abbiamo introdotto semantic reranking?`
* `fammi vedere evoluzione email module`

Import Git opzionale:

```bash
python scripts/ingest_git_timeline.py --limit 100
```

## Modalità Operatore

`/operator` attiva output ultra sintetico:

```text
✔ operator ON
max_tokens=200
```

Comandi:

* `/operator` oppure `/operator on`
* `/operator off`
* `/operator status`

In questa modalita la chat usa un prompt operativo, il motore LLM riceve un
limite di token e gli output senza bottoni vengono compattati in stato/azione.
Le preview con conferma restano estese per sicurezza.

## Annulla Globale

`annulla`, `Annulla` e `/annulla` fermano gli stati operativi correnti:

* bozze email
* preview calendario
* modifica/cancellazione note
* suggerimenti task
* workflow `/vettorizza`, `/piercevector`, `/piercetelegram`
* selezioni pCloud/Telegram in corso

La modalita `/operator` non viene disattivata da `annulla`; si spegne solo con
`/operator off`.


## Stato Attuale
#Completato
routing multi-provider
fallback AI resiliente
cooldown provider automatico
memoria semantica
timeline cognitiva
Telegram assistant
CrewAI integration
Obsidian integration
calendar + tasks
retrieval web
archive ingestion

#In Evoluzione
cognitive routing
provider balancing
reasoning persistence
multi-agent orchestration
vector intelligence
memory ranking
security workflows
domain specialization

## Funzionalità in valutazione: le cose cambiano

* [ ] Supporto Qdrant e migliore gestione dei dati esterni
* [ ] Dashboard web ???
* [ ] Supporto multi-utente ???
* [ ] Command and control sistemi esterni

---

# Stack Tecnologico

## AI

* Groq
* Ollama
* CrewAI
* faster-whisper

## Memoria e Retrieval

* ChromaDB
* Embeddings
* Reranking semantico

## Infrastruttura

* Python
* Telegram Bot API
* AsyncIO
* Google Calendar API
* Vault Markdown
* Storage persistente locale
* JobQueue Telegram per schedulazioni interne
* Cron Linux per automazioni periodiche

---

# Filosofia

Raptor è progettato come:

* un assistente cognitivo personale
* un layer operativo AI modulare
* un sistema di memoria a lungo termine
* un motore semantico della conoscenza

L'architettura privilegia:

* modularità
* estendibilità
* persistenza local-first
* cognizione semantica
* componibilità dei workflow

---

# Disclaimer

Questo progetto è pensato per ricerca, sperimentazione e automazione personale di workflow AI.

Utilizzalo responsabilmente e proteggi:

* chiavi API
* knowledge base personali
* memorie vettoriali
* conversazioni private
* storage locali
