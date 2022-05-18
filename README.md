# FS22-Multi-Terrain-Angle
Anleitung zum Einbau von 32 Bodenwinkeln in Modmaps (Deutsch)

English version down below!

Im Standard Spiel sind die Bodenwinkel auf 8 begrenzt. Dies sieht teils sehr unschön aus, weshalb man mit dieser Anleitung dem Abhilfe schaffen kann. Die Angaben basieren auf mehreren Artikeln, aus dem Giants- sowie FBM Forum und sind am Ende verlinkt.

Gestartet wird mit einer entpackten (**kein zip**) Karte. Es darf sich auch keine gepackte Version im selben Verzeichnis befinden, da der Editor sonst diese lädt!

1) **"maps/data/densityMap_ground.gdm"** mit GRLE-Konverter (Download unter https://gdn.giants-software.com/downloads.php) in PNG konvertieren, Original aus dem Map-Ordner löschen. (**Achtung:** Pfad kann abweichen)

2) die beigefügte **"terrainShader.xml"** in maps-Ordner kopieren

3) die beigefügte **"fieldGround.xml"** in maps-Ordner kopieren

4) i3D mit Texteditor bearbeiten

a) Pfad für **"terrainShader.xml"** anpassen

suche folgenden Eintrag
```xml
<File fileId="2" filename="$data/shaders/terrainShader.xml"/>
```
ändern zu 
```xml
<File fileId="2" filename="terrainShader.xml"/>
```
b) unter dem DetailLayer „terrainDetail“ die Zahlen für die Kanäle anpassen. Hier werden 2 hinzugefügt, ergibt dann 32 Winkel.

suche folgenden Eintrag
```xml
<DetailLayer name="terrainDetail" densityMapId="256" numDensityMapChannels="10" compressionChannels="10" cellSize="8" objectMask="16711935" decalLayer="1" viewDistance="75" blendOutDistance="5" densityMapShaderNames="blendMap;blendMap2" combinedValuesChannels="0 4 0;4 3 0;7 3 0">
```
ändere folgende Einträge
```xml
... numDensityMapChannels="12" compressionChannels="12" ... combinedValuesChannels="0 4 0;4 5 0;9 3 0">
```
c) unter Group „GroundAngle“ die Anzahl der Channels und die Winkel hinzufügen. Diese müssen für für die Anzahl der Winkel ausgerechnet werden. Hier 180/32=5.625

ersetze die kompletten Einträge mit folgendem Codeblock
```xml
<Group name="GroundAngle" firstChannel="4" numChannels="5" >
<Option value="1" name="-5.625 Degrees"/>
<Option value="2" name="-11.25 Degrees"/>
<Option value="3" name="-16.875 Degrees"/>
<Option value="4" name="-22.5 Degrees"/>
<Option value="5" name="-28.125 Degrees"/>
<Option value="6" name="-33.75 Degrees"/>
<Option value="7" name="-39.375 Degrees"/>
<Option value="8" name="-45 Degrees"/>
<Option value="9" name="-50.625 Degrees"/>
<Option value="10" name="-56.25 Degrees"/>
<Option value="11" name="-61.875 Degrees"/>
<Option value="12" name="-67.5 Degrees"/>
<Option value="13" name="-73.125 Degrees"/>
<Option value="14" name="-78.75 Degrees"/>
<Option value="15" name="-84.375 Degrees"/>
<Option value="16" name="-90.0 Degrees"/>
<Option value="17" name="-95.625 Degrees"/>
<Option value="18" name="-101.25 Degrees"/>
<Option value="19" name="-106.875 Degrees"/>
<Option value="20" name="-112.5 Degrees"/>
<Option value="21" name="-118.125 Degrees"/>
<Option value="22" name="-123.75 Degrees"/>
<Option value="23" name="-129.375 Degrees"/>
<Option value="24" name="-135.0 Degrees"/>
<Option value="25" name="-140.625 Degrees"/>
<Option value="26" name="-146.25 Degrees"/>
<Option value="27" name="-151.875 Degrees"/>
<Option value="28" name="-157.5 Degrees"/>
<Option value="29" name="-163.125 Degrees"/>
<Option value="30" name="-168.75 Degrees"/>
<Option value="31" name="-174.375 Degrees"/>
</Group>
```
d) unter Group **„SprayType“** den firstChannel korrigieren
```xml
<Group name="Spraytype" firstChannel="9" numChannels="3" >
```
5) in der **"map.xml"** den Pfad zur fieldGround.xml anpassen (**Achtung:** Pfad kann abweichen)
```xml
<fieldGround filename="maps/fieldGround.xml" />
```
6) **optional!** Anpassung der **"fieldGround.xml"**

