primero arranco abriendo el sitio del laboratorio. este tiene las siguientes preguntas
"What information can you possibly get with just one image file?

Note: This challenge was updated on 2024-02-01. If you are following any older walkthroughs, expect a small change. Additionally, the file is also available on the AttackBox, under the /Rooms/OhSINT directory.
Answer the questions below

What is this user's avatar of?

What city is this person in?

What is the SSID of the WAP he connected to?

What is his personal email address?

What site did you find his email address on?

Where has he gone on holiday?

What is the person's password?"
luego me permite descargar una imagen, la cual se llama "WindowsXP_1551719014755.jpg". usando la herramienta exiftool, ejecuto el siguiente comando:

…/Easy Challenges/OhSINT main ? ❯ exiftool WindowsXP_1551719014755.jpg
ExifTool Version Number         : 13.50
File Name                       : WindowsXP_1551719014755.jpg
Directory                       : .
File Size                       : 234 kB
File Modification Date/Time     : 2026:03:26 21:43:21-03:00
File Access Date/Time           : 2026:03:26 21:46:29-03:00
File Inode Change Date/Time     : 2026:03:26 21:43:21-03:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
XMP Toolkit                     : Image::ExifTool 11.27
GPS Latitude                    : 54 deg 17' 41.27" N
GPS Longitude                   : 2 deg 15' 1.33" W
Copyright                       : OWoodflint
Image Width                     : 1920
Image Height                    : 1080
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 1920x1080
Megapixels                      : 2.1
GPS Latitude Ref                : North
GPS Longitude Ref               : West
GPS Position                    : 54 deg 17' 41.27" N, 2 deg 15' 1.33" W

con esto obtenemos la latitud, longitud y copyright de la foto. si investigamos el copyright, googleandolo encontramos tanto un perfil de github, una pagina de wordpress y un perfil de twitter.

el perfil de github: github.com/OWoodfl1nt/people_finder.git 

el sitio en wordpress: https://oliverwoodflint.wordpress.com/author/owoodflint/

el perfil en twitter: OWoodflint 

en el perfil de twitter podemos ver que tiene una foto de perfil de un gato, entonces con esto resolvemos la primera pregunta: What is this user's avatar of? --> cat 

luego, debemos responder la pregunta de "What city is this person in?". para esto, empezaremos con las coordenadas que nos dan: 54 deg 17' 41.27" N, 2 deg 15' 1.33" W 

si a estas coordenadas las convertimos a grados decimales (latitud: 54.29479722222222, longitud: -2) y buscamos, nos encontramos con un punto en medio de yorkshire dales national park. esto parece ser un callejon sin salida asi que volvemos para atras, a revisar de nuevo los otros sitios. 

en el github, encontramos un repositorio llamado people_finder. si lo abrimos, encontramos el siguiente readme.md:

"Hi all, I am from London, I like taking photos and open source projects.

Follow me on twitter: @OWoodflint

This project is a new social network for taking photos in your home town.

Project starting soon! Email me if you want to help out: OWoodflint@gmail.com

https://oliverwoodflint.wordpress.com/"

entonces con esto respondemos a la pregunta de "What city is this person in?" --> London 

la tercera pregunta propone: "What is the SSID of the WAP he connected to?". esta fue la que mas dificil me resulto. 

en su perfil de twitter encontramos que tiene el siguiente tweet

"From my house I can get free wifi ;D

Bssid: B4:5D:50:AA:86:41 - Go nuts!"

si con este dato nos vamos a wigle

