# Boca Goalkeeper Score

Projeto de análise de dados voltado para avaliar possíveis goleiros para o Boca Juniors utilizando métricas de desempenho da temporada 2026 na Argentina e no Brasil.

## Resumo

Este projeto parte de uma pergunta concreta:

> Existe na Argentina ou no Brasil um goleiro claramente superior a Leandro Brey com base nos dados disponíveis?

A intenção não é construir uma recomendação definitiva de scouting, mas desenvolver uma primeira ferramenta analítica, simples e interpretável, para comparar perfis de goleiros e identificar candidatos que mereçam uma análise mais profunda.

## Pergunta analítica

**Existe uma opção externa que, segundo métricas selecionadas, se destaque claramente acima de Leandro Brey?**

## Fonte dos dados

A análise utiliza dados de goleiros exportados do FBref para a temporada 2026.

Arquivos esperados:

```text
argentina_keepers_2026.csv
argentina_keepers_advanced_2026.csv
brazil_keepers_2026.csv
brazil_keepers_advanced_2026.csv
```

São utilizadas tabelas padrão e avançadas de goleiros da Argentina e do Brasil.

## Metodologia

O notebook segue estas etapas:

1. Carregamento dos arquivos CSV exportados do FBref.
2. Limpeza e normalização das tabelas.
3. União dos dados padrão e avançados.
4. Aplicação de filtros de candidatos.
5. Construção de um score composto.
6. Ranking dos goleiros.
7. Visualização dos resultados.

## Filtros aplicados

| Filtro | Critério | Objetivo |
|---|---:|---|
| Idade | ≤ 34 | Excluir goleiros em fase final de carreira |
| Minutos jogados | ≥ 300 | Evitar amostras muito pequenas |

Esses filtros buscam manter a análise focada em perfis minimamente representativos e potencialmente realistas.

## Boca GK Score v1

O projeto constrói um índice próprio chamado **Boca GK Score v1**.

As variáveis são escaladas entre 0 e 1 com MinMaxScaler antes da aplicação dos pesos.

| Métrica | Peso | Direção | Justificativa |
|---|---:|---|---|
| Percentual de defesas | 45% | Maior é melhor | Principal indicador de shot-stopping |
| Gols sofridos a cada 90 minutos | 20% | Menor é melhor | Penaliza goleiros que sofrem gols com maior frequência |
| Percentual de jogos sem sofrer gols | 15% | Maior é melhor | Valoriza resultados defensivos |
| Minutos jogados | 10% | Maior é melhor | Valoriza continuidade e confiança da comissão técnica |
| Defesas a cada 90 minutos | 5% | Maior é melhor | Captura volume de intervenção |
| Perfil de idade | 5% | Pico entre 24 e 31 | Premia levemente idades consideradas ideais para a posição |

O score é deliberadamente simples e interpretável. Ele foi pensado como uma primeira versão que pode ser melhorada com mais contexto tático, informações contratuais, ajuste por liga e validação qualitativa.

## Outputs

O notebook gera:

- Um ranking de candidatos.
- Uma tabela final comparativa.
- Um mapa de perfis segundo percentual de defesas e gols sofridos a cada 90 minutos.
- Um gráfico de top 10 segundo o Boca GK Score v1.

## Ferramentas utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook

## Reprodutibilidade

Para reproduzir a análise:

1. Baixar os arquivos CSV correspondentes do FBref.
2. Colocá-los no caminho esperado pelo notebook ou carregá-los no Google Colab.
3. Abrir o notebook:

```text
notebooks/01_boca_goalkeeper_score.ipynb
```

4. Executar todas as células.

## Disponibilidade dos dados

Os arquivos originais não são necessariamente incluídos neste repositório, pois podem estar sujeitos a restrições de redistribuição da fonte.

Para reproduzir a análise, recomenda-se baixar os dados originais do FBref e salvá-los com os nomes esperados.

## Limitações

Este projeto deve ser interpretado como um exercício exploratório de análise de dados, não como um relatório completo de scouting.

Principais limitações:

- O score depende das métricas disponíveis.
- Não há ajuste completo pelo contexto da equipe.
- Não há ajuste pelo nível relativo da liga.
- O papel tático do goleiro não é modelado diretamente.
- Contrato, salário e valor de mercado não são incluídos.
- Scouting qualitativo não é incorporado.
- Métricas avançadas de shot-stopping podem ser melhor integradas em versões futuras.

## Próximos passos

Possíveis melhorias:

- Incorporar PSxG+/- e outras métricas avançadas ao score.
- Ajustar o desempenho por contexto de equipe e liga.
- Adicionar idade, contrato e valor de mercado.
- Incluir mais ligas.
- Construir perfis por percentis.
- Comparar candidatos com perfis históricos de goleiros do Boca.
- Somar notas qualitativas de scouting.
- Automatizar a exportação de tabelas e gráficos.

## Disclaimer

Este projeto é um exercício analítico independente e não está afiliado ao Boca Juniors, ao FBref ou a qualquer organização esportiva.

A análise tem fins educativos, de portfólio e de análise esportiva.
