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
### COMPONETI KUBERNETES

#### Pod 
Un Pod è l'unità di calcolo più piccola che può essere creata e gestita in Kubernetes. Rappresenta un gruppo di uno o più container che condividono risorse di archiviazione e rete, e che vengono eseguiti in un contesto condiviso. I Pod modellano un host logico specifico per un'applicazione e contengono container applicativi strettamente accoppiati. Questi container sono sempre co-locati, co-schedulati e eseguiti insieme, rendendo i Pod analoghi a un'applicazione eseguita su una singola macchina fisica o virtuale in contesti non cloud.

#### Namespace 
I namespace forniscono un meccanismo per isolare gruppi di risorse all'interno di un singolo cluster. I nomi delle risorse devono essere univoci all'interno di un namespace, ma non tra i diversi namespace. Lo scope basato sui namespace si applica solo agli oggetti con namespace (ad esempio Deployments, Services, ecc.) e non agli oggetti a livello di cluster (ad esempio StorageClass, Nodi, PersistentVolumes, ecc.).

#### Configmap 
Una ConfigMap è un oggetto Kubernetes che permette di separare la configurazione dell'applicazione dal codice eseguibile. Può essere utilizzata per fornire file di configurazione, variabili d'ambiente, argomenti della riga di comando e altri parametri di configurazione ai Pod. Questo approccio consente di mantenere le configurazioni esterne e indipendenti dai container, permettendo una maggiore flessibilità e riusabilità. Le ConfigMap vengono combinate con i Pod appena prima della loro esecuzione, il che consente di utilizzare la stessa immagine del container e la definizione del Pod in diversi contesti applicativi semplicemente modificando la ConfigMap associata.

#### Service 
Un Service in Kubernetes è un'astrazione che definisce un insieme logico di Pod e una policy per accedervi. Fornisce un singolo punto di accesso stabile per un insieme di Pod, indipendentemente dai cambiamenti dinamici del ciclo di vita dei Pod stessi. I Service consentono di esporre applicazioni di rete che girano nei Pod, senza la necessità di modificare le applicazioni stesse per adattarsi a nuovi meccanismi di scoperta dei servizi. In pratica, un Service rende un insieme di Pod disponibile sulla rete, permettendo ai client di comunicare con esso tramite un indirizzo IP stabile e un nome DNS, semplificando così l'interazione con le applicazioni distribuite nel cluster Kubernetes.

#### Statefulset
Un StatefulSet è un oggetto API di Kubernetes progettato per gestire applicazioni stateful, cioè applicazioni che richiedono uno stato persistente e un'identità stabile. A differenza di un Deployment, che gestisce Pod intercambiabili, un StatefulSet garantisce che ogni Pod mantenga un'identità unica e persistente attraverso le rischedulazioni. Questo è particolarmente utile quando si utilizzano volumi di storage per garantire la persistenza dei dati. Gli StatefulSet assicurano che i Pod siano creati e aggiornati in un ordine specifico e mantengano una relazione stabile con i volumi di storage, facilitando la gestione di applicazioni complesse che richiedono dati persistenti e identificatori unici.

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

## Redis 
Redis è un sistema di archiviazione dati in memoria open-source noto per la sua velocità e versatilità. Supporta diverse strutture dati come stringhe, liste, set e hash, ed è ampiamente utilizzato per applicazioni che richiedono accesso rapido ai dati, come caching e conteggio in tempo reale.
### Architettura Master-Slave e Redis Sentinel:
- Master-Slave: In questa architettura, un nodo Master gestisce le operazioni di scrittura, mentre i nodi Slave replicano i dati dal Master per consentire letture 
  veloci e garantire ridondanza. In un ambiente Kubernetes, puoi implementare questa architettura utilizzando StatefulSet, configurando un pod come Master e gli 
  altri come Slave.
- Redis Sentinel: Redis Sentinel monitora i nodi e garantisce l’alta disponibilità del cluster. In caso di fallimento del Master, Sentinel coordina il failover 
  promuovendo automaticamente un Slave a nuovo Master.

### Persistenza:
- Append Only File (AOF): Redis registra ogni operazione di scrittura in un file AOF. Questo meccanismo di persistenza consente di ripristinare lo stato dei dati in 
  caso di crash del server Redis.
- Redis DataBase Dump (RDB): L’RDB crea snapshot dei dati in un momento specifico. Puoi pianificare backup periodici utilizzando questa opzione. Tuttavia, l’RDB 
  potrebbe perdere dati tra due snapshot in caso di crash.

