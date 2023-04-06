## Árbol Canónico

El orden de las hojas del árbol canónico correspondiente a su consulta cumple con el orden de las tablas dentro del **FROM**.

```sql
SELECT FROM R1, R2, R3 WHERE ...
```

```
   PROYECCIONES
        |
   SELECCIONES
        |
        X
       / \
      X   R3
     / \
   R1   R2
```

### Importante:
- Recostado sobre la izquierda
- El orden de las hojas de izquierda a derecha es el mismo orden del **FROM** de la consulta


## Optimización Heurística
Construir el **Plan Lógico** partiendo del Árbol Canónico:
1. Cambiar las selecciones conjuntivas por una *cascada* de selecciones simples.
2. Mover las selecciones lo más abajo posible.
3. Poner a la izquierda de los productos las hojas que generen menos tuplas, asegurando que el orden de las hojas no generen nuevos productos cartesianos.
4. Cambiar secuencias de selección y productos por *join's*
5. Mover las proyecciones lo más abajo posible.

##TODO