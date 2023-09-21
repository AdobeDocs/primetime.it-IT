---
description: Per implementare DRM è necessario disporre di certificati e chiavi specifici, tra cui una chiave di crittografia del contenuto o un CEK per crittografare il contenuto, un autenticatore del cliente per la protezione delle comunicazioni con i server ExpressPlay e CEKSID per l'identificazione delle chiavi di crittografia del contenuto archiviate in un sistema di gestione delle chiavi.
title: Chiavi, ID e autenticatori
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# Chiavi, ID e autenticatori{#keys-ids-and-authenticators}

Per implementare DRM è necessario disporre di certificati e chiavi specifici, tra cui una chiave di crittografia del contenuto o un CEK per crittografare il contenuto, un autenticatore del cliente per la protezione delle comunicazioni con i server ExpressPlay e CEKSID per l&#39;identificazione delle chiavi di crittografia del contenuto archiviate in un sistema di gestione delle chiavi.

Per creare pacchetti, concedere licenze e riprodurre contenuti protetti sono necessari i seguenti elementi:

## Chiave crittografia contenuto {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

La chiave di crittografia del contenuto (CEK, Content Encryption Key) è una stringa di 16 byte utilizzata per la crittografia del contenuto.

**Che cos&#39;è il CEK?** - Il codice CEK è la chiave che il vostro packager usa per crittografare il vostro contenuto. È una stringa codificata esadecimale a 16 byte.

**Da dove viene il CEK?** : il provider di contenuti crea autonomamente questa chiave utilizzando uno strumento come OpenSSL o Notepad++. Ad esempio:

```
openssl rand 16 -hex > cek_hex_file
```

o (ad Adobe Offline Packager):

1. Genera la stringa con codifica esadecimale a 16 byte, come sopra o utilizzando un altro strumento. Avrà un aspetto simile al seguente:

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. Aprire il Blocco note++ quindi incollarlo nella stringa esadecimale da 16 byte.
1. Converte questo valore da ASCII esadecimale con codifica Base64 per creare il [!DNL keyfile.bin]. (Questo argomento è trattato in [](../../multi-drm-workflows/quick-start/package-your-content.md).)

**Stessa chiave, nome diverso?** - Sì, è possibile che il codice CEK venga visualizzato con altri nomi in altre posizioni, ad esempio:

* ** [!DNL [some file].bin]** - L&#39;Adobe Offline Packager fa riferimento al CEK come [!DNL [some file].bin]; ad esempio, * [!DNL Keyfile.bin]* - Questo è il vostro CEK come usato dall&#39;Adobe Offline Packager, sotto forma di un file sulla macchina che si utilizza per il confezionamento del contenuto.

  &quot;Base64&quot; la stringa esadecimale CEK casuale e la salvi come file (ad es. [!DNL keyfile.bin]), in genere posizionato nel [!DNL creds] directory sotto [!DNL offlinepkgr/]. Nel file di configurazione Packager (ad esempio, è possibile chiamarlo [!DNL widevine.xml] se si sta creando un pacchetto per Widevine DRM), fare riferimento al codice CEK nel file di configurazione in questo modo:

  ```
  <config>  
    <in_path>sample.mp4</in_path>  
    <out_type>dash</out_type>
    <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
    […] 
  </config> 
  ```

* **Chiave contenuto** - Il codice CEK potrebbe anche essere indicato come chiave di contenuto nelle chiamate ( `&contentKey=`), nei messaggi di errore, nei ticket di supporto e in altra documentazione.

**Quando/dove si utilizza?**

1. In primo luogo, è necessario avere il CEK disponibile sulla macchina su cui si sta facendo la confezione. Lo strumento di creazione pacchetti utilizza il codice CEK per crittografare il contenuto.
1. In secondo luogo, è necessario memorizzare il CEK in una forma di sistema di gestione delle chiavi (KMS), con ogni CEK associato al proprio [Chiave crittografia contenuto](../../multi-drm-workflows/glossary/glossary-cek.md). Puoi creare un KMS personalizzato, oppure utilizzare [Archiviazione delle chiavi di ExpressPlay](https://www.expressplay.com/developer/key-storage/). In questo modo la vetrina (il server di adesione, che gestisce il diritto dei clienti e il provisioning del token di licenza) può richiamare un token di licenza per il cliente dal KMS utilizzando un ID chiave invece del CEK effettivo (molto più sicuro).

## ID archiviazione chiave di crittografia contenuto {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

Il Content Encryption Key Storage ID (CEKSID) identifica in modo univoco la chiave memorizzata che decrittografa un contenuto video crittografato.

**Cos’è il CEKSID?** : CEKSID è l’identificatore univoco di una chiave di crittografia del contenuto (CEK). Il CEK è necessario per sbloccare il contenuto protetto; il CEKSID è necessario per accedere al CEK da dove è memorizzato. Quando si esegue il test della configurazione, è possibile fornire un CEKSID e un CEK casuali al momento della creazione del pacchetto, purché si utilizzino le stesse informazioni per i controlli di licenza e riproduzione.

**Da dove viene?** : tu (il provider di contenuti) puoi creare questo ID personalmente o puoi utilizzare un servizio come [Archiviazione delle chiavi di ExpressPlay](https://www.expressplay.com/developer/key-storage/) per generare CEKSID per ciascuno dei CEK (e archiviarli entrambi). Inoltre, puoi utilizzare CEKSID generati in modo casuale o utilizzare uno schema adatto al tuo modello di business. Ad esempio, puoi utilizzare CEKSID che sono stringhe significative piuttosto che stringhe esadecimali casuali (il nome ID può essere costituito da soggetti, date, ore, ecc.)

**Cos’altro si chiama il CEKSID?** - è talvolta indicato come *ID contenuto*.

## Autenticatore del cliente {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

L&#39;autenticatore del cliente è una chiave che si ottiene da ExpressPlay quando si imposta un account amministratore. L&#39;autenticatore viene utilizzato nelle comunicazioni con i server ExpressPlay.

**Cosa sono gli autenticatori del cliente?** - I due autenticatori del cliente formano la coppia di ID — uno per il test, uno per la produzione — che ExpressPlay registra al momento dell&#39;iscrizione al servizio. Sono sempre disponibili nella pagina di amministrazione di ExpressPlay:
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**Quando lo utilizzo?** - L&#39;utente include questo valore in tutte le chiamate ai server ExpressPlay, ad esempio i server di licenze, [Archiviazione chiavi ExpressPlay](https://www.expressplay.com/developer/key-storage/), e altre chiamate.
