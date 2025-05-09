# Projet - Recherche d’Images par le Contenu (CBIR)

Projet réalisé dans le cadre du TP de M2 - Indexation de contenu multimédia.  
Université de La Rochelle / IFI - Université nationale du Vietnam  
Encadré par Nicolas Sidère – 2025

##  Objectif

Développer un système simple de **recherche d’images par le contenu** basé sur :
- Les **caractéristiques de couleur** (histogrammes)
- Les **caractéristiques de forme** (moments de Hu)

Le système compare une image requête à une base d’images (COIL-100) et retourne les N images les plus similaires.

##  Technologies

- Python 3
- OpenCV
- NumPy
- Matplotlib

##  Données utilisées

- **Base COIL-100** (Columbia University Image Library)  
  100 objets x 20 vues par objet  
  → [Télécharger ici](http://www.cs.columbia.edu/CAVE/software/softlib/coil-100.php)

##  Pipeline du système

1. **Lecture de l’image requête**
2. **Calcul des descripteurs** :
   - Histogrammes RVB réduits (3 x 32)
   - Moments de Hu sur image en niveaux de gris
3. **Pour chaque image de la base** :
   - Chargement
   - Extraction des mêmes descripteurs
   - Calcul des distances (couleur + forme)
4. **Fonction globale de similarité** :
   ```math
   distance = w1 * dist_couleur + w2 * dist_forme
   ```
   - Par défaut : `w1 = w2 = 0.5`
5. **Tri des résultats** et affichage des N images les plus proches

##  Caractéristiques utilisées

-  **Histogrammes de couleur** (intersection, Chi-2)
-  **Moments de Hu** (descripteur de forme, distance euclidienne)
-  **Combinaison pondérée des distances**

##  Exemple d’utilisation

```bash
> python cbir.py img035.tif
```

Exemple de sortie (top 5) :

```
Image       Distance
img078.tif     0.001
img032.tif     0.005
img005.tif     0.010
img098.tif     0.012
img062.tif     0.016
```

##  Références utiles

- [Histogram Calculation - OpenCV](https://docs.opencv.org/master/d8/dbc/tutorial_histogram_calculation.html)
- [Histogram Comparison - OpenCV](https://docs.opencv.org/master/d8/dc8/tutorial_histogram_comparison.html)
- [Hu Moments - OpenCV](https://docs.opencv.org/master/d3/dc0/group__imgproc__shape.html)
- [COIL-100 Dataset](http://www.cs.columbia.edu/CAVE/software/softlib/coil-100.php)