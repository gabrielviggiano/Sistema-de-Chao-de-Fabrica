# Estrutura-de-Dados

Sistema de chão de fábrica. Realizado na disciplina de Estrutura de Dados, ministrada por Flavio Lamas.

Especificação do trabalho:

Uma empresa que fabrica rolamentos possui maquinarios para produzi-los, requisicoes de pedidos. 

O processo dela eh o seguinte: chega um pedido de um rolamento especifico, podendo ser cilindrico, conico, esferico de aco ou de titanio. Cada rolamento tem uma ordem a ser seguida nas maquinas e um tempo pra ficar la dentro sendo processada, alem de uma prioridade especifica pra cada pedido. As maquinas possuem filas de prioridade onde os pedidos ficam a medida que sejam requisitados.
Somente depois de sair da ultima maquina que o pedido deveria ficar, eh que finalmente o pedido fica pronto.
Um rolamento cilindrico possui prioridade 1, o conico possui prioridade 2, e esferico prioridade 3. Quanto maior o numero, mais urgente eh o pedido. A media de chegada de um pedido de rolamento cilindrico eh de 21.5 , de um conico 19.1 e de um esferico 8.0. Quando chega um pedido esferico, tem 10% de chance de ser um pedido de titanio.

Ordens do maquinário:
a ordem do maquinario para um rolamento cilindrico eh TORNO,FRESA,TORNO,MANDRIL.
a ordem do maquinario para um rolamento conico eh TORNO,MANDRIL,TORNO.
a ordem do maquinario para um rolamento esferico de aco eh FRESA,MANDRIL,TORNO.
a ordem do maquinario para um rolamento esferico de titanio eh FRESA,MANDRIL,TORNO,FRESA,TORN


Observações: deve ser utilizado fila e lista nesse problema, [fila de prioridade] , structs, alem de TADs. Flags nao serao aceitos, usem DEFINE ou ENUM para simular as prioridades. Ponteiro para funcao será necessario em praticamente todas structs para nao ter que
saber qual tipo que foi passado e somente precisar saber em tempo real.


Especificações de tempo:
o tempo de estadia no mandril eh 1.2 , 2.1 , 1.4 e 1.5 para cilindrico, conico, aco e titanio, respectivamente.
o tempo de estadia na fresa eh 0.5 , 0.5 e 0.6 para cilindrico, aco e titanio, respectivamente.
o tempo de estadia no torno eh 0.8 , 1.8 , 1.0 e 1.6 para cilindrico, conico, aco e titanio, respectivamente.

Entao resumindo tudo:
Estadia_Mandril_Cilindrico 1.2<br>
Estadia_Fresa_Cilindrico 0.5<br>
Estadia_Torno_Cilindrico 0.8<br>

Estadia_Mandril_Conico 2.1
Estadia_Torno_Conico 1.8

Estadia_Mandril_Esferico_Aco 1.4
Estadia_Fresa_Esferico_Aco 0.5
Estadia_Torno_Esferico_Aco 1.0

Estadia_Mandril_Esferico_Titanio 1.5
Estadia_Fresa_Esferico_Titanio 0.6
Estadia_Torno_Esferico_Titanio 1.6

Chegada_Media_Cilindrico 21.5
Chegada_Media_Conico 19.1
Chegada_Media_Esferico 8.0

sequencia_cilindrica eh TORNO,FRESA,TORNO,MANDRIL
sequencia_conica eh TORNO,MANDRIL,TORNO
sequencia_esferica_titanio eh FRESA,MANDRIL,TORNO,FRESA,TORNO
sequencia_esferica_aco eh FRESA,MANDRIL,TORNO

Seu objetivo eh fazer um simulador dessa empresa que usando todos os dados definidos anteriormente e recebendo como argumento de entrada do programa C um double que representará o tempo de simulacao total, imprima na tela quantos rolamentos foram construidos de cada tipo e o tempo medio de construcao de cada tipo. ps: faca o simulador dividindo tudo em bibliotecas [ ou seja, varios arquivos ] , faca pouco a pouco, juntar tudo de vez certamente baguncará sua cabeca e colocara ainda mais dificuldade na hora de debugar.

A funcao gera_exponencial abaixo retorna o tempo que vai demorar para chegar outro pedido, passando como argumento a media de chegada do
pedido que voce quer saber.

#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <time.h>

float Gera_Exponencial (float avg)
{
    float u=0; /* Gera randomicamente um numero entre 0 e 1 */
    do 
        u = ((float)rand()) / ((float) RAND_MAX);
    while ((u==0) || (u==1));
    return (-avg * log (u));
}

para saber quanto tempo o rolamento vai ficar no maquinario, use a funcao abaixo: 
float tempo(float Estadia_Equipamento_Rolamento)
{
    float u = ((float)rand()) / ((float) RAND_MAX);
    return 2.0 * Estadia_Equipamento_Rolamento * u;
}

/*teste pra ver funcionando soh os geradores */
int main()
{
    srand(time(NULL));  /* <-- obrigatorio ter uma vez apenas no seu codigo */
    printf("%f \n" , Gera_Exponencial(21.5));
    printf("%f \n" , tempo(1.6));
    return 0;
}
a entrada será apenas o numero de clicks que seu codigo rodará;
ex:
./simulador 200
rodará por 200 segundos
a saida deve seguir o seguinte padrao:
$ ./oi.exe 1000000
Cilindros : 29.69       46768        
Conicos   : 19.220    52096       
Aco       :   5.409       124385
Titanio   : 10.499      125468

O comando para impressao entao deve seguir o seguinte formato
printf("<tipo de rolamento>   : %7.2f \t %d \n",variaveltempomedio, variavelquantidade);
