# Execução no Colab e devolução dos resultados

## Checkpoint atual

Preparação concluída e validada localmente. Você fará o upload e executará o
notebook. Nenhum treinamento acadêmico, preflight em GPU ou upload ao Drive
foi realizado por Codex nesta rodada. Não é uma entrega acadêmica final.

## Arquivos preparados

- `dataset_fase6_final.zip`: 80 imagens e 80 labels revisados no Make Sense,
  com proveniência. Envie para `MyDrive/Fiap/Fase6/` pelo Google Drive.
- `fase6_colab_preparacao.zip`: arquivos de apoio atualizados, sem dataset,
  pesos, runs ou runtime. É uma alternativa ao clone enquanto estas mudanças
  locais ainda não estiverem publicadas no GitHub.
- `EnzoCaetanoPeracioRodrigues_rm570352_pbl_fase6.ipynb`: abra por upload no Colab.

O manifesto versionado está em `config/dataset_package.json`, com tamanho,
SHA-256 de cada membro e fingerprint das fotos/labels. O notebook confere o
ZIP antes de extraí-lo e compara o dataset com a revisão aprovada.

## Ordem de execução

1. Abra o notebook preparado no Colab e escolha **Ambiente de execução >
   Alterar tipo de ambiente de execução > GPU**.
2. Se a preparação ainda não está no GitHub, envie `fase6_colab_preparacao.zip`
   pelo painel Arquivos do Colab, ficando em `/content/`. Na primeira célula
   de código, habilite `USE_SUPPORT_ZIP=True`. Se a versão já está publicada,
   use `CLONE_REPOSITORY=True`. Ative `INSTALL_DEPENDENCIES=True` na instalação
   inicial. Um reinício de runtime exige reexecutar a configuração; arquivos
   enviados para `/content/` podem precisar ser reenviados.
3. Envie manualmente o dataset ao Drive. Na configuração, deixe
   `RUN_EXPERIMENTS=False`; habilite `MOUNT_DRIVE=True`. Para a primeira
   extração, use `EXTRACT_DATASET=True`. Depois de extrair, volte esse controle
   para False, pois a pasta existente não será sobrescrita. Se você já enviou
   a pasta data extraída, não habilite a extração. `FASE6_DATASET` tem prioridade
   sobre o caminho sugerido `/content/drive/MyDrive/Fiap/Fase6/data`.
4. Execute até o diagnóstico e confira `ready`, 64/8/8, 32/4/4 por classe,
   fingerprint correto, imagens legíveis e ausência de pares inválidos.
5. Habilite `PREPARE_YOLO=True`, `INSTALL_YOLO_DEPENDENCIES=True` e
   `RUN_PREFLIGHT=True`. Execute a preparação do runtime antes de gastar GPU
   nos treinos. Se houver necessidade de reinício após instalação, reinicie,
   refaça a configuração e use `INSTALL_DEPENDENCIES=False` e
   `INSTALL_YOLO_DEPENDENCIES=False`. A GPU deve funcionar no PyTorch e no
   TensorFlow, incluindo uma operação e uma convolução sintética de diagnóstico.
6. Confira `environment.json`. Na célula imediatamente anterior ao treino de
   30 épocas, altere `START_FINAL_EXPERIMENTS=True`. Essa célula habilita os
   experimentos sem reinicializar os dados do preflight. Continue pelas células
   de 30 épocas, 60 épocas, seleção, teste customizado, COCO e CNN.
7. Examine os resultados e execute o benchmark. Todas as oito imagens de teste
   devem aparecer nas tabelas e grades, inclusive quando não há detecções.
8. Depois de concluir, habilite `EXPORT_RESULTS=True` na configuração e
   execute somente a célula final de exportação. Não reexecute a célula de
   configuração durante uma execução ativa: ela reinicializa os controles.
   Para alterar apenas esse controle, execute uma nova célula com
   `EXPORT_RESULTS = True` e, se quiser baixar, `DOWNLOAD_RESULTS = True`.
   O ZIP final fica no Drive, junto à sessão, sem pesos ou dataset bruto.
9. Baixe o notebook executado em **Arquivo > Fazer download > Fazer download
   do .ipynb**. Devolva o notebook e `fase6_resultados_<SESSION_NAME>.zip` para
   revisão das métricas, conclusões, README e auditoria.

## Preservação e recuperação

Sessão padrão: `MyDrive/Fiap/Fase6/experiments/fase6_final_001/`.
Os checkpoints `.pt` e `.keras`, CSVs brutos e runs ficam diretamente nesse
local. Resultados consolidados são copiados após cada etapa concluída.
Nenhum desses artefatos pesados entra no Git.

Se a sessão desconectar depois de um treinamento concluído, use o mesmo
`SESSION_NAME`, `RESTORE_RESULTS=True`, extração e instalação desativadas,
e refaça o preflight. GPU, versões, revisão YOLO e dataset precisam coincidir;
caso contrário, o notebook interrompe a comparação. As etapas concluídas são
recuperadas com conferência dos hashes dos checkpoints. Runs interrompidos
não são retomados automaticamente. Preserve a sessão e use outra sessão,
com uma cópia limpa do repositório, para repetir os dois experimentos.
Não apague runs para contornar as proteções de sobrescrita.

## Resultados e análise

A YOLO customizada usa v7.0, yolov5s, pesos vazios, seed 42, batch 16, imagem
640, SGD, dois workers, hyp.scratch-low e patience 0. Só épocas/nome mudam
entre os treinos. O agendamento de learning rate depende do total de épocas.
Seleção: mAP50_95 de validação, mAP50, menor tempo real e menos épocas, com
igualdade numérica sem tolerância arbitrária. O teste não seleciona o modelo.
A CNN usa 224x224, batch 8, 30 épocas e checkpoint por menor val_loss.

COCO não recebe treino na base e não tem mAP calculado neste pipeline.
Confiança não substitui precision ou mAP. mAP e accuracy têm tarefas distintas.
Tempos incluem pré-processamento e modelo/NMS, mas excluem carga do modelo,
leitura de arquivos, warm-up e salvamento. Todas as métricas finais devem
ser discutidas com o teste pequeno e as limitações da anotação de foco.

O teste customizado usa val.run oficial com o modelo não fundido, dataloader
do split reservado e ComputeLoss, em FP32. As losses são efetivamente calculadas;
zeros de inicialização de uma avaliação sem ComputeLoss não são tratados
como métricas. A execução real desse adaptador em GPU permanece pendente.

A melhor época é registrada pelo callback oficial `on_model_save` quando o YOLOv5 grava `best.pt`, evitando inferir empates a partir do CSV arredondado. O treino usa `train.main` e os mesmos argumentos oficiais, sem alterar a implementação do YOLOv5. Referências: [treinamento v7.0](https://github.com/ultralytics/yolov5/blob/v7.0/train.py) e [callbacks v7.0](https://github.com/ultralytics/yolov5/blob/v7.0/utils/callbacks.py).
