#include <stdio.h>
#include <string.h>
#include <conio.h>
#include <stdlib.h>
#include <locale.h>
#include <ctype.h>
#include <time.h>

/*Um pequeno "Banco de dados" Dentro do código para ARMAZENAR
os dados do Usuário. A typedef nesse bloco de código cria um alias
(um nome alternativo) para a estrutura (struct) anônima
Neste caso, o alias é Usuario.
*/
typedef struct {
    char email[50], senha[20], cpf[12]; 
} Usuario;


//Ocultar senha
void getPassword(char *password, int maxLen) { 
    int i = 0;
    char c;
    while (1) {
        c = getch();
        if (c == '\r') { 
            break;
        } else if (c == '\b' && i > 0) { 
            printf("\b \b");
            i--;
        } else if (i < maxLen - 1) {
            password[i] = c;
            printf("*");
            i++;
        }
    }
    password[i] = '\0';
}


//CPF com 11 caracteres validar
int validarCPF(const char *cpf) {
    if (strlen(cpf) != 11) {
        return 0;
    }
    for (int i = 0; i < 11; ++i) {
        if (!isdigit(cpf[i])) {
            return 0;
        }
    }
    return 1;
}


//Senha com 7 caracteres validar
int validarSenha(const char *senhaTemp) {
    if (strlen(senhaTemp) < 6) {
        return 0;
    }
    for (int i = 0; i < 6; ++i) {
        if (!isdigit(senhaTemp[i])) {
            return 0;
        }
    }
    return 1;
}
    
