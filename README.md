# Implementazione Cluster Minikube con Redis Master, Slave e Sentinel

Questo documento fornisce istruzioni dettagliate per configurare un cluster Minikube con Redis utilizzando Docker Desktop e Chocolatey su un sistema Windows.

## Installazione degli Strumenti Necessari

### Docker Desktop

Docker Desktop è una piattaforma per lo sviluppo e la distribuzione di applicazioni in container. Segui i passaggi seguenti per installarlo:

1. **Scarica Docker Desktop:**
   Vai al sito ufficiale di Docker Desktop per Windows e scarica il programma di installazione: [Download Docker Desktop](https://www.docker.com/products/docker-desktop).

2. **Esegui l'installazione:**
   Una volta scaricato il file di installazione, avvialo e segui le istruzioni sullo schermo per completare l'installazione di Docker Desktop.

3. **Verifica l'installazione:**
   Dopo l'installazione, apri PowerShell o il prompt dei comandi e esegui il comando per verificare se Docker è installato correttamente:
   ```bash
   docker --version

## Chocolatey

Chocolatey è un gestore di pacchetti per Windows che semplifica l'installazione e la gestione di software. Ecco come utilizzarlo per installare Minikube e Kubernetes:

### Installazione di Chocolatey

Per installare Chocolatey, segui le istruzioni disponibili sul sito ufficiale: [Installazione di Chocolatey](https://chocolatey.org/install).

Esegui il seguente comando nel tuo PowerShell con privilegi elevati (Esegui come amministratore):

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol
[System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
Una volta completata l'installazione, si prega di verificare la corretta installazione utilizzando il comando
```powershell
choco -v
```

### Kubernetes
Kubernetes è un sistema open-source per l'automazione del deployment, scaling e gestione delle applicazioni containerizzate.

- Orchestrazione avanzata: Kubernetes gestisce automaticamente la distribuzione, la scalabilità e la gestione delle applicazioni containerizzate su un cluster di host.

- Architettura modulare: Kubernetes è progettato con un'architettura modulare che consente di estendere le funzionalità base con plugin e componenti aggiuntivi.

- Declarative Configuration: Utilizza file di configurazione YAML per dichiarare lo stato desiderato del sistema, permettendo a Kubernetes di gestire le risorse in 
  modo dichiarativo.

- Scaling automatico: Supporta il scaling automatico delle applicazioni in base alle esigenze del carico di lavoro, migliorando l'efficienza e la disponibilità delle 
  applicazioni.

- Service Discovery e Load Balancing: Fornisce servizi di discovery e bilanciamento del carico tra i container, facilitando la comunicazione tra i diversi componenti 
  dell'applicazione.

#### Installazione
```powershell
choco install kubernetes
```
#### Verifica 
```powershell
kubectl version
```




### Minikube
Minikube è uno strumento che consente di eseguire un cluster Kubernetes locale su un singolo nodo.

- Ambiente di sviluppo locale: Minikube permette agli sviluppatori di eseguire e testare applicazioni Kubernetes in un ambiente locale, riducendo la dipendenza da 
  cluster remoti per lo sviluppo e il testing.

- Facilità di setup: Minikube è progettato per essere facile da installare e configurare su sistemi operativi desktop come Windows, macOS e Linux.

- Supporto per funzionalità Kubernetes: Anche se Minikube è destinato a un ambiente di sviluppo locale, supporta molte delle funzionalità di Kubernetes come 
  deployment, scaling, e gestione dei pod e dei servizi.

- Integrazione con strumenti di sviluppo: Minikube si integra con strumenti di sviluppo popolari come Docker, permettendo agli sviluppatori di utilizzare un ambiente 
  familiare per la gestione dei container e delle applicazioni.

- Testing e debugging: Minikube facilita il testing e il debugging delle applicazioni Kubernetes in un ambiente isolato e controllato, prima di distribuirle su 
  cluster Kubernetes più grandi.

#### Installazione
```powershell
choco install minikube
```
#### Verifica 
```powershell
minikube verion
```

## Redis Master  e Slave and failover 


## Deploy del cluster 
**Avviare il nodo di Minikube:**
```bash
minikube start -p redis-cluster 
```
 **Verificare lo stato di Minikube:**
 ```bash
minikube status - p redis-cluster
``` 
**Creare un namespace:**
```bash
kubectl create ns redis-ns
``` 
**In seguito  per l'applicazione in seguito dei manifesti settiamo il namespace creato** 
```bash
kubectl config set-context --current --namespace=redis-ns
```
#### configmap.yaml 
- apiVersion: v1 definisce un oggetto ConfigMap in Kubernetes che contiene la configurazione di un'istanza di Redis tramite il file redis.conf. Ecco una spiegazione 
  del codice:
- apiVersion e kind: Specificano il tipo di risorsa Kubernetes (ConfigMap nel nostro caso). apiVersion: v1 indica che stiamo utilizzando la versione stabile API v1 
  di Kubernetes.
- metadata: Contiene metadati che descrivono il ConfigMap.
- name: redis-config: Specifica il nome del ConfigMap, che è redis-config.
- namespace: redis-ns: Indica il namespace in cui è definito il ConfigMap, che è redis-ns. I namespace in Kubernetes sono usati per organizzare e raggruppare risorse.
  data: Contiene i dati effettivi del ConfigMap, rappresentati come una mappa di coppie chiave-valore.

- redis.conf: È il nome del file all'interno del ConfigMap che conterrà la configurazione di Redis.
- redis.conf: È il contenuto del file di configurazione Redis. Le configurazioni incluse sono:

- cluster-enabled no: Indica che Redis non è configurato in modalità cluster.

- cluster-config-file nodes.conf: Specifica il file in cui vengono salvate le informazioni sui nodi nel caso di configurazione cluster.

- cluster-node-timeout 15000: Imposta il timeout per i nodi del cluster a 15 secondi.

- bind 0.0.0.0: Redis si lega a tutte le interfacce di rete disponibili.

- port 6379: Specifica la porta su cui Redis è in ascolto (default è 6379).

#### Persistenza dei dati:

- dir /data: Indica la directory in cui vengono memorizzati i dati persistenti.
- dbfilename dump.rdb: Nome del file per il dump del database.
- appendonly yes: Abilita il file di append-only (appendonly.aof) per garantire la persistenza dei dati.
- appendfilename "appendonly.aof": Specifica il nome del file di append-only.
#### Autenticazione:
- masterauth dHJlbjc5Cg==: Specifica la password codificata in Base64 per l'autenticazione del master. La stringa "dHJlbjc5Cg==" corrisponde alla password 
  decodificata.
- requirepass dHJlbjc5Cg==: Specifica la password codificata in Base64 necessaria per accedere agli altri comandi di Redis.



## Test 

## Consderazioni 



