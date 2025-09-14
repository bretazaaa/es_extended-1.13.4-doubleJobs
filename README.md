# 🚀 ES Extended – Version 1.13.4 (Double Jobs)

> **Modification personnalisée de es_extended** permettant la gestion de **deux métiers simultanés** :  
> un **job principal** et un **job secondaire** (`job` + `job2`).

---

## 📥 Installation

### Core ESX

Téléchargez le core complet ici :  
👉 [GitHub ESX Core](https://github.com/esx-framework/esx_core)

### Installation d’un serveur FiveM

Suivez la documentation officielle :  
👉 [Docs FiveM](https://docs.fivem.net/docs/server-manual/setting-up-a-server/)

---

## 🔧 Modifications incluses

- Passage en **double jobs** (`job` + `job2`) dans la base de données et le framework.
- Nouvelles **commandes administrateur** pour définir ou consulter le second métier.
- Support complet côté client/serveur pour gérer deux métiers séparés.

---

## 🕹️ Utilisation

### Commandes Admin

- **Changer le job principal** :
  ```bash
  /setjob [playerId] [job] [grade]
  ```
- **Changer le job secondaire** :
  ```bash
  /setjob2 [playerId] [job] [grade]
  ```
- **Informations sur le job principal** :
  ```bash
  /job
  ```
- **Informations sur le job secondaire** :
  ```bash
  /job2
  ```

---

## 🗄️ Mise à jour de la base de données

Si vous avez déjà un serveur en place, exécutez ces requêtes SQL :

```sql
ALTER TABLE users ADD COLUMN job2 VARCHAR(50) DEFAULT 'unemployed';
ALTER TABLE users ADD COLUMN job2_grade INT DEFAULT 0;
```

⚠️ Vous n’avez besoin que des tables jobs et job_grades (pas de jobs2 ni job2_grades).
Les deux jobs utiliseront la même structure de référence.

---

## 📌 Bonnes pratiques & Astuces

- Vérifiez que chaque job secondaire que vous souhaitez utiliser existe bien dans la table jobs et possède ses job_grades.
- Le système est rétrocompatible avec vos scripts ESX existants :

```bash
xPlayer.job → job principal
```

```bash
xPlayer.job2 → job secondaire
```

- Vous pouvez conditionner certains scripts pour vérifier si le joueur a l’un ou l’autre job.
- Exemple côté serveur :

```lua
if xPlayer.job.name == "police" or xPlayer.job2.name == "police" then
    -- Le joueur est policier (même si c'est en secondaire)
end
```

---

## ⚙️ Compatibilité

- Compatible avec ESX Legacy (≥ 1.9) et ESX 1.13.4.
- Compatible avec `esx_society`, `esx_billing`, `esx_policejob`, etc.
- Peut nécessiter une adaptation légère des scripts vérifiant uniquement `xPlayer.job`.

---

## 🐛 Support

Si vous rencontrez un problème :

- Ouvrez une issue sur ce dépôt.
- Discord (en préparation) : lien bientôt disponible

Readme formuler et mise en forme par IA
