# Arquitetura

## Limites do sistema

O frontend em Astro é responsável por composição, acessibilidade, navegação e interações locais. O backend em .NET 9 é um Backend for Frontend (BFF): recebe as chamadas do site, aplica regras de aplicação, estabiliza contratos e conversa com fontes externas. Dados editoriais versionados permanecem no backend até existir um repositório de dados apropriado.

```mermaid
sequenceDiagram
  participant P as Pessoa usuária
  participant A as Astro
  participant B as BFF .NET 9
  participant C as Cache
  participant F as Fonte pública

  P->>A: abre uma página
  A->>B: solicita contrato da jornada
  B->>C: consulta resultado recente
  alt resultado disponível
    C-->>B: resposta íntegra
  else atualização necessária
    B->>F: consulta limitada e identificada
    F-->>B: dados públicos
    B->>C: armazena por janela apropriada
  end
  B-->>A: contrato estável ou indisponibilidade honesta
  A-->>P: conteúdo validado em tempo de execução
```

## Camadas do backend

| Camada | Responsabilidade |
| --- | --- |
| Controllers | Binding HTTP, status e Problem Details; não contêm regra de negócio. |
| Use cases | Orquestração de uma jornada e resultados independentes do protocolo. |
| Services | Regras especializadas, cache e portas para capacidades externas. |
| Repositories e clientes | Leitura de JSON, escrita editorial controlada e adaptadores de provedores. |
| Models | Contratos e entidades sem dependência de ASP.NET ou HTTP. |

As dependências apontam para dentro. Um controller não acessa arquivo, relógio ou cliente externo diretamente.

## Contratos

O BFF é a fronteira de contrato. O Astro valida respostas em tempo de execução com schemas; campos indispensáveis não são convertidos por coerção insegura. Mudanças incompatíveis exigem versionamento explícito ou adaptação coordenada, acompanhada de testes de contrato.

### Modelos de leitura e rotas

O BFF expõe modelos de leitura voltados às jornadas do guia, e não espelhos diretos de tabelas, páginas externas ou arquivos de origem. Uma rota de ministério, por exemplo, reúne descrição editorial, cronologia, fontes e dados financeiros sem delegar essa composição ao navegador. Isso reduz acoplamento com formatos de terceiros e evita que cada página precise conhecer regras de normalização.

Consultas são tratadas como operações REST: recursos possuem rotas estáveis, filtros usam parâmetros explícitos e entradas inválidas recebem resposta de validação. Falhas previsíveis usam Problem Details; indisponibilidade de uma origem é distinta de recurso inexistente e nunca é convertida em dado estimado.

## Dados e proveniência

Repositórios isolam os arquivos JSON editoriais versionados até que exista uma fonte de dados adequada para substituí-los. Integrações públicas passam por adaptadores próprios, que registram a fonte, a data de consulta e a finalidade quando aplicável. Um link ou crédito não substitui a avaliação de licença ou de termos de uso.

## Organização do código

Controllers são organizados por jornada funcional e mantidos pequenos: fazem binding, chamam um caso de uso e traduzem o resultado para HTTP. Casos de uso orquestram uma operação. Serviços concentram regras especializadas e integrações. Repositórios isolam leitura de JSON e escritas editoriais controladas. Essa divisão aplica responsabilidade única e inversão de dependência sem criar módulos vazios.

O projeto permanece em um assembly enquanto isso mantém o custo de manutenção baixo. As fronteiras já permitem separar domínio, aplicação, infraestrutura e API caso o crescimento torne essa divisão necessária.

### Composição e injeção de dependências

O ponto de composição registra interfaces e implementações de repositórios, serviços, casos de uso, clientes HTTP, cache e telemetria. Essa escolha deixa dependências visíveis, facilita testes com substitutos controlados e impede que detalhes de infraestrutura se espalhem pelo domínio. O objetivo não é reproduzir uma arquitetura distribuída em miniatura: cada abstração existe quando protege uma regra, uma integração ou uma variação real do sistema.

## Resiliência e desempenho

- Clientes HTTP têm timeout, retry limitado e cancelamento propagado.
- `HttpClientFactory` centraliza clientes e políticas de transporte; as dependências de infraestrutura entram por injeção de dependência, em vez de serem criadas pelos controllers.
- Endpoints idempotentes usam cache de curta ou média duração quando a origem permite.
- Atualizações de catálogos custosos podem iniciar em segundo plano após a aplicação estar saudável; uma falha nunca bloqueia a aplicação inteira.
- Dados que exigem resposta completa não recebem estimativas nem valores substitutos.
- Chamadas externas são limitadas e identificadas para reduzir risco de sobrecarga ou bloqueio de provedores.

O cache é empregado como proteção de desempenho e de provedores, não como substituição de verdade. Catálogos e consultas custosas têm duração compatível com sua volatilidade; dados de execução financeira e consultas públicas deixam clara a data ou a eventual indisponibilidade. O BFF prefere uma resposta explícita de indisponibilidade a servir um número inventado ou um valor antigo sem contexto.

## Operação e infraestrutura

O frontend estático e o BFF são implantados separadamente, com variáveis de configuração e credenciais mantidas fora do código. A separação permite que a interface seja distribuída com cache de borda, enquanto integrações, regras de negócio e chaves de fontes públicas permanecem no servidor. O desenho também reduz a superfície exposta ao navegador: ele só conhece a URL pública necessária para consumir os contratos.

Pipelines automatizados validam dependências, contratos, tipo, build e jornadas de interface antes da integração. A publicação ocorre a partir da branch principal e os ambientes não recebem segredos por arquivos versionados. Logs e métricas agregados acompanham falhas, latência e indisponibilidade sem registrar dados de visitantes ou detalhes operacionais que ampliem risco.

## Respostas HTTP e falhas esperadas

Controllers cuidam de binding, códigos de status e `Problem Details`. Regras de negócio, acesso a arquivo, relógio e chamadas a provedores ficam fora dessa camada. Assim, uma indisponibilidade de fonte pode ser comunicada com clareza, sem confundir erro técnico, ausência de dado e validação inválida.
