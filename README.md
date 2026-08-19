## Intro

Zunächst eine Erklärung was das Gesamtkonzept ist. Der Server kann entweder etwas was auf ihm gespeichert ist zur Verfügung stellen, oder vice versa Speicherplatz zur Verfügung stellen damit ihr keine großen Datenmengen bei euch lagern müsst. Außerdem kann er euch seine Rechenleistung zur Verfügung stellen, z.B. für Minecraft Server oder am Ende sogar lokale KI, aber dafür hab ich noch keine Grafikkarte und die Modelle sind momentan noch zu groß und brauchen ultra High-End Computer um mit Gemini oder ChatGPT oder so halbwegs konkurrieren zu können.

![Netzwerk Struktur](Netzwerk_Struktur.png)

Aber egal was auf dem Server läuft, ist in Containern, die man über eine Internetadresse besuchen kann. Meine Blu-Ray Sammlung beispielsweise läuft mit dem Bibliotheksverwaltungsprogramm Jellyfin unter der Adresse 192.168.0.182:8095. 
Kleine Erklärung zu diesen Adressen:

192.168.0 is ganz schlicht gesagt das Präfix zu allem was im lokalen Netzwerk ist. Jedes Gerät hat dann nur noch eine ID die man dranhängt. Der Server hat die ID 182. Dadurch hat er die IP in meinem lokalen Netzwerk von 192.168.0.182. Euer Handy könnte zb die ID 45 oder so haben und dann die IP adresse 192.168.0.45. 

Wenn ihr einen Service vom Router benutzen wollt braucht ihr also einmal die IP Adresse, aber weil dem Server vom Router nur 1 IP Adresse zugeteilt wird, öffnet er für jeden Service nochmal einen eigenen Port über den nur dieser eine Service läuft. Jellyfin Filme hat die Port Nummer 8095, werdet ihr in eurem Browser (oder der Desktop Anwendung die ich sehr empfehle) unter 192.168.0.182:8095 benutzen können. Jellyfin Musik hat 192.168.0.182:8096, ist also der Nachbar von eins drüber. Um aber wirklich bei meinem Jellyfin zu landen müsst ihr aber im gleichen Netzwerk wie mein Server sein.

## Tailscale Install

Da mein Heimnetz aber abgeschlossen ist und keine externen Zugriffe zulässt, müsst ihr euch zu mir reintunneln. Dafür brauchen wir Tailscale. Das ist mehr oder weniger unser eigener VPN. Ihr aktiviert Tailscale auf eurem Gerät, werdet damit zu einem Tailscale server verbunden, der euch wiederum direkt an meinen Server weiterleitet (da dieser die "Exit Node" in unserem Subnetz ist) und ihr landet in dem Netzwerk in dem sich mein Server befindet. Jetzt funktionieren auch die Zugriffe zum Server.

Tailscale könnt ihr hier herunterladen: https://tailscale.com/download

Nach dem Download einmal anmelden und dem Subnet beitreten, dem euer Account dann schon angehören sollte. Falls ihr da Probleme habt gerne melden.

Gerade bei mobilen Geräten ist Tailscale zum Filme schauen und Musik oder Hörbücher hören für unterwegs sehr praktisch. Eure Internetgeschwindigkeit wird null beeinträchtigt und ihr seid dazu noch etwas privater Unterwegs weil random IP Adresse in einem Subnetz von Tailscale.

## Troubleshooting

Es kann gut sein, dass euer Router zuhause auch genau 192.168.0 als Präfix vergibt (z.B. wenn ihr auch Vodafone habt), dann müsst ihr stattdessen die IP-Adresse vom Router in unserem Tailscale VPN benutzen. Diese lautet 100.70.111.47

## Services

Da ihr jetzt im Netzwerk seid, könnt ihr die folgenden Dienste alle nutzen:

