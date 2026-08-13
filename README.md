# Raptor

![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)

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
* menu cognitivo Telegram generato da registry semantico
* integrazione Obsidian Vault
* gestione calendario local-first con preview e conferma
* stato operativo persistente minimale
* audit security controllati su target autorizzati
* Raven integrato per breach check, IOC enrichment e monitoraggio passivo
* ingestione documentale e pipeline di conoscenza
* package dedicati per archivi Internet Archive ed embeddings
* routing intelligente tra modelli AI
* architettura estendibile e multi-workflow

Il progetto utilizza:

* Groq
* Cerebras
* OpenRouter
* NVIDIA NIM
* Ollama
* ChromaDB
* CrewAI
* Telegram Bot API
* Google Calendar API e Google Task API
* Vault Markdown Obsidian
* Have I Been Pwned e provider community abuse.ch

---

# Funzionalità

## Core AI

* Routing ibrido dei modelli LLM (Groq + Cerebras + OpenRouter + NVIDIA + Ollama)
* Ragionamento avanzato con CrewAI
* Pipeline di reranking cognitivo
* Workflow AI modulari
* Motore di retrieval semantico
* System prompt arricchito con identity, orario locale, timeline cognitiva e stato operativo

Routing AI Multi-Provider

Pipeline AI resiliente:

Groq
 ↓
Cerebras
 ↓
OpenRouter
 ↓
NVIDIA NIM
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
* Menu guidato Raptor OS con categorie, breadcrumb e quick actions
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

## Ricerca Memoria

* Menu guidato `🧠 Conoscenza > 🔎 Ricerca Memoria`
* Filtri MVP: ovunque, note, timeline e storage
* Output spiegabile con fonte, collection, rilevanza, estratto e motivo del match
* Comandi rapidi: `/memoria provider fallback`, `/memoria note Ragnir`, `/memoria timeline Cloud Vault`, `/memoria storage report`

### Cloud Vault

Cloud Vault espone nell'interfaccia i due remoti attivi (`pcloud`, `gdrive`),
con ricerca e apertura dei contenuti solo on-demand.

* UX: `/storage last`, `page 2`, `next`, `prev`, `open next`, `summarize next`
* Policy: badge dimensione/rischio, Info sempre disponibile, sample da pulsante e force solo esplicito
* Deep ingest: `/storage summarize-range 3 1-10`, `/storage ingest-range 3 1-20`
* Job: `/storage queue-ingest 3`, `/storage jobs`, `/storage job <id>`, `/storage cancel-job <id>`
* Memoria: `/storage link 3 project Raptor`, `/storage insights 3`, `/storage related Raptor`
* Arricchimento: `/storage extract-tags 3`, `/storage extract-entities 3`

Configurazione remoti e policy: `.env.storage.example`. Il servizio Google
Drive pronto per il deploy è in `deploy/raptor-rclone-gdrive.service`.

## Redazione e SEO

* Redazione guidata con `/scriviarticolo` e alias `/redazione`
* Tool SEO leggero con `/seo`, integrato nel menu `✍️ Redazione`
* Keyword clustering semplice per intento di ricerca
* Generazione di title SEO, meta description e slug consigliato
* Brief SEO automatico con H1, struttura H2, FAQ e linee guida editoriali
* SEO report analyzer semplice con score, segnali OK, criticità e azioni consigliate
* SEO URL analyzer con `/seo url`, fetch limitato e parsing di title, meta, H1, H2, testo e slug
* Menu guidato `✍️ Redazione > 🔍 SEO` con flow per cluster, snippet, brief, audit testo e audit URL
* Alias rapidi: `/seobrief` per brief automatico e `/seoreport` per analisi report/testo

## Social publishing

* Dashboard Telegram `/socialpost`
* Account Meta configurabili senza salvare token nel database
* Pubblicazione su pagine Facebook e profili Instagram Business
* Supporto a Page Access Token e token Meta System User autorizzati
* Immagini locali o URL HTTP/HTTPS; copia opzionale verso una directory pubblica
* Pubblicazione immediata o programmata con coda SQLite
* Import bulk da ZIP
* Stati `scheduled`, `publishing`, `published`, `partial` e `failed`
* Notifica Telegram con ID remoti o dettaglio degli errori

Instagram richiede un URL HTTPS pubblicamente raggiungibile per l'immagine.

## Newsletter

* Dashboard Telegram `/newsletter`
* Liste e contatti persistenti con deduplica per email
* Inserimento manuale e import CSV
* Preview e modifica prima dell'invio
* Invio immediato o programmato tramite la coda email esistente
* Invii individuali equivalenti a BCC, tracciati come run newsletter

## Riassunti

* Menu guidato `📅 Produttività > 📚 Riassunti`
* Sorgenti MVP: testo incollato, note recenti e pagina web da URL
* Stili disponibili: breve, operativo, executive
* Salvataggio automatico degli ultimi riassunti e memoria episodica
* Comandi rapidi: `/summary text operativo ...`, `/summary notes breve`, `/summary web executive https://...`, `/summary last`

## Audit Security

* Comando Telegram `/audit`
* OSINT passivo dominio con `/security_osint`
* OSINT pubblico persona/azienda con `/osintpersona` (`/security_person_osint` resta alias)
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

## Raven Threat Intelligence

* Modulo difensivo integrato direttamente in Raptor, con worker HTTP remoto opzionale
* Breach check email tramite Have I Been Pwned
* Controllo password con HIBP Pwned Passwords e k-anonymity
* Ricerca passiva di username, domini, persone e aziende
* Exact-match IOC enrichment tramite ThreatFox
* Controllo URL, host e payload metadata tramite URLhaus
* Metadata hash tramite MalwareBazaar, senza download di sample
* Ricerca su indici dark-web pubblici senza visitare servizi onion
* Monitor periodici persistenti con alert Telegram solo sulle variazioni
* Storico locale SQLite con target email mascherati e permessi `0600`

