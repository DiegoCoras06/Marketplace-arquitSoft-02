## Arquitectura Inicial

```text
┌────────────────────────────────────┐
│           PRESENTACIÓN             │
│                                    │
│       Web / API / Interfaz         │
└─────────────────┬──────────────────┘
                  │
                  ▼
┌────────────────────────────────────┐
│          LÓGICA DE NEGOCIO         │
│                                    │
│  Catálogo                          │
│  Carrito                           │
│  Pedidos                           │
│  Sellers                           │
│  Usuarios                          │
└─────────────────┬──────────────────┘
                  │
                  ▼
┌────────────────────────────────────┐
│                DATOS               │
│                                    │
│            Base de datos           │
└────────────────────────────────────┘


# Arquitectura Inicial del Sistema

## Diagrama de Arquitectura

```mermaid
flowchart TD

%% ========================================
%% ACTORES
%% ========================================
subgraph ACTORES["ACTORES"]
    Cliente["Cliente"]
    Seller["Seller"]
    Admin["Administrador"]
end

%% ========================================
%% PRESENTACIÓN
%% ========================================
subgraph PRESENTACION["CAPA DE PRESENTACIÓN"]
    Web["Aplicación Web"]
    API["API REST"]
end

%% ========================================
%% LÓGICA DE NEGOCIO
%% ========================================
subgraph NEGOCIO["CAPA DE LÓGICA DE NEGOCIO"]
    Usuarios["Gestión de Usuarios"]
    Productos["Gestión de Productos"]
    Carrito["Gestión del Carrito"]
    Pedidos["Gestión de Pedidos"]
end

%% ========================================
%% DATOS
%% ========================================
subgraph DATOS["CAPA DE DATOS"]
    BD["Base de Datos"]
end

%% ========================================
%% SISTEMAS EXTERNOS
%% ========================================
subgraph EXTERNOS["SISTEMAS EXTERNOS"]
    Pago["Pasarela de Pago"]
    Facturacion["Servicio de Facturación"]
    Envio["Servicio de Envío"]
    ERP["ERP"]
end

%% ========================================
%% ACTORES → PRESENTACIÓN
%% ========================================
Cliente --> Web
Seller --> Web
Admin --> Web

%% ========================================
%% PRESENTACIÓN
%% ========================================
Web --> API

%% ========================================
%% API → LÓGICA DE NEGOCIO
%% ========================================
API --> Usuarios
API --> Productos
API --> Carrito
API --> Pedidos

%% ========================================
%% LÓGICA DE NEGOCIO → DATOS
%% ========================================
Usuarios --> BD
Productos --> BD
Carrito --> BD
Pedidos --> BD

%% ========================================
%% INTEGRACIONES EXTERNAS
%% ========================================
Pedidos --> Pago
Pedidos --> Facturacion
Pedidos --> Envio
Productos --> ERP

%% ========================================
%% ESTILOS
%% ========================================
style ACTORES fill:#1f2937,stroke:#ffffff,stroke-width:2px,color:#ffffff
style PRESENTACION fill:#1f2937,stroke:#ffffff,stroke-width:2px,color:#ffffff
style NEGOCIO fill:#1f2937,stroke:#ffffff,stroke-width:2px,color:#ffffff
style DATOS fill:#1f2937,stroke:#ffffff,stroke-width:2px,color:#ffffff
style EXTERNOS fill:#1f2937,stroke:#ffffff,stroke-width:2px,color:#ffffff

style Cliente fill:#374151,stroke:#ffffff,color:#ffffff
style Seller fill:#374151,stroke:#ffffff,color:#ffffff
style Admin fill:#374151,stroke:#ffffff,color:#ffffff

style Web fill:#374151,stroke:#ffffff,color:#ffffff
style API fill:#374151,stroke:#ffffff,color:#ffffff

