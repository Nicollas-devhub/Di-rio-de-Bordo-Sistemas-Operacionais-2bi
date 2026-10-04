1 ENTENDENDO A BARREIRA DO SISTEMA

Quando um processo responsável pela geração de um relatório precisa realizar a leitura de dados armazenados no disco, ele solicita essa operação ao Sistema Operacional por meio de uma chamada de sistema, conhecida como System Call. Essa chamada funciona como uma ponte de comunicação entre o espaço do usuário e o espaço do núcleo do sistema, denominado kernel.

O processo pode ser compreendido em quatro etapas principais.

1.1 Invocação da System Call

O processo executa uma função disponibilizada pela API do Sistema Operacional, solicitando uma determinada operação. Em sistemas Unix e Linux, por exemplo, pode ser utilizada a chamada read. No Windows, uma função equivalente é a ReadFile.

1.2 Troca de modo: Trap e interrupção

Após a solicitação, ocorre uma mudança do modo de execução da CPU. O processo deixa temporariamente o modo usuário e a execução passa para o modo privilegiado, também chamado de modo kernel ou modo supervisor.

Essa transição é controlada pelo hardware e pelo Sistema Operacional com o objetivo de impedir que programas comuns executem diretamente operações que possam comprometer a segurança ou a integridade do sistema.

1.3 Execução pelo Kernel

O Sistema Operacional assume o controle da operação solicitada. Nesse momento, o kernel verifica, entre outros aspectos, se o processo possui permissão para acessar o arquivo, se o arquivo existe e se os endereços de memória utilizados pela operação são válidos.

Depois dessas verificações, o Sistema Operacional solicita ao dispositivo de armazenamento que realize a leitura dos dados.

1.4 Retorno dos dados ao processo

Após a leitura das informações, o Sistema Operacional disponibiliza os dados para o processo solicitante, normalmente por meio de uma área de memória apropriada.

Em seguida, a execução retorna ao modo usuário e o programa continua sua execução a partir do ponto em que havia realizado a chamada de sistema. Dessa maneira, o processo responsável pela geração do relatório pode continuar utilizando os dados obtidos do disco.

2 MUDANÇA ENTRE O MODO USUÁRIO E O MODO KERNEL

A mudança de modo ocorre quando um programa precisa solicitar ao Sistema Operacional uma operação que não pode ser realizada diretamente no modo usuário.

Inicialmente, o processo prepara os argumentos necessários para a chamada de sistema, como o identificador do arquivo e o endereço de memória onde os dados deverão ser armazenados. Essas informações são disponibilizadas de acordo com as convenções definidas pela arquitetura e pelo Sistema Operacional.

Em seguida, o programa executa uma instrução especial que provoca a entrada no modo privilegiado. Essa transição pode ocorrer por meio de uma instrução de trap ou mecanismo equivalente.

Após a transição, o kernel passa a executar o código responsável por atender à solicitação. Nesse momento, ele verifica se a operação é válida e se o processo possui as permissões necessárias.

Por exemplo, no caso de uma leitura de arquivo, o Sistema Operacional verifica a existência do arquivo, as permissões de acesso e a validade dos endereços de memória envolvidos. Depois disso, realiza a operação solicitada de maneira controlada e segura.

Quando a operação é concluída, o resultado é devolvido ao processo e a CPU retorna ao modo usuário. Caso o processo tenha ficado bloqueado aguardando uma operação de entrada e saída, ele poderá voltar à fila de processos prontos quando estiver apto a continuar sua execução.

Essa separação entre modo usuário e modo kernel é fundamental para a segurança do sistema, pois impede que programas comuns tenham acesso direto a recursos críticos do computador.

3 ESCALONADOR

O escalonador de curto prazo, também chamado de scheduler, é um componente do Sistema Operacional responsável por selecionar qual processo da fila de prontos receberá a CPU para executar.

Seu funcionamento está diretamente relacionado ao desempenho do sistema. Entre os principais objetivos do escalonamento estão a utilização eficiente do processador e a redução do tempo de espera dos processos.

Um dos objetivos é manter a CPU ocupada sempre que houver processos prontos para execução, evitando períodos desnecessários de ociosidade.

Outro objetivo importante é reduzir o tempo de espera dos processos e proporcionar uma boa capacidade de resposta ao usuário. Nesse contexto, é importante diferenciar alguns conceitos.