Documentazione completa: [`modules/raven/README.md`](modules/raven/README.md).

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

Il token condiviso con Ragnir viene letto da
`RAGNIR_ENV_PATH=/home/opc/ragnir/.env`, così non deve essere duplicato nel
file `.env` di Raptor.

## Esempio `.env`

```env
TELEGRAM_TOKEN=
YOUR_CHAT_ID=
GROQ_API_KEY=
OPENROUTER_API_KEY=
MODEL_OPENROUTER=openrouter/free
NVIDIA_API_KEY=
MODEL_NVIDIA=nvidia/llama-3.3-nemotron-super-49b-v1

LLM_MODEL=llama3

PCLOUD_FOLDER_URL=

RAGNIR_BASE_URL=
RAGNIR_API_TOKEN=

RAVEN_BASE_URL=
RAVEN_API_TOKEN=
HIBP_API_KEY=
RAVEN_ABUSECH_AUTH_KEY=
RAVEN_DB_PATH=/home/opc/assistente_ia/data/raven.sqlite
RAVEN_DARKWEB_API_KEY=
RAVEN_DARKWEB_INDEX_ENABLED=true
RAVEN_MONITOR_INTERVAL_SECONDS=3600

SOCIAL_DB_PATH=/home/opc/assistente_ia/data/social.sqlite
SOCIAL_MEDIA_DIR=/home/opc/assistente_ia/data/social_media
SOCIAL_PUBLIC_MEDIA_BASE_URL=
SOCIAL_PUBLIC_MEDIA_UPLOAD_DIR=
SOCIAL_GRAPH_API_VERSION=v24.0
SOCIAL_SCHEDULER_ENABLED=true
SOCIAL_SCHEDULER_INTERVAL_SECONDS=60

MEMORY_DIR=/home/opc/assistente_ia/memory
VAULT_PATH=/home/opc/assistente_ia/privatebrain

OLLAMA_BASE_URL=http://localhost:11434
MODEL_LOCAL=llama3.2:3b

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
EMAIL_SCHEDULER_ENABLED=true
EMAIL_SCHEDULER_DB_PATH=/home/opc/assistente_ia/data/email_scheduler.sqlite
EMAIL_SCHEDULER_INTERVAL_SECONDS=30
EMAIL_SCHEDULER_BATCH_SIZE=10
EMAIL_CAMPAIGN_MAX_RECIPIENTS=150
EMAIL_CAMPAIGN_AI_ENABLED=true
EMAIL_CAMPAIGN_AI_BATCH_SIZE=8
EMAIL_CAMPAIGN_MAX_CONSECUTIVE_FAILURES=3
EMAIL_FOLLOWUP_REPLY_CHECK_ENABLED=true
EMAIL_FOLLOWUP_REPLY_CHECK_INTERVAL_SECONDS=900
```

## Modalità privacy locale

`/privacy` (alias `/privato`, `/locale`, `/local`) apre il selettore dei
modelli locali. Sono configurati `gemma4:e2b` (Gemma 4 E2B) e
`llama3.2:3b`; la stessa scelta è disponibile in Utilità → Provider AI.

Quando la modalità privacy è attiva, il router e i workflow CrewAI bloccano
Groq, Cerebras, OpenRouter e NVIDIA. Se Ollama locale non risponde, la
richiesta fallisce senza fallback cloud. Stato e modello selezionato sono
persistiti in `data/privacy_mode.json` (runtime non versionato).

```text
/privacy
/privacy on gemma
/privacy on llama
/privacy off
```

## Variabili Importanti

| Variabile                         | Descrizione                                      |
| --------------------------------- | ------------------------------------------------ |
| TELEGRAM_TOKEN                    | Token del bot Telegram                           |
| YOUR_CHAT_ID                      | Utente Telegram autorizzato                      |
| GROQ_API_KEY                      | Chiave API Groq                                  |
| OPENROUTER_API_KEY                | Chiave del fallback OpenRouter                   |
| MODEL_OPENROUTER                  | Modello OpenRouter, default `openrouter/free`    |
| NVIDIA_API_KEY                    | Chiave del fallback NVIDIA NIM                   |
| MODEL_NVIDIA                      | Modello NVIDIA NIM                               |
| MODEL_LOCAL                       | Modello Ollama usato dal fallback locale         |
| PCLOUD_FOLDER_URL                 | Link PCloud pubblico di default per `/ricercafile` (`/piercepcloud` alias) |
| RAGNIR_BASE_URL                   | Endpoint HTTP del worker remoto Ragnir          |
| RAGNIR_API_TOKEN                  | Token opzionale per autenticare Ragnir          |
| RAVEN_BASE_URL                    | Endpoint opzionale del worker Raven; vuoto usa il servizio locale |
| RAVEN_API_TOKEN                   | Token opzionale per autenticare il worker Raven remoto |
| HIBP_API_KEY                      | Chiave HIBP per verifiche email; password non la richiede |
| RAVEN_ABUSECH_AUTH_KEY            | Auth-Key community abuse.ch per ThreatFox, URLhaus e MalwareBazaar |
| RAVEN_DB_PATH                     | Database SQLite di check e monitor Raven         |
| RAVEN_DARKWEB_API_KEY             | Token opzionale dell'indice dark-web passivo     |
| RAVEN_DARKWEB_INDEX_ENABLED       | Abilita ricerca passiva senza visitare siti onion |
| RAVEN_MONITOR_INTERVAL_SECONDS    | Frequenza worker monitor, minimo 900 secondi      |
| SOCIAL_DB_PATH                    | Database SQLite per account e coda social         |
| SOCIAL_MEDIA_DIR                  | Directory locale dei media social                 |
| SOCIAL_PUBLIC_MEDIA_BASE_URL      | Base URL HTTPS dei media destinati a Instagram    |
| SOCIAL_PUBLIC_MEDIA_UPLOAD_DIR    | Directory locale esposta dalla base URL pubblica  |
| SOCIAL_GRAPH_API_VERSION          | Versione Meta Graph API, default `v24.0`          |
| SOCIAL_SCHEDULER_ENABLED          | Abilita il worker della coda social               |
| SOCIAL_SCHEDULER_INTERVAL_SECONDS | Intervallo coda social, minimo 15 secondi          |
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
| EMAIL_SCHEDULER_ENABLED           | Abilita la coda persistente per gli invii programmati |
| EMAIL_SCHEDULER_DB_PATH           | Database SQLite della coda email                  |
| EMAIL_SCHEDULER_INTERVAL_SECONDS  | Frequenza di controllo della coda                 |
| EMAIL_SCHEDULER_BATCH_SIZE        | Invii massimi reclamati per ciclo; base per campagne future |
| EMAIL_CAMPAIGN_MAX_RECIPIENTS     | Limite hard di destinatari importabili per campagna |
| EMAIL_CAMPAIGN_AI_ENABLED         | Abilita personalizzazione AI con fallback deterministico |
| EMAIL_CAMPAIGN_AI_BATCH_SIZE      | Contatti elaborati per batch di personalizzazione |
| EMAIL_CAMPAIGN_MAX_CONSECUTIVE_FAILURES | Errori consecutivi prima della pausa automatica |
| EMAIL_FOLLOWUP_REPLY_CHECK_ENABLED | Annulla follow-up quando trova una risposta nello stesso thread |
| EMAIL_FOLLOWUP_REPLY_CHECK_INTERVAL_SECONDS | Frequenza del controllo IMAP dei follow-up |

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

