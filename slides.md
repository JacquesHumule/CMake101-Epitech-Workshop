---
theme: default
layout: cover
background: https://cover.sli.dev
author: Jacques "JacquesHumule" Rathier
highlighter: shiki
hideInToc: true
mdc: true
---

# CMake 101

Le système de construction de projet multi-plateforme

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
hideInToc: true
---

# Table des matières

<Toc columns=2 />

---
transition: fade-out
title: "Qu’est ce que CMake"
---

# Qu’est ce que <devicon-cmake/>CMake


<v-clicks>

- Outil de construction du code source
- Générateur de buildsystem (Makefile, Ninja, Meson)
- _“Gestionnaire de dépendances”_
- Integration contextuelle pour différents IDE (Visual Studio, JetBrains, XCode...)
</v-clicks>

<v-click>

Son but:
> _Compiler, Lier, Installer_
</v-click>

---

# Qu’est ce qu’un Buildsystem

<v-clicks>

Le logiciel qui gère la compilation du projet:
- GNU Make
- Ninja
- Meson
- Visual Studio
- Xcode
- Etc...
</v-clicks>

---
layout: section
---

# Créer son projet CMake

---
src: pages/create_cmakelists.md
---

---
src: pages/generate_buildsystem.md
---

---
layout: default
title: Les options basiques de la CLI de cmake
---

# Les options basiques de la CLI de `cmake`
<v-clicks>

- `-S <sources-dir>` : Déclare la racine du projet (contient le CMakeList top-level) :
    ```sh
    cmake -S .
    ```
- `-B <build-dir>` : Déclare la racine du repertoire du buildsystem:
    ```sh
    cmake -B build
    ```
- `-G <generator-name>` : Déclare le nom du générateur
    ```sh
    cmake -G "Unix Makefiles"
    ```
- `-D <var>:<type>=<value>` ou `-D <var>:<value>` : Déclare une variable cache cmake
    ```sh
    cmake -DCMAKE_BUILD_TYPE=Release
    ```
- `--build <build-dir>` : Compile le buildsystem :
    ```sh
    cmake --build build
    ```
</v-clicks>

<v-click>
<br/>

> <fluent-emoji-warning/> [La commande]{style="color:orange"} `cmake .` [permet d’agir sur un buildsystem déjà crée ou utilise le dossier comme source dans le cas où ce dossier n’est pas un buildsystem]{style="color:orange"}
</v-click>

---
layout: section
---

# Les Targets
Cibles de compilation

---
level: 2
---

# Déclaration des Targets
<v-clicks>

- Executable:
    ```cmake
    add_executable(nanotekspice
        app/main.cpp
    )
    ```
- Librairie:
    ```cmake
    add_library(nanoteklib
        src/Circuit.cpp
    )
    ```
- Custom:
    ```cmake
    add_custom_target(coding_style)
    ```
</v-clicks>

---
level: 2
---

# Manipulation des Targets
<v-clicks>

- `target_sources(<target> PRIVATE <file> ...)` :\
    Ajoute des fichier sources a une target
    ```cmake
    target_sources(nanoteklib PRIVATE Comp.hpp Comp.cpp)
    ```
- `target_include_directory(<target> [PUBLIC|PRIVATE|INTERFACE] <dir> ...)` :\
    Ajoute des dossier pour le préprocesseur
    ```cmake
    target_include_directories(nanoteklib PRIVATE ./include)
    ```
- `target_compile_features(<target> PRIVATE <feature> ...)` :\
    Spécifie des fonctionnalités de compilation
    ```cmake
    target_compile_features(nanoteklib PRIVATE cxx_std_20)
    ```
- `set_target_properties(<target> PROPERTIES <prop>)` :\
    Spécifie des propriétés
    ```cmake
    set_target_properties(nanoteklib PROPERTIES INTERPROCEDURAL_OPTIMIZATION_RELEASE TRUE)
    ```
</v-clicks>

---
level: 3
hideInToc: true
---

# Manipulation des Targets (suite)
<v-clicks>

- `target_compile_option(<target> PRIVATE <option> ...)` :\
    Spécifie des option de compilation
    ```cmake
    target_compile_options(nanoteklib PRIVATE -Wextra -Wall -Wpedantic)
    ```
- `target_link_libraries(<target> [PUBLIC|PRIVATE|INTERFACE] <lib> ...)` :\
    Déclare au linker les library a rajouter
    ```cmake
    target_link_libraries(nanotekspice PRIVATE nanoteklib -lmath -lsfml)
    ```
</v-clicks>

---

# Les variables et le cache
<v-clicks>

- Définie une Variable Normale
    ```cmake
    set(<variable> <value>)
    ```
- Définie une Variable Cache
    ```cmake
    set(<variable> <value> CACHE <type> <docstring> [FORCE])
    ```
- Définie une Variable Environnement
    ```cmake
    set(ENV{<variable>} <value>)
    ```
</v-clicks>


<v-click>
<br/>

> Vos variables qui contiennent des listes peuvent être manipulé via la fonction `list`
</v-click>


---

# Les sous-dossiers

En utilisant cette architecture qualitative :
```
.
├── CMakeLists.txt          // CMake qui declare le projet
├── app
│   └── CMakeLists.txt      // CMake qui compile l’executable
├── src
│   ├── CMakeLists.txt      // CMake qui compile la librarie
│   └── components
│       └─ CMakeLists.txt   // CMake qui rajoute des source a la lib
└── tests
    └── CMakeLists.txt      // CMake qui compiler les test
```
On aurait : 
```cmake
project("NanoTekSpice"
        VERSION 1.0
        DESCRIPTION "EPITECH’s electronics simulation"
        LANGUAGES CXX)

add_subdirectory(app)
add_subdirectory(src)
enable_testing()
add_subdirectory(tests)
```

---

# Les Builds Type

- Debug
- Release
- MinSizeRel
- RelWithDebInfo

---

# Les tests CTest

- Activer les tests :
    ```cmake
    enable_testing()
    ```
- Ajouter un test avec :
    ```cmake
    add_test(NAME NoFileTest COMMAND $<TARGET_FILE:nanotekspice> WORKING_DIRECTORY ${CMAKE_SOURCE_DIR})
    ```
- Personaliser un test :
    ```cmake
    set_tests_properties(NoFileTest PROPERTIES
        PASS_REGULAR_EXPRESSION "Usage: nanotekspice FILENAME")
    ```
- Lancer (dans le build system) :
    ```sh
    ctest 
    make test
    ninja test
    ```

---

# Integration avec les IDEs

---

# À voir aussi

- Le scripting
- Les generator expressions
- Les presets et workflow

---
layout: end
---

# C'est tout le monde, les amis