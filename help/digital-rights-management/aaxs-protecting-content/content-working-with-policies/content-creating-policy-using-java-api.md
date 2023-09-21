---
title: Creazione di un criterio utilizzando l’API Java
description: Creazione di un criterio utilizzando l’API Java
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Creazione di un criterio utilizzando l’API Java {#creating-a-policy-using-the-java-api}

Per creare un criterio utilizzando l’API Java, effettua le seguenti operazioni:

1. Configura l’ambiente di sviluppo e includi tutti i file JAR menzionati in [Configurazione dell’ambiente di sviluppo](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) all’interno del progetto.
1. Creare un `com.adobe.flashaccess.sdk.policy.Policy` e specificarne le proprietà, ad esempio i diritti, la durata della memorizzazione nella cache della licenza e la data di fine del criterio.

   ```java
     // Create a new Policy object.  
     // False indicates the policy does not use license chaining.  
     Policy policy = new Policy(false);  
   
     policy.setName("DemoPolicy");  
   
     // Specify that the policy requires authentication to obtain a license.  
     policy.setLicenseServerInfo  
      (new LicenseServerInfo(AuthenticationType.UsernamePassword));  
   
     // A policy must have at least one Right, typically the play right  
     PlayRight play = new PlayRight();  
   
     // Users may only view content for 24 hours.  
     play.setPlaybackWindow(24L * 60 * 60);  
   
     // Add the play right to the policy.  
     List<Right> rightsList = new ArrayList<Right>();  
     rightsList.add(play);  
     policy.setRights(rightsList);  
   
     // Licenses may be stored on the client for 7 days after downloading  
     policy.setLicenseCachingDuration(7L * 24 * 60 * 60);  
     try {  
      // Content will expire December 31, 2010  
      SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");  
      policy.setPolicyEndDate(dateFormat.parse("2010-12-31"));  
     } catch (ParseException e) {  
      // Invalid date specified in dateFormat.parse()  
      e.printStackTrace();  
     }
   ```

1. Serializzare `Policy` e memorizzarlo in un file o database.

   ```java
     // Serialize the policy  
     byte[] policyBytes = policy.getBytes();  
     System.out.println("Created policy with ID: " + policy.getId());  
   
     // Write the policy to a file.   
     // Alternatively, the policy may be stored in a database.  
     FileOutputStream out = new FileOutputStream("demopolicy.pol");  
     out.write(policyBytes);  
     out.close();
   ```

Per l&#39;origine completa del codice di esempio, vedi *com.adobe.flashaccess.samples.policy.CreatePolicy* negli Strumenti della riga di comando per l’implementazione di riferimento &quot; [!DNL samples]&quot;.
