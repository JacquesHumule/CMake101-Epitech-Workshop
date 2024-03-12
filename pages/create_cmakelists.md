---
level: 2
highlighter: shiki
mdc: true
---

# Créer le CMakeList.txt
<v-clicks>

##### Dans le fichier <code>CMakeLists.txt</code> à la racine du projet :
````md magic-move
```cmake
cmake_minimum_required(VERSION 3.27)
```

```cmake
cmake_minimum_required(VERSION 3.27)

project(NanoTekSpice)
```

```cmake
cmake_minimum_required(VERSION 3.27)

project(NanoTekSpice
    LANGUAGES CXX
)
```

```cmake
cmake_minimum_required(VERSION 3.27)

project(NanoTekSpice CXX)
```

```cmake
cmake_minimum_required(VERSION 3.27)

project(NanoTekSpice
  LANGUAGES CXX
)
```

```cmake
cmake_minimum_required(VERSION 3.27)

project(NanoTekSpice
  LANGUAGES CXX
  VERSION 1.0
)
```

```cmake
cmake_minimum_required(VERSION 3.27)

project(NanoTekSpice
  LANGUAGES CXX
  VERSION 1.0
  DESCRIPTION "EPITECH’s electronics simulation"
)
```

```cmake
cmake_minimum_required(VERSION 3.27)

project(NanoTekSpice
  LANGUAGES CXX
  VERSION 1.0
  DESCRIPTION "EPITECH’s electronics simulation"
)

add_executable(nanotekspice)
```

```cmake
cmake_minimum_required(VERSION 3.27)

project(NanoTekSpice
  LANGUAGES CXX
  VERSION 1.0
  DESCRIPTION "EPITECH’s electronics simulation"
)

add_executable(nanotekspice
    src/main.cpp
    src/IComponent.hpp
)
```
````
</v-clicks>