# Escudo Contextual Inteligente — MVP de validación

Prototipo académico en React + TypeScript + Vite para simular intervenciones de protección ante fraude bancario por ingeniería social. **No es una aplicación bancaria real ni un detector validado de fraudes.**

## Iniciar

```bash
npm install
npm run dev
```

Abrir la URL que indique Vite (usualmente http://localhost:5173).

## Experimentos

1. Grupo A: con protección contextual. Grupo B: control sin intervención.
2. Ejecutar los escenarios: operación normal, llamada sospechosa, transferencia de riesgo.
3. Consultar clave o enviar transferencia; observar resultados.
4. Exportar CSV desde Panel del investigador. Guardar junto con los instrumentos y consentimiento de participantes.
5. Medir por separado tasa de divulgación simulada, éxito de respuesta, tiempo de tarea, CSAT, falsos positivos y abandono.

## Limitaciones

Todas las cuentas, valores y códigos son ficticios. El estado de llamada se configura manualmente. El motor utiliza reglas explicables y NO inteligencia artificial entrenada. No se mide batería, no hay conexión con APIs bancarias y los datos de eventos están solo en memoria; recargar elimina el registro.
