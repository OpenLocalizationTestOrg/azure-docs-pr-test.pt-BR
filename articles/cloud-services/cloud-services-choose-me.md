---
title: "opções - serviços de nuvem de computação aaaAzure | Microsoft Docs"
description: "Saiba mais sobre opções de hospedagem de computação do Azure e como elas funcionam: Serviço de Aplicativo, Serviços de Nuvem e Máquinas Virtuais"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
ms.assetid: ed7ad348-6018-41bb-a27d-523accd90305
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: e7f109a54c61cc2f37644d39a61d2d932a374587
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-choose-cloud-services-or-something-else"></a>Devo escolher os serviços de nuvem ou algo mais?
É a opção de saudação do serviços de nuvem do Azure para você? A Azure fornece diferentes modelos de hospedagem para executar aplicativos. Cada um deles fornece um conjunto diferente de serviços, então qual deles você escolher depende exatamente o que você está tentando toodo.

[!INCLUDE [compute-table](../../includes/compute-options-table.md)]

<a name="tellmecs"></a>

## <a name="tell-me-about-cloud-services"></a>Fale-me sobre os serviços de nuvem
Os Serviços de Nuvem são um exemplo de [PaaS (Plataforma como Serviço)](https://azure.microsoft.com/overview/what-is-paas/). Como [do serviço de aplicativo](../app-service-web/app-service-web-overview.md), essa tecnologia é projetado toosupport aplicativos escalonáveis, confiáveis e barata toooperate. Assim como um aplicativo de serviço é hospedado em máquinas virtuais, portanto muito são serviços de nuvem, no entanto, você tem mais controle sobre Olá VMs. Você pode instalar seu próprio software nas VMs do Serviço de Nuvem e controlá-los remotamente.

![cs_diagram](./media/cloud-services-choose-me/diagram.png)

Mais controle também significa menos facilidade de uso. A menos que você precisar de opções de controle adicional Olá, normalmente é mais rápido e fácil tooget um aplicativo web para cima e em execução em aplicativos da Web no serviço de aplicativo comparada tooCloud serviços.

Há dois tipos de funções de Serviço de Nuvem. Olá a única diferença entre Olá dois é como sua função é hospedada na máquina virtual de saudação.

* **Função Web**  
Implanta e hospeda o aplicativo automaticamente por IIS.

* **Função de trabalho**  
Não usa IIS e executa o aplicativo de modo autônomo.

Por exemplo, um aplicativo simples pode usar apenas uma única função web, atendendo a um site. Um aplicativo mais complexo pode usar um toohandle de função web solicitações de entrada dos usuários, em seguida, passar essas solicitações tooa a função de trabalho para processamento. (Essa comunicação pode usar o [Barramento de Serviço](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md) ou as [Filas do Azure](../storage/common/storage-introduction.md)).

Como Olá figura anterior sugere, todos os Olá VMs em um único aplicativo executado em Olá mesmo serviço de nuvem. Os usuários acesso Olá aplicativo por meio de um único endereço IP público, com solicitações automaticamente com balanceamento de carga entre VMs do aplicativo hello. plataforma de saudação [dimensiona e implanta](cloud-services-how-to-scale.md) Olá VMs em um aplicativo de serviços de nuvem de uma maneira que evita um ponto único de falha de hardware.

Embora os aplicativos executam em máquinas virtuais, é importante toounderstand serviços de nuvem fornece PaaS, não IaaS. Aqui está uma maneira toothink sobre ele: com IaaS, como as máquinas virtuais do Azure, você primeiro criar e configurar ambiente Olá seu aplicativo é executado, e implantar seu aplicativo para esse ambiente. Você está responsável por gerenciar grande parte do mundo, fazer coisas como implantar novas versões de patches do sistema operacional de saudação em cada VM. Em PaaS, por outro lado, é como se o ambiente de saudação já existe. Toodo se implantar seu aplicativo. Gerenciamento da plataforma de saudação executa, incluindo a implantação de novas versões do sistema operacional de saudação é manipulado para você.

## <a name="scaling-and-management"></a>Escala e gerenciamento
Com os Serviços de Nuvem, você não cria máquinas virtuais. Em vez disso, você pode fornecer um arquivo de configuração que informa que o Azure a quantidade de cada desejado, como **três instâncias de função de web** e **duas instâncias de função de trabalho**, e a plataforma de saudação criará para você.  Você ainda escolhe o [tamanho](cloud-services-sizes-specs.md) que as VMs devem ter, mas não as cria explicitamente. Se seu aplicativo precisa toohandle uma carga maior, solicite mais VMs e o Azure cria essas instâncias. Se diminuir a carga hello, você pode desligar as instâncias e parar a pagar por eles.

Um aplicativo de serviços de nuvem normalmente é feito toousers disponíveis por meio de um processo de duas etapas. Um desenvolvedor primeiro [carregamentos Olá aplicativo](cloud-services-how-to-create-deploy.md) toohello plataforma da área de transferência. Ao desenvolvedor hello está pronto aplicativo hello de toomake ao vivo, eles usam o preparo do hello tooswap portal do Azure com a produção. Isso [alternar entre a produção e preparo](cloud-services-nodejs-stage-application.md) pode ser feito sem tempo de inatividade, o que permite que um aplicativo em execução a ser a nova versão tooa atualizado sem afetar seus usuários.

## <a name="monitoring"></a>Monitoramento
Os Serviços de Nuvem também fornecem monitoramento. Como o máquinas virtuais do Azure, ele detecta um servidor físico com falha e reinicia Olá máquinas virtuais que estavam em execução no servidor em um novo computador. Mas os Serviços de Nuvem também detectam as VMs e os aplicativos com falha, não apenas as falhas de hardware. Diferentemente das máquinas virtuais, ele tem um agente em cada função web e de trabalho, e por isso, é possível toostart novas VMs e instâncias do aplicativo quando ocorrem falhas.

Olá PaaS natureza dos serviços de nuvem tem outras implicações muito. Uma saudação mais importante é que os aplicativos criados sobre esta tecnologia devem ser escritos toorun corretamente quando qualquer instância de função web ou de trabalho falha. tooachieve isso, um aplicativo não deve manter os serviços de nuvem de estado no hello sistema de arquivos de suas próprias VMs. Ao contrário das máquinas virtuais criadas com as máquinas virtuais do Azure, gravações feitas tooCloud serviços VMs não são persistentes; Não há nada como um disco de dados de máquinas virtuais. Em vez disso, um aplicativo deve explicitamente os serviços de nuvem gravar tooSQL de estado de todos os banco de dados, blobs, tabelas ou algum outro armazenamento externo. Criando aplicativos dessa maneira torna tooscale mais fácil e mais resistente toofailure, ambas as metas importantes dos serviços de nuvem.

## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo de serviço de nuvem em .NET](cloud-services-dotnet-get-started.md)  
[Criar um aplicativo de serviço de nuvem em Node.js](cloud-services-nodejs-develop-deploy-app.md)  
[Criar um aplicativo de serviço de nuvem em PHP](../cloud-services-php-create-web-role.md)  
[Criar um aplicativo de serviço de nuvem no Python](cloud-services-python-ptvs.md)