O turnaround time corresponde ao tempo total entre a chegada de um processo e a sua conclusão. Já o tempo de resposta representa o intervalo entre a solicitação e o momento em que o processo começa a receber uma resposta ou atendimento.

4 TIPOS DE PROCESSOS
4.1 Processos I/O Bound

Os processos classificados como I/O Bound são aqueles que realizam uma quantidade significativa de operações de entrada e saída (Input/Output – I/O).

Esses processos passam parte considerável do seu tempo aguardando operações como leitura ou gravação em disco, comunicação pela rede ou interação com dispositivos.

Como exemplos, podem ser considerados navegadores, editores de texto e aplicações que realizam muitas operações de entrada e saída.

4.2 Processos CPU Bound

Os processos classificados como CPU Bound são aqueles que utilizam intensivamente o processador para realizar seus cálculos e operações.

Normalmente, realizam menos operações de entrada e saída e permanecem por mais tempo utilizando a CPU.

Como exemplos, podem ser citados programas de criptografia, processamento de imagens e aplicações que realizam cálculos científicos.

5 ALGORITMOS DE ESCALONAMENTO
5.1 FIFO ou FCFS – First In, First Out / First-Come, First-Served

O algoritmo FIFO, também conhecido como FCFS, utiliza uma fila simples em que o primeiro processo que chega é o primeiro a ser atendido.

No modelo tradicional não preemptivo, o processo permanece utilizando a CPU até terminar ou até realizar uma operação que provoque sua saída da CPU.

Vantagem

Uma das principais vantagens é a simplicidade de implementação, pois os processos são atendidos seguindo a ordem de chegada.

Desvantagem

Uma desvantagem importante é o aumento do tempo de espera quando um processo muito longo chega antes de vários processos menores. Esse comportamento pode gerar o chamado efeito comboio (convoy effect), prejudicando a responsividade do sistema.

Analogia com o banco

O FIFO pode ser comparado a uma fila de banco com apenas um caixa, na qual os clientes são atendidos exatamente na ordem em que chegaram.

Nesse cenário, não existe atendimento prioritário. Se uma pessoa estiver realizando um atendimento muito demorado, os demais clientes precisarão esperar até que esse atendimento seja finalizado.

5.2 SJF – Shortest Job First

O algoritmo SJF (Shortest Job First) prioriza os processos que possuem o menor tempo estimado de execução.

Dessa forma, os processos considerados mais rápidos são executados primeiro.

Vantagens

Uma das principais vantagens do SJF é a redução do tempo médio de espera quando as estimativas de duração dos processos são conhecidas ou podem ser calculadas de forma adequada.

Além disso, processos curtos conseguem ser atendidos rapidamente, melhorando o tempo médio de espera.

Problemas

Um dos principais problemas é a possibilidade de postergação indefinida, também conhecida como inanição (starvation). Processos longos podem permanecer esperando enquanto novos processos menores continuam chegando.

Outro problema é a dificuldade de prever com precisão quanto tempo um processo levará para utilizar a CPU.

Analogia com o banco

O SJF pode ser comparado a uma fila de banco em que os clientes com atendimentos mais rápidos recebem prioridade.

Nesse caso, uma pessoa que precisa realizar um atendimento mais demorado pode permanecer esperando enquanto os clientes com atendimentos rápidos são atendidos primeiro.

6 PROPONDO A SOLUÇÃO

Considerando o problema apresentado, envolvendo processos interativos responsáveis por atender usuários de uma interface web e processos Batch responsáveis pela geração de relatórios pesados, o algoritmo Round-Robin pode ser considerado uma alternativa adequada para melhorar a responsividade do sistema.

O Round-Robin utiliza o conceito de fatia de tempo, também chamado de quantum. Cada processo recebe uma determinada quantidade de tempo para utilizar a CPU.

Quando o processo não termina sua execução dentro do tempo determinado, ele é interrompido temporariamente e colocado novamente no final da fila de processos prontos. Em seguida, outro processo recebe a oportunidade de utilizar o processador.

Essa alternância entre os processos permite que aplicações interativas recebam oportunidades frequentes de execução, evitando que um processo muito longo monopolize a CPU.

Em uma aplicação web, essa característica pode contribuir para uma melhor percepção de fluidez por parte do usuário, principalmente quando existem várias tarefas concorrendo pela utilização do processador.

