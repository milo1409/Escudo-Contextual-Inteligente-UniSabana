# Escudo Contextual Inteligente 🛡️

**Protección contextual frente al fraude bancario por ingeniería social | MVP B2C**

Proyecto académico de **Innovación y Emprendimiento en Tecnología** de la **Maestría en Arquitectura de Software — Universidad de La Sabana**.

Escudo Contextual Inteligente propone una capa de protección personal que correlacione señales como una llamada no verificada, la apertura de una aplicación financiera y mensajes o enlaces sospechosos, para emitir advertencias claras antes de que una persona comparta credenciales o realice una operación inducida mediante engaño.

> **Estado:** prototipo web interactivo y propuesta de arquitectura móvil. La versión publicada **no monitoriza llamadas, correos ni aplicaciones bancarias reales**, no accede a datos financieros y no demuestra prevención efectiva de fraudes. Las alertas, el historial precargado y los escenarios del sitio son demostrativos.

## 🌐 Aplicaciones publicadas

| Recurso | Enlace | Propósito |
|---|---|---|
| **MVP web — AWS Amplify** | [Abrir aplicación](https://main.d2aqebbf8g10z7.amplifyapp.com/) | Centro de protección personal, canales, historial y eventos de demostración. |
| **Laboratorio interactivo — Figma** | [Abrir escenarios](https://decoy-yard-84626603.figma.site) | Explorar situaciones de vishing, transferencia bajo presión, smishing y actividad normal. |
| **Prototipo conceptual inicial — Figma** | [Abrir prototipo](https://glad-fill-43783451.figma.site) | Documentar la evolución del diseño y del concepto de solución. |

## 🎯 Problema y propuesta de valor

Las medidas tradicionales de autenticación protegen el acceso a las cuentas, pero no necesariamente alertan cuando **la propia persona está siendo manipulada** para divulgar una clave o autorizar un pago. La solución propuesta busca intervenir en ese momento con advertencias oportunas y comprensibles, minimizando la fricción en actividades legítimas.

El proyecto evolucionó de una propuesta **B2B2C** (SDK integrado por entidades financieras) a un enfoque **B2C**: una aplicación de protección personal que el usuario —o un familiar— pueda configurar y contratar directamente. El cambio reduce la dependencia comercial de integraciones bancarias, aunque introduce retos de permisos y acceso a señales de otras aplicaciones.

## ✨ Funcionalidades del MVP web

- **Centro de protección:** indicadores de estado y resumen de actividad.
- **Controles de canales:** activar o pausar la evaluación demostrativa de móvil y correo.
- **Historial:** consulta de eventos precargados y nuevos eventos de prueba, con filtros por canal.
- **Laboratorio de eventos:** ejecución de casos y registro de alertas orientativas.
- **Exportación CSV:** descarga de registros de demostración para revisión.
- **Persistencia local:** preferencias e historial guardados en `localStorage` del navegador.
- **Diseño adaptable:** interfaz utilizable desde computador o teléfono.

### Escenarios incluidos

| Escenario | Señales representadas | Respuesta prevista |
|---|---|---|
| Falso asesor bancario | Llamada activa + acceso a banca | Advertencia para verificar por canal oficial. |
| Transferencia bajo presión | Llamada + destinatario nuevo + monto atípico | Alerta de riesgo elevado. |
| Correo sospechoso | Mensaje urgente + enlace no verificado | Recomendación de revisión. |
| Operación habitual | Actividad financiera sin señales adicionales | Sin advertencia innecesaria. |

## 🧱 Arquitectura

**Implementación web actual**

```text
Navegador
  ├── React + TypeScript (interfaz)
  ├── Reglas y eventos demostrativos
  ├── localStorage (preferencias e historial)
  └── Exportación CSV
          │
          ▼
AWS Amplify Hosting (archivos estáticos / HTTPS)
```

**Evolución prevista del producto móvil**

```text
Dispositivo Android (previsto)
  ├── Señales autorizadas del sistema operativo
  ├── Colector de eventos con permisos explícitos
  └── Motor de correlación y reglas
          └── Alerta preventiva al usuario

Servicios futuros opcionales
  ├── Consulta de reputación de dominios
  └── Sincronización segura y mínima de eventos
```

La solución móvil requiere desarrollo nativo, revisión de políticas Android/iOS, pruebas de privacidad y verificación de rendimiento. **El hosting web no concede permisos para observar otras aplicaciones ni llamadas telefónicas.**

## 🛠️ Tecnologías utilizadas

| Capa | Tecnología |
|---|---|
| Interfaz | React 19, TypeScript |
| Desarrollo y compilación | Vite 6 |
| Iconografía | Lucide React |
| Persistencia del MVP | `localStorage` |
| Publicación | AWS Amplify Hosting |
| Diseño y recorridos | Figma Make |

## ▶️ Ejecución local en Windows

**Requisitos:** Node.js y npm instalados. En PowerShell, desde la carpeta que contiene `package.json`:

```powershell
# Solo si tu red requiere usar los certificados confiables de Windows:
$env:NODE_USE_SYSTEM_CA = "1"

npm.cmd install
npm.cmd run dev
```

Abre la dirección que muestre Vite (habitualmente `http://localhost:5173/`). El sufijo `.cmd` evita problemas habituales con la política de ejecución de `npm.ps1` en PowerShell.

### Compilación de producción

```powershell
npm.cmd run build
npm.cmd run preview
```

La compilación genera la carpeta `dist/`.

## ☁️ Despliegue en AWS Amplify

1. Ejecuta `npm.cmd run build`.
2. Genera un ZIP **con el contenido** de `dist/`, dejando `index.html` en la raíz.
3. Abre [AWS Amplify Console](https://console.aws.amazon.com/amplify/home).
4. Crea o actualiza un despliegue **sin Git**, subiendo el ZIP mediante *drag and drop*.
5. Verifica la URL HTTPS y la carga de JavaScript/CSS en el navegador.

Para evitar problemas de rutas dentro de ZIP creados en Windows, puedes generar el paquete con Python:

```powershell
@'
from pathlib import Path
from zipfile import ZipFile, ZIP_DEFLATED
base = Path('dist')
with ZipFile('escudo-contextual-aws.zip', 'w', ZIP_DEFLATED) as z:
    for f in base.rglob('*'):
        if f.is_file():
            z.write(f, f.relative_to(base).as_posix())
'@ | python -
```

**Nota:** el despliegue manual no actualiza automáticamente la aplicación cuando se modifica el repositorio. Para despliegues continuos, se puede integrar GitHub con Amplify.

## 💼 Modelo de negocio B2C

La estrategia comercial propuesta es **freemium**, dirigida inicialmente a usuarios de banca digital y, especialmente, a hogares donde familiares ayudan a proteger a personas mayores.

| Plan propuesto | Precio mensual | Enfoque |
|---|---:|---|
| Gratuito | COP $0 | Acceso básico y evaluación inicial del valor. |
| Premium | COP $9.900 | Protección multicanal según capacidades y permisos disponibles. |
| Familiar | COP $19.900 | Protección de varios integrantes y acompañamiento consentido. |

**Los precios son hipótesis comerciales, no tarifas actualmente cobradas.** Su viabilidad requiere pruebas de disposición a pagar, costos de adquisición, retención y operación.

## 🔬 Validación e investigación

El trabajo académico estudia cuatro dimensiones: **deseabilidad, usabilidad, factibilidad técnica y viabilidad comercial**. La investigación previa documenta una encuesta exploratoria de 35 personas y 8 entrevistas; el análisis del nuevo enfoque B2C y de los prototipos requiere respaldo trazable de sus pruebas específicas.

Las métricas a medir incluyen decisiones seguras ante una advertencia, tolerancia a la intervención, falsos positivos, permisos concedidos y conversión potencial a planes de pago. Los **eventos demostrativos del MVP no deben interpretarse como incidentes reales bloqueados ni como respuestas de participantes**.

## 🔐 Privacidad y limitaciones

- No solicita contraseñas bancarias, claves dinámicas reales ni datos de pago.
- No graba llamadas ni lee mensajes personales.
- El prototipo web utiliza datos de demostración guardados localmente.
- Los interruptores de canales no conectan un teléfono ni una cuenta de correo.
- La detección real de señales móviles y cualquier integración de correo necesitarían desarrollo, permisos explícitos, cumplimiento normativo y pruebas independientes.

## 🗺️ Hoja de ruta

1. **MVP web:** experiencia de protección, historial y escenarios de evaluación.
2. **Pruebas con usuarios:** comparar decisiones con y sin advertencia; medir comprensión y fricción.
3. **Validación comercial:** probar precios Premium y Familiar y canales de adquisición.
4. **Prueba de concepto Android:** evaluar permisos, eventos disponibles, consumo de batería y políticas de distribución.
5. **Producto comercial:** solo después de verificar seguridad, eficacia, privacidad y sostenibilidad.

## 👥 Equipo académico

- Camilo Andrés Porras Martín
- Oscar Eduardo Clavijo Alarcón
- Edward Daniel Porras Martín

**Universidad de La Sabana — Maestría en Arquitectura de Software**  
Asignatura: Innovación y Emprendimiento en Tecnología.

---

**Aviso:** Este repositorio presenta un proyecto académico en evolución. No es un producto de seguridad certificado ni debe utilizarse como única medida de protección financiera.
