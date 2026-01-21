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

## 9. Historias de Usuario (Listas para Jira / Trello)

### EPIC: Gestión del Menú

**HU-01 – Crear categoría de menú**
Como **Administrador**
Quiero **crear una categoría de menú**
Para **organizar los productos ofrecidos por el restaurante**

**Criterios de aceptación:**

- Dado que estoy autenticado como administrador
- Cuando registro una nueva categoría con nombre válido
- Entonces la categoría debe quedar disponible en el menú

---

**HU-02 – Crear producto del menú**
Como **Administrador**
Quiero **registrar un producto en una categoría**
Para **ofrecerlo a los clientes**

**Criterios de aceptación:**

- Dado que existe una categoría
- Cuando registro un producto con nombre, precio y disponibilidad
- Entonces el producto debe aparecer en el menú

---

### EPIC: Gestión de Mesas

**HU-03 – Registrar mesa**
Como **Administrador**
Quiero **registrar mesas del restaurante**
Para **controlar la ocupación del local**

**Criterios de aceptación:**

- Dado que soy administrador
- Cuando registro una mesa con número y capacidad
- Entonces la mesa debe quedar disponible con estado "Libre"

---

**HU-04 – Consultar estado de mesa**
Como **Mesero**
Quiero **ver el estado de las mesas**
Para **saber cuáles están disponibles**

**Criterios de aceptación:**

- Dado que existen mesas registradas
- Cuando consulto el listado
- Entonces debo ver su estado actual

---

### EPIC: Gestión de Órdenes

**HU-05 – Crear orden por mesa**
Como **Mesero**
Quiero **crear una orden asociada a una mesa**
Para **registrar el pedido de los clientes**

**Criterios de aceptación:**

- Dado que una mesa está libre
- Cuando creo una orden
- Entonces la mesa pasa a estado "Ocupada"
- Y la orden queda en estado "Creada"

---

**HU-06 – Agregar producto a la orden**
Como **Mesero**
Quiero **agregar productos a una orden abierta**
Para **registrar completamente el pedido**

**Criterios de aceptación:**

- Dado que la orden está en estado "Creada"
- Cuando agrego un producto disponible
- Entonces el producto debe reflejarse en el detalle de la orden

---

**HU-07 – Modificar orden**
Como **Mesero**
Quiero **modificar una orden abierta**
Para **ajustar cambios solicitados por el cliente**

**Criterios de aceptación:**

- Dado que la orden está abierta
- Cuando elimino o agrego productos
- Entonces el total de la orden debe recalcularse

---

**HU-08 – Cambiar estado de la orden**
Como **Cocina o Mesero**
Quiero **actualizar el estado de la orden**
Para **reflejar el avance del pedido**

**Criterios de aceptación:**

- Dado que la orden existe
- Cuando se cambia a "En preparación" o "Servida"
- Entonces el nuevo estado debe guardarse correctamente

---

**HU-09 – Cerrar orden**
Como **Mesero**
Quiero **cerrar la orden**
Para **finalizar la atención de la mesa**

**Criterios de aceptación:**

- Dado que la orden está servida
- Cuando la cierro
- Entonces la orden queda no editable
- Y la mesa pasa a estado "Libre"

---

## 10. Evolución Futura

- Integración con pagos.
- Reportes de ventas.
- Control de inventario.
- Módulo de cocina en tiempo real.

---

## 10. Conclusión

Esta aplicación sienta las bases para un sistema de gestión de restaurante centrado en el flujo real de atención en el local, utilizando un lenguaje común entre negocio y desarrollo, facilitando la escalabilidad y el mantenimiento del sistema.