### Migrazione verso Kubernetes:
La migrazione di Redis verso Kubernetes offre vantaggi significativi:
- Scalabilità e Ridondanza: Kubernetes gestisce dinamicamente i nodi Redis, consentendo di scalare orizzontalmente aggiungendo o rimuovendo pod in base al carico.
- Gestione Semplificata: Kubernetes automatizza la distribuzione, la gestione dei fallimenti e la riparazione dei nodi, migliorando l’affidabilità del servizio Redis.
  
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
**In seguito  per l'applicazione dei manifesti settiamo il namespace creato** 
```bash
kubectl config set-context --current --namespace=redis-ns
```

### configmap.yaml 

La versione dell'API è v1 e il tipo di oggetto è ConfigMap. I metadati specificano il nome redis-config e il namespace redis-ns, che serve a organizzare e isolare risorse nel cluster Kubernetes.

All'interno della sezione data, viene definito il contenuto del file redis.conf. Questo file contiene diverse configurazioni per Redis. La configurazione cluster-enabled no indica che Redis non è configurato in modalità cluster. La riga cluster-config-file nodes.conf specifica il file in cui vengono salvate le informazioni sui nodi, mentre cluster-node-timeout 15000 imposta il timeout per i nodi del cluster a 15 secondi. La direttiva bind 0.0.0.0 configura Redis per legarsi a tutte le interfacce di rete disponibili, e port 6379 specifica la porta su cui Redis è in ascolto.

Per la persistenza dei dati, il parametro dir /data indica la directory in cui vengono memorizzati i dati persistenti. Il file dump.rdb viene utilizzato per il dump del database, mentre l'opzione appendonly yes abilita l'uso del file di append-only (appendonly.aof) per garantire la persistenza dei dati. Il nome di questo file è specificato da appendfilename "appendonly.aof".

Infine, la configurazione dell'autenticazione è gestita dalle righe masterauth ********* e requirepass *********, che specificano le password codificate in Base64 per l'autenticazione del master e per l'accesso ai comandi di Redis.

**Applicazione Manifesto**
```bash
kubectl apply -f configmap.yaml 
```

### s-configmap.yaml
Identificato da apiVersion: v1 e kind: ConfigMap. La sezione metadata fornisce metadati essenziali, specificando il nome redis-sentinel-config e il namespace redis-ns, che serve a organizzare e isolare risorse nel cluster Kubernetes.

Il cuore della configurazione si trova nella sezione data, dove viene definito il file sentinel.conf. Questo file specifica che il Sentinel di Redis deve ascoltare sulla porta 5000 e deve risolvere e annunciare i nomi degli host. Viene configurato per monitorare un master chiamato mymaster, identificato dall'indirizzo redis-0.redis.redis-ns.svc.cluster.local sulla porta 6379. Il parametro 2 indica che sono necessari almeno due Sentinel per confermare un fallimento del master.

Altre configurazioni includono il tempo, in millisecondi, dopo il quale il Sentinel considererà il master non raggiungibile (5000 millisecondi), e il timeout per completare un failover (60000 millisecondi). Inoltre, il Sentinel è configurato per consentire una sola sincronizzazione parallela durante il failover. Infine, la riga sentinel auth-pass mymaster ********* specifica la password, codificata in Base64, per l'autenticazione con il master mymaster.

**Applicazione Manifesto**
```bash
kubectl apply -f s-configmap.yaml 
```
### service.yaml 
La versione dell'API è v1 e il tipo di oggetto è Service. I metadati specificano il nome redis, che identifica univocamente il Service all'interno del namespace.

La sezione spec contiene la specifica del Service. clusterIP: None indica che il Service è di tipo Headless, il che significa che non viene assegnato un indirizzo IP cluster-wide, ma viene comunque creato un DNS entry per ciascun Pod. Questo è utile per scenari come StatefulSets, dove i Pod devono essere indirizzabili direttamente.

Il campo ports definisce che il Service ascolterà sulla porta 6379 e indirizzerà il traffico verso la stessa porta nei Pod di destinazione. Il targetPort specifica la porta sul container che riceverà il traffico. Entrambi i valori sono 6379, che è la porta standard di Redis.

Il campo selector definisce una mappa di etichette utilizzata per selezionare i Pod gestiti dal Service. In questo caso, seleziona i Pod con l'etichetta app: redis. Questo consente al Service di instradare il traffico verso i Pod che eseguono Redis.

**Applicazione Manifesto**
```bash
kubectl apply -f service.yaml 
```

### s-service.yaml 
La versione dell'API è v1 e il tipo di oggetto è Service. I metadati specificano il nome sentinel e il namespace redis-ns, che organizza e isola le risorse nel cluster Kubernetes.

Nella sezione spec, la specifica del Service, clusterIP: None indica che il Service è di tipo Headless, quindi non viene assegnato un indirizzo IP unico a livello di cluster. Questo è utile per applicazioni che richiedono un routing diretto ai singoli Pod, come nel caso dei set di StatefulSet o di servizi che richiedono scoperta diretta dei nodi.