Wenn die map eigene InfoLayer für Düngung, Kalk, Steine, Unkraut etc. verwendet muss man die Pfade in der **"fieldGround.xml"** anpassen, da die beigefügte Datei die Standard-Werte der US Karte verwendet. Dazu in folgendem Codeblock die entsprechenden Pfade anpassen und auf die eigenen Dateien verlinken.
```
<sprayLevel filename="$data/maps/mapUS/data/infoLayer_sprayLevel.png" firstChannel="0" numChannels="2" maxValue="2"/>
<limeLevel filename="$data/maps/mapUS/data/infoLayer_limeLevel.png" firstChannel="0" numChannels="2" />
<plowLevel filename="$data/maps/mapUS/data/infoLayer_plowLevel.png" firstChannel="0" numChannels="1" />
<stubbleShredLevel filename="$data/maps/mapUS/data/infoLayer_stubbleShredLevel.png" firstChannel="0" numChannels="1" />
<rollerLevel filename="$data/maps/mapUS/data/infoLayer_rollerLevel.png" firstChannel="0" numChannels="1" />
```
hier dann jeweils den Pfad `$data/maps/mapUS/data/...` anpassen

7) Map im Giants Editor laden, Log auf Fehler prüfen. Wenn erfolgreich (keine Fehler) wieder abspeichern. Dann hat man eine neue "densityMap_ground.gdm" und die PNG im "maps/data" kann gelöscht werden.

8) Wenn der Giants Editor beim Öffnen der map.i3d crasht muss der Name der **densityMap_ground.gdm** von xxx.gdm zu xxx.png innerhalb der **map.i3d** geändert werden!

original (**fileId und Pfad kann abweichen**)
```
<File fileId="331" filename="data/densityMap_ground.gdm"/>
```
ändern zu 
```
<File fileId="331" filename="data/densityMap_ground.png"/>
```

Dann map.i3d erneut öffnen, dieses Mal ohne Crash und wenn ohne Fehler, map abspeichern.

**Wenn es dann immer noch zum Crash kommt, prüfe ob sich die entpackte und die gezippte map nicht auf der selben Ordner-Ebene auf deiner Festplatte befinden, da immer die gezippte präferiert wird. Schiebe dann die gezippte map auf eine andere Ebene!**

9) Wenn Punkt 8 notwendig war, diesen wieder rückgängig machen und die Pfadangabe innerhalb der **map.i3d** wieder von xxx.png zu xxx.gdm ändern.

Link Artikel Giants Forum:
https://forum.giants-software.com/viewtopic.php?f=884&t=182812

Link Artikel FBM Forum
https://forbidden-mods.de/forum/thread/12289-tut-multi-terrain-angle-mehr-bodenwinkel-einer-mod-map-hinzuf%C3%BCgen/

Dies ist nur nochmal eine Zusammenfassung der Handlungsanweisungen sowie Adaption auf Modmaps. Solltet ihr Dateien aus dem Hauptverzeichnis und/ oder aus dem $data ändern, sind vorher immer Backups anzulegen! Es wird keine Haftung für kaputte Spielinstallationen und/ oder Savegames übernommen!

_______________________________________________________________________

# FS22-Multi-Terrain-Angle
Guideline for integration of 32 groundangles to Modmaps (Englisch)

In the basegame the groungangles are limited to 8. This often looks not very nice, so i will help you to change them and make the game much more prettier. All given information is based on several forum threads, from Giants- and FBM forum and they are linked at the end.

Starting with an unzipped (**no zip**) map. Be sure that no zipped version of the map is located in the same folder, because editor will load this one!

1) converting **"maps/data/densityMap_ground.gdm"** with GRLE-converter (you can get this from https://gdn.giants-software.com/downloads.php) into PNG, original from map folder should be deleted. (**Attention:** path could vary depending on your folder structure)

2) copy attached **"terrainShader.xml"** into your maps folder

3) copy attached **"fieldGround.xml"** into your maps folder

4) editing map.i3D with text editor like notepad++ or anything else

a) edit path of **"terrainShader.xml"**

search for following entry
```xml
<File fileId="2" filename="$data/shaders/terrainShader.xml"/>
```
change it to
```xml
<File fileId="2" filename="terrainShader.xml"/>
```
b) search in detaillayer section for „terrainDetail“ and vary the numbers for the channels. There were 2 added, so in total it should be 32.

search for
```xml
<DetailLayer name="terrainDetail" densityMapId="256" numDensityMapChannels="10" compressionChannels="10" cellSize="8" objectMask="16711935" decalLayer="1" viewDistance="75" blendOutDistance="5" densityMapShaderNames="blendMap;blendMap2" combinedValuesChannels="0 4 0;4 3 0;7 3 0">
```
change this values
```xml
... numDensityMapChannels="12" compressionChannels="12" ... combinedValuesChannels="0 4 0;4 5 0;9 3 0">
```
c) in section „GroundAngle“ edit the quantity of channels and angles. These should be calculated for 32 angles, here 180/32=5.625

