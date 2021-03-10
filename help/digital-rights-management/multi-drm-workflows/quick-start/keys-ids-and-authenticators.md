---
description: Per implementare DRM è necessario disporre di cert e chiavi particolari, tra cui una chiave di crittografia del contenuto o CEK per crittografare il contenuto, un autenticatore del cliente per la protezione delle comunicazioni con i server ExpressPlay e CEKSID per identificare le chiavi di crittografia del contenuto come memorizzate in un sistema di gestione delle chiavi.
title: Chiavi, ID e autenticatori
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---


# Tasti, ID e autenticatori{#keys-ids-and-authenticators}

Per implementare DRM è necessario disporre di cert e chiavi particolari, tra cui una chiave di crittografia del contenuto o CEK per crittografare il contenuto, un autenticatore del cliente per la protezione delle comunicazioni con i server ExpressPlay e CEKSID per identificare le chiavi di crittografia del contenuto come memorizzate in un sistema di gestione delle chiavi.

Per creare pacchetti, concedere licenze e riprodurre contenuti protetti è necessario disporre di questi elementi:

## Chiave di crittografia dei contenuti {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

La chiave di crittografia del contenuto (CEK) è una stringa di 16 byte utilizzata per la cifratura del contenuto.

**Cos&#39;è il CEK?** - Il CEK è la chiave utilizzata dal tuo packager per crittografare il tuo contenuto. È una stringa con codifica esadecimale a 16 byte.

**Da dove viene il CEK?** - Crea tu stesso questa chiave (il provider di contenuti) utilizzando uno strumento come OpenSSL o Notepad++. Ad esempio:

```
openssl rand 16 -hex > cek_hex_file
```

o (per l&#39;Adobe del pacchetto offline):

1. Genera la stringa con codifica esadecimale a 16 byte come sopra o utilizzando un altro strumento. Avrà un aspetto simile a questo:

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. Apri Notepad+++ e incolla la stringa esadecimale a 16 byte.
1. Converti questo valore da ASCII esadecimale con Codifica Base64 il valore per creare il [!DNL keyfile.bin]. (Questo è trattato in [](../../multi-drm-workflows/quick-start/package-your-content.md).)

**Stessa chiave, nome diverso?** - Sì, si può vedere il CEK indicato da altri nomi in altri luoghi, come:

* ** [!DNL [file].bin]** - L&#39;Adobe Offline Packager fa riferimento alla CEK come [!DNL [file].bin]; Ad esempio, * [!DNL Keyfile.bin]* - Questo è il vostro CEK utilizzato da Adobe Offline Packager, sotto forma di file sul computer utilizzato per il contenuto del packaging.

   Si &quot;Base64&quot; la stringa esadecimale CEK casuale e la si salva come file (ad esempio, [!DNL keyfile.bin]), in genere si trova nella directory [!DNL creds] sotto [!DNL offlinepkgr/]. Nel file di configurazione Packager (ad es., se stai effettuando il packaging per il DRM Widevine, puoi chiamarlo [!DNL widevine.xml], fai riferimento al tuo CEK nel file di configurazione come segue:

   ```
   <config>  
     <in_path>sample.mp4</in_path>  
     <out_type>dash</out_type>
     <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
     […] 
   </config> 
   ```

* **Chiave del contenuto** : puoi anche vedere la CEK indicata come Chiave del contenuto nelle chiamate (  `&contentKey=`), nei messaggi di errore, nei ticket di supporto e in altra documentazione.

**Quando / dove lo uso?**

1. In primo luogo, è necessario avere il CEK disponibile sulla macchina su cui si sta facendo il vostro imballaggio. Lo strumento di creazione dei pacchetti utilizza il CEK per crittografare il contenuto.
1. In secondo luogo, è necessario memorizzare la CEK in una qualche forma di sistema di gestione delle chiavi (KMS), con ogni CEK associato alla propria [chiave di crittografia dei contenuti](../../multi-drm-workflows/glossary/glossary-cek.md). È possibile creare un proprio KMS o utilizzare [Archiviazione chiave di ExpressPlay](https://www.expressplay.com/developer/key-storage/). Questo consente alla vetrina (il server di adesione, che gestisce l’adesione dei clienti e il provisioning del Token di licenza) di estrarre un token di licenza per il cliente dal servizio di gestione delle relazioni con i clienti utilizzando un ID chiave invece dell’effettivo CEK (questo è molto più sicuro).

## ID archiviazione chiave di crittografia del contenuto {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

L&#39;ID di archiviazione chiave di crittografia del contenuto (CEKSID) identifica in modo univoco la chiave memorizzata che decrittografa un contenuto video crittografato.

**Cos&#39;è il CEKSID?** - Il CEKSID è l&#39;identificatore univoco di una chiave di crittografia del contenuto (CEK). Il CEK è necessario per sbloccare il contenuto protetto; il CEKSID è necessario per accedere al CEK da dove è memorizzato. Quando si esegue il test della configurazione, è possibile fornire un CEKSID e CEK casuali al momento del Packaging, purché si utilizzino le stesse informazioni per i controlli di licenza e riproduzione.

**Da dove viene?** - Puoi creare questo ID tu stesso (il provider di contenuti) oppure puoi utilizzare un servizio come  [ExpressPlay Key ](https://www.expressplay.com/developer/key-storage/) Storagper generare i CEKSID per ciascuno dei CEK (e archiviarli entrambi). Inoltre, è possibile utilizzare CEKSID generati in modo casuale o utilizzare uno schema adatto al proprio modello di business. Ad esempio, puoi utilizzare CEKSID che sono stringhe significative anziché stringhe esadecimali casuali (il nome ID può essere composto da soggetti, date, ore, ecc.)

**Cos&#39;altro si chiama il CEKSID?** - A volte viene indicato come ID  *contenuto*.

## Utente autenticatore {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

L&#39;autenticatore del cliente è una chiave che si ottiene da ExpressPlay quando si configura un account amministratore. L&#39;autenticatore viene utilizzato nelle comunicazioni con i server ExpressPlay.

**Quali sono gli autenticatori del cliente?** - I due autenticatori dei clienti costituiscono la coppia di ID — uno per il test, uno per la produzione — che ExpressPlay registra per te quando ti iscrivi al loro servizio. Sono sempre disponibili nella pagina di amministrazione di ExpressPlay:
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**Quando uso questo?** - Questo è incluso in tutte le chiamate ai server ExpressPlay, ad esempio server di licenza,  [ExpressPlay Key Storage](https://www.expressplay.com/developer/key-storage/) e altre chiamate.
