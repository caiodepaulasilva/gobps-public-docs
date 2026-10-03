# Qualidade e ciclo de entrega

## Fluxo de branches

`feature/*` ou `fix/*` seguem para `development`. Depois de validação, `development` é integrado a `main`, que representa produção. Correções urgentes partem de `main` e retornam a `development`.

## Controles de qualidade

- Build reprodutível e auditoria de dependências.
- Testes automatizados do backend em modo Release.
- Testes de contrato entre endpoints e schemas consumidos pelo Astro.
- Validação de tipagem e build do frontend.
- Revisões para conteúdo, fonte, responsividade, contraste, teclado e celular.
- Testes visuais progressivos com Playwright para jornadas críticas.

Testes de integração usam clientes HTTP falsos somente no ambiente de teste. Eles tornam cenários de indisponibilidade e contratos determinísticos; nunca se tornam respostas alternativas de produção.

## Observabilidade responsável

O sistema mede falhas, duração, indisponibilidade de fonte e entrega do formulário por eventos agregados. Não mede navegação individual, nem inclui nome, e-mail, IP, token, corpo de formulário ou URL com parâmetros nos logs. As mensagens usam catálogo controlado e campos estáveis para permitir análise humana sem vazar dados.

## Definition of Done

Uma mudança é considerada pronta quando o contrato foi revisado, os testes relevantes passaram, a fonte foi conferida, a jornada funciona em teclado e celular, e a revisão editorial foi aprovada. Rota ou conteúdo novo só entra na navegação pública após validação local explícita.
