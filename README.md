# Atribuição de Receita & Métricas de Marketing

Relatório desenvolvido em **Power BI** para a análise de marketing e a **atribuição de receita**
de uma rede varejista. O painel correlaciona o investimento realizado em campanhas com o retorno
em faturamento, permitindo medir a eficiência de cada canal de atração e orientar a alocação de
verba com base em resultado, não em intuição.

---

## Visão Geral

A solução conecta os dados de investimento em campanhas, os custos de mídia e as vendas associadas
em um modelo único, entregando uma leitura clara de ROI, custo de aquisição e conversão por canal.
Responde à pergunta central de qualquer investimento em marketing: onde cada real aplicado está,
de fato, virando receita?

> **Nota de confidencialidade:** todos os dados exibidos no arquivo `.pbix` são fictícios e
> anonimizados, criados exclusivamente para demonstração de portfólio.

---

## Contexto de Negócio

Verba de marketing é finita e cada canal compete por ela. Sem atribuição, o investimento se
distribui por hábito ou por percepção, e canais que não se pagam continuam consumindo orçamento
enquanto os que convertem ficam subfinanciados. A ausência de uma visão consolidada de ROI e CAC
torna impossível defender ou realocar a verba com objetividade.

Este painel resolve isso ligando investimento a faturamento gerado, canal a canal, e traduzindo o
esforço de marketing em indicadores financeiros comparáveis.

## O Problema que Resolve

- **Falta de atribuição** clara entre investimento em campanha e receita gerada.
- **Verba mal alocada** por ausência de comparação objetiva entre canais.
- **ROI e CAC desconhecidos**, dificultando a defesa do orçamento de marketing.
- **Conversão não acompanhada** ao longo do funil de atração.

## Público e Decisões Apoiadas

- **Marketing:** identifica os canais mais eficientes e realoca verba para o que converte.
- **Diretoria / Financeiro:** avalia o retorno do investimento em marketing com dado.
- **Comercial:** entende a origem da receita e o custo de aquisição por cliente.

## Impacto e Valor Gerado

Mostrou onde o investimento de marketing de fato vira receita (ROI e CAC por canal), permitindo
cortar o canal que não se paga e realocar verba para o que converte — aumentando a eficiência do
orçamento sem necessariamente aumentar o gasto.

---

## Arquitetura de Dados e Abordagem Técnica

### Fontes de dados
- **Investimentos / custos de mídia** por campanha e canal.
- **Vendas** associadas às campanhas (receita atribuída).
- Cadastro de **campanhas e canais**.

### Transformação (Power Query / M)
Ingestão e tratamento dos dados de campanhas, custos e vendas; padronização de canais; associação
entre investimento e receita; e cálculo das bases de conversão. A limpeza é centralizada no Power
Query para garantir consistência entre as fontes.

### Modelagem dimensional (Star Schema)
- **Fato Investimentos** — custo por campanha / canal / período.
- **Fato Vendas** — receita atribuída por campanha.
- **Dimensão Campanha / Canal** — atributos de mídia e origem.
- **Dimensão Calendário** — base das análises temporais.

### Principais medidas (DAX) — lógica implementada

```DAX
Investimento Total = SUM( FatoInvestimentos[Custo] )
Receita Gerada     = SUM( FatoVendas[Receita] )
ROI                = DIVIDE( [Receita Gerada] - [Investimento Total], [Investimento Total] )
CAC                = DIVIDE( [Investimento Total], [Novos Clientes] )
Taxa de Conversao  = DIVIDE( [Vendas], [Leads] )
```

> As fórmulas descrevem a lógica de cálculo do relatório e servem como referência de leitura do modelo.

---

## Indicadores e Análises (KPIs)

- **Retorno sobre Investimento (ROI):** rentabilidade financeira de cada real investido em marketing.
- **Receita Gerada por Canal:** distribuição do faturamento por canal de aquisição.
- **Taxa de Conversão:** percentual de leads / oportunidades convertidos em vendas.
- **Custo por Aquisição (CAC):** eficiência de investimento por novo cliente conquistado.

## Estrutura de Páginas do Relatório

1. **Visão Geral de Marketing** — ROI global, investimento e receita atribuída.
2. **Desempenho por Canal** — comparativo de eficiência entre canais de atração.
3. **Funil e Conversão** — leads, conversão e custo por aquisição.

## Como Visualizar

O relatório é apresentado pelas imagens da seção **Prints** abaixo, que reproduzem as páginas
principais do painel. O arquivo-fonte (`.pbix`) não é versionado neste repositório por conter o
modelo de dados; pode ser disponibilizado sob solicitação para avaliação técnica.

## Estrutura de Arquivos

```text
README.md    -> Documentacao do projeto (contexto de negocio + arquitetura tecnica)
docs/        -> Prints das paginas do relatorio
.gitignore   -> Exclui binarios (.pbix) e planilhas de trabalho do versionamento
```

## Prints

As imagens abaixo apresentam as páginas principais do relatório — a imagem é o que comunica o
projeto de forma imediata. Os prints serão adicionados na pasta `docs/`.

<!-- Descomente ao adicionar a imagem:
![Visao geral de marketing e receita](docs/print-1.png)
-->

## Autor

Vitor Santos — Análise de Dados e Inteligência Comercial (Varejo).
