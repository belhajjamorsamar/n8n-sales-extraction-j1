# 🚀 Automatisation n8n : Extraction des Ventes J-1

Ce projet contient un workflow d'automatisation **n8n** conçu pour extraire, transformer et partager automatiquement les données des ventes de la veille (J-1). Il élimine les tâches manuelles de reporting en générant un fichier Excel quotidien transmis par e-mail via Google Drive.

---

## ⚙️ Fonctionnement du Workflow

Le processus s'exécute automatiquement chaque matin et suit ces étapes :

1. **Déclencheur (Schedule Trigger)** : S'active tous les jours à 7h00 du matin.
2. **Génération de la date (Code JavaScript)** : Calcule dynamiquement la date de la veille (J-1).
3. **Extraction SQL (HTTP Request)** : Interroge la base de données interne (`ventes_flat`) pour récupérer les ventes agrégées de la journée ciblée (`FORMAT CSVWithNames`).
4. **Nettoyage des données (Code JavaScript)** : Traite le flux brut, gère le formatage des caractères spéciaux et convertit les quantités en valeurs numériques.
5. **Conversion (Convert to File)** : Transforme les données nettoyées en un fichier tableur `.xlsx` (`Ventes_AAAA-MM-JJ.xlsx`).
6. **Stockage Cloud (Google Drive)** : 
   * Télécharge automatiquement le fichier sur Google Drive.
   * Modifie les permissions du fichier pour le rendre accessible en lecture publique via un lien.
7. **Notification (Send an Email)** : Envoie un e-mail avec un bouton de téléchargement direct vers le fichier Excel stocké sur le Drive.

---

## 🛠️ Prérequis et Technologies

* **n8n** (Version récente avec support du mode binaire séparé)
* Base de données compatible avec les requêtes SQL (ex: ClickHouse ou similaire configurée en local/interne via `host.docker.internal`)
* Comptes et identifiants configurés dans n8n :
  * Credentials HTTP Basic Auth (pour la base de données)
  * Credentials Google Drive OAuth2 API
  * Compte SMTP (pour l'envoi des e-mails)

---

## 📂 Structure du Projet

```text
├── automation extraction data j-1.json   # Export du workflow n8n
└── README.md                             # Documentation du projet
