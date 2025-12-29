![chipy8](https://raw.githubusercontent.com/animaldev/chipy8/5adebdb/docs/banner.png)
[![CI](https://travis-ci.org/animaldev/chipy8.svg)](https://travis-ci.org/animaldev/chipy8)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

# 🔗 chipy8

Ein Python-Script mit Flask Web-Interface zur Verwaltung von Netzwerk-Verbindungen. Das Tool analysiert aktive Peer-Sessions und eingehende Verbindungsanfragen und kann automatisch verwaiste Verbindungen entfernen.

## ✨ Features

- 🌐 **Analyse von Netzwerk-Verbindungen**: Vergleicht aktive mit konfigurierten Peers
- 🔍 **Einseitige Verbindungen erkennen**: Zeigt Peers, die keine Gegenverbindung haben
- 🧹 **Automatisches Cleanup**: Entfernt einseitige Verbindungseinträge automatisch
- 🛡️ **Dry-Run Modus**: Simulation ohne tatsächliche Änderungen
- 🌐 **Web-Interface**: Benutzerfreundliche Web-Oberfläche
- 💻 **CLI-Interface**: Kommandozeilen-Tool für Automatisierung
- ⚡ **Rate Limiting**: Respektiert API-Limits
- 📋 **Detaillierte Reports**: Umfassende Analyse-Berichte

## 🚀 Installation

1. **Repository klonen**:
   ```bash
   git clone https://github.com/animaldev/chipy8.git
   cd chipy8
   ```

2. **Python Virtual Environment erstellen**:
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # macOS/Linux
   ```

3. **Dependencies installieren**:
   ```bash
   pip install flask requests python-dotenv click
   ```

4. **API Token erstellen**:
   - Gehen Sie zu [Einstellungen > Persönliche Zugriffstoken](https://github.com/settings/tokens)
   - Erstellen Sie einen neuen Token mit folgenden Scopes:
     - `conn:manage` (zum Verwalten von Verbindungen)
     - `node:read` (zum Lesen von Peer-Daten)

5. **Umgebungsvariablen konfigurieren**:
   ```bash
   cp .env.example .env
   # Bearbeiten Sie .env und fügen Sie Ihren Token hinzu
   ```

## 📖 Verwendung

### Web-Interface

Starten Sie das Web-Interface:

```bash
python chipy8.py --web
```

Öffnen Sie http://localhost:5000 in Ihrem Browser.

**Web-Interface Features**:
- 📊 Interaktives Analyse-Dashboard
- 👥 Detaillierte Peer-Profile für einseitige Verbindungen
- 🧹 Dry-Run und Cleanup-Funktionen
- 📈 Statistiken und Visualisierungen

### Command Line Interface

**Einfache Analyse**:
```bash
python chipy8.py
```

**Dry-Run (Simulation)**:
```bash
python chipy8.py --dry-run
```

**Cleanup durchführen**:
```bash
python chipy8.py  # ohne --dry-run Flag
```

**Andere Optionen**:
```bash
python chipy8.py --username andererbenutzername
python chipy8.py --token YOUR_TOKEN_HERE
python chipy8.py --web --port 8080
```

## 🛠️ Konfiguration

### Umgebungsvariablen (.env)

```env
NETZ_TOKEN=your_network_token_here
NETZ_ID=your_network_id
NETZ_ENV=development
NETZ_DEBUG=true
```

### Token Berechtigungen

Ihr Token benötigt folgende Scopes:
- `conn:manage` - Zum Verwalten von Netzwerk-Verbindungen
- `node:read` - Zum Lesen von Peer-Profilen und Listen

## 📊 Ausgabe-Beispiel

```
🔗 chipy8 für relay-node
==================================================
📥 Lade aktive Peers von relay-node...
✅ 150 Peers gefunden
📤 Lade konfigurierte Verbindungen von relay-node...
✅ 180 Verbindungen gefunden

📈 ZUSAMMENFASSUNG
==============================
👥 Aktive Peers: 150
📤 Konfiguriert: 180
🤝 Gegenseitig: 145
➡️  Einseitig: 35

🔍 EINSEITIGE VERBINDUNGEN (35)
========================================
relay-node ist mit diesen Peers verbunden, aber sie verbinden nicht zurück:
  • node-1 (Server-Node) - 1200 Verbindungen
  • node-2 (Gateway) - 850 Verbindungen
  • node-3 - 300 Verbindungen

🔍 DRY RUN MODUS
====================
Würde 35 Verbindungen entfernen:
  • Würde node-1 trennen
  • Würde node-2 trennen
  • Würde node-3 trennen
```

## ⚠️ Wichtige Hinweise

- **Rate Limits**: Das Script respektiert API Rate Limits (5000 Requests/Stunde)
- **Backup**: Führen Sie zuerst immer einen Dry-Run durch
- **Token Sicherheit**: Teilen Sie niemals Ihren API-Token
- **Vorsicht**: Einseitige Verbindungen können strategisch wichtig sein

## 🤝 Beitragen

1. Fork des Repositories
2. Feature Branch erstellen (`git checkout -b feature/NeuesFunktion`)
3. Änderungen committen (`git commit -m 'Add some NeuesFunktion'`)
4. Branch pushen (`git push origin feature/NeuesFunktion`)
5. Pull Request erstellen

## 📝 Lizenz

Dieses Projekt steht unter der MIT-Lizenz. Siehe `LICENSE` Datei für Details.

## 🆘 Support

Bei Problemen oder Fragen:
1. Prüfen Sie die API-Dokumentation
2. Stellen Sie sicher, dass Ihr Token gültig ist
3. Prüfen Sie Ihre Netzwerkverbindung
4. Erstellen Sie ein Issue in diesem Repository

## 🧪 Tests

Das Projekt verfügt über umfassende Tests mit pytest.

### Tests ausführen

```bash
pytest
pytest --cov=chipy8 --cov-report=html
pytest tests/test_chipy8.py::TestNetworkManager
pytest tests/test_chipy8.py::TestFlaskApp
pytest -v
pytest -x
```

### Test-Dependencies

```bash
pip install pytest pytest-cov pytest-mock
```

### Coverage-Ziele

- ✅ Gesamt-Coverage: > 90%
- ✅ NetworkManager: > 95%
- ✅ ConnectionAnalyzer: > 95%
- ✅ Flask API: 100%

Siehe [TESTING.md](TESTING.md) für detaillierte Test-Dokumentation.

## 🔧 Entwicklung

```bash
python chipy8.py --web
pytest
pytest --cov=chipy8 --cov-report=html
flake8 chipy8.py
pytest --cov=chipy8 --cov-report=term-missing -v
```

## 📈 Zukünftige Features

- 📱 Mobile-responsive Web-Interface
- 📊 Erweiterte Statistiken und Visualisierungen
- 🔄 Automatische Synchronisation
- 📧 E-Mail-Berichte
- 🔍 Erweiterte Filter-Optionen
- 💾 Datenbank-Integration für historische Daten

## 🤝 Contributing

Beiträge sind willkommen! Bitte lesen Sie unsere [TESTING.md](./TESTING.md).

1. Fork das Repository
2. Erstellen Sie einen Feature-Branch
3. Committen Sie Ihre Änderungen
4. Pushen Sie zum Branch
5. Öffnen Sie einen Pull Request

## 📄 Lizenz

MIT-Lizenz - siehe [LICENSE](LICENSE).

## 👨‍💻 Autor

**animaldev** ([@animaldev](https://github.com/animaldev))

- GitHub: [@animaldev](https://github.com/animaldev)
- Repository: [chipy8](https://github.com/animaldev/chipy8)

## 🙏 Danksagungen

- Danke an die API für die umfassenden Endpunkte
- Inspiriert von der Notwendigkeit, Netzwerk-Verbindungen effizient zu verwalten
- Community-Feedback für kontinuierliche Verbesserungen

---

**Viel Spaß beim Verwalten Ihrer Netzwerk-Verbindungen! 🚀**