## Menu Cognitivo Raptor OS

Raptor mantiene il linguaggio naturale come interfaccia primaria, ma aggiunge
una navigazione guidata per discovery, onboarding e shortcut operativi.

Le tre modalità convivono:

* linguaggio naturale: `fai osint su example.com`
* slash command: `/auditdominio example.com`
* menu guidato: `🛡 Sicurezza > 🌐 Audit Dominio > inserisci target`

Il menu non sostituisce il router naturale. Quando un pulsante richiede input,
Raptor salva uno stato contestuale temporaneo e interpreta il messaggio
successivo come input del comando scelto.

Home menu:

```text
🦖 Raptor OS

🛡 Sicurezza
🧠 Conoscenza
⚙️ Utilità
📅 Produttività
✍️ Redazione
⚡ Ragnir
🐦 Raven
```

Ogni schermata usa breadcrumb, per esempio:

```text
Home > 🛡 Sicurezza
Home > ⚙️ Utilità > 📜 Logs
Home > ⚡ Ragnir > 🌐 Gestione siti
Home > 🐦 Raven
```

Le quick actions globali sono:

* `🏠 Home`
* `⏪ Back`
* `❌ Stop`
* `🧹 Clear`

Il registry centrale vive in `core/menu_registry.py` e descrive comandi,
alias, label utente, categoria, stato feature, placeholder input e descrizioni.
Da questa struttura si possono generare menu Telegram, help automatico,
capability map, futura Web UI e routing AI-aware.

Le feature future sono visibili come `[Coming Soon]` e rispondono con una
roadmap sintetica invece di generare errori o pulsanti rotti.

### Utilità

La sezione `⚙️ Utilità` raccoglie diagnostica, stato sistema e strumenti
operativi non specifici di Ragnir.

```text
⚙️ Utilità

💻 Terminale
📝 Aggiorna Note
🧠 Operatore
📊 Stato Sistema
⚙️ Runtime
🧠 Stato Memoria
🔄 Workflow Attivi
🤖 Provider AI
🧰 Tool Locali
📡 Sessioni
📜 Logs
🧹 Clear
❌ Annulla
```

Questa sezione contiene la diagnostica generale di Raptor:

* runtime e risorse
* stato memoria
* workflow attivi
* provider AI e fallback
* tool locali installati
* sessione corrente
* log applicativi recenti

### Ragnir

Ragnir è il nodo operativo leggero collegato a Raptor. Raptor mantiene
orchestrazione, memoria, UX Telegram e reasoning; Ragnir esegue operazioni
remote su repo, browser, screenshot, patch e publish.

Ragnir non è pensato come hosting, build server pesante o storage persistente:
GitHub resta la sorgente ufficiale del codice e Cloudflare Pages gestisce
pubblicazione/build pubblico dei siti.

Menu Ragnir:

```text
⚡ Ragnir

🌐 Gestione siti
📝 Modifiche sito
📸 Anteprima e controlli
🚀 Pubblicazione
🛠 Operazioni tecniche
🏠 Home
```

#### Registro siti Ragnir

Ragnir usa il registro siti in `modules/ragnir/sites.py`. Il primo sito
configurato è Offfice.it:

```text
slug: offfice-it
repo: offfice-it
url: https://offfice-it.pages.dev/
file principale: public/index.html
pagina principale: home
```

Azioni sito-specifiche usate dai sottomenu:

```text
🌐 Lista siti
ℹ️ Info sito
🩺 Check sito
📸 Screenshot sito
✏️ Modifica sito
🚀 Pubblica sito
```

Comandi collegati:

```text
/ragnir sites
/ragnir site-info offfice
/ragnir check-site offfice
/ragnir screenshot-page offfice home
/ragnir edit-site offfice <istruzione>
/ragnir edit-page offfice home <istruzione>
/ragnir publish-site offfice "messaggio commit"
```

#### Ragnir > Gestione siti

`🌐 Gestione siti` contiene shortcut di gestione multi-sito:

