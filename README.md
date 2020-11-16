# OvescoFacturationBundle

Module de facturation pour le netBS avec emission de factures QR.

## Installation
- Clonez d'abord le netBS et préparez le
- Ajoutez les dépendances suivantes avec composer:
    - genkgo/camt
    - sprain/swiss-qr-bill
- Ajoutez ce bundle en submodule git de votre projet avec `git add submodule https://github.com/sauvabelin/netBS-facturation netBS/ovesco/FacturationBundle`
- Ajoutez l'entrée PSR-4 dans le composer.json ```js
"autoload": {
    "psr-4": {
        // ...
        "Ovesco\\FacturationBundle\\": "netBS/ovesco/FacturationBundle",
    }
},
```
- Générez l'autoload avec `composer dump-autoload`
- Ajoutez le Bundle dans votre `bundles.php` : `\Ovesco\FacturationBundle\OvescoFacturationBundle::class => ['all' => true]`
- Ajoutez les routes dans le `routes.yaml`:
```yaml
facturation:
    resource: '@OvescoFacturationBundle/Resources/config/routing.yml'
    prefix: /netBS/facturation
```
- Ajoutez le chargement des entités dans `doctrine.yaml`:
```yaml
OvescoFacturationBundle:
    type: annotation
    dir: 'Entity'
    is_bundle: true
    prefix: Ovesco\FacturationBundle\Entity
    alias: OvescoFacturationBundle
```
- Ajoutez les services dans votre `services.yaml`:
```yaml
imports:
    - { resource: "@OvescoFacturationBundle/Resources/config/services.yml" }
```
- Mettez à jour le schéma de BDD `php bin/console doctrine:schema:update --force`
- Chargez le ROLE_TRESORIER avec `php bin/console doctrine:fixtures:load --append --group=facturation`