replace the complete entry with given codeblock
```xml
<Group name="GroundAngle" firstChannel="4" numChannels="5" >
<Option value="1" name="-5.625 Degrees"/>
<Option value="2" name="-11.25 Degrees"/>
<Option value="3" name="-16.875 Degrees"/>
<Option value="4" name="-22.5 Degrees"/>
<Option value="5" name="-28.125 Degrees"/>
<Option value="6" name="-33.75 Degrees"/>
<Option value="7" name="-39.375 Degrees"/>
<Option value="8" name="-45 Degrees"/>
<Option value="9" name="-50.625 Degrees"/>
<Option value="10" name="-56.25 Degrees"/>
<Option value="11" name="-61.875 Degrees"/>
<Option value="12" name="-67.5 Degrees"/>
<Option value="13" name="-73.125 Degrees"/>
<Option value="14" name="-78.75 Degrees"/>
<Option value="15" name="-84.375 Degrees"/>
<Option value="16" name="-90.0 Degrees"/>
<Option value="17" name="-95.625 Degrees"/>
<Option value="18" name="-101.25 Degrees"/>
<Option value="19" name="-106.875 Degrees"/>
<Option value="20" name="-112.5 Degrees"/>
<Option value="21" name="-118.125 Degrees"/>
<Option value="22" name="-123.75 Degrees"/>
<Option value="23" name="-129.375 Degrees"/>
<Option value="24" name="-135.0 Degrees"/>
<Option value="25" name="-140.625 Degrees"/>
<Option value="26" name="-146.25 Degrees"/>
<Option value="27" name="-151.875 Degrees"/>
<Option value="28" name="-157.5 Degrees"/>
<Option value="29" name="-163.125 Degrees"/>
<Option value="30" name="-168.75 Degrees"/>
<Option value="31" name="-174.375 Degrees"/>
</Group>
```
d) in section **„SprayType“** correct firstChannel
```xml
<Group name="Spraytype" firstChannel="9" numChannels="3" >
```
5) editing the path in **"map.xml"** to "fieldGround.xml" (**Attention:** path could vary depending on your folder structure)
```xml
<fieldGround filename="maps/fieldGround.xml" />
```
6) **optional!** editing the **"fieldGround.xml"**

If your map has its own infolayers for spray, lime, stones etc. you'll have to change the paths in **"fieldGround.xml"**, because the attached fieldGround.xml uses the standard infolayers from US map. You have to edit the paths and link to your own files. You have to edit following codeblock in the **"fieldGround.xml"**.
```
<sprayLevel filename="$data/maps/mapUS/data/infoLayer_sprayLevel.png" firstChannel="0" numChannels="2" maxValue="2"/>
<limeLevel filename="$data/maps/mapUS/data/infoLayer_limeLevel.png" firstChannel="0" numChannels="2" />
<plowLevel filename="$data/maps/mapUS/data/infoLayer_plowLevel.png" firstChannel="0" numChannels="1" />
<stubbleShredLevel filename="$data/maps/mapUS/data/infoLayer_stubbleShredLevel.png" firstChannel="0" numChannels="1" />
<rollerLevel filename="$data/maps/mapUS/data/infoLayer_rollerLevel.png" firstChannel="0" numChannels="1" />
```
change the paths `$data/maps/mapUS/data/...` to your file-address

7) loading map into Giants Editor, check log for failures. If succesfull (no failure entries in log) save the map.i3d. Now you got a new "densityMap_ground.gdm" and the PNG in "maps/data" could be deleted.


8) If Giants Editor crashes by opening map.i3d, the name of **densityMap_ground.gdm** have to be changed from xxx.gdm to xxx.png inside **map.i3d**!

original (**fileId and path could vary**)
```
<File fileId="331" filename="data/densityMap_ground.gdm"/>
```
change to 
```
<File fileId="331" filename="data/densityMap_ground.png"/>
```

Then open map.i3d again, hopefully this time without crash and save it when there are no errors.

**If the map also crashes, be sure that unzipped and zipped map are not located at the same level on your hard disk. If this is true, paste the zipped one to another level because the zipped map is always preferd by the giants editor**

9) If point 8) was necessary, this have to be reversed inside **map.i3d** and ending from **densityMap_ground** have to be renamed from xxx.png to xxx.gdm

Link thread Giants forum:
https://forum.giants-software.com/viewtopic.php?f=884&t=182812

Link thread FBM forum
https://forbidden-mods.de/forum/thread/12289-tut-multi-terrain-angle-mehr-bodenwinkel-einer-mod-map-hinzuf%C3%BCgen/

This is just another summary of the instructions and adaptation on Modmaps. If you change files from the main directory and/or from the $data, backups must always be created beforehand! No liability is assumed for broken game installations and/or savegames!

**works fine on Calmsden ;)**

![fsScreen_2022_02_06_13_27_53](https://user-images.githubusercontent.com/63619149/153474911-c57e7b7d-bf21-42ca-a1a7-ea0b62d5e7f2.png)
