---
seo-title: Aggiornamento di un criterio tramite l'API Java
title: Aggiornamento di un criterio tramite l'API Java
uuid: 23c50f05-799e-4f5a-869b-4b5e29a36ce1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Aggiornamento di un criterio tramite l&#39;API Java {#updating-a-policy-using-the-java-api}

Per aggiornare un criterio utilizzando l&#39;API Java, eseguire le operazioni seguenti:

1. Configurate l&#39;ambiente di sviluppo e includete tutti i file JAR menzionati in [Impostazione dell&#39;ambiente](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) di sviluppo all&#39;interno del progetto.
1. Create un&#39; `Policy` istanza e leggete il criterio da un file o da un database.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Aggiornare l&#39; `Policy` oggetto impostandone le proprietà, ad esempio il nome e le regole di utilizzo.

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

1. Serializzare l&#39; `Policy` oggetto aggiornato e archiviarlo in un file o in un database.

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

Per l&#39;origine completa di questo codice di esempio, vedere `com.adobe.flashaccess.samples.policy.UpdatePolicy` nella directory &quot;samples&quot; degli strumenti della riga di comando di implementazione di riferimento.
