---
title: Creazione di un criterio DRM con l’API Java
description: Creazione di un criterio DRM con l’API Java
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Creazione di un criterio DRM con API Java {#creating-a-drm-policy-with-the-java-api}

Per creare un criterio DRM con l’API Java:

1. Configura l&#39;ambiente di sviluppo e includi nel progetto tutti i file JAR elencati in [Imposta l&#39;ambiente di sviluppo.](../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
1. Crea un oggetto `com.adobe.flashaccess.sdk.policy.Policy` e specifica le relative proprietà, compresi i diritti, la durata del caching delle licenze e la data di fine del criterio DRM.

   ```java
   // Create a new DRM policy object.  
   // False indicates the DRM policy does not use license chaining.  
   Policy policy = new Policy(false);  
   
   policy.setName("DemoPolicy");  
   
   // Specify that the DRM policy requires authentication to obtain a license.  
   policy.setLicenseServerInfo(new LicenseServerInfo(AuthenticationType.UsernamePassword));  
   
   // A DRM policy must have at least one Right, typically the play right  
   PlayRight play = new PlayRight();  
   
   // Users can only view content for 24 hours.  
   play.setPlaybackWindow(24L * 60 * 60);  
   
   // Add the play right to the DRM policy.  
   List<Right> rightsList = new ArrayList<Right>();  
   rightsList.add(play);  
   policy.setRights(rightsList);  
   
   // Licenses can be stored on the client for 7 days after downloading  
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

1. Serializzare l&#39;oggetto DRM `Policy` e archiviarlo in un file o in un database.

   ```java
   // Serialize the DRM policy  
   byte[] policyBytes = policy.getBytes();  
   System.out.println("Created DRM policy with ID: " + policy.getId());  
   
   // Write the DRM policy to a file.   
   // Alternatively, the DRM policy may be stored in a database.  
   FileOutputStream out = new FileOutputStream("demopolicy.pol");  
   out.write(policyBytes);  
   out.close(); 
   ```

Per l’origine completa di questo codice di esempio, vedi [!DNL com.adobe.flashaccess.samples.policy.CreatePolicy] nella directory Strumenti della riga di comando per l’implementazione di riferimento [!DNL samples] .