int main() {
	//Permite o código a imprimir acentos e outras peripecias da linguagem portuguesa
	setlocale(LC_ALL,"Portuguese");

	//DECLARAÇÃO DE VARIÁVEIS
    Usuario usuarios[100];
    int totalUsuarios = 0;
    int opcao;
    char nome [50];
    char idade [3];
    char cpf [11];
    char email[50];
    char senha[20];
    int logado = 0;
    int i, ticket;
    

    do { //LOOP MAIS IMPORTANTE, ONDE O USUÁRIO SERÁ DIRECIONADO NA MAIORIA DOS FINAIS DE TOMADAS DE DECISÃO
    
        printf("\nBEM VINDO(A) AO SITE DO MUSEU!\n");
        printf("==============================\n\n");
        printf("MENU\n\n");
        printf("1. CRIAR CONTA\n\n");
        printf("2. LOGIN\n\n");
        printf("3. COMPRAR INGRESSO\n\n");
        printf("4. SAIR\n\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);

        switch(opcao) {
        case 1:
        //ENTRADA DE DADOS PARA CADASTRO
        system("cls");
        printf("==========\n");
        printf("CADASTRO\n");
        printf("==========\n\n");
        printf("\nDigite seu nome:");
        scanf("%s",nome);
        printf("\nDigite sua idade:");
        scanf("%s", idade);
        printf("\nDigite seu email: ");
        scanf("%s", email);
        
        strcpy(usuarios[totalUsuarios].email, email);
        
        //Entrada e Conferir se o CPF possui 11 caracteres, caso não tenha irá se repetir
            do {
                printf("\nDigite seu CPF: ");
                scanf("%s", cpf);
                } 
				while (!validarCPF(cpf));
                strcpy(usuarios[totalUsuarios].cpf, cpf);
            
            //Entrada e Conferir se a senha possui 7 caracteres numéricos, caso não tenha irá se repetir
            char senhaTemp[20];
            do {
                printf("\nDigite sua senha utilizando apenas números (minimo 7 dígitos):");
                getPassword(senhaTemp, sizeof(senhaTemp));
                } while (!validarSenha(senhaTemp));
                
            //Conferir se a senha é a mesma
            char confirmacaoSenha[20];
            printf("\nConfirme sua senha: ");
            getPassword(confirmacaoSenha, sizeof(confirmacaoSenha));

            if (strcmp(senhaTemp, confirmacaoSenha) == 0) {
                strcpy(usuarios[totalUsuarios].senha, senhaTemp);
                totalUsuarios++;
                
                printf("\n\n--------------------------");
                printf("\nConta criada com sucesso!\n");
                printf("--------------------------\n");
                
                //ABRINDO ARQUIVO CSV
                FILE *arq = fopen("cadastros.csv", "a"); 
            
	            if (arq != NULL) {
				    
				    fprintf(arq,"%s;%s;%s;%s;%s\n",nome,idade,email,cpf,senhaTemp);
				    
				    fclose(arq);
				}
				
				else {
			        printf("Erro ao abrir o arquivo de cadastro.\n");
			    }
			    
			    system("pause");
                system("cls");
                               
            } else {
                printf("\n\nAs senhas nao coincidem!\n");
                printf("volte ao cadastro e tente novamente.\n\n");
                system("pause");
                system("cls");
                break;
            }

            break;
            
        //VERIFICAÇÃO DE DADOS PARA LOGIN
        case 2:
        system("cls");
        printf("=======\n");
        printf("LOGIN\n");
        printf("=======\n\n");
        printf("Digite seu email: ");
        scanf("%s", email);
        printf("Digite sua senha: ");
        getPassword(senha, sizeof(senha));
                            // VERIFICA SE O USUÁRIO ESTÁ CADASTRADO (SE OS DADOS ESTÃO NO SISTEMA)
            for (int i = 0; i < totalUsuarios; ++i) {
                if (strcmp(email, usuarios[i].email) == 0 && strcmp(senha, usuarios[i].senha) == 0) {
                    logado = 1;
                    printf("\n\n--------------------------");
                    printf("\nLogin bem-sucedido!\n");
                    printf("--------------------------\n");
                    system("pause");
                    system("cls");
                    break;
                    }
                }
                // ERRO NO LOGIN (DADOS INEXISTENTES, ERRO NA SENHA OU EMAIL)
            if (!logado) {
                printf("\n\nEmail ou senha incorretos!\n");
                printf("\nSelecione a opção LOGIN para tentar novamente.\n\n\n");
                system("pause");
                system("cls");
                }
                break;
        case 3:
        if (logado){ //SE o login for bem sucedido, essa área poderá ser acessada
        	
        //Entrada de dados para a escolha da exposição, quantos ingressos comprar e declaração dos preços
        
	    int escolha;
        int escolha2;
        float preco = 30.00;
        float meia = 15.00;
        int quantidade;
        //ESCOLHA DA EXPOSIÇÃO
    system("cls");
    printf("====================\n");
    printf("COMPRA DE INGRESSOS\n");
    printf("====================\n\n");
    printf("Ingresso: R$%.2f\n", preco);
    printf("Limite de 10 ingressos por usuário!\n");
    printf("Meia entrada: R$%.2f \n\n\n", meia);
    
    printf("1. Comprar ingresso para 100 anos da semana de arte moderna\n\n");
    printf("2. Comprar ingresso para 150 anos de Santos Dumont\n\n");
    printf("3. Comprar ingresso para Jogos olímpicos Paris 2024\n\n");
    printf("4. Comprar ingresso para Estande Rei Pelé\n\n");
    printf("5. Voltar\n\n\n");
    printf("Escolha uma opção:\n");
    scanf("%d", &escolha);

    switch(escolha) {
            break;
            case 4:
            int i;
            char dia[5];
            int hora;
            printf("\nPaga meia? \n\n");
        	printf("1. Sim \n\n");
        	printf("2. Não \n");
        	scanf("%d", &escolha2);
        	if(escolha2==1){ 
            printf("\nDigite o dia que gostaria de assistir a exposição.  Exemplo 11/10\n");
            scanf("%s", &dia);
            printf("\nDigite o horario da sua exposição entre as opções disponiveis\n 10h - 12h - 14h - 16h - 18h - 20h\n");
            scanf("%d", &hora);
            printf("\nQuantos ingressos meia entrada você deseja comprar?\n");
            scanf("%d", &quantidade);
            if (quantidade <= 0) {
                printf("Quantidade inválida.\n");
            } 
            // 	PAGAMENTO MEIA ENTRADA
			else {
            float total = meia * quantidade;
            printf("--------------------------");
            printf("\nTotal a pagar: R$%.2f\n", total);
            printf("--------------------------\n");
            printf("Forma de Pagamento:\n\n");
            printf("1. PIX\n");
            printf("2. CARTÃO DE CRÉDITO/DÉBITO\n");
            scanf("%d", &i);
            
            if(i==1){
            	system("cls");
            	printf("---------------------------------------------------\n\n");
            	printf("COMPRA CONCLUÍDA.\n\n");
            	printf("---------------------------------------------------\n\n");
            	printf("Nome: %s \n",nome);
            	printf("CPF: %s \n\n", cpf);
            	printf("---------------------------------------------------\n\n");
            	printf("Exposição: REI PELÉ\n\n");
            	printf("---------------------------------------------------\n\n");
            	printf("Dia %s - Horario %dh\n\n", dia, hora);
            	printf("---------------------------------------------------\n\n");
            	printf("Preço:R$%.2f\n",total);
            	printf("Método de pagamento: PIX\n\n");
            	printf("---------------------------------------------------\n\n");
            	
            	int i, randomNumber;
            	
            	for (i = 0; i<quantidade;i++){
                randomNumber = rand() % 900000 + 100000;
                printf("Ticket %d: %d\n\n", i + 1, randomNumber);
                }
            	printf("---------------------------------------------------\n\n");
            	
            	//Abrindo CSV dos tickets
            	FILE *tick = fopen("tickets.csv", "a+");
            
	            if (tick != NULL) {
	            	
	            	fprintf(tick,"%s;",cpf);
				    
				    for(i=0;i<quantidade;i++){
						fprintf(tick,"%d",randomNumber);
						if (i!= quantidade-1) fprintf(tick,";");
						else  fprintf(tick,"\n");
					}			
				    
				    fclose(tick);
				}
				
				else {
			        printf("Erro ao abrir o arquivo de cadastro.\n");
			    }
            	
            	
				system("pause");
				system("cls");
            	break; // Volta ao menu
			}
			else if(i==2){
				system("cls");
				printf("---------------------------------------------------\n\n");
            	printf("COMPRA CONCLUÍDA.\n\n");
            	printf("---------------------------------------------------\n\n");
            	printf("Nome: %s \n",nome);
            	printf("CPF: %s \n\n", cpf);
            	printf("---------------------------------------------------\n\n");
            	printf("Exposição: REI PELÉ\n\n");
            	printf("---------------------------------------------------\n\n");
            	printf("Dia %s - Horario %dh\n\n", dia, hora);
            	printf("---------------------------------------------------\n\n");
            	printf("Preço:R$%.2f\n",total);
            	printf("Método de pagamento: Cartão de crédito/débito\n\n");
            	printf("---------------------------------------------------\n\n");
            	
            	int i, randomNumber;
            	
            	for (i = 0; i<quantidade;i++){
                randomNumber = rand() % 900000 + 100000;
                printf("Ticket %d: %d\n\n", i + 1, randomNumber);
                }
            	printf("---------------------------------------------------\n\n");
            	
            	FILE *tick = fopen("tickets.csv", "a+");
            
	            if (tick != NULL) {
	            	
	            	fprintf(tick,"%s;",cpf);
				    
				    for(i=0;i<quantidade;i++){
						fprintf(tick,"%d",randomNumber);
						if (i!= quantidade-1) fprintf(tick,";");
						else  fprintf(tick,"\n");
					}			
				    
				    fclose(tick);
				}
				
				else {
			        printf("Erro ao abrir o arquivo de cadastro.\n");
			    }
            	
            	
				system("pause");
				system("cls");
				break; // Volta ao menu
			}
			else{
				printf("Opção inválida!");
			}
            return 0;
            }
                
                // PAGAMENTO ENTRADA INTEIRA
			}
			else{
			printf("\nDigite o dia que gostaria de assistir a exposição.  Exemplo 11/10\n");
            scanf("%s", &dia);
            printf("\nDigite o horario da sua exposição entre as opções disponiveis\n 10h - 12h - 14h - 16h - 18h - 20h\n");
            scanf("%d", &hora);
            printf("\nQuantos ingressos inteiros você deseja comprar?");
            scanf("%d", &quantidade);
            if (quantidade <= 0) {
                printf("Quantidade inválida.\n");
            } else { 
                float total = preco * quantidade;
                printf("--------------------------");
                printf("\nTotal a pagar: R$%.2f\n", total);
                printf("--------------------------\n");
                printf("Forma de Pagamento:\n\n");
                printf("1. PIX \n");
                printf("2. CARTÃO DE CRÉDITO/DÉBITO\n");
                scanf("%d", &i);
                if(i==1){
            	system("cls");
            	printf("---------------------------------------------------\n\n");
            	printf("COMPRA CONCLUÍDA.\n\n");
            	printf("---------------------------------------------------\n\n");
            	printf("Nome: %s \n",nome);
            	printf("CPF: %s \n\n", cpf);
            	printf("---------------------------------------------------\n\n");
            	printf("Exposição: REI PELÉ\n\n");
            	printf("---------------------------------------------------\n\n");
            	printf("Dia %s - Horario %dh\n\n", dia, hora);
            	printf("---------------------------------------------------\n\n");
            	printf("Preço:R$%.2f\n",total);
            	printf("Método de pagamento: PIX\n\n");
            	printf("---------------------------------------------------\n\n");
            	
            	int i, randomNumber;
            	
            	for (i = 0; i<quantidade;i++){
                randomNumber = rand() % 900000 + 100000;
                printf("Ticket %d: %d\n\n", i + 1, randomNumber);
                }
            	printf("---------------------------------------------------\n\n");
            	
            	FILE *tick = fopen("tickets.csv", "a+");
            
	            if (tick != NULL) {
	            	
	            	fprintf(tick,"%s;",cpf);
				    
				    for(i=0;i<quantidade;i++){
						fprintf(tick,"%d",randomNumber);
						if (i!= quantidade-1) fprintf(tick,";");
						else  fprintf(tick,"\n");
					}			
				    
				    fclose(tick);
				}
				
				else {
			        printf("Erro ao abrir o arquivo de cadastro.\n");
			    }
            	
            	
				system("pause");
				system("cls");
            	break; // Volta ao menu
			}
			else if(i==2){
				system("cls");
				printf("---------------------------------------------------\n\n");
            	printf("COMPRA CONCLUÍDA.\n\n");
            	printf("---------------------------------------------------\n\n");
            	printf("Nome: %s \n",nome);
            	printf("CPF: %s \n\n", cpf);
            	printf("---------------------------------------------------\n\n");
            	printf("Exposição: REI PELÉ\n\n");
            	printf("---------------------------------------------------\n\n");
            	printf("Dia %s - Horario %dh\n\n", dia, hora);
            	printf("---------------------------------------------------\n\n");
            	printf("Preço:R$%.2f\n",total);
            	printf("Método de pagamento: Cartão de crédito/débito\n\n");
            	printf("---------------------------------------------------\n\n");
            	
            	int i, randomNumber;
            	
            	for (i = 0; i<quantidade;i++){
                randomNumber = rand() % 900000 + 100000;
                printf("Ticket %d: %d\n\n", i + 1, randomNumber);
                }
            	printf("---------------------------------------------------\n\n");
            	
            	FILE *tick = fopen("tickets.csv", "a+");
            
	            if (tick != NULL) {
	            	
	            	fprintf(tick,"%s;",cpf);
				    
				    for(i=0;i<quantidade;i++){
						fprintf(tick,"%d",randomNumber);
						if (i!= quantidade-1) fprintf(tick,";");
						else  fprintf(tick,"\n");
					}			
				    
				    fclose(tick);
				}
				
				else {
			        printf("Erro ao abrir o arquivo de cadastro.\n");
			    }
            	
            	
				system("pause");
				system("cls");
				break; // Volta ao menu
			}
			else{
				printf("Opção inválida!");
			}
            return 0; // Motivo dos break retornarem ao menu
            }
        }
            break;
            
            case 5:
            system("cls");
            break;
            
            // ERRO AO ESCOLHER OUTRA EXPOSIÇÃO
            default:
            printf("encontramos um erro na seleção de exposição!\n");
            printf("Provavelmente os ingressos para essa exposição ja expiraram.\n");
            printf("Tente novamente, se o problema persistir, consulte o suporte.\n\n");
            system("pause");
            system("cls");
            }
                } else {
                    printf("\nVocê precisa estar logado para comprar ingressos!\n\n");
                    system("pause");
                    system("cls");
                }
                break;
            case 4:
                printf("\nSaindo do programa. Obrigado e volte sempre!\n");
                break;
            default:
                printf("\nOpcao inválida! Tente novamente.\n\n");
                system ("pause");
                system("cls");
        }
         
    } while(opcao != 4);
    
    return 0;
}
