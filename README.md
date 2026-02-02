# Ejercicio 1: Búsqueda en Anchura (Breadth-First Search)

## 📌 Descripción del Problema
Este ejercicio consiste en encontrar el camino más corto en un entorno de rejilla (grid) desde una posición inicial **i** hasta un objetivo **e**. El agente (NPC) puede moverse en cuatro direcciones (horizontal y vertical) con un coste unitario por movimiento, evitando las zonas bloqueadas (obstáculos).

### Detalles del Entorno:
- **Estado Inicial (i):** Celda E5.
- **Estado Objetivo (e):** Celda D2.
- **Algoritmo Aplicado:** Búsqueda en Anchura (BFS).
- **Orden de Expansión:** Arriba, Abajo, Izquierda, Derecha.

---

## ⚙️ Metodología y Traza de Ejecución
Se ha utilizado una **cola (FIFO)** para gestionar la frontera, lo que garantiza que el camino encontrado sea el óptimo en cuanto a número de pasos. A continuación, se detalla la evolución de los conjuntos de nodos durante la búsqueda:

| Paso | Nodo Expandido (Padre) | Exploradas (Nodo(Padre)) | Fronteras / Cola (Nodo(Padre)) |
| :--- | :--- | :--- | :--- |
| 0 | - | - | $i (-)$ |
| 1 | **$i (-)$** | $i (-)$ | $A(i), B(i)$ |
| 2 | **$A (i)$** | $i, A(i)$ | $B(i), C(A), D(A)$ |
| 3 | **$B (i)$** | $i, A, B(i)$ | $C(A), D(A), E(B), F(B)$ |
| 4 | **$C (A)$** | $i, A, B, C(A)$ | $D(A), E(B), F(B)$ |
| 5 | **$D (A)$** | $i, A, B, C, D(A)$ | $E(B), F(B), G(D)$ |
| 6 | **$E (B)$** | $i, A, B, C, D, E(B)$ | $F(B), G(D), H(E)$ |
| 7 | **$F (B)$** | $i, A, B, C, D, E, F(B)$ | $G(D), H(E)$ |
| 8 | **$G (D)$** | $i, \dots, G(D)$ | $H(E), I(G)$ |
| 9 | **$H (E)$** | $i, \dots, H(E)$ | $I(G), L(H), M(H)$ |
| 10 | **$I (G)$** | $i, \dots, I(G)$ | $L(H), M(H), K(I), J(I)$ |
| 11 | **$L (H)$** | $i, \dots, L(H)$ | $M(H), K(I), J(I), O(L)$ |
| 12 | **$M (H)$** | $i, \dots, M(H)$ | $K(I), J(I), O(L)$ |
| 13 | **$K (I)$** | $i, \dots, K(I)$ | $J(I), O(L), N(K)$ |
| 14 | **$J (I)$** | $i, \dots, J(I)$ | $O(L), N(K), \mathbf{e(J)}$ |

---

## 🌳 Árbol de Búsqueda Visual
El siguiente diagrama representa la jerarquía de exploración. La línea resaltada en verde indica el camino solución reconstruido a través de los nodos padres.

```mermaid
graph TD
    i((i)) --> A((A))
    i((i)) --> B((B))
    A --> C((C))
    A --> D((D))
    B --> E((E))
    B --> F((F))
    D --> G((G))
    E --> H((H))
    G --> I((I))
    H --> L((L))
    H --> M((M))
    I --> K((K))
    I --> J((J))
    L --> O((O))
    K --> N((N))
    J --> e((e))

    %% Estilo del camino solución
    linkStyle 0,3,6,8,12,15 stroke:#2ecc71,stroke-width:4px
    style i fill:#2ecc71,stroke:#333
    style A fill:#2ecc71,stroke:#333
    style D fill:#2ecc71,stroke:#333
    style G fill:#2ecc71,stroke:#333
    style I fill:#2ecc71,stroke:#333
    style J fill:#2ecc71,stroke:#333
    style e fill:#f1c40f,stroke:#333,stroke-width:3px