## Scripts de sauvegarde et de restauration des données utilisateur PowerShell


#### Mes objectifs pour créer ceci étaient :

1. Gardez le processus simple
2. Assurer une transition fluide pour mon équipe
3. Sauvegardez et restaurez les mêmes informations qu'avant

#### Qu'est-ce que le script sauvegarde et restaure :

1. Toutes les données utilisateur (Bureau, Documents, Téléchargements, Favoris, Images)
2. Données du navigateur de Google Chrome et Firefox
3. Informations sur l'imprimante réseau et lecteurs réseau mappés

Extrait de code:

```PowerShell
#region DeclaringDataBackupSources
$folder = "Desktop",
  "Downloads",
  "Favorites",
  "Documents",
  "Pictures",
  "AppData\Local\Google\Chrome\User Data",
  "AppData\Local\Mozilla\Firefox\Profiles",
  "AppData\Roaming\Mozilla\Firefox"
#endregion DeclaringDataBackupSources
```

#### Ce qui a été ajouté

J'ai ajouté un petit morceau au script de sauvegarde pour effacer tout le cache du navigateur afin de permettre au temps de sauvegarde de diminuer.

Voici un extrait de ce code :

```Power
##region CacheFolderDeletion Variables (Currently supports Chrome and Firefox)
$delete = "$env:LOCALAPPDATA\Google\Chrome\User Data\Default\Cache\",
  "$env:LOCALAPPDATA\Google\Chrome\User Data\Default\Code Cache\",
  "$env:LOCALAPPDATA\Google\Chrome\User Data\Default\Service Worker\ScriptCache",
  "$env:LOCALAPPDATA\Google\Chrome\User Data\Profile 1\Cache\",
  "$env:LOCALAPPDATA\Google\Chrome\User Data\Profile 1\Code Cache\",
  "$env:LOCALAPPDATA\Google\Chrome\User Data\Profile 1\Service Worker\ScriptCache",
  "$env:LOCALAPPDATA\Mozilla\Firefox\Profiles\*.default\cache",
  "$env:LOCALAPPDATA\Mozilla\Firefox\Profiles\*.default\cache2"
##endregion CacheFolderDeletion Variables

##region DeleteFiles
Write-Host -ForegroundColor Cyan "Begin Browser Cleanup"
Get-ChildItem -Path $delete | Remove-Item -Verbose -Recurse
##endregion
```

Le script a été testé sur Windows 7 et Windows 10 et fonctionne à 100 %.

#### Variables à configurer

Pour le script de sauvegarde :

```PowerShell
$destination
```

Pour le script de restauration :

```PowerShell
$source
```



**Please feel free to use and modify the script to suit your needs.**
