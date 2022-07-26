# Trash Royale

## Problem Statement:
Find the flag, and make sure its wrapped in LITCTF{}

Ugh, I keep forgetting my password for https://spectacle-deprive4-launder.herokuapp.com/, so I will just (sic, we think they meant put but we're not sure) it here.
Username: LexMACS and Password: !codetigerORZ

## Solution
Open the website, and you'll see a login page. At first, we expirmented with different login/password combos (basic SQL injection techniques) to try and break the login page but nothing worked. We moved on to logging in with the provided username and password.

Upon navigating to home, you are presented with the following page:
<img width="1430" alt="image" src="https://user-images.githubusercontent.com/58674441/180915767-24845576-b3a9-4af6-a65c-0befc50f7c0e.png">

The first thing we saw was the morse code at the top. Clicking it, we got HEHEHEHAW. Not useful.

The webpage was unremarkable, except for the line which read `For a special few, our web developers have made the game available in early access!`. This made us search for the early access game.

Viewing the page source, one finds a hidden link:
<img width="1430" alt="image" src="https://user-images.githubusercontent.com/58674441/180916265-74501250-e074-48ef-a6c7-dff413265c3f.png">

Navigating to that url, we see a screen with an exe and an image. The image was useless (according to basic steganography). We also saw a warning that the sounds were buggy, pointing us towards finding sound files, mp3 and wav files.
We downloaded the executable. When we searched for strings in the executable, we found a string called "flag.mp3". This matched up with our observation above, and we started searching for ways to get the mp3 out of the executable. When we ran the executable, the top left icon displayed a snake:
![image](https://user-images.githubusercontent.com/58674441/180918327-af84363b-d910-4224-8440-264baa961478.png)

This snake was clearly the pygame logo, indicating that the executable was compiled with pyinstaller with the --onefile flag. So, we used [pyinstxtractor](https://raw.githubusercontent.com/extremecoders-re/pyinstxtractor/master/pyinstxtractor.py) to extract the contents of the executable. Once extracted, we `cd`ed into the trash-royal.exe_extracted folder:
<img width="1550" alt="image" src="https://user-images.githubusercontent.com/58674441/180917284-e39aced1-57e7-48e9-9090-3c6fa0003655.png">

Music files are typically stored in `/assets` so we checked the folder, and found `flag.mp3`
<img width="1550" alt="image" src="https://user-images.githubusercontent.com/58674441/180917634-ab32c533-cdec-44fa-8c8b-bcf725d3587e.png">

Playing the mp3 file gives the user a bunch of hes and haws, indicating morse code. Given that he was shorter than haw, we let he represent `.` and haw represent `_`.
In order to easily see dots vs dashes, we opened the file in audacity.

<img width="1552" alt="image" src="https://user-images.githubusercontent.com/58674441/180918051-676e8f42-7c99-4356-b9d1-8c515c534bca.png">

The morse code was `.... ...-- .... ...-- .... ...-- .... ....- .-- - .... .-. . . -.-. .-. --- .-- -.`
Translating this to english gave `H3H3H3H4WTHREECROWN`.

## Answer
`LITCTF{H3H3H3H4WTHREECROWN}`
