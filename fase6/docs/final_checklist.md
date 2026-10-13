# Auditoria da Fase 6

13/10/2026: execução e consolidação concluídas; **aceite final parcial**.

## Dataset e ambiente

- [x] 80 imagens, 40 por classe, 32/4/4; 80 labels válidos e 91 caixas.
- [x] Exportações Make Sense, backup, capturas e autoria Codex preservados.
- [x] Upload, SHA-256, extração e fingerprint no Colab conferidos.
- [x] GPU PyTorch/TensorFlow comprovada; environment.json real.
- [x] YOLOv5 oficial v7.0 e commit fixado, arquivos essenciais conferidos.

## Experimentos reais

- [x] YOLO 30/30 e 60/60 épocas, parâmetros equivalentes e sem early stopping.
- [x] CSVs, checkpoint hashes, melhores épocas 30/59, losses e durações reais.
- [x] best.pt/last.pt e runs preservados no Drive, fora do Git.
- [x] Comparação e seleção exclusivamente em validação; selected_model.json.
- [x] Teste apenas da selecionada; ComputeLoss/FP32; oito imagens processadas.
- [x] COCO nas mesmas oito imagens; tempos e detecções, mAP indisponível.
- [x] CNN 30/30; melhor checkpoint val_loss época 29; teste 7/8.
- [x] Curvas, matriz, predições, benchmark e análise real das limitações.
- [x] Evidência positiva das duas classes no fine tuning complementar: 5 garrafas
      e 3 mochilas corretas por IoU. Baselines originais continuam com suas falhas.

## Notebook e documentação

- [x] Nome obrigatório, schema nbformat e código AST válidos.
- [x] 30 células finais executadas localmente sem ações externas; CNN real CPU (2,2).
- [x] Outputs reais GPU e revisão qualitativa local identificada, sem traceback.
- [x] 41 arquivos originais conferidos por CRC/SHA-256, métricas inalteradas.
- [x] Resultados pequenos reais incorporados e controles externos False.
- [x] README, análise, instruções e roteiro até cinco minutos atualizados.
- [ ] Vídeo gravado, duração até 5 min, publicação não listada e URL conferida.
- [ ] Commit/push pelo aluno e link público GitHub/Colab verificado.

## Escopo e honestidade da entrega

- [x] Código somente no notebook; sem src, tests, .py ou .gitkeep.
- [x] Fotos/labels brutos, ZIPs, pesos, runs, runtime e ambientes ignorados.
- [x] Diff somente fase6; README raiz e fases anteriores preservados.
- [x] Nenhum resultado fictício, nenhuma inferência nova na consolidação.
- [x] Confiança não tratada como precisão; accuracy e mAP separados.
- [x] Sugestões de commit por task; nenhum commit/push/release automático.

Não declarar Task 22 integralmente aceita enquanto vídeo/publicação não estiverem comprovados. As duas classes foram
demonstradas no experimento complementar, preservando as falhas dos baselines. Melhorar
as detecções exige novo experimento autorizado e identificado, sem substituir
silenciosamente estes resultados. Revisão independente dos labels é melhoria futura.

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

## Verificação complementar posterior

- [x] Fine tuning COCO autorizado e executado por 30/60 épocas na T4.
- [x] Seleção exclusiva por validação; mesmos dados/splits, hashes conferidos.
- [x] Detecções corretamente localizadas de bottle e backpack no experimento complementar.
- [x] Fonte/manifesto, épocas completas, opções equivalentes e métricas por classe auditados.
- [x] Resultados/outputs do zero e CNN preservados; melhoria identificada como fine tuning.
- [x] Teste adicional tratado como retrospectivo; sem alegação de novo teste cego.
- [ ] Vídeo/URL e publicação GitHub pelo aluno continuam pendentes.

A ausência de mochilas nos baselines originais permanece um resultado real.
A evidência positiva das duas classes agora existe no detector complementar;
ela não transforma os baselines do zero em modelos com esse desempenho.
