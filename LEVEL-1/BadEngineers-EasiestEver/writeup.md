# CrackMe Level 1.0 – Kanax01-Fixed-Easy-crackme

**Źródło:** [crackmes.one  ](https://crackmes.one/crackme/697fd52a16739b40dcb5dabd)  
**Poziom:** 1.7  
**Platforma:** Windows  
**Język:** C/C++  
**Architektura:** x86-64  
**Rozwiązanie:** Znalezienie hasła do oprogramowania 
**Czas rozwiązania:** ~20 minut  
**Narzędzia:** Ghidra

## Co robi program

Po uruchomieniu prosi o wpisanie hasła.  
Po poprawnym haśle → komunikat sukcesu  
Po błędnym → komunikat błędu i prośba o ponowną próbę.

## Podejście krok po kroku

1. Uruchomiłem program i zobaczyłem interfejs:

   **Prośba o hasło**  
   <img width="254" height="25" alt="image" src="https://github.com/user-attachments/assets/8be51d3a-890a-4376-8e05-58445b3b41a4" />


   **Komunikat po błędnym haśle**  
   <img width="263" height="21" alt="image" src="https://github.com/user-attachments/assets/15bbf1dc-eb5a-4378-9233-d8b643d424f9" />


2. Otworzyłem plik w Ghidrze i od razu przeszedłem do:  
   **Window → Defined Strings**

3. Wśród stringów znalazłem m.in.:

   - "Please Enter The Password:"
   - "Wrong Password, Please Try Again:"
   - "Congrats, You deserve this!"

4. Sprawdziłem gdzie wyświetla się string o komunikacie "Congrats, You deserve this!" a była to funckja main.


<img width="629" height="353" alt="image" src="https://github.com/user-attachments/assets/28d67491-b802-4316-813e-e07b7f6dd5c1" />


5. Wniej zauważyłem funkcję PasswordCheck i do niej przeszedłem:

   <img width="490" height="919" alt="image" src="https://github.com/user-attachments/assets/0f133f88-517e-48ac-ab61-ca13b8374e9f" />


  <img width="697" height="921" alt="image" src="https://github.com/user-attachments/assets/40000be9-ba80-4e9d-973e-649f7b832bf2" />

Zauważyłem że funckja wykonuje pętle o maksymalnej długości dla łancucha znaków 16, która po kolei warunkuje zakres poprawnych do użycia cyfr, liczb i znaków za pomocą tabeli kodów ASCII i kążdy z zakresów musi zostać użyty chociaż raz.
Zakres ten wynosi następująco:

| Warunek | Znaki (ASCII) | Zakres HEX | Licznik (Ghidra) |
| :--- | :--- | :--- | :--- |
| **1** | `0, 1, 2, 3, 4` | `0x30 - 0x34` | `local_20` |
| **2** | `H, I, J, K, L, M, N` | `0x48 - 0x4E` | `local_28` |
| **3** | `t, u, v, w, x, y` | `0x74 - 0x79` | `local_30` |
| **4** | `a, b, c, d, e, f` | `0x61 - 0x66` | `local_38` |
| **5** | `!, ", #, $, %, &` | `0x21 - 0x26` | `local_40` |
| **6** | `; , < , = , > , ?` | `0x3B - 0x3F` | `local_48` |
| **7** | `j, k, l, m` | `0x6A - 0x6D` | `local_50` |
| **8** | `z, {, \|, }` | `0x7A - 0x7D` | `local_58` |
| **9** | `o, p, q, r, s` | `0x6F - 0x73` | `local_60` |
| **10** | `\, ], ^, _` | `0x5C - 0x5F` | `local_68` |

## Kluczowy fragmenty kodu (dekompilacja Ghidry)

<img width="629" height="353" alt="image" src="https://github.com/user-attachments/assets/28d67491-b802-4316-813e-e07b7f6dd5c1" />


<img width="490" height="919" alt="image" src="https://github.com/user-attachments/assets/0f133f88-517e-48ac-ab61-ca13b8374e9f" />


<img width="697" height="921" alt="image" src="https://github.com/user-attachments/assets/40000be9-ba80-4e9d-973e-649f7b832bf2"/>
