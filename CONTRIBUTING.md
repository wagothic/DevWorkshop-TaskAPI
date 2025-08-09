# 🤝 Guía de Contribución - TaskFlowPro

¡Gracias por tu interés en contribuir a TaskFlowPro! Este proyecto está diseñado como una plantilla educativa, y valoramos tanto las contribuciones de **profesores** como de **estudiantes**.

## 📋 Tipos de Contribuciones

### 👨‍🏫 **Para Profesores/Instructores**
- Implementaciones completas de endpoints
- Mejoras en la documentación educativa
- Nuevos patrones de diseño
- Casos de uso adicionales
- Guías de enseñanza

### 👨‍🎓 **Para Estudiantes**
- Implementación de TODOs
- Corrección de bugs
- Mejoras en comentarios
- Ejemplos de uso
- Preguntas y sugerencias

## 🚀 Proceso de Contribución

### **1. Fork del Repositorio**

```bash
# Hacer fork en GitHub, luego clonar
git clone https://github.com/tu-usuario/TaskFlowPro.git
cd TaskFlowPro

# Agregar upstream
git remote add upstream https://github.com/original-usuario/TaskFlowPro.git
```

### **2. Crear Rama de Trabajo**

```bash
# Para nuevas funcionalidades
git checkout -b feature/nombre-funcionalidad

# Para correcciones
git checkout -b fix/descripcion-fix

# Para documentación
git checkout -b docs/mejora-documentacion

# Para estudiantes implementando TODOs
git checkout -b student/implementar-users-crud
```

### **3. Realizar Cambios**

#### **Estándares de Código**
- Seguir las convenciones de C# y .NET
- Usar nombres descriptivos en inglés para código
- Comentarios y documentación en español (proyecto educativo)
- Mantener consistencia con el patrón existente

#### **Estructura de Commits**
```bash
# Formato: tipo(scope): descripción

# Ejemplos:
git commit -m "feat(users): implementar CreateUser endpoint"
git commit -m "fix(auth): corregir validación de JWT"
git commit -m "docs(readme): agregar sección de troubleshooting"
git commit -m "student(tasks): implementar GetAllTasks TODO"
```

### **4. Testing**

```bash
# Verificar que compila
dotnet build

# Ejecutar pruebas (si existen)
dotnet test

# Verificar que la API funciona
dotnet run --project DevWorkshop.TaskAPI.Api
```

### **5. Crear Pull Request**

#### **Título del PR**
- `[FEATURE] Implementar autenticación con roles`
- `[FIX] Corregir error en validación de email`
- `[DOCS] Mejorar guía de instalación`
- `[STUDENT] Implementar CRUD de usuarios`

#### **Descripción del PR**
```markdown
## 📋 Descripción
Breve descripción de los cambios realizados.

## 🎯 Tipo de Contribución
- [ ] Nueva funcionalidad
- [ ] Corrección de bug
- [ ] Mejora de documentación
- [ ] Implementación de TODO (estudiante)
- [ ] Refactoring
- [ ] Mejora de performance

## ✅ Checklist
- [ ] El código compila sin errores
- [ ] Se siguieron las convenciones de código
- [ ] Se agregó documentación necesaria
- [ ] Se probó la funcionalidad
- [ ] Se actualizó el README si es necesario

## 🧪 Cómo Probar
Pasos para probar los cambios:
1. Ejecutar `dotnet run`
2. Navegar a `/swagger`
3. Probar endpoint X con datos Y

## 📸 Screenshots (si aplica)
Agregar capturas de pantalla si hay cambios visuales.

## 📚 Contexto Educativo
Explicar qué aprenden los estudiantes con este cambio.
```

## 📝 Estándares de Código

### **Convenciones de Nomenclatura**

```csharp
// ✅ Correcto
public class UserService : IUserService
{
    private readonly IUnitOfWork _unitOfWork;
    
    public async Task<UserDto> GetUserByIdAsync(int userId)
    {
        // Implementación
    }
}

// ❌ Incorrecto
public class userservice : iuserservice
{
    private readonly IUnitOfWork unitOfWork;
    
    public async Task<UserDto> getUserById(int id)
    {
        // Implementación
    }
}
```

### **Documentación de Métodos**

```csharp
/// <summary>
/// EJEMPLO IMPLEMENTADO: Obtiene un usuario por su ID
/// 
/// Este método está completamente implementado como ejemplo para que los estudiantes
/// vean cómo debe estructurarse un servicio completo.
/// </summary>
/// <param name="userId">ID del usuario a buscar</param>
/// <returns>Usuario encontrado o null si no existe</returns>
/// <exception cref="ArgumentException">Cuando el ID es inválido</exception>
public async Task<UserDto?> GetUserByIdAsync(int userId)
{
    // Implementación
}
```

