# ADR 0001 — Backend for Frontend

**Status:** aceito

O frontend não conversa diretamente com fontes públicas. Um BFF em .NET 9 centraliza credenciais, contratos, cache, regras de disponibilidade e limites de chamadas. Isso reduz acoplamento com formatos externos instáveis e impede que chaves sejam expostas no navegador.
