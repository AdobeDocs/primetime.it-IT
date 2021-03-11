---
title: Aggiornamento di un criterio tramite l’API Java
description: Aggiornamento di un criterio tramite l’API Java
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Aggiornamento di un criterio tramite l’API Java {#updating-a-policy-using-the-java-api}

Per aggiornare un criterio utilizzando l’API Java, esegui i seguenti passaggi:

1. Configura l&#39;ambiente di sviluppo e includi tutti i file JAR menzionati in [Impostazione dell&#39;ambiente di sviluppo](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) all&#39;interno del progetto.
1. Crea un&#39;istanza `Policy` e legge nel criterio da un file o da un database.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Aggiornare l’oggetto `Policy` impostandone le proprietà, ad esempio il nome e le regole di utilizzo.

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

1. Serializzare l&#39;oggetto `Policy` aggiornato e archiviarlo in un file o in un database.

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

Per l’origine completa di questo codice di esempio, vedi `com.adobe.flashaccess.samples.policy.UpdatePolicy` nella directory &quot;amples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.
