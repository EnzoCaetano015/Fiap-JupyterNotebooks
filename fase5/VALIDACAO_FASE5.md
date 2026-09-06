# Validação final da Fase 5 pelo barema

Revisão realizada em **6 de setembro de 2026** no repositório `Fiap-JupyterNotebooks`.

Legenda:

- **PASSOU** — requisito verificado localmente ou por evidência disponível.
- **PENDENTE** — depende de uma ação que ainda deve ser realizada.
- **BLOQUEADO** — não pode ser confirmado com as informações disponíveis.

## Resumo executivo

| Área | Status | Observação |
|---|---|---|
| Notebook e Machine Learning | **PASSOU** | Execução integral repetida no novo caminho, sem erros. |
| README da Entrega 1 | **PENDENTE** | Estrutura pronta; falta publicar e inserir o vídeo real. |
| AWS e justificativa | **PASSOU** | Duas regiões, preços, evidências e decisão documentados. |
| README da Entrega 2 | **PENDENTE** | Estrutura pronta; falta publicar e inserir o vídeo real. |
| Vídeos obrigatórios | **PENDENTE** | Roteiros prontos fora do repositório; gravação e publicação ainda não realizadas. |
| Repositório e prazo | **BLOQUEADO** | Publicidade confirmada; adequação do repositório multifases e limite de commits dependem da regra/prazo da instituição. |

## Entrega 1

### Repositório — 1,5

| Item | Status | Evidência ou pendência |
|---|---|---|
| Novo repositório da Fase 5 | **PENDENTE** | A entrega foi colocada em `Fiap-JupyterNotebooks/fase5/`. Confirmar se o barema aceita um repositório acadêmico com outras fases ou exige um repositório exclusivo. |
| Repositório público | **PASSOU** | O GitHub identifica `EnzoCaetano015/Fiap-JupyterNotebooks` como público. |
| Notebook correto | **PASSOU** | Notebook da entrega presente em `fase5/notebook/`. |
| Nome exato | **PASSOU** | `EnzoCaetanoPeracioRodrigues_rm570352_pbl_fase4.ipynb`. |
| Nenhum commit após o prazo | **BLOQUEADO** | O prazo oficial não foi fornecido. Verificar antes de criar ou enviar commits. |

### Notebook — 3,0

| Item | Status | Evidência |
|---|---|---|
| Células executadas | **PASSOU** | 42 células de código com `execution_count`; nenhuma célula de código sem execução. |
| Código funcional | **PASSOU** | Execução integral via `nbconvert` concluída sem erro no novo repositório. |
| Markdown | **PASSOU** | 57 células Markdown documentam objetivos, método, achados e ressalvas. |
| EDA | **PASSOU** | Dimensões, amostra, tipos, estatísticas, ausências, duplicatas, culturas e faixas ambientais. |
| Outliers | **PASSOU** | IQR global e por cultura, totais, exemplos e decisão explícita de manter 156 registros. |
| Clusterização | **PASSOU** | KMeans para `k=2...10`, escolha de `k=8`, PCA e perfis. |
| Tendências | **PASSOU** | Perfis ambientais, composição por cultura e relação entre clusters e rendimento. |
| Cinco modelos | **PASSOU** | Regressão Linear, Árvore de Decisão, Random Forest, Gradient Boosting e KNN. |
| MAE | **PASSOU** | Calculado para os modelos avaliados. |
| MSE | **PASSOU** | Calculado a partir das previsões, antes da derivação do RMSE. |
| RMSE | **PASSOU** | Calculado no holdout e na validação cruzada. |
| R² | **PASSOU** | Calculado para treino, teste e validação cruzada. |
| Validação cruzada | **PASSOU** | Cinco folds agrupados por cenário ambiental, sem compartilhar cenários. |
| Conclusão | **PASSOU** | Seção final consolida EDA, outliers, clusters e regressão. |
| Pontos fortes | **PASSOU** | Seção específica no notebook. |
| Limitações | **PASSOU** | Tamanho, cobertura, diferenças entre culturas, validação externa e causalidade discutidos. |

### README — 2,0

| Item | Status | Evidência ou pendência |
|---|---|---|
| Introdução | **PASSOU** | Projeto, dataset e objetivos apresentados. |
| Link do notebook | **PASSOU** | Link relativo aponta para o arquivo existente. |
| Link real do vídeo | **PENDENTE** | Placeholder preservado; substituir somente após publicação. |

### Vídeo — 2,0

| Item | Status | Pendência |
|---|---|---|
| Até 5 minutos | **PENDENTE** | Roteiro estimado em menos de cinco minutos; confirmar duração da gravação final. |
| YouTube não listado | **PENDENTE** | Gravar e publicar como não listado. |
| Link no README | **PENDENTE** | Substituir o placeholder pelo endereço real. |

### Organização — 1,5

