# Publication du site

Le site est statique : il n'y a pas de commande de build. La publication se fait
en envoyant la branche `master` vers le dépôt GitHub `origin`, ce qui déclenche
la mise à jour de l'hébergement de `https://madebyclo.fr`.

## Git disponible dans GitHub Desktop

La commande `git` n'est pas forcément présente dans le `PATH`. Utiliser celle
embarquée avec GitHub Desktop :

```powershell
$git = 'C:\Users\Claudine PERROT\AppData\Local\GitHubDesktop\app-3.6.3\resources\app\git\cmd\git.exe'
```

Si GitHub Desktop est mis à jour, rechercher `git.exe` dans
`C:\Users\Claudine PERROT\AppData\Local\GitHubDesktop\app-*\resources\app\git\cmd\` et
mettre ce chemin à jour.

## Procédure rapide

1. Vérifier ce qui sera publié :

   ```powershell
   & $git status --short
   & $git diff --check
   ```

2. Synchroniser les références distantes avant tout envoi :

   ```powershell
   & $git fetch origin master
   ```

   Ne pas pousser si l'historique distant a divergé sans avoir examiné la
   situation.

3. Vérifier que les nouvelles pages, images et liens ajoutés existent. Les
   anciens liens cassés éventuellement présents ailleurs dans le site ne doivent
   pas être corrigés ou inclus par défaut dans une publication de contenu.

4. Enregistrer uniquement les changements voulus, puis les envoyer :

   ```powershell
   & $git add --all
   & $git commit -m 'Description courte des modifications'
   & $git push origin master
   ```

5. Vérifier ensuite l'état local et la version publique :

   ```powershell
   & $git status --short
   curl.exe -L --max-time 20 -s https://madebyclo.fr/actualites
   ```

   L'URL avec `.html` redirige vers la route sans extension (par exemple
   `/actualites`). La mise à jour du site public peut prendre quelques minutes
   après le `push` ; confirmer la présence d'un titre ou texte nouvellement
   ajouté dans la réponse.

## Précautions

- Ne jamais publier de modifications apparues après la vérification initiale
  sans confirmer qu'elles font bien partie de la demande.
- Ne pas utiliser de commande destructive (`reset --hard`, etc.).
- Ne jamais enregistrer de jeton ou de mot de passe Git dans ce fichier ou dans
  l'URL du dépôt.
