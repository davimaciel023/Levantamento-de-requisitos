# VANTAGE
## Inteligência em Blindagem Patrimonial

**Documento de Levantamento de Requisitos — Etapa 2**

| Campo | Informação |
|---|---|
| **Disciplina** | Engenharia de Software — Programação Web I |
| **Professor** | Prof. Renato William Rodrigues de Souza |
| **Curso** | Análise e Desenvolvimento de Sistemas |
| **Semestre** | 2026.1 |
| **Equipe** | Davi Maciel · Breno França · Lucas Ferreira · Gabriel Uarem |
| **Versão** | 1.0 — Junho de 2026 |

> Instituto Federal do Ceará — Campus Boa Viagem  
> Curso de Análise e Desenvolvimento de Sistemas

---

## 1. Introdução

### 1.1 Propósito do Documento

Este documento tem como objetivo descrever de forma completa e estruturada os requisitos do sistema VANTAGE, desenvolvido pela equipe no âmbito da disciplina de Engenharia de Software (Programação Web I) do IFCE Campus Boa Viagem. O documento segue as práticas da Etapa 2 do ciclo de desenvolvimento, cobrindo Requisitos Funcionais, Requisitos Não Funcionais, Histórias de Usuário, Casos de Uso e Regras de Negócio.

### 1.2 Escopo do Sistema

O VANTAGE é uma plataforma mobile de gestão financeira inteligente voltada para pequenos empresários brasileiros. O sistema resolve o problema da mistura patrimonial — fenômeno em que o empresário utiliza o caixa da empresa como extensão da conta corrente pessoal — causa central de 60% dos fechamentos de pequenas empresas nos primeiros cinco anos (SEBRAE, 2023).

Através de integração com APIs de Open Finance regulamentadas pelo Banco Central, o VANTAGE lê transações em tempo real, classifica automaticamente gastos pessoais e operacionais, calcula o Pró-labore Seguro e apresenta um dashboard dinâmico baseado no Sistema de Zonas Financeiras (Alerta, Equilíbrio e Expansão). O produto também incorpora gamificação para formação de hábitos financeiros sustentáveis.

### 1.3 Stakeholders

| Stakeholder | Descrição | Papel no Sistema |
|---|---|---|
| **Empresário / MEI** | Pequeno empresário com CNPJ ativo, faturamento entre R$5k–80k/mês, sem formação contábil formal. | Usuário principal: cadastra-se, conecta conta bancária, visualiza dashboard, valida alertas e simula compras. |
| **Equipe de Desenvolvimento** | Estudantes do curso de ADS do IFCE responsáveis pela construção e manutenção do sistema. | Desenvolvem, testam e evoluem o produto. |
| **Professor Orientador** | Prof. Renato William — IFCE Campus Boa Viagem. | Valida os requisitos e orienta o ciclo de desenvolvimento acadêmico. |
| **Banco Central do Brasil** | Regulador do Open Finance via Resolução BCB n. 1/2021. | Define as regras de integração bancária que o sistema deve cumprir. |
| **LGPD / ANPD** | Autoridade Nacional de Proteção de Dados. | Exige conformidade com a Lei 13.709/2018 no tratamento de dados financeiros. |

### 1.4 Definições e Abreviações

| Termo / Abreviação | Significado |
|---|---|
| **RF** | Requisito Funcional — descreve o que o sistema deve fazer. |
| **RNF** | Requisito Não Funcional — descreve como o sistema deve se comportar. |
| **HU** | História de Usuário — descrição de funcionalidade do ponto de vista do usuário. |
| **CDU** | Caso de Uso — descreve a interação entre ator e sistema para atingir um objetivo. |
| **RN** | Regra de Negócio — restrição ou política que governa o comportamento do sistema. |
| **Open Finance** | Sistema Financeiro Aberto regulamentado pelo Banco Central do Brasil (BCB). |
| **Runway** | Índice de Autonomia Financeira: quantos dias a empresa sobrevive sem novas receitas. |
| **Pró-labore Seguro** | Valor calculado automaticamente que o empresário pode retirar sem comprometer o negócio. |
| **Smart Alert** | Notificação em tempo real ao detectar gasto pessoal na conta PJ. |
| **Sistema de Zonas** | Dashboard dinâmico com 3 estados: Alerta (vermelho), Equilíbrio (amarelo), Expansão (verde). |
| **Taxa de Contaminação** | Percentual de gastos pessoais detectados na conta CNPJ em relação à receita total. |
| **Score Vantage** | Pontuação de saúde financeira calculada com base nos 3 indicadores principais do sistema. |
| **LGPD** | Lei Geral de Proteção de Dados — Lei 13.709/2018. |
| **MoSCoW** | Método de priorização: Must Have, Should Have, Could Have, Won't Have. |
| **MEI** | Microempreendedor Individual. |
| **JWT** | JSON Web Token — padrão de autenticação stateless utilizado na API. |

