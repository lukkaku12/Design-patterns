# Design-patterns
easy to understand explanations.


# Patrón Factory (Fábrica)

## ¿Qué es?
Un creador de objetos que esconde los detalles de construcción.

## ¿Cuándo usarlo?

Cuando necesitas crear diferentes versiones de algo (ej: guardar archivos en S3, Google Cloud o local).
Cuando la creación es compleja (configuraciones, conexiones, etc.).
## Partes clave:

Interfaz común: Define qué deben hacer todos los objetos (ej: guardar(), eliminar()).
Clases concretas: Implementan la interfaz (ej: S3Service, LocalService).
Fábrica: Decide cuál crear (ej: StorageFactory.create('s3')).


# Patrón Builder

## ¿Qué es?

Construye objetos complejos paso a paso.

## ¿Cuándo usarlo?

Cuando un objeto requiere muchas configuraciones opcionales
Para evitar constructores con muchos parámetros
## Partes clave:

Clase Builder con métodos de configuración
Método build() para obtener el producto final
Director (opcional) para definir flujos de construcción


# Patron Singleton

## ¿Qué es?

maneja una sola instancia de una clase, sin posibilidad de crear mas de una.

## ¿Cuándo usarlo?

Cuando se quiere manejar una instancia a traves de su codigo.

## Partes clave:
"Solo uno en toda la app".
Constructor privado + propiedad estática instance.
Usado en: Loggers, conexiones a BD, configuraciones globales.
Key Point: Acceso controlado a una única instancia.


# Dependency Injection (DI) - Explicación Clara

## ¿Qué es?
**"Pide tus herramientas en lugar de fabricarlas"**  
Un patrón que permite recibir las dependencias desde afuera en lugar de crearlas internamente.

## ¿Cuándo usarlo?
- Cuando necesites usar un servicio en múltiples partes de tu código
- Cuando quieras poder cambiar fácilmente implementaciones
- Para hacer testing más sencillo con mocks

## Partes clave:
1. **Interfaz/Clase base**: Define qué debe cumplir la dependencia
2. **Implementaciones concretas**: Versiones reales o de testing
3. **Inyector**: El encargado de proveer la dependencia (framework o manual)

## Ejemplo básico:
```typescript
// Sin DI ❌
class Car {
  private engine = new Engine(); // Crea su propia dependencia
  
  start() {
    this.engine.ignite();
  }
}

// Con DI ✅
class Car {
  constructor(private engine: Engine) {} // Recibe la dependencia
  
  start() {
    this.engine.ignite();
  }
}
```
y cuando se reciba ese motor falso funcionara

```typescript
const motorFalso = { arrancar: () => "¡Brrrum fake!" };
const coche = new Coche(motorFalso); // ✅ Test sin motor real
```

Con esta implementacion no nos veremos **FORZADOS** a usar una instancia real y dependencias ocultas (anti-patrón) sino que puede ser reemplazable y por eso su acogida en frameworks de todo tipo de lenguajes.

Tópicos relacionados: IoC (Inversion de control): delega responsabilidades a otros (invierte el control). no se encarga de instanciar la clase el mismo sino que en otra parte de mi codigo yo lo hago y la paso la instancia.
