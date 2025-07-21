# Red Social en Haskell

## Descripción del Proyecto

Este proyecto implementa un modelo de red social utilizando programación funcional en Haskell. El sistema permite representar y manipular una red social con usuarios, relaciones de amistad y publicaciones, proporcionando diversas funcionalidades para analizar las interacciones entre usuarios.

## Características Principales

### Modelo de Datos

La red social está modelada con los siguientes tipos de datos:

- **Usuario**: `(Integer, String)` - Representa un usuario con ID único y nombre
- **Relación**: `(Usuario, Usuario)` - Define una relación de amistad entre dos usuarios
- **Publicación**: `(Usuario, String, [Usuario])` - Publicación con autor, texto y lista de usuarios que dieron "like"
- **RedSocial**: `([Usuario], [Relacion], [Publicacion])` - Estructura principal que contiene todos los elementos

### Funcionalidades Implementadas

#### 1. **Gestión de Usuarios**
- Obtener nombres de todos los usuarios
- Encontrar amigos de un usuario específico
- Calcular cantidad de amigos
- Identificar el usuario con más amigos
- Detectar usuarios con más de un millón de amigos ("Roberto Carlos")

#### 2. **Sistema de Publicaciones**
- Obtener todas las publicaciones de un usuario
- Encontrar publicaciones que le gustan a un usuario
- Verificar si dos usuarios tienen gustos similares (mismas publicaciones)

#### 3. **Análisis de Relaciones**
- Determinar si un usuario tiene un "seguidor fiel" (alguien que le da like a todas sus publicaciones)
- Verificar si existe una secuencia de amigos que conecte dos usuarios

## Estructura del Código

```
solucion/
├── Solucion.hs      # Implementación principal de todas las funciones
├── Auxiliares.hs    # Funciones auxiliares y definiciones de tipos
└── test-catedra.hs  # Casos de prueba
```

### Funciones Principales

| Función | Descripción |
|---------|-------------|
| `nombresDeUsuarios` | Extrae los nombres de todos los usuarios |
| `amigosDe` | Devuelve la lista de amigos de un usuario |
| `cantidadDeAmigos` | Cuenta el número de amigos de un usuario |
| `usuarioConMasAmigos` | Encuentra el usuario más popular |
| `estaRobertoCarlos` | Detecta usuarios con más de 1M de amigos |
| `publicacionesDe` | Obtiene las publicaciones de un usuario |
| `publicacionesQueLeGustanA` | Encuentra publicaciones que le gustan a un usuario |
| `lesGustanLasMismasPublicaciones` | Compara gustos entre usuarios |
| `tieneUnSeguidorFiel` | Verifica la existencia de seguidores leales |
| `existeSecuenciaDeAmigos` | Determina conectividad entre usuarios |

## Implementación Técnica

### Algoritmos Destacados

- **Búsqueda de amigos**: Utiliza pattern matching y recursión para recorrer las relaciones
- **Análisis de popularidad**: Implementa comparaciones recursivas para encontrar máximos
- **Detección de seguidores fieles**: Emplea intersección de conjuntos sobre las listas de likes
- **Conectividad de usuarios**: Algoritmo de búsqueda en amplitud adaptado para grafos de amistad

### Funciones Auxiliares

El módulo `Auxiliares.hs` proporciona:
- Validación de datos (usuarios válidos, relaciones válidas, etc.)
- Operaciones sobre listas (intersección, eliminación de duplicados)
- Predicados de verificación de integridad

## Ejemplo de Uso

```haskell
-- Crear una red social de ejemplo
redEjemplo :: RedSocial
redEjemplo = (
    [(1, "Ana"), (2, "Bob"), (3, "Carlos")],
    [((1, "Ana"), (2, "Bob")), ((2, "Bob"), (3, "Carlos"))],
    [((1, "Ana"), "Hola mundo!", [(2, "Bob")])]
)

-- Obtener amigos de Ana
amigosDe redEjemplo (1, "Ana")
-- Resultado: [(2, "Bob")]

-- Verificar si Bob y Carlos están conectados
existeSecuenciaDeAmigos redEjemplo (2, "Bob") (3, "Carlos")
-- Resultado: True
```

## Tecnologías Utilizadas

- **Lenguaje**: Haskell
- **Paradigma**: Programación Funcional
- **Características utilizadas**:
  - Pattern matching
  - Recursión
  - Funciones de orden superior
  - Tipos algebraicos
  - Composición de funciones

## Equipo de Desarrollo

- **Fernández Ana Celeste**  
- **Galli Casado Sastre Lucas Federico**
- **Peralta Diessler Bernardo**

## Cómo Ejecutar

1. Asegúrate de tener GHC (Glasgow Haskell Compiler) instalado
2. Carga el módulo principal:
   ```bash
   ghci Solucion.hs
   ```
3. Ejecuta las pruebas:
   ```bash
   ghci test-catedra.hs
   ```

## Validaciones y Robustez

El código incluye múltiples validaciones para garantizar la integridad de los datos:
- Usuarios con IDs únicos y nombres no vacíos
- Relaciones válidas entre usuarios existentes
- Publicaciones sin duplicados
- Verificación de consistencia en toda la red social

---

*Este proyecto fue desarrollado como parte del curso de Introducción a la Programación, aplicando los conceptos fundamentales de Haskell para resolver un problema real de modelado de redes sociales.*
