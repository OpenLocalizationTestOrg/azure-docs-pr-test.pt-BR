---
title: "aaaTroubleshooting falha de alocação de serviço de nuvem | Microsoft Docs"
description: "Solução de problemas de falha de alocação ao implantar Serviços de Nuvem no Azure"
services: azure-service-management, cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 529157eb-e4a1-4388-aa2b-09e8b923af74
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: dfd5cc4663ccc6ed1b27ca9df579182737363b0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-allocation-failure-when-you-deploy-cloud-services-in-azure"></a>Solução de problemas de falha de alocação ao implantar Serviços de Nuvem no Azure
## <a name="summary"></a>Resumo
Quando você implanta instâncias tooa serviço de nuvem ou adiciona novo web ou instâncias de função de trabalho, o Microsoft Azure aloca recursos de computação. Ocasionalmente, você poderá receber erros ao executar essas operações, mesmo antes de atingir Olá limites de assinatura do Azure. Este artigo explica as causas de saudação de alguns Olá comuns de falhas de alocação e sugere possíveis correções. informações de saudação também podem ser útil ao planejar a implantação Olá dos seus serviços.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

### <a name="background--how-allocation-works"></a>Histórico – Como funciona a alocação
servidores de saudação em datacenters do Azure são particionadas em clusters. Ocorre uma nova tentativa de solicitação de alocação de serviço de nuvem em vários clusters. Quando a primeira instância de saudação é serviço de nuvem implantado tooa (na preparação ou produção), que o serviço de nuvem é fixado tooa cluster. Mais detalhes as implantações de serviço de nuvem Olá acontecerá em Olá mesmo cluster. Neste artigo, vamos nos referir toothis como "fixado tooa cluster". O diagrama 1 abaixo ilustra o caso de saudação de uma alocação normal que é tentada em vários clusters; Diagrama 2 mostra o caso de saudação de uma alocação tooCluster fixo que 2 porque o que é onde Olá CS_1 de serviço de nuvem existente está hospedado.

![Diagrama de alocação](./media/cloud-services-allocation-failure/Allocation1.png)

### <a name="why-allocation-failure-happens"></a>Motivos das falhas de alocação
Quando uma solicitação de alocação é fixado tooa cluster, há uma possibilidade maior de falha toofind liberar recursos desde que o pool de recursos disponíveis de saudação é limitado tooa cluster. Além disso, se sua solicitação de alocação está fixado tooa cluster, mas tipo de saudação do recurso solicitado não é suportado por cluster, a solicitação falhará mesmo que o cluster Olá tem recurso gratuito. Diagrama de 3 abaixo ilustra o caso de Olá onde uma alocação fixada falha porque cluster do candidato apenas Olá não tem recursos gratuitos. Diagrama 4 ilustra caso Olá onde uma alocação fixada falha porque não dá suporte a cluster de candidato apenas Olá Olá solicitado tamanho da VM, mesmo que o cluster Olá tem liberar recursos.

![Falha na alocação fixada](./media/cloud-services-allocation-failure/Allocation2.png)

## <a name="troubleshooting-allocation-failure-for-cloud-services"></a>Solucionando problemas de falha de alocação para serviços de nuvem
### <a name="error-message"></a>Mensagem de erro
Você pode ver Olá a seguinte mensagem de erro:

    "Azure operation '{operation id}' failed with code Compute.ConstrainedAllocationFailed. Details: Allocation failed; unable toosatisfy constraints in request. hello requested new service deployment is bound tooan Affinity Group, or it targets a Virtual Network, or there is an existing deployment under this hosted service. Any of these conditions constrains hello new deployment toospecific Azure resources. Please retry later or try reducing hello VM size or number of role instances. Alternatively, if possible, remove hello aforementioned constraints or try deploying tooa different region."

### <a name="common-issues"></a>Problemas comuns
Aqui estão Olá cenários comuns de alocação que causam um alocação solicitação toobe tooa fixados único cluster.

* Em seguida, implantar tooStaging Slot - se um serviço de nuvem tem uma implantação em nenhum slot, serviço de nuvem inteira Olá é cluster específico tooa fixados.  Isso significa que se uma implantação já existe no slot de produção de hello, em seguida, uma nova implantação de preparo só pode ser alocada no mesmo cluster como o slot de produção de hello de saudação. Se o cluster hello está se aproximando da capacidade, a solicitação de saudação pode falhar.
* Dimensionamento - adicionando novas instâncias tooan serviço de nuvem existente deve alocar no hello mesmo cluster.  Solicitações pequenas de dimensionamento normalmente podem ser alocadas, mas nem sempre. Se o cluster hello está se aproximando da capacidade, a solicitação de saudação pode falhar.
* Grupo de afinidade - um novo serviço de nuvem vazio do tooan de implantação pode ser alocado pela malha hello em qualquer cluster nessa região, a menos que o serviço de nuvem Olá é fixado tooan grupo de afinidade. Implantações toohello mesmo grupo de afinidade será tentado no hello mesmo cluster. Se o cluster hello está se aproximando da capacidade, a solicitação de saudação pode falhar.
* Rede virtual do grupo de afinidade - redes virtuais mais antigas foram tooaffinity empatados grupos em vez de regiões, e serviços de nuvem nessas redes virtuais seria cluster do grupo de afinidade toohello fixados. Tipo de toothis de implantações de rede virtual será tentado no cluster Olá fixado. Se o cluster hello está se aproximando da capacidade, a solicitação de saudação pode falhar.

## <a name="solutions"></a>Soluções
1. Reimplantação tooa novo serviço de nuvem - esta solução é provavelmente toobe mais bem-sucedida pois permite Olá plataforma toochoose de todos os clusters nessa região.

   * Implantar Olá carga de trabalho tooa novo serviço de nuvem  
   * Atualizar Olá CNAME ou um registro toopoint tráfego toohello novo serviço de nuvem
   * Depois que o tráfego de zero será site antigo toohello, você pode excluir serviço de nuvem antigo hello. Essa solução não causará qualquer tempo de inatividade.
2. Excluir os slots de preparo e produção - essa solução irá preservar seu nome DNS existente, mas fará com que o aplicativo de tooyour de tempo de inatividade.

   * Excluir a produção de hello e de preparo slots de um serviço de nuvem existente para que o serviço de nuvem hello está vazio e, em seguida,
   * Crie uma nova implantação no serviço de nuvem existente hello. Isso tentará novamente tooallocation em todos os clusters na região de saudação. Certifique-se de que o serviço de nuvem Olá não é grupo de afinidade tooan associado.
3. IP reservado - esta solução irá preservar o IP existentes de endereço, mas fará com que o aplicativo de tooyour de tempo de inatividade.  

   * Criar um IP reservado para sua implantação existente usando o Powershell

     ```
     New-AzureReservedIP -ReservedIPName {new reserved IP name} -Location {location} -ServiceName {existing service name}
     ```
   * Siga #2 acima, tornando toospecify se Olá ReservedIP novo no CSCFG do serviço de saudação.
4. Remover o grupo de afinidade para novas implantações: grupos de afinidade não são mais recomendados. Siga as etapas para #1 acima toodeploy um novo serviço de nuvem. Certifique-se de que o serviço de nuvem não esteja em um grupo de afinidade.
5. Converter tooa rede Virtual Regional - consulte [como toomigrate de tooa de grupos de afinidade de rede Virtual Regional (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
