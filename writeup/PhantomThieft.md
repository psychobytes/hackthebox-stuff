---
title: "TryHuntMe - Phantom Thieft"
date: "February 25, 2025"
description: "Investigation of the theft case in the museum. Using various OSINT and Digital Forensics techniques to collect evidence and clues. Can you solve this case?"
difficulty : "Medium"
opsystem : "OSINT"
---

![image](https://github.com/user-attachments/assets/bc473484-0e5a-4775-aad0-bf80054b5430)

# TryHuntMe - Phantom Thieft

Link : [tryhackme.com/room/tryhuntmephantomthieft](https://tryhackme.com/room/tryhuntmephantomthieft)

## Day 1, Task 1

During a traditional festival in West Java, Indonesia, the vibrant energy of the crowd was undeniable. People flocked to various booths, enjoying an array of cultural activities and engaging in the festival's many attractions. One of the most popular spots was a mini museum showcasing unique artifacts and historical items. However, the festival took a mysterious turn when one of the prized items in the museum was discovered missing.

![image](https://github.com/user-attachments/assets/5fbff7f9-9803-4151-87dd-c51a9a9f2d61)

As an experienced investigator in the local police force, I have made a career out of dedication and expertise in solving complex cases, especially those related to cultural heritage. My appointment to investigate this artifact theft case came because of my solid track record in handling similar matters.

As soon as a strange report surfaced amidst the festival crowds, I began piecing together clues and examining every corner of the mini-museum where the incident took place. With a meticulous approach and modern methods of investigation, I was determined to uncover the mastermind behind the artifact loss and restore the public's faith in the preservation of our culture.

Are you ready to help with the investigation? (Y/N)


## Day 1, Task 2

![image](https://github.com/user-attachments/assets/d0caaffb-bc14-471d-96e3-61596b78ddde)

While examining the crime scene, I discovered a scrap of paper covered in erratic scribbles. At first glance, it appeared to be nothing more than careless doodles, yet I couldn't shake the feeling that these markings were intentionally left behind by the thief—a cryptic message meant to mislead or perhaps even challenge the investigators.

Determined to decipher its hidden meaning, I cross-referenced the scribbles with various known codes, local dialects, and even obscure ciphers, but every attempt left me with more questions than answers. Frustrated by the elusive nature of the clue, I reached out to you, hoping that your unique expertise might shed light on this enigma. Your insight could be the key to unlocking the message and ultimately catching the elusive culprit behind this daring theft.

there is written:

    0x00
    
    Ladies and gentlemen, you have discovered that an artifact has been stolen from your beloved museum. Yes, it was I who took it. I am an artist of deception, a master of disguise, and now I challenge you to find me.
    
    The note I left for you reads:
    "vdk3uLc8/zbp.avorgfnc//:fcggu".
    
    Decipher this message if you wish to see the stolen item returned. Follow the clues, prove your cleverness, and only then will you reclaim what was taken.

#### 0x00 What did you find in chall?
Ada kertas yang sengaja ditinggalkan pelaku. Di kertas tersebut terdapat "note I left for you to reads" (catatan kutinggalkan untuk kamu baca) dan string atau teks random dibawahnya ("vdk3uLc8/zbp.avorgfnc//:fcggu"). Di kertas tersebut juga terdapat pesan "Decipher this message if you wish to see the stolen item returned" berarti kita harus decipher atau memecahkan pesan tersebut.

Jika kita perhatikan baik-baik, string tersebut memiliki struktur yang mirip dengan url namun dibalik dari belakang ke depan. Mirip seperti url karena ada tanda "://", "fcggu" yang terdiri dari 5 huruf sehingga kemungkinan berarti https, lalu ada "zbp." yang kemungkinan merupakan TLD yang terdiri dari 3 huruf, "/vdk3uLc8" yang sepertinya merupakan direktori / path. 

Kita bisa mirror teks tersebut menggunakan cyberchef dan hasilnya adalah "uggcf://cnfgrova.pbz/8cLu3kdv"

![image](https://github.com/user-attachments/assets/1f2717bf-ac55-486c-9e96-7910a9827473)

URL tersebut masih belum bisa terbaca. Sepertinya setiap huruf pada url diganti dengan huruf lain. Saya berasumsi bahwa teks tersebut dienkripsi menggunakan caesar cipher. Kita bisa menggunakan tools online seperti [https://www.dcode.fr/caesar-cipher](https://www.dcode.fr/caesar-cipher) untuk memecahkan enkripsi caesar cipher.

![image](https://github.com/user-attachments/assets/4987aab6-c187-44fa-af6f-2c6382717854)

Kita mendapat URL pastebin. Di dalam pastebin tersebut terdapat catatan lagi. Catatan tersebut merupakan clue untuk pertanyaan berikutnya.

![image](https://github.com/user-attachments/assets/ef795d97-22c7-46e8-8f5b-8b2275678f85)

> What did you find in chall ? { https://pastebin.com/xxxxx }


#### 0x00 What ciphers are being used?
Chiper yang digunakan di challenge tadi adalah Caesar Chiper ROT13 (rotate by 13 places) yang dibalik (mirror / reverse). Namun karena keterbatasan petunjuk mengenai format jawaban, saya tidak bisa solve di chall ini.


#### 0x01 What did you find in chall?
Dari pastebin yang kita peroleh dari chall sebelumnya kita mendapatkan sebuah catatan lagi.

    0x01 Enjoy the game, chill... it will be fun, hehe
     
    =QK/PS49tiamhPaotCOony6q627r+Ge403rv6qrp
     
    :D I know, I'm not that evil, I think you need this one...
    https://bit.ly/41cWqY8
     
    that's city is cool :D

Terdapat string random lagi (ciphertext) dan terdapat clue berupa URL. Chipertext tersebut mirip dengan Base64 karena ada tanda "=". Namun saya tidak berhasil untuk decode ciphertext tersebut.

![image](https://github.com/user-attachments/assets/b34c56cc-e60d-49d6-83f6-017ed0d810be)

Terdapat Hint ":D all doors needed key right?" di chall tersebut. Sehingga tidak mungkin ini adalah base64 karena base64 merupakan encoding sehingga tidak memerlukan key.

Clue kedua berupa URL. Jika dibuka URL tersebut berisi file "up-and-low-for-me-matter-1740438506947.wav"

![image](https://github.com/user-attachments/assets/4c915f5f-4dc9-4875-84df-e43c35a5b24c)

Download file wav tersebut. File .wav merupakan file audio, jika diputar file tersebut berisi suara seperti bunyi tombol telepon kabel ketika ditekan. Suara setiap tombol pada telepon kabel memiliki nada yang berbeda. Kita bisa mengetahui tombol berapa saja yang ditekan di telepon melalui suaranya. Kode suara ini disebut Dual-tone multi-frequency signaling (DTMF). Kita bisa menggunakan DTMF decoder [dtmf.netlify.app/](https://dtmf.netlify.app/) untuk mengetahui tombol berapa yang ditekan berdasarkan suaranya.

![image](https://github.com/user-attachments/assets/918d47ac-6e55-4701-8699-ffb288adb442)

Hasil decode masih berupa angka random. Mungkin ada arti / maksud tertentu dari angka tersebut. Kita bisa mengidentifikasi angka tersebut menggunakan [www.dcode.fr/cipher-identifier](https://www.dcode.fr/cipher-identifier). Hasilnya, kemungkinan angka tersebut merupakan ASCII code.

![image](https://github.com/user-attachments/assets/8b5ba4de-8e92-44fe-b511-f95aaf016d9c)

Jika diconvert hasilnya adalah sebuah URL.

![image](https://github.com/user-attachments/assets/aedb268b-b9dc-4b36-be4e-40a8cb8d2e75)

URL tersebut akan redirect ke imgur. Di halaman tersebut terdapat gambar jalan dengan clue "I've laid the next stepping stone here, find it if you can hihi...".

![image](https://github.com/user-attachments/assets/1afb1913-639a-44f6-bdd8-1f8586745194)

Saya stuck disini. Di gambar semua plat nomor sudah disensor sehingga saya tidak bisa mengidentifikasi lokasi tempat tersebut berdasarkan plat nomor. Ada Alfamart di foto tersebut namun alfamart tersebar di seluruh Indonesia sehingga tidak bisa menjadi clue. Clue yang saya punya hanyalah "SUKOWATI Bakso & Mie Ayam", dan pada pastebin sebelumnya terdapat clue "that's city is cool :D" yang berarti kota itu dingin / keren?. Mungkin bisa jadi petunjuk untuk lokasi foto tersebut. Bisa disimpulkan bahwa kemungkinan foto tersebut diambil di kota yang dingin atau dataran tinggi.

#### 0x01 What ciphers are being used?
Not Solved Yet.

#### 0x02 What did you find in chall?
Not Solved Yet.

#### 0x02 What did the thief do last?
Not Solved Yet.


## Day 2, Task 1
After a long day of unraveling puzzles alongside the investigator, we finally retreated home to rest, our minds still buzzing with unanswered questions. The night passed in uneasy silence, and I drifted into a deep sleep, hopeful that the morning would bring clarity.

![image](https://github.com/user-attachments/assets/0ce61014-d8b9-40ba-bfb9-91045ef96ace)

In the early hours, still half-asleep, a mysterious phone call shattered the quiet. The caller was unidentified, and there was an eerie, barely audible hum on the line—no words, no explanation, just a sense of foreboding. Reacting on instinct, I immediately activated my recording device to capture every moment of the call. This secret message, cryptic and uninvited, would soon serve as a pivotal piece of evidence for further analysis with the investigator.

> Download Task File on TryHackMe. (Joker-Unknown-Call-1739806429987.wav)

#### 1x01 What's that sound?
Jika diputar, file audio tersebut berisi suara piano dan nada "beep" putus-putus. Jika didengarkan dengan headset atau speaker stereo (dua arah) suara piano terdengar di kiri dan kode morse di kanan.

Nada "beep" putus-putus itu adalah kode morse

> 1x01 What's that sound? { morxx }


#### 1x01 What did you get from the sound?
Kita perlu memecahkan pesan yang disampaikan menggunakan kode morse tersebut. Gunakan Audacity untuk mengedit audio tersebut agar kode morse bisa terdengar dengan jelas. Matikan suara di sebelah kiri dengan menggeser slider "R L" ke kanan (R) agar suara piano menjadi tidak terdengar. Potong audio di bagian kode morsenya saja. Setelah itu export hasilnya menjadi mono (audio satu arah).

![image](https://github.com/user-attachments/assets/ad5937ba-9d55-4f28-b78d-a88d26158aca)

Upload hasilnya ke [morsecode.world/international/decoder/audio-decoder-adaptive.html](https://morsecode.world/international/decoder/audio-decoder-adaptive.html).

![image](https://github.com/user-attachments/assets/46435809-277c-483b-aefc-cdd60a7274af)

Hasil decode berupa sebuah URL.

> 1x01 What did you get from the sound? { https://bit.ly/xxxxx }


#### 1x01 What is in the picture?
URL tadi akan redirect ke imgur. Halaman tersebut berisi sebuah gambar bulan dengan gambar QR code yang samar-samar (perhatikan atas kiri bulan).

![image](https://github.com/user-attachments/assets/26b92ee5-5c70-4837-b777-204e098ab030)

> 1x01 What is in the picture? { xxcode }


#### 1x01 What was the data you got from the Images?
QR code terlihat samar-samar. Kita bisa memperjelas kode QR tersebut dengan mengatur pencahayaan pada gambar. Kita bisa menggunakan [www.photopea.com/](https://www.photopea.com/)

![image](https://github.com/user-attachments/assets/78d0fd81-2c68-40ad-b544-a704a85b9286)

Scan QR code tersebut, hasilnya adalah sebuah URL.

![image](https://github.com/user-attachments/assets/73144b35-61b5-4ef8-97ca-05f1d3b61d24)

Jika dibuka URL tersebut akan redirect ke pastebin.

![image](https://github.com/user-attachments/assets/cac45143-dfc7-4b5d-bdb4-87ad2fedfe81)

> 1x01 What was the data you got from the Images? { https://pastebin.com/xxxxx }


#### 1x02  What is the full name in question?
Pastebin tersebut berisi teks sebagai berikut :

    1x01
    wow... I guess you are quite excited about this challenge rather than getting items in the junkyard museum right? hehe
     
     
    you know what?
    In the land of Pasundan, a teacher became a fighter, his voice loudly defending the people. He took the lead in youth organizations when radio was still a rarity, then promoted culture and education when silent cinema became popular. When the world was hit by a major crisis, he sat in the people's council, challenging the colonizers with courage. After the proclamation, his job was to build the laskar, but his footsteps stopped at the end of the same year. Now his name is engraved on streets, stadiums and monuments.
     
    he is maybe bring the keys :D
    https://pastebin.com/SDy4AdPR

Berdasarkan pesan tersebut kita perlu mengidentifikasi siapa orang yang membawa kunci untuk membuka pastebin yang ada di pesan (baris paling bawah). Terdapat clue bahwa dia adalah seorang guru yang menjadi petarung untuk membela rakyat dengan suaranya di pasundan (bandung?). Dia menentang penjajah (pahlawan nasional?). Setelah proklamasi pekerjaan dia untuk membangun laskar, namun berakhir di tahun yang sama (meninggal setelah kemerdekaan?). Sekarang namanya ada di jalan, stadium, dan monumen.

Dari clue tersebut bisa diketahui bahwa orang yang dimaksud adalah Otto Iskandardinata (+100 Bhinneka Point if u guessed it :D).

Otto Iskandardinata merupakan pahlawan dari bandung. Ia mengajar di HIS (Hollandsch-Inlandsche School). Ia juga membela rakyat dengan suaranya karena dia berkerja sebagai pemimpin surat kabar Tjahaja. Dia meninggal dibunuh oleh laskar hitam di tahun yang sama setelah kemerdekaan (20 Desember 1945). Dia diangkat sebagai pahlawan nasional berdasarkan Surat Keputusan Presiden Republik Indonesia Nomor 088/TK/Tahun 1973. Namanya dijadikan nama jalan di beberapa kota, nama stadion, dan terdapat Monumen Pasir Pahlawan di Lembang untuk mengabadikan perjuangannya. sc : [wikipedia](https://id.wikipedia.org/wiki/Oto_Iskandar_di_Nata)

> 1x02  What is the full name in question? { Otxx Iskanxxxxx }


#### 1x02  What is the link password?
![image](https://github.com/user-attachments/assets/7f2218ba-0e27-44a8-a8fd-cd7569e0c47a)

Karena Chall sebelumnya membahas mengenai Otto Iskandardinata, saya berasumsi bahwa passwordnya adalah nama depan pahlawan tersebut.

> 1x02  What is the link password? { otxx }