Portanto, o Round-Robin apresenta uma característica importante para ambientes interativos: a distribuição do tempo de processamento entre os processos.

7 INANIÇÃO (STARVATION)

A inanição ocorre quando um processo permanece esperando por um período excessivamente longo para receber os recursos necessários para sua execução.

Em sistemas multitarefa, diversos processos precisam compartilhar os recursos do computador, principalmente a CPU. O escalonador é responsável por definir qual processo será executado em determinado momento.

Quando um processo possui prioridade muito baixa e outros processos de maior prioridade continuam recebendo a CPU, pode ocorrer uma situação em que o processo de menor prioridade permaneça esperando indefinidamente.

A inanição é diferente do deadlock. Na inanição, um processo continua aguardando uma oportunidade de execução ou acesso a um recurso. Já no deadlock, dois ou mais processos podem permanecer bloqueados porque cada um depende de recursos que estão sendo mantidos pelos outros processos.

Uma técnica utilizada para reduzir a possibilidade de inanição é o Aging.

7.1 Aging

O Aging consiste no aumento gradual da prioridade de um processo conforme ele permanece esperando na fila de processos prontos.

O funcionamento pode ser resumido da seguinte forma:

Aumento gradual: conforme o processo permanece esperando, sua prioridade é aumentada gradualmente pelo Sistema Operacional.
Garantia de execução: depois de determinado período, a prioridade do processo que estava esperando pode alcançar um nível suficientemente alto para que ele seja selecionado pelo escalonador.
Fim do bloqueio: o processo finalmente recebe tempo de CPU e consegue continuar sua execução. Depois disso, o Sistema Operacional pode ajustar novamente suas prioridades de acordo com a política de escalonamento utilizada.

Dessa forma, o Aging ajuda a evitar que processos de baixa prioridade permaneçam indefinidamente sem receber tempo de processamento.

8 CONCLUSÃO

A análise dos conceitos de chamadas de sistema, modos de execução, escalonamento e inanição permite compreender como o Sistema Operacional controla os processos e os recursos do computador.

As chamadas de sistema são importantes porque permitem que programas no modo usuário solicitem serviços ao kernel de maneira controlada e segura. A separação entre modo usuário e modo kernel contribui para a proteção do sistema e impede que aplicações comuns tenham acesso direto a recursos críticos.

Em relação ao escalonamento, algoritmos como FIFO e SJF apresentam características diferentes e podem gerar vantagens ou problemas dependendo do cenário. Para ambientes interativos, como interfaces web, o Round-Robin apresenta uma alternativa interessante por distribuir o tempo de CPU entre os processos e proporcionar maior capacidade de resposta.

Por fim, mecanismos como o Aging são importantes para reduzir a possibilidade de inanição, garantindo que processos que permanecem esperando tenham sua prioridade aumentada gradualmente.

9 LINKS CONSULTADOS
9.1 Vídeo sobre processos interativos e processos Batch

Disponível em: https://www.google.com/search?q=videos+sobre+Processos+Interativos+Requisi%C3%A7%C3%B5es+r%C3%A1pidas+de+usu%C3%A1rios+acessando+a+interface+web+Processos+Batch+FCFS

Acesso em: 4 out. 2026.

9.2 IBM – Diagnosing lock escalation problem

IBM. Diagnosing lock escalation problem. Disponível em: https://www.ibm.com/docs/pt-br/db2/11.5.x?topic=problems-diagnosing-lock-escalation-problem

Acesso em: 4 out. 2026.

9.3 Instituto Federal de Educação, Ciência e Tecnologia Sul-rio-grandense – Sistemas Operacionais

INSTITUTO FEDERAL DE EDUCAÇÃO, CIÊNCIA E TECNOLOGIA SUL-RIO-GRANDENSE. Sistemas Operacionais. Disponível em: http://tics.ifsul.edu.br/matriz/conteudo/disciplinas/so/uf/1/4.html

Acesso em: 4 out. 2026.

9.4 Universidade Federal de Santa Catarina – Inanição

SOBRAL, Bosco. Inanição. Universidade Federal de Santa Catarina. Disponível em: https://www.inf.ufsc.br/~bosco.sobral/ensino/ine5645/Inanicao.pdf

Acesso em: 4 out. 2026.

