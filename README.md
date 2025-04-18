# Sistema de Refrigerios para Call Center

Sistema para asignar refrigerios (descansos) a asesores de call center que trabajan en días especiales como fines de semana y feriados, dividido en campañas "IN" y "OUT".

## Descripción

Este proyecto implementa un sistema de asignación automática de refrigerios para asesores de call center, considerando dos campañas diferentes:

### Campaña "IN"
- Primer refrigerio: 10 minutos después de 2 horas de trabajo
- Segundo refrigerio: 20 minutos después de 4 horas de trabajo

### Campaña "OUT"
La duración del refrigerio depende de las horas trabajadas:
- 3 horas: 15 minutos de refrigerio
- 4 horas: 20 minutos de refrigerio
- 5 horas o más: 25 minutos de refrigerio

## Instalación

1. Clona este repositorio:
   ```
   git clone https://github.com/gabibenitezzz003/golang_refrigerios.git
   cd golang_refrigerios
   ```

2. Ejecuta el servidor:
   ```
   go run cmd/servidor/main.go
   ```

## Uso de la API

### Crear un turno y calcular refrigerios

**Endpoint:** `POST /api/turnos`

**Payload de ejemplo para Campaña IN:**
```json
{
  "persona": {
    "id": "E001",
    "nombre": "Juan Pérez",
    "campaña": "IN"
  },
  "inicio": "2023-11-25T08:00:00Z",
  "duración": 4
}
```

**Respuesta:**
```json
{
  "turno": {
    "persona": {
      "id": "E001",
      "nombre": "Juan Pérez",
      "campaña": "IN"
    },
    "inicio": "2023-11-25T08:00:00Z",
    "duración": 14400000000000
  },
  "refrigerios": [
    {
      "inicio": "2023-11-25T10:00:00Z",
      "duración": 600000000000
    },
    {
      "inicio": "2023-11-25T12:00:00Z",
      "duración": 1200000000000
    }
  ]
}
```

**Payload de ejemplo para Campaña OUT:**
```json
{
  "persona": {
    "id": "E002",
    "nombre": "María González",
    "campaña": "OUT"
  },
  "inicio": "2023-11-25T09:00:00Z",
  "duración": 5
}
```

### Listar todos los turnos

**Endpoint:** `GET /api/turnos/listar`

### Buscar turnos por ID de persona

**Endpoint:** `GET /api/turnos/persona/{id}`

## Estructura del Proyecto

El proyecto sigue los principios de Clean Architecture:

- `cmd/servidor`: Punto de entrada de la aplicación
- `pkg/dominio`: Entidades y reglas de negocio
- `pkg/aplicacion`: Casos de uso e implementación de la lógica
- `pkg/infraestructura`: Implementación de repositorios
- `pkg/manejador`: Controladores HTTP y API REST

## Tecnologías Utilizadas

- Go (Golang)
- API REST con el paquete estándar `net/http`
- JSON para serialización

## Autor

Gabriel Benítez 