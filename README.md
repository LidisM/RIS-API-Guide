# RIS API: Arquitectura y Mejores Prácticas

Guía práctica para desarrolladores que desean comprender y construir un **Radiology Information System (RIS)** desde cero, usando **.NET 9, C#, PostgreSQL y Entity Framework Core**.

Esta guía resume los conceptos clave, la arquitectura recomendada y los primeros pasos para levantar un backend funcional orientado a salud digital.

---

## Tabla de Contenidos
1. [¿Qué es un RIS?](#qué-es-un-ris)
2. [Arquitectura técnica](#arquitectura-técnica)
3. [Primeros pasos](#primeros-pasos)
4. [Módulos principales](#módulos-principales)
5. [Mejores prácticas](#mejores-prácticas)
6. [Documentación extendida](#documentación-extendida)
7. [Sobre la autora](#sobre-la-autora)

---

## ¿Qué es un RIS?
Un **Radiology Information System (RIS)** es el sistema encargado de gestionar:
- Pacientes
- Estudios radiológicos (RX, TC, RM, US)
- Reportes médicos
- Integración con PACS/DICOM

Es la **columna vertebral** del flujo de trabajo en radiología, desde la cita hasta la entrega del informe.

---

## Arquitectura Técnica
**Stack referenciado:**
- **Backend:** C# con .NET 9
- **Base de datos:** PostgreSQL + Entity Framework Core
- **Testing:** Scalar, Swagger/OpenAPI
- **Logging:** Serilog
- **Interoperabilidad:** DICOM, HL7 FHIR (futuro)

**Diagrama básico:**

```plaintext
[Paciente] → [RIS API] → [Base de Datos]
                   ↓
                [PACS] → [Radiólogo]
```

---

## Primeros pasos

1. **Crear un nuevo proyecto Web API**
```bash
dotnet new webapi -n RisBackend
cd RisBackend
```

2. **Agregar Entity Framework Core y PostgreSQL**
```bash
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL
```

3. **Configurar DbContext mínimo**
```csharp
public class RisDbContext : DbContext
{
    public DbSet<Patient> Patients { get; set; }

    public RisDbContext(DbContextOptions<RisDbContext> options)
        : base(options) { }
}
```

---

## Módulos principales
- **Pacientes** → Registro y actualización de datos demográficos.
- **Estudios** → Programación, seguimiento y estado de los procedimientos.
- **Organizaciones** → Gestión de instituciones vinculadas (hospitales, clínicas).

Cada módulo se expone mediante controladores REST con operaciones **CRUD**.

---

## Mejores prácticas
✔️ Validaciones robustas en los modelos.  
✔️ Generación de identificadores únicos de historia clínica.  
✔️ Paginación y filtros para escalabilidad.  
✔️ Auditoría y logs detallados para compliance (HIPAA/GDPR).  
✔️ Testing de endpoints con Scalar o Swagger UI.

---

## Documentación extendida
Para detalles más completos revisa la carpeta [`/docs`](./docs):
- [Arquitectura](./docs/arquitectura.md)
- [Mejores prácticas](./docs/mejores-practicas.md)
- [Problemas comunes](./docs/problemas-comunes.md)
- [Siguientes pasos](./docs/siguientes-pasos.md)

---

## Sobre la autora
**Lidis Méndez**  
Technical Writer & Backend Developer (C#/.NET)  
Especializada en sistemas médicos, documentación técnica y transformación digital.

 Conecta en: [Medium](https://medium.com/@lidismendez369) | [LinkedIn](https://www.linkedin.com/in/lidis-mendez/) | [GitHub](https://github.com/LidisM)
