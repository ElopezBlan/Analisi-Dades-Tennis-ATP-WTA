# Anàlisi de Dades: ATP vs WTA (2018-2023) 🎾

Aquest repositori conté el codi Python utilitzat per a la neteja, transformació i preparació de les dades per la PR2 del projecte de Visualització de Dades.

## 🛠️ Tecnologies
* **Python** (Pandas, NumPy)
* **Jupyter Notebook / Google Colab**

## 📊 Visualització Final
Pots veure el resultat final interactiu a Tableau Public aquí:
https://public.tableau.com/views/PR2_EduardLopez/Historia1?:language=es-ES&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link

El script de Python realitza les següents tasques:

### 1. Fusió i Etiquetatge
* Càrrega iterativa dels fitxers CSV per anys.
* Unificació dels dos circuits en un sol DataFrame.
* Creació de la variable `Circuit` ('ATP' o 'WTA') per permetre la comparativa directa.

### 2. Neteja de Dades
* Eliminació de registres amb valors nuls en columnes crítiques per a la visualització:
    * Alçada (`winner_ht`, `loser_ht`)
    * Durada (`minutes`)
    * Estadístiques de servei (`w_ace`, `l_ace`)

### 3. Enginyeria de Característiques (Feature Engineering)
Per respondre a les preguntes, s'han creat noves variables calculades:

* **⚡ Eficiència del Servei (`w_ace_eff`)**
    * *Càlcul:* `(Aces / Punts de Servei Jugats) * 100`
    * *Motiu:* El nombre total d'aces enganya si el partit és llarg. L'eficiència permet comparar realment la potència del servei independentment de la durada.

* **🥵 Resistència / Partit Decisiu (`is_decider`)**
    * *Lògica:* Detecta si el marcador conté 3 sets (o 5 en Grand Slams masculins) comptant els guions.
    * *Motiu:* Mesurar la igualtat competitiva ("Quins partits van al límit?").

* **⏱️ Normalització Temporal (`min_per_set`)**
    * *Càlcul:* `Minuts Totals / Sets Jugats`
    * *Motiu:* **Crític.** No es pot comparar la durada total de l'ATP vs WTA directament, ja que en Grand Slams els homes juguen al millor de 5 sets i les dones al millor de 3. Aquesta variable elimina aquest biaix.
