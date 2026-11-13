# RESUMO NLP V2: plano de reestruturação para 60 slides

Versão enxuta da `Apresentacao NLP V2`, que **não foi alterada**. A V2 compila em
**73 páginas**; esta versão compila em **58 páginas** (limite: 60), contando título,
sumário, referências, "Chegamos ao Fim" e os 2 slides de backup.

Premissas: público de pós-graduação em Engenharia Elétrica (COPPE/UFRJ, CPE727), que já
conhece softmax, gradiente e RNN/CNN. Não foi informado o tempo de aula; 58 páginas
cabem em ~1h só se os slides de código e o backup forem ditos rápido (ver §3).

## 1. Diagnóstico de redundância e ritmo

| Seção (V2) | Págs. | Diagnóstico |
|---|---|---|
| Referências | 5 | **Maior desperdício.** 18 entradas (`\nocite{*}`) em `\footnotesize`. Em `\tiny` cabem em 2 páginas, sem perder nenhuma referência. |
| 01 Motivação / word2vec / Skip-gram / CBOW | 16 | Mais longa. One-hot e "por que é má escolha" são o mesmo argumento; "Janela de contexto" e "diferenças Skip-gram × CBOW" mostram os mesmos pares duas vezes; SGD e gradiente são dois slides para uma só ideia ("observado menos esperado"); o gradiente do CBOW repete o do skip-gram. |
| 02 Treinamento aproximado | 8 | O slide "só positivos não basta" é a continuação direta do slide da sigmoide; "probabilidade é o caminho" e "vantagens" são a mesma conta vista duas vezes. |
| 04 GloVe | 9 | "Evolução" e "matriz de coocorrência" contam a mesma ideia (contar uma vez); "vieses" e "função de peso" são duas mudanças curtas; "simétrico" é um detalhe de uma linha de conteúdo. |
| 05 Subword | 6 | fastText gasta 2 slides (n-gramas, soma) para uma ideia só. |
| 07 BERT | 10 | MLM e a estratégia 80/10/10 são um mesmo raciocínio; "De onde vêm os dados" repete que MLM e NSP geram rótulos do texto. |
| 06 Similaridade, 08 RNN, 09 CNN | 2 / 7 / 5 | Ritmo bom. 08 e 09 têm candidatos a fusão futura (ver §3), mas não foram mexidos. |

## 2. Mapa de fusão (aplicado)

Os números são as páginas da V2.

| # | Slides da V2 | Viram | Como organizei sem poluir |
|---|---|---|---|
| 1 | 6 + 7 (one-hot, "má escolha") | **One-hot: simples, mas toda palavra é ortogonal** | Texto à esquerda (definição, cosseno, ortogonalidade), matriz à direita; "Problemas" e "O que queremos" viram duas caixas de uma linha cada. |
| 2 | 10 + 11 (janela, Skip-gram × CBOW) | **Janela de contexto: de onde vêm os dados** | Uma figura da janela; embaixo, duas colunas (Skip-gram / CBOW) e uma caixa de intuição. O diagrama de "?" foi cortado, porque a figura da janela já mostra o mesmo. |
| 3 | 15 + 16 (SGD, gradiente) | **SGD e gradiente: observado menos esperado** | Duas equações empilhadas (log P e o gradiente), com a figura à direita; as duas regras de derivada viram um item. Os 3 *cards* de SGD viram uma frase. |
| 4 | 17 + 18 (CBOW fórmula, gradiente) | **CBOW: a fórmula e o gradiente** | Fórmula, uma linha de leitura, o gradiente com $1/2m$ e a caixa "o que isso muda". |
| 5 | 20 + 21 (evento positivo, só positivos) | **O evento positivo e por que precisamos de negativos** | Sigmoide e gráfico em cima; a caixa vermelha "perda zero, utilidade zero" embaixo. A tabela virou uma frase. |
| 6 | 25 + 26 (caminho, vantagens) | **Softmax hierárquica: a probabilidade é o caminho, e o custo** | O exemplo numérico e a fórmula geral em cima; os 3 *cards* de custo (1.000.000 / 6 / ≈20) numa linha embaixo. |
| 7 | 27 + 28 (evolução, matriz) | **Evolução para o GloVe: contar uma vez, treinar na matriz** | A matriz já trazia as caixas word2vec × GloVe; a analogia do "resumo" e a citação entraram nelas. |
| 8 | 31 + 32 (vieses, peso) | **Mudanças 2 e 3: os vieses e a função de peso** | Duas colunas, uma mudança por coluna, cada uma com sua equação. |
| 9 | 33 + 35 (equação final, simetria) | **A equação final** (com caixa "O GloVe é simétrico") | A simetria virou uma caixa ao lado de "Objetivo". |
| 10 | 37 + 38 (fastText n-gramas, soma) | **fastText: a palavra como a soma dos seus n-gramas** | Figura dos n-gramas menor, fórmula da soma, e Ganho/Custo lado a lado. |
| 11 | 49 + 50 (MLM, 80/10/10) | **Pré-treino 1: MLM** | Figura GPT × BERT; o 80/10/10 virou três caixinhas numa linha, com o "por que não sempre `<mask>`" em uma frase. |
| 12 | 51 + 52 (NSP, dados) | **Pré-treino 2: NSP e rótulos de graça** | Texto e figura do NSP; a caixa verde final resume de onde vêm os rótulos e os corpora. |

