# CrackMe Level 1.0 – [Kanax01-Fixed-Easy-crackme]

**Źródło:** crackmes.one
**Poziom:** 1 – Very Easy / Beginner  
**Platforma:** Windows
**Language:** C/C++
**Arch:** x86-64
**Rozwiązanie:** Znalezienie hardcoded hasła w Ghidrze  
**Czas:** ~5 min
**Narzędzia:** Ghidra

## Co robi program

Po uruchomieniu prosi o wpisanie hasła.  
Po wpisaniu albo wyświetla komunikat o sukcesie, albo zamyka się / wyświetla błąd.

## Podejście

1. Uruchomiłem program → zobaczyłem, że prosi o hasło  

<img width="442" height="64" alt="image" src="https://github.com/user-attachments/assets/be540404-2824-46af-a818-52ae86bd9bd6" />

   Komunikat po błędnym wpisaniu hasła
   
<img width="298" height="42" alt="image" src="https://github.com/user-attachments/assets/76eb10f9-1436-4a1b-9a94-ae62dde4cd81" />

2. Otworzyłem plik w Ghidrze po czym odrazu przeszedłem do window --> defined strings
3. Przeglądając liste stringów znalazłem m.in.:
   "Congrats!!! You Cracked The Code"
   
   "Please Enter The Password:"
   
   "Wrong Passowrd, Please Try Again:"
   
   Oraz string który odrazu przykuł moją uwagę:
   
   "EasyPassword"
   
<img width="395" height="13" alt="image" src="https://github.com/user-attachments/assets/9b16a032-7755-48f9-bf18-f4d66ade9fad" />

4. Sprawdziłem czy ten string nigdzie nie był używany jako komunikat.
5. Wrzuciłem go do programu i przeszedł:

<img width="350" height="114" alt="image" src="https://github.com/user-attachments/assets/9735babb-4841-47d8-94c6-dc51aeb300f8" />

Kluczowy fragment który zawiera warunek sukcesu (dekompilacja Ghidry):

```
if ((local_28 == DAT_1400050b8) &&
   ((Local_28 == 0 || (iVar4 = memcmp(ppppuVar5,pcVar6,local_28), iVar4 == 0))) {
   pcVar6 = "\n Congrats!!! You Cracked The Code";
}
Else {
pcVar6 = "\n Wrong Password, Please Try Again";
}
```
