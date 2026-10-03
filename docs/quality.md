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

O workflow de CI executa as verificações antes de integrar mudanças. Dependabot acompanha atualizações de dependências; a revisão humana continua necessária para avaliar impacto de contrato, origem de dados, acessibilidade e comportamento em celular.

Testes de integração usam clientes HTTP falsos somente no ambiente de teste. Eles tornam cenários de indisponibilidade e contratos determinísticos; nunca se tornam respostas alternativas de produção.

## Segurança e configuração

Segredos ficam fora do repositório e não são enviados ao navegador. Origens permitidas são explícitas; o formulário de contato combina proteção anti-robô e limitação de requisições. Escritas editoriais permanecem restritas fora do ambiente de desenvolvimento enquanto não houver autenticação e armazenamento durável.

## Observabilidade responsável

O sistema mede falhas, duração, indisponibilidade de fonte e entrega do formulário por eventos agregados. Não mede navegação individual, nem inclui nome, e-mail, IP, token, corpo de formulário ou URL com parâmetros nos logs. As mensagens usam catálogo controlado e campos estáveis para permitir análise humana sem vazar dados.

Métricas e logs apoiam a operação: tornam visíveis latência, falhas de origem e resultado de envio de contato, sem transformar visitantes em perfis de acompanhamento. Alertas e painéis são instrumentos de manutenção, não de coleta comportamental.

## Automação com revisão humana

Atualizações automatizadas preservam o último catálogo válido quando uma fonte falha e não promovem arquivos parciais. A automação reduz tarefas repetitivas; fatos políticos, cronologias, fontes, licenças e decisões editoriais continuam sujeitos à revisão humana antes da publicação.

## Definition of Done

Uma mudança é considerada pronta quando o contrato foi revisado, os testes relevantes passaram, a fonte foi conferida, a jornada funciona em teclado e celular, e a revisão editorial foi aprovada. Rota ou conteúdo novo só entra na navegação pública após validação local explícita.
