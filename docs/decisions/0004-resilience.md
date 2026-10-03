# ADR 0004 — Resiliência sem sobrecarregar fontes

**Status:** aceito

Integrações externas usam timeout, retry limitado, cache e atualização controlada. Catálogos caros podem ser preparados em segundo plano uma vez por inicialização. O objetivo é reduzir latência para visitantes sem usar automação agressiva, contornar proteções ou aumentar tráfego indevidamente.
