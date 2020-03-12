---
description: Separare la logica dell'interfaccia utente del lettore dal processo che gestisce i clic degli annunci. Un modo per farlo è implementare più frammenti per un'attività.
seo-description: Separare la logica dell'interfaccia utente del lettore dal processo che gestisce i clic degli annunci. Un modo per farlo è implementare più frammenti per un'attività.
seo-title: Separare il processo di annunci cliccabili
title: Separare il processo di annunci cliccabili
uuid: c37f5916-eb25-41ec-b5f4-efb82ec56371
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Separare il processo di annunci cliccabili {#separate-the-clickable-ad-process}

Separare la logica dell&#39;interfaccia utente del lettore dal processo che gestisce i clic degli annunci. Un modo per farlo è implementare più frammenti per un&#39;attività.

1. Implementare un frammento per contenere l&#39; `MediaPlayer`.

   Questo frammento deve essere chiamato `notifyClick()` e deve essere responsabile della riproduzione video.

   ```java
   public class PlayerFragment extends SherlockFragment { 
       ... 
       public void notifyAdClick () { 
           _mediaPlayer.notifyClick(); 
       } 
       ... 
   } 
   ```

1. Implementare un frammento diverso per visualizzare un elemento dell&#39;interfaccia utente che indica che un annuncio può essere cliccato, monitorare tale elemento dell&#39;interfaccia utente e comunicare i clic dell&#39;utente al frammento che contiene `MediaPlayer`.

   Questo frammento deve dichiarare un&#39;interfaccia per la comunicazione dei frammenti. Il frammento acquisisce l&#39;implementazione dell&#39;interfaccia durante il metodo `onAttach()` lifecycle e può chiamare i metodi dell&#39;interfaccia per comunicare con l&#39;attività.

   ```java
   public class PlayerClickableAdFragment extends SherlockFragment { 
       private ViewGroup viewGroup; 
       private Button button; 
       OnAdUserInteraction callback; 
       @Override 
       public View onCreateView(LayoutInflater inflater,  
                                ViewGroup container,  
                                Bundle savedInstanceState) { 
           // the custom fragment is defined by a custom button 
           viewGroup = (ViewGroup) inflater.inflate(R.layout.fragment_player_clickable_ad,  
                                                    container, false); 
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

