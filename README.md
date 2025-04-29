# Spring Boot Redis Caching Example

Ce projet Spring Boot montre comment intégrer **Redis** comme système de cache avec des fonctionnalités avancées.

## Fonctionnalités de base

- API REST pour accéder aux livres.
- Cache Redis avec `@Cacheable`, `@CacheEvict`, `@CachePut`.
- Configuration de cache TTL personnalisé pour différents types de données.

## Défis supplémentaires implémentés

1. ✅ **Compteur de hits/misses du cache** via un compteur simple (`CacheStats`).
2. ✅ **Chargement par lot** des livres pour tester le comportement du cache à grande échelle.
3. ✅ **Délais d'expiration personnalisés** : 10 minutes pour les livres, 1 heure pour les auteurs.
4. ✅ **Mise en cache conditionnelle** : seulement si un livre dépasse 300 pages.
5. ✅ **Interface simple pour comparaison** du temps de réponse entre accès avec et sans cache.

## Endpoints principaux

| Méthode | Endpoint                      | Description                                     |
|--------|-------------------------------|------------------------------------------------|
| GET    | `/book/cached/{id}`           | Récupère un livre avec cache                   |
| GET    | `/book/direct/{id}`           | Récupère un livre directement de la DB         |
| GET    | `/cache/stats`                | Donne les stats de cache (hits, misses)        |
| POST   | `/books/bulk`                 | Chargement par lots de livres                  |

## Configuration du cache

Dans la classe `RedisConfig` :
```java
configMap.put("books", RedisCacheConfiguration.defaultCacheConfig().entryTtl(Duration.ofMinutes(10)));
configMap.put("authors", RedisCacheConfiguration.defaultCacheConfig().entryTtl(Duration.ofHours(1)));
```

## Lancer le projet

1. Assurez-vous d'avoir Redis lancé sur `localhost:6379`
2. Exécutez la commande :
```bash
mvn spring-boot:run
```
3. Testez les endpoints via Postman ou votre navigateur.

---

© 2025 - Projet pédagogique Spring Boot + Redis
