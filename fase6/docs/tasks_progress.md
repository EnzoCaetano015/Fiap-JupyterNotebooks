# Progresso das tasks 10–22

Atualizado em 13/10/2026. O aluno autorizou upload e execução pelo Codex;
treinos/inferências reais foram feitos no Colab. Código exclusivamente no notebook.

| Task | Estado real | Evidência / pendência | Sugestão de commit semântico |
|---|---|---|---|
| 10 | Revisão real concluída | docs/makesense_validation.md | `feat(fase6): registra revisao e evidencias do Make Sense` |
| 11 | Upload/extração conferidos | config/dataset_package.json; fingerprint real | `feat(fase6): integra dataset verificado no Drive e Colab` |
| 12 | GPU real comprovada | results/environment.json; cuDNN isolada | `fix(fase6): garante compatibilidade GPU entre TensorFlow e PyTorch` |
| 13 | 30/30 épocas concluídas | metrics_30_epochs.json; history; recuperação sem novo treino | `feat(fase6): registra treino YOLO de 30 epocas e recuperacao de metricas` |
| 14 | 60/60 épocas concluídas | metrics_60_epochs.json; opts equivalentes | `feat(fase6): registra treino YOLO de 60 epocas com parametros equivalentes` |
| 15 | Seleção real em validação | selected_model.json; melhor época 59 | `feat(fase6): consolida comparacao e selecao YOLO pela validacao` |
| 16 | Teste real concluído; evidência positiva das classes não demonstrada | test_metrics.json; 8 imagens sem deteccoes a 0,25 | `feat(fase6): registra teste reservado e limitacoes da YOLO customizada` |
| 17 | COCO real concluída; backpack sem detecção | 8 evidencias; detections.csv; mAP indisponivel | `feat(fase6): consolida baseline COCO e falhas observadas` |
| 18 | CNN real 30/30; teste 7/8 | training.json; metrics.json; matriz e curvas | `feat(fase6): consolida CNN do zero e avaliacao real` |
| 19 | Benchmark e análise reais | final_benchmark.csv; results_analysis.md | `feat(fase6): consolida benchmark com metricas distintas por tarefa` |
| 20 | Notebook consolidado; publicação GitHub pendente | outputs reais; controles resetados; README | `docs(fase6): documenta notebook executado e resultados reais` |
| 21 | Roteiro pronto; vídeo/URL pendentes | docs/video_script.md | `docs(fase6): prepara roteiro de video com resultados reais` |
| 22 | Auditoria técnica feita; aceite parcial | docs/final_checklist.md; audit/final_audit.json | `docs(fase6): registra auditoria final e requisitos nao comprovados` |

## Decisões, verificações e limitações

- 27 células da preparação e 30 células finais executadas localmente com ações externas False;
  fixtures temporárias/mocks cobriram configurações, labels, dataset vazio,
  manifesto, ZIP seguro, comandos, filtros, métricas, timers e recuperação.
- CNN real construída/compilada em CPU, model.summary e inferência sintética (2,2).
  A validação técnica não foi usada como resultado acadêmico.
- Runtime 2026.07/Python 3.12.13, Tesla T4; GPU Torch e convolução TF comprovadas.
  JAX opcional removido no Colab; cuDNN 8 isolada, cuDNN 9 Torch preservada.
- Official YOLOv5 v7.0 fixado; pesos iniciais vazios, SGD, workers 2,
  hyp.scratch-low, 640, batch 16, seed 42, patience 0. Opções brutas equivalentes,
  exceto epochs/name e save_dir derivado. CSVs reais com 30/60 épocas.
- NomeError na coleta após treino 30 completo corrigido; duração original
  recuperada de perf_counter e persistida, sem fabricar tempo ou refazer treino.
- Seleção exclusiva por val: 60 épocas, checkpoint da época 59. Teste reservado
  comum de oito imagens, hashes/fingerprint e configuração conferidos.
- COCO sem mAP neste pipeline; CNN accuracy/F1 macro separados de mAP.
  16 imagens YOLO, curvas e matriz reais; painel adicional derivado no Jupyter local.
- 41 arquivos originais conferidos por CRC/SHA-256 e mantidos sem alterar métricas.
  Auditoria/manifestos e revisão qualitativa são acréscimos identificados.
- Notebook nbformat/AST validado, sem error outputs; outputs reais preservados,
  controles externos resetados False. Pesos/runs privados no Drive e ignorados.
- Evidência positiva de mochila nas YOLOs não foi demonstrada; não declarar
  detecções positivas das duas classes nem aceite completo desse requisito.
- Roteiro de vídeo pronto; gravação/publicação/URL dependem do aluno.
- Alterações apenas em fase6; README raiz/fases anteriores preservados.
  Nenhum commit, push ou release automático.

Sugestão da entrega: `feat(fase6): consolida experimentos reais e resultados de visao computacional`.

## Melhoria complementar solicitada em 13/10/2026

Seção 15 preparada com fine tuning COCO 30/60, nova sessão, validação por classe
e IoU, seleção por val e teste bloqueado antes de demonstração das duas classes.
35 células locais executadas sem ações externas; CNN CPU (2,2) preservada.
Testes temporários conferiram correspondência única, duplicatas, classe incorreta,
limiar, IoU e comandos. Nenhum treino novo nem métrica acadêmica nova.
Conexão GPU/uso de pesos COCO bloqueados pela revisão automática até aprovação
específica. O aceite deste objetivo de melhoria continua pendente.
Veja model_improvement.md.
Commit sugerido: `feat(fase6): prepara melhoria YOLO com validacao por classe e IoU`.


## Melhoria complementar concluída

Fine tuning 30/60 concluído em 13/10/2026; seleção em val de 60
épocas, checkpoint 58. Teste comum observado demonstrou
as duas classes com IoU >=0,5/confiança >=0,25. Resultados originais preservados.
Arquivos: notebook seção 15, results/yolo_improved, docs/model_improvement.md,
README e análise atualizados. Manifesto/CSVs/callbacks/checkpoints conferidos;
nenhuma inferência sintética tratada como acadêmica. Vídeo/URL seguem pendentes.
Commit sugerido: `feat(fase6): melhora deteccao das duas classes com fine tuning validado`.

## Validação final da melhoria

36 células de código da entrega executadas localmente com controles externos
False; nenhuma instalação, Drive, GPU ou novo treinamento nessa validação.
Contagens de IoU/TP/FP/FN de val/test recalculadas diretamente dos labels
Make Sense imutáveis e das predições reais, correspondendo aos CSVs exportados.
41 arquivos originais e 46 arquivos do pacote complementar conferidos por SHA-256.
Painel real executado no Colab, com FN e FP destacados; nenhum resultado removido.
Diff só fase6 e git diff --check aprovado; dados brutos/pesos/runs ignorados.
Commit sugerido: `feat(fase6): melhora deteccao das duas classes com fine tuning validado`.
