# Build Instructions für FindMySync

## Voraussetzungen

- macOS 10.15 (Catalina) oder neuer (getestet bis macOS 26 Tahoe)
- Xcode 11.0 oder neuer
- CocoaPods
- Git

## Build-Schritte

### 1. Repository klonen

```bash
git clone https://github.com/MartinPham/FindMySync.git
cd FindMySync
```

### 2. Dependencies installieren

```bash
# CocoaPods installieren (falls nicht vorhanden)
sudo gem install cocoapods

# Dependencies installieren
pod install
```

### 3. Projekt öffnen

```bash
# Öffne den Workspace (NICHT das .xcodeproj!)
open FindMySync.xcworkspace
```

### 4. In Xcode kompilieren

1. Wähle das Target "FindMySync" aus
2. Wähle "My Mac" als Zielgerät
3. Drücke `Cmd + B` zum Kompilieren
4. Drücke `Cmd + R` zum Kompilieren und Starten

### Alternative: Command Line Build

```bash
# Mit fastlane (empfohlen)
bundle install
bundle exec fastlane mac release

# Oder direkt mit xcodebuild
xcodebuild -workspace FindMySync.xcworkspace \
           -scheme FindMySync \
           -configuration Release \
           -derivedDataPath build \
           clean build

# Die kompilierte App findest du dann unter:
# build/Build/Products/Release/FindMySync.app
```

## Troubleshooting

### "Command not found: pod"

```bash
sudo gem install cocoapods
```

### "Command not found: bundle"

```bash
sudo gem install bundler
bundle install
```

### Signing-Fehler

1. Öffne das Projekt in Xcode
2. Gehe zu "Signing & Capabilities"
3. Wähle dein Team/Developer Account
4. Aktiviere "Automatically manage signing"

### Dependencies-Fehler

```bash
# Pod-Cache löschen und neu installieren
pod cache clean --all
pod deintegrate
pod install
```

## Syntax-Check ohne vollständige Kompilierung

Wenn du nur prüfen möchtest, ob der Swift-Code syntaktisch korrekt ist:

```bash
# Syntax-Check für einzelne Dateien
swiftc -syntax-only FindMySync/Synchronizer.swift \
       -import-objc-header FindMySync/FindMySync-Bridging-Header.h \
       -sdk $(xcrun --show-sdk-path)

# Oder mit xcodebuild
xcodebuild -workspace FindMySync.xcworkspace \
           -scheme FindMySync \
           -sdk macosx \
           -destination 'platform=macOS' \
           clean build \
           -dry-run
```

## Entwicklung

### Hot Reload während der Entwicklung

Xcode unterstützt keine automatische Hot-Reload-Funktion. Du musst nach Änderungen:

1. Stoppe die laufende App (`Cmd + .`)
2. Kompiliere neu (`Cmd + B`)
3. Starte die App (`Cmd + R`)

### Debugging

1. Setze Breakpoints in Xcode
2. Starte mit `Cmd + R`
3. Nutze die Konsole für Log-Ausgaben

### Tests

```bash
# Alle Tests ausführen
xcodebuild test -workspace FindMySync.xcworkspace \
                -scheme FindMySync \
                -destination 'platform=macOS'
```

## Distribution

### DMG erstellen (mit fastlane)

```bash
bundle exec fastlane mac release
```

Die DMG-Datei wird im `build/`-Verzeichnis erstellt.

### Manuelles Export

1. Archive erstellen: `Product > Archive` in Xcode
2. Im Organizer: `Distribute App > Copy App`
3. DMG mit Disk Utility erstellen

## Hinweise für macOS Sequoia/Tahoe

Wenn du auf macOS 15+ (Sequoia) oder 26+ (Tahoe) entwickelst und testest:

1. Die App benötigt "Full Disk Access" zum Lesen der FindMy-Daten
2. Der BeaconStore-Schlüssel muss möglicherweise manuell extrahiert werden
3. Siehe `docs/SEQUOIA_TAHOE_SUPPORT.md` für Details

## Weitere Ressourcen

- [Xcode Documentation](https://developer.apple.com/documentation/xcode)
- [CocoaPods Documentation](https://cocoapods.org)
- [fastlane Documentation](https://docs.fastlane.tools)