style Usuarios fill:#374151,stroke:#ffffff,color:#ffffff
style Productos fill:#374151,stroke:#ffffff,color:#ffffff
style Carrito fill:#374151,stroke:#ffffff,color:#ffffff
style Pedidos fill:#374151,stroke:#ffffff,color:#ffffff

style BD fill:#374151,stroke:#ffffff,color:#ffffff

style Pago fill:#374151,stroke:#ffffff,color:#ffffff
style Facturacion fill:#374151,stroke:#ffffff,color:#ffffff
style Envio fill:#374151,stroke:#ffffff,color:#ffffff
style ERP fill:#374151,stroke:#ffffff,color:#ffffff
```

## Descripción de la Arquitectura

La arquitectura inicial del Marketplace se organiza en **tres capas principales**: presentación, lógica de negocio y datos. Además, se consideran los actores que interactúan con el sistema y los sistemas externos necesarios para complementar sus funcionalidades.

### 1. Actores

Los principales actores que interactúan con el Marketplace son:

- **Cliente:** busca productos, consulta información, gestiona su carrito y realiza pedidos.
- **Seller:** registra y gestiona los productos que ofrece en la plataforma.
- **Administrador:** administra y supervisa la plataforma.

### 2. Capa de Presentación

La capa de presentación está conformada por la **Aplicación Web**, mediante la cual los actores interactúan con el Marketplace.

La aplicación se comunica con la lógica de negocio mediante una **API REST**, permitiendo intercambiar información entre el frontend y el backend.

### 3. Capa de Lógica de Negocio

Esta capa contiene las principales funcionalidades del Marketplace:

- **Gestión de Usuarios:** administra la información de los usuarios.
- **Gestión de Productos:** permite registrar, actualizar y consultar productos.
- **Gestión del Carrito:** permite agregar, modificar y eliminar productos del carrito.
- **Gestión de Pedidos:** permite generar y consultar los pedidos realizados.

### 4. Capa de Datos

La capa de datos está representada por una **Base de Datos**, donde se almacena la información necesaria para el funcionamiento del sistema.

Entre los principales datos almacenados se encuentran:

- Usuarios.
- Sellers.
- Productos.
- Carritos.
- Pedidos.

### 5. Sistemas Externos

El Marketplace requiere integrarse con diferentes sistemas externos:

| Sistema externo | Función |
|---|---|
| **Pasarela de Pago** | Procesar los pagos realizados por los clientes. |
| **Servicio de Facturación** | Generar los comprobantes correspondientes a las compras. |
| **Servicio de Envío** | Gestionar la información relacionada con la entrega de los pedidos. |
| **ERP** | Proporcionar información de productos y disponibilidad de stock. |

Estas integraciones se realizan mediante mecanismos de comunicación basados en **API REST**.

## Flujo General

El flujo principal del sistema es:

```text
Cliente / Seller / Administrador
              │
              ▼
       Aplicación Web
              │
              ▼
           API REST
              │
              ▼
      Lógica de Negocio
       │      │      │
       │      │      └── Gestión de Pedidos
       │      └───────── Gestión del Carrito
       └──────────────── Gestión de Productos
              │
              ▼
        Base de Datos

Gestión de Pedidos ────► Pasarela de Pago
          │
          ├────────────► Servicio de Facturación
          │
          └────────────► Servicio de Envío

