# Pipeline de Engenharia de Dados – Câmara dos Deputados

> Análise integrada com governança, visualização, storytelling e dados reais do legislativo brasileiro.

## Objetivo
Construir um pipeline de ponta a ponta (Bronze–Silver–Gold) para ingestão, tratamento, modelagem, análises e visualização de dados da Câmara dos Deputados, demonstrando domínio de engenharia de dados, boas práticas e ciência de dados aplicada.

## Fontes de Dados
- **Discursos Parlamentares**: Dados extraídos do endpoint de discursos do portal Dados Abertos da Câmara dos Deputados (não estruturado).
- **Proposições Legislativas**: Dados tabulares de documentos legislativos (estruturado).
- Extração via API REST pública: https://dadosabertos.camara.leg.br/swagger/api.html

## Pipeline Implementado
### Bronze
- Ingestão robusta e paginada das APIs, controlando limites de requisição e salvando arquivos brutos.
- Armazenamento local em formato .json, simulação de bronze “data lake”.

### Silver
- Seleção, limpeza e validação de campos relevantes em ambos os conjuntos.
- Filtragem textual (transcrições válidas ≥ 100 caracteres).
- Adição de metadados de processamento (timestamp).
- Organização em DataFrames prontos para análise.

### Gold
- Modelo analítico e agregações para suporte ao BI.
- Tabelas de apoio com totalizadores, ranking, keywords e tipos de proposições.
- Opção de exportação em .csv para integração com ferramentas externas (Power BI, Databricks).

## Visualizações & Insights
- **Top 5 Tipos de Discurso:** Identifica as falas mais realizadas na casa legislativa.
- **Top 10 Palavras-chave de Discursos:** Principais temas trazendo à tona debate público e agendas do Plenário.
- **Distribuição de Discursos por Mês:** Tendências de engajamento político ao longo do tempo (sazonalidade, picos, recessos).
- **Proposições por Tipo:** Quais formatos de proposição mais movimentam o processo legislativo.
*Todos os gráficos e outputs são salvos na pasta `/data` e podem ser facilmente incorporados ao README ou relatórios.*

## Como Executar
1. Abra o notebook `.ipynb` no Databricks Community, JupyterLab ou VSCode com Spark.
2. Crie a pasta `data` local (se não existir).
3. Execute as células sequencialmente. O pipeline faz toda a coleta/persistência por você.
4. Use os CSVs e imagens geradas tanto para análise visual quanto para reporting externo.

## Perguntas de Negócio & Storytelling
- Quais são os tipos de discurso mais utilizados na Câmara e por quê?
- Que temas e palavras-chave aparecem com mais frequência nos debates?
- Como a produção legislativa está distribuída entre proposições do tipo requerimento, projeto de lei, etc.?
- Há sazonalidade ou variação mensal relevante na atividade do plenário?

O pipeline permite explorar instantaneamente essas perguntas com gráficos de fácil interpretação, além de exportações personalizáveis.

## Governança & Boas Práticas
- Controle de qualidade textual (transcrição mínima para validade).
- Timestamp e metadados de processamento em todas as etapas.
- Comentários em código, separação clara entre Bronze, Silver, Gold.
- Permite extensão fácil para modelos de dados, análise temática, sentiment analysis ou dashboards BI.

## Estrutura de Diretórios
```shell
├── data/
│   ├── discursos_*.json
│   ├── proposicoes_*.json
│   ├── discursos_gold.csv
│   ├── proposicoes_gold.csv
│   ├── grafico_top_5_tipos.png
│   ├── grafico_top_keywords.png
│   ├── grafico_discursos_mes.png
│   ├── grafico_proposicoes_tipo.png
├── Notebook-Projeto-Engenharia-de-Dados-Camara-dos-Deputados.ipynb
└── README.md
```

## Possíveis Extensões
- Análise de sentimento dos discursos.
- Dashboards dinâmicos com Power BI/Tableau.
- Agendamento de execução automática para pipelines semanais/mensais.
- Enriquecimento cruzando com votações ou presença.

Projeto desenvolvido como desafio final do programa Upskill Tiller – Engenharia de Dados.
