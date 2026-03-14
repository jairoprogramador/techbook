# Acceso Condicional (Entra ID)

## Analogía

El acceso condicional es como el portero que no solo comprueba la identidad, sino también desde dónde entras, con qué dispositivo y qué aplicación usas. Si entras desde una red de confianza y un dispositivo corporativo, te deja pasar; si entras desde una red desconocida o un dispositivo no gestionado, te pide un segundo factor (MFA) o te bloquea. Las reglas se definen en "políticas": quién (usuarios o grupos), qué aplicación (Microsoft 365, Azure Portal, etc.) y bajo qué condiciones (ubicación, dispositivo, riesgo) deben cumplir un requisito (MFA, dispositivo compatible, bloqueo). Así se protege el acceso a aplicaciones y recursos sin depender solo de la contraseña.

## Definición

El acceso condicional de Microsoft Entra ID es un mecanismo que aplica políticas de acceso basadas en condiciones (usuarios, aplicaciones en la nube, ubicación, dispositivo, riesgo de inicio de sesión, etc.): si se cumplen las condiciones asignadas, se aplican los controles de concesión (por ejemplo, exigir MFA, dispositivo compatible o unión híbrida a Entra ID) o se bloquea el acceso. Requiere Microsoft Entra ID Premium P1 (o superior).

Permite:

- Definir políticas tipo "si (quién, qué aplicación, qué condiciones) entonces (conceder con requisitos o bloquear)"
- Restringir o proteger el acceso según ubicación (red de confianza, IP, país), estado del dispositivo (compatible, unido a Entra ID, híbrido) o riesgo de inicio de sesión
- Exigir MFA, dispositivo marcado como compatible (Intune), dispositivo unido a Entra ID (híbrido o solo en la nube) o aplicación cliente aprobada antes de conceder acceso
- Bloquear el acceso cuando no se cumplan las condiciones o cuando se use autenticación heredada (legacy) si la política lo exige
- Aplicar políticas a aplicaciones en la nube (Microsoft 365, Azure Portal, aplicaciones propias integradas con Entra ID) y a usuarios o grupos concretos
- Usar modo solo informe (report-only) para evaluar el impacto de una política sin aplicarla

## Componentes

**Política de acceso condicional** – Regla que asocia asignaciones (quién, qué aplicación, qué condiciones) con controles de concesión o bloqueo; varias políticas pueden aplicarse al mismo usuario (se evalúan todas las que apliquen)

**Asignaciones (assignments)** – Quién y a qué aplica la política: usuarios o grupos (incluir/excluir), aplicaciones en la nube (incluir/excluir), y condiciones opcionales (ubicación, dispositivo, riesgo, aplicación cliente, etc.)

**Condiciones** – Señales que se evalúan para decidir si la política aplica: ubicación (red de confianza, países, IP), estado del dispositivo (compatible, unido a Entra ID, híbrido), plataforma del dispositivo (Windows, iOS, Android, etc.), aplicaciones cliente (autenticación moderna vs. heredada), riesgo de inicio de sesión o riesgo del usuario (con Identity Protection)

**Controles de concesión (grant controls)** – Requisitos que deben cumplirse para conceder el acceso: exigir MFA, exigir dispositivo compatible (Intune), exigir dispositivo unido a Entra ID (híbrido o cloud), exigir aplicación cliente aprobada, exigir política de protección de aplicaciones, exigir cambio de contraseña, o combinar varios

**Bloquear acceso** – Control que deniega el acceso cuando se cumplen las asignaciones y condiciones de la política; no concede acceso aunque se cumplan otros requisitos

**Modo solo informe (report-only)** – La política se evalúa y se registra el resultado (habría bloqueado o habría exigido controles) pero no se aplica; sirve para probar antes de activar

**Autenticación heredada (legacy)** – Clientes que no usan autenticación moderna (p. ej. POP, IMAP, SMTP, clientes antiguos de Office); no envían estado del dispositivo ni soportan MFA interactiva; las políticas que exigen MFA o dispositivo compatible suelen bloquearlos si no se excluyen