As **notas do apresentador** de cada slide fundido foram reescritas para cobrir os
dois slides originais. Ganho: 12 slides, mais 3 páginas de referências = 15 a menos
(73 → 58).

## 3. Cortes e apêndice

Nada foi cortado de fato; o que perdeu espaço foi condensado. Itens que **saíram do
slide** (e por que não prejudica):

- Diagrama de "?" do slide Skip-gram × CBOW (pág. 11): a figura da janela e os pares já dizem o mesmo.
- Os 3 *cards* do SGD (pág. 15): a ideia ficou numa frase; o que importa é o gradiente.
- A tabela "gato/miou × gato/cloreto" (pág. 21): virou uma frase na caixa vermelha.
- O slide "Evolução para o GloVe" (pág. 27) como slide separado: o conteúdo está na matriz.

**Candidatos a apêndice ou fusão futura** (não aplicados; há folga de 2 páginas):

- 08 RNN: "Embeddings pré-treinados: o GloVe de 100 dimensões" (pág. 59) é rápido e poderia ir para o backup, e "arquitetura BiRNN" + "Por que LSTM?" (págs. 55–56) poderiam virar um.
- 09 CNN: "A arquitetura completa do textCNN" e "O fluxo de dados" (págs. 64–65) se sobrepõem; podem virar um.
- 07: "Juntando tudo: o `BERTModel`" (código) pode ir para o backup se o tempo apertar.

## 4. Slides intocáveis (espinha dorsal)

- **Resumo: do word2vec ao BERT** (4): o roteiro da aula.
- **Embedding: um dicionário de números** (8): a definição central.
- **A fórmula do skip-gram** e **Função de Perda** (13, 14): a softmax e a máxima verossimilhança.
- **SGD e gradiente** (fundido): "observado menos esperado" é a virada de raciocínio que justifica o treino aproximado.
- **Amostragem negativa**: "A aproximação" e "Função de Perda" (22, 23), e a **softmax hierárquica** (árvore, 24).
- **GloVe**: "Por que não continuar com o word2vec?" (29), "Mudança 1" (30) e "A equação final".
- **BPE** (39–41) e **fastText** (fundido): subpalavras e palavras fora do vocabulário.
- **Do vetor fixo ao vetor com contexto** (44), **ELMo e GPT** (45) e **BERT: o melhor dos dois mundos** (46): a virada estático → contextual.
- **Representação de entrada**, **MLM** e **NSP** (48, 49–52).

## 5. Novo roteiro: 58 slides

"Origem" = página na `Apresentacao NLP V2`. `+` marca fusão.