Il campo ports indica che il Service ascolta sulla porta 5000 e indirizza il traffico verso la stessa porta sui Pod di destinazione. Sia la porta del Service (port) che la porta di destinazione (targetPort) sono impostate a 5000, il che è tipico per il Sentinel di Redis.

Il campo selector definisce un criterio di selezione dei Pod gestiti dal Service, usando l'etichetta app: sentinel. Questo permette al Service di indirizzare il traffico verso tutti i Pod che eseguono il servizio Sentinel di Redis all'interno del namespace redis-ns.

**Applicazione Manifesto**
```bash
kubectl apply -f s-service.yaml
```

### statefulset.yaml 
La versione dell'API è apps/v1 e il tipo di oggetto è StatefulSet. I metadati specificano il nome redis e il namespace redis-ns, che organizza e isola le risorse nel cluster Kubernetes.

La specifica (spec) definisce che questo StatefulSet utilizza un servizio chiamato redis per il networking e ha tre repliche. Il selector utilizza l'etichetta app: redis per identificare i Pod gestiti dallo StatefulSet. La sezione template contiene la definizione dei Pod, compresi i metadati con le etichette e la specifica del Pod.

Nella specifica del Pod, è definito un initContainer chiamato config che esegue operazioni di configurazione prima di avviare il container principale di Redis. Questo initContainer utilizza l'immagine redis:7.0.10-alpine e copia un file di configurazione Redis nella directory corretta. Cerca poi di determinare il master Redis utilizzando Sentinel, aggiornando la configurazione del file redis.conf per impostare il nodo corrente come replica del master individuato.

Il container principale, denominato redis, utilizza anch'esso l'immagine redis:7.0.10-alpine e avvia il server Redis utilizzando il file di configurazione precedentemente aggiornato. Il container espone la porta 6379, che è la porta standard di Redis, e monta i volumi necessari per la configurazione e i dati.

I volumi sono definiti nella sezione volumes. Un volume temporaneo (emptyDir) viene utilizzato per il file di configurazione Redis, mentre un ConfigMap chiamato redis-config fornisce i file di configurazione iniziali. I dati persistenti sono gestiti tramite volumeClaimTemplates, che specifica un volume di storage con accesso in modalità ReadWriteOnce e una dimensione richiesta di 64Mi.

**Applicazione Manifesto**
```bash
kubectl apply -f statefulset.yaml 
```
### sentinel-statefulset.yaml 
La versione dell'API è apps/v1 e il tipo di oggetto è StatefulSet. I metadati specificano il nome sentinel e il namespace redis-ns, che organizza e isola le risorse nel cluster Kubernetes.

Nella specifica (spec), serviceName: sentinel indica che questo StatefulSet utilizza il servizio chiamato sentinel per il networking. Il numero di repliche è configurato su 3 (replicas: 3). Il selettore (selector) utilizza l'etichetta app: sentinel per identificare i Pod gestiti dallo StatefulSet.

La sezione template definisce il modello per la creazione dei Pod. I metadati del Pod includono l'etichetta app: sentinel. La specifica del Pod include anche un initContainer chiamato config che esegue operazioni di configurazione prima di avviare il container principale di Sentinel Redis.

Questo initContainer utilizza l'immagine redis:7.0.10-alpine e esegue un processo per identificare il master Redis tra i nodi disponibili (redis-0.redis, redis-1.redis, redis-2.redis). Utilizza il comando redis-cli per interrogare ciascun nodo e determinare quale nodo sia il master effettivo. Una volta identificato il master, crea un file di configurazione sentinel.conf che specifica le configurazioni necessarie per il Sentinel, inclusi parametri come la porta di ascolto, le configurazioni di failover e l'autenticazione con la password di Redis.

Il container principale, chiamato sentinel, utilizza anch'esso l'immagine redis:7.0.10-alpine e avvia il processo di Sentinel Redis utilizzando il file di configurazione generato. Il container espone la porta 5000, che è la porta standard per Sentinel Redis, e monta i volumi necessari per la configurazione e i dati.

I volumi sono definiti nella sezione volumes. Un volume temporaneo (emptyDir) viene utilizzato per il file di configurazione sentinel.conf, mentre i dati persistenti sono gestiti tramite volumeClaimTemplates. Questo specifica un volume di storage con accesso in modalità ReadWriteOnce e una dimensione richiesta di 64Mi.

**Applicazione Manifesto**
```bash
kubectl apply -f sentinel-statefulset.yaml 
```
## Test 
Per un corretto punto di vista dello stato del nostro cluster possiamo applicare il comado 

