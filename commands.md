https://github.com/aelassas/movinin/wiki/Run-from-Source-(Docker)

Common problems are issues with mongodb version. 7.0.12 is the current stable version for development.

# initial load
docker-compose -f docker-compose.dev.yml up -d
# update with code changes
docker-compose -f docker-compose.dev.yml up -d --build
# update with code changes and rewrite the network
docker-compose -f docker-compose.dev.yml up -d --force-recreate--build
# delete
docker-compose -f docker-compose.dev.yml down

# to see logs if not set to silent in yaml
docker compose logs mongo
