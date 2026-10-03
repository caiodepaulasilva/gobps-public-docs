# Interface e experiência

O frontend usa Astro para organizar rotas editoriais e entregar a maior parte das páginas como conteúdo estático. TypeScript fica concentrado nas interações que realmente precisam dele, como comparações, filtros, simuladores e a colinha eleitoral. Isso reduz trabalho no navegador sem transformar a interface em uma coleção de páginas isoladas.

## Componentes e linguagem visual

Componentes de composição como layout, navegação de retorno, abas e coleções preservam padrões de leitura e evitam duplicação. Novos componentes compartilhados só são criados quando têm mais de um uso real. A paleta usa superfícies neutras; verde sinaliza navegação e ação, amarelo indica atenção excepcional e azul contextualiza o Lab.

## Dados no navegador

O Astro não mantém catálogos políticos locais. Cada resposta vinda do BFF é validada em tempo de execução antes de virar um view model. Quando uma fonte obrigatória estiver indisponível, a interface não inventa valores; ela comunica a limitação ou omite apenas complementos previamente classificados como opcionais.

Consultas repetidas na mesma jornada podem usar cache de navegador e deduplicação. O objetivo é reduzir espera e chamadas redundantes, sem mudar a origem, o significado ou a rastreabilidade dos dados.

## Acessibilidade e telas menores

Fluxos interativos incluem foco perceptível, navegação por teclado, regiões de anúncio e estados claros de seleção. Imagens recebem dimensões explícitas para reduzir mudanças de layout. A revisão inclui celular, ausência de rolagem horizontal, contraste e preferência por redução de movimento.
