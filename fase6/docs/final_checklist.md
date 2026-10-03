# Auditoria da Fase 6 — preparação e pendências finais

Data: 02/10/2026. Estado: **pronto para upload/execução; entrega final pendente**.

## Dataset e Make Sense

- [x] 80 imagens, 40 por classe; 32/4/4 por classe.
- [x] 80 labels válidos, 91 caixas, pares completos e imagens legíveis.
- [x] Exportações reais Make Sense e backup anterior preservados.
- [x] Proveniência, revisão por Codex e limitações documentadas.
- [x] Capturas reais das classes, caixas e exportação.
- [x] ZIP de transferência íntegro; manifesto com SHA-256.
- [ ] Upload de imagens e rotulações ao Drive confirmado pelo usuário.
- [ ] Dataset acessível e validado no Colab.

## Ambiente e experimentos — pendentes de execução real

- [ ] GPU PyTorch/TensorFlow funcionando; environment.json real.
- [ ] YOLOv5 v7.0 preparada e validada no Colab.
- [ ] YOLO 30 épocas completas, best.pt/last.pt/CSV preservados.
- [ ] YOLO 60 épocas completas, mesmos parâmetros/hardware/dataset.
- [ ] Comparação real com best_epoch, métricas, losses e duração.
- [ ] Seleção exclusivamente pela validação e selected_model.json.
- [ ] Teste do selecionado, métricas reais e oito imagens processadas.
- [ ] COCO nas mesmas oito imagens, tempos e detecções observadas.
- [ ] CNN do zero por 30 épocas e melhor checkpoint preservado.
- [ ] CNN: accuracy, precision/recall/F1 macro, curvas e matriz de confusão.
- [ ] Benchmark das quatro dimensões e conclusões com evidências.

## Notebook, documentação e vídeo

- [x] Nome obrigatório e schema Jupyter validado.
- [x] 26 células executadas localmente com ações externas desativadas.
- [x] Smoke test real de CNN em CPU: saída (2,2).
- [x] Roteiro de execução e pacote de devolução preparados.
- [x] Roteiro de vídeo até cinco minutos preparado.
- [ ] Notebook final executado no Colab, outputs reais visíveis, sem traceback.
- [ ] Revisão dos resultados devolvidos e substituição dos textos pendentes.
- [ ] Versão atual publicada pelo usuário; link Colab/GitHub testado.
- [ ] Vídeo gravado, até cinco minutos, publicado não listado e URL conferida.

## Git e entrega

- [x] Código apenas no notebook; sem src, tests ou .gitkeep.
- [x] Fotos/labels, ZIPs, pesos, runs e runtime fora do versionamento.
- [x] Mudanças limitadas a fase6; README raiz e fases anteriores preservados.
- [x] Nenhum treinamento, métrica ou conclusão fictícia em results.
- [ ] Resultados pequenos reais incorporados após conferência.
- [ ] Auditoria final e commit pelo usuário antes do prazo.

Nenhum commit ou push automático. Após a entrega oficial, evite novos commits
conforme orientação da FIAP. O notebook e as instruções estão prontos para
execução; a ausência dos resultados reais e do vídeo impede aceite final.
Veja tasks_progress.md para verificações e sugestões de commit por task.
