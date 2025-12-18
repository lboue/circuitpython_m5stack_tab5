# M5Stack Tab5 IoT Development Kit by M5Stack

# Circuitpython

- https://circuitpython.org/board/m5stack_tab5/
- https://github.com/adafruit/circuitpython/tree/main/ports/espressif/boards/m5stack_tab5

Pour **compiler CircuitPython pour la carte `m5stack_tab5`** (le dossier que tu montres sur GitHub), voici une **procédure concrète pas à pas** basée sur la documentation officielle de CircuitPython & Espressif.

---

## 🧰 Prérequis

### 1) Dépendances système (Linux/macOS)

Installe les outils requis :

```sh
sudo apt update
sudo apt install git cmake ninja-build python3 python3-pip python-is-python3
```

Puis installe les paquets Python nécessaires pour CircuitPython :

```sh
pip3 install --upgrade -r requirements-dev.txt
pip3 install --upgrade -r requirements-doc.txt
```

⚠️ Tu dois être dans le dossier racine du repo CircuitPython pour ces commandes.([Adafruit][1])

---

## 📦 2) Récupérer le code CircuitPython

Clone le dépôt officiel :

```sh
git clone https://github.com/adafruit/circuitpython.git
cd circuitpython
```

Si tu veux faire des modifs *et* éventuellement proposer un patch, pense à **forker** le dépôt sur GitHub et cloner ton fork.([Adafruit][1])

---

## 🧠 3) Configurer l’environnement Espressif

CircuitPython utilise **ESP-IDF**, le SDK officiel d’Espressif.

### a) Aller dans le port Espressif :

```sh
cd ports/espressif
```

### b) Installer ESP-IDF + outils associés :

```sh
./esp-idf/install.sh
```

### c) Charger l’environnement dans ton shell :

Chaque fois que tu ouvriras une nouvelle fenêtre :

```sh
source esp-idf/export.sh
```

Cela exporte les variables d’environnement nécessaires pour la compilation.([docs.circuitpython.org][2])

---

## 🔨 4) Compiler pour **m5stack_tab5**

Retourne dans le dossier principal du port Espressif :

```sh
cd ~/circuitpython/ports/espressif
```

Puis lance **make** en ciblant le nom du **BOARD** correspondant à la carte (`m5stack_tab5`).
⚠️ Le nom du board = le nom du dossier dans `ports/espressif/boards/` (donc ici `m5stack_tab5`).

```sh
make BOARD=m5stack_tab5
```

### 🧪 Si tu veux *flasher* directement après compilation :

Précise aussi le port série :

```sh
make BOARD=m5stack_tab5 PORT=/dev/ttyUSB0 flash
```

(adapte `/dev/ttyUSB0` à ton port réel)([docs.circuitpython.org][2])

---

## 📦 5) Fichiers générés

Après compilation réussie, les firmwares sont dans un dossier `build-m5stack_tab5/`.
Tu verras typiquement :

* `firmware.bin` → l’image *flashable*
* `firmware.uf2` → option UF2 si supporté

⚠️ Le `.bin` est généralement ce qu’il faut flasher sur les ESP32.([Adafruit][3])

---

## 🛠️ Notes de personnalisation (facultatives)

### 🎛️ Ajuster les configs

Dans le dossier `ports/espressif/boards/m5stack_tab5/`, tu as sûrement :

* un fichier `mpconfigboard.h`
* un fichier `sdkconfig.defaults` (ou équivalent)

Tu peux y ajuster les paramètres comme le flash, LED, broches, etc., *avant* de compiler.([Adafruit][4])

---

## ❓ Problèmes possibles

### 📌 USB / support ESP32-P4

CircuitPython supporte **ESP32**, mais les SoC **ESP32-P4** (comme celui du Tab5) peuvent être encore partiellement pris en charge (parfois sans USB natif ou avec limitations).
Vérifie la page du board sur circuitpython.org pour voir si une version binaire est déjà fournie — ça te permet souvent d’éviter la compilation toi-même et de tester d’abord.([circuitpython.org][5])

---

## 🧪 Résumé rapide

| Étape       | Commande / Action                                  |
| ----------- | -------------------------------------------------- |
| Clone       | `git clone … && cd circuitpython`                  |
| Dépendances | `pip3 install -r …`                                |
| ESP-IDF     | `./esp-idf/install.sh && source esp-idf/export.sh` |
| Build       | `make BOARD=m5stack_tab5`                          |
| Flash       | `make … PORT=/dev/… flash`                         |

---

Si tu veux, je peux aussi te fournir **scripts d’automatisation** (Bash ou PowerShell) pour simplifier ces étapes sur ton système, ou t’aider à débugger une erreur de compilation spécifique.

[1]: https://learn.adafruit.com/building-circuitpython/build-circuitpython?utm_source=chatgpt.com "Build CircuitPython | Building CircuitPython | Adafruit Learning System"
[2]: https://docs.circuitpython.org/en/latest/ports/espressif/README.html?utm_source=chatgpt.com "Espressif — Adafruit CircuitPython 1 documentation"
[3]: https://learn.adafruit.com/building-circuitpython/espressif-build?utm_source=chatgpt.com "Espressif Builds | Building CircuitPython | Adafruit Learning System"
[4]: https://learn.adafruit.com/how-to-add-a-new-board-to-circuitpython/customizing-the-board-files?utm_source=chatgpt.com "Customizing the Board Files | How to Add a New Board to CircuitPython | Adafruit Learning System"
[5]: https://circuitpython.org/board/m5stack_tab5/?utm_source=chatgpt.com "M5Stack Tab5 IoT Development Kit Download"