Gestión de Productos ──► ERP
```

## Relación con los Drivers Arquitectónicos

| Driver | Consideración arquitectónica |
|---|---|
| **DA01 – Escalabilidad** | La separación de responsabilidades permite evolucionar y escalar los componentes del sistema. |
| **DA02 – Rendimiento** | La separación entre presentación, negocio y datos facilita la optimización del procesamiento y acceso a la información. |
| **DA03 – Seguridad** | La API REST y la lógica de negocio pueden incorporar mecanismos de autenticación y autorización. |
| **DA04 – Pasarela de Pago** | Se contempla una integración independiente con una pasarela de pago externa. |
| **DA05 – API REST** | La comunicación entre la aplicación web y la lógica de negocio se realiza mediante una API REST. |

## Tipo de Arquitectura

La propuesta corresponde inicialmente a una **arquitectura en capas**, utilizada como punto de partida para organizar las responsabilidades del Marketplace.

Esta arquitectura podrá evolucionar posteriormente de acuerdo con los requisitos funcionales, atributos de calidad, restricciones y necesidades de integración identificadas en el proyecto.



## Descripción

La arquitectura inicial del Marketplace se organiza en **tres capas principales**: presentación, lógica de negocio y datos. Esta estructura permite separar las responsabilidades principales del sistema y establecer una base para la evolución de la arquitectura.

### 1. Presentación

La capa de **Presentación** proporciona el punto de interacción entre los actores y el sistema mediante una **aplicación web**, utilizando una **API REST** para la comunicación con los componentes de negocio.

Los principales actores son:

* **Cliente:** consulta productos, gestiona su carrito y realiza pedidos.
* **Seller:** registra y gestiona sus productos.
* **Administrador:** administra la plataforma.

### 2. Lógica de Negocio

La capa de **Lógica de Negocio** contiene los módulos principales del Marketplace:

* **Usuarios:** gestiona la información y operaciones relacionadas con los usuarios.
* **Sellers:** gestiona la información de los vendedores y sus productos.
* **Catálogo:** permite consultar productos y su disponibilidad.
* **Carrito:** gestiona los productos seleccionados por el cliente.
* **Pedidos:** permite generar y consultar los pedidos realizados.

### 3. Datos

La capa de **Datos** está conformada por una **base de datos**, encargada de almacenar la información relacionada con usuarios, sellers, productos, carritos y pedidos.

### 4. Sistemas Externos

La arquitectura considera la integración con servicios externos:

* **Pasarela de pago:** procesa los pagos asociados a los pedidos.
* **Servicio de facturación:** genera los comprobantes de pago.
* **Servicio de envío:** gestiona la información relacionada con la entrega de los pedidos.
* **ERP:** proporciona información relacionada con productos y disponibilidad de stock.

Estas integraciones permiten que el Marketplace delegue funcionalidades especializadas a sistemas externos mediante mecanismos de comunicación basados en **API REST**.

## Flujo General

El flujo principal de la arquitectura es:

```text
Actores
   │
   ▼
Presentación
(Web / API REST)
   │
   ▼
Lógica de Negocio
   │
   ├── Usuarios
   ├── Sellers
   ├── Catálogo
   ├── Carrito
   └── Pedidos
          │
          ▼
      Base de Datos

Pedidos ──────► Pasarela de pago
Pedidos ──────► Facturación
Pedidos ──────► Servicio de envío
Catálogo ─────► ERP
```

## Relación con los Drivers Arquitectónicos

La arquitectura inicial considera los principales drivers identificados durante el análisis:

| Driver                      | Consideración arquitectónica                                                                                  |
| --------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **DA01 – Escalabilidad**    | La separación de responsabilidades permite evolucionar y escalar los componentes del sistema.                 |
| **DA02 – Rendimiento**      | La separación entre presentación, negocio y datos facilita optimizar el procesamiento y acceso a información. |
| **DA03 – Seguridad**        | La API y la capa de negocio pueden incorporar mecanismos de autenticación y autorización.                     |
| **DA04 – Pasarela de pago** | Se contempla una integración independiente con la pasarela de pago externa.                                   |
| **DA05 – API REST**         | La comunicación entre la aplicación web y la lógica del sistema se establece mediante API REST.               |

## Tipo de Arquitectura

La propuesta corresponde inicialmente a una **arquitectura en capas**, utilizada como punto de partida para organizar las responsabilidades del Marketplace.

Esta arquitectura podrá evolucionar posteriormente de acuerdo con los requisitos funcionales, atributos de calidad, restricciones y necesidades de integración identificadas en el proyecto.
