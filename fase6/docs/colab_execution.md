# Execução e preservação no Colab

Estado em 13/10/2026: upload e experimentos concluídos; notebook consolidado
com outputs reais. [Abrir notebook](https://colab.research.google.com/drive/1tOPqLqF--WRhIR8VweO8-4SQi4PKFW-j). Não é necessário treinar novamente
para entregar estes resultados. Para revisar, leia outputs e docs/results_analysis.md.

## Arquivos existentes no Drive

Pasta: `/content/drive/MyDrive/Faculdade/Fiap/Fase6`.
- dataset_fase6_final.zip: 18.258.978 bytes; SHA-256
  `51a01c51862133478be8927768c61364411cd137a893fe62171c281ecffb59fd`.
- fase6_colab_preparacao.zip: pacote original do bootstrap; SHA-256
  `23204e81b58c1c2bd900fbe366a2a42bb7b1c68ed2e6b6a8178604b15ea00349`.
- data: 80 imagens/80 labels, 91 caixas, 64/8/8.
- experiments/fase6_final_001: runs e checkpoints YOLO/CNN, environment.json,
  resultados e ZIP original. O pacote revisado acrescenta auditoria e painel.

Preserve esses arquivos. Pesos e runs permanecem no Drive; não os inclua no Git.
O pacote de apoio original não foi substituído: seu hash é usado no bootstrap.
As funções atualizadas estão no notebook consolidado.

## Se precisar reproduzir em uma NOVA sessão

1. Abra uma cópia do notebook; os outputs existentes são históricos reais.
   Escolha GPU T4 e versão do runtime **2026.07** (Python 3.12.13), cuja
   compatibilidade foi comprovada. Se indisponível, valide outro runtime antes
   de habilitar treinos; não reduza épocas ou parâmetros para contornar falhas.
2. Habilite MOUNT_BOOTSTRAP_DRIVE na primeira célula para autenticar e copiar o
   pacote original conferido. Na preparação, habilite USE_SUPPORT_ZIP. Alternativa:
   clone somente após publicar a versão atual. Configure DRIVE_BASE/DRIVE_DATASET
   ou FASE6_DATASET se usar outra pasta.
3. Instale requirements com INSTALL_DEPENDENCIES. REMOVE_UNUSED_COLAB_JAX remove
   jax/jaxlib opcionais somente do runtime temporário: a versão pré-instalada
   conflitou com ml_dtypes do TensorFlow 2.17. Reinicie Python quando necessário;
   reexecute definições com instalações já concluídas desativadas.
4. Habilite INSTALL_TF_GPU_LIBRARIES uma vez. cuDNN 8.9.7.29 é instalada isolada
   em fase6/.runtime/tf_cudnn, sem substituir cuDNN 9 do PyTorch. O preflight
   importa PyTorch, carrega as bibliotecas locais e só então importa TensorFlow.
   RUN_ISOLATED_GPU_DIAGNOSTIC é opcional; ele verifica operação Torch e convolução TF.
5. Na configuração, MOUNT_DRIVE=True; mantenha EXTRACT_DATASET=False se data já
   existe. Extração explícita somente para destino inexistente, com manifesto,
   CRC, SHA-256 e proteção contra caminhos inseguros. Confira status ready,
   classes, pares, legibilidade, distribuição e fingerprint.
6. Use SESSION_NAME **novo** para novos experimentos. PREPARE_YOLO=True,
   INSTALL_YOLO_DEPENDENCIES=True na instalação inicial e RUN_PREFLIGHT=True,
   mantendo RUN_EXPERIMENTS=False. Confirme v7.0/commit oficial, arquivos essenciais,
   GPU em ambos os frameworks e environment.json. Sem GPU, o fluxo bloqueia.
7. Após conferir preflight, START_FINAL_EXPERIMENTS=True. Execute 30 épocas,
   60 épocas, seleção em val, teste apenas do selecionado, COCO, CNN 30 épocas,
   avaliação, painel e benchmark. Não altere hiperparâmetros entre YOLOs.
8. EXPORT_RESULTS=True exporta apenas resultados pequenos; DOWNLOAD_RESULTS
   é opcional. Salve também o notebook executado. Não reutilize o nome da sessão
   de referência para novos treinos e não sobrescreva checkpoints.

Todos esses controles estão False na entrega consolidada. Os outputs preservados
foram produzidos com os controles necessários habilitados durante a execução.

## Recuperação da sessão existente

Para visualizar resultados, prefira o notebook e o pacote consolidado. Para
recuperar no Colab, refaça preparação/definições/preflight com SESSION_NAME
fase6_final_001 e RESTORE_RESULTS=True antes das células de experimentos.
O fluxo valida configuração, hardware, fingerprint, checkpoint e quantidade
de épocas; não presume que um treino interrompido esteja completo.
RECOVER_COMPLETED_30 é uma célula técnica da execução original, desativada:
ela recuperou o tempo real após uma falha de coleta; não estima tempo.
Os treinos foram concluídos uma vez, sem repetição após a correção.

## Compatibilidade comprovada

Colab 2026.07, Python 3.12.13, Tesla T4, Torch 2.5.1+cu124/CUDA 12.4/cuDNN 9,
TensorFlow 2.17.1 (build CUDA 12.3/cuDNN 8), cuDNN local 8.9.7.29.
Ambos os testes reais GPU passaram antes dos treinos. Referências:
[runtimes Colab](https://research.google.com/colaboratory/runtime-version-faq.html),
[builds TensorFlow](https://www.tensorflow.org/install/source#gpu).
Não foi alterada a venv Python 3.14 do repositório nem o ambiente global.

## Sua parte restante

Confira o notebook e as limitações, grave o roteiro de até cinco minutos,
publique como não listado e forneça URL/duração. Depois revise o diff, faça
commit/push e confira o link público. Não compartilhe pesos, credenciais ou
autorização do Drive para gravar. Nenhum commit/push foi automatizado.


## Experimento complementar das duas classes

Seção 15: fine tuning COCO executado, sessão fase6_transfer_001, resultados reais
preservados. Não substitui o estudo original do zero. Helpers precedem o setup;
reutilize definições sem rodar novamente treinos originais. Dados locais SSD
vieram do ZIP original conferido. Instalação inicial/reinício foram necessários;
flags agora False. Runs/weights existentes não são sobrescritos; arquivo execution.json
e CSV/callback permitem recuperar etapas concluídas. Não reavaliar o teste para
escolher ajustes; seu uso adicional é retrospectivo. Veja model_improvement.md.
