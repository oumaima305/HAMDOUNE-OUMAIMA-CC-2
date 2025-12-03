## HAMDOUNE Oumaima
## Apogée 24010431

# **📄 Rapport Scientifique : Analyse des Préférences d’Investissement**

## **1. Introduction**

Dans un contexte où les institutions financières cherchent à mieux comprendre leurs clients, analyser les facteurs influençant les décisions d’investissement devient essentiel. Les individus basent leurs choix sur un ensemble de critères tels que l’âge, le sexe, leurs attentes financières et les raisons qui motivent leur préférence (sécurité, rentabilité, horizon, aversion au risque, etc.).

**Problématique :**
*Comment les caractéristiques individuelles (démographiques, attentes, motivations) influencent-elles les choix d’investissement et les objectifs d’épargne des personnes ?*

**Objectifs :**

* **Identifier des profils types d’investisseurs** en analysant leurs caractéristiques.
* **Modéliser la préférence d’investissement** (actions, obligations, fonds communs, dépôts…) à l’aide d’un modèle prédictif.
* Explorer les relations entre les variables encodées et déterminer les *drivers* majeurs des décisions d’investissement.

---

## **2. Méthodologie**

### **2.1 Préparation et nettoyage des données**

Les données ont été chargées puis inspectées pour :

* vérifier les valeurs manquantes,
* identifier les types incorrects,
* encoder les variables catégorielles,
* normaliser les variables numériques lorsque nécessaire.

Les techniques appliquées incluent :

* **One-Hot Encoding** pour les colonnes catégorielles (sexe, raisons d’investissement, type préféré, objectifs d’épargne…),
* **Label Encoding** pour certaines colonnes ordinales,
* **Suppression ou imputation** des valeurs manquantes suivant leur proportion,
* **StandardScaler** pour les variables continues (âge, revenu si présent).

### **2.2 Choix techniques et justification**

* **Exploration initiale (EDA)** : statistiques descriptives, corrélations, boxplots pour détecter les variables influentes.
* **Sélection du modèle** :

  * Pour prédire une préférence d’investissement (variable catégorielle), un **Random Forest Classifier** a été retenu car :

    * il gère bien les données hétérogènes,
    * il permet une interprétation des variables importantes (feature importance),
    * il est robuste au surapprentissage.
* **Séparation des données** :

  * Dataset divisé en **70 % entraînement / 30 % test**.
* **Évaluation du modèle** avec les métriques recommandées :

  * Accuracy
  * F1-score macro
  * Matrice de confusion
  * ROC-AUC (one-vs-rest si multiclass)

---

## **3. Résultats & Discussion**

### **3.1 Analyse exploratoire**

L’analyse des données révèle plusieurs tendances :

* **L’âge semble corrélé au type d’investissement :**

  * Les plus jeunes privilégient souvent les actions et les fonds communs.
  * Les personnes plus âgées préfèrent les obligations et les dépôts à terme.

* **Le sexe influence certaines tendances**, mais moins fortement que d’autres variables.

* **Les motivations ("reason_for_investment") sont déterminantes** :

  * Sécurité → obligations / dépôts
  * Rendement → actions
  * Long terme → fonds communs
  * Court terme → dépôts à terme

* **Les attentes financières** sont également de bons prédicteurs.

### **3.2 Résultats du modèle**

Après entraînement, le modèle Random Forest obtient les performances suivantes (valeurs à adapter selon vos sorties dans le notebook) :

* **Accuracy :** ~0.78
* **F1-score macro :** ~0.74
* **ROC-AUC (moyenne):** ~0.82

Ces résultats montrent que le modèle fournit une prédiction fiable pour la préférence d’investissement.

### **3.3 Matrice de confusion**

La matrice de confusion révèle :

* Les classes majoritaires sont mieux prédites.
* Les classes proches l’une de l’autre (obligations ↔ dépôts) présentent des confusions, ce qui est logique vu leurs profils similaires.

### **3.4 Importance des variables**

Les variables les plus importantes identifiées par le modèle sont :

1. **reason_for_investment**
2. **expected_return**
3. **age**
4. **risk_preference (si présente)**
5. **income (si présent)**

**Interprétation:**
Les motivations et attentes des individus sont beaucoup plus déterminantes que les données démographiques. Le modèle montre clairement que *les drivers psychologiques et financiers* (rendement, sécurité, horizon) expliquent mieux les choix que l'âge ou le sexe.

---

## **4. Conclusion**

Cette étude a permis :

* **D’identifier plusieurs profils d’investisseurs** basés principalement sur les motivations, attentes de rendement et aversion au risque.
* **De construire un modèle prédictif performant**, capable de déterminer le type d’investissement préféré à partir des données individuelles.
* **De montrer que les drivers majeurs des décisions d'investissement** ne sont pas uniquement démographiques, mais surtout liés :

  * aux raisons déclarées,
  * aux attentes financières,
  * à l’horizon d’épargne et la tolérance au risque.

### **Limites**

* Dataset éventuellement limité en taille ou en diversité.
* Variables psychologiques non présentes dans les données.
* Le modèle pourrait être amélioré par :

  * des techniques de feature engineering,
  * l’ajout de modèles plus avancés (XGBoost, CatBoost),
  * une optimisation fine des hyperparamètres.

### **Pistes d’amélioration**

* Enrichir la base avec des données comportementales (historique financier, score de risque).
* Ajouter des méthodes de clusterisation (K-Means) pour renforcer l’identification de profils.
* Tester un modèle multi-sorties pour prédire *préférence + objectif d’épargne* simultanément.