**Requisito de licencia** – Microsoft Entra ID Premium P1 (o superior) para usar acceso condicional

## Funcionalidad

1. Se crea una política de acceso condicional en Entra ID (Protección de identidad → Acceso condicional → Nueva política)
2. Se configuran las asignaciones: usuarios o grupos (incluir/excluir), aplicaciones en la nube (incluir/excluir)
3. Se configuran las condiciones opcionales: ubicación (redes de confianza, países), dispositivo (compatible, unido a Entra ID, híbrido), plataforma, aplicación cliente, riesgo de inicio de sesión o riesgo del usuario
4. Se eligen los controles: conceder acceso exigiendo MFA, dispositivo compatible, dispositivo unido a Entra ID, aplicación aprobada, etc., o bloquear acceso
5. Se puede habilitar la política en modo solo informe para ver el impacto sin aplicar
6. Al activar la política, Entra ID evalúa cada inicio de sesión: si el usuario y la aplicación coinciden con las asignaciones y se cumplen las condiciones, se aplican los controles (MFA, dispositivo, bloqueo); si no se cumplen, se bloquea o se pide cumplir el requisito
7. Varias políticas pueden aplicarse al mismo usuario; normalmente todas las que apliquen deben satisfacerse (lógica AND)
8. La autenticación heredada no soporta MFA ni estado de dispositivo; si la política exige MFA o dispositivo compatible y no se excluyen los clientes heredados, el acceso con legacy puede bloquearse

## Casos de Uso

- Exigir MFA cuando el usuario accede desde una red no confiable o desde fuera de la oficina
- Exigir dispositivo compatible (Intune) o unido a Entra ID para acceder a aplicaciones sensibles
- Bloquear el acceso desde ciertos países o desde redes no confiables
- Bloquear o restringir la autenticación heredada para forzar el uso de clientes modernos
- Proteger el acceso a Azure Portal (aplicación "Microsoft Azure Management") exigiendo MFA o dispositivo compatible
- Probar políticas en modo solo informe antes de activarlas
- Aplicar políticas distintas a invitados (B2B) o a grupos de alto riesgo

## Errores Comunes

- Creer que el acceso condicional está en Entra ID Free (requiere Premium P1)
- Configurar una política que exige MFA o dispositivo compatible sin excluir emergencias o cuentas de acceso de emergencia (riesgo de bloqueo total)
- No tener en cuenta que la autenticación heredada no soporta MFA ni estado de dispositivo (políticas que exigen MFA o dispositivo compatible pueden bloquear legacy si no se excluye)
- Activar una política en producción sin probarla antes en modo solo informe (puede bloquear a usuarios legítimos)
- Confundir "conceder con requisitos" con "bloquear" (conceder exige cumplir MFA, dispositivo, etc.; bloquear deniega el acceso directamente)
- Olvidar que varias políticas aplican a la vez y que normalmente todas deben cumplirse (AND)

## Preguntas

1. ¿El acceso condicional de Entra ID aplica políticas de acceso basadas en condiciones (usuarios, aplicaciones, ubicación, dispositivo, riesgo) y exige controles (MFA, dispositivo compatible) o bloquea el acceso?

2. ¿El acceso condicional requiere Microsoft Entra ID Premium P1 (o superior)?

3. ¿Los controles de concesión pueden exigir MFA, dispositivo compatible (Intune), dispositivo unido a Entra ID (híbrido) o aplicación cliente aprobada antes de conceder el acceso?

4. ¿La autenticación heredada (legacy) no soporta MFA ni estado de dispositivo, por lo que las políticas que exigen MFA o dispositivo compatible pueden bloquearla si no se excluye?

5. ¿El modo solo informe (report-only) evalúa y registra el resultado de la política sin aplicarla, para probar antes de activar?

6. ¿Varias políticas de acceso condicional pueden aplicarse al mismo usuario y normalmente todas las que apliquen deben satisfacerse (lógica AND)?
