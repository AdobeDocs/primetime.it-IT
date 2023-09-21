---
title: Crittografia a chiave asimmetrica
description: Crittografia a chiave asimmetrica
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Crittografia a chiave asimmetrica{#asymmetric-key-encryption}

La crittografia a chiave asimmetrica (detta anche crittografia a chiave pubblica) utilizza coppie di chiavi. Una chiave viene utilizzata per la crittografia, l&#39;altra per la decrittografia. La chiave di decrittografia viene mantenuta segreta e viene definita *chiave privata*. La chiave di crittografia, denominata *chiave pubblica*, è reso disponibile a chiunque sia autorizzato a crittografare i contenuti. Chiunque abbia accesso alla chiave pubblica è in grado di crittografare il contenuto, ma solo chi ha accesso alla chiave privata può decrittografare il contenuto. Impossibile ricostruire la chiave privata dalla chiave pubblica.

Quando si crea un pacchetto di contenuto, la chiave pubblica del server licenze viene utilizzata per crittografare la chiave di crittografia del contenuto (CEK) nei metadati DRM. È necessario assicurarsi che solo il server licenze abbia accesso alla chiave privata del server licenze; se un altro utente dispone della chiave, può decrittografare e visualizzare il contenuto.

***Attenzione:**Assicurarsi di ottenere il certificato del server licenze (contenente la chiave pubblica) da una fonte attendibile, in modo da essere certi che si tratti della chiave del server licenze e non di una chiave pubblica non valida. Se un utente malintenzionato dovesse sostituire la propria chiave pubblica con quella del server licenze, potrebbe decrittografare il contenuto.*

Per ulteriori informazioni sul contenuto della confezione, consulta *Utilizzo dell’SDK per l’accesso agli Adobi per la protezione dei contenuti*.
