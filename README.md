## Navigation (`cd`, `ls`, `pwd`)
- `pwd` — aktuellen Pfad anzeigen.
- `ls` / `ls -la` — Inhalt anzeigen (inkl. versteckter Dateien).
- `cd <pfad>` — in Ordner wechseln; Tab-Completion nutzen.
- `cd ..` / `cd ../..` — eine oder zwei Ebenen hoch.
- `cd -` — zum vorherigen Verzeichnis zurück.
- `cd ~` — ins Home-Verzeichnis.
- `cd ~/proj/esphome` — Pfad relativ zum Home (Beispiel).
- `cd /c/Users/Artem/Documents/esphome` — Windows-Pfad in Git Bash (Laufwerk als `/c`).
- `cd "$(git rev-parse --show-toplevel)"` — direkt zur Git-Repo-Wurzel.
- `cd /` — Root des Dateisystems.

## Häufige Git-Befehle
- `git status` — Repo-Status prüfen.
- `git add <pfad>` — Dateien vormerken.
- `git restore --staged <pfad>` — versehentlich vorgemerkte Datei lösen.
- `git commit -m "Nachricht"` — committen.
- `git log --oneline --graph --decorate -20` — kompakte Historie.
- `git diff` / `git diff --staged` — Änderungen ansehen.
- `git branch -vv` — Branches mit Tracking.
- `git switch <branch>` / `git switch -c <neu>` — Branch wechseln/erstellen.
- `git fetch --all --prune` — Remotes aktualisieren & verwaiste Refs entfernen.
- `git pull --rebase` — Remote-Änderungen sauber einreihen.
- `git push` — Commits senden; mit `-u origin <branch>` Tracking setzen.
- `git stash push -m "kurz"` / `git stash pop` — Arbeitsstand parken/holen.
- `git cherry -v` — Commits anzeigen, die auf Remote fehlen.
- `git revert <commit>` — Commit rückgängig als neuer Commit.
- `git clean -fd` — ungetrackte Dateien löschen (vorsicht!).
- `git tag -a v1.0.0 -m "Release"` — annotierten Tag setzen.
- `git rebase -i HEAD~N` — letzte N Commits interaktiv aufräumen.
- `git bisect start|bad|good` — fehlerverursachenden Commit finden.
- `git config --global user.name "Name"` / `user.email "mail@dom"` — Identität setzen.

## Rebase-Kommandos
- `git pull --rebase` — Remote-Änderungen rebasen.
- `git rebase <branch>` — aktuellen Branch auf Basis von `<branch>` neu aufbauen.
- `git rebase --continue` — nach Konfliktlösung fortsetzen.
- `git rebase --abort` — Rebase abbrechen und Zustand vor Start wiederherstellen.
- `git rebase --quit` — Rebase-Flow beenden, Arbeitsbaum/Index unverändert lassen.
- `git rebase --skip` — aktuellen Patch überspringen (nur wenn sinnvoll).
- `git rebase -i HEAD~N` — interaktiv umordnen/squashen.
- `GIT_SEQUENCE_EDITOR="code --wait" git rebase -i ...` — Editor festlegen.
- `git status` — Rebase-Status prüfen („rebase in progress“).

## Remote-Verwaltung
- `git remote -v` — Remotes mit URLs anzeigen.
- `git remote add origin <URL>` — neuen Remote hinzufügen.
- `git remote set-url origin <URL>` — Remote-URL ändern (https/ssh).
- `git remote rename origin upstream` — Remote umbenennen.
- `git remote remove <name>` — Remote löschen.
- `git fetch --all --prune` — alle Remotes aktualisieren & verwaiste Refs entfernen.
- `git push -u origin <branch>` — Branch erstmals pushen und Tracking setzen.
- `git push --delete origin <branch>` — Remote-Branch entfernen.
- `git ls-remote origin` — Refs/Tags direkt beim Remote anzeigen.

## Typische Workflows
1) Repo öffnen: `cd /c/Users/Artem/Documents/esphome`
2) Überblick: `git status` → `git diff`
3) Ändern & committen: `git add ...` → `git commit -m "..."`
4) Aktuell bleiben: `git fetch --all --prune` → `git pull --rebase`
5) Branch veröffentlichen: `git push -u origin <branch>`
6) Aufräumen: `git clean -fd` (vorher `git status` prüfen)

## Branch-Wechsel mit lokalen Änderungen
- Wenn `git switch/checkout <branch>` wegen lokaler Änderungen blockt:
  - Behalten & committen: `git add ...` → `git commit -m "..."`
  - Oder parken: `git stash push -m "wip"` → `git switch <branch>` → `git stash pop`
  - Oder verwerfen: `git checkout -- <datei>` (löscht Änderungen!)

## Upstream/Push-Probleme
- Fehlermeldung „has no upstream branch“: `git push -u origin <branch>`
- Abweichender Remote-Name (z.B. `origin/arti`):  
  - Sofort pushen: `git push origin HEAD:arti`  
  - Upstream neu setzen: `git branch --unset-upstream` → `git push -u origin <branch>`
- Standardverhalten für neue Branches: `git config --global push.default current`
