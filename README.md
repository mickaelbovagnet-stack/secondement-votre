# Secondement Vôtre · site vitrine

One-pager statique (un seul `index.html`, polices Parkinsans et Shrikhand intégrées, aucun cookie ni outil tiers). Hébergement GitHub Pages, domaine et e-mail chez Hostinger.

## Contenu du dépôt

| Fichier | Rôle |
|---|---|
| `index.html` | La page complète |
| `CNAME` | Le domaine personnalisé lu par GitHub Pages (`secondementvotre.fr`) |
| `.nojekyll` | Sert les fichiers tels quels, sans traitement Jekyll |
| `favicon.svg`, `favicon-32.png`, `apple-touch-icon.png` | Icônes d'onglet et d'écran d'accueil |
| `og-image.png` | Visuel de partage LinkedIn et messageries |
| `robots.txt`, `sitemap.xml` | Référencement |

## Avant la mise en ligne

Les mentions légales sont complètes (adresse et TVA identiques à CxO).

Si le domaine ou l'adresse e-mail diffèrent de `secondementvotre.fr` et `bonjour@secondementvotre.fr`, remplacer partout dans `index.html`, `CNAME`, `robots.txt` et `sitemap.xml`.

## 1 · GitHub

1. Créer un dépôt public, par exemple `secondement-votre`
2. Y déposer tous les fichiers de ce dossier (glisser-déposer via « Add file › Upload files » suffit)
3. Settings › Pages › Source · « Deploy from a branch », branche `main`, dossier `/ (root)`
4. Custom domain · `secondementvotre.fr`, puis Save
5. Dans les paramètres GitHub du compte (Settings › Pages › Add a domain), vérifier le domaine pour le protéger. GitHub fournit un enregistrement TXT `_github-pages-challenge-…` à ajouter chez Hostinger

## 2 · Hostinger · DNS du site

Domaines › secondementvotre.fr › DNS / Nameservers. Supprimer d'abord l'enregistrement A `@` et le CNAME `www` de parking créés par défaut, puis ajouter les suivants.

| Type | Nom | Valeur |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| AAAA | @ | 2606:50c0:8000::153 |
| AAAA | @ | 2606:50c0:8001::153 |
| AAAA | @ | 2606:50c0:8002::153 |
| AAAA | @ | 2606:50c0:8003::153 |
| CNAME | www | `<compte-github>.github.io` (sans le nom du dépôt) |

Une fois la propagation faite (de quelques minutes à quelques heures), revenir dans GitHub › Settings › Pages et cocher « Enforce HTTPS » dès que la case devient disponible.

## 3 · Hostinger · e-mail

Créer la boîte `bonjour@secondementvotre.fr` dans Hostinger Email. Si le domaine utilise les serveurs DNS de Hostinger, les enregistrements sont en général ajoutés automatiquement. Sinon, ajouter les suivants.

| Type | Nom | Valeur | Priorité |
|---|---|---|---|
| MX | @ | mx1.hostinger.com | 5 |
| MX | @ | mx2.hostinger.com | 10 |
| TXT | @ | `v=spf1 include:_spf.mail.hostinger.com ~all` | |
| CNAME | hostingermail-a._domainkey | hostingermail-a.dkim.mail.hostinger.com | |
| CNAME | hostingermail-b._domainkey | hostingermail-b.dkim.mail.hostinger.com | |
| CNAME | hostingermail-c._domainkey | hostingermail-c.dkim.mail.hostinger.com | |
| TXT | _dmarc | `v=DMARC1; p=none; rua=mailto:bonjour@secondementvotre.fr` | |

Les enregistrements A, AAAA et CNAME `www` du site ne gênent pas l'e-mail, qui repose uniquement sur les MX, SPF, DKIM et DMARC.

Si le domaine avec accent (`secondementvôtre.fr`) a aussi été réservé, le rediriger vers `https://secondementvotre.fr` depuis Hostinger (Domaines › Redirections).

## 4 · Vérifications

- `https://secondementvotre.fr` et `https://www.secondementvotre.fr` affichent la page en HTTPS
- Un e-mail envoyé depuis Gmail vers `bonjour@` arrive, la réponse aussi
- Le lien partagé sur LinkedIn affiche le visuel (outil Post Inspector de LinkedIn)
