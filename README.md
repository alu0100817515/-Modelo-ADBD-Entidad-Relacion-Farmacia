# Modelo ADBD. Entidad-Relación. Farmacia

## Miembros
1. Laura Álvarez Zamora **alu0101349824@ull.edu.es**
2. Pablo Fernández Herrera **alu0100817515@ull.edu.es**
---
## Descripción de las Entidades

### 1. **Medicamento**
- **Descripción**: Representa los productos farmacéuticos disponibles en la farmacia.
- **Atributos**:
  - **Código**: Identificador único del medicamento. Ejemplo: "MED001".
  - **Nombre**: Nombre del medicamento. Ejemplo: "Paracetamol".
  - **Tipo**: Tipo de medicamento (jarabe, comprimido, pomada, etc.). Ejemplo: "Comprimido".
  - **Unidades**: Cantidad de unidades en stock. Ejemplo: "50".
  - **Vendidas**: Unidades vendidas. Ejemplo: "30".
  - **Stock**: Unidades disponibles en stock. Ejemplo: "20".
  - **Precio**: Precio por unidad del medicamento. Ejemplo: "5.99".
  - **Receta**: Indica si el medicamento requiere receta para ser dispensado. Valores posibles: "Libre" o "Receta".

### 2. **Pedido**
- **Descripción**: Registra las compras realizadas por los clientes en la farmacia.
- **Atributos**:
  - **Fecha de compra del medicamento**: Fecha en la que se realizó el pedido. Ejemplo: "15-01-2024".
  - **Unidades compradas**: Cantidad de unidades compradas en el pedido. Ejemplo: "2".
  - **Código del pedido**: Código único del pedido relacionado con el medicamento. Ejemplo: "PED001".
  - **Medicamento comprado**: Nombre del medicamento. Ejemplo: "Paracetamol".

### 3. **Con crédito**
- **Descripción**: Representa a los clientes de la farmacia que realizan los pagos de sus pedidos a fin de cada mes. 
- **Atributos**:
  - **Datos bancarios**: Información bancaria para clientes con crédito. Ejemplo: "IBAN: ES91 2100 0418 4502 0005 1332".
  - **Fecha de Pago**: Fecha en la que se realiza el pago por parte del cliente. Ejemplo: "15-01-2024".
    
### 4. **Sin crédito**
- **Descripción**: Representa a los clientes de la farmacia que realizan los pagos sin crédito.

### 5. **Familia**
- **Descripción**: Categoriza los medicamentos según el tipo de enfermedad para la cual son aplicables.
- **Atributos**:
  - **Código**: Identificador único de la familia. Ejemplo: "FAM001".
  - **Nombre**: Nombre de la familia. Ejemplo: "Analgésicos".
  - **Enfermedad sobre la que aplica**: Tipo de enfermedad para la cual los medicamentos de esta familia son relevantes. Ejemplo: "Dolor de cabeza".

### 6. **Laboratorio**
- **Descripción**: Proveedor de los medicamentos.
- **Atributos**:
  - **Código**: Identificador único del laboratorio. Ejemplo: "LAB001".
  - **Nombre**: Nombre del laboratorio. Ejemplo: "Laboratorios Pharma".
  - **Dirección Postal**: Dirección física del laboratorio. Ejemplo: "Calle Mayor, 123".
  - **Persona de Contacto**: Nombre de la persona a contactar en el laboratorio. Ejemplo: "Juan Expósito".
  - **Teléfono**: Número de teléfono de contacto. Ejemplo: "+34 123 456 789".
  - **Fax**: Número de fax del laboratorio. Ejemplo: "+34 987 654 321".

### 7. **Farmacia**
- **Descripción**: Representa la farmacia que fabrica los medicamentos.
- **Atributos**:
  - **Medicamento fabricado**: Nombre del medicamento. Ejemplo: "Paracetamol".

## Descripción de las Relaciones

### 1. **Pedido - Medicamento (Incluye)**
- **Cardinalidad**: N:1 desde "Pedido" a "Medicamento" y N:1 desde "Medicamento" a "Pedido".
- **Descripción**: Un pedido puede incluir múltiples medicamentos, y un medicamento puede estar en varios pedidos.
- **Ejemplo**: Un pedido realizado el "15-01-2024" incluye "2 unidades" del medicamento "Paracetamol".

### 2. **Medicamento - Familia (Agrupan)**
- **Cardinalidad**: N:1 desde "Medicamento" a "Familia" y 1:1 desde "Familia" a "Medicamento".
- **Descripción**: Un medicamento pertenece a una única familia, mientras que una familia puede agrupar varios medicamentos.
- **Ejemplo**: El medicamento "Paracetamol" pertenece a la familia "Analgésicos".

### 3. **Medicamento - Medicamento (Reemplaza)**
- **Cardinalidad**: 1:1 desde "Medicamento" a "Medicamento" y 1:1 desde "Medicamento" a "Medicamento".
- **Descripción**: Un medicamento puede ser reemplazado por otro similar si no está disponible.
- **Restricción Semántica**: Si la farmacia no dispone de un medicamento concreto, puede vender otro similar aunque de distinto laboratorio.
- **Ejemplo**: Si el "Paracetamol" no está disponible, puede ser reemplazado por "Ibuprofeno".

### 4. **Farmacia - Medicamento (Fabrica)**
- **Cardinalidad**: 1:1 desde "Farmacia" a "Medicamento" y 0:N desde "Medicamento" a "Farmacia".
- **Descripción**: Cada farmacia puede fabricar uno o más medicamentos, mientras que un medicamento puede ser fabricado por una única farmacia o por ninguna (si se adquiere de un laboratorio).
- **Ejemplo**: La "Farmacia Central" fabrica el medicamento "Paracetamol".

### 5. **Laboratorio - Medicamento (Compra)**
- **Cardinalidad**: 1:1 desde "Laboratorio" a "Medicamento" y 0:N desde "Medicamento" a "Laboratorio".
- **Descripción**: La farmacia puede comprar varios o ningún medicamento a un laboratorio, mientras que un laboratorio puede vender un medicamento a la farmacia.
- **Ejemplo**: "Laboratorios Pharma" vende "Paracetamol" y "Ibuprofeno".

### 6. **Pedido - Forma de Pago**
- **Cardinalidad**: 1:1 desde "Pedido" a "Forma de Pago" y 0:1 desde "Forma de Pago" a "Pedido".
- **Descripción**: Cada pedido tiene una única forma de pago.
- **Ejemplo**: El pedido realizado el "15-01-2024" se pagó "con crédito".
- **Atributos**:
  - **Forma de Pago**: Cada pedido tiene una única forma de pago, que puede ser "Con crédito" o "Sin crédito". 

## Restricciones Semánticas

- **Reemplazo de Medicamentos**: Si la farmacia no dispone de un medicamento concreto, puede vender otro similar, aunque de distinto laboratorio, siempre que pertenezcan a la misma familia.
- **Nombre de Contacto del Laboratorio**: Solo habrá un nombre de contacto por laboratorio.