| # | Título | Origem |
|---|---|---|
| 1 | Título | 1 |
| 2 | Conteúdo da apresentação | 2 |
| 3 | Por que estudar Processamento de Linguagem Natural? | 3 |
| 4 | Resumo: do word2vec ao BERT | 4 |
| 5 | Introdução: representação de palavras por vetores | 5 |
| 6 | One-hot: simples, mas toda palavra é ortogonal | 6 + 7 |
| 7 | Embedding: um dicionário de números | 8 |
| 8 | word2vec | 9 |
| 9 | Janela de contexto: de onde vêm os dados de treino | 10 + 11 |
| 10 | Treino do Skip-gram e CBOW | 12 |
| 11 | A fórmula do skip-gram | 13 |
| 12 | Função de Perda | 14 |
| 13 | SGD e gradiente: observado menos esperado | 15 + 16 |
| 14 | CBOW: a fórmula e o gradiente | 17 + 18 |
| 15 | Negative Sampling e Hierarchical Softmax | 19 |
| 16 | O evento positivo e por que precisamos de negativos | 20 + 21 |
| 17 | A aproximação com amostragem negativa | 22 |
| 18 | Negative Sampling e a Função de Perda | 23 |
| 19 | Softmax hierárquica | 24 |
| 20 | Softmax hierárquica: a probabilidade é o caminho, e o custo | 25 + 26 |
| 21 | Evolução para o GloVe: contar uma vez, treinar na matriz | 27 + 28 |
| 22 | Por que não continuar com o word2vec? | 29 |
| 23 | Mudança 1: logaritmo e erro quadrático | 30 |
| 24 | Mudanças 2 e 3: os vieses e a função de peso | 31 + 32 |
| 25 | A equação final (e a simetria do GloVe) | 33 + 35 |
| 26 | Treino do GloVe: o algoritmo | 34 |
| 27 | Subword Embedding: olhando para dentro das palavras | 36 |
| 28 | fastText: a palavra como a soma dos seus n-gramas | 37 + 38 |
| 29 | Byte Pair Encoding (BPE) | 39 |
| 30 | BPE com números: as primeiras junções | 40 |
| 31 | BPE: segmentando palavras que nunca vimos | 41 |
| 32 | Usando vetores pré-treinados: similaridade | 42 |
| 33 | Analogias: aritmética de vetores | 43 |
| 34 | Do vetor fixo ao vetor com contexto | 44 |
| 35 | Os antecessores do BERT: ELMo e GPT | 45 |
| 36 | BERT: combinando o melhor dos dois mundos | 46 |
| 37 | Como o BERT é usado: pré-treino e ajuste fino | 47 |
| 38 | Representação de entrada | 48 |
| 39 | Pré-treino 1: Masked Language Modeling (MLM) | 49 + 50 |
| 40 | Pré-treino 2: NSP e rótulos de graça | 51 + 52 |
| 41 | Juntando tudo: o BERTModel | 53 |
| 42 | Aplicação: análise de sentimento com RNN | 54 |
| 43 | A arquitetura BiRNN: três camadas | 55 |
| 44 | Por que LSTM? Por que bidirecional? | 56 |
| 45 | O pulo do gato: concatenar o primeiro e o último passo | 57 |
| 46 | O código da BiRNN | 58 |
| 47 | Embeddings pré-treinados: o GloVe de 100 dimensões | 59 |
| 48 | Treino e resultados | 60 |
| 49 | A matemática da convolução 1D | 61 |
| 50 | A arquitetura textCNN na prática | 62 |
| 51 | Max-over-time: muitos números, um resumo | 63 |
| 52 | A arquitetura completa do textCNN | 64 |
| 53 | O fluxo de dados: de $T$ palavras a 2 números | 65 |
| 54–55 | Referências (2 páginas, `\tiny`) | 66–70 |
| 56 | Chegamos ao Fim | 71 |
| 57 | Backup: o minibatch, quatro tensores | 72 |
| 58 | Backup: o laço de treino | 73 |

## Como compilar

`pdflatex main.tex`, `bibtex main`, `pdflatex main.tex` (duas vezes), como na V2. A
imagem `img/StockSnap_REB7CJXE8C.jpg` precisa estar no projeto (também falta na V2).
