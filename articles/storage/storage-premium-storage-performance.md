---
title: 'Armazenamento Premium do Azure: projetado para desempenho | Microsoft Docs'
description: "Crie aplicativos de alto desempenho usando o Armazenamento Premium do Azure. O Armazenamento Premium dá suporte ao disco de alto desempenho e baixa latência para cargas de trabalho que usam muita E/S em execução em máquinas virtuais do Azure."
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: e6a409c3-d31a-4704-a93c-0a04fdc95960
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: aungoo
ms.openlocfilehash: 75845eb4707e8e5606153a5e1a7c10b4113ee121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-premium-storage-design-for-high-performance"></a>Armazenamento Premium do Azure: projeto para alto desempenho
## <a name="overview"></a>Visão geral
Este artigo fornece diretrizes para a criação de aplicativos de alto desempenho usando o Armazenamento Premium do Azure. Você pode usar instruções Olá fornecidas neste documento combinado com desempenho melhores práticas aplicável tootechnologies usados pelo seu aplicativo. diretrizes de saudação tooillustrate, usamos SQL Server em execução no armazenamento Premium como exemplo neste documento.

Enquanto estamos abordam cenários de desempenho para a camada de armazenamento Olá neste artigo, você precisará de camada de aplicativo hello toooptimize. Por exemplo, se você estiver hospedando um Farm do SharePoint no armazenamento do Azure Premium, você pode usar exemplos do SQL Server Olá deste servidor de banco de dados do artigo toooptimize hello. Além disso, otimize o servidor de Web do Farm do SharePoint hello e saudação do aplicativo servidor tooget a maioria dos desempenho.

Este artigo ajudará a responder às perguntas comuns a seguir sobre como otimizar o desempenho de aplicativos no Armazenamento Premium do Azure.

* Como toomeasure o desempenho do aplicativo?  
* Por que você não está vendo o alto desempenho esperado?  
* Quais fatores influenciam o desempenho do aplicativo no Armazenamento Premium?  
* Como esses fatores influenciam o desempenho do aplicativo no Armazenamento Premium?  
* Como você pode otimizar para IOPS, Largura de Banda e Latência?  

Fornecemos estas diretrizes especificamente para Armazenamento Premium porque as cargas de trabalho em execução no Armazenamento Premium são altamente sensíveis ao desempenho. Fornecemos exemplos onde apropriado. Você também pode aplicar alguns desses tooapplications diretrizes em execução em VMs de IaaS com discos de armazenamento padrão.

Antes de começar, se você estiver tooPremium novo armazenamento, leia primeiro Olá [armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho de máquina Virtual do Azure](storage-premium-storage.md) e [escalabilidade do armazenamento do Azure e metas de desempenho](storage-scalability-targets.md)artigos.

## <a name="application-performance-indicators"></a>Indicadores de desempenho de aplicativo
Podemos avaliar se um aplicativo está executando o bem ou não usar como indicadores de desempenho, rapidez um aplicativo está processando uma solicitação de usuário, a quantidade de dados está processando um aplicativo por solicitação, quantas solicitações é um aplicativo de processamento em uma determinada período de tempo, quanto tempo que um usuário tiver uma resposta toowait tooget depois de enviar a solicitação. termos de saudação técnico para esses indicadores de desempenho são IOPS, taxa de transferência ou largura de banda e latência.

Nesta seção, discutiremos indicadores de desempenho comuns Olá no contexto de saudação do armazenamento Premium. Olá a seção seguinte, reunir os requisitos de aplicativo, você aprenderá como toomeasure esses indicadores de desempenho para o seu aplicativo. Mais tarde otimizando o desempenho do aplicativo, você aprenderá sobre fatores de saudação que afetam essas toooptimize de indicadores e recomendações de desempenho-los.

## <a name="iops"></a>IOPS
IOPS é o número de solicitações que seu aplicativo está enviando toohello discos de armazenamento em um segundo. Uma operação de entrada/saída pode ser de leitura ou gravação, sequencial ou aleatória. Aplicativos OLTP como um site de varejo online precisam tooprocess muitos usuários simultâneos solicitações imediatamente. Olá solicitações do usuário são inserir e atualizar transações de banco de dados de uso intensivo, o aplicativo hello deve processar rapidamente. Desse modo, os aplicativos OLTP exigem IOPS bastante alta. Tais aplicativos tratam milhões de solicitações de E/S aleatórias e pequenas. Se você tiver um aplicativo desse tipo, você deve projetar Olá toooptimize de infraestrutura de aplicativo para o IOPS. Em Olá seção mais tarde, *otimizando o desempenho do aplicativo*, discutiremos detalhadamente todos os fatores de saudação que você deve considerar tooget IOPS alta.

Quando você anexa uma premium armazenamento em disco tooyour alta escala de VM, provisões do Azure para você um número garantido de IOPS de acordo com a especificação de disco hello. Por exemplo, um disco P50 provisiona 7500 IOPS. Cada tamanho de VM de alta escala também tem um limite específico de IOPS que ela pode manter. Por exemplo, uma VM GS5 Padrão tem um limite de 80.000 IOPS.

## <a name="throughput"></a>Taxa de transferência
Taxa de transferência ou largura de banda é a quantidade de saudação de dados que seu aplicativo está enviando toohello discos de armazenamento em um intervalo especificado. Se o aplicativo estiver executando operações de entrada/saída com tamanhos grandes de unidade de E/S, ele exigirá Taxa de Transferência alta. Aplicativos de data warehouse tendem tooissue verificação operações intensivas que acessam grandes porções de dados por vez e geralmente executam operações em massa. Em outras palavras, tais aplicativos exigem Taxa de Transferência mais alta. Se você tiver um aplicativo desse tipo, você deve projetar sua infra-estrutura toooptimize para taxa de transferência. Na próxima seção, Olá, discutiremos nos fatores de saudação de detalhes deve ajustar tooachieve isso.

Quando você anexa uma premium armazenamento em disco tooa alta escala de VM do Azure provisiona taxa de transferência de acordo com a especificação desse disco. Por exemplo, um disco P50 provisiona Taxa de Transferência de disco de 250 MB por segundo. Cada tamanho de VM de alta escala também tem um limite específico de Taxa de Transferência que ela pode manter. Por exemplo, a VM GS5 padrão tem uma Taxa de Transferência máxima de 2.000 MB por segundo. 

Há uma relação entre a taxa de transferência e IOPS, conforme mostrado na fórmula de saudação abaixo.

![](media/storage-premium-storage-performance/image1.png)

Portanto, é importante toodetermine Olá taxa de transferência e IOPS valores ideais que seu aplicativo requer. Como você tentar toooptimize um, Olá outros também obtém afetado. Em uma seção mais adiante, *Otimizando o desempenho do aplicativo*, abordaremos em mais detalhes como otimizar a IOPS e Taxa de Transferência.

## <a name="latency"></a>Latência
Latência é Olá tempo que leva a um aplicativo tooreceive uma única solicitação, enviá-la em discos de armazenamento toohello e enviar Olá resposta toohello cliente. Esta é uma medida crítica de desempenho de um aplicativo em adição tooIOPS e taxa de transferência. Olá latência de um disco de armazenamento premium é tempo de saudação necessário tooretrieve Olá informações de uma solicitação e se comunicar aplicativo tooyour-o novamente. O Armazenamento Premium fornece baixas latências consistentes. Ao habilitar o cache do host ReadOnly nos discos do Armazenamento Premium, você obtém latência de leitura mais baixa. Abordaremos o Cache de Disco em mais detalhes na seção *Otimizando o desempenho do aplicativo*.

Ao otimizar seu aplicativo tooget superior IOPS e taxa de transferência, isso afetará Olá latência do seu aplicativo. Depois de ajustar o desempenho do aplicativo hello, sempre retornam Olá latência de saudação aplicativo tooavoid comportamento inesperado de alta latência.

## <a name="gather-application-performance-requirements"></a>Entender os requisitos de desempenho do aplicativo
Olá primeira etapa na criação de aplicativos de alto desempenho em execução no armazenamento do Azure Premium é, requisitos de desempenho de saudação toounderstand do seu aplicativo. Depois de reunir os requisitos de desempenho, você pode otimizar o desempenho ideal do aplicativo tooachieve hello.

