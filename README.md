# Desafio-2-DIO.me-C/C++
# jogo da velha

#include <stdio.h>
#include <stdbool.h>

// Função para imprimir o tabuleiro
void imprimirTabuleiro(char tabuleiro[3][3]) {
    printf("\n  0 1 2\n");
    for (int i = 0; i < 3; ++i) {
        printf("%d ", i);
        for (int j = 0; j < 3; ++j) {
            printf("%c ", tabuleiro[i][j]);
        }
        printf("\n");
    }
}

// Função para verificar se houve vitória
bool verificarVitoria(char tabuleiro[3][3], char jogador) {
    // Verificar linhas e colunas
    for (int i = 0; i < 3; ++i) {
        if ((tabuleiro[i][0] == jogador && tabuleiro[i][1] == jogador && tabuleiro[i][2] == jogador) ||
            (tabuleiro[0][i] == jogador && tabuleiro[1][i] == jogador && tabuleiro[2][i] == jogador)) {
            return true;
        }
    }

    // Verificar diagonais
    if ((tabuleiro[0][0] == jogador && tabuleiro[1][1] == jogador && tabuleiro[2][2] == jogador) ||
        (tabuleiro[0][2] == jogador && tabuleiro[1][1] == jogador && tabuleiro[2][0] == jogador)) {
        return true;
    }

    return false;
}

int main() {
    char tabuleiro[3][3] = {
        {'#', '#', '#'},
        {'#', '#', '#'},
        {'#', '#', '#'}
    };

    bool jogoAtivo = true;
    bool empate = false;
    char jogadorAtual = 'O'; // Começa com 'O'

    while (jogoAtivo) {
        imprimirTabuleiro(tabuleiro);

        int linha, coluna;
        printf("\nJogador %c, informe a linha e coluna para jogar (Ex: 0 1): ", jogadorAtual);
        scanf("%d %d", &linha, &coluna);

        // Verificar se a posição é válida
        if (linha < 0 || linha > 2 || coluna < 0 || coluna > 2 || tabuleiro[linha][coluna] != '#') {
            printf("Posição inválida. Tente novamente.\n");
            continue;
        }

        tabuleiro[linha][coluna] = jogadorAtual;

        // Verificar vitória
        if (verificarVitoria(tabuleiro, jogadorAtual)) {
            printf("\nJogador %c venceu!\n", jogadorAtual);
            jogoAtivo = false;
        } else {
            // Mudar jogador
            jogadorAtual = (jogadorAtual == 'O') ? 'X' : 'O';
        }

        // Verificar empate
        empate = true;
        for (int i = 0; i < 3; ++i) {
            for (int j = 0; j < 3; ++j) {
                if (tabuleiro[i][j] == '#') {
                    empate = false;
                    break;
                }
            }
        }

        if (empate) {
            printf("\nEmpate!\n");
            break;
        }
    }

    char jogarNovamente;
    printf("\nDeseja jogar novamente? (S/N): ");
    scanf(" %c", &jogarNovamente);

    if (jogarNovamente == 'S' || jogarNovamente == 's') {
        main(); // Reiniciar o jogo
    } else {
        printf("Obrigado por jogar!\n");
    }

    return 0;
}
