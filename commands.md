https://github.com/aelassas/movinin/wiki/Run-from-Source-(Docker)
https://movin-in.github.io/?lang=en

Environment Variables for payments are in 
../aws-resources/movinin.sh

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

# to test if mongo is up
docker run --rm --network=movinin_mi-network debian:bookworm-slim getent hosts mongo

# test signup 
curl -X POST http://localhost:4004/api/sign-up \
  -H "Content-Type: application/json" \
  -d '{
    "email": "david@davidthigpen.com",
    "password": "test",
    "fullName": "David Thigpen",
    "language": "en",
    "birthDate": "1984-03-21T00:00:00.000Z",
    "phone": "6018269237",
    "avatar": "AVATAR1"
  }'

curl -X POST http://localhost:4004/api/sign-up \
  -H "Content-Type: application/json" \
  -d '{
    "email":"david@davidthigpen.com",
    "phone":"6018269237",
    "password":"xdN9S5FBd3LEk8R",
    "fullName":"David Thigpen",
    "birthDate":"1984-03-21T18:00:00.000Z",
    "language":"en"
}'

// Originally called from top context.
// To resend from the same execution context, select it in the Console’s toolbar.
await fetch("http://localhost:4004/api/sign-up", {
  "headers": {
    "accept": "application/json, text/plain, */*",
    // "accept-encoding": "gzip, deflate, br, zstd", // Browser negotiates compression
    "accept-language": "en-US,en;q=0.9",
    // "connection": "keep-alive", // Browser manages connections
    // "content-length": "166", // Browser calculates from body
    "content-type": "application/json",
    // "host": "localhost:4004", // Browser will derive from URL
    // "origin": "http://localhost:8081", // Browser will set based on request context
    // "referer": "http://localhost:8081/", // Browser will set this from referrer option + policy
    // All sec-* headers are set by the browser
    // "sec-ch-ua": "\"Chromium\";v=\"154\", \"Google Chrome\";v=\"154\", \"Not A(Brand\";v=\"99\"",
    // "sec-ch-ua-mobile": "?0",
    // "sec-ch-ua-platform": "\"Linux\"",
    // "sec-fetch-dest": "empty",
    // "sec-fetch-mode": "cors",
    // "sec-fetch-site": "same-site",
    "user-agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/154.0.0.0 Safari/537.36"
  },
  "referrer": "http://localhost:8081/",
  "body": "{\"email\":\"david@davidthigpen.com\",\"phone\":\"6018269237\",\"password\":\"xdN9S5FBd3LEk8R\",\"fullName\":\"David Thigpen\",\"birthDate\":\"1984-03-21T18:00:00.000Z\",\"language\":\"en\"}",
  "method": "POST",
  "mode": "cors",
  "credentials": "omit"
});
// Make any edits, then ENTER to resend