```text
🌐 Lista siti
➕ Aggiungi sito
ℹ️ Info sito
📦 Stato repo
🕓 Ultima modifica
↩️ Ripristina ultima modifica
🌐 Configura URL pubblico
✅ Abilita publish
```

Le azioni sito-specifiche aprono prima una selezione sito, poi richiamano i
callback Ragnir esistenti.

In `🛠 Operazioni tecniche`, `☁️ Cloudflare Agent` mostra lo stato delle
Cloudflare Skills, dei cinque MCP ufficiali e delle credenziali API usate da
Ragnir. Offre collegamenti diretti a Dashboard, Pages, API Tokens e alla guida
Agent Setup; i token non vengono mai raccolti tramite Telegram.

`➕ Aggiungi sito` offre due percorsi: collegare un repository GitHub già
esistente oppure creare un nuovo sito statico. Nel secondo percorso si può
incollare HTML/JSON (anche come documento Telegram) o descrivere il sito in
linguaggio naturale. Raptor prepara e mostra l'anteprima; soltanto la conferma
esplicita delega a Ragnir la creazione del repository pubblico, il push
iniziale e il progetto Cloudflare Pages `*.pages.dev` con deploy automatico.

Flusso tipico:

```text
Modifiche sito / Anteprima e controlli / Pubblicazione
 ↓
scelta azione
 ↓
scelta sito
 ↓
preview o operazione Ragnir
 ↓
eventuale conferma
```

Le modifiche ai siti sono protette da preview, conferma e backup. I file
modificabili sono limitati da `safe_edit_files` in `sites.py`; i file protetti,
i path pericolosi e i path fuori whitelist vengono bloccati.

#### Ragnir > Ultima attività

`🧭 Ultima attività` richiama:

```text
/ragnir last
```

Mostra ultimo job, repo, sito, URL pubblico, request id, stato e bottoni rapidi.

#### Ragnir > Operazioni tecniche

`🛠️ Operazioni tecniche` contiene gli strumenti grezzi/manuali del worker
Ragnir, utili per debug personale e interventi diretti:

```text
🌐 Fetch URL
📸 Screenshot URL
📡 Status Ragnir
🧹 Cleanup temp
📦 Repo status manuale
```

Comandi collegati:

```text
/ragnir fetch <url>
/ragnir screenshot <url>
/ragnir status
/ragnir cleanup
/ragnir repo <repo>
```

### Raven Exposure Monitoring

Raven è il modulo difensivo funzionante di Raptor per breach check, threat
intelligence e monitoraggio passivo. Se `RAVEN_BASE_URL` è vuoto, il client
esegue `RavenService` direttamente nello stesso processo di Raptor; se è
configurato, invia lo stesso contratto job a un worker Raven HTTP remoto.

Provider attivi:

* **HIBP Pwned Passwords:** sempre disponibile, usa k-anonymity e invia solo i
  primi cinque caratteri dello SHA-1; password, hash completo e prefisso non
  vengono salvati
* **HIBP email:** usa `HIBP_API_KEY`; senza chiave reale accetta esclusivamente
  gli account ufficiali `@hibp-integration-tests.com`
* **HIBP breach catalogue:** controllo pubblico dei breach organizzativi per
  dominio; gli account verificati del dominio richiedono chiave e permessi HIBP
* **ThreatFox:** exact-match per IOC, domini, IP, URL e hash
* **URLhaus:** lookup read-only di URL, host/IP e metadata MD5/SHA-256
* **MalwareBazaar:** metadata per hash MD5/SHA-1/SHA-256, senza scaricare sample
* **Ahmia / indice configurato:** sole menzioni passive e non verificate, senza
  connessione diretta a siti onion

ThreatFox, URLhaus e MalwareBazaar condividono la Auth-Key gratuita abuse.ch
configurata in `RAVEN_ABUSECH_AUTH_KEY`. Lo status mostra per ogni provider se
è configurato, disponibile o limitato.

Raven salva check, digest e monitor in `data/raven.sqlite` con permessi `0600`.
Il JobQueue di Raptor esegue periodicamente i monitor dovuti e invia un alert
Telegram soltanto quando un target già inizializzato cambia. L'intervallo del
runner non può essere inferiore a 900 secondi; ogni monitor mantiene anche il
proprio intervallo in ore.

```text
🐦 Raven

📡 Status Raven
📧 Verifica email
🔐 Verifica password
👤 Verifica username
🌐 Verifica dominio
🏢 Persona / azienda
🔔 Aggiungi monitor
```

Esempi:

```text
/raven status
/raven email nome@example.com
/breach nome@example.com
/raven password CONFERMO password-non-piu-usata
/raven username nomeutente
/raven domain example.com
/raven azienda Nome Azienda
/raven ioc 8.8.8.8
/raven ioc <sha256>
/raven monitor add email nome@example.com 24
/raven monitor list
/raven monitor run
/raven monitor remove email nome@example.com
```

`/breach nome@example.com` è l'alias rapido per il controllo email. Le ricerche
su persone e aziende sono OSINT indicativo: omonimie e menzioni non provano una
compromissione. I dettagli architetturali, il contratto job e i guardrail sono
in [`modules/raven/README.md`](modules/raven/README.md).

## Comandi Principali

