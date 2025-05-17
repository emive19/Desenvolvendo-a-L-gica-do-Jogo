# Desenvolvendo-a-L-gica-do-Jogo
#include <stdio.h>
#include <string.h>

// Estrutura da carta
struct Carta {
    char nome[30];
    int populacao;
    float area;
    float densidadeDemografica;
};

// Função para exibir os atributos disponíveis
void exibirMenu(int opcaoJaEscolhida) {
    printf("Escolha um atributo:\n");
    if (opcaoJaEscolhida != 1) printf("1 - Populacao\n");
    if (opcaoJaEscolhida != 2) printf("2 - Area\n");
    if (opcaoJaEscolhida != 3) printf("3 - Densidade Demografica\n");
}

// Função para capturar uma escolha válida
int escolherAtributo(int opcaoJaEscolhida) {
    int escolha;
    do {
        printf("Digite o numero do atributo: ");
        scanf("%d", &escolha);
        if (escolha < 1 || escolha > 3 || escolha == opcaoJaEscolhida)
            printf("Opcao invalida. Tente novamente.\n");
    } while (escolha < 1 || escolha > 3 || escolha == opcaoJaEscolhida);
    return escolha;
}

// Função para pegar o valor de um atributo
float obterValor(struct Carta c, int atributo) {
    switch (atributo) {
        case 1: return c.populacao;
        case 2: return c.area;
        case 3: return c.densidadeDemografica;
        default: return 0;
    }
}

// Função para comparar os dois atributos
int compararAtributos(struct Carta c1, struct Carta c2, int attr1, int attr2) {
    float v1c1 = obterValor(c1, attr1);
    float v1c2 = obterValor(c2, attr1);
    float v2c1 = obterValor(c1, attr2);
    float v2c2 = obterValor(c2, attr2);

    printf("\nComparando os atributos:\n");
    printf("%s - %.2f e %.2f => Soma: %.2f\n", c1.nome, v1c1, v2c1, v1c1 + v2c1);
    printf("%s - %.2f e %.2f => Soma: %.2f\n", c2.nome, v1c2, v2c2, v1c2 + v2c2);

    // Lógica de vitória (atenção à Densidade Demográfica)
    float soma1 = ((attr1 == 3) ? -v1c1 : v1c1) + ((attr2 == 3) ? -v2c1 : v2c1);
    float soma2 = ((attr1 == 3) ? -v1c2 : v1c2) + ((attr2 == 3) ? -v2c2 : v2c2);

    return (soma1 > soma2) ? 1 : (soma1 < soma2 ? 2 : 0);
}

// Função para imprimir o nome do atributo
void imprimirNomeAtributo(int attr) {
    switch (attr) {
        case 1: printf("Populacao"); break;
        case 2: printf("Area"); break;
        case 3: printf("Densidade Demografica"); break;
    }
}

int main() {
    // Cartas pré-definidas
    struct Carta carta1 = {"Brasil", 213000000, 8515767.0, 25.0};
    struct Carta carta2 = {"Japao", 125800000, 377975.0, 332.0};

    printf("Comparacao entre %s e %s!\n", carta1.nome, carta2.nome);

    // Escolher primeiro atributo
    printf("\nEscolha o primeiro atributo:\n");
    exibirMenu(0);
    int atributo1 = escolherAtributo(0);

    // Escolher segundo atributo
    printf("\nEscolha o segundo atributo:\n");
    exibirMenu(atributo1);
    int atributo2 = escolherAtributo(atributo1);

    // Mostrar atributos escolhidos
    printf("\nAtributos escolhidos:\n1. ");
    imprimirNomeAtributo(atributo1);
    printf("\n2. ");
    imprimirNomeAtributo(atributo2);
    printf("\n");

    // Comparação
    int resultado = compararAtributos(carta1, carta2, atributo1, atributo2);

    // Resultado
    printf("\nResultado da rodada:\n");
    if (resultado == 1)
        printf("Vencedor: %s!\n", carta1.nome);
    else if (resultado == 2)
        printf("Vencedor: %s!\n", carta2.nome);
    else
        printf("Empate!\n");

    return 0;
}