---

## 2. Requisitos Funcionais (RF)

### 2.1 Regras para Escrita de RF

- Verbos de ação: cadastrar, calcular, exibir, detectar, classificar, reclassificar, simular, autenticar.
- Um requisito por sentença — ações distintas em itens distintos.
- Todos os RF são específicos, verificáveis e observáveis.
- Padrão: `RF[número]: [Ator] deve [verbo + objeto + contexto]`.

### 2.2 Tabela de Requisitos Funcionais

Mínimo exigido: 5 RF. Total documentado: 14 RF.

| ID | Descrição | Prioridade |
|---|---|---|
| **RF01** | O sistema deve permitir que o empresário cadastre sua conta com nome, e-mail, CNPJ e senha. | Must Have |
| **RF02** | O sistema deve autenticar o empresário por e-mail e senha, gerando token JWT com validade de 24 horas. | Must Have |
| **RF03** | O sistema deve calcular automaticamente o Pró-labore Seguro mensal, descontando custos fixos, impostos provisionados, aporte à reserva de emergência e capital de giro mínimo da receita recebida. | Must Have |
| **RF04** | O sistema deve classificar o empresário em uma das três Zonas Financeiras (Alerta, Equilíbrio ou Expansão) com base no Runway calculado em tempo real, exibindo o estado no dashboard principal. | Must Have |
| **RF05** | O sistema deve integrar-se às APIs de Open Finance regulamentadas pelo Banco Central, lendo e classificando transações bancárias do CNPJ em tempo real. | Must Have |
| **RF06** | O sistema deve emitir um Smart Alert ao detectar uma transação de caráter pessoal realizada na conta ou cartão do CNPJ, permitindo que o empresário reclassifique o gasto como Antecipação de Lucro com um único toque. | Must Have |
| **RF07** | O sistema deve permitir que o empresário simule o impacto de uma compra planejada, exibindo a projeção do Runway antes e depois da compra, com alerta visual caso a zona financeira piore. | Must Have |
| **RF08** | O sistema deve calcular e exibir o Score Vantage com base em três indicadores: Índice de Autonomia (Runway em dias), Taxa de Contaminação (% de gastos pessoais no CNPJ) e Eficiência Operacional (% de lucro líquido sobre receita). | Must Have |
| **RF09** | O sistema deve permitir que o empresário configure o valor do Piso de Sobrevivência (pró-labore mínimo mensal) durante o onboarding, podendo revisá-lo a qualquer momento nas configurações. | Should Have |
| **RF10** | O sistema deve registrar e exibir o histórico mensal de métricas financeiras (Runway, Taxa de Contaminação, Eficiência Operacional) em formato de gráfico de barras. | Should Have |
| **RF11** | O sistema deve disponibilizar missões semanais de educação financeira, atribuindo pontos de saúde ao empresário conforme a conclusão das tarefas. | Should Have |
| **RF12** | O sistema deve exibir um ranking anônimo setorial (Score Vantage) comparando a saúde financeira do empresário com a média de empresas do mesmo setor. | Could Have |
| **RF13** | O sistema deve conceder troféus de conquista ao empresário ao atingir marcos financeiros, como 30 dias consecutivos sem misturar contas pessoais e empresariais (Selo Muralha Patrimonial). | Could Have |
| **RF14** | O sistema deve gerar e exportar relatório mensal em PDF com resumo das métricas financeiras, gastos reclassificados e evolução do Score Vantage. | Won't Have |

### 2.3 Priorização MoSCoW

| Nível | Definição | RF do VANTAGE |
|---|---|---|
| **Must Have** | Sem isso o sistema não funciona. Crítico e inegociável. | RF01 a RF08 |
| **Should Have** | Importante, deve entrar se houver tempo e recursos. | RF09 a RF11 |
| **Could Have** | Agrega valor, pode ficar para versões futuras. | RF12 e RF13 |
| **Won't Have** | Reconhecido, mas fora do escopo desta versão. | RF14 |

---

## 3. Requisitos Não Funcionais (RNF)

### 3.1 Categorias de RNF

