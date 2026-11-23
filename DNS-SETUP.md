# DNS: playbackforward.com auf GitHub Pages umstellen

Stand: 23.11.2026. Die Domain und die E-Mail bleiben bei IONOS, die Website läuft auf GitHub Pages.

> **Erst umstellen, wenn die Seite auf GitHub läuft.** Sonst zeigt die Domain ins Leere.
> **WordPress-Vertrag erst danach ändern**, und zwar per Wechsel auf einen Domain- und Mail-Tarif, nicht per Kündigung (sonst sind Domain und Postfächer weg).

## Wo in IONOS

Kundenbereich → **Domains & SSL** → **playbackforward.com** → Reiter **DNS**.

Ist die Domain fest mit dem WordPress-Paket verbunden, unter **Domain-Verwendung** bzw. „Ziel ändern“ zuerst auf **Eigene DNS-Einstellungen** stellen.

## Einträge

Die bestehenden A- und AAAA-Einträge für `@`, die auf WordPress zeigen, löschen und durch diese ersetzen:

| Typ | Host | Wert |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| AAAA | @ | 2606:50c0:8000::153 |
| AAAA | @ | 2606:50c0:8001::153 |
| AAAA | @ | 2606:50c0:8002::153 |
| AAAA | @ | 2606:50c0:8003::153 |
| CNAME | www | `<github-name>.github.io` |

Einen vorhandenen A-Eintrag für `www` löschen, denn ein CNAME darf nicht neben anderen Einträgen stehen.

**Domain-Verifizierung:** GitHub → Profilbild → *Settings → Pages → Add a verified domain*. GitHub nennt dort einen TXT-Eintrag:

| Typ | Host | Wert |
|---|---|---|
| TXT | `_github-pages-challenge-<github-name>` | Code von GitHub |

## Nicht anfassen (E-Mail)

- **MX**-Einträge
- **TXT** mit `v=spf1 …` und alles mit DKIM/DMARC
- `autodiscover` und andere Einträge, die mit Mail zu tun haben

## Danach

1. Repo → *Settings → Pages → Custom domain*: `playbackforward.com` eintragen und **Enforce HTTPS** aktivieren.
2. Die Umstellung wirkt meist nach Minuten, spätestens nach 24 Stunden.
3. Prüfen: Läuft https://playbackforward.com? Kommen Mails an info@ noch an?
4. Erst dann bei IONOS das WordPress-Paket auf einen Domain- und Mail-Tarif umstellen.

Die IP-Adressen vor dem Umstellen mit der GitHub-Doku abgleichen: „Managing a custom domain for your GitHub Pages site“.
