# TRAITEMENT-DU-SIGNLA--TP2-Jeux-de-mots 
Synthèse et analyse spectrale d’une gamme de musique

![image](https://user-images.githubusercontent.com/79712514/215355282-b1120bdc-7332-4943-8eda-1795a9c41297.png)


OBJECTIFS
Comprendre comment manipuler un signal audio avec Matlab, en effectuant certaines opérations classiques sur un fichier audio d’une phrase enregistrée via un smartphone.  Comprendre la notion des sons purs à travers la synthèse et l’analyse spectrale d’une gamme de musique. Commentaires : Il est à remarquer que ce TP traite en principe des signaux continus. Or, l'utilisation de Matlab suppose l'échantillonnage du signal. Il faudra donc être vigilant par rapport aux différences de traitement entre le temps continu et le temps discret. Tracé des figures : toutes les figures devront être tracées avec les axes et les légendes des axes appropriés. Travail demandé : un script Matlab commenté contenant le travail réalisé et des commentaires sur ce que vous avez compris et pas compris, ou sur ce qui vous a semblé intéressant ou pas, bref tout commentaire pertinent sur le TP

Synthèse-et-analyse-spectrale-d’une-gamme-de-musique
« phrase.wave » est un fichier audio enregistré à l’aide d’un smartphone, en prononçant lentement la phrase :

1- Sauvegardez ce fichier sur votre répertoire de travail, puis charger-le dans MATLAB à l’aide de la commande « audioread ».

[y,Fs]=audioread('phrase.wav');
dt = 1/Fs;
t = 0:dt:(length(y)-1)*dt;
2- Tracez le signal enregistré en fonction du temps, puis écoutez-le en utilisant la commande « sound ».

sound(y,Fs);
3- Cette commande permet d’écouter la phrase à sa fréquence d’échantillonnage d’enregistrement. Ecoutez la phrase en modifiant la fréquence d’échantillonnage à double ou deux fois plus petite pour vous faire parler comme « Terminator » ou « Donald Duck ». En effet, modifier la fréquence d’échantillonnage revient à appliquer un changement d’échelle y(t) = x(at) en fonction de la valeur du facteur d’échelle, cela revient à opérer une compression ou une dilatation du spectre initial d’où la version plus grave ou plus aigüe du signal écouté.

sound(y,2*Fs); %Donald Duck
sound(y,Fs/2); %Terminator
4- Tracez le signal en fonction des indices du vecteur x, puis essayez de repérer les indices de début et de fin de la phrase « Rien ne sert de ».

rien_ne_sert_de = y(5055:77249);
plot(rien_ne_sert_de);
title('Rien ne sert de');
![image](https://user-images.githubusercontent.com/79712514/215355298-1de05a14-2bd2-4379-8a62-7e0ab9f5130b.png)


5- Pour segmenter le premier mot, il faut par exemple créer un vecteur « riennesertde » contenant les n premières valeurs du signal enregistré x qui correspondent à ce morceau. Créez ce vecteur, puis écoutez le mot segmenté.

rien_ne_sert_de = y(5055:77249);
sound(rien_ne_sert_de,Fs);
6- Segmentez cette fois-ci toute la phrase en créant les variables suivantes : riennesertde, courir, ilfaut, partirapoint.

partir_a_point  = y(121652:168300);
il_faut = y(95393:121652);
courir  = y(76613:95393);
rien_ne_sert_de = y(5055:77249);
partir_a_point  = y(121652:168300);
il_faut = y(95393:121652);
courir  = y(76613:95393);
#Synthèse-et-analyse-spectrale-d’une-gamme-de-musique

Les notes de musique produites par un piano peuvent être synthétisées approximativement numériquement. En effet, chaque note peut être considérée comme étant un son pur produit par un signal sinusoïdal. La fréquence de la note « La » est par exemple de 440 Hz.

1- Créez un programme qui permet de jouer une gamme de musique. La fréquence de chaque note est précisée dans le tableau ci-dessous. Chaque note aura une durée de 1s. La durée de la gamme sera donc de 8s. La fréquence d’échantillonnage fe sera fixée à 8192 Hz.

Dol Ré Mi Fa Sol la Si Do2 262 Hz 294 Hz 330 Hz 349 Hz 392 Hz 440 Hz 494 Hz 523 Hz

 m_Fs=8192;
 Ts=1/m_Fs;
 t=[0:Ts:1];
 F_A=440; 
 F_dol=262;
 F_re=294;
 F_m=330;
 F_fa=349;
 F_sol=392;
 F_si=494;
 F_do2=523;
 A=sin(2*pi*F_A*t);
 Dol=sin(2*pi*F_dol*t); 
 re=sin(2*pi*F_re*t);
 mi=sin(2*pi*F_m*t);
 fa=sin(2*pi*F_fa*t);
 so=sin(2*pi*F_sol*t);
 la=sin(2*pi*F_A*t);
 si=sin(2*pi*F_si*t);
 do=sin(2*pi*F_do2*t);

doremifasol_solfamiredo= [Dol,re,mi,fa,so,la,si,do,do,si,la,so,fa,mi,re,Dol];
faded =[fa,fa,fa,si,mi,mi,re,si,si,si,si,fa,fa,fa,mi];
doremifa =[Dol,re,mi,fa,so,la,si,do];
inv =[do,si,la,so,fa,mi,re,do];
sound(doremifasol_solfamiredo,m_Fs);
#Spectre-de-la-gamme-de-musique

rien_ne_sert_de = y(5055:77249);
partir_a_point  = y(121652:168300);
il_faut = y(95393:121652);
courir  = y(76613:95393);
3- Tracez le spectrogramme qui permet de visualiser le contenu fréquentiel du signal au cours du temps (comme le fait une partition de musique) mais la précision sur l’axe des fréquences n’est pas suffisante pour relever précisément les 8 fréquences. image image
![image](https://user-images.githubusercontent.com/79712514/215355389-d814676c-d28c-401b-aeea-d45a7222e9eb.png)
![image](https://user-images.githubusercontent.com/79712514/215355398-935b19f9-e921-4b2a-a995-d37cd8fd7e92.png)

#Approximation-du-spectre-dun-signal-sinusoïdal-à-temps-continu-par-FFT 4- Le spectre d’un signal à temps continu peut être approché par transformée de Fourier discrète (TFD) ou sa version rapide (Fast Fourier Transform (FFT). Afficher le spectre de fréquence de la gamme musicale crée en échelle linéaire, puis avec une échelle en décibels.

Sp=abs(fft(doremifa));
u=mag2db(Sp);
subplot(2,1,1);
fshift=(-length(doremifa)/2:length(doremifa)/2 -1 )*Fs/length(doremifa);
plot(fshift,fftshift(Sp));
title('signal(doremi) spectre');
subplot(2,1,2);
plot(fshift,fftshift(u));
title('signal(doremi) spectre shifted');
![image](https://user-images.githubusercontent.com/79712514/215355435-51594eee-e0e0-43a9-8aec-3629f0de3e7a.png)
