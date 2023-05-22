---
title: Aggiornamento di una policy DRM con API Java
description: Aggiornamento di una policy DRM con API Java
copied-description: true
exl-id: 00bb9b64-30f7-4900-b6bd-57604295b44d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Aggiornamento di una policy DRM con API Java {#updating-a-drm-policy-with-the-java-api}

Per aggiornare un criterio DRM con l’API Java:

1. Configura l’ambiente di sviluppo e includi nel progetto tutti i file JAR elencati in [Configurazione dell’ambiente di sviluppo](../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
1. Creare un DRM `Policy` e leggere il criterio DRM da un file o da un database.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Aggiornare il DRM `Policy` impostandone le proprietà, ad esempio il nome e le regole di utilizzo.

   ```java
   // Change the DRM policy name.  
   policy.setName("UpdatedDemoPolicy");  
   
   // Add DRM module restrictions to the play right  
   for (Right r: policy.getRights()) {  
       if (r instanceof PlayRight) {  
           PlayRight pr = (PlayRight) r;  
           // Disallow Linux versions up to and including 1.9.  Allow  
           // all other OSes and Linux versions above 1.9  
           VersionInfo toExclude = new VersionInfo();  
           toExclude.setOS("Linux");  
           toExclude.setReleaseVersion("1.9");  
           Collection<VersionInfo> exclusions = new ArrayList<VersionInfo>();  
           exclusions.add(toExclude);  
           ModuleRequirements drmRestrictions = new ModuleRequirements();  
           drmRestrictions.setExcludedVersions(exclusions);  
           pr.setDRMModuleRequirements(drmRestrictions);  
           break;  
       }  
   }
   ```

1. Serializzare il DRM aggiornato `Policy` e memorizzarlo in un file o database.

   ```java
   // Serialize the DRM policy.  
   byte[] policyBytes = policy.getBytes();  
   System.out.println("New DRM policy revision number: "  
       +  policy.getRevision());      
   // Write the DRM policy to a file.   
   // Alternatively, the DRM policy may be stored in a database.  
   FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
   out.write(policyBytes);  
   out.close();
   ```

Consulta `com.adobe.flashaccess.samples.policy.UpdatePolicy` negli strumenti della riga di comando per l’implementazione di riferimento [!DNL samples] per l&#39;origine di questo codice di esempio.