```bash
minikube dashboard -p redis-cluster
```
in seguito dalla dalla cli di visualstudio possiamo applicare il comado 
```bash
kubectl get all -o wide
```
per notare tutti  gli oggetti e le loro repliche al interno del nostro namespace.

Per comprendere la individuazione del master e verificare la corretta sincronizzazione dei pod tra di loro e con le sentinel, utilizzare il seguente comando da terminale
```bash
kubectl logs redis-0
```
Questo comando restituirà i log del container all'interno del pod chiamato redis-0. I log sono utili per monitorare l'attività e identificare eventuali problemi relativi alla configurazione, alla sincronizzazione dei dati o alla connessione con le sentinel nel cluster Redis.

Una volta completati gli accertamenti preliminari, è possibile procedere con il failover e il testing del corretto funzionamento nel seguente modo:

1. Elimina il pod redis-0 utilizzando il comando:
   ```bash
   kubectl logs redis-0
   ```
   Questo comando rimuove il pod redis-0 dal cluster.
   
2. Successivamente, attendi che uno dei pod slave disponibili venga eletto come nuovo master dal sistema di gestione dei failover Sentinel. Questo processo avviene      automaticamente secondo le configurazioni di Sentinel.

3. Verifica che il nuovo master sia stato correttamente sincronizzato con i dati tramite l'operazione delle Sentinel.

4. Dopo aver completato il failover, verifica il funzionamento complessivo eseguendo il comando di log sui pod di interesse. Ad esempio, per visualizzare i log di un 
   pod specifico, puoi utilizzare:
   ```bash
   kubectl logs <nome-pod>
   ```

Per accedere ai database Redis all'interno del nostro cluster utilizzando kubectl exec, segui questi passaggi:
Esegui il comando per accedere al prompt interattivo all'interno del container Redis di redis-1:
 ```bash
kubectl exec -it redis-n -- redis-cli
```
Questo comando aprirà una sessione interattiva all'interno del pod redis-n utilizzando il client Redis.

Una volta all'interno della sessione interattiva di redis-cli, puoi eseguire diversi comandi per interagire con il database Redis. Alcuni esempi di comandi utili sono:
Visualizzare tutte le chiavi nel database:
``` redis
Copia codice
keys *
```
Questo comando elenca tutte le chiavi presenti nel database.

Ottenere il valore di una chiave specifica:
```redis
get <nome_chiave>
```
Sostituisci <nome_chiave> con il nome della chiave di cui desideri ottenere il valore.

Inserire o aggiornare il valore di una chiave:
```redis
set <nome_chiave> <valore>
```
Questo comando imposta il valore specificato per la chiave indicata.

Eliminare una chiave:
``` redis
del <nome_chiave>
```
Questo comando elimina la chiave specificata dal database.

Controllare la scadenza di una chiave:
```redis
ttl <nome_chiave>
```
Questo comando restituisce il tempo di vita rimanente di una chiave con scadenza.

## Consderazioni 
Questo progetto si è dimostrato significativo non solo per l'implementazione di Redis con architettura master-slave e Sentinel su Minikube, ma anche per l'introduzione all'approccio del cloud computing e l'acquisizione di nuove conoscenze.

L'utilizzo di Kubernetes su Minikube ha fornito un ambiente controllato e sicuro per lo sviluppo e il testing delle capacità di Redis, consentendo di esplorare l'orchestrazione dei container e le metodologie di gestione delle risorse. Questo ha permesso di acquisire familiarità con le best practices per il deployment e la gestione dei dati in memoria, essenziali per applicazioni che richiedono alta disponibilità e prestazioni elevate.

È importante notare che Minikube ha alcune limitazioni rispetto a una piattaforma cloud. Per esempio, Minikube non può interfacciarsi direttamente con risorse esterne come servizi cloud pubblici, come invece può fare un cluster Kubernetes su una piattaforma cloud. Questo implica che alcune funzionalità avanzate come l'integrazione con servizi di archiviazione esterna o il routing del traffico esterno potrebbero non essere completamente supportate o testabili in un ambiente locale come Minikube.

Tutto ciò che è stato sviluppato durante questo progetto rappresenta comunque un solido punto di partenza per un'eventuale migrazione o ampliamento verso un ambiente di produzione più complesso. Con le opportune modifiche per adattarsi a un ambiente cloud con risorse maggiori, come un cluster Kubernetes su una piattaforma cloud, questo setup può essere ottimizzato per gestire carichi di lavoro più intensivi e migliorare l'affidabilità del sistema.

In conclusione, l'implementazione di Redis su Minikube con architettura master-slave e Sentinel ha fornito un'importante base di conoscenze per esplorare scenari più avanzati nel contesto del cloud computing.
