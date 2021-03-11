---
title: Crittografia delle chiavi asimmetriche
description: Crittografia delle chiavi asimmetriche
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Cifratura a chiave asimmetrica{#asymmetric-key-encryption}

La crittografia a chiave asimmetrica (o crittografia a chiave pubblica) utilizza coppie di chiavi. Per la crittografia viene utilizzata una chiave; l&#39;altro per la decrittografia. La chiave di decrittografia viene mantenuta segreta ed è indicata come *chiave privata*. La chiave di crittografia, denominata *chiave pubblica*, viene resa disponibile a chiunque sia autorizzato a crittografare i contenuti. Chiunque abbia accesso alla chiave pubblica è in grado di crittografare il contenuto, ma solo chi ha accesso alla chiave privata può decifrare il contenuto. Impossibile ricostruire la chiave privata dalla chiave pubblica.

Quando si crea il pacchetto di contenuto, la chiave pubblica del server licenze viene utilizzata per crittografare la chiave di crittografia del contenuto (CEK) nei metadati DRM. È necessario assicurarsi che solo il server licenze abbia accesso alla chiave privata del server licenze; se un altro utente dispone della chiave può decodificare e visualizzare il contenuto.

***Attenzione:**assicurarsi di ottenere il certificato del server licenze (contenente la chiave pubblica) da un&#39;origine attendibile in modo da essere certi che si tratti della chiave del server licenze e non di una chiave pubblica non valida. Se un autore dell&#39;attacco dovesse sostituire la propria chiave pubblica alla chiave del server licenze, potrebbe decifrare il contenuto.*

Per ulteriori informazioni sul contenuto del pacchetto, consulta *Utilizzo dell&#39;SDK di accesso Adobe per la protezione dei contenuti*.