- **Desempenho:** tempo de resposta, velocidade de carregamento, latência de processamento.
- **Segurança:** criptografia, autenticação, proteção de dados em trânsito e em repouso.
- **Conformidade:** LGPD, regulamentações do Banco Central, Open Finance.
- **Disponibilidade:** uptime mínimo, tempo de inatividade aceitável.
- **Usabilidade:** número de toques por fluxo, responsividade, acessibilidade.
- **Escalabilidade:** capacidade de crescimento sem degradação de performance.
- **Manutenibilidade:** padrões de código, cobertura de testes, documentação.
- **Portabilidade:** compatibilidade com sistemas operacionais Android e iOS.

### 3.2 Tabela de Requisitos Não Funcionais

Mínimo exigido: 3 RNF. Total documentado: 9 RNF.

| ID | Categoria | Descrição | Prioridade |
|---|---|---|---|
| **RNF01** | Desempenho | O dashboard principal deve carregar e exibir todas as métricas em menos de 2 segundos após a autenticação, mesmo com conexão 4G (10 Mbps). | Must Have |
| **RNF02** | Segurança | As senhas dos usuários devem ser armazenadas com hash bcrypt (custo mínimo 12); toda comunicação deve usar HTTPS/TLS 1.3; os dados financeiros devem ser criptografados em repouso com AES-256. | Must Have |
| **RNF03** | Conformidade | O sistema deve estar em conformidade com a Lei Geral de Proteção de Dados (LGPD — Lei 13.709/2018), exigindo consentimento explícito do usuário para coleta de dados financeiros e permitindo exclusão completa dos dados a qualquer momento. | Must Have |
| **RNF04** | Disponibilidade | O sistema deve ter uptime mínimo de 99,5% ao mês, equivalente a no máximo 3,65 horas de indisponibilidade mensal, monitorado via Grafana com alertas automáticos. | Must Have |
| **RNF05** | Usabilidade | O fluxo de reclassificação de gasto (Smart Alert) deve ser concluído em no máximo 2 toques na tela. A interface deve ser responsiva entre 320px e 2560px de largura. | Must Have |
| **RNF06** | Desempenho | O processamento de transações bancárias via Open Finance deve ocorrer em modo assíncrono (Celery + Redis), sem bloquear a interface do usuário. Latência máxima de processamento: 5 segundos por lote de transações. | Should Have |
| **RNF07** | Escalabilidade | A arquitetura deve suportar crescimento de até 10.000 usuários simultâneos sem degradação de performance, utilizando contêineres Docker orquestrados com possibilidade de escala horizontal. | Should Have |
| **RNF08** | Manutenibilidade | O código backend deve seguir o padrão PEP 8 com cobertura mínima de testes unitários de 70%, documentado via docstrings e versionado no GitHub com commits semânticos. | Could Have |
| **RNF09** | Portabilidade | O aplicativo mobile deve funcionar corretamente nos sistemas operacionais Android (versão 10 ou superior) e iOS (versão 14 ou superior), compilado via Capacitor. | Should Have |

---

## 4. Histórias de Usuário (HU)

Mínimo exigido: 3 HU. Total documentado: 5 HU. Todas seguem o formato: *Como [tipo de usuário], quero [objetivo/ação], para que [benefício/valor].*

---

### HU01 — Visualização do Dashboard e Sistema de Zonas

| Campo | Detalhe |
|---|---|
| **Narrativa** | Como pequeno empresário, quero visualizar no dashboard minha zona financeira atual (Alerta, Equilíbrio ou Expansão) junto com meu Runway em dias e o valor de pró-labore disponível, para que eu saiba de imediato se posso fazer retiradas do negócio com segurança. |
| **Critérios de Aceitação** | 1. O dashboard deve exibir a zona financeira atual com a cor correspondente (vermelho, amarelo ou verde) em menos de 2 segundos após login. 2. O Runway deve ser calculado em tempo real como: Saldo disponível ÷ (Custo fixo mensal ÷ 30), exibido em dias inteiros. 3. O valor de pró-labore disponível deve ser exibido em destaque, bloqueado visualmente quando o Runway for inferior a 60 dias. 4. Ao mudar de zona, o sistema deve exibir uma notificação informando a mudança e o motivo. |
| **Prioridade** | Must Have |
| **Story Points** | 8 |
| **Sprint** | 2 |
| **Status** | To Do |

---

### HU02 — Smart Alert — Reclassificação de Gasto Pessoal