| Comando | Descrizione |
|---|---|
| /menu | Apre la home guidata di Raptor OS |
| /help | Mostra help e capability dal registry del menu |
| /scriviarticolo | Genera o pianifica contenuti/articoli per il blog |
| /redazione | Alias compatibile di `/scriviarticolo` |
| /seo | Keyword cluster, snippet SEO, brief e report analyzer semplice |
| /seobrief | Alias rapido per generare un brief SEO automatico |
| /seoreport | Alias rapido per analizzare un report/testo SEO |
| /socialpost | Dashboard per pubblicare o programmare post Facebook/Instagram |
| /newsletter | Liste contatti e newsletter immediate o programmate |
| /cmd | Esegue comandi terminale autorizzati |
| /aggiornanote | Aggiorna e sincronizza subito le note Obsidian |
| /clear | Pulisce il contesto conversazionale e la memoria breve |
| /annulla | Interrompe il workflow attivo |
| /vettorizza | Indicizza domini e contenuti tramite Internet Archive |
| /ricercadominio | Recupera e approfondisce memoria vettoriale temporanea |
| /piercevector | Alias compatibile di `/ricercadominio` |
| /ricercafile | Analizza, riassume e traduce file/cartelle PCloud |
| /piercepcloud | Alias compatibile di `/ricercafile` |
| /ricercatelegram | Analizza e indicizza contenuti di canali Telegram |
| /piercetelegram | Alias compatibile di `/ricercatelegram` |
| /web | Ricerca web con sintesi breve e fonti |
| /email | Workflow email con preview e conferma |
| /calendar | Gestione calendario ed eventi |
| /audit | Audit security controllato su target autorizzati |
| /auditdominio | Audit tecnico controllato, default `recon` |
| /security_audit | Alias compatibile di `/auditdominio` |
| /security_osint | OSINT passivo su dominio |
| /osintpersona | OSINT pubblico su persona/azienda |
| /security_person_osint | Alias compatibile di `/osintpersona` |
| /audit_allow | Gestione allowlist security da Telegram |
| /audit_watch | Monitor periodico dei target autorizzati |
| /watchtarget | Monitor periodico dei target autorizzati |
| /security_watch | Alias compatibile di `/watchtarget` |
| /audit_history | Storico degli audit security |
| /real_audit | Avvio diretto di `real-audit` con conferma |
| /statooffensive | Stato del gate offensive |
| /offensive_status | Stato del gate offensive |
| /offensive_enable | Abilita temporaneamente offensive safe mode per un target |
| /offensive_run | Esegue controlli offensivi safe su target abilitato |
| /offensive_explicit | Esegue controlli lab-only con conferma specifica |
| /offensive_disable | Disabilita offensive mode |
| /timeline | Consulta timeline cognitiva e storica del progetto |
| /operatore | Attiva modalità operatore ultra sintetica; `/operatore off` per disattivare |
| /operator | Alias compatibile di `/operatore` |
| /ragnir | Worker remoto Ragnir per repo, siti, screenshot, patch e publish |
| /raven | Exposure monitoring difensivo, breach check e OSINT passivo |
| /breach | Alias rapido Raven per la verifica di un indirizzo email |

### Comandi Ragnir principali

| Comando | Descrizione |
|---|---|
| /ragnir status | Ping/status rapido del worker Ragnir |
| /ragnir last | Ultima attività Ragnir con sito, repo, request id e bottoni rapidi |
| /ragnir sites | Lista dei siti configurati in `modules/ragnir/sites.py` |
| /ragnir site-info `<site>` | Configurazione completa del sito |
| /ragnir check-site `<site>` | Check online del sito tramite URL pubblico |
| /ragnir screenshot-page `<site>` `<page>` | Screenshot di una pagina configurata |
| /ragnir edit-site `<site>` `<istruzione>` | Modifica il file principale del sito con preview e conferma |
| /ragnir edit-page `<site>` `<page>` `<istruzione>` | Modifica una pagina configurata con preview e conferma |
| /ragnir edit-section `<site>` `<page>` `<section>` `<istruzione>` | Modifica una sezione configurata, ad esempio footer/hero/main, con preview e conferma |
| /ragnir publish-site `<site>` `"messaggio"` | Prepara commit + push del sito con conferma |
| /ragnir diff-last | Mostra l'ultimo diff Ragnir disponibile |
| /ragnir rollback-last | Prepara rollback dell'ultima modifica applicata, sempre con conferma |
| /ragnir fetch `<url>` | Fetch tecnico di una URL libera |
| /ragnir screenshot `<url>` | Screenshot tecnico di una URL libera |
| /ragnir cleanup | Pulizia file temporanei lato Ragnir |
| /ragnir repo `<repo>` | Stato Git di una repo gestita da Ragnir |
| /ragnir conferma | Conferma una pending action Ragnir |
| /ragnir annulla | Annulla una pending action Ragnir |

### Comandi Raven principali

| Comando | Descrizione |
|---|---|
| /raven status | Stato Raven, provider e monitor attivi |
| /breach `<email>` | Breach check email rapido |
| /raven email `<email>` | Breach e menzioni passive per email |
| /raven password CONFERMO `<password>` | Check password HIBP con k-anonymity e conferma esplicita |
| /raven username `<username>` | Ricerca passiva di uno username |
| /raven domain `<dominio>` | Breach organizzativi, menzioni e IOC enrichment |
| /raven persona `<nome>` | OSINT passivo su persona, senza attribuzione automatica |
| /raven azienda `<nome>` | OSINT passivo su azienda |
| /raven ioc `<indicatore>` | Lookup di IP, dominio o hash sui provider compatibili |
| /raven monitor add `<tipo>` `<target>` `[ore]` | Aggiunge o riattiva un monitor |
| /raven monitor list | Elenca i monitor attivi |
| /raven monitor run | Forza il controllo di tutti i monitor |
| /raven monitor remove `<tipo>` `<target>` | Disattiva un monitor |

## Esempi Rapidi

