# 🖥️ Glance Dashboard - Homelab

[![English](https://img.shields.io/badge/🇬🇧_English-blue)](README.md)

Dashboard de monitoring pour homelab basé sur [Glance](https://github.com/glanceapp/glance).

![Glance](https://img.shields.io/badge/Glance-Dashboard-blue)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?logo=docker&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

## 🎯 Objectif

Ce dashboard est conçu pour être **la page d'accueil de votre navigateur** afin d'accéder rapidement à tous vos services homelab et avoir un coup d'œil rapide sur les informations pertinentes.

Déployé sur **Dockge** sur une VM Debian — léger et parfaitement optimisé.

## 📸 Captures d'écran

### Accueil
![Accueil](screenshots/accueil.png)

### Media
![Media](screenshots/media.png)

### Monitoring
![Monitoring](screenshots/monitoring.png)

## ✨ Fonctionnalités

- **Infrastructure** : Proxmox VE (3 nodes), PBS Backup, Synology NAS, UniFi
- **Media Stack** : Plex, Sonarr, Radarr, Prowlarr, Tautulli, Transmission
- **Monitoring** : Beszel, Uptime Kuma, Speedtest Tracker
- **Domotique** : Home Assistant, Zigbee2MQTT, Scrypted
- **Extras** : Météo, RSS Tech News (Macg, Numerama, Selfh.st, ServeTheHome), Calendrier F1, Spotify Now Playing

## 🚀 Installation

### Prérequis

- Docker & Docker Compose (ou Dockge)
- Les services que vous souhaitez monitorer

### Déploiement

1. **Récupérer les fichiers**
   
   Téléchargez les fichiers depuis ce dépôt ou clonez-le.

2. **Configurer les variables d'environnement**
   ```bash
   cp .env.example .env
   nano .env  # Remplir avec vos vraies valeurs
   ```

3. **Adapter les URLs** (optionnel)
   ```bash
   nano urls.env  # Modifier selon votre infrastructure
   ```

4. **Lancer le dashboard**
   ```bash
   docker-compose up -d
   ```

5. **Accéder au dashboard**
   ```
   http://localhost:8083
   ```

## 📁 Structure

```
glance-dashboard/
├── docker-compose.yml    # Configuration Docker
├── glance.yml            # Configuration Glance (à placer dans /docker/glance/config/)
├── urls.env              # URLs des services
├── .env.example          # Template des secrets
├── .env                  # Vos secrets (non versionné)
├── screenshots/          # Captures d'écran du dashboard
└── README.md
```

## ⚙️ Configuration

### Fichiers d'environnement

| Fichier | Description | Git |
|---------|-------------|-----|
| `.env` | Clés API, mots de passe, tokens | ❌ Ignoré |
| `.env.example` | Template à copier | ✅ Versionné |
| `urls.env` | URLs de vos services | ✅ Versionné |

### Variables requises

<details>
<summary>📋 Liste des variables</summary>

#### Infrastructure
| Variable | Description |
|----------|-------------|
| `PVE_API_TOKEN` | Token API Proxmox VE |
| `PBS_API_TOKEN` | Token API Proxmox Backup Server |
| `SYNOLOGY_USER` / `SYNOLOGY_PASSWORD` | Identifiants Synology |
| `UNIFI_API_KEY` | Clé API UniFi |

#### Media
| Variable | Description |
|----------|-------------|
| `TAUTULLI_API_KEY` | Clé API Tautulli |
| `SONARR_API_KEY` | Clé API Sonarr |
| `RADARR_API_KEY` | Clé API Radarr |
| `PROWLARR_API_KEY` | Clé API Prowlarr |
| `TMDB_API_KEY` | Clé API TMDB |
| `OVERSEERR_API` | Clé API Overseerr |
| `TRANSMISSION_USER` / `TRANSMISSION_PASSWORD` | Identifiants Transmission |

#### Monitoring
| Variable | Description |
|----------|-------------|
| `SPEEDTEST_API_KEY` | Token Speedtest Tracker |
| `BESZEL_API_KEY` | Token JWT Beszel |

</details>

### Obtenir les clés API

<details>
<summary>🔑 Guide rapide</summary>

| Service | Emplacement |
|---------|-------------|
| **Proxmox** | Datacenter → Permissions → API Tokens |
| **Sonarr/Radarr/Prowlarr** | Settings → General → API Key |
| **Tautulli** | Settings → Web Interface → API Key |
| **TMDB** | [themoviedb.org/settings/api](https://www.themoviedb.org/settings/api) |
| **Beszel** | Settings → API Keys |
| **Overseerr** | Settings → General → API Key |

</details>

## 🎨 Personnalisation

### Thème

Modifier dans `glance.yml` :
```yaml
theme:
  background-color: 50 1 6      # HSL
  primary-color: 157 47 65      # HSL
  contrast-multiplier: 1.1
```

### Pages

Le fichier `glance.yml` est organisé par pages :
- `Accueil` - Vue d'ensemble infrastructure, services, bookmarks
- `Media` - Stack Plex/Arr, stats Tautulli, tendances
- `Monitoring` - Stats serveurs Beszel, Uptime Kuma, stockage

## 🔒 Sécurité

- ⚠️ Ne jamais commit le fichier `.env`
- Les URLs internes (`10.x.x.x`) ne sont pas accessibles de l'extérieur
- Utiliser un reverse proxy (NPM, Traefik) pour l'exposition externe

## 📝 Notes

- Le widget Spotify nécessite un token OAuth stocké dans `/app/config/spotify_token.txt`
- Certains widgets utilisent `allow-insecure: true` pour les certificats auto-signés
- Cache configuré par widget (1m à 1h selon la fréquence de mise à jour)
- L'API F1 tourne dans un conteneur séparé pour les données du calendrier

## 🙏 Crédits

- [Glance](https://github.com/glanceapp/glance) - Le projet original
- [Beszel Community Widget](https://github.com/glanceapp/glance/discussions) - Widget Beszel
- [Glance F1 Widget](https://github.com/SkyAllinott/glance-F1) - Widget calendrier Formule 1
- [Claude by Anthropic](https://claude.ai) - Vibe codé avec assistance IA 🤖

## 📄 Licence

Licence MIT - Libre d'utilisation et de modification.

---

<p align="center">
  <i>Fait avec ❤️ pour la communauté homelab</i>
</p>
