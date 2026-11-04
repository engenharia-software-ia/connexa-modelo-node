# Atividade em grupo: uma melhoria vertical com IA

**Duração máxima: 120 minutos.** A equipe parte de uma User Story e de uma Task já existentes no Azure Boards, usa um agente de IA para implementar uma mudança pequena e demonstrável, verifica o resultado e registra uma decisão humana. O mesmo formato pode ser aplicado aos modelos Java e .NET: requisito no Boards, plano aprovado por pessoas, mudança pequena, verificação oficial e evidência.

Esta atividade ensina o fluxo de trabalho; não pede para ampliar o modelo-base. O agente não cria nem altera work items. A equipe escolhe uma Task real e uma pessoa registra a decisão final no Azure Boards.

## Preparação obrigatória — fora dos 120 minutos

Não inicie o cronômetro até que:

- O repositório da equipe e o projeto `Connexa` do Azure Boards estejam configurados, com a conexão GitHub–Boards pronta.
- A User Story e sua Task estejam prontas, com critérios observáveis, escopo permitido e a Task vinculada à história.
- O agente escolhido consiga ler os work items pelo MCP. Configure a organização em `.vscode/mcp.json` (Copilot) ou `.codex/config.toml` (Codex) e conclua o login antes da atividade. Não coloque tokens ou senhas em prompts ou arquivos.
- O grupo tenha aberto o repositório e confirmado Node.js 24 e PostgreSQL em `localhost:5432` (no Codespaces, use o banco já iniciado).
- A verificação inicial `./verificar` (Codespaces/Linux/macOS) ou `.\verificar.ps1` (Windows) termine sem falhas. Resolva problemas de ambiente antes da sessão.

Escolha uma Task com um ou dois resultados verificáveis, que não exija dependências novas, alterações de autenticação ou mudança ampla de arquitetura. Se a preparação falhar, corrija-a antes ou reagende: não reduza o tempo de implementação para compensar setup.

## Roteiro de 120 minutos

| Minutos | Etapa | Resultado |
|---|---|---|
| 0–10 | Ler a User Story e a Task completas no Azure Boards; identificar critérios e limites de escopo. | O grupo consegue explicar o comportamento esperado e o que não pode mudar. |
| 10–20 | Colar o prompt abaixo no agente; revisar o plano proposto e aprová-lo como grupo antes de qualquer edição. | Plano curto, arquivos permitidos e teste associado a cada critério. |
| 20–55 | Implementar a menor mudança que satisfaça os critérios, com uma pessoa acompanhando o diff. | Mudança demonstrável e testes pertinentes, sem alterações fora do escopo. |
| 55–80 | Executar `./verificar` (Codespaces/Linux/macOS) ou `.\verificar.ps1` (Windows). | Resultado real do comando oficial anotado; falhas não são ocultadas. |
| 80–100 | Revisar o diff e demonstrar o cenário na aplicação ou por teste/API, conforme a Task. | A equipe confirma o comportamento e identifica qualquer risco ou pendência. |
| 100–115 | Reunir evidências mínimas e uma pessoa registrar a decisão humana na discussão da Task no Azure Boards. | Evidências vinculadas à Task e decisão explícita: aceito ou pendente, com justificativa. |
| 115–120 | Conferir a Definition of Done abaixo e encerrar. | Estado final claro; se algo falhou, a Task permanece pendente. |

**Total: 10 + 10 + 35 + 25 + 20 + 15 + 5 = 120 minutos.** Não use o tempo para expandir escopo. Se a verificação falhar ou a mudança não couber, registre o bloqueio e deixe a Task pendente em vez de declarar sucesso.

## Prompt pronto para o agente

Substitua os marcadores pelos IDs reais do Azure Boards; não invente IDs nem critérios. A User Story e a Task devem ser vinculadas por `AB#<id>`.

```text
Leia a User Story AB#<ID_DA_HISTORIA> inteira e a Task filha
AB#<ID_DA_TASK>, incluindo descrição, critérios/cenários e o escopo permitido.
Use o Azure Boards como especificação. Não crie nem edite work items.

Objetivo desta atividade: entregar uma melhoria vertical pequena, visível e
verificável, sem ampliar o modelo-base. Mantenha-se estritamente no escopo e
nas permissões da Task. Este modelo já possui o arquivo de teste de componente `frontend/src/features/sessao/SeletorDeEstudante.test.tsx`. `AGENTS.md` exige autorização explícita da pessoa supervisora para alterar testes existentes. Inclua esse arquivo no plano e peça autorização antes de adicionar casos; não remova nem enfraqueça testes existentes. Sem autorização explícita, não edite o arquivo e pare para ajustar a Task.

Antes de editar, apresente um plano com os arquivos
que pretende alterar/criar e um teste para cada cenário aplicável. Aguarde a
aprovação explícita do grupo. Se a Task for ambígua, incompleta ou grande
para uma mudança pequena, pare e explique o que falta.

Exemplo de mudança pequena compatível com este repositório: mostrar, junto ao
seletor, o e-mail do estudante simulado da sessão atual. O endpoint
GET /api/identidade/sessao já fornece esse dado no contrato Sessao; use o fluxo
existente e não altere a API.

Critérios de aceitação do exemplo:
1. A tela do seletor mostra o e-mail do estudante retornado pela sessão atual.
2. Ao trocar de estudante simulado, o e-mail exibido corresponde à sessão atualizada.
3. O seletor e as consultas existentes continuam funcionando.
4. Adicione testes de componente para os critérios, use dados fictícios e não inclua
dependências, migrações ou mudanças de back-end.

Após a aprovação do plano, implemente somente os arquivos autorizados. Execute
a verificação oficial: ./verificar no Codespaces/Linux/macOS ou
.\verificar.ps1 no Windows. Apresente arquivos alterados, testes executados e
resultado literal do comando. Não declare concluído se a verificação falhar.
Deixe a decisão de aceitar ou pedir ajustes para uma pessoa do grupo.
```

O exemplo reaproveita o contrato de sessão e a feature `frontend/src/features/sessao/`; ele é uma sugestão de escopo, não uma funcionalidade nova pré-instalada. Os IDs e critérios reais vêm sempre da User Story e da Task escolhidas.

## Evidências mínimas

Registre na discussão da Task no Azure Boards, por uma pessoa da equipe:

- IDs `AB#<id>` da User Story e da Task.
- Resumo do resultado, lista de arquivos alterados e link do pull request/diff, se houver.
- Comando oficial executado e resultado; se falhou, saída relevante e motivo de a Task continuar pendente.
- Evidência da demonstração (passos reproduzíveis, captura de tela ou resultado de teste/API).
- Decisão humana explícita — aceito ou pendente — e quem revisou; para pendência, o próximo ajuste necessário.

## Definition of Done

- [ ] A mudança atende aos critérios da Task e altera apenas o que o escopo permitido autoriza.
- [ ] O grupo aprovou o plano antes da edição e revisou o diff e o comportamento demonstrado.
- [ ] Os cenários aplicáveis têm testes; verificações não foram enfraquecidas.
- [ ] A verificação oficial terminou sem falhas e seu comando/resultado foi registrado.
- [ ] As evidências e a decisão humana foram registradas na Task do Azure Boards.
- [ ] Nenhuma dependência, funcionalidade ou alteração fora do escopo foi incluída.
