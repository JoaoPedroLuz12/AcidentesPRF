# Gravidade de acidentes em rodovias federais (PRF)

Previsão da gravidade de acidentes em rodovias federais com dados abertos da PRF (2021–2025), com auditoria de vazamento de dados e análise de viés regional. Projeto final da disciplina de Inteligência Artificial da UFPI.

**Autor:** João Pedro Pereira da Luz · **Professor:** Dr. Pedro Almir Martins de Oliveira

## Pergunta de pesquisa

Quanto da gravidade de um acidente em rodovia federal é previsível apenas pelo contexto (onde, quando e em que condições ele ocorre), e quanto do desempenho obtido nessa base depende de informações que só existem depois do acidente?

Um acidente é considerado **grave** quando tem pelo menos um morto ou um ferido grave (28,3% dos casos).

## Abrir e executar

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/JoaoPedroLuz12/AcidentesPRF/blob/main/notebook/acidentes_prf_gravidade.ipynb)

No Colab, use **Ambiente de execução → Executar tudo**. O notebook baixa os dados direto da página da PRF e não depende de nenhum arquivo local. A execução completa leva de 10 a 15 minutos no Colab gratuito, quase todo esse tempo no treino dos modelos.

## Conteúdo

| Caminho | O que é |
|---|---|
| `notebook/acidentes_prf_gravidade.ipynb` | Código e relatório técnico: dados, análise exploratória, modelos, avaliação, robustez, análise de erros e conclusões |
| `artigo/artigo.tex` e `artigo/refs.bib` | Resumo expandido em inglês, no formato de artigos da SBC |
| `artigo/figuras/` | Figuras do artigo, geradas pelo próprio notebook |
| `artigo/artigo.pdf` | Artigo final, compilado no Overleaf com o modelo oficial da SBC |

## Dados

Polícia Rodoviária Federal, [Dados Abertos da PRF](https://www.gov.br/prf/pt-br/acesso-a-informacao/dados-abertos/dados-abertos-da-prf), seção "Acidentes", arquivos agrupados por ocorrência de 2021 a 2025: 342.670 acidentes.

## Método

- **Divisão por ano:** treino em 2021–2023, validação em 2024 (escolha de hiperparâmetros e do limiar) e teste em 2025, usado uma única vez.
- **Três conjuntos de atributos:** (A) só contexto, que existe antes do acidente; (B) contexto mais a dinâmica do acidente; (C) com colunas de desfecho, ou seja, vazamento.
- **Modelos:** regressão logística e Random Forest, comparados com referências triviais. Métrica principal: PR-AUC.

## Principais resultados (teste, 2025)

| Atributos | PR-AUC da Random Forest |
|---|---|
| Sem modelo | 0,283 |
| A — Contexto | 0,395 |
| B — Contexto + dinâmica | 0,528 |
| C — Com vazamento | 0,965 (regressão logística: 0,994) |

- O contexto sozinho prevê pouco.
- Resultados muito altos nessa base podem vir de vazamento.
- Com um único limiar, o modelo de contexto marca como graves 99,0% dos acidentes do Piauí e 54,4% dos do Sudeste.

## Uso de modelos de linguagem

O projeto foi desenvolvido com o auxílio do assistente Claude (Anthropic). A declaração completa está no notebook (Seção 13) e no artigo (seção *Use of Large Language Models*).