```text
/menu
/scriviarticolo articolo SEO WordPress per hotel
/seo software preventivi online
/seo cluster crm freelance, miglior crm freelance, crm prezzi
/seo snippet tool gestione task per freelance
/seo brief guida fatturazione elettronica forfettari
/seo report Title: Esempio SEO Meta description: troppo corta
/seo url https://example.com/software-preventivi-online
/summary text operativo testo lungo da riassumere
/summary notes breve
/summary last
/memoria provider fallback
/memoria note modulo SEO
/cmd ls -la
/aggiornanote
/clear

/vettorizza example.com cybersecurity
/ricercadominio example.com
/ricercafile
/ricercatelegram

/email
/calendar domani
/auditdominio dominio.it

/timeline semantic reranking
/operatore on

/ragnir status
/ragnir last
/ragnir sites
/ragnir site-info offfice
/ragnir check-site offfice
/ragnir screenshot-page offfice home
/ragnir edit-page offfice home rendi il footer più chiaro
/ragnir publish-site offfice "Aggiorna contenuti sito"
/ragnir fetch https://example.com
/ragnir screenshot https://example.com

/raven status
/raven intel example.com
/raven ioc 8.8.8.8
/raven monitor list
```

## Workflow Cognitivi

Raptor distingue:

* navigazione guidata e discovery (`/menu`)
* retrieval semantico (`/ricercadominio`, alias `/piercevector`)
* ingestione conoscenza (`/vettorizza`)
* ingestione documentale (`/ricercafile`, alias `/piercepcloud`)
* ingestione Telegram (`/ricercatelegram`, alias `/piercetelegram`)
* generazione contenuti (`/scriviarticolo`, alias `/redazione`)
* operazioni sistema (`/cmd`)
* sincronizzazione knowledge base (`/aggiornanote`)
* gestione siti/repo tramite Ragnir (`/ragnir`)
* threat intelligence Raven locale, con worker remoto opzionale (`/raven`)

Questo permette di mantenere separati:

* memoria
* retrieval
* automazione
* knowledge ingestion
* workflow operativi

## Ragnir e gestione siti

Il modulo Ragnir vive in `modules/ragnir/` lato Raptor e comunica con un worker
remoto tramite `RAGNIR_BASE_URL` e `RAGNIR_API_TOKEN`.

Ruoli separati:

```text
Raptor
= orchestratore, UX Telegram, memoria, LLM reasoning, pending action

Ragnir
= execution node leggero: repo, git, browser, screenshot, patch, publish

GitHub
= source of truth del codice

Cloudflare Pages
= deploy/build pubblico dei siti
```

Il worker Ragnir deve restare leggero:

* niente hosting applicativo pesante
* niente build server persistente
* niente storage permanente enorme
* repo limitate e controllate
* screenshot, backup e tmp gestiti come artefatti temporanei

### Registro siti

La configurazione site-aware vive in:

```text
modules/ragnir/sites.py
```

Per ogni sito il registry può definire:

* slug e alias
* repo Git
* branch e remote
* URL pubblico
* healthcheck URL
* screenshot URL
* file principale
* pagine configurate
* file modificabili
* file protetti
* policy operative
* provider deploy

Esempio attuale:

```text
site: offfice-it
alias: offfice, offfice.it, office
repo: offfice-it
branch: main
remote: origin
provider: cloudflare_pages
public_url: https://offfice-it.pages.dev/
main_file: public/index.html
page: home -> public/index.html
```

### Flusso edit sicuro

Le modifiche Ragnir non vengono applicate direttamente. Il flusso è:

```text
utente/menu
 ↓
/ragnir edit-page offfice home <istruzione>
 ↓
LLM edit preview
 ↓
diff leggibile
 ↓
pending repo_apply_patch
 ↓
/ragnir conferma
 ↓
backup + apply patch
 ↓
repo dirty
 ↓
/ragnir publish-site offfice "messaggio"
 ↓
pending repo_publish
 ↓
/ragnir conferma
 ↓
commit + push
 ↓
Cloudflare Pages pubblica
```

Ogni modifica genera backup lato Ragnir prima dell'applicazione. Il publish usa
commit + push verso il remote/branch configurato.

#### Modifica avanzata e patch proposta

Nel flusso Telegram di modifica avanzata Raptor separa intenzionalmente
pianificazione, patch e applicazione:

* la preview LLM e il bottone `Prompt esterno` producono solo piano/JSON
  conservativo, non contenuti applicabili
* `Genera patch proposta` chiede all'LLM solo una sostituzione strutturata
  `path`, `old_text`, `new_text`, `reason`
* Raptor verifica che `old_text` esista esattamente e una sola volta nel file
  reale analizzato
* Raptor applica la sostituzione in memoria e genera la unified diff con
  `difflib`, senza far calcolare hunk o numeri di riga all'LLM
* Ragnir esegue `repo_check_patch` sulla diff proposta prima di creare il
  pending `advanced_patch`
* la diff viene sempre mostrata in preview; apply, commit e push richiedono
  conferma esplicita

Raptor non applica mai piani descrittivi, JSON o testo libero come patch:
il JSON dell'LLM serve solo a costruire una diff deterministica lato Raptor.

### Safe edit enforcement

La sicurezza dell'editing si basa su whitelist e blocchi espliciti:

* `safe_edit_files`: file modificabili
* `protected_files`: file sempre bloccati
* blocco di path traversal (`../`)
* blocco di path assoluti (`/etc/passwd`)
* blocco di file non previsti dal registry sito
* conferma obbligatoria prima di apply e publish

### Limiti attuali dell'editing HTML

L'editing LLM leggero funziona bene per modifiche puntuali, ma file HTML con
molti stili inline o sezioni lunghe possono produrre modifiche parziali.

Per questo la roadmap prevede:

* controllo qualità sulla preview
* warning se il diff sembra troppo piccolo rispetto alla richiesta
* preset deterministici per modifiche ripetitive, ad esempio footer/privacy
* full-file edit solo in modalità controllata


## Ingestione PCloud

`/ricercafile` legge link pubblici PCloud e apre un browser Telegram con
cartelle e file. I bottoni cartella navigano dentro il percorso selezionato; i
bottoni file leggono o analizzano il contenuto.

`/piercepcloud` resta alias compatibile.

Uso con link configurato nel `.env`:

