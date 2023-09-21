---
title: Aggiornamento di un criterio tramite API Java
description: Aggiornamento di un criterio tramite API Java
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Aggiornamento di un criterio tramite API Java {#updating-a-policy-using-the-java-api}

Per aggiornare un criterio utilizzando l’API Java, effettua le seguenti operazioni:

1. Configura l’ambiente di sviluppo e includi tutti i file JAR menzionati in [Configurazione dell’ambiente di sviluppo](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) all’interno del progetto.
1. Creare un `Policy` e letti nel criterio da un file o database.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Aggiornare il `Policy` impostandone le proprietà, ad esempio il nome e le regole di utilizzo.

   ```java
     // Change the policy name.  
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

1. Serializza il file aggiornato `Policy` e memorizzarlo in un file o database.

   ```java
      // Serialize the policy.  
      byte[] policyBytes = policy.getBytes();  
      System.out.println("New policy revision number: "  
       +  policy.getRevision());      
      // Write the policy to a file.   
      // Alternatively, the policy may be stored in a database.  
      FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
      out.write(policyBytes);  
      out.close(); 
   ```

Per l&#39;origine completa del codice di esempio, vedi `com.adobe.flashaccess.samples.policy.UpdatePolicy` nella directory &quot;samples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.
