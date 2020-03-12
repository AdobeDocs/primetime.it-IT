---
seo-title: Cifratura delle chiavi asimmetriche
title: Cifratura delle chiavi asimmetriche
uuid: 0aae25f1-a609-4c73-9aef-13f8ae63f6e1
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Cifratura delle chiavi asimmetriche{#asymmetric-key-encryption}

La cifratura delle chiavi asimmetriche (o cifratura delle chiavi pubbliche) utilizza coppie di chiavi. Una chiave è utilizzata per la crittografia; l&#39;altro per la decrittazione. La chiave di decrittazione viene mantenuta segreta e viene definita chiave ** privata. La chiave di crittografia, detta chiave ** pubblica, viene messa a disposizione di chiunque sia autorizzato a crittografare il contenuto. Chiunque abbia accesso alla chiave pubblica è in grado di cifrare il contenuto, ma solo chi ha accesso alla chiave privata può decrittografare il contenuto. Impossibile ricostruire la chiave privata dalla chiave pubblica.

Quando si crea il pacchetto di contenuto, la chiave pubblica del server licenze viene utilizzata per crittografare la chiave di crittografia del contenuto (CEK) nei metadati DRM. È necessario assicurarsi che solo il server licenze abbia accesso alla chiave privata del server licenze; se qualcun altro dispone della chiave, può decrittografare e visualizzare il contenuto.

***Attenzione:**Assicurarsi di ottenere il certificato del server licenze (contenente la chiave pubblica) da un&#39;origine affidabile, in modo da essere certi che si tratti della chiave del server licenze e non di una chiave pubblica non in linea. Se un utente malintenzionato dovesse sostituire la chiave pubblica con quella del server licenze, potrebbe decifrare il contenuto.*

Per ulteriori informazioni sulla creazione di pacchetti di contenuto, consulta *Utilizzo di Adobe Access SDK per la protezione dei contenuti*.
