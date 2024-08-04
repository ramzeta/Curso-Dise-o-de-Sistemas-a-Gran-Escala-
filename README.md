### Curso: Diseño de Sistemas a Gran Escala 🚀

#### Introducción
Este curso aborda conceptos clave y componentes esenciales en el diseño de sistemas a gran escala, centrándose en los atributos de calidad necesarios para asegurar un funcionamiento eficiente y fiable.

---

### Clase 1: Introducción a la Escalabilidad 📈

#### Concepto de Escalabilidad
- **Definición:** Capacidad de un sistema para manejar una creciente carga de trabajo añadiendo recursos.
- **Importancia:** Permite que un sistema mantenga su rendimiento a medida que aumenta la demanda.

#### Tipos de Escalabilidad
1. **Escalabilidad Vertical:**
   - Añadir más recursos a un solo servidor.
   - **Ventajas:** Fácil de implementar.
   - **Desventajas:** Tiene un límite físico y no mejora la fiabilidad.

   ```pseudocode
   servidor = obtenerServidor()
   servidor.aumentarRecursos(CPU, RAM, almacenamiento)
   ```

2. **Escalabilidad Horizontal:**
   - Añadir más servidores para distribuir la carga.
   - **Ventajas:** Sin límite teórico, mejora la tolerancia a fallos.
   - **Desventajas:** Puede requerir modificaciones en el software y es más complejo de implementar.

   ```pseudocode
   servidores = [servidor1, servidor2, servidor3]
   balanceador = crearBalanceadorDeCarga(servidores)
   balanceador.distribuirCargas()
   ```

#### Estrategias de Gestión de Estado
1. **Stateful Services:**
   - Almacenan información de usuario en el servidor.
   - **Problema:** Dificulta la escalabilidad horizontal.

   ```pseudocode
   servidor.guardarEstado(usuario, datosSesion)
   ```

2. **Stateless Services:**
   - No almacenan información de usuario en el servidor.
   - **Ventaja:** Facilita la escalabilidad horizontal.

   ```pseudocode
   cliente.enviarSolicitud({usuario, datosSesion})
   servidor.procesarSolicitud(cliente.datos)
   ```

---

### Clase 2: Fiabilidad 🛠️

#### Concepto de Fiabilidad
- **Definición:** Probabilidad de que un sistema opere sin fallos durante un periodo de tiempo.
- **Métrica Clave:** Uptime (tiempo de actividad).

#### Métricas Importantes
1. **MTBF (Mean Time Between Failures):** Tiempo medio entre fallos.
2. **MTTR (Mean Time to Recover):** Tiempo medio para recuperar el sistema tras un fallo.

#### Estrategias para Mejorar la Fiabilidad
1. **Prevención de Fallos:**
   - Eliminar puntos únicos de fallo.
   - Implementar redundancia.

   ```pseudocode
   if sistema.detectarFallo():
       sistema.activarRedundancia()
   ```

2. **Detección de Fallos:**
   - Monitorización continua y alertas automáticas.

   ```pseudocode
   sistema.monitorizar()
   if sistema.detectarAnomalia():
       sistema.enviarAlerta(administrador)
   ```

3. **Recuperación de Fallos:**
   - Estrategias rápidas de recuperación (rollback, copias de seguridad).

   ```pseudocode
   if sistema.detectarFallo():
       sistema.rollback(versionAnterior)
       sistema.restaurarDesdeCopiaSeguridad()
   ```

---

### Clase 3: Mantenibilidad 🧹

#### Concepto de Mantenibilidad
- **Definición:** Facilidad con la que un sistema puede ser mantenido y evolucionado.
- **Importancia:** La mayor parte del costo de un proyecto de software proviene de su mantenimiento.

#### Características Clave
1. **Observabilidad:**
   - Monitorización y visibilidad del sistema.
   - Documentación detallada.

   ```pseudocode
   sistema.monitorizar()
   sistema.generarDocumentacion()
   ```

2. **Simplicidad:**
   - Código limpio y fácil de entender.
   - Reducir la complejidad innecesaria.

   ```pseudocode
   def funcionSimple():
       hacerAlgoSimple()
   ```

3. **Extensibilidad:**
   - Facilidad para añadir nuevas funcionalidades.
   - Adopción de metodologías ágiles (Agile).

   ```pseudocode
   sistema.agregarModulo(nuevaFuncionalidad)
   equipo.adoptarAgile()
   ```

---

### Clase 4: Balanceadores de Carga (Load Balancers) ⚖️

#### Concepto de Load Balancer
- **Definición:** Elemento que distribuye la carga de trabajo entre múltiples servidores.

#### Ventajas del Load Balancer
- Mejora la escalabilidad.
- Mejora el rendimiento.
- Mejora la fiabilidad al evitar puntos únicos de fallo.

#### Algoritmos de Balanceo de Carga
1. **Algoritmos Estáticos:**
   - **Round Robin:** Distribuye las peticiones secuencialmente.

   ```pseudocode
   balanceador = RoundRobin(servidores)
   while peticion:
       servidor = balanceador.obtenerSiguienteServidor()
       servidor.procesar(peticion)
   ```

   - **Round Robin Ponderado:** Distribuye las peticiones según pesos asignados.

   ```pseudocode
   balanceador = RoundRobinPonderado(servidores, pesos)
   while peticion:
       servidor = balanceador.obtenerSiguienteServidor()
       servidor.procesar(peticion)
   ```

   - **Hash de IP o URL:** Asigna peticiones basadas en un hash.

   ```pseudocode
   balanceador = HashBalanceador(servidores)
   while peticion:
       servidor = balanceador.obtenerServidorPorHash(peticion.ip)
       servidor.procesar(peticion)
   ```

2. **Algoritmos Dinámicos:**
   - **Menor Número de Conexiones:** Dirige la carga al servidor con menos conexiones activas.

   ```pseudocode
   balanceador = MenorNumeroDeConexiones(servidores)
   while peticion:
       servidor = balanceador.obtenerServidorConMenosConexiones()
       servidor.procesar(peticion)
   ```

   - **Menor Tiempo de Respuesta:** Envía peticiones al servidor con menor tiempo de respuesta.

   ```pseudocode
   balanceador = MenorTiempoDeRespuesta(servidores)
   while peticion:
       servidor = balanceador.obtenerServidorConMenorTiempo()
       servidor.procesar(peticion)
   ```

---

### Clase 5: Cachés 🗄️

#### Concepto de Caché
- **Definición:** Área de almacenamiento temporal para resultados de peticiones frecuentes y costosas.

#### Estrategias de Caché
1. **Cache Aside:**
   - La aplicación maneja la lógica de consulta a la caché y base de datos.

   ```pseudocode
   def obtenerDato(clave):
       dato = cache.obtener(clave)
       if not dato:
           dato = baseDeDatos.consultar(clave)
           cache.almacenar(clave, dato)
       return dato
   ```

2. **Read Through:**
   - La caché maneja la consulta a la base de datos.

   ```pseudocode
   def obtenerDato(clave):
       return cache.obtenerOConsultar(clave, baseDeDatos)
   ```

3. **Write Through:**
   - Actualiza la caché durante las escrituras.

   ```pseudocode
   def actualizarDato(clave, valor):
       cache.actualizar(clave, valor)
       baseDeDatos.actualizar(clave, valor)
   ```

4. **Write Behind (Write Back):**
   - Actualiza la caché antes de sincronizar con el almacenamiento principal.

   ```pseudocode
   def actualizarDato(clave, valor):
       cache.actualizar(clave, valor)
       cache.sincronizarAsincronamente(clave, valor, baseDeDatos)
   ```

#### Consideraciones Clave
- **Necesidad y Ubicación:** Analizar si realmente se necesita una caché y dónde implementarla.

   ```pseudocode
   if sistema.necesitaCache():
       sistema.implementarCache(ubicacion)
   ```

- **Expiration Policy (Política de Vencimiento):** Establecer un TTL adecuado.

   ```pseudocode
   cache.establecerTTL(clave, tiempoDeVida)
   ```

- **Eviction Policy (Política de Reemplazo):** Estrategias para gestionar espacio limitado (LRU, LFU, FIFO).

   ```pseudocode
   cache.establecerPoliticaReemplazo("LRU")
   ```

- **Consistencia:** Gestionar la consistencia entre múltiples instancias de caché y bases de datos.

   ```pseudocode
   sistema.gestionarConsistencia()
   ```

---

### Clase 6: CDN (Content Delivery Network) 🌐

#### Concepto de CDN
- **Definición:** Red de distribución de contenidos para mejorar el tiempo de acceso a recursos estáticos como imágenes y videos.

   ```pseudocode
   cdn = crearCDN()
   cdn.distribuirContenido([imagenes, videos, css, js])
   ```

---

Este curso proporciona una visión general de los conceptos y componentes necesarios para diseñar sistemas a gran escala eficientes y fiables. A medida que avancemos, profundizaremos en cada uno de estos temas con ejemplos prácticos y ejercicios.
