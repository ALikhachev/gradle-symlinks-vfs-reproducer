# Reproducer for the problem with VFS inputs tracking

1. Ensure `src/main` is a symlink to `src/real-main`
2. Invoke `./gradlew compileJava`
3. Apply some change to `src/real-main/java/Main.java` (e.g. such one introducing a compilation error)
4. Invoke `./gradlew compileJava` – the `:compileJava` task will be UP-TO-DATE
5. Restore the state of the source.
6. Invoke `./gradlew compileJava --no-watch-fs`
7. Apply some change to `src/real-main/java/Main.java` (e.g. such one introducing a compilation error)
8. Invoke `./gradlew compileJava --no-watch-fs` – now it's properly recompiled

Gradle issue tracker link: https://github.com/gradle/gradle/issues/27373