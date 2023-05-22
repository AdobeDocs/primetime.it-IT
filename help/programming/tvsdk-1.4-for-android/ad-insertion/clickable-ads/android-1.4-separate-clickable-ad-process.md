---
description: Devi separare la logica dell’interfaccia utente del lettore dal processo che gestisce i clic sugli annunci. Un modo per farlo è implementare più frammenti per un’attività.
title: Separa il processo pubblicitario cliccabile
exl-id: 6519b8ed-2963-4708-bbb9-8ff178c1fa86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Separa il processo pubblicitario cliccabile{#separate-the-clickable-ad-process}

Devi separare la logica dell’interfaccia utente del lettore dal processo che gestisce i clic sugli annunci. Un modo per farlo è implementare più frammenti per un’attività.

1. Implementa un frammento per contenere il `MediaPlayer` e quale sarà responsabile della riproduzione del video.

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

1. Implementa un frammento diverso per visualizzare un elemento dell’interfaccia utente che indica che è possibile fare clic su un annuncio, monitorare tale elemento dell’interfaccia utente e comunicare i clic dell’utente al frammento che contiene `MediaPlayer`.

   Questo frammento deve dichiarare un’interfaccia per la comunicazione del frammento. Il frammento acquisisce l’implementazione dell’interfaccia durante il suo metodo del ciclo di vita onAttach e può chiamare i metodi dell’interfaccia per comunicare con l’attività.

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
