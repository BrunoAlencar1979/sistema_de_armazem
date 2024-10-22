# sistema_de_armazem
Sistema de Armazém  para controle de entrada e saída de produtos.
# Codigo em C

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_PRODUTOS 100

typedef struct {
    int id;
    char nome[50];
    float preco;
} Produto;

Produto produtos[MAX_PRODUTOS];
int num_produtos = 0;

void adicionar_produto() {
    if (num_produtos >= MAX_PRODUTOS) {
        printf("Limite de produtos atingido.\n");
        return;
    }

    Produto p;
    p.id = num_produtos + 1; // Atribuindo ID baseado na quantidade atual
    printf("Digite o nome do produto: ");
    scanf("%s", p.nome);
    printf("Digite o preco do produto: ");
    scanf("%f", &p.preco);

    produtos[num_produtos] = p;
    num_produtos++;
    printf("Produto adicionado com sucesso!\n");
}

void remover_produto() {
    int id;
    printf("Digite o ID do produto a ser removido: ");
    scanf("%d", &id);

    if (id <= 0 || id > num_produtos) {
        printf("Produto não encontrado.\n");
        return;
    }

    // Move os produtos para "fechar" o espaço vazio
    for (int i = id - 1; i < num_produtos - 1; i++) {
        produtos[i] = produtos[i + 1];
    }
    num_produtos--;

    // Atualiza os IDs dos produtos restantes
    for (int i = 0; i < num_produtos; i++) {
        produtos[i].id = i + 1;
    }

    printf("Produto removido com sucesso!\n");
}

void ver_detalhes_produto() {
    int id;
    printf("Digite o ID do produto para ver detalhes: ");
    scanf("%d", &id);

    if (id <= 0 || id > num_produtos) {
        printf("Produto não encontrado.\n");
        return;
    }

    Produto p = produtos[id - 1];
    printf("ID: %d\nNome: %s\nPreço: %.2f\n", p.id, p.nome, p.preco);
}

void exibir_produtos() {
    if (num_produtos == 0) {
        printf("Nenhum produto cadastrado.\n");
        return;
    }

    printf("Produtos cadastrados:\n");
    for (int i = 0; i < num_produtos; i++) {
        printf("ID: %d | Nome: %s | Preço: %.2f\n", produtos[i].id, produtos[i].nome, produtos[i].preco);
    }
}

int main() {
    int opcao;

    do {
        printf("\nMenu:\n");
        printf("1. Adicionar Produto\n");
        printf("2. Remover Produto\n");
        printf("3. Ver Detalhes do Produto\n");
        printf("4. Exibir Produtos\n");
        printf("5. Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                adicionar_produto();
                break;
            case 2:
                remover_produto();
                break;
            case 3:
                ver_detalhes_produto();
                break;
            case 4:
                exibir_produtos();
                break;
            case 5:
                printf("Saindo...\n");
                break;
            default:
                printf("Opção inválida! Tente novamente.\n");
        }
    } while (opcao != 5);

    return 0;
}
