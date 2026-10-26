# K-Mat IA

Aplicación educativa y adaptativa de matemáticas para Android, orientada a estudiantes de **1° y 2° Básico**. El estudiante practica de forma autónoma escribiendo con el dedo o con un lápiz digital, recibe corrección inmediata y avanza según su desempeño, incluso sin conexión a Internet.

Proyecto APT (Capstone) · Ingeniería en Informática · Duoc UC
Cliente: TriskelEdu

## Equipo

| Integrante | Correo |
|---|---|
| Patricio Quijada | Pa.quijada@duocuc.cl |
| Fernando Vidal | Fe.vidaln@duocuc.cl |
| Matías Gallardo | Mati.gallardoc@duocuc.cl |

## Descripción del proyecto

K-Mat IA convierte la práctica de matemáticas, que normalmente se corrige a mano, en una experiencia digital, autónoma y medible:

1. **Diagnóstico:** ubica el nivel inicial del estudiante.
2. **Práctica:** presenta ejercicios de numeración, conteo, secuencias, adición y sustracción básica.
3. **Escritura:** el estudiante responde a mano y la app reconoce los números y signos con ML Kit Digital Ink.
4. **Adaptación:** un motor de reglas decide si el estudiante avanza, mantiene el nivel o refuerza.
5. **Progreso:** los resultados se guardan localmente y se sincronizan al recuperar la conexión.

El docente puede, de forma opcional, crear una sala, revisar el progreso de sus estudiantes y generar reportes. El adulto responsable gestiona los perfiles de sus hijos/as y puede consultar su avance.

## Tecnologías utilizadas

| Capa | Tecnología |
|---|---|
| App Android | Kotlin + Jetpack Compose |
| Reconocimiento de escritura | ML Kit Digital Ink Recognition |
| Almacenamiento local | Room / SQLite |
| Sincronización | WorkManager |
| Backend | Supabase (Auth, PostgreSQL, Storage, Edge Functions) |
| Seguridad | Row Level Security (RLS) y control de acceso por rol |
| IA (opcional) | Gemini API, vía backend |
| Gestión | GitHub, Scrum |

## Arquitectura

La app sigue **MVVM + Clean Architecture**, con un enfoque **offline-first**:

```
UI (Jetpack Compose)
   ↓
ViewModel (MVVM)
   ↓
Casos de uso (dominio)
   ↓
Repositorios
   ├── Local: Room / SQLite  ← fuente principal, funciona sin conexión
   └── Remoto: Supabase      ← sincronización con WorkManager
```

- La práctica del estudiante se guarda primero en el dispositivo.
- WorkManager sincroniza con Supabase cuando hay conexión.
- Supabase Auth y RLS controlan qué datos ve cada rol: el docente ve a los estudiantes de sus salas y el adulto responsable solo a los suyos.
- El núcleo del MVP funciona sin IA generativa; Gemini es un complemento.

## Funcionalidades implementadas

### ✅ Completadas

- Registro, inicio y cierre de sesión de adultos (docente y adulto responsable)
- Gestión de perfiles de estudiantes por el adulto responsable
- Acceso infantil por selección visual del perfil (avatar), sin contraseña
- Escritura a mano y reconocimiento con ML Kit
- Corrección y retroalimentación inmediata
- Registro de desempeño
- Guardado y consulta del progreso
- Práctica sin conexión y sincronización automática
- Creación de salas por el docente y unión a sala o grupo
- Revisión del progreso por el docente y el adulto responsable
- Gestión de usuarios por el administrador

### 🔄 En desarrollo

- Diagnóstico inicial
- Ejercicios personalizados
- Motor adaptativo (avanzar, mantener o reforzar)
- Asignación de refuerzos por el docente
- Generación de reportes en PDF o Excel

## Instalación y ejecución

### Requisitos

- Android Studio (versión reciente)
- JDK 17
- Un dispositivo o emulador Android; idealmente una **tablet** para probar la escritura
- Un proyecto de Supabase con sus credenciales

### Pasos

1. Clonar el repositorio:
   ```bash
   git clone https://github.com/fernandovidalnn/Portafolio-titulo-informatica.git
   ```
2. Abrir la carpeta del proyecto en **Android Studio** y esperar a que Gradle sincronice.
3. Configurar las credenciales de Supabase en el archivo `local.properties` (no se sube al repositorio):
   ```properties
   SUPABASE_URL=tu_url_de_supabase
   SUPABASE_ANON_KEY=tu_clave_publica
   ```
4. Conectar el dispositivo Android o iniciar un emulador.
5. Presionar **Run ▶** en Android Studio.

> La primera vez que se usa el reconocimiento de escritura, ML Kit descarga el modelo de idioma, así que en ese momento se necesita conexión.

## Documentación

La documentación de la Fase 1 (requerimientos, casos de uso, historias de usuario, modelo de datos y Carta Gantt) está en la carpeta del portafolio del equipo.