| Campo | Detalhe |
|---|---|
| **Narrativa** | Como pequeno empresário, quero receber um alerta imediato quando o sistema detectar um gasto de natureza pessoal no cartão ou conta da minha empresa, para que eu possa reclassificá-lo corretamente e manter minha Taxa de Contaminação sob controle. |
| **Critérios de Aceitação** | 5. O alerta deve aparecer em até 30 segundos após a transação ser detectada via Open Finance, exibindo nome do estabelecimento, valor, data e método de pagamento. 6. O botão 'Reclassificar' deve concluir a ação em um único toque, sem abrir tela adicional. 7. Após a reclassificação, a Taxa de Contaminação deve ser recalculada e atualizada no dashboard em tempo real. 8. Transações abaixo de R$ 5,00 devem ser ignoradas automaticamente para evitar alertas irrelevantes. |
| **Prioridade** | Must Have |
| **Story Points** | 13 |
| **Sprint** | 3 |
| **Status** | To Do |

---

### HU03 — Simulação de Impacto de Compra

| Campo | Detalhe |
|---|---|
| **Narrativa** | Como pequeno empresário, quero simular o impacto financeiro de uma compra planejada antes de realizá-la, para que eu possa tomar a decisão com consciência do risco e evitar comprometer a autonomia financeira do negócio. |
| **Critérios de Aceitação** | 9. O simulador deve exibir o Runway atual e o Runway projetado após a compra, em barras visuais comparativas com as cores das zonas financeiras. 10. Caso a compra reduza o Runway abaixo de 60 dias ou mude a zona financeira, o sistema deve exibir alerta em vermelho com a variação exata em dias. 11. O resultado da simulação deve aparecer em até 1 segundo após o usuário informar o valor da compra. 12. O sistema deve sugerir alternativas quando o impacto for crítico (ex: parcelamento ou adiamento para o próximo trimestre). |
| **Prioridade** | Must Have |
| **Story Points** | 8 |
| **Sprint** | 3 |
| **Status** | To Do |

---

### HU04 — Onboarding e Configuração do Piso de Sobrevivência

| Campo | Detalhe |
|---|---|
| **Narrativa** | Como novo usuário do VANTAGE, quero configurar meu Piso de Sobrevivência (valor mínimo de pró-labore mensal) durante o cadastro inicial, para que o sistema saiba qual é o mínimo que preciso retirar para cobrir meus gastos pessoais essenciais. |
| **Critérios de Aceitação** | 13. O onboarding deve guiar o usuário em no máximo 5 passos: dados pessoais, dados do CNPJ, conexão bancária via Open Finance, configuração de custos fixos e definição do Piso de Sobrevivência. 14. O campo de Piso de Sobrevivência deve exibir sugestão automática baseada no salário mínimo vigente como referência. 15. O consentimento explícito para coleta de dados financeiros (LGPD) deve ser obtido no passo 3, com linguagem clara e sem jargão jurídico. 16. O usuário deve conseguir concluir o onboarding completo em menos de 5 minutos. |
| **Prioridade** | Must Have |
| **Story Points** | 5 |
| **Sprint** | 1 |
| **Status** | To Do |

---

### HU05 — Gamificação — Missões Semanais e Score Vantage

| Campo | Detalhe |
|---|---|
| **Narrativa** | Como empresário usuário do VANTAGE, quero completar missões semanais de disciplina financeira e acompanhar minha evolução no Score Vantage, para que eu me mantenha engajado e desenvolva o hábito de gerir bem as finanças do meu negócio. |
| **Critérios de Aceitação** | 17. O sistema deve exibir pelo menos uma missão semanal ativa, com descrição, prazo e pontos de saúde a ganhar. 18. O Score Vantage deve ser recalculado semanalmente com base nos três indicadores (Runway, Taxa de Contaminação, Eficiência Operacional) e exibido com variação em relação à semana anterior. 19. Ao completar uma missão, o sistema deve exibir animação de conclusão e atualizar os pontos do usuário imediatamente. 20. O ranking setorial deve exibir a posição do usuário de forma anônima, comparando apenas com empresas do mesmo setor cadastrado. |
| **Prioridade** | Should Have |
| **Story Points** | 13 |
| **Sprint** | 4 |
| **Status** | To Do |

---

## 5. Casos de Uso (CDU)

Esta seção detalha os fluxos críticos do VANTAGE em especificação textual, complementando as Histórias de Usuário com fluxos alternativos e de exceção.

---

### CDU01 — Calcular e Exibir Pró-labore Seguro

