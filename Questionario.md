# Questionário Sistemas Embarcados I

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
Quando um programa é compilado em uma plataforma diferente daquela em que será executado, isso se mostra vantajoso para o desenvolvimento de software destinado a plataformas diversas, particularmente quando os recursos disponíveis na plataforma de desenvolvimento são mais restritos em comparação com a plataforma alvo.

## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
São instruções que entram em ação durante a inicialização do sistema ou quando o programa é executado, tendo como propósito a preparação do ambiente para a execução do programa principal.

## 3. Sobre o utilitário **make** e o arquivo **Makefile responda**:

#### (a) Explique com suas palavras o que é e para que serve o **Makefile**.
É um arquivo de texto que contém instruções destinadas a automatizar o processo de compilação. Ele define as "regras" para a compilação do programa, especificando como os diferentes componentes devem ser compilados e vinculados para gerar o executável final.

#### (b) Descreva brevemente o processo realizado pelo utilitário **make** para compilar um programa.
   O processo é verificar as dependências de cada arquivo fonte e, se precisar, recompilar os arquivos que foram modificados.  

#### (c) Qual é a sintaxe utilizada para criar um novo **target**?
  targets: prerequisites
          	recipe  

#### (d) Como são definidas as dependências de um **target**, para que elas são utilizadas?
  É definido após o nome do target, representam os arquivos ou outros targets que o target atual depende para ser feito, o make usa essas dependencias para definir a ordem da compilação e recompilção do programa.

#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?
São instruções que indicam como o programa deve ser compilado. As regras implícitas são aquelas definidas pelo próprio sistema de compilação, enquanto as explícitas são desenvolvidas pelo próprio desenvolvedor, fornecendo diretrizes específicas sobre como compilar e construir o programa de acordo com as necessidades do projeto.

## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?
É uma versão compacta do conjunto de instruções ARM original, as vantagens dele é que ele utiliza apenas 16 bits para economizar espaço e melhorar a eficiência da memoria. O thumb opera em conjunto com o conjunto do ARM original, assim aproveitando a vantagem de ambos conjuntos de instruções.

### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Register***.
Na arquitetura ARM, as operações de Load/Store separam explicitamente as operações que acessam a memória das operações de processamento. Isso é feito usando instruções específicas de Load (carregamento) e Store (armazenamento) para acessar a memória. Por outro lado, na modalidade Register/Register, as operações de acesso à memória estão integradas às operações de processamento. Nesse caso, os registradores de dados são usados para acessar diretamente a memória, sem a necessidade de instruções separadas de Load e Store.

### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.
Para o acesso, temos o Privileged Mode, que concede ao software acesso total às instruções do processador. Nesse modo, o software tem controle total sobre o sistema quando executado, podendo utilizar todas as instruções e acessar todos os recursos do sistema. Por outro lado, o Unprivileged Mode restringe o acesso do software a certas instruções e recursos do sistema. O software não pode executar certas instruções privilegiadas e tem acesso limitado a recursos do sistema. Quanto aos modos de operação, temos o Thread Mode, utilizado para a execução normal de tarefas do usuário ou sistema. Nesse modo, as interrupções e exceções podem ser tratadas de acordo com as configurações de prioridade definidas. Por outro lado, o Handler Mode é ativado quando uma interrupção ocorre, priorizando o tratamento desses eventos em relação à execução normal do código. Nesse modo, as rotinas de tratamento de interrupção são executadas para lidar com as interrupções de forma adequada. Por fim, o Privileged Mode é um modo no qual o software pode executar instruções privilegiadas e acessar recursos exclusivos do sistema. Esse modo é geralmente utilizado para operações que exigem permissões especiais, como configurações de hardware e controle do sistema.

### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.
Ele trata as interrupções pelo sistema de priorização em  niveis de exceção e grupos de prioridade. Tem diversos tipos de interrupções, como reset, IRQ,FIQ e SVC e cada um tem sua propria prioridade. São criados grupos com as interrupções onde tem seus niveis de prioridade, e dentro de cada grupo são colocadas prioridades adicionais, onde esses grupos são o Group priority e as prioridades adicionais são as sub-priority.

### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?
 O CPSR armazena o estado atual do processador durante a execução do programa, e o SPSR é temporario para salvar o estado do processador antes que ele seja alterado por uma execução ou interrupção. 

