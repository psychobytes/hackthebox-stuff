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

### 0x00 What did you find in chall?
Ada kertas yang sengaja ditinggalkan pelaku. Di kertas tersebut terdapat "note I left for you to reads" (catatan kutinggalkan untuk kamu baca) dan string atau teks random dibawahnya ("vdk3uLc8/zbp.avorgfnc//:fcggu"). Di kertas tersebut juga terdapat pesan "Decipher this message if you wish to see the stolen item returned" berarti kita harus decipher atau memecahkan pesan tersebut.

Jika kita perhatikan baik-baik, string tersebut memiliki struktur yang mirip dengan url namun dibalik dari belakang ke depan. Mirip seperti url karena ada tanda "://", "fcggu" yang terdiri dari 5 huruf sehingga kemungkinan berarti https, lalu ada "zbp." yang kemungkinan merupakan TLD yang terdiri dari 3 huruf, "/vdk3uLc8" yang sepertinya merupakan direktori / path. 

Kita bisa mirror teks tersebut menggunakan cyberchef dan hasilnya adalah "uggcf://cnfgrova.pbz/8cLu3kdv"

![image](https://github.com/user-attachments/assets/1f2717bf-ac55-486c-9e96-7910a9827473)

URL tersebut masih belum bisa terbaca. Sepertinya setiap huruf pada url diganti dengan huruf lain. Saya berasumsi bahwa teks tersebut dienkripsi menggunakan caesar cipher. Kita bisa menggunakan tools online seperti [https://www.dcode.fr/caesar-cipher](https://www.dcode.fr/caesar-cipher) untuk memecahkan enkripsi caesar cipher.

![image](https://github.com/user-attachments/assets/4987aab6-c187-44fa-af6f-2c6382717854)

Kita mendapat URL pastebin. Di dalam pastebin tersebut terdapat catatan lagi. Catatan tersebut merupakan clue untuk pertanyaan berikutnya.

![image](https://github.com/user-attachments/assets/ef795d97-22c7-46e8-8f5b-8b2275678f85)

> What did you find in chall ? { https://pastebin.com/xxxxx }


### 0x00 What ciphers are being used?
Chiper yang digunakan di challenge tadi adalah Caesar Chiper ROT13 (rotate by 13 places) yang dibalik (mirror / reverse). Namun karena keterbatasan petunjuk mengenai format jawaban, saya tidak bisa solve di chall ini.


### 0x01 What did you find in chall?
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

### 0x01 What ciphers are being used?
Not Solved Yet.

### 0x02 What did you find in chall?
Not Solved Yet.

### 0x02 What did the thief do last?
Not Solved Yet.


## Day 2, Task 1
After a long day of unraveling puzzles alongside the investigator, we finally retreated home to rest, our minds still buzzing with unanswered questions. The night passed in uneasy silence, and I drifted into a deep sleep, hopeful that the morning would bring clarity.

![image](https://github.com/user-attachments/assets/0ce61014-d8b9-40ba-bfb9-91045ef96ace)

In the early hours, still half-asleep, a mysterious phone call shattered the quiet. The caller was unidentified, and there was an eerie, barely audible hum on the line—no words, no explanation, just a sense of foreboding. Reacting on instinct, I immediately activated my recording device to capture every moment of the call. This secret message, cryptic and uninvited, would soon serve as a pivotal piece of evidence for further analysis with the investigator.

> Download Task File on TryHackMe. (Joker-Unknown-Call-1739806429987.wav)

### 1x01 What's that sound?
Jika diputar, file audio tersebut berisi suara piano dan nada "beep" putus-putus. Jika didengarkan dengan headset atau speaker stereo (dua arah) suara piano terdengar di kiri dan kode morse di kanan.

Nada "beep" putus-putus itu adalah kode morse

> 1x01 What's that sound? { morxx }


### 1x01 What did you get from the sound?
Kita perlu memecahkan pesan yang disampaikan menggunakan kode morse tersebut. Gunakan Audacity untuk mengedit audio tersebut agar kode morse bisa terdengar dengan jelas. Matikan suara di sebelah kiri dengan menggeser slider "R L" ke kanan (R) agar suara piano menjadi tidak terdengar. Potong audio di bagian kode morsenya saja. Setelah itu export hasilnya menjadi mono (audio satu arah).

![image](https://github.com/user-attachments/assets/ad5937ba-9d55-4f28-b78d-a88d26158aca)

Upload hasilnya ke [morsecode.world/international/decoder/audio-decoder-adaptive.html](https://morsecode.world/international/decoder/audio-decoder-adaptive.html).

![image](https://github.com/user-attachments/assets/46435809-277c-483b-aefc-cdd60a7274af)

Hasil decode berupa sebuah URL.

> 1x01 What did you get from the sound? { https://bit.ly/xxxxx }


### 1x01 What is in the picture?
URL tadi akan redirect ke imgur. Halaman tersebut berisi sebuah gambar bulan dengan gambar QR code yang samar-samar (perhatikan atas kiri bulan).

![image](https://github.com/user-attachments/assets/26b92ee5-5c70-4837-b777-204e098ab030)

> 1x01 What is in the picture? { xxcode }


### 1x01 What was the data you got from the Images?
QR code terlihat samar-samar. Kita bisa memperjelas kode QR tersebut dengan mengatur pencahayaan pada gambar. Kita bisa menggunakan [www.photopea.com/](https://www.photopea.com/)

![image](https://github.com/user-attachments/assets/78d0fd81-2c68-40ad-b544-a704a85b9286)

Scan QR code tersebut, hasilnya adalah sebuah URL.

![image](https://github.com/user-attachments/assets/73144b35-61b5-4ef8-97ca-05f1d3b61d24)

Jika dibuka URL tersebut akan redirect ke pastebin.

![image](https://github.com/user-attachments/assets/cac45143-dfc7-4b5d-bdb4-87ad2fedfe81)

> 1x01 What was the data you got from the Images? { https://pastebin.com/xxxxx }


### 1x02  What is the full name in question?
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


### 1x02  What is the link password?
![image](https://github.com/user-attachments/assets/7f2218ba-0e27-44a8-a8fd-cd7569e0c47a)

Karena Chall sebelumnya membahas mengenai Otto Iskandardinata, saya berasumsi bahwa passwordnya adalah nama depan pahlawan tersebut.

![image](https://github.com/user-attachments/assets/6bbb0781-83d0-42bf-b96c-fb4ea4ab7a17)

Pastebin Unlocked :3

> 1x02  What is the link password? { otxx }


## Day 2, Task 2
A sense of unease crept in as we realized that "J0k3r" wasn’t just an alias—it was the name of a crime syndicate that specialized in stealing valuable items and selling them in public community auctions. If the vase we were searching for changed hands, tracking it down would become nearly impossible. We had no idea when the auction would take place, making the situation even more critical.

With time slipping away, we scoured various community marketplaces and trading forums where collectors and traders gathered to discuss and sell rare items. Every uploaded photo, every suspicious comment—we analyzed them carefully. It wasn’t easy, as these criminals were meticulous in covering their tracks.

We decided to take a different approach—creating a fake identity as a potential buyer. A new account was set up, crafted to appear as a legitimate collector of rare vases. We posted inquiries, pretending to be highly interested in purchasing a vase matching the stolen one’s description. Our goal was simple: to lure out the current holder of the stolen item.

The player begins searching through various auction sites and online marketplaces, looking for posts featuring a similar vase. Determined to track down its owner, they not only scour existing forums but also take the initiative to create a new account, posing as a collector interested in purchasing the vase.

![image](https://github.com/user-attachments/assets/6cd9a5c2-2d4d-464e-86cf-7b828c73d97c)

After some time, a message arrives—someone claims to have the vase the player is looking for. However, the seller is cautious. They are not willing to proceed with the transaction right away; instead, they want to ensure that the player is part of their underground community. For security reasons, they present a cryptic puzzle—one that must be solved to gain access to a secret group where further discussions can take place.

    "I see you've been searching for the antique vase, correct? I happen to have one.
    If you truly want it, prove that you can be trusted. Go far a little Bit and dont Ly'eeer to me,
    my advice is addition would be better https://pastebin.com/JUzZspYa"


### What does the message pastebin refer to?

![image](https://github.com/user-attachments/assets/8f61899d-ed38-4ad4-ac3b-73eb3a0fd2a3)

"The City At the northern edge, amid the whispers of waves and the timeless aroma of spices, lies a city that once served as the heart of a sultanate. Here, the 'mega mendung' motif on batik conceals the secret fusion of Islamic, Malay, and indigenous wisdom, etched into every facet of its history."

Clue tersebut mengarahkan kita ke suatu kota. Kota tersebut berada di ujung utara, identik dengan spices (rempah?), kota pusat kesultanan, Mega Mendung (batik). Clue paling menarik adalah mega mendung. Batik Mega Mendung berasal dari kota Cirebon. Lokasi kota Cirebon berada di utara pulau Jawa, sesuai dengan clue. Dan kota Cirebon dulunya merupakan pusat Kesultanan Cirebon.

![image](https://github.com/user-attachments/assets/2e386d80-5a66-4c2c-b63c-cfae1fa247d8)

Hint di soal jawabannya adalah "Alternate Name of the city", berarti nama lain dari Cirebon. Berdasarkan informasi dari [id.wikipedia.org/wiki/Kota_Cirebon](https://id.wikipedia.org/wiki/Kota_Cirebon), kota Cirebon pada awalnya berasal dari kata sarumban.

> What does the message pastebin refer to? { saruxxxx }


### What are we asked to visit?
Karena pada chall sebelumnya sering menggunakan bit.ly dan format jawaban yang terdiri dari xxx.xx/xxxxxxxx, saya berasumsi bahwa jawabannya adalah bit.ly/saruxxxx

> What are we asked to visit? { bit.ly/saruxxxx }


### Where is the actual location of the place?
URL bit.ly pada chall sebelumnya jika dikunjungi akan redirect ke sebuah channel telegram.
![image](https://github.com/user-attachments/assets/5f02006e-1265-4cfb-9c10-f0a8e62acc44)

> Where is the actual location of the place? { https://t.me/Phantomxxxxxx }

Penjual vas yang dicuri memberikan puzzle sebelum melakukan transaksi dan akhirnya kita diarahkan ke dalam grup telegram tersebut.


## Day 2, Task 3
The investigator team begins an initial analysis of the suspected group. During this process, the team examined all activity and content available in the group. From the search results, the group contained only two messages and three accounts registered as members.

![image](https://github.com/user-attachments/assets/9f9fac68-ba8d-45b0-8626-7b5017ad7ca9)

The first step was to identify the account that sent the image. Investigators focused on the digital footprint of the account, such as message metadata or potential links to other accounts. After that, the team also reviewed the two messages contained in the group. As a result, it was found that both messages contained instructions or invitations to go to a certain place, although the details of the location still need to be explored further.

### Which country is it?
Pesan terakhir di telegram oleh Elene Kurtanidze "meet me here..." dan sebuah foto. Dia meminta kita untuk menemuinya disana, jadi kita perlu menentukan lokasi gambar tersebut.

![image](https://github.com/user-attachments/assets/bcd0b064-302c-42d5-b4a3-ea6739930a04)

Lakukan reverse image search gambar tersebut menggunakan [images.google.com](https://images.google.com/) ditemukan bahwa ada kesesuaian gambar dengan National Monument di Cork, Ireland.

![image](https://github.com/user-attachments/assets/97eaf70c-99e4-4d15-8393-a277723ddf37)

> Which country is it? { Irel*** }


### Which location is it?
Search "National Monument Ireland" di maps dan ditemukan lokasi monumen nasional itu.

![image](https://github.com/user-attachments/assets/87298086-a41a-4648-b1d7-7f697b4c47bb)

> Which location is it? { Grxxx Paxxxx }


### What was the inspiration for the sock puppet identity of the alleged perpetrator?
Kita dapat mengetahui Inspirasi dari identitas palsu (sock puppet) pelaku dengan cara googling username pelaku (Elene Kurtanidze).

![image](https://github.com/user-attachments/assets/7152dfe4-c2bb-43f5-9ddd-86465a908915)

Hasil pencarian masih terlalu luas, kita dapat mempersempit pencarian dengan menyertakan negara asal pelaku (Ireland).

![image](https://github.com/user-attachments/assets/df6e9b76-5ee1-4969-bbe6-d12cdcf9fca9)

Sepertinya identitas sock puppet yang digunakan pelaku terinspirasi dari Elene Kurtanidze yang merupakan anggota Lisdoonvarna Crew (grup penyanyi hip-hop anak populer dari Ireland).

![image](https://github.com/user-attachments/assets/710a5f1d-b341-4496-ba34-2339f9cbe31e)

> What was the inspiration for the sock puppet identity of the alleged perpetrator? { Lisxxxxxxxx Crxx }


### Who is the owner of the group?
Owner dari grup bisa kita lihat di bagian members di telegram. Terlihat jOk3r p merupakan owner dari grup itu.
![image](https://github.com/user-attachments/assets/5baf9530-0a85-4eb4-9b03-b8207b2e2deb)

Jika kita cek, username dari user tersebut adalah @jOk3rph
![image](https://github.com/user-attachments/assets/1fb81726-98c3-4a09-8d8e-976386c232f2)

> Who is the owner of the group? { jOk3xxx }


### When was the photo of the building taken?
Karena di gambar terdapat watermark google, dapat dipastikan bahwa gambar tersebut bukan diambil secara langsung, melainkan diambil dari google street view. Cek google street view dan lihat tanggal lainnya. Foto di grup telegram cocok dengan streetview di tahun 2011 (perhatikan gambar bunga taman berbentuk segitiga di bawah lampu hijau. bunga tersebut hanya muncul di streetview tahun 2011).

![image](https://github.com/user-attachments/assets/3fc233b7-2894-49d4-91c2-b1d4fb4b59bb)

> When was the photo of the building taken? { 20xx }


## Day 3, Task 1
After obtaining the location from the image, the investigation team was deployed to the site for preliminary surveillance using an elite unit trained in covert observation. Some team members even disguised themselves as local residents and entered a nearby bar. There, from an adjacent table, they observed a man in his thirties who appeared to be scanning his surroundings as if searching for someone, frequently checking his watch. The team then approached him under the pretense of being first-time tourists visiting the area.

![image](https://github.com/user-attachments/assets/7530eba4-2ed6-415d-b2c7-fd77a057ce84)

Upon making contact, the team introduced themselves and soon learned that the man was named "Ross Jennings" He explained that he was waiting for a friend who was supposed to treat him to drinks, but his friend had not yet arrived. Additionally, he shared that his background was as a salt harvester in Ireland. The team maintained surveillance until late at night, and no suspicious individuals with mysterious appearances were observed in the surrounding area.

![image](https://github.com/user-attachments/assets/8ccee753-a9e4-44ac-9cd3-c19838e58c23)

As it was getting late and suspicious activity was no longer visible, we returned with very limited information - information that was, shall we say, insignificant. Even so, every scrap of data is valuable in the context of an ongoing investigation. With these limitations, we're reaching out to you, our go-to player, to help solve the puzzle from the minimal information we've obtained.

What will be your next step?

### What's odd about ross jennings' statement?
Yang janggal / aneh dari statement ross jennings adalah dia menunggu temannya dan temannya tersebut memiliki background sebagai salt harvester di Ireland. Janggal karena dia memberikan detail berlebih yang sebenarnya tidak diperlukan. Orang ketika bohong, gugup, atau grogi biasanya akan memberikan detail berlebih yang tidak diperlukan ketika berbicara. Selain itu Irlandia beriklim dingin dan biasanya Salt Harvesting biasanya dilakukan di daerah beriklim tropis dengan paparan sinar matahari yang cukup agar dapat mempercepat penguapan air laut dalam proses pembuatan garam. Sehingga pekerjaan salt harvester di Irlandia sepertinya cukup janggal dan mungkin mengada-ngada, kemungkinan besar dia berbohong dan dia bohong dengan alibi yang buruk karena gugup.

> What's odd about ross jennings' statement? { saxx harvxxxxxx }

### What does ross jennings do for a living?
Untuk mengetahui pekerjaan Ross Jennings kita bisa mengecek sosial medianya. Karena hint dari pertanyaan setelah ini adalah "A little birdie told me.." kita bisa mulai mencari di twitter.

![image](https://github.com/user-attachments/assets/b9f409f0-fc0d-4553-829f-65c6b96b85e1)

Ditemukan akun twitter dengan nama Ross Jennings, dia berasal dari Ireland dan foto profilnya cocok dengan wajahnya. Di bio akun tersebut tertulis "Ex-ARW & G2 intel. Now offering private security & protection services when needed. Living the quiet life in Cobh, but always ready for action."

![image](https://github.com/user-attachments/assets/91a068cf-aea1-421f-95bd-980f918d33d0)


Ex-ARW and G2 Intel. ARW (Army Ranger Wing) merupakan pasukan operasi khusus militer irlandia, dan G2 merujuk ke staff intelijen militer Amerika Serikat. Dia merupakan mantan pekerja di dua tempat tersebut. Sekarang dia menawarkan layanan private security & protection. Bisa dibilang bahwa dia merupakan Tentara Bayaran (mercenaries).

![image](https://github.com/user-attachments/assets/2e78f1c3-0d55-4eff-8325-a9f361618333)

> What does ross jennings do for a living? { mercxxxxxxx }


### What's the username of ross social media?
Username sosial media yang ross gunakan berdasarkan informasi yang diperoleh dari challenge sebelumnya adalah @r_jennings70

![image](https://github.com/user-attachments/assets/b9f409f0-fc0d-4553-829f-65c6b96b85e1)

> What's the username of ross social media? { r_jenxxxxxxx }


### Where did might be the perpetrator lurk on the day of the encounter?
Berdasarkan kejadian sebelumnya ("Some team members even disguised themselves as local residents and entered a nearby bar. There, from an adjacent table, they observed a man in his thirties who appeared to be scanning his surroundings as if searching for someone, frequently checking his watch. The team then approached him under the pretense of being first-time tourists visiting the area."), diketahui bahwa tim bertemu dengan Ross Jennings di dalam sebuah bar di lokasi sekitar.

Lokasi pertemuan ada di Grand Parade, dekat National Monument, Cork, Ireland. Berarti tim menemui Ross Jennings di sebuah bar di sekitar National Monument di Grand Parade. Kita bisa menggunakan google street view untuk melihat bar di sekitar lokasi.

Jika kita berdiri dari arah foto diambil dan melihat ke kanan terdapat toko dengan banner gambar bir besar diatasnya. Kemungkinan besar itu adalah Bar dimana tim bertemu dengan Ross Jennings. Jadi besar kemungkinan perpetrator mengintai dari dalam bar itu juga. Nama bar tersebut adalah Deep South.

![image](https://github.com/user-attachments/assets/11b0e0d4-e247-4a8d-a9be-7f6547923ea5)

> Where did might be the perpetrator lurk on the day of the encounter? { Dexx Soxxx }


## Day 3, Task 2
After conducting a SOCMINT on the suspect, the team found a number of peculiarities in the digital activities left by the social media targets associated with the suspect.

Based on these findings, we decided to strategically divide the tasks. Players will focus on exploring SOCMINT by digging further into the suspect's digital footprint, interaction traces and online activities to gather additional information that can strengthen the initial analysis. Meanwhile, investigators are tasked with finding and verifying the suspect's home address using digital investigation techniques cross-referencing data from public sources.

This division of tasks is expected to speed up the evidence collection process and provide a more comprehensive picture of the target's physical location, so that follow-up steps can be carried out appropriately and effectively.

### What is the full name of he's daughter?
Karena kita sudah menemukan twitter milik tersangka pada challenge sebelumnya, kita akan mencari informasi mengenai anaknya di twitter tersangka. Ditemukan tweet dimana tersangka meminta doa untuk anaknya. Dan terdapat URL rumah sakit di tweet tersebut.

![image](https://github.com/user-attachments/assets/8fa7091b-f0cf-4c47-8ecc-125575da461f)

URL tersebut berisi daftar nama pasien perempuan dan terdapat nama "Hellen Jennings" yang dicetak tebal. Hellen Jennings merupakan anak perempuan dari tersangka karena dia menggunakan nama belakang "Jennings" sama seperti ayahnya "Ross Jennings".

![image](https://github.com/user-attachments/assets/b8dd55fe-9b75-4c2a-bb20-8c47bfc0a143)

> What is the full name of he's daughter? { Hxxxxx Jennings }


### What disease does the daughter of he have?
Berdasarkan dokumen di URL tadi diketahui bahwa anak tersangka mengidap penyakit cancer

> What disease does the daughter of he have? { canxxx }


### Who is he might be working for?
Tersangka berkerja sebagai mercenaries dan kemungkinan dia dibayar oleh seseorang untuk melakukan pekerjaan ini. Dari informasi yang ditemukan pada challenge sebelumnya diketahui bahwa owner dari grup telegram adalah j0k3r dan kita beberapa kali menemukan nama tersebut di challenge lain sepanjang penyelidikan kasus ini. j0k3r juga merupakan orang yang memberikan berbagai challenge ini ke kita, seperti yang diketahui dari pastebin terakhir di Day 2, Task 2 (Joker@phantomt.id).

> Who is he might be working for? { j0kxx }


### What's the name of his sockpuppet?
Nama akun palsu (sockpuppet) milik tersangka adalah "Elene Kurtanidze". Diketahui dari challenge Day 2, Task 3 dimana dia merupakan orang yang mengirim pesan berupa gambar petunjuk lokasi pertemuan di telegram.

Selain itu pelaku juga ada membuat tweet dimana dia berkata bahwa anak perempuannya sangat menyukai Elene Kurtanidze.

![image](https://github.com/user-attachments/assets/05991bda-4d39-4830-9d70-f502231bc8ea)


> What's the name of his sockpuppet? { Exxxx Kurtxnxxxx }


### What is his full address?
Kita bisa menemukan alamat pelaku dari website rumah sakit dimana anaknya dirawat. Di daftar pasien perempuan yang ada di website rumah sakit tersebut, klik nama anaknya dan kita akan diarahkan ke srcibd yang berisi dokumen invoice biaya perawatan anaknya. Di dokumen tersebut ada alamat lengkapnya.

![image](https://github.com/user-attachments/assets/c253c76a-f3a5-4f31-b261-6e41fce3edcf)

> What is his full address? { 4x Uxxxx Jxxx Sx Cxxx }


### Which hospital is the child currently in?
Nama rumah sakitnya adalah Cork University Hospital. Nama ini dapat kita peroleh dari website rumah sakit, atau di dokumen invoice di scribd tadi.

![image](https://github.com/user-attachments/assets/72d52cb6-3ed1-4767-9bd2-cee71c2689da)

> Which hospital is the child currently in? { Cxxx Uxxxxxx Hxxxxx }


### How much did the man have to pay for his daughter's surgery?
Biaya operasi anaknya adalah $200.000.000. Bisa dilihat di dokumen invoice di scribd.

![image](https://github.com/user-attachments/assets/a017f8af-c868-4124-9ec5-75044fc7b9aa)

> How much did the man have to pay for his daughter's surgery? { $xxx.xxx.xxx }


### When is ross's daughter's birthday?
Tersangka pernah mereply sebuah tweet mengenai hadiah ulang tahun anaknya. Hadiah tersebut sepertinya adalah konser yang akan digelar pada tanggal 6 maret.

![image](https://github.com/user-attachments/assets/58944ab4-5aef-456c-8abc-157921b29e5f)

Diketahui sekarang anaknya berusia 12 tahun (informasi dari website rumah sakit). Berarti 2025 - 12 = 2013. Karena data di rumah sakit kemungkinan dibuat di awal tahun 2025 lalu sekarang belum
bulan maret dan anaknya masih berusia 12 tahun, ini berarti anaknya lahir pada tahun 2012.

Berarti tanggal lahir anaknya adalah 03-06-2012 (mm-dd-yyyy).

> When is ross's daughter's birthday? { xx-xx-20xx }


## Day 3, Task 3
After the player successfully identifies the suspect’s exact address, the investigator and their team proceed to raid Ross’s residence. Upon arrival, they discover that the house is unlocked. Exercising caution, the team enters and begins assessing the scene. Tragically, they find the suspect, Ross, deceased from an apparent self-inflicted gunshot wound to the head. A pistol is found in proximity, suggesting a possible suicide.

![image](https://github.com/user-attachments/assets/609a5edd-6b4a-4e28-9d3f-4076f3ac3c48)

The investigator and their team step cautiously into Ross’s residence, the door eerily left unlocked. The dim light casts long shadows across the room, revealing a motionless figure slumped on the floor. In Ross’s hand, a Glock 17 pistol, its barrel still warm. The scent of gunpowder lingers in the air, Scattered nearby, .45 ACP rounds, considering the weapon in his grasp. A laptop sits on the desk, screen frozen, locked out.

Then, while searching the small shelf of the desk, the team discovered a piece of paper bearing a mysterious code.

![image](https://github.com/user-attachments/assets/66f4cfa3-5f8f-4c12-b794-33567198b1f7)

Not far from there, a floor with a distinct echo sounded beneath each step, amplifying the sense of uncertainty in the air. Upon closer inspection, a hidden mechanism was discovered beneath the surface—a cleverly concealed cover, designed to obscure what lay beneath. The investigator carefully opened it, revealing an intricate locking system with four columns, each requiring a specific digit to unlock the room. The puzzle seemed to stretch out endlessly, urging the team to decipher the correct combination.

![image](https://github.com/user-attachments/assets/2eba8cc4-7e21-44d5-8f8b-25d5bca26cb0)

On the nearest floor, a strange carving caught the eye of the investigator—a symbol often associated with unlocking or revealing something hidden. The engraving depicted a lock, labeled as 🔓, with symbols etched beneath it: ✊️ ✋️ ✌️ ✍️. This cryptic inscription posed a new puzzle. What did these symbols truly signify?
example:
🔓 = ✊️ ✋️ ✌️ ✍️

After successfully cracking the initial code, we were led into a dimly lit underground chamber. In the far corner of the room stood a large safe secured with another 4-digit code with image in bottom of safe:
 🔓 =✊️✌️✊️✋️

![image](https://github.com/user-attachments/assets/cdcbd435-277c-4865-8d7e-d49691c02e02)


### What was the cause of Ross' death?
Hint: is it real suicide?

Sepertinya penyebab kematian ross bukan bunuh diri. Karena pintu rumah tidak dikunci (kemungkinan jalur keluar pelaku) dan pistol yang dipegang Ross adalah Glock 17 sedangkan peluru yang berceceran adalah .45 ACP. Seharusnya Glock 17 menggunakan peluru 9mm bukan .45 ACP.

![image](https://github.com/user-attachments/assets/da147db2-5f60-4929-9b8c-1282fe3172a4)

![image](https://github.com/user-attachments/assets/7d704336-a7c5-47bc-8fbf-a0889bc0b860)

> What was the cause of Ross' death? { kilxxx }


### What's strange about crime scene evidence?
Yang aneh dari tempat kejadian adalah selongsong peluru (shell) yang digunakan.  Seharusnya Glock 17 menggunakan peluru 9mm bukan .45 ACP

> What's strange about crime scene evidence? { shxxx }


### What are the value of the following variables? (sort according to the question) ✊️,✋️,✌️,✍️
Definisikan emoji sebagai variabel. ✊ (Fist) = x, ✋ (Open Hand) = y, ✌️ (Victory Hand) = z, ✍️ (Writing Hand) = w. Dari petunjuk gambar yang ada di laci diketahui bahwa :

![image](https://github.com/user-attachments/assets/cd8ab85c-1ef8-41cc-8ecf-4caba9263ab8)

Berarti x + y = 9, z + w = 3, x + z = 4, w = y − 4.

    y = x - 9
    
    w = (x - 9) - 4
    w = 5 - x
    
    z = 4 - x
    
    (4x - x) + (5 - x) = 3
    9 − 2x = 3
    −2x = −6
    x = 3 (✊)
    
    y = 9 − 3 = 6 (✋)
    z = 4 − 3 = 1 (✌️)
    w = 5 − 3 = 2 (✍️)

> What are the value of the following variables? (sort according to the question) ✊️,✋️,✌️,✍️ { 3,x,x,x }


### What is the code for an underground door locker?
Kode pintu bawah tanah adalah 🔓 = ✊️ ✋️ ✌️ ✍️. Berdasarkan perhitungan tadi, berarti kodenya adalah 3612.

> What is the code for an underground door locker? { 3xxx }


### What is the code for the safe in the basement?
Kode untuk safe (brangkas) di basement adalah 🔓 =✊️✌️✊️✋️. Berdasarkan perhitungan tadi, berarti kodenya adalah 3136.

> What is the code for the safe in the basement? { 3xxx }


## Final Task
Inside the safe, we discovered two crucial items that had long eluded us a stolen vase, the very artifact we had been relentlessly pursuing, and a handwritten note bearing a message from J0K3R, the mastermind behind the museum theft.

The note read:

    "Well done, detective. You've completed the warm-up game! I hope you're ready for the real challenge ahead.
    You see, everything that has happened so far? It's all been part of the plan. Every twist, every turn, every clue... all neatly aligned.
    But don’t get too comfortable this was just the beginning.
    I trust the next stages will keep you on your toes. Let’s see how you fare with the real puzzles. It's been fun... for now."
    
    Signed,
    J0K3R


### What was Ross Jennings' involvement in this incident?
Bisa disimpulkan bahwa keterlibatan Ross Jennings dalam kasus ini adalah sebagai mercenary (tentara bayaran). Kemungkinan besar dia berkerja untuk j0k3r karena memerlukan biaya yang besar untuk operasi anak perempuannya.

> What was Ross Jennings' involvement in this incident? { mercxxxxx }


### Is this robbery case over yet?
Kasus ini belum selesai karena kita belum mengetahui identitas j0k3r.

> Is this robbery case over yet? { Nx }





