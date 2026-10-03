# FarmTech Solutions — Fase 6

## Visão Computacional

**Enzo Caetano Peracio Rodrigues — RM 570352** · Projeto individual

A FarmTech explora visão computacional. Esta fase compara
YOLOv5 customizada, YOLOv5 padrão pré-treinada em COCO e uma CNN própria treinada
do zero, nas classes `bottle` (0) e `backpack` (1).

O [notebook principal](notebook/EnzoCaetanoPeracioRodrigues_rm570352_pbl_fase6.ipynb)
contém todo o código Python da entrega e é o roteiro de execução. A preparação atual pode ser aberta por upload no Colab, usando o pacote de
apoio enquanto as mudanças não forem publicadas. Após publicação, use o
[link Colab](https://colab.research.google.com/github/EnzoCaetano015/Fiap-JupyterNotebooks/blob/main/fase6/notebook/EnzoCaetanoPeracioRodrigues_rm570352_pbl_fase6.ipynb).
Esse link aponta para main e só representará esta preparação após seu commit/push;
a execução publicada ainda não foi validada.

## Estrutura

```text
fase6/
├── config/       # contrato YOLO e parâmetros dos experimentos
├── data/         # 80 fotos locais, labels YOLO e metadados de origem
├── docs/         # arquitetura e relatório de validação técnica
├── notebook/     # entrega acadêmica principal
├── results/      # pequenos resultados reais, quando disponíveis
├── requirements.txt
└── .gitignore
```

## Como executar

1. Abra o notebook preparado por upload no Colab e selecione GPU. Se esta
   versão não está publicada, envie o pacote de apoio para /content e use
   USE_SUPPORT_ZIP; caso contrário, use CLONE_REPOSITORY.
2. Envie manualmente dataset_fase6_final.zip para MyDrive/Fiap/Fase6/.
   Monte o Drive e habilite a extração explicitamente. O ZIP e cada membro
   são conferidos pelo manifesto; a pasta existente não será sobrescrita.
3. Confira o diagnóstico ready, as contagens 64/8/8 e o fingerprint. Prepare
   o runtime e execute o preflight mantendo RUN_EXPERIMENTS=False. Se a
   instalação pedir reinício, reinicie e reexecute com instalação desativada.
4. Confira a GPU nos dois frameworks e environment.json. Só então habilite
   START_FINAL_EXPERIMENTS na célula anterior ao treino de 30 épocas.
5. Execute YOLO do zero 30/60, seleção em val, teste do selecionado, COCO e CNN.
   Runs e checkpoints ficam no Drive em experiments/SESSION_NAME; resultados
   pequenos são preservados após cada etapa. Nenhum run existente é sobrescrito.
6. Exporte o ZIP de resultados e baixe o notebook executado pelo menu do Colab.
   Devolva os dois arquivos para revisão e consolidação final.

Leia o [roteiro detalhado](docs/colab_execution.md), incluindo os controles,
recuperação após desconexão e preservação dos artefatos. A Task 11 está
**pronta para upload**; upload e treinamentos serão realizados pelo usuário.

Para execução local, instale as dependências em uma venv isolada:

```bash
python -m pip install -r fase6/requirements.txt
```

Abra o notebook em um ambiente Jupyter e execute as células na ordem apresentada.
As funções são definidas dentro do notebook, sem imports de código local ou
ajustes de `sys.path`. Configurações YAML, documentação e diretórios de dados
continuam como arquivos de apoio. Não há arquivos Python separados nem pasta
de testes na entrega. O smoke test técnico da CNN permanece no notebook.

TensorFlow/PyTorch são importados nas funções que precisam desses frameworks.
Definir funções não inicia treinamento nem baixa pesos. Não instale as
dependências globalmente.

## Dataset

O dataset local tem **80 fotos do Open Images**, 40 de cada classe,
com **32/4/4 por classe** para treino/validação/teste. As fotos passaram por
inspeção visual e têm 80 labels YOLO (91 caixas). As anotações da fonte foram
importadas no Make Sense, revisadas visualmente e corrigidas por Codex via
navegador, e exportadas em YOLO. A revisão alterou 13 imagens; não houve
geração de labels por modelo de detecção. Veja o [registro da revisão](docs/makesense_validation.md).
Veja o [contrato e a proveniência](data/README.md) e a
[tabela de origem e atribuição](data/sources.csv).

O manifesto de classificação vem dos labels e aceita somente uma classe de
interesse por imagem. Fotos e labels estão no projeto, mas continuam ignorados
pelo Git. Para usar no Colab, transfira o dataset ao Drive.

## Abordagens e métricas

- **YOLO customizada:** arquitetura yolov5s, pesos aleatórios, 30/60 épocas,
  imagem 640, batch 16, seed 42, parada antecipada desativada.
- **YOLO padrão:** yolov5s COCO, classes resolvidas pelos nomes, sem treino na base.
- **CNN:** três blocos convolucionais, saída softmax com duas classes, loss sparse
  categorical crossentropy, 224 × 224, batch 8, 30 épocas e augmentation apenas no treino.

YOLO realiza detecção; CNN realiza classificação. **mAP e accuracy não são
grandezas equivalentes.** Precision/recall da detecção também não equivalem
automaticamente aos valores macro da classificação. Tempos e facilidade de uso
podem ser comparados com hardware, tamanhos de entrada e escopo de medição registrados.

O cronômetro usa `perf_counter`, exclui carga de modelo, leitura de arquivos,
warm-up e salvamento. Inclui pré-processamento e execução (NMS na YOLO).
Calcula média e mediana por imagem, e desvio padrão amostral com duas ou mais
imagens. A GPU YOLO é sincronizada e a saída TensorFlow é materializada.

## Resultados — pendentes

| Abordagem | Métrica principal | Resultado | Tempo |
|---|---|---|---|
| YOLO customizada | mAP@0.5:0.95 | Pendente | Pendente |
| YOLO padrão COCO | mAP indisponível neste pipeline de inferência | Pendente | Pendente |
| CNN do zero | Accuracy e F1 macro | Pendente | Pendente |

As tabelas de detecção COCO e seus tempos estarão disponíveis após a inferência.
Confiança de predição não será apresentada como mAP. O pipeline padrão não
calcula mAP com labels customizados 0/1: esse cálculo exigiria remapeamento dos
IDs para COCO. O benchmark preserva esse campo como indisponível.

`results/` permanece vazio enquanto os experimentos não forem executados. Não há métricas nem gráficos
acadêmicos fabricados. As validações técnicas não geram resultados acadêmicos.

## Vídeo demonstrativo

Link: será adicionado após a conclusão dos experimentos.

## Limitações atuais

Dataset integrado localmente e revisado no Make Sense; treinamentos e inferências acadêmicas ainda não executados;
métricas finais, prints, vídeo e conclusões indisponíveis. A execução completa
em Colab/GPU ainda precisa de validação com os dados reais. Não implementamos
ESP32-CAM, Transfer Learning, Fine Tuning ou segmentação.

Veja [arquitetura](docs/architecture.md), [validação técnica](docs/validation.md),
[progresso das tasks](docs/tasks_progress.md), [checklist final](docs/final_checklist.md)
e [roteiro do vídeo](docs/video_script.md).
