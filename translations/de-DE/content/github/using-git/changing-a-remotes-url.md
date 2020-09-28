---
title: Die URL eines Remote-Repositorys ändern
redirect_from:
  - /articles/changing-a-remote-s-url
  - /articles/changing-a-remotes-url
intro: Der Befehl `git remote set-url` ändert die vorhandene URL eines Remote-Repositorys.
versions:
  free-pro-team: '*'
  enterprise-server: '*'
---

{% tip %}

**Tipp:** Informationen zum Unterschied zwischen HTTPS- und SSH-URLs findest Du unter „[Welche Remote-URL sollte ich verwenden?](/articles/which-remote-url-should-i-use).“

{% endtip %}

Der Befehl `git remote set-url` hat zwei Argumente:

* einen vorhandenen Remote-Namen. Zwei gängige Namen sind z. B. `origin` oder `upstream`.
* eine neue URL für das Remote-Repository. Ein Beispiel:
  * Wenn Du eine Aktualisierung auf HTTPS durchführst, sieht die URL ähnlich aus wie folgende:
```shell
https://{{ site.data.variables.command_line.backticks }}/<em>USERNAME</em>/<em>REPOSITORY</em>.git
```
  * Wenn Du eine Aktualisierung auf SSH durchführst, sieht die URL ähnlich aus wie folgende:
```shell
git@{{ site.data.variables.command_line.codeblock }}:<em>USERNAME</em>/<em>REPOSITORY</em>.git
```

### Remote-URLs von SSH auf HTTPS umstellen

{{ site.data.reusables.command_line.open_the_multi_os_terminal }}
2. Wechsle Dein aktuelles Arbeitsverzeichnis in das lokale Projekt.
3. Liste die vorhandenen Remote-Repositorys auf, um den Namen des Remote-Repositorys zu erhalten, dessen URL Du ändern möchtest.
  ```shell
  $ git remote -v
  > origin  git@{{ site.data.variables.command_line.codeblock }}:<em>USERNAME/REPOSITORY</em>.git (fetch)
  > origin  git@{{ site.data.variables.command_line.codeblock }}:<em>USERNAME/REPOSITORY</em>.git (push)
  ```
4. Ändere die URL Deines Remote-Repositorys mit dem Befehl `git remote set-url` von SSH in HTTPS.
  ```shell
  $ git remote set-url origin https://{{ site.data.variables.command_line.codeblock }}/<em>USERNAME</em>/<em>REPOSITORY</em>.git
  ```
5. Überprüfe, ob die Remote-URL geändert wurde.
  ```shell
  $ git remote -v
  # Überprüfe die neue Remote URL
  > origin  https://{{ site.data.variables.command_line.codeblock }}/<em>USERNAME/REPOSITORY</em>.git (fetch)
  > origin  https://{{ site.data.variables.command_line.codeblock }}/<em>USERNAME/REPOSITORY</em>.git (push)
  ```

Wenn Du das nächste Mal den Befehl `git fetch`, `git pull` oder `git push` für das Remote-Repository ausführst, musst Du Deinen GitHub-Benutzernamen und Dein Passwort eingeben.

- Wenn Du die [Zwei-Faktor-Authentifizierung](/articles/securing-your-account-with-two-factor-authentication-2fa) aktiviert hast, musst Du [ein persönliches Zugriffstoken erstellen](/github/authenticating-to-github/creating-a-personal-access-token), das Du anstelle Deines GitHub-Passworts verwendest.
- Sie können einen [Credential-Helper](/github/using-git/caching-your-github-credentials-in-git) verwenden, damit Git Ihren GitHub-Benutzernamen und Ihr -Passwort für die Kommunikation mit GitHub speichert.

### Switching remote URLs from HTTPS to SSH

{{ site.data.reusables.command_line.open_the_multi_os_terminal }}
2. Wechsle Dein aktuelles Arbeitsverzeichnis in das lokale Projekt.
3. Liste die vorhandenen Remote-Repositorys auf, um den Namen des Remote-Repositorys zu erhalten, dessen URL Du ändern möchtest.
  ```shell
  $ git remote -v
  > origin  https://{{ site.data.variables.command_line.codeblock }}/<em>USERNAME/REPOSITORY</em>.git (fetch)
  > origin  https://{{ site.data.variables.command_line.codeblock }}/<em>USERNAME/REPOSITORY</em>.git (push)
  ```
4. Ändere die URL Deines Remote-Repositorys mit dem Befehl `git remote set-url` von HTTPS in SSH.
  ```shell
  $ git remote set-url origin git@{{ site.data.variables.command_line.codeblock }}:<em>USERNAME</em>/<em>REPOSITORY</em>.git
  ```
5. Überprüfe, ob die Remote-URL geändert wurde.
  ```shell
  $ git remote -v
  # Überprüfe die neue Remote URL
  > origin  git@{{ site.data.variables.command_line.codeblock }}:<em>USERNAME/REPOSITORY</em>.git (fetch)
  > origin  git@{{ site.data.variables.command_line.codeblock }}:<em>USERNAME/REPOSITORY</em>.git (push)
  ```

### Problemlösungen

Beim Ändern eines Remote-Repositorys können folgende Fehler auftreten.

#### No such remote '[name]' (kein solches Remote-Repository)

Wenn dieser Fehler ausgegeben wird, ist das Remote-Repository, das Du ändern wolltest, nicht vorhanden:

```shell
$ git remote set-url sofake https://{{ site.data.variables.command_line.codeblock }}/octocat/Spoon-Knife
> fatal: No such remote 'sofake'
```

Überprüfen Sie, ob Sie den Remote-Namen korrekt eingegeben haben.

### Weiterführende Informationen

- [„Mit Remote-Repositorys arbeiten“ aus dem _Pro Git_-Buch](https://git-scm.com/book/en/Git-Basics-Working-with-Remotes)