# Idea de API: Sistema de Gestión de Restaurante (Consumo en Local)

## 1. Visión General

La aplicación tiene como objetivo gestionar de manera integral la operación de un restaurante enfocado **exclusivamente en consumo en el local**, cubriendo el manejo del **menú**, la **toma y seguimiento de órdenes**, y el **estado de las mesas**, optimizando la experiencia tanto del personal como del cliente.

El sistema busca reducir errores operativos, mejorar los tiempos de atención y ofrecer información clara y en tiempo real sobre lo que ocurre en el restaurante.

---

## 2. Problema que se Desea Resolver

- Toma manual de pedidos propensa a errores.
- Falta de visibilidad del estado de las órdenes (pendiente, en preparación, servida).
- Dificultad para actualizar el menú (precios, disponibilidad).
- Escasa trazabilidad de lo que se ordena por mesa.

---

## 3. Alcance del Sistema

**Incluye:**

- Gestión del menú.
- Gestión de mesas.
- Creación y seguimiento de órdenes para consumo en el local.
- Control del estado de las órdenes.

**No incluye (por ahora):**

- Domicilios.
- Pagos en línea.
- Gestión contable o facturación electrónica.

---

## 4. Funcionalidades Principales

### 4.1 Gestión del Menú

- Crear, editar y eliminar categorías (ej. Entradas, Platos fuertes, Bebidas).
- Crear, editar y desactivar productos del menú.
- Definir precio y disponibilidad de cada producto.

### 4.2 Gestión de Mesas

- Registrar mesas del restaurante.
- Definir capacidad por mesa.
- Consultar estado de la mesa: **Libre, Ocupada, En atención**.

### 4.3 Gestión de Órdenes

- Crear una orden asociada a una mesa.
- Agregar uno o varios productos a la orden.
- Modificar la orden mientras esté abierta.
- Cambiar el estado de la orden:
  - Creada
  - En preparación
  - Servida
  - Cerrada

### 4.4 Seguimiento Operativo

- Visualizar órdenes activas por mesa.
- Ver detalle de productos solicitados.
- Controlar el flujo de atención en tiempo real.

---

## 5. Criterios de Aceptación (Ejemplos)

### Historia: Crear una Orden

**Dado** que existe una mesa registrada y libre
**Cuando** el mesero crea una nueva orden
**Entonces** la orden debe quedar asociada a la mesa
**Y** su estado inicial debe ser "Creada"

---

### Historia: Agregar Producto a la Orden

**Dado** que una orden está en estado "Creada"
**Cuando** se agrega un producto disponible del menú
**Entonces** el producto debe reflejarse en el detalle de la orden
**Y** debe recalcularse el total de la orden

---

### Historia: Cambiar Estado de Orden

**Dado** que una orden existe
**Cuando** se cambia su estado a "En preparación"
**Entonces** el sistema debe registrar la transición de estado
**Y** la orden no debe poder eliminarse

---

## 6. Roles del Sistema

- **Administrador**: gestiona menú y mesas.
- **Mesero**: crea y gestiona órdenes.
- **Cocina** (opcional): visualiza órdenes en preparación.

---

## 7. Lenguaje Ubicuo (Lenguaje Oblicuo del Dominio)

| Término          | Descripción                                                     |
| ---------------- | --------------------------------------------------------------- |
| Menú             | Conjunto de categorías y productos ofrecidos por el restaurante |
| Producto         | Ítem disponible para ser ordenado                               |
| Categoría        | Agrupación lógica de productos                                  |
| Mesa             | Espacio físico donde se atienden clientes                       |
| Orden            | Solicitud de productos asociada a una mesa                      |
| Detalle de Orden | Conjunto de productos dentro de una orden                       |
| Estado de Orden  | Situación actual de la orden dentro del flujo                   |
| Orden Abierta    | Orden que aún admite cambios                                    |
| Orden Cerrada    | Orden finalizada y no editable                                  |

---

## 8. Posible Modelo de Dominio (Conceptual)

- **Menú** → contiene **Categorías**
- **Categoría** → contiene **Productos**
- **Mesa** → tiene cero o una **Orden activa**
- **Orden** → contiene **Detalles de Orden**
- **Detalle de Orden** → referencia un **Producto**

---

## 9. Evolución Futura

- Integración con pagos.
- Reportes de ventas.
- Control de inventario.
- Módulo de cocina en tiempo real.

---

## 10. Conclusión

Esta aplicación sienta las bases para un sistema de gestión de restaurante centrado en el flujo real de atención en el local, utilizando un lenguaje común entre negocio y desarrollo, facilitando la escalabilidad y el mantenimiento del sistema.
