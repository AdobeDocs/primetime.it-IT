---
title: Esecuzione del server DRM per lo streaming protetto
description: Esecuzione del server DRM per lo streaming protetto
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# Esecuzione del server DRM per lo streaming protetto {#running-the-drm-server-for-protected-streaming}

Prima di poter avviare Adobe Primetime DRM Server for Protected Streaming, è consigliabile verificare la validità delle impostazioni nei file di configurazione.

È possibile verificare la validità delle impostazioni utilizzando le utilità fornite con il server licenze. (vedere *Convalida configurazione* in questa guida.

Per avviare Tomcat e il server licenze, è necessario eseguire [!DNL catalina.bat start] o [!DNL catalina.sh start] da Tomcat [!DNL bin] directory.

Dopo l&#39;avvio del server, è necessario verificare che sia stato configurato correttamente aprendo `https://<lic<span></span>ense-server-host:port>/flashaccessserver/<tenant-name>/flashaccess/license/v1` in una finestra del browser. Se la configurazione del tenant è stata caricata correttamente, viene visualizzato un messaggio di conferma.

## File di registro {#log-files}

I file di registro generati dall&#39;applicazione Adobe Primetime DRM Server for Protected Streaming si trovano nella directory specificata da LicenseServer.LogRoot.

>[!NOTE]
>
>Se i file di registro correnti vengono eliminati o spostati durante l&#39;esecuzione del server, è possibile che il file di registro non venga ricreato. Di conseguenza, alcune informazioni del registro potrebbero essere eliminate.

### Struttura della directory di registro {#section_F490A483D60145ADBC21038914C39203}

Le directory dei registri sono strutturate in modo da semplificarne l’utilizzo. La directory di registro ha la seguente struttura:

```
<i class="+ topic ph hi-d="" i "="">
 LicenseServer.LogRoot/ 
 flashaccess-global.log 
     flashaccessserver/ 
         flashaccess-partition.log 
         tenants/ 
             
 <i class="+ topic ph hi-d="" i "="">
  tenantname/ 
                  flashaccess-tenant.log
 </i class="+ topic>
</i class="+ topic>
```

### File di registro globale {#section_1CFA90748142439C9F3BE380969539DA}

Il file di registro globale, [!DNL flashaccess-global.log], si trova in *LicenseServer.LogRoot*. Il registro può includere messaggi di registro generati dall’SDK Java di Adobe Primetime DRM o messaggi di registro durante il periodo di inizializzazione del server.

### File di registro della partizione {#section_5660137CD6AA40519E72A4315534846B}

Il file di registro della partizione, [!DNL flashaccess-partition.log], si trova in `<LicenseServer.LogRoot>/flashaccesserver` directory. Include i messaggi di registro generati durante l’elaborazione di una richiesta di licenza.

### File di registro tenant {#section_F0257CC0831647F18A746B4F02E3E910}

File di registro tenant di ogni tenant, [!DNL flashaccess-tenant.log], si trova in `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. Il registro tenant include informazioni di audit che descrivono ogni licenza generata per questo tenant.

## Aggiornamento dei file di configurazione {#updating-configuration-files}

Non appena il server licenze legge uno dei file di configurazione del server licenze (configurazione globale o tenant), le informazioni di configurazione vengono memorizzate nella cache. Pertanto, i file non devono essere letti dal disco per ogni richiesta di licenza. Tuttavia, il server consente anche di modificare la maggior parte dei valori contenuti nei file di configurazione senza richiedere il riavvio del server per rendere effettive le modifiche.

Ogni volta che si modifica il file di configurazione, il server licenze memorizza l&#39;ora dell&#39;ultima modifica apportata al file. A un intervallo configurabile, il server controlla se il tempo di modifica del file è cambiato. Se è stato modificato, il server ricarica automaticamente il contenuto del file di configurazione.

Per controllare la frequenza con cui il server verifica la disponibilità di aggiornamenti, è necessario impostare `refreshDelaySeconds` attributo in `Caching` del file di configurazione globale. Ad esempio, se `refreshDelaySeconds` è impostato su 3600 secondi, il server aggiornerà la configurazione entro al massimo un&#39;ora dalla modifica del file di configurazione. Se `refreshDelaySeconds` è impostato su 0, il server controlla la disponibilità di aggiornamenti della configurazione a ogni richiesta. Non è consigliabile impostare `refreshDelaySeconds` a un valore ridotto in qualsiasi ambiente di produzione, in quanto ciò può influire sulle prestazioni.

Il `Caching` L&#39;elemento controlla anche il numero di configurazioni dei tenant memorizzate nella cache contemporaneamente. Puoi impostare questo valore su un numero inferiore al numero totale di tenant, in modo da limitare la quantità di memoria utilizzata per memorizzare nella cache le informazioni di configurazione. Se viene ricevuta una richiesta per un tenant non presente nella cache, la configurazione viene caricata prima che la richiesta possa essere elaborata. Se la cache è piena, il tenant utilizzato meno di recente viene rimosso dalla cache.

La versione cache della configurazione continua a essere utilizzata nelle seguenti situazioni (fino alla successiva verifica della disponibilità di aggiornamenti da parte del server):

* Se una modifica viene salvata in un file di configurazione o in uno dei file di certificato a cui si fa riferimento nel [!DNL flashaccess-tenant.xml] mentre il server tenta di leggere il file
* Se il timestamp del file risulta essere inferiore a un secondo prima dell’ora corrente
* Se la marca temporale del file è nel futuro

Se non è presente alcuna versione memorizzata nella cache, il caricamento della configurazione non riesce e viene restituito un errore al client. Il server tenta quindi di caricare di nuovo il file alla successiva richiesta per quel tenant.

### Aggiornamento del file di configurazione globale {#section_AA546C72442646CFB8906AEEBDF50587}

È possibile modificare la password HSM in [!DNL flashaccess-global.xml] in qualsiasi momento. Le modifiche diventano effettive al successivo ricaricamento del file di configurazione da parte del server. Tuttavia, le modifiche apportate agli elementi Logging e Caching non vengono ricaricate. È necessario riavviare il server prima che qualsiasi modifica apportata a questi elementi diventi effettiva.

### Aggiornamento del file di configurazione tenant {#section_71624DB8DF28480F84F34F0FF7FD4365}

È possibile modificare tutti i valori specificati in [!DNL flashaccess-tenant.xml] in qualsiasi momento. Le modifiche diventano effettive al successivo ricaricamento del file di configurazione da parte del server. Inoltre, il server verifica la presenza di eventuali modifiche in tutte le credenziali ( [!DNL .pfx]) file e file di certificato di elenco consentiti packager a cui viene fatto riferimento nel file di configurazione tenant.
