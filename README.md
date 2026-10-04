# Di-rio-de-Bordo-Sistemas-Operacionais-2bi

Entendendo a barreira do Sistema
 Quando gerado o processos da geração do Relatório é preciso ler dados do disco, ele solicita essa leitura ao Sistema Operacional por meio de uma chamada de sistema (System Call), que funciona como uma ponte para a comunicação entre o espaço do usuário e o espaço do núcleo (kernel).

 O processo ocorre em quatro passos: 
 1- Invocação da System Call: O processo executa uma função específica pela API do sistema operacional como read em sistemas Unix, Linux ou ReadFile no Windows.

 2- Troca de Modo(Trap/Interrupção): A CPU interrompe a execução do processo e muda do Modo Usuário para Modo Supervisor/Kernel. Garantindo a integridade da máquina.

 3- Execução pelo Kernel- O sistema Operacional assume o controle, valida se o processo tem permissão para acessar aquele tipo de arquivo e sendo assim aciona o drive do disco para buscar dados.


4- Retorno desses dados: Após o disco ler essas informações, o kernel copia os dados para a memória do processo, altera o modo da CPU de volta para o modo Usuário, devolvendo o controle do programa para o relatório prosseguir sua execução.

 Já quando ocorre esta mudança de modo  é onde a CPU altera seu nível de privilégio do modo Usuário para Modo Núcleo. Esta mudança é controlada rigidamente pelo hadware para impedir que o processo execute instruções perigosas. Para isso primeiramente ocorre o estado de bloqueio e a instrução de trap onde o programa coloca os argumentos da chamada exemplo: identificador do arquivo e o endereço de memória em registradores específicos da CPU, sendo assim ele executa uma instrução especial de máquina chamada trap(interrupção do software.). Apos se passa para a transiçãoo para o modo Kernel, onde a mudança de privilégio ocorre, fazendo com que o bit de modo no registrador de status da CPU é alterado de 1 para 0, colocando a CPU em privilégio máximo. E então a execução pelo Kernel e o Bloqueio do processo, onde quem executa não é mais o código do seu relatório, mas sim o próprio do Sistema Operacional, sendo assim o kernel valida a operação, vendo se os arquivos existem, se o usuário possui permissões necessárias para acessá-los e se os endereçoes de memória fornecidos são válidos. Após essa verificação, o Sistema Operacional executa a instrução solicitada de forma segura como por exemplo ler ou gravar dados no disco. Já que uma vez finalizada esta etapa a execução pelo Kernel, ocorre o processo inverso. O bit no registrador de status da CPU é alterado de 0 de volta para , restaurando o modo usuário. Pois o processo que estava bloqueado ele é liberado, recebendo o resultado da operação nos registradores e retoma sua execução normal a partir da instrução seguinte à trap.


 Escalonador:
 Escalonador de curto prazo, também chmado de scheduler, é a parte do sistema operacional que organiza e determina o funcionamneto da fila de prontos e o tempo que cada processo terá de execução no processador. Ele é avaliada em dois aspectos dentre eles estão Quanto a produção que o escalonador precisa manter o processador ocupado por mais tempo e produzir mais em menos tempo ou seja basicamente ele quer que o processador seja bem utilizado e não fique ocioso. Já o tempo de resposta (turnaround time) ele faz com que o baixo tempo médio de espera na fila do processador, fazendo com que o processador não fique por muito tempo na fila.

 Tipos de processos: I/O Bound – são processos caracterizados por fazer mais uso de requisições de I/O. Estes processos não “gastam” processador porque trabalham mais com entrada e saída. Por exemplo,editores de texto e browsers.
   CPU Bound – são processos caracterizados por fazer mais uso de CPU. Estes processos precisam de CPU para trabalhar, fazendo pouca I/O. Exemplos como, programas de criptografia e programas de cálculos cinetíficos.

   Algoritmos escalonadores:
   lgoritmo FIFO (first-in/first-out)
Este algoritmo implementa uma fila simples, onde o primeiro processo que chega na fila é executado até seu encerramento (processo não sai do processador até terminar seu processamento).

Vantagens:
Favorece processos do tipo CPU Bound porque estes “pegam” a CPU e não soltam mais;
Desvantagens:
Causa um aumento no tempo de espera da fila;
Analogia com o banco:
Este escalonador equivale a uma fila de banco, com apenas UM caixa, onde a ordem de atendimento é definida pela chegada na fila. A insatisfação dos clientes está em:
Não há atendimento prioritário;

Algoritmo SJF (Shortest Job First)
Trabalhos mais curtos primeiro - este algoritmo implementa uma fila ordenada pelo menor tempo de execução, ou seja, quanto menor o tempo de execução mais na frente da fila o processo está.

Vantagens:
Favorece processos I/O Bound, porque são rápidos na ocupação do processador;
Processos rápidos ficam pouco tempo na fila de espera – diminui o tempo médio de espera.
Problemas:
Postergação indefinida – processos considerados lentos ficarão esperando na fila por tempo indeterminado;
Impossibilidade de implementação – é impossível prever o tempo de execução de um processo.
Analogia com o banco:
Este escalonador equivale a uma fila de banco, com apenas UM caixa, onde a ordem de atendimento é definida pela quantidade de papéis a serem processados – se for rápido passa na frente. A insatisfação dos clientes está em:
Não há atendimento prioritário;
Se algum cliente tiver muitos papéis para serem processados, irá ficar na fila aguardando até que todos os “rapidinhos” sejam atendidos;



Propondo a Solução
 O algoritmo mais adequado para resolver este problema de responsividade em uma interface web seria o Round-Robin. Pois, interfaces de web exigem um sistema interativo, onde o tempo de resposta percebida pelo usuário final é a métrica mais crítica. Algumas vantagens do porque foi escolhido para este tipo de problema. O fatiamento de tempo ele aloca cada processo como a renderização de um elemento ou a resposta a um clique, alternância rápida, se um processo não terminar de executar dentro do seu quantum, ele é interrompido e colocado no fim da fila, sendo a CPU passada imediatamente para o próximo processo e a previsibilidade e fluidez onde essa alternância é rápida e garante que nenhum processo longo congele ou trave a execução. Para os usuários da web, isso cria uma ilusão de que todas as tarefas e interações estão acontecendo de forma fluida e simultânea.