---
seo-title: Creazione di un criterio tramite l'API Java
title: Creazione di un criterio tramite l'API Java
uuid: c653548d-4abf-46b9-8669-d68b966da359
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Creazione di un criterio tramite l&#39;API Java {#creating-a-policy-using-the-java-api}

Per creare un criterio utilizzando l&#39;API Java, effettuate le seguenti operazioni:

1. Configurate l&#39;ambiente di sviluppo e includete tutti i file JAR menzionati in [Impostazione dell&#39;ambiente di sviluppo](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) all&#39;interno del progetto.
1. Create un oggetto `com.adobe.flashaccess.sdk.policy.Policy` e specificatene le proprietà, quali i diritti, la durata del caching delle licenze e la data di fine del criterio.

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

1. Serializzare l&#39;oggetto `Policy` e archiviarlo in un file o in un database.

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

Per l&#39;origine completa di questo codice di esempio, vedere *com.adobe.flashaccess.samples.policy.CreatePolicy* nella directory Reference Implementation Command Line Tools &quot;[!DNL samples]&quot;.
