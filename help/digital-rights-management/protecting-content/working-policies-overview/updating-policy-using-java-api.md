---
seo-title: Aggiornamento di un criterio DRM con l'API Java
title: Aggiornamento di un criterio DRM con l'API Java
uuid: ec21351c-900e-48f5-845a-c0b430c210d7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Aggiornamento di un criterio DRM con l&#39;API Java {#updating-a-drm-policy-with-the-java-api}

Per aggiornare un criterio DRM con l&#39;API Java:

1. Configurate l&#39;ambiente di sviluppo e includete nel progetto tutti i file JAR elencati in [Impostazione dell&#39;ambiente](../../protecting-content/setting-up-the-sdk/setup-dev-env.md)di sviluppo.
1. Create un&#39; `Policy` istanza DRM e leggete il criterio DRM da un file o un database.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Aggiornare l&#39; `Policy` oggetto DRM impostandone le proprietà, ad esempio il nome e le regole di utilizzo.

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

1. Serializzare l&#39; `Policy` oggetto DRM aggiornato e archiviarlo in un file o in un database.

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

Consultate `com.adobe.flashaccess.samples.policy.UpdatePolicy` nella directory Strumenti della riga di comando Implementazione di riferimento [!DNL samples] l&#39;origine di questo codice di esempio.
