# Progresso das tasks 10–22

Data: 02/10/2026. Escopo: preparação para execução pelo usuário no Colab.
As instruções do ZIP de tasks foram confrontadas com o pedido atual e com o
estado real. A numeração abaixo corresponde ao ZIP fase6_codex_tasks_restante.

| Task | Estado real | Evidência / pendência | Sugestão de commit semântico |
|---|---|---|---|
| 10 | Revisão real concluída; evidência de classes complementada | docs/makesense_validation.md | `feat(fase6): registra evidencias de classes no Make Sense` |
| 11 | Pronto para upload; envio manual pendente | config/dataset_package.json; docs/colab_execution.md | `feat(fase6): prepara transferencia verificada do dataset ao Colab` |
| 12 | Preflight implementado e bloqueios testados; GPU real pendente | notebook; environment.json será gerado no Colab | `feat(fase6): adiciona preflight de GPU e registro de ambiente` |
| 13 | Fluxo preparado; 30 épocas reais pendentes | notebook; metrics_30_epochs.json ainda ausente | `feat(fase6): prepara treino YOLO de 30 epocas com preservacao no Drive` |
| 14 | Fluxo preparado; 60 épocas reais pendentes | notebook; metrics_60_epochs.json ainda ausente | `feat(fase6): prepara treino YOLO de 60 epocas com parametros equivalentes` |
| 15 | Seleção e campos preparados; comparação real pendente | notebook; selected_model.json ainda ausente | `feat(fase6): registra selecao YOLO pela validacao e desempate por tempo` |
| 16 | Oito evidências e teste preparados; avaliação real pendente | notebook; results/yolo_custom permanece vazio | `feat(fase6): prepara teste reservado e evidencias da YOLO customizada` |
| 17 | COCO e tempos preparados; inferência real pendente | notebook; results/yolo_standard permanece vazio | `feat(fase6): prepara baseline COCO nas oito imagens de teste` |
| 18 | CNN validada em CPU; treino e teste acadêmicos pendentes | notebook; smoke test sintético (2,2) | `feat(fase6): prepara CNN do zero com checkpoint e evidencias` |
| 19 | Benchmark ampliado; dados e conclusões reais pendentes | notebook; results/comparison permanece vazio | `feat(fase6): amplia benchmark com medianas e tipos de tarefa` |
| 20 | Notebook de execução preparado; versão acadêmica executada pendente | notebook; README; docs/colab_execution.md | `docs(fase6): documenta execucao e devolucao dos resultados reais` |
| 21 | Roteiro preparado; vídeo e URL pendentes | docs/video_script.md | `docs(fase6): prepara roteiro de video de ate cinco minutos` |
| 22 | Auditoria da preparação feita; aceite final pendente | docs/final_checklist.md | `docs(fase6): registra auditoria e pendencias da entrega` |

## Decisões e verificações

- Código permanece no notebook, sem src, tests ou arquivos .py no repositório.
- Upload e execução no Colab serão feitos pelo aluno; nenhum upload automático.
- Dataset e exportações Make Sense reais preservados. Capturas em
  docs/evidencias/makesense; backup e ZIPs locais permanecem ignorados.
- Runtime oficial v7.0, pesos customizados aleatórios e ausência de early stopping.
- Dois workers/SGD/hyp.scratch-low fixos e iguais nos experimentos 30/60.
- Seleção apenas em val, com desempate por duração real e depois épocas.
- Checkpoints ficam no Drive; resultados pequenos têm pacote separado de devolução.
- Validação local: 26 células com ações externas desativadas, ZIP íntegro,
  dataset ready, proteção de extração/sobrescrita, rejeição de imagens ilegíveis
  e labels inválidos, comandos equivalentes, seleção, métricas e tempos.
- Fixtures temporárias e mocks verificaram oito evidências e recuperação;
  nada disso foi salvo em results como resultado acadêmico.
- CNN real construída/compilada em CPU, model.summary e inferência sintética
  com shape (2,2). Outputs do notebook permanecem vazios nesta preparação.
- Alterações exclusivas em fase6; nenhum commit, push ou release realizado.

GPU Colab, compatibilidade conjunta em GPU, durações, métricas reais,
conclusões e entrega acadêmica final ainda dependem da execução devolvida.
Não declarar as tasks 12–20 ou a Task 22 concluídas academicamente nesta etapa.