### (f) Qual a finalidade do **LR** (***Link Register***)?
Isso descreve o propósito da pilha de chamadas em um programa. A pilha de chamadas é uma estrutura de dados que armazena informações sobre as chamadas de função em execução. Uma das informações importantes armazenadas na pilha de chamadas é o endereço de retorno de uma função. Esse endereço indica o ponto no programa onde a execução deve continuar após a conclusão da função atual. Assim, quando a função termina sua execução, o programa usa o endereço de retorno na pilha de chamadas para voltar à instrução de chamada original e continuar a execução a partir desse ponto. Essa técnica é fundamental para a execução de sub-rotinas e funções em linguagens de programação.

### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?
 Ele serve para armazena informações sonbre o estado atual do processador e informações importantes para o controle e o gerenciamento do processador.

### (h) O que é a tabela de vetores de interrupção?
Trata-se de uma tabela que mapeia os endereços de entrada de todas as interrupções suportadas pelo processador.

### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?
   Tem a finalidade de gerenciar as interrupções de forma que siga a hierarquia de prioridade e eficiente. Ele pode ser utilizado para que as interrupções sejam priorizadas de acordo com a sua importancia,para responder interrupções de forma eficiente, suporta uma interrupção enquanto outra esta sendo feita, permite que algumas interrupções sejam temporariamente desativasdas, mascaradas se necessario.

### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 
Esse processo de preenchimento do valor EXC_RETURN no Cortex-M tem como objetivo identificar o contexto da interrupção e realizar um retorno de interrupção adequado. O valor EXC_RETURN contém informações sobre o estado em que o processador estava antes da ocorrência da interrupção, permitindo que o sistema retorne ao seu estado anterior de maneira precisa e eficiente.

### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 
A diferença está relacionada ao suporte de ponto flutuante no Cortex-M4F e seu impacto no tempo de resposta e uso da pilha. No Cortex-M3, durante uma interrupção, o contexto do processador é automaticamente salvo na pilha principal. Porém, no Cortex-M4F, devido ao suporte de ponto flutuante, é possível utilizar uma pilha de contexto separada para salvar os registradores de ponto flutuante durante uma interrupção. O "lazy stack" é uma técnica que visa economizar tempo e espaço na pilha para o tratamento de interrupções. Com o "lazy stack", o salvamento dos registradores de ponto flutuante pode ser adiado até que sejam utilizados em uma interrupção. Esse comportamento é configurado através do bit "LSPACT", que pode ser ajustado durante a inicialização do sistema para ativar ou desativar o "lazy stack". Essa abordagem permite otimizar o desempenho do sistema, economizando recursos de memória e melhorando o tempo de resposta às interrupções.


## Referências

### Básicas

[1] [STM32F411xC Datasheet](https://www.st.com/resource/en/datasheet/stm32f411ce.pdf)

[2] [RM0383 Reference Manual](https://www.st.com/resource/en/reference_manual/rm0383-stm32f411xce-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)

[3] [Using the GNU Compiler Collection (GCC)](https://gcc.gnu.org/onlinedocs/gcc/index.html)

[4] [GNU Make](https://www.gnu.org/software/make/manual/html_node/index.html)

### Vídeos Microsoft Teams

[5] [05 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[6] [06 - Arquitetura Cortex-M Parte 1/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[7] [07 - Arquitetura Cortex-M Parte 2/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[8] [08 - Microcontroladores STM32](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[9] [10 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

### Material Suplementar

[5] [A General Overview of What Happens Before main()](https://embeddedartistry.com/blog/2019/04/08/a-general-overview-of-what-happens-before-main/)
 
[6] [Bare metal embedded lecture-1: Build process](https://youtu.be/qWqlkCLmZoE?si=mn5yDnJYudQ1PpZH)
 
[7] [Bare metal embedded lecture-2: Makefile and analyzing relocatable obj file](https://youtu.be/Bsq6P1B8JqI?si=yuNLPj3JQ-2IT1yo)
 
[8] [Bare metal embedded lecture-3: Writing MCU startup file from scratch](https://youtu.be/2Hm8eEHsgls?si=c27MpZ47ApiMSwHR)
 
[9] [Lecture 15: Booting Process](https://youtu.be/3brOzLJmeek?si=MsHRUEJP8zofjwJQ)