| Item | Status | Evidência ou pendência |
|---|---|---|
| Estrutura limpa | **PASSOU** | Entrega isolada em `fase5/`, sem ambiente virtual ou arquivos temporários. |
| Nomeação correta | **PASSOU** | Pastas e notebook seguem os nomes definidos nas tarefas. |
| Sem arquivos temporários | **PASSOU** | Ambiente e notebook de reexecução ficaram fora do repositório. |
| `requirements.txt` funcional | **PASSOU** | Dependências instaladas em ambiente virtual temporário e notebook executado com sucesso. |

## Entrega 2

### AWS — 2,5

| Item | Status | Evidência |
|---|---|---|
| São Paulo | **PASSOU** | Região `sa-east-1` documentada e capturada. |
| N. da Virgínia | **PASSOU** | Região `us-east-1` documentada e capturada. |
| 2 vCPUs | **PASSOU** | Instância `t3.micro`. |
| 1 GiB | **PASSOU** | Instância `t3.micro`. |
| Rede de até 5 Gbps | **PASSOU** | Perfil confirmado na calculadora. |
| 50 GB | **PASSOU** | Volume EBS `gp3` em ambas as regiões. |
| Linux | **PASSOU** | Mesmo sistema operacional nas duas estimativas. |
| On-Demand | **PASSOU** | Utilização de 100%, 730 horas mensais. |
| Preços atuais | **PASSOU** | Consulta direta à AWS Pricing Calculator em 06/09/2026. |
| Evidências | **PASSOU** | Capturas armazenadas em `fase5/assets/aws/`. |

### Justificativa — 2,5

| Item | Status | Evidência |
|---|---|---|
| Região mais barata | **PASSOU** | N. da Virgínia: US$ 11,59/mês. |
| Diferença de custo | **PASSOU** | US$ 8,27/mês; São Paulo custa 71,35% a mais sobre a opção barata. |
| Latência | **PASSOU** | Proximidade dos sensores brasileiros discutida sem garantia indevida. |
| Restrição de armazenamento no exterior | **PASSOU** | São Paulo escolhida quando aplicada a restrição do cenário. |
| Trade-off | **PASSOU** | Custo maior contraposto à residência dos dados e proximidade geográfica. |

### README — 2,0

| Item | Status | Evidência ou pendência |
|---|---|---|
| Comparação | **PASSOU** | Tabela com EC2, EBS e totais das duas regiões. |
| Imagens | **PASSOU** | Links relativos apontam para arquivos existentes. |
| Justificativa | **PASSOU** | Decisão econômica e decisão sob restrição apresentadas separadamente. |
| Link real do vídeo | **PENDENTE** | Placeholder preservado; substituir após publicação. |

### Vídeo — 2,0

| Item | Status | Pendência |
|---|---|---|
| Até 5 minutos | **PENDENTE** | Roteiro estimado em menos de cinco minutos; confirmar a gravação. |
| Calculadora mostrada | **PENDENTE** | Exibir as configurações e os cálculos durante a gravação. |
| Comparação explicada | **PENDENTE** | Seguir o roteiro preparado e conferir a gravação final. |
| YouTube não listado | **PENDENTE** | Publicar o vídeo e copiar o endereço real. |

### Organização — 1,0

| Item | Status | Evidência ou pendência |
|---|---|---|
| README acessível | **PASSOU** | `fase5/README.md` presente. |
| Imagens acessíveis | **PASSOU** | Sete capturas PNG válidas e referenciadas. |
| Nenhum commit após o prazo | **BLOQUEADO** | O prazo oficial não foi fornecido. |

## Validação técnica extra

| Item | Status | Evidência |
|---|---|---|
| Nenhum alvo sintético da Fase 4 reaproveitado | **PASSOU** | `y` é formado exclusivamente pela coluna real `yield` do dataset oficial. |
| Nenhum leakage | **PASSOU** | Split por cenário e pré-processamento ajustado dentro das Pipelines. |
| Validação cruzada implementada | **PASSOU** | Cinco folds por cenário ambiental. |
| Heatmap implementado | **PASSOU** | Heatmap de correlação presente nos outputs executados. |
| Resultados não hardcoded | **PASSOU** | Métricas, tabelas e gráficos são produzidos pelas células de cálculo. |
| Preços AWS não inventados | **PASSOU** | Valores acompanhados por capturas da AWS Pricing Calculator. |
| Nenhum item “Ir Além” implementado | **PASSOU** | Não foram encontrados componentes adicionais fora do escopo definido. |
| Notebook executável por outra pessoa | **PASSOU** | Caminho relativo do dataset, dependências declaradas e reexecução integral validada. |
| README suficiente para orientar a correção | **PASSOU** | Inclui execução, resultados, notebook, AWS, evidências e pendências de vídeo. |

## Ações obrigatórias antes da entrega

1. Confirmar se a instituição aceita o repositório multifases ou exige um repositório exclusivo para a Fase 5.
2. Confirmar o prazo e não criar nem enviar commits depois dele.
3. Gravar os dois vídeos com duração máxima de cinco minutos.
4. Publicar os vídeos no YouTube como não listados.
5. Substituir os dois placeholders do README pelos links reais.
6. Abrir os links no GitHub após o push e conferir notebook, imagens e README.
