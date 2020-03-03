# grundstuecksinformation-gretljobs

## Developing

### Database

```
mkdir -m 0777 ~/pgdata-grundstuecksinformation
docker run --rm --name grundstuecksinformation-db -p 54321:5432 --hostname primary \
-e PG_DATABASE=grundstuecksinformation -e PG_LOCALE=de_CH.UTF-8 -e PG_PRIMARY_PORT=5432 -e PG_MODE=primary \
-e PG_USER=admin -e PG_PASSWORD=admin \
-e PG_PRIMARY_USER=repl -e PG_PRIMARY_PASSWORD=repl \
-e PG_ROOT_PASSWORD=secret \
-e PG_WRITE_USER=gretl -e PG_WRITE_PASSWORD=gretl \
-e PG_READ_USER=ogc_server -e PG_READ_PASSWORD=ogc_server \
-v ~/pgdata-grundstuecksinformation:/pgdata:delegated \
sogis/oereb-db:latest
```

## Running

```
export ORG_GRADLE_PROJECT_dbUriGrundstuecksinformation="jdbc:postgresql://localhost:54321/grundstuecksinformation"
export ORG_GRADLE_PROJECT_dbUserGrundstuecksinformation="gretl"
export ORG_GRADLE_PROJECT_dbPwdGrundstuecksinformation="gretl"
```

Beispiel mit Docker:
```
./start-gretl.sh --docker-image sogis/gretl-runtime:latest --job-directory $PWD/grundstuecksinformation-av-download --no-daemon -i tasks --all
./start-gretl.sh --docker-image sogis/gretl-runtime:latest --job-directory $PWD/grundstuecksinformation-av-import --no-daemon -i tasks --all
```

Beispiel mit Gradle "pur":
```
./gradlew --init-script $PWD/init.gradle -p grundstuecksinformation-av-download/ --no-daemon -i tasks --all
./gradlew --init-script $PWD/init.gradle -p grundstuecksinformation-av-import/ --no-daemon -i tasks --all
```

## TODO:
- Wie soll der AV-Import in Jenkins funktionieren? Entweder Jobs 'irgendwie' verdrahten oder mit Subprojekten o.ä. probieren.
