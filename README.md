# Asistent pentru Trierea Defectelor - Fabrică Auto

O aplicație software dezvoltată în Java care modelează un sistem informatic de gestiune și automatizare a trierii defectelor utilajelor dintr-o fabrică auto. Sistemul analizează problemele raportate pe linia de producție și le alocă automat inginerilor de mentenanță pe baza unui set de reguli predefinite. 

Proiectul implementează principiile fundamentale de Programare Orientată pe Obiecte (OOP) — generalizare, compoziție și asociație — susținute de o arhitectură UML completă (diagrame de cazuri de utilizare, clase, activități și stări).

## Funcționalități Principale

* **Sistem de Autentificare și Roluri:** Aplicația folosește o ierarhie de utilizatori bazați pe clasa abstractă `Utilizator`. Există trei actori principali:
  * **Raportorul:** Operatorul de pe linie (ex. departamentul Sudură, Asamblare) care introduce datele problemei (titlu, descriere, mod reproducere, cod utilaj).
  * **Inginerul:** Specialistul (ex. Mecanic, Electric, Robotică) definit prin nivelul de experiență și numărul de defecte active, care preia și rezolvă problemele.
  * **Administratorul:** Gestionează regulile de triaj, adaugă ingineri noi în sistem și generează rapoarte globale.
* **Triaj Automat:** O componentă centrală (`AsistentTriaj`) analizează descrierea defectului folosind cuvinte-cheie (`RegulaTriaj`). Aceasta deduce automat componenta afectată, severitatea (CRITICA, MAJORA, MINORA, COSMETICA) și prioritatea (URGENTA, INALTA, MEDIE, SCAZUTA).
* **Asignare Inteligentă (Algoritm în Cascadă):** Asistentul evaluează toți inginerii disponibili și asignează defectul în funcție de specializarea necesară componentei afectate, nivelul minim de experiență cerut de severitate și încărcarea curentă a inginerului.
* **Trasabilitate și Istoric:** Orice defect parcurge un ciclu strict de stări (`NOU`, `IN_TRIAJ`, `ASIGNAT`, `IN_LUCRU`, `REZOLVAT`, `INCHIS`, `RESPINS`). Modificările de status, comentariile adăugate de utilizatori și deciziile algoritmului sunt salvate într-un istoric intern inseparabil de defect.
* **Generare Automată de Rapoarte:** La finalizarea unei intervenții, asistentul generează un raport complet de mentenanță (salvat ca fișier text), care include detaliile problemei, justificarea triajului automat, cronologia și istoricul detaliat. Administratorul poate salva, de asemenea, un raport global cu statistici asupra tuturor defectelor.

## Structura Proiectului (Core OOP)

* **`Main.java`**: Scenariu demonstrativ de utilizare, care simulează raportarea mai multor defecte, procesarea acestora, logarea utilizatorilor și generarea rapoartelor finale.
* **`Defect.java`**: Entitatea centrală a aplicației, care agregă informațiile problemei, relațiile cu inginerul și raportorul, istoricul (`IntrareIstoric`) și discuțiile atașate (`Comentariu`).
* **`AsistentTriaj.java` & `RegulaTriaj.java`**: Logica decizională. Asistentul conține o listă de reguli (compoziție) pe care le aplică pentru a sugera o rezolvare și a alege inginerul potrivit.
* **Utilizatori (`Utilizator.java`, `Raportor.java`, `Inginer.java`, `Administrator.java`)**: Modelarea generalizării. Clasele copil extind clasa de bază și adaugă comportament specific pentru fiecare tip de angajat din fabrică.
* **`Raport.java`**: Clasă responsabilă de agregarea textului și exportarea (scrierea pe disc) documentelor cu rezultatele mentenanței.
* **Enum-uri (`Status.java`, `Severitate.java`, `Prioritate.java`)**: Tipuri standardizate folosite pentru a asigura corectitudinea clasificărilor.
