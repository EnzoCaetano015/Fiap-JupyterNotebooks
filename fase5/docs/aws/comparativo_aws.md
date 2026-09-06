# Comparativo de custos AWS — São Paulo x Virgínia do Norte

Consulta realizada em **6 de setembro de 2026** na [AWS Pricing Calculator](https://calculator.aws/). Os valores são estimativas mensais em dólares americanos (USD), não incluem impostos e podem variar conforme alterações de preço ou uso real.

## Configuração comparada

O mesmo perfil técnico foi aplicado nas duas regiões:

- Amazon EC2 `t3.micro` de geração atual;
- Linux, locação compartilhada e uma instância;
- 2 vCPUs, 1 GiB de memória e desempenho de rede de até 5 Gigabits;
- cobrança **On-Demand**, com 100% de utilização (730 horas por mês);
- um volume Amazon EBS SSD de uso geral `gp3` com 50 GB;
- sem armazenamento de snapshots, monitoramento detalhado, transferência de dados ou custos adicionais.

## Comparativo mensal

| Região | Código | EC2 On-Demand | EBS gp3 (50 GB) | Total mensal |
|---|---|---:|---:|---:|
| América do Sul (São Paulo) | `sa-east-1` | US$ 12,264 | US$ 7,60 | **US$ 19,86** |
| Leste dos EUA (N. da Virgínia) | `us-east-1` | US$ 7,592 | US$ 4,00 | **US$ 11,59** |

Os totais exibidos pela calculadora são arredondados para duas casas decimais. Com base nesses totais, São Paulo custa **US$ 8,27 a mais por mês**, diferença de **71,35%** em relação à opção mais barata. Portanto, para este perfil e sem considerar requisitos de latência, residência de dados ou transferência, **Virgínia do Norte é a região de menor custo**.

## Memória de cálculo

- São Paulo — EC2: `1 × US$ 0,0168/h × 730 h = US$ 12,264/mês`.
- São Paulo — EBS: `50 GB × US$ 0,152/GB-mês = US$ 7,60/mês`.
- Virgínia do Norte — EC2: `1 × US$ 0,0104/h × 730 h = US$ 7,592/mês`.
- Virgínia do Norte — EBS: `50 GB × US$ 0,08/GB-mês = US$ 4,00/mês`.
- Diferença absoluta pelos totais apresentados: `US$ 19,86 − US$ 11,59 = US$ 8,27/mês`.
- Diferença percentual sobre Virgínia do Norte: `(US$ 8,27 ÷ US$ 11,59) × 100 = 71,35%`.

## Evidências

### São Paulo (`sa-east-1`)

- [Região, locação e sistema operacional](../../assets/aws/sao-paulo/configuracao-regiao-linux.png)
- [Preço EC2 On-Demand e utilização](../../assets/aws/sao-paulo/on-demand-ec2.png)
- [Configuração do EBS gp3 com 50 GB](../../assets/aws/sao-paulo/ebs-gp3-50gb.png)
- [Cálculo do EBS e total mensal](../../assets/aws/sao-paulo/calculo-ebs-total.png)

### Virgínia do Norte (`us-east-1`)

- [Região, locação e sistema operacional](../../assets/aws/virginia-norte/configuracao-regiao-linux.png)
- [Preço EC2 On-Demand e utilização](../../assets/aws/virginia-norte/on-demand-ec2.png)
- [Configuração e cálculo do EBS gp3 com 50 GB](../../assets/aws/virginia-norte/ebs-gp3-50gb.png)

## Observações

A escolha final não deve considerar apenas preço. Latência para usuários no Brasil, exigências de conformidade e residência de dados, disponibilidade regional e custos de transferência podem justificar São Paulo mesmo com custo mensal superior. Este comparativo isola somente os componentes definidos para a tarefa e não demonstra o custo total de uma arquitetura de produção.
