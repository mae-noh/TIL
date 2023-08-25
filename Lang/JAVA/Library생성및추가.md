# Library 생성 및 추가

### build.gradle
```
    enabled = true

    version = '10.25.1-SNAPSHOT'

    manifest {
        attributes 'Main-Class': 'ai.plats.scr.OcrApplication'
    }

    from {
        configurations.runtimeClasspath.collect {
            it.isDirectory() ? it : zipTree(it)
        }
    }

    duplicatesStrategy = DuplicatesStrategy.EXCLUDE
```

### 

### 
