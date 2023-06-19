# TemaMAX

In acest proiect m-am folosit de biblioteca jit pentru a pune intr-o fereastra imaginea extrasa de la camerea web a laptop-ului. Aceasta librarie se poate instala din package manager -> cv.jit. Autorul este Jean-Marc Pelletier si este o biblioteca folosita foarte mult in aplicatii de tip computer vision.

Fiecare preluare de cadru se face la 50 ms cu ajutorul blocului metro 50.
In blocul din stanga din patch-ul MAX am extras datele de la camera web prin obiectul jit.qt.grab si am inversat matricea prin jit.dimmap #invert 1.
La partea de procesare a imaginii am folosit jit.brcosa prin care putem modifica luminozitatea, contrastul si saturatia imaginii de la iesire.
Prin obiectul cv.jit.faces.draw am desenat un chenar de tip matrice cu 4 colturi pentru fiecare fata care apare in imagine (getnfaces ne ajuta la acest lucru).
Am rutat numarul fetelor care apar si in functie de acest counter am mers pe 2 branch-uri la iesire:
  - o fata: canta nota aferenta gamei alese si pozitiei fetei in imagine
  - 2 fete: canta acordul aferent gamei alese si pozitiei fetei initiale in imagine

Pentru a alege gama sau varianta mute am folosit un umenu si apoi mai multe blocuri if pentru a trimite root note catre keyslider.

Daca avem o fata detectata in imagine:
  - In functie de pozitia fetei in imagine, pe orizontala, de la stanga la dreapta, se incrementeaza root note cu +0, +4, +7 sau +12, pentru a crea notele unui acord major plecand de la nota initiala.
  - In functie de pozitia fetei in imagine, pe verticala, de sus in jos, se incrementeaza velocitatea notei.

Daca avem 2 sau mai multe fete detectate in imagine:
  - Se canta acordul aferent gamei alese si pozitiei fetei initiale in imagine (controalele sus-jos si stanga-dreapta nu sunt acceptate in acest mod)

Auditia semnalului de la iesire se poate face prin combinatia de blocuri makenote si noteout. Vizionarea intensitatii semnalului se poate face prin obiectul gain~.

Proiectul este setat sa inceapa in modul presentation si avem la dispozitie fereastra in care este extrasa camera, keyslider-ul pentru a viziona nota cantata, selectorul umenu pentru a putea selecta gama de interes si obiectul gain~ pentru a observa nivelul semnalului audio.
