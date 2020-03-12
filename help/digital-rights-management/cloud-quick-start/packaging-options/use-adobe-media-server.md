---
seo-title: Usa Adobe Media Server
title: Usa Adobe Media Server
uuid: 272b9919-6ae4-4adb-aab5-28b1f92aa9fe
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Usa Adobe Media Server {#use-adobe-media-server}

Alcuni clienti potrebbero già usare Adobe Media Server e desiderano mantenere tale modello di distribuzione dei contenuti. In questo caso, i dati specifici di Primetime Cloud DRM richiesti possono essere raccolti da uno dei file di configurazione inclusi in questo kit per compilare la configurazione XML JIT (Just In Time) per AMS.

Ad esempio:

```xml
<?xml version="1.0"?>
<Application>
  <HDS>
    <HLS>
      <Encryption enabled="true" protection-scheme="AdobeAccessV4">
        <AdobeAccessV4>
          <ContentID>SampleVideo</ContentID>
          <CommonKeyPath>common-key.bin</CommonKeyPath>
          <LicenseServerURL>
            https://access.adobeprimetime.com/flashaccessserver/axs_prod
          </LicenseServerURL>
          <KeyServerURL>
            https://access.adobeprimetime.com:443/faxsks/axs_prod/key
          </KeyServerURL>
          <TransportCertPath>cert/Cloud DRM-transport.cer</TransportCertPath>
          <LicenseServerCertPath>cert/Cloud DRM-license.cer</LicenseServerCertPath>
          <PackagerCredentialPath>cert-from-adobe.pfx</PackagerCredentialPath>
          <PackagerCredentialPwd>pass-for-cert-from-adobe</PackagerCredentialPwd>
          <PolicyPath>policy_ios_localkeyserver.pol</PolicyPath>
        </AdobeAccessV4>
      </Encryption>
    </HLS>
  </HDS>
</Application>
```

