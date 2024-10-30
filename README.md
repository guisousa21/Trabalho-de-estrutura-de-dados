#include <stdio.h>
#include <stdlib.h>

typedef struct No {
    int dado;
    struct No* prox;
} No;

typedef struct {
    No* inicio;
} Lista;

Lista* criarLista() {
    Lista* lista = (Lista*) malloc(sizeof(Lista));
    lista->inicio = NULL;
    return lista;
}

int verificarVazia(Lista* lista) {
    return lista->inicio == NULL;
}

void inserirListaOrdenada(Lista* lista, int dado) {
}

void exibirLista(Lista* lista) {
    No* atual = lista->inicio;
    while (atual != NULL) {
        printf("%d ", atual->dado);
        atual = atual->prox;
    }
    printf("\n");
}

int buscarLista(Lista* lista, int dado) {
    No* atual = lista->inicio;
    while (atual != NULL && atual->dado != dado) {
        atual = atual->prox;
    }
    return atual != NULL;
}

void excluirLista(Lista* lista, int dado) {
    if (lista->inicio == NULL) return;

    if (lista->inicio->dado == dado) {
        No* aux = lista->inicio;
        lista->inicio = lista->inicio->prox;
        free(aux);
        return;
    }

    No* anterior = lista->inicio;
    No* atual = lista->inicio->prox;
    while (atual != NULL && atual->dado != dado) {
        anterior = atual;
        atual = atual->prox;
    }

    if (atual != NULL) {
        anterior->prox = atual->prox;
        free(atual);
    }
}

void liberarLista(Lista* lista) {
    No* atual = lista->inicio;
    while (atual != NULL) {
        No* prox = atual->prox;
        free(atual);
        atual = prox;
    }
    free(lista);
}

int main() {
    Lista* lista = criarLista();

    inserirListaOrdenada(lista, 5);
    inserirListaOrdenada(lista, 10);
    inserirListaOrdenada(lista, 3);
    inserirListaOrdenada(lista, 8);
    inserirListaOrdenada(lista, 1);

    printf("Lista ordenada: ");
    exibirLista(lista);

    liberarLista(lista);

    return 0;
}
