# Módulo 4 — Integraciones Avanzadas e Interconexión de Sistemas

Proyecto: **Agente CRM e Inteligencia Comercial**

Este checkpoint evoluciona el workflow desarrollado en el Módulo 3, manteniendo la arquitectura de Manager, Workers y memoria persistente, e incorporando una nueva ruta de atención de correos integrada con Gmail, HubSpot y Slack.

## Flujo M4

Gmail Trigger  
→ IF Anti auto-reply  
→ Limpieza de payload  
→ Búsqueda de contacto en HubSpot  
→ Actualización / creación según existencia  
→ Worker de Redacción Comercial  
→ Creación de Draft en Gmail para revisión humana  
→ Limpieza de payload  
→ Notificación en Slack

## Controles implementados

- **Anti-loop:** filtro inmediato después del Gmail Trigger para bloquear:
  - `Auto-reply`
  - `Out of office`
  - `Undeliverable`
  - remitentes `no-reply@`
- **Prevención de duplicados:** búsqueda por email en HubSpot antes de crear o actualizar.
- **Human-in-the-loop:** Gmail genera exclusivamente un **Draft**, sin envío automático.
- **Payload mínimo:** uso de Edit Fields antes del procesamiento CRM y antes de Slack.
- **OAuth2:** Gmail, HubSpot y Slack utilizan autenticación OAuth2.
- **Reutilización:** la nueva ruta utiliza el subworkflow existente `Worker | Redacción Comercial`.

## Pruebas realizadas

- Creación de contacto nuevo.
- Detección de contacto existente y actualización sin duplicarlo.
- Generación correcta de borrador en Gmail.
- Notificación correcta en Slack.
- Bloqueo exitoso de un correo `Auto-reply`.
- Regresión punta a punta del flujo M4.

## Archivos

- `checkpoint4_omar_rodriguez_montes_de_oca.json`
- `/evidencias` — capturas de arquitectura, controles y pruebas.
