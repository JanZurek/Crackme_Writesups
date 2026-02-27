# CrackMe Level 1.0 – Kanax01-Fixed-Easy-crackme

**Źródło:** [crackmes.one](https://crackmes.one/crackme/698d2206e2ba6023bfacaa4f)
**Poziom:** 1 – Very Easy / Beginner  
**Platforma:** Windows  
**Język:** C/C++  
**Architektura:** x86-64  
**Rozwiązanie:** Znalezienie hardcoded hasła w stringach Ghidry  
**Czas rozwiązania:** ~5 minut  
**Narzędzia:** Ghidra

## Co robi program

Po uruchomieniu wyświetla powitanie i prosi o wpisanie hasła.  
Po poprawnym haśle → komunikat sukcesu  
Po błędnym → komunikat błędu i prośba o ponowną próbę.

## Podejście krok po kroku

1. Uruchomiłem program i zobaczyłem interfejs:

   **Prośba o hasło**  
   <img width="442" height="64" alt="Prośba o hasło" src="https://github.com/user-attachments/assets/be540404-2824-46af-a818-52ae86bd9bd6" />

   **Komunikat po błędnym haśle**  
   <img width="298" height="42" alt="Błędne hasło" src="https://github.com/user-attachments/assets/76eb10f9-1436-4a1b-9a94-ae62dde4cd81" />

2. Otworzyłem plik w Ghidrze i od razu przeszedłem do:  
   **Window → Defined Strings**

3. Wśród stringów znalazłem m.in.:

   - "Congrats!!! You Cracked The Code"
   - "Please Enter The Password:"
   - "Wrong Password, Please Try Again:"
   - "Enter To Exit"

   oraz string, który od razu wzbudził podejrzenia:

   **"EasyPassword"**

   <img width="395" height="13" alt="EasyPassword w Defined Strings" src="https://github.com/user-attachments/assets/9b16a032-7755-48f9-bf18-f4d66ade9fad" />

4. Szybko sprawdziłem, czy "EasyPassword" jest używany jako komunikat.

5. Wpisałem hasło **EasyPassword** → sukces:

   <img width="350" height="114" alt="Sukces – Congrats!!!" src="https://github.com/user-attachments/assets/9735babb-4841-47d8-94c6-dc51aeb300f8" />

## Kluczowy fragment kodu (dekompilacja Ghidry)

```c
if ((local_28 == DAT_1400050b8) &&
    ((local_28 == 0) || (iVar4 = memcmp(ppppuVar5, pcVar6, local_28), iVar4 == 0))) {
    pcVar6 = "\nCongrats!!! You Cracked The Code";
}
else {
    pcVar6 = "\nWrong Password, Please Try Again";
}
