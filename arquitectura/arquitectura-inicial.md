# Arquitectura inicial del sistema

## Arquitectura en tres capas

La arquitectura inicial de la plataforma se organiza en tres capas principales: presentación, lógica de negocio y datos.

| Capa | Pregunta que responde | Elementos |
|---|---|---|
| Presentación | ¿Cómo interactúa el usuario? | Aplicación Web y API REST |
| Lógica de negocio | ¿Qué hace el sistema? | Usuarios, Prestadores, Servicios, Solicitudes, Propuestas y Contrataciones |
| Datos | ¿Dónde se almacena la información? | Base de datos |

## Diagrama de arquitectura

mermaid
flowchart TD

%% =========================
%% ACTORES
%% =========================
subgraph ACTORES["ACTORES"]
    Cliente["Cliente"]
    Prestador["Prestador de servicios"]
    Admin["Administrador"]
end

%% =========================
%% PRESENTACIÓN
%% =========================
subgraph PRESENTACION["PRESENTACIÓN"]
    Web["Aplicación Web → API REST"]
end

%% =========================
%% LÓGICA DE NEGOCIO
%% =========================
subgraph NEGOCIO["LÓGICA DE NEGOCIO"]
    Usuarios["Usuarios"]
    Prestadores["Prestadores"]
    Servicios["Servicios"]
    Solicitudes["Solicitudes"]
    Propuestas["Propuestas"]
    Contrataciones["Contrataciones"]
end

%% =========================
%% DATOS
%% =========================
subgraph DATOS["DATOS"]
    BD["Base de datos"]
end

%% =========================
%% SISTEMAS EXTERNOS
%% =========================
subgraph EXTERNOS["SISTEMAS EXTERNOS"]
    Pago["Pasarela de pago"]
    Notificaciones["Servicio de notificaciones"]
    Ubicacion["Servicio de ubicación"]
end

%% =========================
%% FLUJO PRINCIPAL
%% =========================
ACTORES --> PRESENTACION
PRESENTACION --> NEGOCIO
NEGOCIO --> DATOS

%% Integraciones externas
NEGOCIO --> EXTERNOS

%% =========================
%% DISTRIBUCIÓN HORIZONTAL
%% =========================
Cliente ~~~ Prestador
Prestador ~~~ Admin

Usuarios ~~~ Prestadores
Prestadores ~~~ Servicios
Servicios ~~~ Solicitudes
Solicitudes ~~~ Propuestas
Propuestas ~~~ Contrataciones

Pago ~~~ Notificaciones
Notificaciones ~~~ Ubicacion

%% =========================
%% ESTILOS
%% =========================
style ACTORES fill:#222,stroke:#fff,stroke-width:2px,color:#fff
style PRESENTACION fill:#222,stroke:#fff,stroke-width:2px,color:#fff
style NEGOCIO fill:#222,stroke:#fff,stroke-width:2px,color:#fff
style DATOS fill:#222,stroke:#fff,stroke-width:2px,color:#fff
style EXTERNOS fill:#222,stroke:#fff,stroke-width:2px,color:#fff

style Cliente fill:#222,stroke:#fff,color:#fff
style Prestador fill:#222,stroke:#fff,color:#fff
style Admin fill:#222,stroke:#fff,color:#fff
style Web fill:#222,stroke:#fff,color:#fff

style Usuarios fill:#222,stroke:#fff,color:#fff
style Prestadores fill:#222,stroke:#fff,color:#fff
style Servicios fill:#222,stroke:#fff,color:#fff
style Solicitudes fill:#222,stroke:#fff,color:#fff
style Propuestas fill:#222,stroke:#fff,color:#fff
style Contrataciones fill:#222,stroke:#fff,color:#fff

style BD fill:#222,stroke:#fff,color:#fff

style Pago fill:#222,stroke:#fff,color:#fff
style Notificaciones fill:#222,stroke:#fff,color:#fff
style Ubicacion fill:#222,stroke:#fff,color:#fff


## Descripción

La arquitectura inicial se organiza en tres capas principales:

- *Presentación:* permite la interacción del cliente, prestador de servicios y administrador con el sistema mediante la aplicación web y la API REST.
- *Lógica de negocio:* contiene los módulos principales de usuarios, prestadores, servicios, solicitudes, propuestas y contrataciones.
- *Datos:* almacena y permite consultar la información de la plataforma mediante una base de datos.

Además, la lógica de negocio se integra con sistemas externos como la pasarela de pago, el servicio de notificaciones y el servicio de ubicación.