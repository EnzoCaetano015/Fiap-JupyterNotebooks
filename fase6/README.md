# FarmTech Solutions — Fase 6

## Visão Computacional

**Enzo Caetano Peracio Rodrigues — RM 570352** · Projeto individual

A FarmTech explora visão computacional. Esta fase compara
YOLOv5 customizada, YOLOv5 padrão pré-treinada em COCO e uma CNN própria treinada
do zero, nas classes `bottle` (0) e `backpack` (1).

O [notebook principal](notebook/EnzoCaetanoPeracioRodrigues_rm570352_pbl_fase6.ipynb)
contém todo o código Python da entrega e é o roteiro de execução. Link direto Colab: será adicionado
após publicação desta versão no GitHub. Abra o notebook pelo GitHub no Colab.

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

1. Abra o notebook no Google Colab. Na preparação, habilite `CLONE_REPOSITORY`
   se necessário e `INSTALL_DEPENDENCIES` na primeira execução. O clone pressupõe
   que esta implementação já foi publicada no repositório.
2. Use Python 3.11 ou 3.12 com as dependências de `requirements.txt`. Se uma
   instalação alterar bibliotecas carregadas, reinicie a sessão e reexecute
   as células. Para validar localmente, use uma venv separada da usada por outras fases.
3. Execute configuração e inspeção. Com o dataset local, o estado esperado é
   `ready`. Sem os arquivos de fotos, a saída é `Dataset ainda não integrado`.
   A CNN pode ser construída e validada com
   um tensor sintético, sem treinar ou produzir resultado acadêmico.
4. As imagens e labels já estão integrados localmente. Para Colab, transfira o
   pacote do dataset ao Drive e extraia a pasta `data/`; esses arquivos estão
   ignorados pelo Git e não acompanham o clone. Habilite `MOUNT_DRIVE`
   e ajuste `DRIVE_DATASET`, ou use a variável de ambiente `FASE6_DATASET`.
   A pasta deve conter `train`, `val` e `test`, cada uma com `images` e `labels`.
5. Somente após a validação, habilite `RUN_EXPERIMENTS`. O preparo explícito
   da YOLO clona o runtime oficial `v7.0` em `.runtime/yolov5` e instala suas
   dependências, com PyTorch 2.5.1, torchvision 0.20.1 e setuptools abaixo de 81.
   Os mosaicos internos antigos do YOLO ficam desativados para compatibilidade
   com Pillow moderno; gráficos e bounding boxes são gerados pelas funções do notebook. O modelo COCO
   baixa pesos oficiais na primeira carga, quando a execução é habilitada.
6. Execute 30/60 épocas com pesos aleatórios, mantendo os outros parâmetros.
   Escolha pela validação (mAP50_95, mAP50, menor duração em épocas para desempate)
   e só depois execute o teste do selecionado. Execute COCO e CNN no mesmo teste.
7. Gere tabelas, gráficos, evidências e conclusões usando apenas resultados reais.
   Treinos existentes não são sobrescritos: use outro diretório de saída ou
   arquive conscientemente o experimento anterior. Para a CNN, preserve os
   resultados anteriores antes de remover localmente seu diretório `runs/cnn`.

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
inspeção visual e têm 80 labels YOLO (91 caixas) convertidos das anotações
da fonte. Não houve rotulação manual no Make Sense nem geração por modelo.
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

Dataset integrado localmente; treinamentos e inferências acadêmicas ainda não executados;
métricas finais, prints, vídeo e conclusões indisponíveis. A execução completa
em Colab/GPU ainda precisa de validação com os dados reais. Não implementamos
ESP32-CAM, Transfer Learning, Fine Tuning ou segmentação.

Veja [arquitetura](docs/architecture.md) e [validação técnica](docs/validation.md).
