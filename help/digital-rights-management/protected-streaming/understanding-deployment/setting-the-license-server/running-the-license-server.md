---
seo-title: Esecuzione del server DRM per lo streaming protetto
title: Esecuzione del server DRM per lo streaming protetto
uuid: 9bbe211d-268b-43c2-9e55-7ce62de40d30
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---


# Esecuzione del server DRM per lo streaming protetto {#running-the-drm-server-for-protected-streaming}

Prima di avviare Adobe Primetime DRM Server for Protected Streaming, è consigliabile verificare la validità delle impostazioni nei file di configurazione.

È possibile verificare la validità delle impostazioni utilizzando le utility fornite con il server licenze. (vedere Convalida della *configurazione* in questa guida.

Se si desidera avviare Tomcat e il server licenze, è necessario eseguire [!DNL catalina.bat start] o [!DNL catalina.sh start] dalla [!DNL bin] directory Tomcat.

Dopo l&#39;avvio del server, è necessario verificare che sia stato configurato correttamente aprendo [!DNL https://<lic<span></span>ense-server-host:port>/flashaccessserver/<tenant-name>/flashaccess/license/v1] in una finestra del browser. Se la configurazione del tenant è stata caricata correttamente, viene visualizzato un messaggio di conferma.

## File di registro {#log-files}

I file di registro generati da Adobe Primetime DRM Server for Protected Streaming application si trovano nella directory specificata da LicenseServer.LogRoot.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Se i file di registro correnti vengono eliminati o spostati durante l&#39;esecuzione del server, il file di registro potrebbe non essere ricreato. È pertanto possibile eliminare alcune informazioni di registro.

### Struttura delle directory di registro {#section_F490A483D60145ADBC21038914C39203}

Le directory di registro sono strutturate per semplificare l&#39;utilizzo. La directory di registro ha la struttura seguente:

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

Il file di registro globale, [!DNL flashaccess-global.log], si trova in *LicenseServer.LogRoot*. Il registro può includere messaggi di registro che l&#39;SDK Java DRM di Adobe Primetime o i messaggi di registro potrebbero essere stati generati durante il periodo in cui il server è stato inizializzato.

### File di registro delle partizioni {#section_5660137CD6AA40519E72A4315534846B}

Il file di registro della partizione, [!DNL flashaccess-partition.log], si trova nella [!DNL <LicenseServer.LogRoot>/flashaccesserver] directory. Include i messaggi di registro generati durante l&#39;elaborazione di una richiesta di licenza.

### File di registro tenant {#section_F0257CC0831647F18A746B4F02E3E910}

Il file di registro del tenant di ciascun tenant, [!DNL flashaccess-tenant.log], si trova in [!DNL &lt;LicenseServer.LogRoot>/flashaccesserver/locants/<tenantname>]. Il registro tenant include informazioni di controllo che descrivono ogni licenza generata per questo tenant.

## Aggiornamento dei file di configurazione {#updating-configuration-files}

Non appena il server licenze legge uno dei file di configurazione del server licenze (configurazione globale o tenant), le informazioni di configurazione vengono memorizzate nella cache. Pertanto i file non devono essere letti da disco per ogni richiesta di licenza. Tuttavia, il server consente anche di modificare la maggior parte dei valori nei file di configurazione senza che sia necessario riavviare il server per rendere attive le modifiche.

Ogni volta che modificate il file di configurazione, il server licenze memorizza l&#39;ora dell&#39;ultima modifica del file. A un intervallo configurabile, il server verifica se l&#39;ora di modifica del file è cambiata. Se è stato modificato, il server ricarica automaticamente il contenuto del file di configurazione.

Per controllare la frequenza con cui il server verifica la presenza di aggiornamenti, è necessario impostare l&#39; `refreshDelaySeconds` attributo nell&#39; `Caching` elemento del file di configurazione globale. Ad esempio, se `refreshDelaySeconds` è impostato su 3600 secondi, il server aggiorna la configurazione entro al massimo un&#39;ora dal momento in cui il file di configurazione viene modificato. Se `refreshDelaySeconds` è impostato su 0, il server verifica la disponibilità di aggiornamenti di configurazione a ogni richiesta. Non è consigliabile impostare `refreshDelaySeconds` un valore basso in qualsiasi ambiente di produzione, in quanto questo può influire sulle prestazioni.

L&#39; `Caching` elemento controlla anche quante configurazioni di tenant vengono memorizzate nella cache contemporaneamente. È possibile impostare questo valore su un numero inferiore al numero totale di tenant per limitare la quantità di memoria utilizzata per memorizzare nella cache le informazioni di configurazione. Se viene ricevuta una richiesta per un tenant che non si trova nella cache, la configurazione viene caricata prima che sia possibile elaborare la richiesta. Se la cache è piena, il tenant utilizzato meno di recente viene rimosso dalla cache.

La versione memorizzata nella cache della configurazione continua a essere utilizzata nelle seguenti situazioni (fino alla successiva verifica degli aggiornamenti da parte del server):

* Se una modifica viene salvata in un file di configurazione o in uno dei file di certificato a cui si fa riferimento nel [!DNL flashaccess-tenant.xml] file mentre il server tenta di leggere il file
* Se la marca temporale del file è inferiore a un secondo prima dell&#39;ora corrente
* Se la marca temporale del file è futura

In assenza di una versione memorizzata nella cache, il caricamento della configurazione non riesce e viene restituito un errore al client. Il server quindi tenta di caricare di nuovo il file alla successiva ricezione di una richiesta per quel tenant.

### Aggiornamento del file di configurazione globale {#section_AA546C72442646CFB8906AEEBDF50587}

È possibile modificare la password HSM in [!DNL flashaccess-global.xml] qualsiasi momento. Le modifiche avranno effetto alla successiva ricarica del file di configurazione da parte del server. Tuttavia, le modifiche apportate agli elementi Logging e Caching non vengono ricaricate. È necessario riavviare il server prima che eventuali modifiche per questi elementi diventino effettive.

### Aggiornamento del file di configurazione del tenant {#section_71624DB8DF28480F84F34F0FF7FD4365}

È possibile modificare tutti i valori specificati nel [!DNL flashaccess-tenant.xml] file in qualsiasi momento. Le modifiche avranno effetto alla successiva ricarica del file di configurazione da parte del server. Inoltre, il server verifica la presenza di eventuali modifiche in tutti i file di credenziali ( [!DNL .pfx]) e di packager per consentire file di certificati di elenco a cui viene fatto riferimento nel file di configurazione del tenant.