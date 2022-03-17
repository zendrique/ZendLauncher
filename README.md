<p align="center"><img src="./app/assets/images/SealCircle.png" width="150px" height="150px" alt="aventium softworks"></p>

<h1 align="center">ZendLauncher</h1>


[<p align="center"><img src="https://img.shields.io/github/workflow/status/dscalzi/HeliosLauncher/Build.svg?style=for-the-badge" alt="gh actions">](https://github.com/zendrique/ZendLauncher/actions) [<img src="https://img.shields.io/github/downloads/dscalzi/HeliosLauncher/total.svg?style=for-the-badge" alt="downloads">](https://github.com/zendrique/ZendLauncher/releases)
## Téléchargements

Vous pouvez télécharger depuis [le site de zendland.](https://zendland.zendrique.fr/)

#### Dernière version

[![](https://img.shields.io/github/release/dscalzi/HeliosLauncher.svg?style=flat-square)](https://github.com/zendrique/ZendLauncher/releases/latest)

#### Dernière version préliminaire
[![](https://img.shields.io/github/release/dscalzi/HeliosLauncher/all.svg?style=flat-square)](https://github.com/zendrique/ZendLauncher/releases)

**Plates-formes prises en charge**

Si vous téléchargez à partir des [version](https://github.com/zendrique/ZendLauncher/releases), sélectionnez le programme d'installation de votre système.

| Platform | Fichichier |
| -------- | ---- |
| Windows x64 | `ZendLauncher-VERSION.exe` |
| macOS x64 | `ZendLauncher-VERSION-x64.dmg` |
| macOS arm64 | `HZendLauncher-VERSION-arm64.dmg` |
| Linux x64 | `ZendLauncher-VERSION.AppImage` |

## Develpopment

Cette section détaille la configuration d'un environnement de développement de base.

### Démarrage

**Configuration requise**

* [Node.js][nodejs] v16

---

**Cloner et installer les dépendances**

```console
> git clone https://github.com/zendrique/ZendLauncher.git
> cd ZendLauncher
> npm install
```

---

**Lancer l'application**

```console
> npm start
```

---

**Build le ZendLauncher**

Pour build pour votre plate-forme actuelle.

```console
> npm run dist
```

Pour build une plate-forme spécifique.

| Plate-forme    | Commande              |
| ----------- | -------------------- |
| Windows x64 | `npm run dist:win`   |
| macOS       | `npm run dist:mac`   |
| Linux x64   | `npm run dist:linux` |

Les versions pour macOS peuvent ne pas fonctionner sous Windows/Linux et vice-versa.

---

### Visual Studio Code

Tout développement du ZendLauncher doit être fait en utilisant [Visual Studio Code][vscode].

Collez ce qui suit dans `.vscode/launch.json`

```JSON
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug Main Process",
      "type": "node",
      "request": "launch",
      "cwd": "${workspaceFolder}",
      "program": "${workspaceFolder}/node_modules/electron/cli.js",
      "args" : ["."],
      "outputCapture": "std"
    },
    {
      "name": "Debug Renderer Process",
      "type": "chrome",
      "request": "launch",
      "runtimeExecutable": "${workspaceFolder}/node_modules/.bin/electron",
      "windows": {
        "runtimeExecutable": "${workspaceFolder}/node_modules/.bin/electron.cmd"
      },
      "runtimeArgs": [
        "${workspaceFolder}/.",
        "--remote-debugging-port=9222"
      ],
      "webRoot": "${workspaceFolder}"
    }
  ]
}
```

Cela ajoute deux configurations de débogage.

#### Déboguer le processus principal

Cela vous permet de déboguer le [processus principal][mainprocess] d'Electron. Vous pouvez déboguer des scripts dans le [processus de rendu][rendererprocess] en ouvrant la fenêtre DevTools.

#### Déboguer le processus de rendu

Cela vous permet de déboguer le [processus de rendu][rendererprocess] d'Electron. Cela nécessite que vous installiez l'extension du [débogueur pour Chrome][chromedebugger].

Notez que vous **ne pouvez pas** ouvrir la fenêtre DevTools lors de l'utilisation de cette configuration de débogage. Chromium n'autorise qu'un seul débogueur, en ouvrir un autre fera planter le programme.

---