* [Jellyfin Filme](#jellyfin-filme)
* [Jellyfin Musik](#jellyfin-musik)
* [Obsidian](#obsidian)
* [Immich](#immich)
* [Audiobookshelf](#audiobookshelf)

## Jellyfin Filme

Damit der Server euch die beste Video- und Audioqualität zur Verfügung stellen kann, muss er genau wissen, was euer Gerät Decodieren kann, damit er Korrekt Encodiert. Anstatt Jellyfin einfach im Browser zu benutzen, was natürlich geht, würde ich euch deshalb die extra App dazu ans Herz legen. Da die meisten Browser sich keine Mühe geben gute Audiocodecs zu unterstützen, muss der Server euch das runterrechnen, was unnötig Leistung und Strom zieht. Am besten ladet ihr euch für Laptop/Desktop die "Jellyfin Media Player" Anwendung und für Handy/iPad die "Jellyfin" App runter. Dann können Server und Endgerät das optimale gemeinsame Format finden und in den meisten Filmen muss der Server dann nämlich gar nichts umrechnen.

[Jellyfin Media Player](https://github.com/jellyfin/jellyfin-desktop)

[Jellyfin Android](https://play.google.com/store/apps/details?id=org.jellyfin.mobile)

[Jellyfin iOS](https://apps.apple.com/us/app/jellyfin-mobile/id1480192618)

Tja und sobald ihr die richtige Anwendung habt werdet ihr nach der Serveradresse gefragt. Denkt dran, dass ihr Tailscale im Hintergrund laufen lassen müsst, damit der Server gesehen wird. Die Adresse ist 

192.168.0.182:8095

Danach werdet ihr nach Usernamen und Passwörtern gefragt. Ich hab für euch alle einen Account mit folgenden Credentials eingerichtet:

Username: Euer vorname (alles klein)

Passwort: abcdefgh

Das Passwort könnt ihr jederzeit ändern. Viel Spaß beim schauen!!✨✨

## Jellyfin Musik

Hier könnt ihr eigentlich der Anleitung [Jellyfin Filme](#jellyfin-filme) folgen. Ablauf und Accounts sind identisch. Zum aufm Handy Musik hören benutze ich persönlich aber [Symfonium](https://play.google.com/store/apps/details?id=app.symfonik.music.player&referrer=utm_source%3Dwebsite%26utm_medium%3Dcta%26utm_campaign%3Dsite_home%26utm_content%3Dhero_primary), was es leider nur für Android gibt. Es gibt aber eine Million Alternativen. Ihr könnt hier nur Musik abspielen, die ich bereits auf dem Server habe. Aber natürlich könnt ihr sie auch aufs Handy runterladen für Offline use. Ist alles FLAC, also sehr hohe Qualität, dementsprechend glaub so 20GB ca. momentan. Falls ihr großes Interesse hättet Spotify und so actually nicht mehr zu benutzen, könnte man auch paar Sachen einrichten, dass ihr selber Musik hinzufügen könnt, aber bisher hat es mich nicht gestört mal auf der Musik die bisher da ist auszuruhen. Momentan ist das natürlich auch nur meine eigene Musik, eure Bibliotheken einzurichten ist aber möglich und euer Spotify rüberzukopieren in Theorie auch. Könnt mir einfach mal sagen falls ihr Interesse habt.

Port: http://192.168.0.182:8096


## Obsidian
[Obsidian](https://obsidian.md/) ist ein absolut tolles Notizen-Programm, was für mich momentan OneNote ersetzt. Hab damit z.B. das Netzwerk Schema im [Intro](#intro) gemacht. Damit man das auch schön über alle Geräte synchronisiert benötigt ihr das Plug-In "Self-hosted LiveSync". Das braucht etwas mehr Account setup als Jellyfin, weshalb ich das nicht für euch alle einfach mal so vorbereitet habe, aber dauert wirklich nur 5min und falls das jemand von euch gerne benutzen mag auch hier einfach sagen.

## Immich
[Immich](https://immich.app/) ist einfach Google Photos nur selber gehostet und damit privat und nicht KI Futter :)
Ne ehrlich, ist einfach gut zu Wissen man hat seinen Stuff bei sich selber. Das braucht auch einmal ne Account Einrichtung und dann könnt ihr das benutzen, schreibt gerne falls ihr Interesse habt. 

Port: http://192.168.0.182:30041/


## Audiobookshelf
[Audiobookshelf](https://audiobookshelf.org/) hab ich erst neulich eingerichtet, da sind bisher nur die ersten 4 Harry Potter teile drauf. Aber denke da werden noch einige Hörbücher und eBooks kommen und falls ihr da schon was habt gerne her damit :)

[Android](https://play.google.com/store/apps/details?id=com.audiobookshelf.app&hl=en-US)

Auf iOS scheint es als Alternative [FableFrog](https://apps.apple.com/us/app/fable-frog/id6760953386) zu geben.

Port: http://192.168.0.182:30067/


## Abschluss
Der Server hat momentan einen redundanten 4TB Pool (Musik, Obsidian, Immich, Audiobookshelf) und zwei nicht redundante 3TB Pools (Filme).  Mehr Speicher und vor allem mehr Redundanz aufzubauen ist super wichtig damit einerseits mehr und außerdem nichts verloren geht. Am besten wären tatsächlich mehrere Server auf unsere Homes verteilt die die wichtigsten Sachen auf alle verteilt synchronisieren. Dann geht wirklich nichts verloren.

Also falls ihr jemanden kennt der Festplatten mit mehreren Terabyte günstig abgeben würde oder Computer loswerden will (man kann aus allem einen Server machen), dann wärs mega wenn ihr mir das weiterleitet <3