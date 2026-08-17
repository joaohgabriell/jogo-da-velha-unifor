# Especificação de Requisitos Funcionais
## Caso de Uso (CDU) - Jogo da Velha Web - UNIFOR

**Histórico de Versões**
| Data | Versão | Descrição | Autor |
|---|---|---|---|
| 08/08/2026 | 1.0 | Criação do caso de uso de Jogar Jogo da Velha | Equipe LAPIS |

### 1. Nome do Caso de Uso
Jogar Jogo da Velha

### 2. Objetivo
Permitir que o usuário dispute partidas do Jogo da Velha em ambiente web, oferecendo modos contra outro jogador local ou contra o computador, formatos de partida única ou Melhor de 3 (MD3), acompanhamento do placar, efeitos visuais da linha vitoriosa, efeitos sonoros e confetes na vitória.

### 3. Tipo de Caso de Uso
Concreto

### 4. Atores
**4.1 Primário:** Jogador: Inicia o caso de uso e realiza as jogadas no tabuleiro.
**4.2 Secundário:** Computador: Solução interna/autômata que responde ativamente às jogadas do Jogador quando o modo contra IA está ativado.

### 5. Precondições
O Jogador deve acessar a aplicação web por meio de um navegador compatível com suporte a JavaScript e Web Audio API.

### 6. Fluxo Principal
* **P1.** O Jogador acessa a aplicação.
* **P2.** O sistema exibe a interface principal contendo a identificação da universidade, título, seletores de modo e formato, placar, etc.
* **P3.** O Jogador seleciona uma célula vazia do tabuleiro.
* **P4.** O sistema registra a jogada do jogador atual.
  * P4.1. Preenche a célula selecionada com o símbolo do jogador atual ('X' ou 'O').
  * P4.2. Toca o efeito sonoro sintetizado correspondente ao símbolo.
  * P4.3. Avalia o tabuleiro em busca de combinações vitoriosas. [E1] [A1]
* **P5.** O sistema alterna o turno para o próximo jogador.
* **P6.** O sistema atualiza a mensagem de status.
* **P7.** O Jogador realiza a jogada seguinte. [A2]

### 7. Fluxos Alternativos
* **A1. Fim de Rodada por Vitória:** O sistema traça uma linha visual, dispara confetes, toca acorde de vitória, incrementa o placar e declara o vencedor (ou avança a rodada no formato MD3).
* **A2. Jogada do Computador (Modo Contra a CPU):** O sistema bloqueia cliques do jogador temporariamente, aguarda reflexão, escolhe uma posição e executa o movimento na vez do 'O'.
* **A3. Reinício da Partida:** O sistema zera o placar e contador de rodadas, oculta a linha vitoriosa e limpa as células.

### 8. Fluxos de Exceção
* **E1. Fim de Rodada por Empate:** O sistema toca som de empate, atualiza o status e, se for MD3, reinicia a rodada sem incrementar o contador.

### 9. Requisitos Não Funcionais
* **Interface Institucional:** Aplicação de paleta de cores e tipografia correspondentes à identidade visual da UNIFOR (Azul #003366, Azul Destaque #0056b3, Laranja #d97706 e Fundo #f4f6f9).
* **Sintetização de Áudio (Zero Dependência):** Efeitos sonoros gerados via Web Audio API nativa.
* **Portabilidade:** Execução completa contida em um único arquivo HTML/CSS/JS.

### 10. Critérios de Aceite
* [x] CA-01 (Fidelidade Visual): Aplicação utiliza a paleta UNIFOR.
* [x] CA-02 (Regra de Ocupação): Não é possível sobrescrever uma célula ocupada.
* [x] CA-03 (Bloqueio pós-Fim de Jogo): Bloqueia cliques em células vazias até próxima rodada.
* [x] CA-04 (Comportamento CPU): Sistema executa a jogada do robô na vez do 'O'.
* [x] CA-05 (Regra MD3): Zera o tabuleiro entre rodadas e só encerra com 2 vitórias.
* [x] CA-06 (Efeitos Visuais): Linha contínua sobre as 3 células e confetes.
* [x] CA-07 (Autonomia de Áudio): Emite efeitos sem depender de arquivos .mp3 externos.
