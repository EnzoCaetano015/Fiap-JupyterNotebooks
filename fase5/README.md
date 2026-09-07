# FarmTech Solutions — Fase 5

## Sobre o projeto

Esta entrega evolui o projeto FarmTech Solutions com uma análise de Machine Learning aplicada ao rendimento agrícola. O trabalho utiliza o dataset oficial `crop_yield.csv` e reúne análise exploratória, clusterização e modelos de regressão em um notebook Jupyter reproduzível.

**Aluno:** Enzo Caetano Peracio Rodrigues  
**RM:** 570352

## Entrega 1 — Machine Learning

### Dataset

O arquivo `data/crop_yield.csv` contém 156 registros de quatro culturas e relaciona o rendimento a precipitação, temperatura, umidade relativa e umidade específica.

O conjunto foi analisado sem criação de dados ou alvos sintéticos. As 39 combinações ambientais foram mantidas agrupadas durante as separações de treino, teste e validação cruzada.

### Objetivos

- Explorar a qualidade, as distribuições e as relações presentes nos dados.
- Investigar outliers sem remover cenários agrícolas válidos automaticamente.
- Identificar tendências de produtividade por clusterização.
- Comparar cinco algoritmos de regressão.
- Selecionar um modelo com holdout e validação cruzada de cinco folds.

### Técnicas utilizadas

- Pandas, NumPy, Matplotlib e Seaborn.
- Análise exploratória e método IQR.
- KMeans, Elbow Method, Silhouette Score e PCA para visualização.
- `ColumnTransformer`, `OneHotEncoder`, `StandardScaler` e `Pipeline`.
- Regressão Linear, Árvore de Decisão, Random Forest, Gradient Boosting e KNN.
- KFold, `cross_validate` e `GridSearchCV`.

### Notebook Jupyter

O relatório técnico completo, incluindo código, gráficos, métricas, conclusões e limitações, está disponível em:

[Abrir notebook da Entrega 1](notebook/EnzoCaetanoPeracioRodrigues_rm570352_pbl_fase4.ipynb)

### Como executar

Execute os comandos a partir da pasta `fase5/`.

```bash
python -m venv .venv
```

Ative o ambiente virtual.

No Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

No Linux ou macOS:

```bash
source .venv/bin/activate
```

Instale as dependências e inicie o Jupyter:

```bash
pip install -r requirements.txt
jupyter notebook
```

Abra `notebook/EnzoCaetanoPeracioRodrigues_rm570352_pbl_fase4.ipynb` e execute todas as células em ordem.

### Principais resultados

- O dataset não possui valores ausentes ou linhas duplicadas.
- O óleo de palma apresenta rendimento muito superior às demais culturas; por isso, os 35 outliers globais de rendimento foram mantidos após análise por cultura.
- A clusterização selecionou `k=8`, com Silhouette Score de `0,391`, separando três perfis de alta produtividade de óleo de palma e cinco perfis ambientais compartilhados pelas demais culturas.
- O Gradient Boosting ajustado foi selecionado como modelo final, com RMSE médio de validação cruzada de `7.254,12`, RMSE de teste de `7.920,47` e R² de teste de `0,9884`.

Os resultados devem ser interpretados considerando o tamanho reduzido do conjunto e a ausência de informações temporais, geográficas e de manejo agrícola.

### Vídeo demonstrativo

[Vídeo da Entrega 1 — Machine Learning](https://youtu.be/qyWgyC9aXxg)

## Entrega 2 — Cloud Computing com AWS

### Cenário

Esta entrega compara o custo mensal de uma instância Amazon EC2 executada continuamente em duas regiões: América do Sul (São Paulo) e Leste dos EUA (N. da Virgínia). A consulta foi realizada na AWS Pricing Calculator em 6 de setembro de 2026.

### Configuração analisada

O mesmo perfil técnico foi utilizado nas duas regiões para permitir uma comparação direta:

- uma instância EC2 `t3.micro` de geração atual;
- Linux e locação compartilhada;
- 2 vCPUs, 1 GiB de memória e rede de até 5 Gigabits;
- cobrança On-Demand com 100% de utilização, equivalente a 730 horas mensais;
- volume EBS SSD de uso geral `gp3` com 50 GB;
- sem snapshots, monitoramento detalhado, transferência de dados ou custos adicionais.

### Região São Paulo

Na região América do Sul (São Paulo), código `sa-east-1`, a instância EC2 custa **US$ 12,264 por mês** e o volume EBS custa **US$ 7,60 por mês**, resultando no total estimado de **US$ 19,86 por mês**.

### Região N. Virginia

Na região Leste dos EUA (N. da Virgínia), código `us-east-1`, a instância EC2 custa **US$ 7,592 por mês** e o volume EBS custa **US$ 4,00 por mês**, resultando no total estimado de **US$ 11,59 por mês**.

### Comparativo de custos

| Região | EC2 On-Demand | EBS gp3 (50 GB) | Total mensal |
|---|---:|---:|---:|
| São Paulo (`sa-east-1`) | US$ 12,264 | US$ 7,60 | **US$ 19,86** |
| N. da Virgínia (`us-east-1`) | US$ 7,592 | US$ 4,00 | **US$ 11,59** |

A diferença mensal entre as regiões é de **US$ 8,27**. Em relação à opção mais barata, São Paulo custa **71,35% a mais**; de forma equivalente, N. da Virgínia custa **41,64% menos** que São Paulo.

### Opção mais barata

Considerando somente os recursos incluídos na estimativa, **N. da Virgínia é a opção mais barata**, com economia mensal de US$ 8,27. Os valores são estimativas em dólares, não incluem impostos e podem variar conforme o preço vigente e o uso real.

### Escolha considerando restrição de armazenamento no exterior

Se o cenário estabelece uma restrição legal que impede o armazenamento dos dados no exterior, a escolha adequada é **São Paulo**, mesmo com o custo superior. Essa decisão mantém a residência dos dados no Brasil e atende à restrição informada no enunciado.

Além disso, uma região fisicamente mais próxima dos sensores instalados no Brasil pode reduzir a latência e favorecer o acesso rápido aos dados agrícolas. Essa vantagem depende da conectividade e da arquitetura completas, mas reforça São Paulo como escolha técnica para o cenário. O custo mensal maior representa o trade-off para cumprir a restrição de armazenamento e aproximar o processamento da origem dos dados.

Essa justificativa se baseia na restrição específica apresentada pelo cenário; ela não pressupõe que a LGPD determine que todos os dados devam permanecer no Brasil.

### Evidências

Os cálculos detalhados estão documentados em [Comparativo de custos AWS](docs/aws/comparativo_aws.md).

São Paulo:

- [Região, locação e Linux](assets/aws/sao-paulo/configuracao-regiao-linux.png)
- [EC2 On-Demand e utilização](assets/aws/sao-paulo/on-demand-ec2.png)
- [EBS gp3 com 50 GB](assets/aws/sao-paulo/ebs-gp3-50gb.png)
- [Cálculo do EBS e total](assets/aws/sao-paulo/calculo-ebs-total.png)

N. da Virgínia:

- [Região, locação e Linux](assets/aws/virginia-norte/configuracao-regiao-linux.png)
- [EC2 On-Demand e utilização](assets/aws/virginia-norte/on-demand-ec2.png)
- [EBS gp3 com 50 GB e total](assets/aws/virginia-norte/ebs-gp3-50gb.png)

### Vídeo demonstrativo

[Vídeo da Entrega 2 — Cloud Computing com AWS](https://youtu.be/UKYKhwVzVz4)
