# Buildpack Dart pour Scalingo (serveur Idélia)

Scalingo n'a pas de buildpack Dart : celui-ci installe le SDK Dart et compile le serveur Serverpod
d'Idélia avec `dart build cli`, **sans SDK Flutter**. Il ne contient aucun secret.

- `bin/detect` : reconnaît un espace de travail Dart (`pubspec.yaml` et `pubspec.lock` à la racine) ;
- `bin/compile` : installe Dart (empreinte SHA-256 vérifiée), résout les dépendances dans un espace
  de travail réduit aux paquets du serveur, refuse toute version différente du `pubspec.lock` du
  dépôt, compile ;
- `bin/release` : rien par défaut, le `Procfile` de l'application donne la commande de démarrage.

Réglages facultatifs (variables d'environnement de l'application Scalingo) : `DART_VERSION`
(3.12.2 par défaut), `DART_WORKSPACE_MEMBERS`, `DART_BUILD_PACKAGE`, `DART_BUILD_TARGET`.

Ce dossier est la source : il vit dans le dépôt Idélia (`deploy/scalingo-buildpack/`) et se publie
tel quel dans un dépôt git **public** que Scalingo lit par la variable `BUILDPACK_URL`. Les trois
fichiers de `bin/` doivent y être exécutables. Mode d'emploi complet : `docs/dev/11-back-end.md`.
