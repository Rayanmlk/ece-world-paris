# ECE World — Jeu de Plateau Multijoueur en C

> Projet d'informatique ING1 — ECE Paris | Groupe 11, Équipe 2 | 2022–2023
> Cours : Algorithmique Avancée & Bibliothèque Graphique

---

## Description

**ECE World** est un jeu de plateau 2D multijoueur (2 joueurs, tour par tour) développé en **C** avec la bibliothèque graphique **Allegro 4**. Le thème est inspiré de la carte de **Pokémon : Diamant et Perle**, dont les bâtiments servent d'entrées vers 7 mini-jeux distincts.

Les joueurs se déplacent sur la carte, accèdent aux jeux en appuyant sur Entrée devant les entrées, et s'affrontent dans des mini-jeux pour gagner ou perdre des tickets. Le joueur qui tombe à 0 ticket perd la partie.

---

## Mini-Jeux

| Jeu | Description | Développeur |
|-----|-------------|-------------|
| **Guitar Hero** | Jeu de rythme avec défilement du fond et détection des touches | Elias |
| **Paris Équestres** | Parier sur un cheval dans une course aléatoire | Nicolas |
| **Jeu de la Taupe** | Frapper les taupes avec un marteau, timer 25s, vitesse croissante | Rayan |
| **Tir aux Ballons** | Viser et tirer sur des ballons se déplaçant aléatoirement | Alex |
| **Pong** | Ping-pong solo, la balle accélère à chaque rebond | Alex |
| **Traversée de la Rivière** | Sauter de rondin en rondin pour traverser la rivière | Elias |
| **Pêche aux Canards** | Cliquer sur des canards se déplaçant à vitesses aléatoires | Rayan |

---

## Architecture

Le projet est structuré autour d'un **main.c** minimaliste et d'un fichier **fonctions.c** contenant l'intégralité des sous-programmes, avec leurs prototypes dans **fonctions.h**.

```
main.c          → Initialisation, boucle principale, appel des mini-jeux
fonctions.c     → Implémentation de tous les sous-programmes
fonctions.h     → Prototypes et définitions des structures
```

### Boucle principale

```c
int main() {
    initialiser_joueurs();
    while (!fin && tickets > 0) {
        deplacement_personnage();
        guitar_hero();
        paris_equestre();
        jeu_taupe();
        tir_ballon();
        pong();
        traversee_riviere();
        peche_canard();
    }
    ecran_victoire();
}
```

### Structures de données clés

```c
typedef struct {
    BITMAP* haut[3]; BITMAP* bas[3];
    BITMAP* gauche[3]; BITMAP* droite[3];
    int x, y, direction, instant, deplacement;
    char nom[20];
    int nb_tickets, bet;
} personnage;

typedef struct { int x, y; } t_taupe;

typedef struct {
    int x, y, vitesse, vivant;
    BITMAP* sprite;
} t_canard;
```

### Fonctionnalités notables de la carte
- Sprite sheet unique pour tous les personnages (optimisation mémoire)
- Sprint avec touche `E`
- Collisions sur les bordures blanches
- Système tour par tour
- Sauvegarde des scores dans un fichier texte, accessible in-game

---

## Stack Technique

| Outil | Version |
|-------|---------|
| Langage | C99 |
| Bibliothèque graphique | Allegro 4.4 |
| Build system | CMake 3.10+ |
| Compilateur | MinGW (GCC Windows) |
| Contrôle de version | Git / GitHub |

---

## Compilation et Lancement

### Prérequis

- [MinGW-w64](https://www.mingw-w64.org/) avec GCC
- [Allegro 4.4](https://liballeg.org/) (`liballeg44`)
- [CMake 3.10+](https://cmake.org/)

### Build

```bash
mkdir build && cd build
cmake .. -G "MinGW Makefiles"
make
./PROJET.exe
```

> **Note :** Les fichiers assets (`.bmp`, `.wav`) se trouvent dans le dossier `assets/`. Ils doivent être copiés dans le même dossier que l'exécutable (`cmake-build-debug/`) pour lancer le jeu.
>
> **Assets manquants :** `viseur.bmp` et les BMPs de ballons (`rouge.bmp`, `noir.bmp`, `rose.bmp`, `blanc.bmp`, `violet.bmp`) utilisés par le mini-jeu Tir aux Ballons n'ont pas été retrouvés.

---

## Équipe

| Membre | Jeux réalisés |
|--------|---------------|
| **Elias Elabd** | Carte & collisions, Guitar Hero, Traversée de la rivière |
| **Nicolas Chaudemanche** | Paris Équestres |
| **Alex Huang** | Tir aux Ballons, Pong |
| **Rayan Malki** | Jeu de la Taupe, Pêche aux Canards |

---

## Résultats

- ~160 commits sur GitHub tout au long du projet
- 7 mini-jeux fonctionnels
- Système de sauvegarde des highscores
- Projet 100% fonctionnel rendu en fin de semestre
