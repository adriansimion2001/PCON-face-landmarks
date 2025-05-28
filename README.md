# Proiect MAX MSP: Redare de scnene audio pe baza expresiilor faciale

Proiectul are în prinm plan redarea dinamică (în timp real) a unor scene audio prestabilite pe baza schimbărilor de emoție, cu scopul de a permite interpretarea unei piese de teatru/ o reprezentație artistică live, fară a necesita prezența unui inginer de playback.

## Pentru a funcționa sunt necesare urmatoarele tool-uri ajutătoare:
*   MAX MSP 9 (compatibilitatea cu versiunile mai vechi nu este verificată) : https://cycling74.com/downloads
   ** MAX MSP necesită achiziția unei licențe, în schimb furnizorul oferă o vaiantă gratuită pentru 30 de zile (valabilă la momentul publicării repozitori-ului).
*   Prin intermediul Wekinator se va realiza antrenarea algoritmului de clasificare: http://www.wekinator.org
*   Data OSC este o aplicație disponibilă pe iOS și permite transmiterea coordonatelor faciale prin OSC in MAX : https://github.com/kylemcdonald/ofxFaceTracker/releases
*   Pentru demonstrație se va furniza și o colecție de fișiere audio, care ulterior pot fi înlocuite după bunul plac.

## (Utilizare)
...

## Etapele intermediare

## 15.05: 
În cadrul primului target am realizat o clasificare între "ochi deschiși"/"închisi". Problemele întampinate au fost din cauza numărului mare de puncte trimise (66 de coordonate x,y -> 132 numere la intrarea wekinator), astfel erau foarte multe înregistrari eronate (clasificarea era foarte zgomotoasă). De asemenea am decis să schimb aplicația care genera date osc din FaceOSC in Data OSC, deoarece prin intermediul FaceOSC datele erau aproximate folosind webcam-ul laptop-ului, în schimb aplicația Data OSC de pe iOS folosește senzorul de recunoaștere facială de pe iPhone, care este mult mai precis. De asemenea, aplicația Data OSC permite o transmitere selectivă a coordonatelor faciale, astfel nu vor mai fi trimise date nesemnificative care introduc zgomot în procesul de predicție.

## 29.05: 
În cel de-al doilea target am decis sa ma rezum la un numar de 5 "emoții"/trasături faciale (neutru, zâmbet, furie, surprindere, ochi închiși), iar datele OSC sunt mediate în prealabil în perechi (stânga-dreapta datorate simetriei feței), astfel wekinator va primi la intrare 5 numere reale cuprinse între [0,1] și va returna un număr întreg [1,5] corespunzător fiecărei expresii faciale. Prin această metodă rezultatele predicției sunt mult îmbunătățite, însă unele artefacte sunt în continuare prezente (tranziții eronate dintr-o stare în alta). Acest comportament însă ar putea fi folosit constructiv în reprezentații artistice, astfel până la varianta finala voi dori să implementezi un panou care să ii permită utilizatorului să selecteze dacă dorește să redea o scenă audio la fiecare tranziție sau să nu poată reda de mai multe ori aceeași scenă audio până când aceasta nu ajunge la finalul redării.

(X.06) ...

## (Link-uri)
...

# Dezvoltarea proiectului

Pentru început:
