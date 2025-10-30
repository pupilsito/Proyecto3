# Introducción

Como miembros del equipo técnico de la consultora **EverPia**, se nos ha asignado un nuevo reto profesional: realizar una **auditoría teórica y práctica del servicio DNS** para nuestro cliente **DigiCore**, una empresa dedicada al marketing digital.  
Esta organización ha detectado errores de conectividad en algunas de sus aplicaciones, y su equipo técnico sospecha que el origen del problema puede estar relacionado con una **resolución de nombres (DNS) incorrecta o lenta**.

El objetivo principal de esta tarea es **formar al personal técnico de DigiCore** en los fundamentos del DNS y, al mismo tiempo, **proporcionar herramientas de diagnóstico eficaces** que les permitan identificar y resolver problemas de manera autónoma.

La auditoría se divide en dos fases complementarias:

## Fase Teórica: Sesión Formativa

En esta primera fase se elaborará un **material formativo** que explique de manera clara los conceptos fundamentales del sistema DNS.  
Entre los temas a tratar se incluyen:

- **Jerarquía y estructura del DNS**: comprensión del árbol jerárquico desde la raíz hasta los dominios de segundo nivel.  
- **Proceso de resolución de nombres**: diferencias entre consultas iterativas y recursivas.  
- **Tipos de zonas**: directas e inversas, primarias y secundarias.  
- **Registros clave (Records)**: función de los registros A, CNAME, MX, NS y SOA.  
- **Conceptos esenciales**: TTL, respuesta autoritativa, reenviadores y resolución local mediante mDNS.

El resultado de esta etapa será la creación de una **píldora formativa en vídeo** (entre 10 y 15 minutos) que explique de forma breve pero comprensible todos estos contenidos.

## Fase Práctica: Diagnóstico de Nombres (Auditoría con CLI)

En la segunda fase se llevará a cabo una **demostración práctica** del uso de herramientas de diagnóstico DNS en diferentes sistemas operativos (Linux/macOS y Windows).  
Se emplearán comandos como `dig` y `nslookup` para:

- Realizar consultas sobre distintos dominios.  
- Analizar las respuestas obtenidas y los valores de TTL.  
- Identificar los servidores autoritativos.  
- Comprobar la resolución inversa y la resolución local.

El resultado final de esta fase será la elaboración de un documento llamado **guía.md**, que incluirá las **capturas de pantalla** y el **análisis detallado** de las consultas realizadas, así como las **pruebas de resolución local**.

## Fichero de solución y menu principal
- Aqui se adjunta el fichero con la [solucion](solucion.md)
- [Volver al menu principal](/README.md)



