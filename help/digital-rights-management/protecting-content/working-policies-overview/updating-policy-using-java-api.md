---
title: Aggiornamento di un criterio DRM con l’API Java
description: Aggiornamento di un criterio DRM con l’API Java
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Aggiornamento di un criterio DRM con API Java {#updating-a-drm-policy-with-the-java-api}

Per aggiornare un criterio DRM con l’API Java:

1. Imposta l&#39;ambiente di sviluppo e includi nel progetto tutti i file JAR elencati in [Impostazione dell&#39;ambiente di sviluppo](../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
1. Crea un&#39;istanza DRM `Policy` e leggi i criteri DRM da un file o da un database.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Aggiornare l’oggetto DRM `Policy` impostandone le proprietà, ad esempio il nome e le regole di utilizzo.

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

1. Serializzare l&#39;oggetto DRM aggiornato `Policy` e archiviarlo in un file o in un database.

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

Per l’origine di questo codice di esempio, vedi `com.adobe.flashaccess.samples.policy.UpdatePolicy` nella directory Strumenti della riga di comando per l’implementazione di riferimento [!DNL samples] .
