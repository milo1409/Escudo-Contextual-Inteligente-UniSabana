# Escudo Contextual Inteligente — B2C v1.0

MVP académico para consumidores: asistente de evaluación de señales de estafa, recomendaciones preventivas, simulaciones educativas y exportación de registros.

## Ejecutar en Windows

En PowerShell, desde la carpeta que contiene `package.json`:

```powershell
$env:NODE_USE_SYSTEM_CA = "1" # Solo si la red utiliza certificados confiados por Windows
npm.cmd install
npm.cmd run dev
```

Abrir la URL que muestre Vite.

## Generar versión publicable en AWS Amplify

```powershell
npm.cmd run build
Compress-Archive -Path ".\dist\*" -DestinationPath ".\escudo-b2c-amplify.zip" -Force
```

Publicar el ZIP del contenido compilado mediante despliegue manual en Amplify Hosting. El ZIP debe contener `index.html` en la raíz.

## Alcance

- Evaluación orientativa de señales seleccionadas por el propio usuario.
- Consejos preventivos explicables, basados en reglas.
- Simulaciones educativas de vishing, smishing y fraude por mensajería.
- Registro local y exportación CSV.
- No intercepta llamadas, no se conecta a bancos, no realiza transferencias y no predice fraude mediante IA.
- Los datos en localStorage no se centralizan: cada participante debe exportar su CSV para la evaluación académica.

## Hipótesis por validar

- Comprensión de mensajes preventivos.
- Capacidad de reconocer situaciones sospechosas.
- Utilidad percibida y disposición a pagar por un asistente B2C.

Este MVP NO valida por sí mismo disposición de pago, eficacia antifraude real ni precisión de un clasificador. Registrar resultados de pruebas reales y conservar su protocolo.
