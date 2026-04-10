    #include <stdio.h>
    #include <string.h>

    char alfabeto_normal[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

    // alfabetos pré-definidos
    char codigoA[] = "IJKLMNOPQRSTUVWXYZABCDEFGH";
    char codigoB[] = "DEFGHIJKLMNOPQRSTUVWXYZABC";
    char codigoC[] = "TUVWXYZABCDEFGHIJKLMNOPQRS";
    char codigoD[] = "MNOPQRSTUVWXYZABCDEFGHIJKL";
    char codigoE[] = "PQRSTUVWXYZABCDEFGHIJKLMNO";
    char codigoF[] = "GHIJKLMNOPQRSTUVWXYZABCDEF";

    // senhas
    char senhaA[] = "123";
    char senhaB[] = "456";
    char senhaC[] = "789";
    char senhaD[] = "111";
    char senhaE[] = "222";
    char senhaF[] = "333";

    // função pra escolher o alfabeto
    char* escolherCodigo(char chave) {
    if (chave == 'A') return codigoA;
    if (chave == 'B') return codigoB;
    if (chave == 'C') return codigoC;
    if (chave == 'D') return codigoD;
    if (chave == 'E') return codigoE;
    if (chave == 'F') return codigoF;

    return alfabeto_normal;
    }

    // validar senha
    int validarSenha(char chave) {
    char senha[20];

    printf("Digite a senha: ");
    scanf("%s", senha);

    if (chave == 'A' && strcmp(senha, senhaA) == 0) return 1;
    if (chave == 'B' && strcmp(senha, senhaB) == 0) return 1;
    if (chave == 'C' && strcmp(senha, senhaC) == 0) return 1;
    if (chave == 'D' && strcmp(senha, senhaD) == 0) return 1;
    if (chave == 'E' && strcmp(senha, senhaE) == 0) return 1;
    if (chave == 'F' && strcmp(senha, senhaF) == 0) return 1;

    printf("Senha incorreta!\n");
    return 0;
    }

    // criptografar
    void criptografar(char chave) {
    if (!validarSenha(chave)) return;

    char texto[100];
    char *codigo = escolherCodigo(chave);

    printf("Digite o texto (MAIUSCULO): ");
    getchar();
    fgets(texto, 100, stdin);

    for (int i = 0; texto[i] != '\0'; i++) {
        if (texto[i] >= 'A' && texto[i] <= 'Z') {
            int pos = texto[i] - 'A';
            texto[i] = codigo[pos];
        }
    }

    printf("Criptografado: %s\n", texto);
    }

    // descriptografar
    void descriptografar(char chave) {
    if (!validarSenha(chave)) return;

    char texto[100];
    char *codigo = escolherCodigo(chave);

    printf("Digite o texto (MAIUSCULO): ");
    getchar();
    fgets(texto, 100, stdin);

    for (int i = 0; texto[i] != '\0'; i++) {
        if (texto[i] >= 'A' && texto[i] <= 'Z') {
            for (int j = 0; j < 26; j++) {
                if (texto[i] == codigo[j]) {
                    texto[i] = alfabeto_normal[j];
                    break;
                }
            }
        }
    }

    printf("Descriptografado: %s\n", texto);
    }

    int main() {
    int opcao;
    char chave;

    printf("Escolha a chave: ");
    scanf(" %c", &chave);

    do {
        printf("\n1 - Criptografar\n");
        printf("2 - Descriptografar\n");
        printf("0 - Sair\n");
        printf("Opcao: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                criptografar(chave);
                break;
            case 2:
                descriptografar(chave);
                break;
        }

    } while (opcao != 0);

    return 0;
    }

    
