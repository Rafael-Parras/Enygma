# Enygma

    #include <stdio.h>
    #include <stdlib.h>
    #include <time.h>

    void criptografar();
    void descriptografar();
    void gerarMapa();

    char mapa[26];
    char mapa_inverso[26];

    int main(){
    int opcao;

    srand(time(NULL));
    gerarMapa(); // gera o alfabeto UMA vez

    do{
        printf("\n---------------------------------------------------------------------------------------------\n");
        printf("1 - Criptografar\n");
        printf("2 - Descriptografar\n");
        printf("0 - Sair\n");
        printf("---------------------------------------------------------------------------------------------\n");

        printf("Digite a opcao desejada: ");
        scanf("%d",&opcao);

        switch (opcao){
            case 1:
                criptografar();
                break;
            case 2:
                descriptografar();
                break;
            case 0:
                printf("Saindo...\n");
                break;
            default:
                printf("Opcao invalida! Tente novamente.\n");
        }

        } while (opcao != 0);

        return 0;
        }   

        void gerarMapa(){
        char letras[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

        // copia inicial
        for (int i = 0; i < 26; i++) {
        mapa[i] = letras[i];
        }

        // embaralhar (Fisher-Yates)
        for (int i = 25; i > 0; i--) {
        int j = rand() % (i + 1);

        char temp = mapa[i];
        mapa[i] = mapa[j];
        mapa[j] = temp;
    }

    // criar mapa inverso
    for (int i = 0; i < 26; i++) {
        mapa_inverso[mapa[i] - 'A'] = 'A' + i;
    }
    }

    void criptografar(){
    char texto[100];

    printf("Digite o texto (sem espaco): ");
    scanf("%s", texto);

    for (int i = 0; texto[i] != '\0'; i++) {
        if (texto[i] >= 'A' && texto[i] <= 'Z') {
            texto[i] = mapa[texto[i] - 'A'];
        }
    }

    printf("Criptografado: %s\n", texto);
    }

    void descriptografar(){
    char texto[100];

    printf("Digite o texto (sem espaco): ");
    scanf("%s", texto);

    for (int i = 0; texto[i] != '\0'; i++) {
        if (texto[i] >= 'A' && texto[i] <= 'Z') {
            texto[i] = mapa_inverso[texto[i] - 'A'];
        }
    }

    printf("Descriptografado: %s\n", texto);
    }