| Campo | Detalhe |
|---|---|
| **ID / Nome** | CDU01 — Calcular e Exibir Pró-labore Seguro |
| **Ator Principal** | Empresário (usuário autenticado) |
| **Pré-condição** | Usuário autenticado; conta bancária PJ conectada via Open Finance; custos fixos e Piso de Sobrevivência configurados no onboarding. |
| **Pós-condição** | Dashboard atualizado com valor de pró-labore disponível, zona financeira e Runway calculados. |
| **Fluxo Principal** | 21. O sistema lê as transações bancárias via Open Finance. 22. O sistema soma as receitas recebidas no mês corrente. 23. O sistema desconta: custos fixos, impostos provisionados (alíquota do Simples Nacional), aporte à reserva de emergência e capital de giro mínimo. 24. O sistema calcula o Lucro Operacional Líquido e aplica o percentual de pró-labore configurado (padrão: 70%). 25. O sistema calcula o Runway: Saldo ÷ (Custo fixo ÷ 30). 26. O sistema classifica a zona financeira com base no Runway. 27. O dashboard é atualizado e exibido ao usuário. |
| **Fluxo Alternativo** | Se não houver transações bancárias suficientes (menos de 7 dias de dados), o sistema exibe aviso de 'dados insuficientes' e solicita inserção manual dos valores. |
| **Fluxo de Exceção** | Se a conexão com o Open Finance falhar, o sistema exibe último cálculo em cache com timestamp e badge 'Dados desatualizados', acionando reprocessamento automático a cada 5 minutos. |

---

### CDU02 — Reclassificar Gasto via Smart Alert

| Campo | Detalhe |
|---|---|
| **ID / Nome** | CDU02 — Reclassificar Gasto via Smart Alert |
| **Ator Principal** | Empresário (usuário autenticado) |
| **Pré-condição** | Transação de natureza pessoal detectada na conta PJ via Open Finance. |
| **Pós-condição** | Transação reclassificada; Taxa de Contaminação recalculada; dashboard atualizado. |
| **Fluxo Principal** | 28. O sistema detecta transação com padrão de gasto pessoal (MCC de restaurante, farmácia, supermercado etc.). 29. O sistema emite Smart Alert com detalhes da transação. 30. O usuário visualiza o alerta e toca em 'Reclassificar'. 31. O sistema move a transação para a categoria 'Antecipação de Lucro'. 32. O sistema recalcula a Taxa de Contaminação e atualiza o Score Vantage. 33. O dashboard reflete as alterações em tempo real. |
| **Fluxo Alternativo** | O usuário toca em 'Ignorar' — a transação permanece como gasto operacional e não impacta a Taxa de Contaminação. |
| **Fluxo de Exceção** | Se o usuário não interagir com o alerta em 24 horas, o sistema classifica automaticamente a transação como 'Pendente de revisão' e reduz o Score Vantage em 2 pontos. |

---

## 6. Regras de Negócio

As Regras de Negócio definem as restrições e políticas que governam o comportamento do VANTAGE de acordo com a lógica financeira do produto.

| ID | Regra de Negócio |
|---|---|
| **RN01** | O Pró-labore Seguro nunca pode ser liberado quando o Runway calculado for inferior a 30 dias, independentemente do valor do Lucro Operacional Líquido. |
| **RN02** | O percentual padrão de distribuição do Lucro Operacional Líquido como pró-labore é de 70%; os 30% restantes são mantidos na empresa como reserva de reinvestimento. O empresário pode alterar esse percentual entre 50% e 85%. |
| **RN03** | A Zona Vermelha é ativada automaticamente quando o Runway cair abaixo de 60 dias; a Zona Amarela entre 60 e 90 dias; a Zona Verde quando superior a 90 dias. Esses limiares são fixos e não podem ser alterados pelo usuário. |
| **RN04** | A Taxa de Contaminação é calculada mensalmente como: (total de gastos pessoais detectados no CNPJ ÷ receita total do mês) × 100. Valores acima de 10% reduzem o percentual de pró-labore liberável em 5 pontos percentuais. |
| **RN05** | O consentimento explícito do usuário para acesso às transações bancárias via Open Finance tem validade máxima de 12 meses, conforme Resolução BCB n. 1/2021, devendo ser renovado ao expirar. |
| **RN06** | Transações com valor inferior a R$ 5,00 não geram Smart Alert para evitar sobrecarga de notificações. Transações acima de R$ 500,00 com padrão pessoal geram alerta prioritário com vibração e som no dispositivo. |
