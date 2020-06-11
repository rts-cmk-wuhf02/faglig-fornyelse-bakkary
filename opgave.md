jeg har haft nogle problemer ved henhold til at lave noget visuelt med cobol
siden det hovedsageligt bliver brugt til mainframe har jeg været nød til at kigge på nogle emulators eller andet for at køre med det
det har jeg ikke turde fordi jeg ikke kan finde en hjemmeside jeg tør downloade noget på og jeg betaler heller ikke for det
cobol er designet til at læse simple opgaver og ikke avanceret opgaver dette er både en fordel og en ulempe
noget så enkelt som at skrive 

PROCEDURE DIVISION.
   DISPLAY 'Hello World'.
STOP RUN.

ville i en compile skrive "hello world" og jeg ved godt at det er som ofte den første opgave man får i pretty much alle sprog
men siden at cobol er designed til at læse lette opgaver giver det virkelig god mening hvor "let" det er at bare komme igang og skrive
hvis vi lige tilføjer lidt mere til eksemplet kan vi skrive 

 
IDENTIFICATION DIVISION.
PROGRAM-ID. HELLO.
PROCEDURE DIVISION.
DISPLAY 'Cobol er et simpelt program'.
STOP RUN.

hvis vi så bruger jcl compileren og skriver 

//SAMPLE JOB(TESTJCL,XXXXXX),CLASS = A,MSGCLASS = C
//STEP1 EXEC PGM = HELLO

så vil den i sit "step1" exec pgm Hello hvilket betyder den vil exec=execute pgm=program HELLO

det vil sige hvis vi kigger på vores identification division kan vi se vi har et program med en ID der er HELLO
så compileren executer dette program hvilket ville "display" altså vise en linje hvor der stod "Cobol er et simpelt program"
og grunden til at vi altid ender den med "STOP RUN" er så vi kan fortælle vores compiler at der ikke er mere den skal arbejde med

vi kan bygge endnu mere videre på det ovenover

IDENTIFICATION DIVISION.
PROGRAM-ID. HELLO.

DATA DIVISION.
   WORKING-STORAGE SECTION.
   01 WS-NAME PIC A(30).
   01 WS-ID PIC 9(5) VALUE '12345'.

PROCEDURE DIVISION.
   A000-FIRST-PARA.
   DISPLAY 'Hello World'.
   MOVE 'TutorialsPoint' TO WS-NAME.
   DISPLAY "My name is : "WS-NAME.
   DISPLAY "My ID is : "WS-ID.
STOP RUN.

det kan godt virke lidt overvældende med alt muligt ligepludselig men bare tag 1 ting af gangen
vi ved hvad 
Identification Divisionen gør

og procedure division fortæller bare vores compiler hvad vi gerne vil køre igennem
vores data division er der hvor vi har den... ja data som vi bruger i vores procedure

så hvis vi går igennem procedure divisionen A000-FIRST-PARA den siger vores første paragraph skal display "Hello World"
så har vi vores "MOVE 'TutorialsPoint' TO WS-NAME." den siger vi skal rykke vores text "TutorialsPoint" til WS-NAME
så har vi en DISPLAY mere denne gang siger den vis "my name is": og så WS-NAME og siden vi har rykket TutorialsPoint til WS-name
så vil den vise "my name is: TutorialsPoint
og så siger den vis "my ID is": og så WS-ID`et hvis vi så kigger pååe i vores data division kan vi se at WS-ID har en value på 12345
så den vil vise os "my ID is: 12345

det vil sige hvis vi kører dette program i vores compiler ved at skrive
//SAMPLE JOB(TESTJCL,XXXXXX),CLASS = A,MSGCLASS = C
//STEP1 EXEC PGM = HELLO
i compileren
vil der stå

Hello World
My name is : TutorialsPoint
My ID is : 12345

og så har vi lavet noget data og hentet det data man kunne sagtens ændre på data divisionen både tilføje og fjerne
og så brude en data man laver i sin procedure division eller bare lave nogle strings man kan vise og så vores Identification division
bruges til at identificere hvad det er for et prgram vi kører vi kan sagtens give den et andet program ID men så skal vi huske når vi skal compile og køre den så skal vi også ændre vores "EXEC PGM ="vores nye navn" så vi skal huske at execute vores programs itentifications navn