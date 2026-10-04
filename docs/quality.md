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

### Pirâmide de verificação

Testes de unidade do BFF cobrem regras, normalização e resultados de casos de uso. Testes de contrato verificam que os campos indispensáveis retornados pelos endpoints correspondem aos schemas que o Astro aceita. A camada de interface usa Playwright para percorrer jornadas críticas, incluindo filtros, comparação, guia de votação, navegação móvel e ausência de rolagem horizontal.

O objetivo não é buscar cobertura numérica isolada. Cada teste protege um comportamento de produto ou uma fronteira importante: uma alteração de contrato não deve produzir tela parcialmente interpretada, um provedor indisponível deve ser comunicado de forma clara e uma mudança visual não deve quebrar uma jornada em celular.

Testes de integração usam clientes HTTP falsos somente no ambiente de teste. Eles tornam cenários de indisponibilidade e contratos determinísticos; nunca se tornam respostas alternativas de produção.

## Segurança e configuração

Segredos ficam fora do repositório e não são enviados ao navegador. Origens permitidas são explícitas; o formulário de contato combina proteção anti-robô e limitação de requisições. Escritas editoriais permanecem restritas fora do ambiente de desenvolvimento enquanto não houver autenticação e armazenamento durável.

## Observabilidade responsável

O sistema mede falhas, duração, indisponibilidade de fonte e entrega do formulário por eventos agregados. Não mede navegação individual, nem inclui nome, e-mail, IP, token, corpo de formulário ou URL com parâmetros nos logs. As mensagens usam catálogo controlado e campos estáveis para permitir análise humana sem vazar dados.

Métricas e logs apoiam a operação: tornam visíveis latência, falhas de origem e resultado de envio de contato, sem transformar visitantes em perfis de acompanhamento. Alertas e painéis são instrumentos de manutenção, não de coleta comportamental.

## Automação com revisão humana

Atualizações automatizadas preservam o último catálogo válido quando uma fonte falha e não promovem arquivos parciais. A automação reduz tarefas repetitivas; fatos políticos, cronologias, fontes, licenças e decisões editoriais continuam sujeitos à revisão humana antes da publicação.

## Entrega e reversibilidade

Uma pull request reúne contexto, evidências e checklist de fonte, contrato, acessibilidade, celular e segurança. A integração em `development` reduz o risco de publicar mudanças isoladas diretamente em produção; `main` representa a versão pública. Dependências automatizadas recebem o mesmo fluxo de validação das demais alterações.

Publicações são deliberadamente pequenas quando possível. Uma alteração pode ser revertida pela própria trilha de Git sem exigir edição manual em servidores, e um incidente de origem externa não autoriza dados substitutos. Essa combinação favorece recuperação rápida e histórico auditável.

## Definition of Done

Uma mudança é considerada pronta quando o contrato foi revisado, os testes relevantes passaram, a fonte foi conferida, a jornada funciona em teclado e celular, e a revisão editorial foi aprovada. Rota ou conteúdo novo só entra na navegação pública após validação local explícita.
