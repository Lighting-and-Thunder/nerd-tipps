# Nerd Tipps #02: Bildsequenzen blitzschnell abspielen

## 1. Terminal im richtigen Ordner öffnen

Systemeinstellungen → Tastatur → Tastaturkurzbefehle

![macOS Tastatur Settings](assets/01-settings.png)

Dienste → Dateien und Ordner → Neuer Terminal-Tab beim Ordner

![macOS Kurzbefehl Settings](assets/02-settings.png)

Dann den Kurzbefehl festlegen.

Ich benutze: ``⌘ + .``

Caveat: Mit dem default mac Terminal funktioniert der Tastaturbefehl nur wenn du einen Ordner ausgewählt hast, nicht bei Dateien. Das Problem hast du bei vielen anderen Terminal Emulatoren nicht. Empfehlung: [ghostty](https://ghostty.org/docs/install/binary#macos).

Für ghostty Tastenkombination für *"New Ghostty Tab Here"* anpassen.


## 2. mpv installieren

**macOS:** Nutze Homebrew im Terminal:

    brew install mpv


## 3. Setup (Einmalig)
Öffne das Terminal.

Öffne deine zsh-Konfiguration, z.B. mit TextEdit:

    open -e ~/.zshrc
Füge diesen Code ganz unten in die Datei ein.
Passe den Funktionsnamen seq oder die default frame rate (24) bei Bedarf an.:

```
seq() {
    # USAGE: when 24fps, just type seq, otherwise type seq {framerate}, for example: seq 60
    local fps=${1:-24}
    # Find most frequent extension (excluding hidden files)
    local ext=$(ls -1 | grep '\.' | sed 's/.*\.//' | sort | uniq -c | sort -nr | head -n1 | awk '{print $2}')

    if [[ -z "$ext" ]]; then
    echo "No files with extensions found."
    return 1
    fi

    mpv "mf://*.${ext}" --mf-fps="${fps}" --loop --icc-profile-auto
}
```

Speichere die Datei (⌘ + S) und schließe TextEdit.

Lade die Konfiguration neu (oder starte das Terminal neu):

```
source ~/.zshrc
```

## 4. Nutzung
Im Terminal, im Ordner mit einer Bildsequenz.

Mit Standard-Framerate (24 fps):

```
seq
```
Mit benutzerdefinierter Framerate (z.B. 60 fps):

```
seq 60
```

... sick, oder?