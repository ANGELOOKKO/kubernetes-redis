# Implementazione Cluster Minikube con Redis Master, Slave e Sentinel

Questo documento fornisce istruzioni dettagliate per configurare un cluster Minikube con Redis utilizzando Docker Desktop e Chocolatey su un sistema Windows.

## Capitolo 1: Installazione degli Strumenti Necessari

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
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))





