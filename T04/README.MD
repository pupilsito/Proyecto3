# Introducción

La empresa **Innovatech**, una start-up tecnológica en pleno crecimiento, se enfrenta a serios problemas de gestión de usuarios y accesos debido a la falta de un sistema centralizado de autenticación.  
Actualmente, cada servicio interno —como el servidor de archivos, la wiki de documentación o las aplicaciones corporativas— utiliza su **propia base de datos de usuarios y contraseñas**, mientras que los equipos clientes gestionan el acceso mediante **autenticación local**.  

Esta situación genera múltiples inconvenientes:

- **Ineficiencia operativa:** cada vez que un empleado se incorpora o abandona la empresa, el equipo técnico debe crear o eliminar cuentas en varios sistemas de forma manual.  
- **Riesgo de seguridad:** los usuarios tienden a reutilizar contraseñas entre servicios, lo que incrementa la vulnerabilidad del sistema.  
- **Falta de escalabilidad:** a medida que Innovatech añade nuevos servicios, el modelo actual se vuelve insostenible.

Ante este escenario, el **CEO de Innovatech** ha contactado con la consultora **EverPia** para implementar una **solución de autenticación centralizada**.  
La propuesta es desplegar **OpenLDAP (Lightweight Directory Access Protocol)**, una herramienta robusta, escalable y de código abierto, que encaja perfectamente con el entorno **GNU/Linux** utilizado por la compañía.

## Objetivo del Proyecto

La misión del equipo técnico es **implantar el servicio OpenLDAP** en un servidor Linux y dejarlo completamente operativo.  
Esto incluye las siguientes tareas principales:

1. **Instalación del servicio OpenLDAP.**  
2. **Configuración del dominio base** y creación de la **jerarquía de unidades organizativas**.  
3. **Integración de usuarios y grupos** dentro del directorio para su posterior uso en otros servicios de red.  
4. **Configuración de un equipo cliente** para que utilice el directorio como sistema de autenticación centralizado.

## Material de Referencia

Para el desarrollo de este proyecto, se proporcionará documentación técnica y materiales formativos disponibles en la plataforma Moodle, entre ellos:

- **UD04.AA1:** Servicios de Directorio  
- **UD04.AA2:** Instalación de OpenLDAP  
- **UD04.AA3:** Configuración del Directorio  
- **UD04.AA5:** Integración del Cliente al Directorio  

---



## Fichero de solución y menu principal
- Aqui se adjunta el fichero con la [solucion](solucio.md)
- [Volver al menu principal](/README.MD)
