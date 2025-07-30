# FEM Heat Equation 1D

Ce projet implémente une méthode des éléments finis (P1) pour résoudre l'équation de la chaleur en 1D.  
Le cœur du code est en C++17, construit avec CMake, et prévoit des extensions pour le parallélisme OpenMP/MPI et des bindings Python via `pybind11`.

---

## Objectifs

- Résolution numérique de l'équation de la chaleur en 1D
- Méthode des éléments finis linéaires (P1)
- Assemblage matriciel (Masse et Rigidité)
- Solveur implicite (Euler implicite)
- Préparation au parallélisme (OpenMP, MPI)
- Exposition du noyau en Python via `pybind11` (optionnel)

---

## Structure du projet

├── include/ # Headers C++
├── src/ # Fichiers sources C++
├── python/ # Bindings Python (pybind11)
├── tests/ # Tests unitaires (à venir)
├── CMakeLists.txt # Configuration du projet
└── README.md


---

## Compilation

### Prérequis

- Linux ou WSL
- [CMake ≥ 3.14](https://cmake.org/)
- [Eigen3](https://eigen.tuxfamily.org)
- Un compilateur C++17 (`g++`, `clang++`, etc.)

### Compilation minimale

```bash
git clone https://github.com/<TON_USER>/fem-heat-1d.git
cd fem-heat-1d
mkdir build && cd build
cmake ..
cmake --build .
./fem_main

