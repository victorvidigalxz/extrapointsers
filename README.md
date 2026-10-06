# Clustering de consumidores de energia (K-Means) — Python e Orange

Atividade da disciplina de Computer Science (1CC). Base simulada com 60 consumidores e três atributos: consumo mensal (kWh), demanda máxima (kW) e percentual do consumo entre 22h e 6h.


| Integrante |
|---|
| Victor Vidigal RM 571318 |
| Gabriel Savoy RM 568991 |

## Conteúdo

| Arquivo | Descrição |
| --- | --- |
| `1CC_SERS_Clustering_Energia_Python_Orange_RESOLVIDO.ipynb` | Notebook com o exercício 2 implementado, resultados visíveis e respostas (seções 2.7 e 3.4) |
| `consumidores_energia_proposto.csv` | CSV de entrada (sem clusters) |
| `consumidores_energia_orange_clusters.csv` | Base com `Cluster` (C1–C4) e `Silhouette` no formato de saída do widget k-Means do Orange |
| `orange/fluxo_clusterizacao_energia.ows` | Fluxo do Orange: File → Select Columns → k-Means → Data Table / Scatter Plot ×2 / Box Plot / Save Data |
| `orange_silhouette_por_k.csv` | Silhouette Score por k (Orange) |
| `imagens/` | Elbow, Silhouette, dispersões e box plots (Python e Orange) |

## Escolha de k: 4

- **Elbow:** queda da inércia de 52,03 (k = 2→3) e 12,78 (k = 3→4), mas só 2,89 (k = 4→5). O cotovelo está em k = 4.
- **Silhouette Score (Python e Orange):** k = 2: 0,526 · k = 3: 0,648 · **k = 4: 0,667** · k = 5: 0,586 · k = 6: 0,594 / 0,583 · k = 7: 0,533 / 0,524 · k = 8: 0,531 / 0,534. O melhor valor é o de k = 4.
- **Interpretação:** com k = 3, os perfis de consumo baixo e intermediário diurno se misturam; k = 4 os separa em quatro grupos de 15 consumidores, cada um com leitura clara.

## Perfis (médias nas unidades originais)

| Perfil | Consumo | Demanda | % noturno |
| --- | --- | --- | --- |
| Baixo consumo, uso diurno | ≈ 224,9 kWh | ≈ 3,1 kW | ≈ 18,8% |
| Consumo intermediário, uso diurno | ≈ 473,4 kWh | ≈ 6,2 kW | ≈ 21,5% |
| Consumo intermediário, uso noturno | ≈ 482,3 kWh | ≈ 6,4 kW | ≈ 72,1% |
| Alto consumo e alta demanda | ≈ 918,2 kWh | ≈ 12,2 kW | ≈ 46,5% |

Os dois perfis intermediários só se distinguem pelo percentual noturno. Sem esse atributo, eles viram um único grupo.

## Ações sugeridas (hipóteses a validar)

1. **Intermediário noturno:** levantar as cargas que operam entre 22h e 6h e avaliar tarifa diferenciada por horário.
2. **Alto consumo e alta demanda:** acompanhar a demanda máxima, orientar o escalonamento de partida de equipamentos e revisar a demanda contratada.

Os grupos descrevem similaridade nesta base simulada; não comprovam eficiência, desperdício ou tipo de estabelecimento.

## Nota sobre o Orange

O `.ows` foi gerado com a estrutura padrão do Orange (k-Means com Normalize columns, k-Means++, 10 re-runs, k fixo em 4). O CSV com clusters, os valores de Silhouette e as imagens do Orange foram produzidos reproduzindo o widget k-Means via biblioteca Orange 3.40 (mesmo pré-processamento e parâmetros), e não por capturas de tela da interface. Ao abrir o `.ows`, selecione `consumidores_energia_proposto.csv` no widget File e configure Select Columns (três atributos em Features, `consumidor` em Meta).
