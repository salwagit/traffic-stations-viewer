# Traffic Stations Viewer - PeMSD7

**Application web pour importer, visualiser et naviguer vers les stations de trafic du dataset PeMSD7.**
**Web app to import, visualize, and navigate to traffic stations from the PeMSD7 dataset.**

## ✨ Fonctionnalités / Features

- 📥 **Import CSV** – Chargez `PeMSD7_M_Station_Info.csv` dans MongoDB
- 📊 **Dashboard** – Nombre de stations, colonnes, aperçu des premières lignes
- 🗺️ **Carte interactive** – Leaflet + OpenStreetMap, marqueurs avec liens Waze
- 🚗 **Intégration Waze** – Liens directs de navigation vers chaque station
- 📡 **REST API** – `/api/stations` pour les données JSON
- 🐳 **Dockerisé** – `docker-compose up` pour démarrer

## 🎨 Thème / Theme
Nouveau thème vert pastel, blanc et beige pour une interface apaisante.

## 🚀 Usage / Quick Start

```bash
# Placez le dataset
cp your/pemsd7.csv dataset/PeMSD7_M_Station_Info.csv

# Démarrer (MongoDB + app)
docker-compose up --build

# Accéder
http://localhost:3000
```

1. **Home** : Dashboard avec KPIs et preview table
2. **Import** : Cliquez pour importer CSV → ~17000 stations
3. **Carte** : Visualisez toutes les stations californiennes (PeMSD7), cliquez pour Waze

## 🛠️ Guide Technique / Technical Guide

### Architecture
```
MongoDB ← CSV (csv-parser) ← Express app
Leaflet map ← /api/stations (JSON)
Static HTML/CSS/JS templates
```

### Endpoints
| Route | Description | 
|-------|-------------|
| `/` | Dashboard |
| `/import` | Import CSV → MongoDB |
| `/map` | Carte interactive |
| `/api/stations` | Toutes les stations JSON |

### Code Breakdown
- **app.js** : Express server, MongoDB client, template render
- **style.css** : Thème vert pastel/beige/blanc, animations
- **html/** : Templates minimaux (Mustache-like `{{var}}`)
- **Docker** : Node 18 + Mongo 6

### Dépendances / Dependencies
```json
{
  "express": "^4.18.2",
  "mongodb": "^5.0.0", 
  "csv-parser": "^3.0.0"
}
```

### Build & Deploy
```dockerfile
# Dockerfile (Node)
FROM node:18
COPY . /app
npm install
EXPOSE 3000
CMD ["node", "app.js"]
```

### Structure du Projet
```
.
├── backend/                 # App Node.js
│   ├── app.js              # Serveur Express
│   ├── package.json        # Dépendances
│   ├── html/               # Templates HTML
│   │   ├── layout.html     # Layout commun
│   │   ├── home.html       # Dashboard
│   │   ├── import.html     # Import CSV
│   │   └── map.html        # Carte Leaflet
│   └── style.css           # Thème vert pastel
├── dataset/                # PeMSD7_M_Station_Info.csv
├── docker-compose.yml      # Web + MongoDB
└── README.md               # Ce fichier
```

## 🔧 Dépannage / Troubleshooting

| Problème | Solution |
|----------|----------|
| Pas de données | Vérifiez `dataset/PeMSD7_M_Station_Info.csv` |
| Mongo erreur | `docker-compose down -v && docker-compose up` |
| Carte vide | Importez d'abord |
| Port 3000 occupé | Changez `ports: "3001:3000"` |

## 📈 Dataset PeMSD7
- **~17k stations** de trafic en Californie
- Colonnes: ID, Fwy, Dir, District, Latitude, Longitude...
- Source: Caltrans PeMS

**Auteur / Author**: BLACKBOXAI  
**Licence**: MIT