```text
/ricercafile
```

Uso con uno o più link passati direttamente da Telegram:

```text
/ricercafile https://e.pcloud.link/publink/show?code=...
/ricercafile https://link-cartella-1 https://link-cartella-2
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

`/ricercadominio` consulta memoria già costruita: selezioni una collection,
inserisci una query, il sistema recupera documenti da Chroma, li reranka e
mostra sorgenti e sintesi. Quando i metadata Chroma contengono identifier o URL
Internet Archive, prova anche un fetch live leggero: legge solo pochi file
testuali/PDF limitati, reranka chunk reali e li passa alla sintesi. Se non trova
contesto pertinente non genera una sintesi inventata. Se il retrieval Chroma
fallisce, lo dichiara e usa un fallback live da Internet Archive.

`/piercevector` resta alias compatibile.

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
* programmazione persistente con SQLite
* due proposte rapide intelligenti e data/ora in linguaggio naturale
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

[⚡ Invia ora]
[🕘 Prima fascia utile]
[✨ Momento migliore]
[🗓 Personalizza data e ora]
[✏️ Modifica] [❌ Annulla]
```

La scelta non esegue ancora l'azione: Raptor mostra sempre una seconda
conferma con destinatario, oggetto e momento esatto di consegna. Solo
`✅ Conferma` invia subito oppure salva il messaggio nella coda persistente.

La programmazione personalizzata comprende, tra le altre, queste forme:

```text
Invia ora
Mandala domani alle 10
Mandala domani mattina
Mandala venerdì pomeriggio
Mandala il 18/08 alle 14:30
Mandala nel momento migliore
```

Le fasce generiche vengono tradotte in un orario preciso e spiegate nella
conferma. Le proposte intelligenti usano `Europe/Rome`, privilegiano orari
lavorativi ed evitano il fine settimana. Lo scheduler continua a funzionare
dopo un riavvio e usa lo stesso servizio SMTP Aruba dell'invio immediato.

La tabella `scheduled_emails` include già `campaign_id`, metadati, stati,
tentativi e invio a blocchi. È quindi pronta per deduplicazione, rate limiting
e campagne multi-destinatario senza introdurre Brevo o Sendinblue nel core.

### Centro Email e campagne

Il comando `/campaign` (alias `/campagne` e `/mailcenter`) apre una dashboard
Telegram con quattro viste:

* Email
* Campagne
* Programmate
* Storico

Raptor accetta direttamente file `.csv`, `.json` e `.txt`. Una caption utile è:

```text
Campagna: Candidatura docenza settembre |
Obiettivo: propormi come docente di informatica |
Modalità: assisted
```

Il parser deriva dalla logica collaudata di GV Mail Sender e riconosce alias
italiani e inglesi per nome, cognome, email, azienda, settore, sito, città,
ruolo, corsi, note, oggetto e testi personalizzati. Gestisce CSV con virgola o
punto e virgola, UTF-8/Windows-1252, `mailto:`, `Nome <email>`, liste semplici
e colonne LeadRocks. Gli errori di una riga non bloccano le altre.

Il workflow è sempre separato in fasi persistenti:

```text
import → deduplicazione/soppressioni → generazione → quality control
       → salvataggio immutabile → approvazione → scheduling → Aruba SMTP
```

Prima dell'approvazione non viene creato alcun invio. I messaggi generati sono
salvati in `email_messages` e non vengono rigenerati dal worker. I controlli
bloccano indirizzi non validi, oggetti o testi mancanti, placeholder irrisolti,
lunghezze anomale e saluti con un nome incoerente.

Le modalità disponibili sono:

* `STRICT`: revisione e approvazione di ogni email, poi conferma campagna
* `ASSISTED`: una conferma della campagna, quindi gestione autonoma degli orari
* `AUTONOMOUS`: attivazione esplicita iniziale, poi applicazione delle regole

`ASSISTED` è il default. Anche `AUTONOMOUS` richiede un'attivazione esplicita:
un CSV o un comando ambiguo non può avviare invii multipli.

Le regole sono modificabili dal pulsante `⚙️ Regole campagna`:

```text
max_per_hour: 5, max_per_day: 25, orari: 9-17,
pausa: 8-16, giorni: lun-ven, modalità: assisted
```

La distribuzione usa pause variabili ma riproducibili, rispetta giorni e orari
consentiti e limita sia la singola ora sia la giornata. Dopo errori SMTP
consecutivi la campagna viene messa automaticamente in pausa. I follow-up a
5 giorni sono opzionali, cancellabili e programmati soltanto dopo conferma.
Raptor assegna un `Message-ID` agli invii e controlla periodicamente via IMAP:
quando rileva una risposta dello stesso mittente con riferimento esatto al
thread, annulla il relativo follow-up. Non usa semplici somiglianze dell'oggetto,
così una vecchia email non può cancellare per errore un invio futuro.

Comandi naturali supportati:

```text
Che email devo ancora inviare?
Mostrami quelle programmate per domani.
Annulla la mail a Mario.
Posticipa tutta la campagna a lunedì.
Quali aziende abbiamo già contattato?
Rimanda solo quelle fallite.
Non scrivere più a nome@example.com.
```

Le operazioni che modificano coda o soppressioni chiedono una conferma
esplicita. L'analisi opzionale dei siti usa soltanto URL già presenti nei dati,
blocca reti private e redirect non sicuri e non cerca nuove aziende.

La ricerca lead è disponibile tramite `/outreach` o linguaggio naturale.
Raptor crea il progetto e richiede approvazione; Ragnir scopre e analizza i
siti, mentre Raptor deduplica, assegna score, conserva CRM e crea la campagna.
I job di ricerca vengono recuperati dopo un riavvio e ritentati fino al limite
configurato. Nessuna email viene inviata dalla fase outreach: preparazione,
anteprima e conferma finale restano nel Centro email. Brevo, Sendinblue e
SendFox non fanno parte del core; il trasporto resta Aruba SMTP dietro
l'interfaccia `EmailService`.

