# Estudo de caso: GOBPS

O GOBPS parte de um problema simples: conteúdo político circula rapidamente, mas suas relações institucionais raramente ficam organizadas para consulta posterior. A proposta foi criar uma experiência pública que não se limita a reunir links — ela organiza ministérios, representantes, instituições, eleições, orçamento e participação, preservando fontes e limites de cada informação.

Tecnicamente, o trabalho combina Astro para entrega de interface e .NET 9 para uma camada de dados e regras. A separação permite que o navegador permaneça leve e que integrações, cache, credenciais, contratos e indisponibilidades sejam tratados em um ponto controlado. O projeto também adotou validação de contratos em tempo de execução, arquitetura com controllers finos e casos de uso explícitos, telemetria de baixo risco e um fluxo de entrega com testes e revisão.

Os desafios mais relevantes não foram apenas visuais: consistência de dados públicos, limites de fontes, resposta honesta quando uma origem falha, associação cuidadosa entre registros externos e perfis internos, acessibilidade em interações densas e responsabilidade editorial sobre pessoas e instituições.

Para uma entrevista, este caso permite discutir arquitetura de BFF, contratos, cache, resiliência, observabilidade, LGPD, CI/CD, revisão de fontes e produto educacional. O ponto central é que decisões técnicas foram feitas em função de uma plataforma pública confiável, não como abstrações isoladas.