Na seção anterior do hello, explicamos Olá comuns indicadores de desempenho, IOPS, taxa de transferência e latência. Você deve identificar qual esses indicadores de desempenho são a experiência do usuário do tooyour crítico aplicativo toodeliver Olá desejado. Por exemplo, um IOPS alto importa a maioria dos aplicativos de tooOLTP processar milhões de transações em um segundo. Já a Taxa de Transferência alta é essencial para aplicativos de data warehouse que processam grandes volumes de dados em um segundo. A Latência extremamente baixa é essencial para aplicativos em tempo real, como sites de streaming de vídeo ao vivo.

Em seguida, avaliar requisitos de desempenho máximo de saudação do seu aplicativo durante seu tempo de vida. Use a lista de verificação de exemplo de hello abaixo como uma inicialização. Requisitos de desempenho máximo do registro Olá durante normal, períodos de carga de trabalho de pico e fora do horário comercial. Identificando os requisitos para todos os níveis de cargas de trabalho, você será capaz de toodetermine Olá requisito geral de desempenho do seu aplicativo. Por exemplo, a carga de trabalho normal de um site de comércio eletrônico hello serão transações de saudação serve durante a maioria dos dias em um ano. carga de trabalho de pico de Olá do site Olá será transações Olá serve durante a temporada ou eventos de venda especial. carga de trabalho de pico de saudação é normalmente experiente por um período limitado, mas pode exigir tooscale seu aplicativo duas ou mais vezes sua operação normal. Descubra 99 requisitos de percentil, 90 percentil e percentual de 50 hello. Isso ajuda a filtrar quaisquer exceções em requisitos de desempenho de saudação e você possa concentrar seus esforços em otimizar para valores de saudação à direita.

**Lista de verificação dos requisitos de desempenho do aplicativo**

| **Requisitos de desempenho** | **Percentil 50** | **Percentil 90** | **Percentil 99** |
| --- | --- | --- | --- |
| Máx. Transações por segundo | | | |
| % de operações de Leitura | | | |
| % de operações de Gravação | | | |
| % de operações Aleatórias | | | |
| % de operações Sequenciais | | | |
| Tamanho da solicitação de E/S | | | |
| Taxa de transferência média | | | |
| Máx. Taxa de transferência | | | |
| Mín. Latência | | | |
| Latência Média | | | |
| Máx. CPU | | | |
| CPU Média | | | |
| Máx. Memória | | | |
| Memória Média | | | |
| Profundidade da Fila | | | |

> [!NOTE]
> você deve considerar o dimensionamento desses números com base no futuro crescimento esperado do aplicativo. É tooplan uma boa ideia para crescimento antecipadamente, pois pode ser mais difícil infra-estrutura de saudação toochange para melhorar o desempenho mais tarde.
>
>

Se você tiver um aplicativo existente e quiser toomove tooPremium armazenamento, primeiro crie a lista de verificação do hello acima para o aplicativo hello. Em seguida, crie um protótipo do seu aplicativo no armazenamento Premium e o design de aplicativo hello com base nas diretrizes descritas em *otimizando o desempenho do aplicativo* em uma seção posterior deste documento. Olá próxima seção descreve ferramentas Olá você pode usar medidas de desempenho toogather hello.

