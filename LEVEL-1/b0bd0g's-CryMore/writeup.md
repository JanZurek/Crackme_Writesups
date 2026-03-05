# CrackMe Level 1.0 – Kanax01-Fixed-Easy-crackme

**Źródło:** [crackmes.one](https://crackmes.one/crackme/698d2206e2ba6023bfacaa4f)  
**Poziom:** 1.3
**Platforma:** Multiplatform  
**Język:** C/C++  
**Architektura:** x86 
**Rozwiązanie:** Zablokowanie malwaru przed jego wykonaniem
**Czas rozwiązania:** ~ 12 minut  
**Narzędzia:** Ghidra

## Podejście krok po kroku

1. Otworzyłem plik w Ghidrze i od razu przeszedłem do:   **Window → Defined Strings**

2. Wśród stringów znalazłem m.in.:

   - "127.0.0.1"  
   - "Malware exectued. You are screwed. Have a nice day."  
   - "200 OK"  
   - "Malware succesfully neutralized. Good Job."   

   
<img width="1439" height="31" alt="image" src="https://github.com/user-attachments/assets/0d8d11c9-1a28-43aa-97f0-ea1fb077c9fc" />


3. Stringi odnoszące się do malwaru były komunikatami w funckcji main a string który zwrócił moją uwagę był adres IP. Był on używany w zmiennej a sama ta zmienna była wykorzystywana
połącznie do adresu 127.0.0.1 o porcie 44333 (0xad2d).

4.s Po znalezeniu owego połączenia zablokowałem je przy pomocy powershella blokując wykonanie się malwaru.

   <img width="1439" height="31" alt="image" src="https://github.com/user-attachments/assets/4bc00909-2391-427b-8304-8da3d54bf62a" />


## Kluczowy fragment kodu (dekompilacja Ghidry)

<img width="729" height="894" alt="image" src="https://github.com/user-attachments/assets/66c40bff-df1f-4c90-a39d-d3e32998ce20" />


