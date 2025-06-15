# Proiect MAX MSP: Redare de scene audio pe baza expresiilor faciale

Proiectul are în prim plan redarea dinamică (în timp real) a unor scene audio prestabilite pe baza schimbărilor de emoție, cu scopul de a permite interpretarea unei piese de teatru/ o reprezentație artistică live, fară a necesita prezența unui inginer de playback.

![image](https://github.com/user-attachments/assets/17164801-c297-4a57-9c97-eb73f118d9cf)



## Pentru a funcționa sunt necesare urmatoarele tool-uri ajutătoare:
*   MAX MSP 9 (compatibilitatea cu versiunile mai vechi nu este verificată) : https://cycling74.com/downloads
   ![image](https://github.com/user-attachments/assets/70984252-f63f-4e84-a03b-c66e64a91c79)
   ** MAX MSP necesită achiziția unei licențe, în schimb furnizorul oferă o vaiantă gratuită pentru 30 de zile (valabilă la momentul publicării repozitori-ului).
*   Prin intermediul Wekinator se va realiza antrenarea algoritmului de clasificare: http://www.wekinator.org
    <img width="698" alt="image" src="https://github.com/user-attachments/assets/e1bb7058-76d9-484e-96e2-8c88a727178f" />

*   Data OSC este o aplicație disponibilă pe iOS și permite transmiterea coordonatelor faciale prin OSC in MAX: https://apps.apple.com/us/app/data-osc/id6447833736
   <img width="518" alt="image" src="https://github.com/user-attachments/assets/a5552961-4cc6-43a0-8696-716ec5b536ee" />

*   Pentru demonstrație se va furniza și o colecție de fișiere audio, care ulterior pot fi înlocuite după bunul plac.

## Pașii de urmat:
* Inițial trebuie să clonăm local repository-ul. Mai apoi importăm în MAX MSP patch-ul din sectiunea source.
* Deschidem în paralel "wekinator" și importăm modelul deja antrenat din secțiunea /assets/model_antrenare_emotii. Butonul "run" trebuie de asemenea apăsat pentru a ne asigura că modelul nostru va prezice expresia bazat pe datele furnizate de DataOSC.
* Deschidem DataOSC pe telefonul mobil -> activăm funcția OSC și ne asigurăm că atât IP-ul prezentat în aplicație, cât și portul corespund cu laptop-ul de pe care am încărcat patch-ul, respectiv portului prevăzut în patch.
* Tot din aplicația DataOSC activăm FaceTracking și din submeniul blendShape ne asigurăm ca avem activate:
** browDownLeft, browDownRight; browOuterUpLeft, browOuterUpRight; eyeBlinkLeft, eyeBlinkRight; mouthSmileLeft, mouthSmileRight;
* Cu "drag and drop" aducem un director care să conțină sample-urile audio pe care dorim să le redăm (în cadrul repozitory-ului se află deja un director cu sample-uri de test în secțiunea /assets/Sound_library).
* Ne asigurăm că atribuim fiecărei expresii faciale pe care dorim să o folosim un sample și stabilim nivelul de redare dorit.
* Dacă toți pașii au fost urmați ar trebui să putem reda fișiere audio cu ajutorul propriilor expresii faciale.

## Etapele intermediare
## 15.05: 
În cadrul primului target am realizat o clasificare între "ochi deschiși"/"închisi". Problemele întampinate au fost din cauza numărului mare de puncte trimise (66 de coordonate x,y -> 132 numere la intrarea wekinator), astfel erau foarte multe înregistrari eronate (clasificarea era foarte zgomotoasă). De asemenea am decis să schimb aplicația care genera date osc din FaceOSC in Data OSC, deoarece prin intermediul FaceOSC datele erau aproximate folosind webcam-ul laptop-ului, în schimb aplicația Data OSC de pe iOS folosește senzorul de recunoaștere facială de pe iPhone, care este mult mai precis. De asemenea, aplicația Data OSC permite o transmitere selectivă a coordonatelor faciale, astfel nu vor mai fi trimise date nesemnificative care introduc zgomot în procesul de predicție.

## 29.05: 
În cel de-al doilea target am decis sa ma rezum la un numar de 5 "emoții"/trasături faciale (neutru, zâmbet, furie, surprindere, ochi închiși), iar datele OSC sunt mediate în prealabil în perechi (stânga-dreapta datorate simetriei feței), astfel wekinator va primi la intrare 5 numere reale cuprinse între [0,1] și va returna un număr întreg [1,5] corespunzător fiecărei expresii faciale. Prin această metodă rezultatele predicției sunt mult îmbunătățite, însă unele artefacte sunt în continuare prezente (tranziții eronate dintr-o stare în alta). Acest comportament însă ar putea fi folosit constructiv în reprezentații artistice, astfel până la varianta finala voi dori să implementezi un panou care să ii permită utilizatorului să selecteze dacă dorește să redea o scenă audio la fiecare tranziție sau să nu poată reda de mai multe ori aceeași scenă audio până când aceasta nu ajunge la finalul redării.

## 16.06:
Pentru target-ul final am implementat o interfață grafică în modul de prezentare, care permite vizualizarea asupra imaginii de pe camera web a laptop-ului (camera web nu este implicată în procesul de detecție al expresiilor faciale, dar poate fi folosită pentru a putea realiza o incadrare corectă pentru a putea înregistra ulterior momentul artistic). De asemenea, interfața grafică este prevăzută cu un spațiu de tip "drag and drop" în care se poate aduce folder-ul cu semple-urile pe care dorim să le utilizăm. Patch-ul prevede 5 expresii faciale/emoții (zambet, furie, uimire, detectează închiderea ochilor, neutru). Pentru fiecare emoție în parte avem câte un "channel strip" pentru a putea modifica nivelul sample-urilor corespunzătoare fiecărei emoții. Tot în cadrul "channel strip-ului" avem un trigger care permite oprirea din redare a sample-ului în clipa în care trecem în starea neutră. Sample-urile se pot schimba în timp real, este nevoie doar ca toate fișierele audio folosite să se afle în același director care a fost importat anterior.

## Link-uri utilizate
MAX MSP: https://cycling74.com/downloads
Wekinator: http://www.wekinator.org
Data OSC: https://apps.apple.com/us/app/data-osc/id6447833736
