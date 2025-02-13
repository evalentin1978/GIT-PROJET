# GIT-PROJET

#deFéfinir la fonction MAITRE qui parcoure la grille=CELLE QUI VA VERIFIER LE GAGNANT.

import time #import le module temps

def testValeur(grille, ligne, colonne, valeur):

    # Check row
    if valeur in grille[ligne]:
        return False

    # Check column
    if valeur in [grille[i][colonne] for i in range(9)]:
        return False

    # Check 3x3 subgrid
    subgrid_row = (ligne // 3) * 3
    subgrid_col = (colonne // 3) * 3
    for i in range(subgrid_row, subgrid_row + 3):
        for j in range(subgrid_col, subgrid_col + 3):
            if grille[i][j] == valeur:
                return False

    return True  # Value is valid


def parcoursGrille(grille):
    ligne = 0
    colonne = 0
    compteurCaseNon0 = 0
    compteurCaseNonChangee = 0
    listeValeursVides = []
    rechercher = True
    temsDepart = time.time()

    while rechercher:
        if grille[ligne][colonne]== 0:
            compteurCaseNon0 = 0
            #Essai les valeurs de 0 à 9
            for valeur in range(1,10):

                if testValeur(grille, ligne, colonne, valeur):
                   listeValeursVides.append(valeur)

            if len(listeValeursVides)==1:
                compteurCaseNonChangee = 0
                grille[ligne][colonne] = listeValeursVides[0] #Modification de grille
            listeValeursVides.clear()
        compteurCaseNonChangee+=1
        compteurCaseNon0+=1
        colonne+=1
        if colonne == 9:
            ligne+=1
            colonne = 0
        if ligne == 9:
            ligne=0
        #Conditions d'arrêt de la recherche=TROUVER LA SOLUTION AU JEU.
        if compteurCaseNon0>81:
            rechercher = False
            print("voici la solution")
        if compteurCaseNonChangee>162:
            rechercher = False
            print("impossible pour moi,voici la grille...")
    tempsFin  = time.time()
    for ligne in grille:
        print(ligne)
    print("En {} seconde" .format(round(tempsFin-temsDepart,5)))

# Define the Soduku puzzle as a 3D list
Soduku = [
    [5, 3, 0, 0, 7, 0, 0, 0, 0],
    [6, 0, 0, 1, 9, 5, 0, 0, 0],
    [0, 9, 8, 0, 0, 0, 0, 6, 0],
    [8, 0, 0, 0, 6, 0, 0, 0, 3],
    [4, 0, 0, 8, 0, 3, 0, 0, 1],
    [7, 0, 0, 0, 2, 0, 0, 0, 6],
    [0, 6, 0, 0, 0, 0, 2, 8, 0],
    [0, 0, 0, 4, 1, 9, 0, 0, 5],
    [0, 0, 0, 0, 8, 0, 0, 7, 9]
]
# Assuming `testValeur` function is defined elsewhere in your code.

parcoursGrille(Soduku)
