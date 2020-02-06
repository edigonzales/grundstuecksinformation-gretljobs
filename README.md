# grundstuecksinformation-gretljobs

```
export ORG_GRADLE_PROJECT_dbUriGrundstuecksinformation="jdbc:postgresql://localhost:54321/grundstuecksinformation"
export ORG_GRADLE_PROJECT_dbUserGrundstuecksinformation="gretl"
export ORG_GRADLE_PROJECT_dbPwdGrundstuecksinformation="gretl"
```

Beispiel:
```
./gradlew --init-script $PWD/init.gradle -p grundstuecksinformation-av-download/ --no-daemon -i tasks --all
./gradlew --init-script $PWD/init.gradle -p grundstuecksinformation-av-import/ --no-daemon -i tasks --all
```