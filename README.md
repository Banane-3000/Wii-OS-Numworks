# Wii-OS pour NumWorks

Wii-OS remplace l'écran d'accueil de la NumWorks (**n0110**, **n0115** ou **n0120**) par un menu
façon **Wii** : une grille de « chaînes » (toutes les applis de la calculatrice
+ tes jeux `.nwa`), un pointeur en forme de main, une horloge, un bouton Wii et
un bouton message.

Projet de fan, sans lien avec Nintendo ni NumWorks. Aucun asset Nintendo : tout
est dessiné par le code. Il est basé sur le moteur de dessin et l'installateur de
**Windows-OS** (derim00), sous licence **CC BY-NC-SA 4.0** : garde le fichier
`LICENSE`, ne vends rien, et ne publie pas le firmware compilé (il contient du
code NumWorks sous licence non commerciale).

Il s'installe dans le **slot B** : ton système officiel (slot A) n'est pas touché.
Reset au dos de la calculatrice = retour au système officiel.

## Utilisation

| Touche | Action |
|---|---|
| Flèches | Déplacer la main (elle accélère si tu restes appuyé) |
| OK / EXE | Cliquer |
| Toolbox | Clic droit (sur l'horloge : recule l'heure) |
| Back / Home | Ferme la fenêtre « Start » ou revient à la page 1 |

- Clique sur une chaîne : fenêtre **Start this channel?** puis *Start* ou *Wii Menu*.
- Flèches bleues sur les côtés : page précédente / suivante (12 chaînes par page).
- **Bouton Wii** (en bas à gauche) : ouvre Réglages.
- **Bouton enveloppe** (en bas à droite) : met la calculatrice en veille.
- **Horloge** : clique sur les heures (+1 h) ou les minutes (+1 min). Pas d'horloge
  interne : l'heure repart de 00:00 à chaque démarrage. Toolbox = recule.

## Installer

1. Crée un dépôt GitHub **privé** avec le contenu de ce dossier.
2. Mets tes jeux `.nwa` dans `games/` (facultatif, voir `games/LISEZMOI.md`).
3. Onglet **Actions** → *Build Wii-OS* → *Run workflow* → modèle **n0110**, **n0115** ou **n0120** (la n0115 se compile comme une n0110).
4. Télécharge l'installateur (Windows ou Mac), branche la calculatrice, appuie sur
   **Reset** au dos, clique sur *Installer*.

## Notes

- Les chaînes sont les applis intégrées dans l'ordre d'Epsilon, puis les jeux.
- Le code du menu est dans `patches/wii-os-epsilon.patch`
  (`epsilon/apps/home/win/shell.cpp`). Le dossier garde le nom `win/` pour
  réutiliser le moteur de dessin de Windows-OS.
- Non testé sur une vraie n0110 : si la compilation ou l'installation échoue,
  donne le message d'erreur.

## Menu v2 (réplique plus fidèle)

- Fond blanc à fines rayures, tuiles 66×45 aux coins arrondis (bordure d'un pixel, fines lignes), tuiles vides grises avec « Wii ».
- Barre du bas avec le creux sous l'horloge et le liseré bleu d'un pixel (réglable : `k_dip` dans `shell.cpp`, négatif = bosse).
- Horloge à 7 segments en 12 h (AM/PM) et date « Fri 11/20 ». Sans horloge interne, elle part de l'heure de compilation (UTC+1, `k_utcOffsetMinutes`), puis se règle en cliquant sur les heures / minutes (Toolbox = reculer).
- Main blanche à contour noir avec le badge bleu « 1 », dessinée pixel par pixel (24×30, antialiasing) ; la pointe de l'index est le point de clic.
- Boutons : **Wii** = Réglages, **carte SD** = saute à la première page de jeux .nwa, **enveloppe** = veille.
