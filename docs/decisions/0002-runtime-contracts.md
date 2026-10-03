# ADR 0002 — Contratos validados em tempo de execução

**Status:** aceito

Tipos estáticos não validam a resposta recebida pela rede. O Astro valida os payloads do BFF em runtime antes de renderizar cada jornada. Campos essenciais ausentes ou incompatíveis são erros de contrato, não dados assumidos pelo cliente.