```env
OUTREACH_RESEARCH_ENABLED=1
OUTREACH_RESEARCH_TIMEOUT_SECONDS=600
OUTREACH_RESEARCH_MAX_ATTEMPTS=3
```

Stati temporanei principali:

* `waiting_recipient`
* `waiting_contact_confirmation`
* `waiting_subject`
* `waiting_body`
* `waiting_edit`
* `preview_ready`
* `waiting_schedule_custom`
* `waiting_delivery_confirmation`

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
/auditdominio dominio.it
/security_audit dominio.it recon
/security_osint dominio.it
/osintpersona "Nome Cognome"
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
/watchtarget dominio.it
/security_watch dominio.it
/statooffensive
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

`/osintpersona "Nome Cognome"` usa solo dati pubblici e username
candidati. Lo scopo è orientativo: profili, domini o email devono essere
verificati manualmente per evitare omonimie e falsi positivi. Lo stack locale
integrabile è `maigret` e `sherlock`; `holehe` resta disponibile come tool
OSINT specializzato su email, ma non viene eseguito automaticamente senza un
indirizzo esplicito.

`/security_person_osint` resta alias compatibile.

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
| sync_notes.sh                    | Sincronizza `privatebrain/` con Git: commit, pull rebase e push |
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
Git: committa le modifiche locali del vault, esegue `git pull --rebase` e poi
`git push`. Il log viene scritto in:

```text
logs/sync_notes.log
```

Il repository Git interno di `privatebrain/` usa come remote:

```text
https://github.com/gabrieleviolait/privatebrain.git
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
| core/menu_registry.py | Registry semantico menu, alias e capability |
| handlers/         | Handler Telegram                       |
| handlers/menu_handler.py | UI Telegram del menu cognitivo e input contestuale |
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
| modules/raven/   | Breach check, IOC enrichment e monitor passivi |
| modules/social/  | Account Meta, pubblicazione e coda social |
| modules/newsletter/ | Liste contatti e run newsletter       |
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

`/operatore` attiva output ultra sintetico:

```text
✔ operator ON
max_tokens=200
```

Comandi:

* `/operatore` oppure `/operatore on`
* `/operatore off`
* `/operatore status`
* `/operator` resta alias compatibile

In questa modalita la chat usa un prompt operativo, il motore LLM riceve un
limite di token e gli output senza bottoni vengono compattati in stato/azione.
Le preview con conferma restano estese per sicurezza.

## Annulla Globale

`annulla`, `Annulla` e `/annulla` fermano gli stati operativi correnti:

* bozze email
* preview calendario
* modifica/cancellazione note
* suggerimenti task
* workflow `/vettorizza`, `/ricercadominio`, `/ricercatelegram`
* selezioni pCloud/Telegram in corso

La modalita `/operatore` non viene disattivata da `annulla`; si spegne solo con
`/operatore off`.


## Stato Attuale

### Completato

* Raven — servizio locale integrato con fallback worker HTTP remoto
* Raven — HIBP email/password, catalogo domini e indici dark-web passivi
* Raven — ThreatFox, URLhaus e MalwareBazaar read-only
* Raven — monitor SQLite, digest delle variazioni e alert Telegram
* Social publishing — Facebook e Instagram, scheduling e notifiche Telegram
* Newsletter — liste, import CSV, preview e invio tramite coda email
* v0.5.8 — LLM edit leggero
* v0.5.9 — `sites.py` e snellimento operativo
* v0.6.0 — bottoni Telegram per pending Ragnir
* v0.6.1 — `/ragnir last` e sessione runtime in-memory
* v0.6.1.1 — `sites.py` futureproof
* v0.6.2 — `/ragnir edit-site`
* v0.6.3 — `/ragnir site-info`
* v0.6.4 — `/ragnir sites`
* v0.6.5 — `/ragnir check-site`
* v0.6.6 — `/ragnir screenshot-page`
* v0.6.7 — `/ragnir edit-page`
* v0.6.8 — `/ragnir publish-site`
* v0.6.9 — safe edit enforcement
* v0.7.0 — rework menu Telegram Ragnir
* v0.7.0.1 — diagnostica generale spostata in Utilità
* v0.7.0.2 — sezione Ragnir `🌐 Siti`
* v0.7.0.3 — sezione Ragnir `⚡ Gestione sito`
* v0.7.0.4 — sezione Ragnir `🧭 Ultima attività`
* v0.7.0.5 — sezione Ragnir `🛠️ Operazioni tecniche`
* v0.7.0.6 — advanced patch via JSON replace e diff deterministica

### In evoluzione

* v0.7.1 — post-publish flow guidato con screenshot/check/status/last
* v0.7.3 — aggiornamento help/usage interno
* v0.7.4 — qualità LLM edit e rilevamento modifiche incomplete
* v0.7.5 — test negativi sicurezza e regressione safe edit
* v0.8.x — preset deterministici, full-file edit controllato e multi-site reale

### Funzionalità in valutazione

* Web UI locale per configurazione API e moduli
* Gestione plugin Raptor/Ragnir installabili
* Multi-site reale con più domini e repo configurati

# Stack Tecnologico

## AI

* Groq
* Cerebras
* OpenRouter
* NVIDIA NIM
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


## Licenza

Questo progetto è rilasciato sotto licenza **GNU Affero General Public License v3.0 or later** (`AGPL-3.0-or-later`).

Raptor OS è un sistema modulare pensato per essere usato anche come servizio, bot o componente server.  
Le versioni modificate e rese disponibili tramite rete devono rispettare i termini della AGPLv3.

Vedi il file [`LICENSE`](LICENSE).
