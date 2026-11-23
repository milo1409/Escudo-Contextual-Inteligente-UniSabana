# Escudo Contextual Inteligente · B2C v3 — Demo de producto

Aplicación React + TypeScript + Vite con estética de consola de seguridad personal. Permite configurar **preferencias simuladas** de protección móvil y correo, visualizar un centro de protección, inspeccionar un historial ficticio de intervenciones y ejecutar escenarios de prueba que generan eventos locales.

**Importante:** Los canales móvil y correo no son conexiones reales. Ninguna web puede detectar por sí misma llamadas y aplicaciones financieras externas. No se consultan correos, contactos, contraseñas, OTP ni operaciones bancarias. Todos los eventos de seguridad están etiquetados DEMO. La consola no debe comercializarse como protección real.

## Ejecutar en Windows (PowerShell)

```powershell
$env:NODE_USE_SYSTEM_CA = "1"
npm.cmd install
npm.cmd run dev
```

## Compilar para AWS Amplify

```powershell
npm.cmd run build
Compress-Archive -Path '.\dist\*' -DestinationPath '.\escudo-contextual-amplify.zip' -Force
```

Sube el ZIP compilado mediante despliegue manual de Amplify Hosting. `dist/index.html` debe quedar en la raíz del ZIP.

## Demostraciones incluidas

- Llamada en curso + banca abierta: advertencia preventiva.
- Transferencia bajo presión: alerta crítica.
- Correo de phishing: revisión recomendada.
- Operación normal: no se genera alerta.

Los eventos ficticios de ejemplo se cargan la primera vez y se guardan en `localStorage`. Todos los controles de activación afectan las simulaciones, no los dispositivos reales. El historial se exporta a CSV.

## Próximas etapas técnicas

Para una implementación real se requiere agente móvil compatible con políticas Android/iOS, permisos explícitos, definición de señales observables, pruebas en dispositivos, API autenticada y/o integración de correo autorizada. La ejecución web no otorga protección sobre otras aplicaciones.