### **TODOs para Estudiantes**

```csharp
/// <summary>
/// TODO: ESTUDIANTE - Implementar creación de usuario
/// 
/// Pasos a seguir:
/// 1. Validar que el email no exista
/// 2. Hashear la contraseña
/// 3. Crear entidad User
/// 4. Guardar en base de datos usando Unit of Work
/// 5. Mapear a UserDto y retornar
/// 
/// Tip: Usar _unitOfWork.Users.AddAsync() y _unitOfWork.SaveChangesAsync()
/// </summary>
public async Task<UserDto> CreateUserAsync(CreateUserDto createUserDto)
{
    // TODO: ESTUDIANTE - Implementar
    throw new NotImplementedException("Método pendiente de implementación por el estudiante");
}
```

## 🎓 Guías Específicas

### **Para Profesores**

#### **Implementar Nuevo Endpoint Completo**
1. Crear DTOs necesarios
2. Definir interfaz de servicio
3. Implementar servicio completo
4. Crear controlador con todos los casos
5. Agregar documentación educativa
6. Incluir ejemplos de uso

#### **Agregar Nuevo Patrón de Diseño**
1. Documentar el patrón en README
2. Implementar ejemplo práctico
3. Agregar comentarios explicativos
4. Crear ejercicios para estudiantes

### **Para Estudiantes**

#### **Implementar TODO**
1. Leer cuidadosamente las instrucciones
2. Seguir el patrón del ejemplo implementado
3. Probar la funcionalidad
4. Agregar comentarios explicando tu solución

#### **Reportar Bug**
1. Describir el problema claramente
2. Incluir pasos para reproducir
3. Agregar logs o mensajes de error
4. Sugerir posible solución si la tienes

## 🔍 Review Process

### **Criterios de Aprobación**

#### **Para Código**
- ✅ Compila sin errores ni warnings
- ✅ Sigue las convenciones establecidas
- ✅ Incluye documentación adecuada
- ✅ Mantiene la arquitectura limpia
- ✅ Es educativamente valioso

#### **Para Documentación**
- ✅ Está en español (proyecto educativo)
- ✅ Es clara y comprensible
- ✅ Incluye ejemplos prácticos
- ✅ Ayuda al aprendizaje

### **Proceso de Review**

1. **Revisión Automática**: GitHub Actions verifica compilación
2. **Revisión de Código**: Maintainer revisa implementación
3. **Revisión Educativa**: Se evalúa valor pedagógico
4. **Aprobación**: Se merge si cumple criterios

## 🚨 Qué NO Hacer

### **❌ Cambios No Permitidos**
- Cambiar la arquitectura base sin discusión
- Eliminar comentarios educativos existentes
- Agregar dependencias innecesarias
- Romper la compatibilidad con .NET 9
- Cambiar URLs de endpoints ya establecidas

### **❌ Prácticas Desaconsejadas**
- Commits sin descripción clara
- PRs muy grandes (>500 líneas)
- Código sin documentar
- Ignorar las convenciones establecidas

## 🎯 Roadmap de Contribuciones

### **Prioridad Alta**
- [ ] Implementar pruebas unitarias
- [ ] Completar endpoints de Users
- [ ] Completar endpoints de Tasks
- [ ] Agregar validaciones avanzadas

### **Prioridad Media**
- [ ] Implementar caching
- [ ] Agregar logging estructurado
- [ ] Mejorar manejo de errores
- [ ] Documentación de deployment

### **Prioridad Baja**
- [ ] Frontend Blazor
- [ ] Notificaciones en tiempo real
- [ ] Métricas y monitoring
- [ ] Internacionalización

## 📞 Contacto

¿Tienes preguntas sobre cómo contribuir?

- 📧 **Email**: [tu-email@ejemplo.com]
- 💬 **Discussions**: [GitHub Discussions](https://github.com/tu-usuario/TaskFlowPro/discussions)
- 🐛 **Issues**: [GitHub Issues](https://github.com/tu-usuario/TaskFlowPro/issues)

## 🙏 Reconocimientos

Todos los contribuidores serán reconocidos en:
- README principal
- Sección de contributors
- Release notes

¡Gracias por ayudar a hacer de TaskFlowPro una mejor herramienta educativa! 🚀