Crie um lista de verificação semelhante tooyour aplicativo existente para o protótipo de saudação. Usando as ferramentas de Benchmarking pode simular cargas de trabalho hello e medir o desempenho do aplicativo de protótipo hello. Consulte a seção de saudação em [Benchmarking](#benchmarking) toolearn mais. Com isso, você pode determinar se o Armazenamento Premium pode corresponder ou superar os requisitos de desempenho do aplicativo. Em seguida, você pode implementar Olá mesmas diretrizes para seu aplicativo de produção.

### <a name="counters-toomeasure-application-performance-requirements"></a>Contadores de toomeasure requisitos de desempenho de aplicativo
Olá melhor toomeasure requisitos de desempenho de maneira do seu aplicativo, é toouse ferramentas de monitoramento de desempenho fornecidas pelo sistema operacional de saudação do servidor de saudação. Você pode usar o PerfMon para Windows e iostat para Linux. Essas ferramentas capturam contadores medida tooeach correspondente é explicada em Olá acima de seção. Você deve capturar os valores desses contadores hello quando seu aplicativo está executando seu normal, cargas de trabalho de pico e fora do horário comercial.

contadores de desempenho de saudação estão disponíveis para o processador, memória e, em cada disco lógico e o disco físico do seu servidor. Quando você usar discos de armazenamento premium com uma VM, contadores de disco físico Olá são para cada disco de armazenamento premium, e os contadores de disco lógico são para cada volume criado nos discos de armazenamento premium Olá. Você deve capturar os valores hello discos Olá sua carga de trabalho do aplicativo de host. Se houver um mapeamento de tooone um entre discos lógicos e físicos, você pode consultar os contadores de disco toophysical; Caso contrário, consulte toohello contadores de disco lógico. No Linux, o comando de iostat Olá gera um relatório de utilização de CPU e disco. relatório de utilização de disco Olá fornece estatísticas por partição ou o dispositivo físico. Se você tiver um servidor de banco de dados com seus dados e registrados em discos separados, colete esses dados de ambos os discos. A tabela abaixo descreve contadores de discos, processador e memória:

| Contador | Descrição | PerfMon | Iostat |
| --- | --- | --- | --- |
| **IOPS ou Transações por segundo** |Número de solicitações de e/s emitida toohello de disco de armazenamento por segundo. |Leituras de Disco/s  <br> Gravações de Disco/s |tps  <br> r/s  <br> w/s |
| **Leituras e gravações de discos** |% de leituras de operações realizadas no disco de saudação e gravação. |% de Tempo de Leitura de Disco  <br> % de Tempo de Gravação de Disco |r/s  <br> w/s |
| **Taxa de transferência** |Quantidade de dados lida ou gravada toohello de disco por segundo. |Bytes Lidos no Disco/s  <br> Bytes Gravados no Disco/s |kB_read/s <br> kB_wrtn/s |
| **Latência** |Total de tempo toocomplete uma solicitação de e/s de disco. |Média por Segundo do Disco/Leitura  <br> Média por segundo do disco/Gravação |await  <br> svctm |
| **Tamanho de E/S** |tamanho de saudação de solicitações de e/s emite toohello discos de armazenamento. |Média de Bytes do Disco/Leitura  <br> Média de Bytes do Disco/Gravação |avgrq-sz |
| **Profundidade da Fila** |Número de e/s pendentes solicitações toobe espera ler formulário ou gravados em disco de armazenamento toohello. |Comprimento da Fila do Disco Atual |avgqu-sz |
| **IOPS Máxima** |Quantidade de memória exigida toorun aplicativo sem problemas |% de Bytes Confirmados em Uso |Usar o vmstat |
| **IOPS Máxima** |Quantidade de CPU necessário toorun aplicativo sem problemas |% do Tempo do Processador |%util |

Saiba mais sobre o [iostat](http://linuxcommand.org/man_pages/iostat1.html) e [PerfMon](https://msdn.microsoft.com/library/aa645516.aspx).

## <a name="optimizing-application-performance"></a>Otimizando o desempenho do aplicativo
Olá principais fatores que influenciam o desempenho de um aplicativo em execução no armazenamento Premium são natureza de e/s solicitações, tamanho da VM, o tamanho do disco, o número de discos, Multithreading, cache de disco e a profundidade da fila. Você pode controlar alguns desses fatores com botões fornecidos pelo sistema de saudação. A maioria dos aplicativos podem não oferecer Olá de tooalter uma opção de e/s e a profundidade de fila diretamente. Por exemplo, se você estiver usando o SQL Server, você não pode escolher a profundidade de fila e tamanho de e/s hello. SQL Server escolhe Olá ideal i / o tamanho e a fila de profundidade valores tooget Olá maioria do desempenho. É importante toounderstand os efeitos de saudação de ambos os tipos de fatores no desempenho do aplicativo, para que você pode provisionar os recursos adequados às necessidades de desempenho de toomeet.

Ao longo desta seção, consulte toohello aplicativo requisitos lista de verificação que você criou, tooidentify quanto precisar toooptimize o desempenho do aplicativo. Com base no que, você será capaz de toodetermine quais fatores desta seção que você precisará tootune. toowitness Olá efeitos de cada fator no desempenho do seu aplicativo, executar análise comparativa ferramentas na sua configuração de aplicativo. Consulte toohello [Benchmarking](#Benchmarking) seção Olá final deste artigo para etapas toorun comuns benchmark ferramentas no Windows e VMs do Linux.

### <a name="optimizing-iops-throughput-and-latency-at-a-glance"></a>Otimizando a IOPS, a Taxa de Transferência e a latência em segundos
Olá tabela a seguir resume todos os fatores de desempenho hello e Olá etapas toooptimize IOPS, taxa de transferência e latência. Olá seções seguintes esse resumo descreve cada fator é muito mais profundidade.

| &nbsp; | **IOPS** | **Taxa de transferência** | **Latência** |
| --- | --- | --- | --- |
| **Cenário de exemplo** |Aplicativo OLTP corporativo que exige taxa muito alta de transações por segundo. |Aplicativo de data warehouse corporativo que processa grandes volumes de dados. |Próximo a aplicativos em tempo real que exigem a solicitações de toouser respostas instantâneas, como jogos online. |
| Fatores de desempenho | &nbsp; | &nbsp; | &nbsp; |
| **Tamanho de E/S** |E/S menores geram IOPS mais altas. |Tooyields de tamanho de e/s maior taxa de transferência mais alta. | &nbsp;|
| **Tamanho da VM** |Use um tamanho de VM que ofereça IOPS maior que o requisito do seu aplicativo. Veja os tamanhos de VM e respectivos limites de IOPS aqui. |Use um tamanho de VM com limite de Taxa de Transferência maior que o requisito do seu aplicativo. Veja os tamanhos de VM e respectivos limites de Taxa de Transferência aqui. |Use um tamanho de VM que ofereça limites de escala maiores que o requisito do seu aplicativo. Veja os tamanhos de VM e os respectivos limites aqui. |
| **Tamanho do disco** |Use um tamanho de disco que ofereça IOPS maior que o requisito de seu aplicativo. Veja os tamanhos de disco e respectivos limites de IOPS aqui. |Use um tamanho de disco com limite de Taxa de Transferência maior que o requisito do seu aplicativo. Veja os tamanhos de disco e respectivos limites de Taxa de Transferência aqui. |Use um tamanho de disco que ofereça limites de escala maiores que o requisito do seu aplicativo. Veja os tamanhos de disco e respectivos limites aqui. |
| **Limites de escala de VM e disco** |Limite de IOPS de escolhida de tamanho VM Olá deve ser maior que o IOPS total orientada por discos de armazenamento premium anexado tooit. |Limite de taxa de transferência de escolhida de tamanho VM Olá deve ser maior que a taxa de transferência total é orientada por discos de armazenamento premium anexado tooit. |Limites de escala de escolhida de tamanho VM Olá devem ser maiores que os limites de escala total de discos de armazenamento premium anexado. |
| **Cache de disco** |Habilite o Cache de somente leitura em discos de armazenamento premium com tooget de operações pesadas de leitura superior IOPS de leitura. | &nbsp; |Habilite o Cache de somente leitura em discos de armazenamento premium com latências de leitura pronto operações pesadas tooget muito baixas. |
| **Distribuição de disco** |Use vários discos e distribua-los junto tooget um combinado de IOPS superior e o limite de taxa de transferência. Observe que Olá combinado limite por VM deve ser maior do que o hello limites combinados de discos anexados premium. | &nbsp; | &nbsp; |
| **Tamanho da distribuição** |Tamanho menor de distribuição para padrão pequeno de E/S aleatório visto em aplicativos OLTP. Por exemplo, use o tamanho de distribuição de 64 KB para aplicativo OLTP do SQL Server. |Tamanho maior de distribuição para padrão grande de E/S sequencial visto em aplicativos de data warehouse. Por exemplo, use o tamanho de distribuição de 256 KB para aplicativo de data warehouse do SQL Server. | &nbsp; |
| **Multithreading** |Use multithreading toopush um maior número de solicitações tooPremium armazenamento que levará toohigher IOPS e taxa de transferência. Por exemplo, no SQL Server definir uma alta tooallocate de valor MAXDOP mais CPUs tooSQL Server. | &nbsp; | &nbsp; |
| **Profundidade da Fila** |Profundidade da fila maior gera IOPS mais alta. |Uma Profundidade da Fila maior gera uma Taxa de Transferência mais alta. |Profundidade da fila menor gera latências mais baixas. |

## <a name="nature-of-io-requests"></a>Natureza das solicitações de E/S
Uma solicitação de E/S é uma unidade da operação de entrada/saída que seu aplicativo executará. Identificar a natureza da saudação de solicitações de e/s aleatórias ou sequenciais, leitura ou gravação, pequena ou grande, o ajudará a determinar os requisitos de desempenho de saudação do seu aplicativo. É muito importante toounderstand natureza de saudação de solicitações de e/s, toomake Olá as decisões certas durante a criação de sua infraestrutura de aplicativo.

Tamanho de e/s é uma saudação fatores mais importantes. saudação de e/s é o tamanho de saudação da solicitação de operação de entrada/saída Olá gerado pelo seu aplicativo. saudação de e/s tem um impacto significativo no desempenho, especialmente em Olá IOPS e largura de banda Olá aplicativo é capaz de tooachieve. Olá, fórmula a seguir mostra a relação Olá entre IOPS, tamanho de e/s e largura de banda/taxa de transferência.  
    ![](media/storage-premium-storage-performance/image1.png)

Alguns aplicativos permitem tooalter suas e/s de tamanho, enquanto alguns aplicativos não. Por exemplo, SQL Server determina o tamanho e/s ideal Olá em si e não fornecer aos usuários qualquer toochange botões-lo. Em Olá outro lado, a Oracle fornece um parâmetro chamado [DB\_bloquear\_tamanho](https://docs.oracle.com/cd/B19306_01/server.102/b14211/iodesign.htm#i28815) com o qual você pode configurar Olá tamanho da solicitação de e/s de banco de dados de saudação.

Se você estiver usando um aplicativo, que não permite que você toochange Olá de e/s, use as diretrizes de saudação neste artigo toooptimize Olá KPI de desempenho com aplicativo tooyour mais relevantes. Por exemplo,

* Um aplicativo OLTP gera milhões de solicitações de E/S pequenas e aleatórias. solicitações de toohandle esses tipo de e/s, você deve projetar seu tooget de infraestrutura de aplicativo mais IOPS.  
* Um aplicativo de data warehouse gera solicitações de E/S grandes e sequenciais. toohandle esses tipo de solicitações de e/s, você deve projetar seu tooget de infraestrutura do aplicativo maior largura de banda ou de taxa de transferência.

Se você estiver usando um aplicativo, o que permite o tamanho de e/s de saudação toochange, use esta regra geral para hello e/s de tamanho além tooother diretrizes de desempenho,

* Menor tooget de tamanho de e/s IOPS superior. Por exemplo, 8 KB para um aplicativo OLTP.  
* Tooget de tamanho de e/s maior largura de banda/taxa de transferência mais alta. Por exemplo, 1024 KB para um aplicativo de data warehouse.

Aqui está um exemplo sobre como você pode calcular hello IOPS e largura de banda/taxa de transferência para o seu aplicativo. Considere um aplicativo usando um disco P30. Olá IOPS máximo e taxa de transferência/largura de banda pode obter um disco de P30 é 5.000 IOPS e 200 MB por segundo respectivamente. Agora, se seu aplicativo exigir Olá que IOPS máximo do disco Olá P30 e você usar um tamanho menor de e/s como 8 KB, hello resultante da largura de banda será capaz de tooget é 40 MB por segundo. No entanto, se seu aplicativo exigir Olá taxa de transferência/largura de banda máxima de disco P30 e você usar um tamanho maior de e/s como 1024 KB, hello IOPS resultante será menor, 200 IOPS. Portanto, ajuste o tamanho de e/s de hello, de modo que ele atende aos requisitos de IOPS e largura de banda/taxa de transferência de ambos do seu aplicativo. Tabela a seguir resume os tamanhos diferentes de e/s hello e suas IOPS e taxa de transferência para um disco P30.

| Requisito de aplicativo | Tamanho de E/S | IOPS | Taxa de Transferência/Largura de Banda |
| --- | --- | --- | --- |
| IOPS Máxima |8 KB |5.000 |40 MB por segundo |
| Taxa de Transferência Máxima |1024 KB |200 |200 MB por segundo |
| Taxa de Transferência Máxima + IOPS alta |64 KB |3.200 |200 MB por segundo |
| IOPS máxima + Taxa de Transferência alta |32 KB |5.000 |160 MB por segundo |

tooget IOPS e largura de banda maior do que o valor máximo de saudação de um disco de armazenamento premium única, use vários discos de premium distribuídos juntos. Por exemplo, distribua dois tooget de discos P30 um IOPS combinado de IOPS de 10.000 ou uma taxa de transferência combinada de 400 MB por segundo. Conforme explicado na próxima seção, Olá, você deve usar um tamanho VM que oferece suporte a saudação combinada IOPS de disco e taxa de transferência.

> [!NOTE]
> Como aumentar o IOPS ou saudação de taxa de transferência outros também aumenta, verifique se que você não clicar em taxa de transferência ou limites IOPS de disco de saudação ou VM quando aumentar um.
>
>

toowitness Olá efeitos de tamanho de e/s no desempenho do aplicativo, você pode executar ferramentas de avaliação no VM e discos. Criar várias execuções de teste e usar o tamanho diferente de e/s para cada impacto de saudação toosee de execução. Consulte toohello [Benchmarking](#Benchmarking) seção Olá final deste artigo para obter mais detalhes.

## <a name="high-scale-vm-sizes"></a>Tamanhos de VM de alta escala
Quando você começar a criar um aplicativo, uma saudação primeiro coisas toodo é, escolha uma VM toohost seu aplicativo. O Armazenamento Premium surge com os tamanhos de VM de alta escala que podem executar aplicativos que exigem potência mais alta de computação e um alto desempenho de E/S do disco local. Essas VMs fornecem processadores mais rápidos, uma maior taxa de memória por núcleo e um Solid-State unidade (SSD) para o disco local hello. Exemplos de alta VMs de escala, dando suporte a armazenamento Premium são Olá DS, série DSv2 e GS VMs da série.

As VMs de alta escala estão disponíveis em diferentes tamanhos com diferentes números de núcleos de CPU, memória, sistema operacional e tamanho de disco temporário. Cada tamanho VM também tem o número máximo de discos de dados que você pode anexar toohello VM. Portanto, o tamanho da VM Olá escolhido afetará quanta capacidade de processamento, memória e armazenamento está disponível para seu aplicativo. Isso também afeta hello computação e o custo de armazenamento. Por exemplo, abaixo estão as especificações de Olá Olá maior do tamanho da VM em uma série DS, série DSv2 série e uma série GS:

| Tamanho da VM | Núcleos de CPU | Memória | Tamanhos de disco da VM | Máx. de discos de dados | Tamanho do cache | IOPS | Limites de E/S do cache da largura de banda |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS14 |16 |112 GB |SO = 1023 GB  <br> SSD local = 224 GB |32 |576 GB |50.000 IOPS  <br> 512 MB por segundo |4.000 IOPS e 33 MB por segundo |
| Standard_GS5 |32 |448 GB |SO = 1023 GB  <br> SSD local = 896 GB |64 |4224 GB |80.000 IOPS  <br> 2.000 MB por segundo |5.000 IOPS e 50 MB por segundo |

tooview uma lista completa de todos os tamanhos de VM do Azure disponíveis, consulte muito[tamanhos de VM do Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [tamanhos de VM do Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Escolha um tamanho VM que pode atender e dimensionar os requisitos de desempenho de aplicativo tooyour desejado. Além disso toothis, leve em consideração a seguir considerações importantes ao escolher tamanhos de VM.

*Limites de Escala*  
Olá limites máximos de IOPS por VM e por disco são diferentes e independentes um do outro. Certifique-se de que o aplicativo hello está gerando IOPS dentro dos limites de saudação VM, bem como Olá premium discos anexados tooit hello. Caso contrário, o desempenho do aplicativo será limitado.

Por exemplo, suponha que o requisito de um aplicativo seja de 4.000 IOPS. tooachieve isso, você provisionar um disco P30 em uma VM DS1. disco de P30 Olá proporcionam até too5, IOPS, 000. No entanto, Olá VM DS1 é limitado too3, 200 IOPS. Consequentemente, o desempenho do aplicativo hello será limitado pelo limite VM Olá em 3.200 IOPS e haverá degradação do desempenho. tooprevent nessa situação, escolha uma máquina virtual e tamanho que ambos os requisitos do aplicativo atenda de disco.

*Custo da operação*  
Em muitos casos, é possível que o custo geral de operação usando o Armazenamento Premium seja menor do que usando o Armazenamento Padrão.

Por exemplo, considere um aplicativo que exija 16.000 IOPS. tooachieve esse desempenho, você precisará de um padrão\_D14 Azure IaaS VM, o que pode dar a um máximo de IOPS de 16.000 usando 32 discos de 1 TB de armazenamento padrão. Cada disco de armazenamento padrão de 1TB pode atingir um máximo de 500 IOPS. Olá estimativa de custo desta VM por mês será de US $1,570. custo mensal de saudação do 32 discos de armazenamento padrão será $1,638. Olá estimativa de custo mensal total será $3,208.

No entanto, se você hospedado Olá mesmo aplicativo no armazenamento Premium, será necessário um tamanho menor de VM e discos de armazenamento premium menos, reduzindo o custo geral de saudação. Um padrão\_DS13 VM pode atender aos requisitos de IOPS Olá 16.000 usando quatro discos P30. Olá DS13 VM tem um máximo de IOPS 25,600 e cada disco P30 tem um máximo de IOPS de 5.000. Em geral, essa configuração pode alcançar 5.000 x 4 = 20.000 IOPS. Olá estimativa de custo desta VM por mês será de US $1,003. custo mensal de saudação do quatro discos de armazenamento premium P30 será $544.34. Olá estimativa de custo mensal total será $1,544.

Tabela a seguir resume a divisão de custo Olá deste cenário para Standard e Premium armazenamento.

| &nbsp; | **Standard** | **Premium** |
| --- | --- | --- |
| **Custo de VM por mês** |US$ 1.570,58 (Standard\_D14) |US$ 1.003,66 (Standard\_DS13) |
| **Custo de discos por mês** |US$ 1.638,40 (32 discos x 1 TB) |US$ 544,34 (4 discos x P30) |
| **Custo geral por mês** |US$ 3.208,98 |US$ 1.544,34 |

*Distribuições do Linux*  

Com o armazenamento do Azure Premium, você obtém Olá mesmo nível de desempenho para as VMs que executam o Windows e Linux. Há suporte para vários tipos de distribuições de Linux, e você pode ver a lista completa de saudação [aqui](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). É importante toonote que diferentes distribuições são melhores adequado para diferentes tipos de cargas de trabalho. Você verá diferentes níveis de desempenho, dependendo da distribuição Olá que sua carga de trabalho está em execução no. Olá distribuições de Linux com o seu aplicativo de teste e escolha Olá que funciona melhor.

Quando executando o Linux com o armazenamento Premium, verifica se há atualizações mais recentes de saudação sobre drivers necessários tooensure de alto desempenho.

## <a name="premium-storage-disk-sizes"></a>Tamanhos de disco do Armazenamento Premium
Atualmente, o Armazenamento Premium do Azure oferece sete tamanhos de disco. Cada tamanho de disco tem um limite de escala diferente para IOPS, largura de banda e armazenamento. Escolha o tamanho correto de disco de armazenamento Premium Olá dependendo requisitos do aplicativo hello e escala de alta Olá tamanho da VM. tabela de Olá abaixo mostra os tamanhos de discos sete hello e seus recursos. Atualmente, os tamanhos de disco P4 e P6 têm suporte somente para o Managed Disks.

| Tipo de discos premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Tamanho do disco           | 32 GB | 64 GB | 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPS por disco       | 120   | 240   | 500   | 2.300              | 5.000              | 7500              | 7500              | 
| Taxa de transferência por disco | 25 MB por segundo  | 50 MB por segundo  | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo | 250 MB por segundo | 250 MB por segundo | 


Quantos discos que você escolher depende de disco Olá tamanho escolhido. Você pode usar um disco de P50 único ou vários toomeet de discos P10 seu requisito de aplicativo. Leve em considerações de conta listadas abaixo ao fazer a escolha de saudação.

*Limites de Escala (IOPS e Taxa de Transferência)*  
limites IOPS e taxa de transferência de saudação de cada tamanho de disco Premium é diferente e independente de limites de escala VM hello. Certifique-se de que Olá IOPS total e taxa de transferência de discos Olá estão dentro dos limites de escala de saudação escolhida tamanho da VM.

Por exemplo, se o requisito de um aplicativo for de, no máximo, 250 MB/s de Taxa de Transferência e você estiver usando uma VM DS4 com um único disco P30. Olá DS4 VM pode fornecer a taxa de transferência too256 MB/s. No entanto, um único disco P30 tem limite de taxa de transferência de 200 MB/s. Consequentemente, o aplicativo hello será limitado em 200 MB/s de vencimento toohello limite de disco. tooovercome esse limite, provisionar toohello de discos de dados mais de uma VM ou redimensionar seus discos tooP40 ou P50.

> [!NOTE]
> Leituras atendidas pelo cache de saudação não são incluídas no disco Olá IOPS e taxa de transferência, portanto, não sujeito toodisk limites. O cache tem seu limite de IOPS e Taxa de Transferência separado por VM.
>
> Por exemplo, inicialmente as leituras e gravações são de 60 MB/s e 40 MB/s, respectivamente. Ao longo do tempo, o cache de saudação aquecido e serve mais Olá leituras do cache de saudação. Em seguida, você pode obter gravação maior taxa de transferência do disco hello.
>
>

*Número de discos*  
Determine o número de saudação de discos, que você precisará avaliando requisitos do aplicativo. Cada tamanho VM também tem um limite no número de saudação de discos que você pode anexar toohello VM. Normalmente, isso é Olá dobro de núcleos. Certifique-se de que o tamanho de VM escolhido pode dar suporte Olá número de discos necessário hello.

Lembre-se de que os discos de armazenamento Premium Olá tem desempenho superior tooStandard recursos em comparação com discos de armazenamento. Portanto, se você estiver migrando seu aplicativo do Azure IaaS VM usando o armazenamento padrão tooPremium armazenamento, você provavelmente precisará menos discos premium tooachieve Olá desempenho igual ou superior para o seu aplicativo.

## <a name="disk-caching"></a>Cache de disco
As VMs de alta escala que aproveitam o Armazenamento Premium do Azure têm uma tecnologia de cache de várias camadas chamada BlobCache. BlobCache usa uma combinação de hello RAM de máquina Virtual e SSD local para armazenar em cache. Esse cache está disponível para discos persistentes de armazenamento Premium Olá e os discos locais de VM de saudação. Por padrão, essa configuração de cache é definida tooRead/gravação para discos do sistema operacional e ReadOnly para discos de dados hospedados no armazenamento Premium. Com o cache de disco habilitado em discos de armazenamento Premium Olá, escala de alta Olá VMs pode obter extremamente altos níveis de desempenho que excedem o desempenho do disco subjacente hello.

> [!WARNING]
> Alterando a configuração de cache de saudação de um disco do Azure desanexa e anexa novamente o disco de destino hello. Se o disco de sistema operacional Olá, Olá VM for reiniciado. Pare todos os aplicativos/serviços que podem ser afetados por essa interrupção antes de alterar a configuração de cache de disco de saudação.
>
>

toolearn mais informações sobre como BlobCache funciona, consulte toohello dentro de [armazenamento Premium do Azure](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/) postagem de blog.

É importante tooenable cache em Olá certo conjunto de discos. Você deve habilitar o cache de disco em um disco premium ou não dependem padrão de carga de trabalho Olá desse disco será manipula. Tabela a seguir mostra o padrão de saudação configurações de cache para o sistema operacional e discos de dados.

| **Tipo de disco** | **Configuração padrão de cache** |
| --- | --- |
| Disco do sistema operacional |ReadWrite |
| Disco de dados |Nenhum |

A seguir são Olá configurações de cache em disco recomendado para discos de dados

| **Configuração do cache de disco** | **Recomendação sobre quando toouse essa configuração** |
| --- | --- |
| Nenhum |Configure o cache do host como None para discos de gravação pesada e somente gravação. |
| ReadOnly |Configure o cache do host como ReadOnly para discos de leitura/gravação e somente leitura. |
| ReadWrite |Configure o cache de host como ReadWrite somente se o seu aplicativo lida corretamente com gravação em cache os discos de dados toopersistent quando necessário. |

*ReadOnly*  
Ao configurar o cache ReadOnly em discos de dados do Armazenamento Premium, você pode obter baixa latência de leitura e IOPS de leitura e Taxa de Transferência muito altas para seu aplicativo. Isso se deve a dois motivos:

1. Leituras executadas do cache, que está na memória da VM hello e SSD local, são muito mais rápidas do que as leituras de disco de dados hello, que está no hello armazenamento de BLOBs do Azure.  
2. Armazenamento Premium não conta Olá leituras servidas do cache, em direção de IOPS de disco hello e taxa de transferência. Portanto, o aplicativo é capaz de tooachieve superior total de IOPS e taxa de transferência.

*ReadWrite*  
Por padrão, os discos de SO Olá têm ReadWrite cache habilitado. Recentemente, adicionamos suporte ao cache ReadWrite também nos discos de dados. Se você estiver usando o armazenamento em cache ReadWrite, você deve ter um modo adequado toowrite Olá os dados de discos de toopersistent de cache. Por exemplo, gravação de identificadores SQL Server armazenados em cache discos de armazenamento persistente toohello dados por conta própria. Usando o cache de ReadWrite com um aplicativo que não processa Olá persistente necessário dados podem levar a perda de toodata se Olá VM falhar.

Por exemplo, você pode aplicar essas diretrizes tooSQL Server em execução no armazenamento Premium Olá seguinte,

1. Configure o cache "ReadOnly" em discos do Armazenamento Premium que hospedam arquivos de dados.  
   a.  Olá rápida lê do tempo de consulta do cache inferior saudação do SQL Server como páginas de dados são recuperadas muito mais rápido do hello cache comparado toodirectly de discos de dados de saudação.  
   b.  Atender às leituras no cache, significa que há Taxa de Transferência adicional disponível nos discos de dados premium. O SQL Server pode usar essa Taxa de Transferência adicional para recuperar mais páginas de dados e outras operações, como backup/restauração, cargas em lote e recriações de índice.  
2. Configurar "None" cache em armazenamento premium discos hospedagem Olá os arquivos de log.  
   a.  Os arquivos de log têm basicamente operações pesadas de gravação. Portanto, eles não se beneficiam da saudação cache somente leitura.

## <a name="disk-striping"></a>Distribuição de disco
Quando uma alta escala que VM é anexada com vários premium armazenamento persistente discos, Olá pode ser juntos distribuídos tooaggregate seus IOPs, a largura de banda e a capacidade de armazenamento.

No Windows, você pode usar discos de toostripe de espaços de armazenamento em conjunto. É preciso configurar uma coluna para cada disco em um pool. Caso contrário, hello desempenho geral do volume distribuído pode ser menor que o esperado, devido a toouneven distribuição do tráfego entre os discos de saudação.

Importante: Usando o Gerenciador do servidor UI, você pode definir o número total de saudação de colunas de too8 para um volume distribuído. Ao anexar mais de 8 discos, use o volume de saudação do PowerShell toocreate. Usando o PowerShell, você pode definir Olá número de colunas iguais toohello número de discos. Por exemplo, se houver 16 discos em um conjunto único de distribuição; especificar 16 colunas em Olá *NumberOfColumns* parâmetro hello *New-VirtualDisk* cmdlet do PowerShell.

No Linux, use discos de toostripe Olá MDADM utilitário juntos. Para obter etapas detalhadas sobre discos de distribuição no Linux, consulte muito[configurar RAID de Software no Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

*Tamanho da distribuição*  
Uma configuração importante na distribuição de disco é o tamanho do stripe hello. tamanho da faixa Hello ou tamanho de bloco é parte de menor Olá de dados que o aplicativo pode resolver em um volume distribuído. você configurar o tamanho do stripe Olá depende do tipo de saudação do aplicativo e o padrão de solicitação. Se você escolher o tamanho do stripe errado hello, isso pode levar desalinhamento tooIO, o que aumenta o desempenho toodegraded de seu aplicativo.

Por exemplo, se uma solicitação de e/s gerada pelo seu aplicativo é maior do que o tamanho de distribuição de disco hello, sistema de armazenamento Olá grava em faixa limites de unidade em mais de um disco. Quando ele é tempo tooaccess dados, ele terá tooseek em mais de uma distribuição unidades toocomplete Olá solicitação. efeito cumulativo de saudação de tal comportamento pode levar toosubstantial degradação do desempenho. Em Olá outro lado, se Olá tamanho da solicitação de e/s é menor do que o tamanho de distribuição e, se for aleatória, solicitações de e/s de saudação podem adiciona Olá mesmo disco provocando um afunilamento e, por fim, comprometer o desempenho de e/s de saudação.

Dependendo do tipo de saudação da carga de seu aplicativo estiver em execução, escolha um tamanho de distribuição apropriados. Para solicitações pequenas e aleatórias de E/S, use um tamanho de distribuição menor. Já para solicitações de E/S grandes e sequenciais, use um tamanho de distribuição maior. Descubra Olá stripe recomendações de tamanho para o aplicativo hello que serão executados em armazenamento Premium. Para SQL Server, configure o tamanho da distribuição de 64 KB para cargas de trabalho OLTP e 256 KB para cargas de trabalho de data warehouse. Consulte [práticas recomendadas de desempenho do SQL Server em máquinas virtuais do Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md#disks-guidance) toolearn mais.

> [!NOTE]
> você pode usar a distribuição com um máximo de 32 discos do armazenamento premium em uma VM série DS e 64 discos do armazenamento premium em uma VM série GS.
>
>

## <a name="multi-threading"></a>Multithreading
Azure projetou toobe de plataforma de armazenamento Premium paralela em grande escala. Portanto, um aplicativo com multithread atinge desempenho muito mais alto que um aplicativo de único thread. Um aplicativo multithread divide o suas tarefas entre vários threads e aumenta a eficiência de sua execução por Olá utilizando VM e toohello de recursos de disco máximo.

Por exemplo, se seu aplicativo estiver em execução em um único núcleo VM usando dois threads, Olá CPU pode alternar entre a eficiência de tooachieve dois threads hello. Enquanto um thread está aguardando um toocomplete de e/s de disco, a saudação da CPU pode alternar toohello outro thread. Dessa forma, dois threads podem fazer mais do que um único thread. Se Olá VM tem mais de um núcleo, ele diminui ainda mais tempo de execução desde que cada principal pode executar tarefas em paralelo.

Forma de saudação toochange capaz de um aplicativo comercial implementa único pode não ser threading ou vários threads. Por exemplo, o SQL Server é capaz de lidar com várias CPUs e vários núcleos. No entanto, o SQL Server decide sob que condições, ele utilizará um ou mais threads tooprocess uma consulta. Ele pode executar consultas e criar índices usando multithreading. Para uma consulta que envolve a junção de tabelas grandes e classificando dados antes de retornar o usuário toohello, SQL Server provavelmente usará vários threads. No entanto, um usuário não pode controlar se o SQL Server executará uma consulta usando um único thread ou vários threads.

Há configurações que você pode alterar tooinfluence nesse multi-thread ou paralela de processamento de um aplicativo. Por exemplo, no caso do SQL Server é configuração de grau de paralelismo máximo hello. Essa configuração chamada MAXDOP, permite que você número máximo de saudação de tooconfigure de processadores do SQL Server pode usar ao processamento paralelo. É possível configurar MAXDOP para consultas individuais ou operações de índice. Isso é útil quando você deseja toobalance recursos do sistema para um aplicativo crítico de desempenho.

Por exemplo, digamos que seu aplicativo usando o SQL Server está executando uma consulta grande e uma operação de índice no hello simultaneamente. Vamos supor que você desejava Olá toobe de operação de índice mais consultas grandes toohello de alto desempenho em comparação com. Nesse caso, você pode definir o valor MAXDOP de Olá maior Olá valor MAXDOP para consulta de saudação de toobe de operação de índice. Dessa forma, o SQL Server tem mais de número de processadores que ele pode aproveitar para Olá índice operação comparado toohello número de processadores podem dedicar consulta grande toohello. Lembre-se de que você não controlar o número de saudação de threads do SQL Server usará para cada operação. Você pode controlar o número máximo de saudação de processadores sendo dedicada para multithreading.

Saiba mais sobre [Graus de Paralelismo](https://technet.microsoft.com/library/ms188611.aspx) no SQL Server. Descobrir essas configurações influenciam multithreading em seu aplicativo e o desempenho de toooptimize suas configurações.

## <a name="queue-depth"></a>Profundidade da Fila
Olá profundidade da fila ou o comprimento da fila ou o tamanho da fila é o número de saudação de solicitações de e/s pendentes no sistema de saudação. valor de saudação da profundidade da fila determina quantas operações e/s seu aplicativo pode preparar os discos de armazenamento Olá processará. Ela afeta todas as Olá três aplicativos indicadores de desempenho que abordamos na viz. neste artigo, IOPS, taxa de transferência e latência.

A profundidade da fila e o multithreading estão intimamente relacionados. Olá valor profundidade da fila indica quanto multi-thread pode ser obtida com o aplicativo hello. Se a profundidade da fila de saudação for grande, aplicativo pode executar operações mais simultaneamente, em outras palavras, mais multithreading. Se Olá profundidade da fila é pequeno, mesmo que o aplicativo é multi-threaded, ele não terá suficiente solicitações programadas para execução simultânea.

Normalmente, desativar Olá prateleira aplicativos não permitem que você toochange a profundidade da fila hello, porque se definida incorretamente, ele fará mais mal do que bem. Aplicativos definirá o valor à direita de saudação do desempenho ideal da fila de profundidade tooget hello. No entanto, ele é importante toounderstand esse conceito para que você pode solucionar problemas de desempenho com o seu aplicativo. Você também pode observar efeitos de saudação da profundidade da fila executando as ferramentas de avaliação em seu sistema.

Alguns aplicativos fornecem configurações tooinfluence Olá profundidade da fila. Por exemplo, a configuração de MAXDOP (grau máximo de paralelismo) saudação no SQL Server explicado na seção anterior. MAXDOP é uma maneira tooinfluence a profundidade da fila e multithreading, embora ele não alterar valor de profundidade da fila de saudação do SQL Server diretamente.

*Profundidade Alta de Fila*  
Uma profundidade de fila alta linhas mais operações no disco hello. disco Olá sabe a próxima solicitação Olá em sua fila antecipadamente. Consequentemente, disco Olá pode agendar operações antecipadamente e processá-los em uma sequência ideal. Desde que o aplicativo hello está enviando o disco de toohello mais solicitações, disco Olá pode processar mais IOs paralelos. Por fim, o aplicativo hello serão tooachieve capaz de IOPS superior. Desde que o aplicativo é processar mais solicitações, hello taxa de transferência total do aplicativo hello também aumenta.

Normalmente, um aplicativo pode atingir a taxa máxima de transferência com 8 a pouco mais de 16 E/S pendentes por disco anexado. Se uma profundidade de fila, aplicativo não é força suficiente sistema toohello de IOs e processará menor quantidade de em um determinado período. Em outras palavras, Taxa de Transferência menor.

Por exemplo, no SQL Server, Olá configuração MAXDOP valor para uma consulta muito "4" informa que ele pode usar a consulta de saudação do toofour núcleos tooexecute SQL Server. SQL Server determinará o que é melhor fila profundidade valor e hello número de núcleos para a execução da consulta hello.

*Profundidade Ideal de Fila*  
Um valor muito alto de profundidade de fila também tem suas desvantagens. Se o valor de profundidade de fila é muito alta, o aplicativo hello tentará toodrive IOPS muito alto. A menos que o aplicativo tenha discos persistentes com provisão suficiente de IOPS, isso pode afetar negativamente as latências do aplicativo. Fórmula a seguir mostra a relação de saudação entre IOPS, latência e a profundidade da fila.  
    ![](media/storage-premium-storage-performance/image6.png)

Você não deve configurar a profundidade da fila tooany alto valor, mas tooan ideal, que pode oferecer IOPS suficientes para o aplicativo hello sem afetar as latências. Por exemplo, se precisar de latência do aplicativo hello toobe 1 milissegundo, Olá profundidade da fila necessário tooachieve é 5.000 IOPS, QD = 5000 x 0,001 = 5.

*Profundidade da fila para volume distribuído*  
Para um volume distribuído, mantenha uma profundidade de fila alta o suficiente, de tal forma que cada disco tenha uma profundidade de fila de pico individualmente. Por exemplo, considere um aplicativo que envia uma profundidade da fila de 2 e há 4 discos na faixa de saudação. duas solicitações de e/s Olá irá tootwo discos e restantes dois discos serão ocioso. Portanto, configure a profundidade da fila hello, de modo que todos os discos de saudação podem estar ocupados. Fórmula a seguir mostra como toodetermine Olá profundidade da fila de volumes distribuídos.  
    ![](media/storage-premium-storage-performance/image7.png)

## <a name="throttling"></a>Limitação
Provisões de armazenamento Premium do Azure especificado o número de IOPS e taxa de transferência dependendo de tamanhos de VM hello e tamanhos de disco que você escolher. Sempre que o aplicativo tenta toodrive IOPS ou a taxa de transferência acima desses limites de quais Olá VM ou o disco pode manipular, o armazenamento Premium limite-lo. Isso se manifesta na forma de saudação de degradação do desempenho em seu aplicativo. Isso pode significar latência mais alta, Taxa de Transferência mais baixa ou IOPS mais baixa. Se o Armazenamento Premium não for restrito, o aplicativo poderá falhar completamente, excedendo o que seus recursos são capazes de alcançar. Assim, o desempenho tooavoid emite devido toothrottling, sempre provisionamento de recursos suficientes para o seu aplicativo. Leve em consideração é discutido nas seções de tamanhos de disco acima e tamanhos de VM hello. Análise comparativa é Olá melhor maneira toofigure quais recursos você precisará toohost seu aplicativo.

## <a name="benchmarking"></a>Parâmetros de comparação
Análise comparativa é o processo de saudação de simular cargas de trabalho diferentes em seu aplicativo e medir o desempenho do aplicativo hello para cada carga de trabalho. Usando as etapas de saudação descritas em uma seção anterior, você coletou requisitos de desempenho de aplicativo hello. Ao executar o benchmark ferramentas em VMs de saudação hospedando o aplicativo hello, você pode determinar níveis de desempenho de saudação que seu aplicativo pode obter com o armazenamento Premium. Nesta seção, forneceremos exemplos de parâmetros de comparação de uma VM DS14 padrão provisionada com discos do Armazenamento Premium do Azure.

Usamos ferramentas comuns de parâmetros de comparação, Iometer e FIO, para Windows e Linux, respectivamente. Essas ferramentas geram vários threads simulando uma carga de trabalho e desempenho do sistema Olá medidas de produção. Usando as ferramentas de saudação você também pode configurar parâmetros, como bloco tamanho e a fila de profundidade, que normalmente não é possível alterar para um aplicativo. Isso proporciona mais flexibilidade toodrive Olá máximo desempenho em alta escala VM provisionado com discos de premium para diferentes tipos de cargas de trabalho do aplicativo. toolearn mais sobre cada ferramenta de avaliação, visite [Iometer](http://www.iometer.org/) e [FIO](http://freecode.com/projects/fio).

exemplos de saudação toofollow abaixo, crie uma VM DS14 padrão e anexe 11 toohello de discos de armazenamento Premium VM. De discos Olá 11, configurar 10 discos com o host de cache como "Nenhum" e distribua-os em um volume chamado NoCacheWrites. Configurar o cache como "ReadOnly" em disco restante de saudação do host e criar um volume chamado CacheReads com esse disco. Usando esta configuração, você será capaz de toosee Olá leitura e gravação desempenho máximo de uma VM DS14 padrão. Para obter etapas detalhadas sobre como criar uma VM DS14 com discos premium, ir muito[criar e usar a conta de armazenamento Premium para um disco de dados de máquina virtual](storage-premium-storage.md).

*Aquecendo Olá Cache*  
disco de Olá com cache de host de somente leitura será capaz de toogive IOPS maior que o limite de disco hello. tooget esse máximo o desempenho de leitura do cache de host hello, primeiro você deve aquecimento cache Olá desse disco. Isso garante que Olá IOs leitura conduzirão qual ferramenta de avaliação no volume CacheReads realmente acertos do cache hello e não o disco Olá diretamente. resultado de acertos de cache Olá no IOPS adicionais do cache único Olá habilitado em disco.

> **Importante:**  
> Você deve aquecimento cache Olá antes de executar a análise comparativa, sempre que a VM é reiniciada.
>
>

#### <a name="iometer"></a>Iometer
[Baixar a ferramenta de Iometer Olá](http://sourceforge.net/projects/iometer/files/iometer-stable/2006-07-27/iometer-2006.07.27.win32.i386-setup.exe/download) em Olá VM.

*Arquivo de teste*  
Iometer usa um arquivo de teste que é armazenado no volume Olá no qual você executará Olá teste de benchmark. Unidades de leituras e gravações neste teste IOPS de disco do arquivo toomeasure hello e taxa de transferência. O Iometer criará esse arquivo de teste caso você não tenha fornecido um. Crie um arquivo de teste de 200GB chamado iobw.tst em volumes de CacheReads e NoCacheWrites hello.

*Especificações de Acesso*  
Hello especificações, solicitação de tamanho de e/s, % de leitura/gravação, % aleatória/sequencial são configurados usando o guia de "Acesso especificações" hello Iometer. Crie uma especificação de acesso para cada um dos cenários de saudação descritos a seguir. Criar especificações de acesso hello e "Salvar" com um número apropriado nome – RandomWrites\_8K, RandomReads\_8 KB. Selecione especificação de saudação correspondente ao executar o cenário de teste de saudação.

Um exemplo de especificações de acesso para o cenário de IOPS de gravação máxima é mostrado abaixo,   
    ![](media/storage-premium-storage-performance/image8.png)

*Especificações de teste de IOPS máxima*  
máximo de toodemonstrate IOPs, use o menor tamanho de solicitação. Use o tamanho de solicitação de 8 K e crie especificações para gravações e leituras aleatórias.

| Especificação de acesso | Tamanho da solicitação | Aleatório % | Leitura % |
| --- | --- | --- | --- |
| RandomWrites\_8K |8 K |100 |0 |
| RandomReads\_8K |8 K |100 |100 |

*Especificações de Teste de Taxa de Transferência Máxima*  
toodemonstrate taxa de transferência máxima, use maior tamanho da solicitação. Use o tamanho de solicitação de 64 K e crie especificações para gravações e leituras aleatórias.

| Especificação de acesso | Tamanho da solicitação | Aleatório % | Leitura % |
| --- | --- | --- | --- |
| RandomWrites\_64K |64 K |100 |0 |
| RandomReads\_64K |64 K |100 |100 |

*Executando Olá Iometer teste*  
Olá as etapas abaixo toowarm o cache

1. Crie duas especificações de acesso com os valores mostrados abaixo:

   | Nome | Tamanho da solicitação | Aleatório % | Leitura % |
   | --- | --- | --- | --- |
   | RandomWrites\_1MB |1 MB |100 |0 |
   | RandomReads\_1MB |1 MB |100 |100 |
2. Execute teste de Iometer Olá para inicializar o disco de cache com os seguintes parâmetros. Use três threads de trabalho para o volume de destino hello e uma profundidade de fila de 128. Definir Olá durante saudação too2hrs de teste na guia de "Configuração de teste" hello "Tempo de execução".

   | Cenário | Volume de destino | Nome | Duração |
   | --- | --- | --- | --- |
   | Inicializar disco do cache |CacheReads |RandomWrites\_1MB |2 horas |
3. Execute teste de Iometer Olá para aquecer o disco de cache com os seguintes parâmetros. Use três threads de trabalho para o volume de destino hello e uma profundidade de fila de 128. Definir Olá durante saudação too2hrs de teste na guia de "Configuração de teste" hello "Tempo de execução".

   | Cenário | Volume de destino | Nome | Duração |
   | --- | --- | --- | --- |
   | Aquecer o disco do cache |CacheReads |RandomReads\_1MB |2 horas |

Após o disco do cache é aquecido, continue com cenários de teste de saudação listados abaixo. Olá toorun Iometer teste, use pelo menos três threads de trabalho para **cada** volume de destino. Para cada thread de trabalho, selecione o volume de destino Olá, definir a profundidade da fila e selecione uma das especificações de teste Olá salvada, conforme mostrado na tabela Olá abaixo, o cenário de teste correspondente toorun hello. tabela de Olá também mostra os resultados esperados para IOPS e taxa de transferência quando a execução desses testes. Em todos os cenários são usados um tamanho pequeno de 8 KB de E/S e uma profundidade de fila alta de 128.

| Cenário de teste | Volume de destino | Nome | Result |
| --- | --- | --- | --- |
| Máx. IOPS de leitura |CacheReads |RandomWrites\_8K |50.000 IOPS  |
| Máx. IOPS de gravação |NoCacheWrites |RandomReads\_8K |64.000 IOPS |
| Máx. IOPS combinada |CacheReads |RandomWrites\_8K |100.000 IOPS |
| NoCacheWrites |RandomReads\_8K | &nbsp; | &nbsp; |
| Máx. MB/s de leitura |CacheReads |RandomWrites\_64K |524 MB/s |
| Máx. MB/s de gravação |NoCacheWrites |RandomReads\_64K |524 MB/s |
| MB/s combinado |CacheReads |RandomWrites\_64K |1000 MB/s |
| NoCacheWrites |RandomReads\_64K | &nbsp; | &nbsp; |

Abaixo estão capturas de tela de saudação Iometer resultados de teste para cenários combinados de IOPS e taxa de transferência.

*IOPS Máxima de Leituras e Gravações Combinadas*  
![](media/storage-premium-storage-performance/image9.png)

*Taxa de Transferência Máxima de Leituras e Gravações Combinadas*  
![](media/storage-premium-storage-performance/image10.png)

### <a name="fio"></a>FIO
FIO é um armazenamento de toobenchmark popular ferramenta no hello VMs do Linux. Ele tem Olá flexibilidade tooselect diferentes e/s tamanhos, sequenciais ou aleatórias leituras e gravações. Ele gera threads de trabalho ou saudação de tooperform processos especificados operações de e/s. Você pode especificar o tipo de saudação de operações de e/s, que cada thread de trabalho deve executar usando os arquivos de trabalho. Criamos um arquivo de trabalho por cenário ilustrado nos exemplos de saudação abaixo. Você pode alterar as especificações de saudação essas trabalho arquivos toobenchmark diferentes cargas de trabalho em execução no armazenamento Premium. Exemplos de hello, estamos usando um execução de VM padrão de 14 DS **Ubuntu**. Olá Use mesma configuração descrita no início de saudação do hello [benchmark seção](#Benchmarking) e passiva cache Olá antes de executar testes de benchmark do hello.

Antes de começar, [baixe o FIO](https://github.com/axboe/fio) e instale-o em sua máquina virtual.

Olá executar comando a seguir para Ubuntu,

```
apt-get install fio
```

Usaremos quatro threads de trabalho para orientar operações de gravação e quatro threads de trabalho principais para operações de leitura em discos de saudação. Olá trabalhadores de gravação serão dirigindo tráfego no volume nocache"hello", que tem 10 discos com o cache configurado muito "None". Olá trabalhadores de leitura serão dirigindo tráfego no volume readcache"hello", que tem o 1 disco com o conjunto de cache muito "ReadOnly".

*IOPS máxima de gravação*  
Criar arquivo de saudação do trabalho com tooget de especificações seguintes máximo de IOPS de gravação. Dê o nome de "fiowrite.ini".

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[writer1]
rw=randwrite
directory=/mnt/nocache
[writer2]
rw=randwrite
directory=/mnt/nocache
[writer3]
rw=randwrite
directory=/mnt/nocache
[writer4]
rw=randwrite
directory=/mnt/nocache
```

Saudação de Observação Siga procedimentos essenciais que estejam de acordo com as diretrizes de design de saudação descritas nas seções anteriores. Essas especificações são essencial toodrive IOPS máximo,  

* Uma profundidade de fila alta de 256.  
* Um bloco pequeno de 8 KB.  
* Vários threads que executam gravações aleatórias.

Executar Olá tookick comando off Olá FIO de teste para 30 segundos, a seguir  

```
sudo fio --runtime 30 fiowrite.ini
```

Enquanto Olá teste é executado, você será toosee capaz de número de saudação de entrega de discos VM e Premium Olá IOPS de gravação. Conforme mostrado no exemplo hello abaixo, Olá DS14 VM está oferecendo seu limite de IOPS de 50.000 IOPS de gravação máxima.  
    ![](media/storage-premium-storage-performance/image11.png)

*IOPS máxima de leitura*  
Criar arquivo de saudação do trabalho com tooget de especificações seguintes máximo de IOPS de leitura. Dê o nome de "fioread.ini".

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache
```

Saudação de Observação Siga procedimentos essenciais que estejam de acordo com as diretrizes de design de saudação descritas nas seções anteriores. Essas especificações são essencial toodrive IOPS máximo,

* Uma profundidade de fila alta de 256.  
* Um bloco pequeno de 8 KB.  
* Vários threads que executam gravações aleatórias.

Executar Olá tookick comando off Olá FIO de teste para 30 segundos, a seguir

```
sudo fio --runtime 30 fioread.ini
```

Enquanto Olá teste é executado, você será o número de saudação do toosee capaz de leitura IOPS Olá VM e discos Premium estão entregando. Conforme mostrado no exemplo hello abaixo, Olá DS14 VM está oferecendo mais de 64.000 IOPS de leitura. Isso é uma combinação de disco hello e desempenho de cache de saudação.  
    ![](media/storage-premium-storage-performance/image12.png)

*IOPS Máxima de Leitura e Gravação*  
Criar arquivo de saudação do trabalho com as seguintes especificações de tooget máximo combinado de leitura e gravação IOPS. Dê o nome de "fioreadwrite.ini".

```
[global]
size=30g
direct=1
iodepth=128
ioengine=libaio
bs=4k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache

[writer1]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer2]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer3]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer4]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
```

Saudação de Observação Siga procedimentos essenciais que estejam de acordo com as diretrizes de design de saudação descritas nas seções anteriores. Essas especificações são essencial toodrive IOPS máximo,

* Uma profundidade alta de fila de 128.  
* Um bloco pequeno de 4 KB.  
* Vários threads que executam leituras e gravações aleatórias.

Executar Olá tookick comando off Olá FIO de teste para 30 segundos, a seguir

```
sudo fio --runtime 30 fioreadwrite.ini
```

Enquanto executa o teste Olá, será ser capaz de toosee Olá número de leitura combinada e IOPS de gravação Olá VM e entrega de discos Premium. Conforme mostrado no exemplo hello abaixo, Olá DS14 VM está oferecendo mais de 100.000 leitura combinada e IOPS de gravação. Isso é uma combinação de disco hello e desempenho de cache de saudação.  
    ![](media/storage-premium-storage-performance/image13.png)

*Taxa de Transferência Máxima Combinada*  
tooget Olá máximo combinado de leitura e gravação taxa de transferência, use um tamanho de bloco maior e a profundidade da fila grande com vários threads de execução de leituras e gravações. É possível usar um tamanho de bloco de 64 KB e uma profundidade de fila de 128.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre o Armazenamento Premium do Azure:

* [Armazenamento Premium: Armazenamento de Alto Desempenho para as Cargas de Trabalho da Máquina Virtual do Azure](storage-premium-storage.md)  

Para usuários do SQL Server, leia os artigos sobre Práticas recomendadas de desempenho para o SQL Server:

* [Práticas recomendadas para o SQL Server em Máquinas Virtuais do Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md)
* [Armazenamento Premium do Azure fornece desempenho mais alto para SQL Server na VM do Azure](http://blogs.technet.com/b/dataplatforminsider/archive/2015/04/23/azure-premium-storage-provides-highest-performance-for-sql-server-in-azure-vm.aspx)
