# Git Bash Spickzettel

## Häufige Befehle
- `git status` — aktuellen Repo-Status anzeigen (Änderungen, Branch).
- `git add <pfad>` — Dateien für den nächsten Commit vormerken.
- `git restore --staged <pfad>` — versehentlich vorgemerkte Datei wieder lösen.
- `git commit -m "Nachricht"` — vorgemerkte Änderungen committen.
- `git log --oneline --graph --decorate -20` — kompakte Historie der letzten 20 Commits.
- `git diff` — nicht vorgemerkte Änderungen sehen; mit `--staged` für vorgemerkte.
- `git branch -vv` — lokale Branches mit Tracking-Info.
- `git switch <branch>` — Branch wechseln; `-c` um neuen zu erstellen.
- `git fetch --all --prune` — Remotes aktualisieren und verwaiste Branch-Refs aufräumen.
- `git pull --rebase` — Änderungen vom Remote holen und sauber einreihen.
- `git push` — lokale Commits zum Remote senden; `-u origin <branch>` zum Setzen des Tracking.
- `git stash push -m "kurz"` — Arbeitsstand temporär weglegen; `git stash pop` wiederholen.
- `git cherry -v` — Commits zeigen, die auf Remote fehlen.
- `git revert <commit>` — einzelnen Commit rückgängig machen (neuer Commit).
- `git clean -fd` — nicht getrackte Dateien/Ordner löschen (vorsichtig!).
- `git tag -a v1.0.0 -m "Release"` — annotierten Tag setzen.
- `git rebase -i HEAD~5` — letzte 5 Commits interaktiv aufräumen (umordnen/squashen).
- `git bisect start|bad|good` — fehlerverursachenden Commit eingrenzen.
- `git config --global user.name "Name"` — Git-Identität setzen; analog `user.email`.

## Nützliche Alias-Ideen (optional)
- `git config --global alias.st "status -sb"`
- `git config --global alias.lg "log --oneline --graph --decorate --all"`
- `git config --global alias.co switch`
- `git config --global alias.br "branch -vv"`
- `git config --global alias.df "diff --stat"`

## Typische Workflows
1) Änderungen ansehen: `git status` → `git diff`.
2) Vormerken & committen: `git add ...` → `git commit -m "..."`
3) Auf aktuellem Stand bleiben: `git fetch --all --prune` → `git pull --rebase`
4) Branch veröffentlichen: `git push -u origin <branch>`
5) Schnelles Aufräumen: `git clean -fd` (vorher `git status` prüfen).

## Sicherheitstipps
- Vor destruktiven Aktionen (z.B. `clean`, `reset`, `rebase`) immer `git status` prüfen.
- `git pull --rebase` minimiert Merge-Commits; bei Konflikten: Konflikte lösen, `git rebase --continue`.
- Regelmäßig `git fetch --all --prune`, damit alte Remote-Refs verschwinden.
