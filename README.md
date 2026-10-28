# Suivi de commande client · cas pratique Qwokka

Kit de démo du cas pratique « Lead Delivery & AI Automation » (Growth Ex Machina × Qwokka).
Site : https://growthexmachina2.github.io/qwokka-demo/

| Dossier | Contenu |
|---|---|
| `presentation/` | La présentation (mode plein écran, notes) |
| `simulateur/` | Le simulateur des règles, jour par jour |
| `n8n/` | Les 3 workflows n8n à importer |
| `donnees/` | Le jeu de démo : 30 commandes « ERP » et la mémoire de la veille (CSV et JSON) |

## Installer les workflows dans votre n8n

1. **Créer deux tables de données** (Data tables) :
   - `Qwokka · ERP commandes (démo)` : `order_number`, `company`, `contact_email`, `order_date`, `delivery_date`, `status`, `scenario`, `attendu` (texte).
   - `Qwokka · Mémoire du flux` : `order_number`, `contact_email`, `last_status`, `status_since`, `last_delivery_date`, `initial_delivery_date`, `sent`, `last_seen` (texte), `nb_glissements` (nombre).
2. **Importer** les 3 fichiers de `n8n/` (menu *Import from file*).
3. Dans chaque nœud « table de données », **sélectionner la table** correspondante (le nom est pré-rempli).
4. Créer un identifiant **SendGrid** et le choisir dans les deux nœuds d’envoi du workflow 1.
5. Dans le nœud **Réglages** du workflow 1 : adresse d’expédition (domaine authentifié dans SendGrid), adresses internes et de test, URL de votre instance, secret du lien. Reporter l’URL et le secret dans le nœud « Construire la page client » du workflow 2.
6. Lancer **Qwokka · 0 · Réinitialiser la démo**, publier les workflows 1 et 2, puis ouvrir `https://VOTRE-INSTANCE/webhook/qwokka-apercu`.

Modes du workflow 1 : planifié à 7h = *simulation* (rien ne part) tant que le distributeur n’a pas validé ; lancement manuel = *test* (envois réels redirigés vers la boîte de test) ; aperçu web = page « qui recevrait quoi ».

Les données sont fictives. Le jeu de démo est daté du 28 octobre 2026 dans `donnees/` ; le workflow 0 le recrée avec des dates relatives au jour de son lancement.
