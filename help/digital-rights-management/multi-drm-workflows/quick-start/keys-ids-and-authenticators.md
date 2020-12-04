---
description: Per implementare DRM è necessario disporre di certificati e chiavi particolari, inclusa una chiave di crittografia del contenuto o CEK per crittografare il contenuto, un autenticatore cliente per proteggere le comunicazioni con i server ExpressPlay e CEKSID per identificare le chiavi di crittografia del contenuto come memorizzate in un sistema di gestione delle chiavi.
seo-description: Per implementare DRM è necessario disporre di certificati e chiavi particolari, inclusa una chiave di crittografia del contenuto o CEK per crittografare il contenuto, un autenticatore cliente per proteggere le comunicazioni con i server ExpressPlay e CEKSID per identificare le chiavi di crittografia del contenuto come memorizzate in un sistema di gestione delle chiavi.
seo-title: Tasti, ID e autenticatori
title: Tasti, ID e autenticatori
uuid: 9e5b1a64-b4e9-442f-ac15-26831aaf585d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 0%

---


# Tasti, ID e autenticatori{#keys-ids-and-authenticators}

Per implementare DRM è necessario disporre di certificati e chiavi particolari, inclusa una chiave di crittografia del contenuto o CEK per crittografare il contenuto, un autenticatore cliente per proteggere le comunicazioni con i server ExpressPlay e CEKSID per identificare le chiavi di crittografia del contenuto come memorizzate in un sistema di gestione delle chiavi.

Per creare pacchetti, ottenere licenze e riprodurre i contenuti protetti è necessario disporre dei seguenti elementi:

## Chiave di crittografia del contenuto {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

La chiave CEK (Content Encryption Key) è una stringa di 16 byte utilizzata per cifrare il contenuto.

**Cos&#39;è il CEK?** - CEK è la chiave utilizzata dal packager per cifrare il contenuto. È una stringa con codifica esadecimale a 16 byte.

**Da dove viene il CEK?** - Potete creare questa chiave voi stessi (il fornitore del contenuto) utilizzando uno strumento come OpenSSL o Notepad++. Ad esempio:

```
openssl rand 16 -hex > cek_hex_file
```

oppure (per il Adobe  Offline Packager):

1. Generare la stringa con codifica esadecimale a 16 byte, come sopra o utilizzando un altro strumento. Sarà simile a questo:

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. Aprite Notepad++ e incollate nella stringa esadecimale a 16 byte.
1. Converti questo valore da ASCII esadecimale con codifica Base64 il valore per creare il [!DNL keyfile.bin]. (Questo campo è compreso in [](../../multi-drm-workflows/quick-start/package-your-content.md).)

**Stessa chiave, nome diverso?** - Sì, si può vedere il CEK riferito da altri nomi in altri luoghi, come:

* ** [!DNL [file].bin]** - Il Packager offline  Adobe fa riferimento alla CEK come [!DNL [file].bin]; ad esempio * [!DNL Keyfile.bin]* - Questo è il CEK utilizzato dal  Adobe Offline Packager, sotto forma di file sul computer utilizzato per creare pacchetti di contenuto.

   &quot;Base64&quot; la stringa esadecimale CEK casuale e salvarla come file (ad esempio, [!DNL keyfile.bin]), in genere si trova nella directory [!DNL creds] sotto [!DNL offlinepkgr/]. Nel file di configurazione di Packager (ad esempio, è possibile chiamarlo [!DNL widevine.xml] se si crea un pacchetto per il DRM di Widevine), fare riferimento al CEK nel file di configurazione come segue:

   ```
   <config>  
     <in_path>sample.mp4</in_path>  
     <out_type>dash</out_type>
     <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
     […] 
   </config> 
   ```

* **Chiave**  di contenuto - È anche possibile che il CEK venga definito come una chiave di contenuto nelle chiamate (  `&contentKey=`), nei messaggi di errore, nei biglietti di supporto e in altra documentazione.

**Quando / dove lo uso?**

1. In primo luogo, è necessario avere il CEK disponibile sulla macchina su cui si sta facendo il vostro imballaggio. Lo strumento di creazione pacchetti utilizza CEK per cifrare il contenuto.
1. In secondo luogo, è necessario memorizzare CEK in una qualche forma di sistema di gestione delle chiavi (KMS), con ogni CEK associato a una propria [chiave di crittografia dei contenuti](../../multi-drm-workflows/glossary/glossary-cek.md). È possibile creare un proprio KMS o utilizzare [ExpressPlay&#39;s Key Storage](https://www.expressplay.com/developer/key-storage/). Questo consente al vostro storefront (il server di adesione, che gestisce l&#39;adesione dei clienti e il provisioning del token di licenza) di ottenere un token di licenza per il cliente dal KMS utilizzando un ID chiave invece del CEK effettivo (questo è molto più sicuro).

## ID archiviazione chiave di crittografia contenuto {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

L&#39;ID di archiviazione della chiave di crittografia dei contenuti (CEKSID) identifica in modo univoco la chiave memorizzata che decrittografa un contenuto video crittografato.

**Cos&#39;è il CEKSID?** - CEKSID è l&#39;unico identificatore di una chiave di crittografia dei contenuti (CEK). La CEK è necessaria per sbloccare il contenuto protetto; il CEKSID è necessario per accedere al CEK da cui è memorizzato. Durante il test della configurazione, è possibile fornire un CEKSID e CEK casuali al momento del Packaging, purché si utilizzino le stesse informazioni per i controlli di licenza e riproduzione.

**Da dove viene?** - È possibile creare questo ID autonomamente, oppure utilizzare un servizio come  [ExpressPlay&#39;s Key ](https://www.expressplay.com/developer/key-storage/) Storagper generare CEKSID per ciascuno dei CEK (e archiviarli entrambi). Inoltre, potete utilizzare i CEKSID generati in modo casuale, oppure utilizzare uno schema adatto al vostro modello di business. Ad esempio, potete utilizzare i CEKSID che sono stringhe significative anziché stringhe esadecimali casuali (il nome ID può essere composto da soggetti, date, ore ecc.)

**Come si chiama il CEKSID?** - Talvolta viene definito ID ** contenuto.

## Autenticazione cliente {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

L&#39;autenticatore del cliente è una chiave che si ottiene da ExpressPlay quando si configura un account amministratore. L&#39;autenticatore viene utilizzato nelle comunicazioni con i server ExpressPlay.

**Quali sono gli autenticatori cliente?** - I due autenticatori cliente costituiscono la coppia di ID — uno per il test, uno per la produzione che ExpressPlay si registri al momento dell&#39;accesso con il loro servizio. Sono sempre disponibili sulla pagina di amministrazione di ExpressPlay:
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**Quando uso questo?** - Includerlo in tutte le chiamate ai server ExpressPlay — ad esempio, server di licenze,  [ExpressPlay Key Storage](https://www.expressplay.com/developer/key-storage/) e altre chiamate.
