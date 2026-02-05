# it_sikkerhed_2026f
### Intro til GIT i Softwaresikkerhed fag

<img width="1657" height="1418" alt="billede" src="https://github.com/user-attachments/assets/1e35266f-93c3-46a3-a05e-f904b726cd93" />

## Opgave - Test strategier

Emner inden for IT-sikkerhed hvor man anvender

### Ækvivalens klasser

Roller, forstået som forskellige slags brugere.  
Man kan for eksempel have: 

- Admin  
- Leder  
- Medarbejder

Hver slags bruger har sine egen tilladte handlinger og har adgang til forskellige dele af systemet. De er allesammen brugere, men de er delt op på baggrund af deres forskelligheder, der i dette tilfælde er deres tilladte handlinger og deres adgang. 

-### Grænseværdi test

I forhold til ratelimiting kunne man have grænseværdi af:  
A=9 godkendt (Lige under)  
A=10 godkendt (Lige på)  
A=11 fejler (Lige over)  
Så hvis man antager, at man maks må lave 10 request inden for en bestemt periode, vil man tjekke både under, på og over værdien. Vi tjekker under og på værdien for at sikre at tillade en bruger kan lave request til vores system og vi tjekker over værdien for at sikre, at man ikke kan fx bruteforce ved login eller unødigt belaste systemet.

### CRUD(L)

Indenfor verdenen af IT-sikkerhed kan man bruge CRUD(L) som en testteknik ved fx at se, om en bruger har tilladelse til at udføre den handling.   
For eksempel kunne man teste med en bruger med en medarbejder-rolle, der skulle forsøge at få adgang til noget, hvor en bruger skal have en leder-rolle. Her ville man kunne se, om man succesfuldt kan blokere de forkerte typer af brugere fra at få adgang til det data, man vil beskytte.
### Cycle process test

<img width="305" height="649" alt="billede" src="https://github.com/user-attachments/assets/1ac120d9-783c-4ffc-b721-fee2d49b2774" />

\-En bruger starter på start-siden.

\-Brugeren forsøger at logge ind.

\-Her tjekker autentifikationen om de må.

\-Hvis **nej**, bliver de sendt tilbage til login.  
(Eventuelt kan man have et tjek på antal gange de forsøger, så de bliver stoppet efter 3 måske.)

\-Hvis **ja**, bliver får de tilladelse og bliver givet adgang til systemet. 

\-Her kan de vælge at trykke på log ud-knappen, hvor der bliver spurgt om brugeren gerne vil det.

\-Hvis **nej**, forbliver brugeren i systemet.

\-Hvis **ja**, bliver brugeren logget ud.

\-Her bliver brugeren ført tilbage til start, som før de loggede ind.
## Test Pyramiden

<img width="632" height="404" alt="billede" src="https://github.com/user-attachments/assets/ba2dde38-1d81-40ad-bd9d-7adec93ec8c0" />

**End-to-end-test**: Brugerrejser fra ende til anden bl.a. med fokus på funktionalitet, brugervenlighed, brugeroplevelse. 

**System test/UI**: Om en bruger oplever cyklussen korrekt i UI, 

**Integration test**: teste flower uden UI (fx login også i forhold til session)

**Unit Test**: Funktionalitet, sessioner, om et password bliver hashet, tjekke roller

## Decision table test

  Placering i security gate

| Situation          | Test1        | Test2                         | Test3                        | Test4                         |
|--------------------|--------------|-------------------------------|------------------------------|-------------------------------|
| Gyldigt brugernavn | Ja           | Ja                            | Ja                           | Ja                            |
| Gyldigt password   | Ja           | Ja                            | Ja                           | Nej                           |
| MFA aktiveret      | Ja           | Ja                            | Nej                          | -                             |
| MFA korrekt        | Ja           | Nej                           | Nej                          | -                             |
| Resultat           | Adgang givet | Adgang nægtet Hændelse logget | Adgang givet Advarsel om MFA | Adgang nægtet Hændelse logget |

## Security gates:

**Ækvivalens klasser**:  
Code / Dev gate, System security gate

**Grænseværdi test**:  
Code / Dev gate

**CRUD(L)**:  
Code / Dev gate, Integration security gate

**Cycle process test**:  
Go / No-Go security gate (Prod),

**Test Pyramiden**:  
Integration security gate, Release candidate security gate (Pre-Prod)

**Decision table test**:  
Code / Dev gate, System security gate

