---
title: "desempenho de saudação aaaTesting de um serviço de nuvem | Microsoft Docs"
description: "Testar o desempenho de saudação de um serviço de nuvem usando o criador de perfil do hello Visual Studio"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7a5501aa-f92c-457c-af9b-92ea50914e24
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 98bd775e6ffcf948e737c5ec26399c81f4770fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service"></a>Teste de desempenho de saudação de um serviço de nuvem
## <a name="overview"></a>Visão geral
Você pode testar o desempenho de saudação de um serviço de nuvem em Olá maneiras a seguir:

* Use o diagnóstico do Azure toocollect informações sobre solicitações e conexões e tooreview estatísticas de site que mostram o desempenho do serviço Olá da perspectiva do cliente. tooget iniciado, consulte [configurar o diagnóstico para os serviços de nuvem do Azure e máquinas virtuais](http://go.microsoft.com/fwlink/p/?LinkId=623009).
* Use Olá Visual Studio profiler tooget uma análise detalhada dos aspectos computacionais de saudação do funcionamento do serviço de saudação. Como descrito neste tópico, você pode usar o desempenho do hello profiler toomeasure como um serviço é executado no Azure. Para obter informações sobre como desempenho do toouse Olá profiler toomeasure como um serviço é executado localmente em um emulador de computação, consulte [saudação de teste de desempenho de um Azure serviço de nuvem localmente no Olá usando o emulador de computação Olá criador de perfil do Visual Studio ](http://go.microsoft.com/fwlink/p/?LinkId=262845).

## <a name="choosing-a-performance-testing-method"></a>Escolhendo um método de teste de desempenho
### <a name="use-azure-diagnostics-toocollect"></a>Use toocollect de diagnóstico do Azure:
* Estatísticas em páginas ou em da Web, como solicitações e conexões.
* Estatísticas sobre funções, como a frequência com que uma função é reiniciada.
* Geral, informações sobre o uso de memória, como porcentagem de saudação do tempo Olá coletor de lixo leva ou Olá memória definida de uma função em execução.

### <a name="use-hello-visual-studio-profiler-to"></a>Use o criador de perfil do hello Visual Studio para:
* Determine quais funções utilizam Olá maior parte do tempo.
* Medir quanto tempo leva cada parte de um programa de computação intensivo.
* Comparar relatórios detalhados de desempenho de duas versões de um serviço.
* Analise a alocação de memória em mais detalhes do nível de saudação de alocações de memória individuais.
* Analisar problemas de simultaneidade em código multi-threaded.

Quando você usa o criador de perfil hello, você pode coletar dados quando um serviço de nuvem é executado localmente ou no Azure.

### <a name="collect-profiling-data-locally-to"></a>Colete dados de perfil localmente para:
* Testar o desempenho de saudação de uma parte de um serviço de nuvem, como a execução da função de trabalho específicos, que não exige uma carga simulada realística hello.
* Testar o desempenho de saudação de um serviço de nuvem isoladamente, em condições controladas.
* Olá testar o desempenho de um serviço de nuvem antes de implantá-lo tooAzure.
* Teste o desempenho de saudação de um serviço de nuvem em particular, sem prejudicar as implantações existentes hello.
* Testar o desempenho de saudação do serviço de saudação sem incorrer em encargos para execução no Azure.

### <a name="collect-profiling-data-in-azure-to"></a>Colete dados de perfil no Azure para:
* Testar o desempenho de saudação de um serviço de nuvem sob uma carga real ou simulada.
* Use o método de instrumentação hello de coleta de dados de criação de perfil, como esse tópico descreve posteriormente.
* Testar desempenho de saudação do serviço de saudação em Olá mesmo ambiente, como quando o serviço de saudação é executado em produção.

Você geralmente simula uma carga tootest serviços em nuvem em normal ou condições de estresse.

## <a name="profiling-a-cloud-service-in-azure"></a>Criando um perfil de serviço de nuvem no Azure
Quando você publicar seu serviço de nuvem do Visual Studio, você pode Olá serviço de perfil e especificar Olá criação de perfil de configurações que fornecem que Olá informações que você deseja. Uma sessão de criação de perfil é iniciada para cada instância de uma função. Para obter mais informações sobre como toopublish o serviço do Visual Studio, consulte [publicação tooan serviço de nuvem do Azure do Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx).

toounderstand mais informações sobre a criação de perfil de desempenho no Visual Studio, consulte [tooPerformance guia do Iniciante criação de perfil](https://msdn.microsoft.com/library/azure/ms182372.aspx) e [analisando o desempenho do aplicativo usando ferramentas de criação de perfil](https://msdn.microsoft.com/library/azure/z9z62c29.aspx).

> [!NOTE]
> Você pode habilitar o IntelliTrace ou a criação de perfis quando publicar seu serviço de nuvem. Não é possível habilitar ambos.
> 
> 

### <a name="profiler-collection-methods"></a>Métodos de coleção do criador de perfil
Você pode usar diferentes métodos de coleção para a criação de perfil com base nos seus problemas de desempenho:

* **Amostragem de CPU** - esse método coleta estatísticas de aplicativo que são úteis para a análise inicial de problemas de utilização de CPU. Amostragem de CPU é Olá método sugerido para iniciar a maioria das investigações de desempenho. Há um impacto pequeno no aplicativo hello que você estiver criando um perfil quando você coletar dados de amostragem de CPU.
* **Instrumentação** - esse método coleta dados detalhados de tempo úteis para a análise concentrada e para analisar problemas de desempenho de entrada/saída. método de instrumentação Hello registra cada entrada, saída e chamada de função das funções de saudação em um módulo durante uma criação de perfil. Esse método é útil para coletar informações detalhadas de cronometragem sobre uma seção de seu código e para entender o impacto de saudação de operações de entrada e saídas no desempenho do aplicativo. Este método está desabilitado para um computador que esteja executando um sistema operacional de 32 bits. Essa opção está disponível somente quando você executa o serviço de nuvem Olá no Azure, não localmente no emulador de computação hello.
* **Alocação de memória .NET** -esse método coleta dados de alocação de memória do .NET Framework usando o método de criação de perfil de amostragem de saudação. Olá os dados coletados incluem hello número e tamanho dos objetos alocados.
* **Simultaneidade** - esse método coleta dados de contenção de recursos e dados de execução de thread e processo úteis na análise de aplicativos multi-threaded e multiprocessados. método de simultaneidade Hello coleta dados para cada evento que bloqueia a execução de seu código, como quando um thread aguarda bloqueado acesso tooan aplicativo recurso toobe liberado. Este método é útil para analisar aplicativos multi-threaded.
* Você também pode habilitar **criação de perfil de interação de camadas**, que fornece informações adicionais sobre os tempos de execução de saudação do ADO.NET síncronas chama em funções de aplicativos de várias camadas que se comunicam com um ou mais bancos de dados. Você pode coletar dados de interação de camadas com qualquer um dos métodos de criação de perfil de saudação. Para saber mais sobre a criação de perfil de interação de camadas, consulte [Exibição de interações de camada](https://msdn.microsoft.com/library/azure/dd557764.aspx).

## <a name="configuring-profiling-settings"></a>Definindo configurações de criação de perfil
Olá na ilustração a seguir como tooconfigure suas configurações de perfil na caixa de diálogo Olá publicar aplicativo do Azure.

![Definir configurações de criação de perfil](./media/vs-azure-tools-performance-profiling-cloud-services/IC526984.png)

> [!NOTE]
> Olá tooenable **permitem a criação de perfil** caixa de seleção, você deve ter o criador de perfil de saudação instalado no computador local hello, que você está usando toopublish seu serviço de nuvem. Por padrão, o criador de perfil de saudação está instalado quando você instala o Visual Studio.
> 
> 

### <a name="tooconfigure-profiling-settings"></a>tooconfigure configurações de criação de perfil
1. No Gerenciador de soluções, abrir o menu de atalho de saudação de seu projeto do Azure e, em seguida, escolha **publicar**. Para obter etapas detalhadas sobre como toopublish um serviço de nuvem, consulte [publicar uma nuvem de serviço usando as ferramentas do Azure de Olá](http://go.microsoft.com/fwlink/p?LinkId=623012).
2. Em Olá **publicar aplicativo do Azure** caixa de diálogo, escolha Olá **configurações avançadas** guia.
3. tooenable criação de perfil, selecione Olá **permitem a criação de perfil** caixa de seleção.
4. tooconfigure suas configurações de perfil, escolha Olá **configurações** hiperlink. caixa de diálogo de configurações de criação de perfil de saudação é exibida.
5. De saudação **qual método de criação de perfil você gostaria que toouse** botões de opção, escolha o tipo de saudação de criação de perfil que você precisa.
6. interação de camadas de saudação toocollect criação de perfil de dados, selecione Olá **habilitar perfis de interação de camada** caixa de seleção.
7. configurações de saudação toosave, escolha Olá **Okey** botão.
   
    Quando você publica esse aplicativo, essas configurações são usados toocreate Olá sessão para cada função de criação de perfil.

## <a name="viewing-profiling-reports"></a>Exibindo relatórios de criação de perfil
Uma sessão de criação de perfil é gerada para cada instância de uma função no serviço de nuvem. a criação de perfil relatórios tooview de cada sessão do Visual Studio, você pode exibir a janela do Gerenciador de servidores de saudação e escolha uma instância de uma função hello tooselect de nó de computação do Azure. Você pode exibir relatório de criação de perfil conforme mostrado na ilustração a seguir de saudação do hello.

![Exibir relatórios de criação de perfil do Azure](./media/vs-azure-tools-performance-profiling-cloud-services/IC748914.png)

### <a name="tooview-profiling-reports"></a>tooview relatórios de criação de perfil
1. tooview Olá janela Gerenciador de servidores no Visual Studio, escolha Olá de barra de menu Exibir, Gerenciador de servidores.
2. Escolha o nó de computação do Azure hello e, em seguida, escolha o nó de implantação do Azure Olá Olá serviço de nuvem que você selecionou tooprofile quando publicado do Visual Studio.
3. perfis tooview relatórios de uma instância, escolha a função hello no serviço hello, menu de atalho Olá aberto para uma instância específica, **Exibir relatório de criação de perfil**.
   
    relatório Hello, um arquivo. vsp, agora é baixado do Azure e status de saudação do download de saudação aparece na Olá Log de atividades do Azure. Quando a conclusão do download hello, Olá relatório de criação de perfil aparece em uma guia no editor de saudação do Visual Studio chamado <Role name>  *<Instance Number>*  <identifier>. vsp. Dados de resumo para o relatório de saudação é exibida.
4. toodisplay diferentes modos de exibição de relatório hello, na lista de exibição atual hello, escolha o tipo de saudação do modo de exibição que você deseja. Para saber mais, consulte [Exibições de relatório de ferramentas de criação de perfil](https://msdn.microsoft.com/library/azure/bb385755.aspx).

## <a name="next-steps"></a>Próximas etapas
[Depurando serviços de nuvem](https://msdn.microsoft.com/library/azure/ee405479.aspx)

[Publicação tooan serviço de nuvem do Azure do Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)

