# Coleta e integração do dataset da Fase 6

Data: 02/10/2026. As imagens foram coletadas e salvas conforme pedido atual
do usuário, que amplia o escopo anterior de preparação sem dataset.

## Entrega

- 80 fotos reais: 40 bottle e 40 backpack.
- 64 imagens no treino, 8 na validação e 8 no teste: 32/4/4 por classe.
- 80 labels YOLO, totalizando 91 bounding boxes.
- Fotos JPEG em `fase6/data/{train,val,test}/images/`.
- Labels TXT correspondentes em `fase6/data/{train,val,test}/labels/`.
- Metadados em `data/sources.csv`, `annotations_source.json` e
  `dataset_summary.json`; README e notebook atualizados para o dataset integrado.
- Pacote de transferência `dataset_fase6.zip`: 17,41 MB, com fotos, labels,
  contrato e metadados de atribuição. Extrair a pasta data no Drive para Colab.
- Contact sheets das 40 fotos de cada classe disponíveis junto ao pacote.

Não há arquivos Python separados, pasta src ou pasta tests na entrega.
Resultados de modelos continuam pendentes; results permanece vazio.

## Fonte e seleção

Usada a skill vercel:agent-browser para consultar os downloads oficiais do
[Open Images](https://storage.googleapis.com/openimages/web/download_v7.html).
O download seletivo usou o bucket público `open-images-dataset`, conforme
o [downloader oficial](https://github.com/openimages/dataset/blob/master/downloader.py).
Os metadados de classes, imagens, bounding boxes e labels humanamente verificados
foram baixados dos links oficiais observados no navegador.

IDs resolvidos por nome: Bottle `/m/04dr76w` e Backpack `/m/01940j`.
Imagens com ambas as classes anotadas, grupos, desenhos e anotações inside
foram excluídas. A inspeção visual descartou latas, potes, malas, bolsas de
ombro e enquadramentos inadequados presentes entre os candidatos da fonte.
Foram preservadas as caixas existentes para os objetos selecionados.

As 80 fotos selecionadas são de 79 autores. São 75 imagens originalmente
do split test e 5 do validation do Open Images. Os splits locais 32/4/4 foram
definidos com seed 42; autor repetido foi mantido somente no treino.
Os splits do projeto não representam o benchmark oficial do Open Images.

## Licença e anotações

Metadados da fonte informam CC BY 2.0 para as fotos; anotações são disponibilizadas
pelo Open Images em CC BY 4.0. Autor, título, perfil, página original e licença
informada estão registrados para cada imagem em sources.csv. Esses registros
não representam uma auditoria da licença atual de cada página Flickr;
consulte as URLs originais caso vá redistribuir as fotos publicamente.

As fotos foram copiadas dos JPEGs do bucket oficial, sem recorte ou edição
de pixels na coleta. As caixas foram convertidas de xyxy normalizado para
centro/largura/altura YOLO com IDs locais 0/1; não são predições de modelo.
Não houve rotulação manual no Make Sense. Caso essa ferramenta seja exigida
pela atividade, revise os labels nela e registre as evidências requeridas.

## Verificação real executada

- Schema Jupyter validado; outputs continuam vazios no notebook entregue.
- As 22 células de código executaram em sequência com RUN_EXPERIMENTS=False:
  dataset ready, manifesto com 80 linhas, nenhum download de pesos ou treinamento.
- 80 JPEGs decodificados/verificados com Pillow; SHA-256 conferido contra sources.csv.
- 80 hashes distintos; nenhum autor compartilhado entre splits do projeto.
- Labels lidos pelo validador do notebook: classes 0/1, coordenadas válidas,
  quantidade de caixas consistente e nenhuma imagem sem label.
- Todas as seis contagens por classe/split correspondem a 32/4/4.
- CNN construída e compilada em CPU; saída sintética (1,2).
- ZIP verificado: 80 JPGs, 80 TXTs, integridade CRC sem falha.
- git check-ignore confirmou que as 80 fotos e 80 labels continuam ignorados.
- git diff confirmou README raiz e fases 3, 4 e 5 sem alterações.
- Nenhum peso ou resultado acadêmico fictício adicionado.

## Próximos passos

Para o ambiente local, o dataset já está integrado. Para Colab, transfira o ZIP
ao Drive, extraia data/ e configure o caminho no notebook. Depois execute os
treinamentos YOLO 30/60 e CNN, inferências, métricas, gráficos, conclusões,
prints e vídeo. Esses experimentos não foram executados nesta coleta.

As fotos e labels estão presentes no projeto local, mas não acompanham
commit/push por estarem ignorados. Os arquivos de configuração, documentação
e atribuição são versionáveis. Nenhum commit ou push foi executado.

Commit sugerido para esta etapa:
`feat(fase6): integra dataset de garrafas e mochilas com labels e proveniência`
