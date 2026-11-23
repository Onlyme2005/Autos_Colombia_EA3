# Autos Colombia — Iteración 3: Gestión de pagos

## Ejecutar

```bash
python -m venv .venv
# Windows
.venv\\Scripts\\activate
# macOS/Linux
source .venv/bin/activate
pip install -r requirements.txt
python app.py
```

Verificar en `http://127.0.0.1:5000/api/health`.

## Endpoints de pagos

- `GET /api/pagos` — listar pagos.
- `GET /api/pagos?estado=PENDIENTE` — listar obligaciones pendientes.
- `GET /api/pagos/<id>` — consultar el detalle y recibo de un pago.
- `POST /api/pagos` — confirmar pago.
- `GET /api/reportes/resumen` — consultar recaudo.
- `POST /api/salidas/<movimiento_id>` — cerrar movimiento y generar obligación pendiente.

Body para confirmar un pago:

```json
{
  "movimiento_id": 1,
  "metodo": "TRANSFERENCIA"
}
```

Métodos válidos: `EFECTIVO`, `TARJETA` y `TRANSFERENCIA`.

## Flujo de prueba

1. Registrar una entrada con `POST /api/entradas`.
2. Registrar la salida con `POST /api/salidas/<movimiento_id>`.
3. Consultar el pendiente con `GET /api/pagos?estado=PENDIENTE`.
4. Confirmar el pago con `POST /api/pagos`.
5. Consultar el recibo con `GET /api/pagos/<id>`.
6. Verificar el recaudo con `GET /api/reportes/resumen`.

La base de datos SQLite `autos_colombia.db` se crea automáticamente. Para reiniciar las pruebas, detener la API y eliminar ese archivo.
