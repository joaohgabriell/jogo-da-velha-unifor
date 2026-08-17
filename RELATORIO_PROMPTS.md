# Relatório de Prompting e Auditoria de IA

## 1. Ferramenta de IA Utilizada
- **IA:** Gemini
- **Data da Interação:** Agosto de 2026

## 2. Processo de Prompting

O processo de construção seguiu as diretrizes de Spec-Driven Development, fornecendo a Especificação de Requisitos Funcionais completa como contexto (System Prompt / Contexto Primário).

**Prompt Principal Enviado:**
> Forneci a Especificação de Requisitos Funcionais (CDU do Jogo da Velha Web - UNIFOR), além das regras de estrutura do repositório e os critérios de aceitação. Solicitei a geração completa do código em um único arquivo HTML contendo CSS e JS, e as estruturas documentais.

**Instruções de Correção/Direcionamento:**
- Foi explicitamente exigido que o CSS obedecesse à paleta de cores UNIFOR descrita no Requisito Não Funcional (Azul #003366, Azul Destaque #0056b3, Laranja #d97706 e Fundo #f4f6f9).
- Foi instruído que o áudio não poderia usar dependências locais (mp3) para cumprir o RNF de "Zero Dependência", ordenando o uso exclusivo da **Web Audio API**.
- A IA foi instruída a embutir uma lógica de confetes via Canvas dentro do próprio script do `index.html` para não necessitar de bibliotecas de terceiros (como canvas-confetti via CDN ou arquivo local).
- Como Auditor de Qualidade, solicitei a implementação de uma IA de nível médio para o modo "Contra o Computador", com heurística de ataque/defesa, mantendo o estrito cumprimento da regra de executar a jogada na vez do 'O'. O pedido de colocar uma imagem de fundo foi barrado para não violar o Requisito de Identidade Visual.

## 3. Checklist de Autoavaliação (Critérios de Aceite)

Auditoria realizada no código fornecido pela IA:

| ID | Descrição do Critério de Aceite | Status | Observações |
|----|--------------------------------|--------|-------------|
| **CA-01** | Fidelidade Visual: A aplicação utiliza a paleta de cores institucional da UNIFOR e possui o subtítulo. | ✅ Atendido | Identidade visual mapeada e aplicada nas variáveis CSS (`:root`). Cabeçalho reflete os elementos estruturados no protótipo. |
| **CA-02** | Regra de Ocupação: Não é possível sobrescrever uma célula que já possui o símbolo 'X' ou 'O'. | ✅ Atendido | Lógica bloqueada no passo inicial de `cellClicked` validando o array de estado. |
| **CA-03** | Bloqueio pós-Fim de Jogo: O tabuleiro bloqueia cliques em células vazias até que a próxima rodada/reinício aconteça. | ✅ Atendido | Uso da variável de controle booleana `running` ou `isGameOver` sendo setada para `false` no handle de empate ou vitória. |
| **CA-04** | Comportamento do Modo CPU: Sistema executa automaticamente a jogada do robô na vez do 'O' após uma breve pausa. | ✅ Atendido | Implementado via função `setTimeout(cpuPlay, 400)` após bloqueio de cliques do jogador. Inteligência heurística adicionada. |
| **CA-05** | Regra do Melhor de 3: MD3 zera o tabuleiro entre rodadas e só encerra com 2 vitórias ou fim da 3ª rodada. | ✅ Atendido | Implementado no laço de `handleWin` limitando e incrementando as rodadas; limpa apenas o grid preservando a pontuação. |
| **CA-06** | Efeitos Visuais de Vitória: Linha contínua sobre as 3 células e confetes. | ✅ Atendido | Div `#win-line` posicionada e rotacionada via classes CSS específicas com base no index da matriz de vitória; canvas injetado para disparo da animação. |
| **CA-07** | Autonomia de Áudio: Efeitos sonoros sem arquivos mp3. | ✅ Atendido | Sintetizador puro utilizando classes base da `window.AudioContext` oscilando frequências para tons de X, O, Vitória (Acorde) e Empate (Descendente). |

## 4. Conclusão da Auditoria
A aplicação foi validada garantindo 100% de compliance com o caso de uso (CDU) "Jogar Jogo da Velha", englobando ambos os fluxos (Principal de PvP, Alternativos de MD3 e CPU, além de Exceção de Empate). As restrições arquiteturais (arquivo único) foram plenamente satisfeitas.
