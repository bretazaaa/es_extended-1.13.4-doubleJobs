# 🚀 ES Extended – Version 1.13.4 (Double Jobs, Orga & Gang)

**Modification avancée de es_extended** permettant la gestion de :

- **Deux métiers simultanés** : job principal (`job`) et job secondaire (`job2`)
- **Organisation** (`orga`)
- **Gang** (`gang`)

---

## 📥 Installation

### Core ESX

Téléchargez le core complet ici :  
👉 [GitHub ESX Core](https://github.com/esx-framework/esx_core)

### Installation d’un serveur FiveM

Suivez la documentation officielle :  
👉 [Docs FiveM](https://docs.fivem.net/docs/server-manual/setting-up-a-server/)

---

## 🔧 Fonctionnalités et modifications

- Gestion complète de **deux jobs** (principal et secondaire) dans la base de données et le framework.
- Ajout de la gestion **organisation** et **gang** (stockés dans la base et accessibles côté framework).
- Nouvelles **commandes administrateur** pour définir ou consulter le job secondaire, l’organisation ou le gang.
- Support complet côté client/serveur pour tous ces rôles.
- Système rétrocompatible avec les scripts ESX existants.

---

## 🕹️ Commandes administrateur

- **Définir le job principal** :
  ```
  /setjob [playerId] [job] [grade]
  ```
- **Définir le job secondaire** :
  ```
  /setjob2 [playerId] [job] [grade]
  ```
- **Définir l’organisation** :
  ```
  /setorga [playerId] [orga] [grade]
  ```
- **Définir le gang** :
  ```
  /setgang [playerId] [gang] [grade]
  ```

---

## 🗄️ Mise à jour de la base de données

Si vous migrez depuis une version antérieure, exécutez :

```sql
ALTER TABLE users ADD COLUMN job2 VARCHAR(50) DEFAULT 'unemployed';
ALTER TABLE users ADD COLUMN job2_grade INT DEFAULT 0;
ALTER TABLE users ADD COLUMN orga VARCHAR(50) DEFAULT 'unemployed';
ALTER TABLE users ADD COLUMN orga_grade INT DEFAULT 0;
ALTER TABLE users ADD COLUMN gang VARCHAR(50) DEFAULT 'unemployed';
ALTER TABLE users ADD COLUMN gang_grade INT DEFAULT 0;
```

⚠️ Seules ces colonnes sont nécessaires dans la table `users`.
Les jobs utilisent la même structure de référence ; organisation et gang disposent de leurs propres tables pour plus de clarté (voir `es_extended.sql`).

---

## 📌 Bonnes pratiques & astuces

- Vérifiez que chaque job secondaire, organisation ou gang existe bien dans les tables correspondantes et possède ses grades.
- Le système reste compatible avec vos scripts ESX :
  - `xPlayer.job` → job principal
  - `xPlayer.job2` → job secondaire
  - `xPlayer.orga` → organisation
  - `xPlayer.gang` → gang
- Vous pouvez conditionner vos scripts sur n’importe lequel de ces rôles, par exemple :

  ```lua
  if xPlayer.job.name == "police" or xPlayer.job2.name == "police" or xPlayer.gang.name == "ballas" or xPlayer.orga.name == "lostmc" then
      -- Le joueur est policier, dans le gang ballas ou l’orga lostmc
  end
  ```

---

## ⚙️ Compatibilité

- Compatible avec ESX Legacy (≥ 1.9) et ESX 1.13.4.
- Fonctionne avec `esx_society`, `esx_billing`, `esx_policejob`, etc.
- Une légère adaptation peut être nécessaire pour les scripts qui ne vérifient que `xPlayer.job`, `xPlayer.orga` ou `xPlayer.gang`.

---

## 🐛 Support

En cas de problème :

- Ouvrez une issue sur ce dépôt.
- Discord (en préparation) : lien à venir.
