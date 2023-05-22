---
title: Creazione di un criterio DRM con API Java
description: Creazione di un criterio DRM con API Java
copied-description: true
exl-id: fcae76c3-4e51-449d-b6d5-2138bf1c583e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Creazione di un criterio DRM con API Java {#creating-a-drm-policy-with-the-java-api}

Per creare un criterio DRM con API Java:

1. Configura l’ambiente di sviluppo e includi nel progetto tutti i file JAR elencati in [Configura l’ambiente di sviluppo.](../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
1. Creare un `com.adobe.flashaccess.sdk.policy.Policy` e specificarne le proprietà, inclusi i diritti, la durata della memorizzazione nella cache della licenza e la data di fine del criterio DRM.

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

1. Serializzare il DRM `Policy` e memorizzarlo in un file o database.

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

Consulta [!DNL com.adobe.flashaccess.samples.policy.CreatePolicy] negli strumenti della riga di comando per l’implementazione di riferimento [!DNL samples] per l&#39;origine completa del codice di esempio.
