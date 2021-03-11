---
description: Separa la logica dell’interfaccia utente del lettore dal processo che gestisce i clic degli annunci. Un modo per farlo è quello di implementare più frammenti per un’attività.
title: Separa il processo degli annunci cliccabili
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Separa il processo degli annunci cliccabili{#separate-the-clickable-ad-process}

Separa la logica dell’interfaccia utente del lettore dal processo che gestisce i clic degli annunci. Un modo per farlo è quello di implementare più frammenti per un’attività.

1. Implementa un frammento contenente il `MediaPlayer` responsabile della riproduzione video.

   Questo frammento deve chiamare `notifyClick`.

   ```java
   public class PlayerFragment extends SherlockFragment { 
       ... 
       public void notifyAdClick () { 
           _mediaPlayer.notifyClick(); 
       } 
       ... 
   } 
   ```

1. Implementa un frammento diverso per visualizzare un elemento dell’interfaccia utente che indica che un annuncio è cliccabile, monitora tale elemento dell’interfaccia utente e comunica i clic dell’utente al frammento che contiene `MediaPlayer`.

   Questo frammento deve dichiarare un&#39;interfaccia per la comunicazione dei frammenti. Il frammento acquisisce l&#39;implementazione dell&#39;interfaccia durante il relativo metodo onAttach lifecycle e può chiamare i metodi dell&#39;interfaccia per comunicare con l&#39;attività.

   ```java
   public class PlayerClickableAdFragment extends SherlockFragment { 
       private ViewGroup viewGroup; 
       private Button button; 
       OnAdUserInteraction callback; 
   
       @Override 
       public View onCreateView(LayoutInflater inflater,  
                                ViewGroup container, Bundle 
                                savedInstanceState) { 
   
           // the custom fragment is defined by a custom button 
           viewGroup =  
             (ViewGroup) inflater.inflate(R.layout.fragment_player_clickable_ad, container, false); 
           button = (Button) viewGroup.findViewById(R.id.clickButton); 
   
           // register a click listener to detect user interaction 
           button.setOnClickListener(new View.OnClickListener() { 
               @Override 
               public void onClick(View v) { 
                   // send the event back to the activity 
                   callback.onAdClick(); 
               } 
           }); 
   
           viewGroup.setVisibility(View.INVISIBLE); 
           return viewGroup; 
       } 
   
       public void hide() { 
           viewGroup.setVisibility(View.INVISIBLE); 
       } 
   
       public void show() { 
           viewGroup.setVisibility(View.VISIBLE);  
       } 
   
       @Override 
       public void onAttach(Activity activity) { 
           super.onAttach(activity); 
           // attaches the interface implementation 
           // if the container activity does not implement the methods  
           // from the interface an exception will be thrown 
           try { 
               callback = (OnAdUserInteraction) activity; 
           } catch (ClassCastException e) { 
               throw new ClassCastException(activity.toString() 
               + " must implement OnAdUserInteraction"); 
           }  
       } 
   
       // user defined interface that allows fragment communication 
       // must be implemented by the container activity 
       public interface OnAdUserInteraction { 
           public void onAdClick(); 
       } 
   } 
   ```

