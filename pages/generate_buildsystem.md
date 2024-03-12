---
level: 2
---

# Générer son buildsystem
<v-clicks>

* Dans le terminal à la racine du projet :
````md magic-move
```sh
cmake .
```
```sh
cmake -S .
```
```sh
cmake -S . -B build
```
````
* Compiler le projet:
```sh
cmake --build build
```

* Lancer l’executable
```sh
./build/nanotekspice Circuit.nts
```
</v-clicks>