---
seo-title: Creare un'interfaccia utente di autenticazione
title: Creare un'interfaccia utente di autenticazione
uuid: 4744bac0-c36e-4b0a-b3fb-d81c7f2e7617
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Creare un&#39;interfaccia utente di autenticazione {#create-an-authentication-ui}

1. Create un&#39;interfaccia utente per recuperare le credenziali di autenticazione dell&#39;utente.

   Di seguito è riportato un esempio Flex di semplice interfaccia utente per il recupero delle credenziali utente. È costituito da un oggetto del pannello contenente due oggetti `TextInput`, uno per ciascuna delle credenziali di nome utente e password. Il pannello contiene anche un pulsante che avvia il metodo `credentials()`.

   ```xml
   <mx:Panel x="236.5"  
             y="113"  
             width="325"  
             height="204"  
             layout="absolute"  
             title="Login">  
       <mx:TextInput x="110"  
                     y="46"  
                     id="uName"/>  
       <mx:TextInput x="110"  
                     y="76"  
                     id="pWord"  
                     displayAsPassword="true"/>  
       <mx:Text x="35"  
                y="48"  
                text="Username:"/>  
       <mx:Text x="35"  
                y="78"  
                text="Password:"/>  
       <mx:Button x="120"  
                  y="115"  
                  label="Login"  
                  click="credentials()"/>  
   </mx:Panel>  
   ```

1. Scrivere il metodo `credentials()` per elaborare i valori di autenticazione forniti dall&#39;utente.

   Il metodo `credentials()` è un metodo definito dall&#39;utente che trasmette i valori di nome utente e password al metodo `setDRMAuthenticationCredentials()`. Una volta passati i valori, il metodo `credentials()` reimposta i valori degli oggetti `TextInput`.

   ```
   <mx:Script> 
       <![CDATA[ 
         public function credentials():void { 
             videoStream.setDRMAuthenticationCredentials(uName, pWord, "drm"); 
             uName.text = ""; 
             pWord.text = ""; 
   } ]]> 
   </mx:Script> 
   ```

   Un modo per implementare questo tipo di interfaccia semplice è includere il pannello come parte di un nuovo stato. Il nuovo stato viene generato dallo stato base quando viene generato l&#39;oggetto `DRMAuthenticateEvent`. L&#39;esempio seguente contiene un oggetto `VideoDisplay` con un attributo di origine che punta a un file video protetto. In questo caso, il metodo `credentials()` viene modificato in modo che restituisca anche l&#39;applicazione allo stato di base. Questo metodo esegue questa operazione dopo aver passato le credenziali utente e aver reimpostato i valori dell&#39;oggetto TextInput.

   ```xml
   <?xml version="1.0" encoding="utf-8"?> 
   <mx:WindowedApplication xmlns:mx="https://www.adobe.com/2006/mxml" 
       layout="absolute" 
       width="800" 
       height="500" 
       title="DRM FLV Player" 
       creationComplete="initApp()" > 
       <mx:states> 
           <mx:State name="LOGIN"> 
               <mx:AddChild position="lastChild"> 
                       <mx:Panel x="236.5"  
                                 y="113"  
                                 width="325"  
                                 height="204"  
                                 layout="absolute"  
                                 title="Login"> 
                       <mx:TextInput x="110"  
                                     y="46"  
                                     id="uName"/> 
                       <mx:TextInput x="110"  
                                     y="76"  
                                     id="pWord"  
                                     displayAsPassword="true"/> 
                       <mx:Text x="35"  
                                y="48"  
                                text="Username:"/> 
                       <mx:Text x="35"  
                                y="78"  
                                text="Password:"/> 
                       <mx:Button x="120"  
                                  y="115"  
                                  label="Login"  
                                  click="credentials()"/> 
                       <mx:Button x="193"  
                                  y="115"  
                                  label="Reset"  
                                  click="uName.text=''; 
               </mx:Panel> 
           </mx:AddChild> 
       </mx:State> 
   </mx:states> 
   pWord.text='';"/> 
   
   <mx:Script> 
       <![CDATA[ 
           import flash.events.DRMAuthenticateEvent; 
           private function initApp():void { 
               videoStream.addEventListener(DRMAuthenticateEvent.DRM_AUTHENTICATE, 
                                            drmAuthenticateEventHandler); 
           } 
           public function credentials():void { 
               videoStream.setDRMAuthenticationCredentials(uName, pWord, "drm"); 
               uName.text = ""; 
               pWord.text = ""; 
               currentState=''; 
           } 
           private function drmAuthenticateEventHandler(event:DRMAuthenticateEvent):void { 
               currentState='LOGIN'; 
           } 
       ]]> 
   </mx:Script> 
   <mx:VideoDisplay id="video"  
                    x="50"  
                    y="25"  
                    width="700"  
                    height="350" 
                    autoPlay="true" 
                    bufferTime="10.0" 
                    source="https://www.example.com/flv/Video.flv" /> 
   </mx:WindowedApplication> 
   ```

