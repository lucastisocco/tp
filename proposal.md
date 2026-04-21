# Propuesta TP DSW 2026 - COM 305 - GesThor

## Grupo
### Integrantes
* 43187 - Tisocco, Lucas Maximiliano
* legajo - Apellido(s), Nombre(s)
* legajo - Apellido(s), Nombre(s)
* legajo - Apellido(s), Nombre(s)

### Repositorios
* [frontend app](http://hyperlinkToGihubOrGitlab)
* [backend app](http://hyperlinkToGihubOrGitlab)

## Tema
### Descripción
Sistema de gestión de recursos humanos orientado al control de horas laborales. Permite a empleados registrar sus horas trabajadas asociadas a proyectos de clientes, mientras que el área de RRHH administra empleados, clientes y proyectos, verifica la carga horaria y gestiona la asignación de personal a cada proyecto.

### Modelo

```mermaid
erDiagram
    EMPLEADO {
        int id PK
        string dni
        string nomyape
        date fecha_nac
        string categoria
        string num_tel
        string rol
        string user
        string pass
    }
    CLIENTE {
        int id_cliente PK
        string razon_social
        string cuit
        string tel
        string mail
    }
    PROYECTO {
        int id_proyecto PK
        string nombre_proyecto
        int proyecto_horas
        date fecha_ini_proy
        date fecha_fin_proy
    }
    REGISTRO_HORAS {
        int id_registro PK
        string desc_tareas
        float cant_horas_trab
        date fecha
    }
    ASIGNACION {
        int id_asignacion PK
        date fecha_ini
        date fecha_fin
    }
 
    EMPLEADO ||--o{ ASIGNACION : "participa en"
    PROYECTO ||--o{ ASIGNACION : "tiene asignados"
    CLIENTE ||--o{ PROYECTO : "contrata"
    EMPLEADO ||--o{ REGISTRO_HORAS : "registra"
    PROYECTO ||--o{ REGISTRO_HORAS : "recibe horas de"
```

## Alcance Funcional 

### Alcance Mínimo

Regularidad:
|Req|Detalle|
|:-|:-|
| CRUD simple | 1. CRUD Empleado<br>  2. CRUD Cliente<br>  3. CRUD Categoría de Empleado |
| CRUD dependiente | 1. CRUD Proyecto {depende de} CRUD Cliente<br>  2. CRUD Asignación {depende de} CRUD Empleado y CRUD Proyecto<br>  3. CRUD Registro de Horas {depende de} CRUD Empleado y CRUD Proyecto |
| Listado<br>+<br>detalle | 1. Listado de proyectos filtrado por cliente, muestra nombre del proyecto, fechas y horas estimadas => detalle muestra datos completos del proyecto, cliente y empleados asignados<br>  2. Listado de registros de horas filtrado por empleado y rango de fecha, muestra nombre del empleado, proyecto, fecha y horas cargadas => detalle muestra descripción completa de la tarea |
| CUU/Epic | 1. Registrar horas trabajadas en un proyecto (Empleado)<br>  2. Asignar empleado a un proyecto (Admin RRHH)<br>  3. Verificar y aprobar carga horaria de un empleado (Admin RRHH)<br>  4. Consultar resumen de horas por proyecto (Admin RRHH) |


Adicionales para Aprobación
|Req|Detalle|
|:-|:-|
| CRUD | 1. CRUD Empleado<br>  2. CRUD Cliente<br>  3. CRUD Categoría de Empleado<br>  4. CRUD Proyecto<br>  5. CRUD Asignación<br>  6. CRUD Registro de Horas |
| CUU/Epic | 1. Registrar horas trabajadas en un proyecto (Empleado)<br>  2. Asignar empleado a un proyecto (Admin RRHH)<br>  3. Verificar y aprobar carga horaria de un empleado (Admin RRHH)<br>  4. Consultar resumen de horas por proyecto (Admin RRHH)<br>  5. Login con autenticación propia y control de acceso por rol (Admin / Empleado) |


### Alcance Adicional Voluntario

|Req|Detalle|
|:-|:-|
| Listados | 1. Dashboard de horas por proyecto filtrado por mes, muestra empleados, horas cargadas y porcentaje de avance sobre el estimado<br>  2. Historial de asignaciones de un empleado, muestra proyectos en los que participó con fechas y horas totales registradas |
| CUU/Epic | 1. Notificación por email al empleado cuando es asignado a un proyecto<br>  2. Exportar reporte de horas de un proyecto en formato CSV |
| Otros | 1. Contador de horas diarias disponibles por empleado con alerta visual al superar el límite |

