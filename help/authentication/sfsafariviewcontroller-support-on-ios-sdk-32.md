---
title: Supporto SFSafariViewController in iOS SDK 3.2+
description: Supporto SFSafariViewController in iOS SDK 3.2+
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Supporto SFSafariViewController in iOS SDK 3.2+ {#sfsafariviewcontroller-support-on-ios-sdk-3.2}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>


**A causa dei requisiti di sicurezza, alcune pagine di login di MVPD DEVONO essere presentate in un SFSafariViewController, invece che nelle visualizzazioni web.**

Alcuni MVPD richiedono che le loro pagine di login siano presentate in un controllo browser sicuro come SFSafariViewController. Stanno bloccando attivamente le visualizzazioni web, quindi per essere in grado di autenticare con loro dobbiamo utilizzare SVC. 

## Compatibilità {#compatiblity}

A partire dalla versione 3.1 dell&#39;SDK per iOS, AccessEnabler SDK visualizza automaticamente la pagina di accesso per MVPD specifici in un SFSafariViewController, in base alla configurazione del server.

La versione 3.1 dell&#39;SDK presenta automaticamente SFSafariViewController dal controller della visualizzazione radice dell&#39;applicazione. Anche se questo semplifica la gestione delle pagine di accesso per gli implementatori, ci sono casi in cui la presentazione di SFSafariViewController dal controller della visualizzazione principale non è possibile, a causa dell&#39;implementazione specifica dell&#39;app (come un controller modale già visibile).

Per questi casi, la versione 3.2 introduce la capacità del programmatore di gestire manualmente lo SVC.

## Gestione SVC manuale {#manual-svc-management}

Per gestire manualmente SVC, l’implementatore deve eseguire le seguenti operazioni:
 

1. chiamare **setOptions([&quot;handleSVC&quot;:true])** dopo l&#39;inizializzazione di AccessEnabler (assicurati che questa chiamata venga eseguita prima dell&#39;inizio dell&#39;autenticazione). In questo modo verrà attivata la gestione SVC &quot;manuale&quot;, l&#39;SDK non presenterà automaticamente l&#39;SVC, ma, quando necessario, chiamerà **naviga(toUrl:*{url}* useSVC:true)**.  

1. implementare il callback opzionale **navigaToUrl:useSVC:** all&#39;interno dell&#39;implementazione devi creare un&#39;istanza svc utilizzando l&#39;istanza SFSafariViewController utilizzando l&#39;url fornito e presentarla sullo schermo:

   ```obj-c
   func navigate(toUrl url: String!, useSVC: Bool) {
       svc =  SFSafariViewController(url: URL(string: url)!)
       svc.delegate = self
       myController.present(svc, animated: true)
       }
   ```

   ***Note:***

   - *Puoi personalizzare il SFSafariViewController nel modo desiderato. Ad esempio, in iOS 11+ puoi modificare l’etichetta &quot;Fine&quot; in &quot;Annulla&quot;.*
   - *per poter chiudere il svc, è necessario un riferimento ad esso, non crearlo nell&#39;ambito di **navigaToUrl:useSVC***
   - *utilizza il tuo controller di visualizzazione per &quot;myController&quot;*\
       

1. Nell&#39;implementazione delegata dell&#39;applicazione di **application(\_app: Applicazione UIA, url aperto: URL, opzioni: \[UIApplicationOpenURLOptionsKey: Any\]) -\> Bool**, aggiungi il codice per chiudere il svc. Dovresti già avere un codice che chiama **accessEnabler.handleExternalURL()**. Di seguito aggiungi:

   ```obj-c
   if(svc != nil) {
       svc.dismiss(animated: true)
   }
   ```

   Anche in questo caso, svc è un riferimento al SFSafariViewController creato al passaggio 2.\
    

1. Implementare **safariViewControllerDidFinish(\_ controller: SFSafariViewController)** da **SFSafariViewControllerDelegate** per rilevare quando l&#39;utente ha annullato l&#39;svc utilizzando il pulsante &quot;Fine&quot;. In questa funzione, per informare l&#39;SDK che l&#39;autenticazione è stata annullata, devi chiamare:

   ```obj-c
   accessEnabler.setSelectedProvider(nil)
   ```

