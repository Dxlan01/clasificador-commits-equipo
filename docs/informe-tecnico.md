# Informe Técnico — Clasificador de Commits

## Caracterización del modelo local (Semana 1)

| Dato | Valor |
|---|---|
| Perfil de hardware | Perfil C (4 GB RAM asignados a WSL2, disco HDD) |
| RAM total del equipo | 1.9 GiB disponibles en WSL2 (8 GB físicos del equipo, limitados por .wslconfig) |
| Modelo y etiqueta | gemma3:270m |
| Tamaño en disco | 291 MB |
| Latencia ejecución 1 | 5510 ms |
| Latencia ejecución 2 | 5302 ms |
| Latencia ejecución 3 | 5487 ms |
| Latencia ejecución 4 | 5763 ms |
| Latencia ejecución 5 | 5762 ms |
| Latencia promedio | 5565 ms |
| RAM usada durante la inferencia | ~488 MB de 1.9 GiB disponibles |
| Calidad percibida (1 a 5) | 4 — el modelo respondió correctamente y de forma coherente a saludos simples, aunque es un modelo pequeño con capacidad limitada para tareas complejas |
