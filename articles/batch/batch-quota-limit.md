---
title: aaaService cotas e limites de lote do Azure | Microsoft Docs
description: "Saiba mais sobre cotas do lote do Azure padrão, limites e restrições e como toorequest cota aumenta"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a>Cotas e limites de serviço do Lote

Como com outros serviços do Azure, há limites no determinados recursos associados à saudação serviço de lote. Muitos desses limites são cotas padrão aplicadas pelo Azure no nível de conta ou assinatura de saudação. Este artigo discute esses padrões e como você pode solicitar aumentos de cotas.

Lembre-se dessas cotas quando estiver projetando e dimensionando suas cargas de trabalho do Lote. Por exemplo, se o pool não alcançar o número de destino de Olá de nós de computação que você especificou, você pode atingiu limite de cota de núcleos Olá para a conta de lote ou uma cota de núcleos VM regional para sua assinatura.

Você pode executar várias cargas de trabalho em lotes em uma única conta de lote ou distribuir suas cargas de trabalho entre contas em lotes que estão em Olá mesma assinatura, mas em diferentes regiões do Azure.

Se você planejar toorun cargas de trabalho de produção em lote, talvez seja necessário tooincrease uma ou mais das cotas Olá acima padrão hello. Se você quiser tooraise uma cota, você pode abrir um online [solicitação de suporte do cliente](#increase-a-quota) sem custo adicional.

> [!NOTE]
> Uma cota é um limite de crédito, não uma garantia de capacidade. Se você precisar de capacidade em larga escala, entre em contato com o suporte do Azure.
> 
> 

## <a name="resource-quotas"></a>Cotas de recursos
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a>Cotas no modo de assinatura de usuário

Para uma conta de lote com o modo de alocação de pool definido muito**assinatura de usuário**, máquinas virtuais e outros recursos, como contas de armazenamento do lote, são criados diretamente em sua assinatura, quando um pool é criado. cota de núcleos de lote do Azure Olá não se aplica a conta tooan criada nesse modo. Em vez disso, são aplicadas as cotas de saudação em sua assinatura de núcleos de computação regional e outros recursos. Saiba mais sobre a [assinatura do Azure e limites de serviços, cotas e restrições](../azure-subscription-service-limits.md).

Ao planejar o uso de recursos para uma conta criada no modo de usuário de assinatura, Olá Observação recursos de lote (em núcleos de toocompute adição) a seguir são necessários para cada 40 VMs do Linux, ou 20 VMs do Windows:

| Recurso | Cota | Provedor |
| --- | ---| --- |
| Uma conta de armazenamento | Contas de armazenamento | Microsoft.Storage |
| Um endereço IP público | Endereços IP públicos | Microsoft.Network | 
| Uma rede virtual | Redes Virtuais | Microsoft.Network | 
| Um grupo de segurança de rede | Grupos de segurança de rede | Microsoft.Network | 
| Conjunto de escala de máquina virtual | Conjuntos de Escala de Máquina Virtual | Microsoft.Compute | 
| Um balanceador de carga | Balanceadores de Carga | Microsoft.Network | 

cota de núcleos de saudação em um nível regional ou por família VM deve ser conjunto acordo toohello VM tamanho necessário para o pool de lote ou pools:

| Quota | Provedor |
| --- | ---- |
| Total de núcleos regionais | Microsoft.Compute |
| … Núcleos de família | Microsoft.Compute |



## <a name="other-limits"></a>Outros limites
| **Recurso** | **Limite máximo** |
| --- | --- |
| [Tarefas simultâneas](batch-parallel-node-tasks.md) por nó de computação |4 vezes o número de núcleos de nó |
| [Aplicativos](batch-application-packages.md) por conta do Lote |20 |
| Pacotes de aplicativos por aplicativo |40 |
| Tamanho do pacote de aplicativos (cada) |Aproximadamente 195 GB<sup>1</sup> |
| Tamanho de tarefa inicial máximo | 32768 caracteres<sup>2</sup> |

<sup>1</sup> O limite do Armazenamento do Azure para o tamanho máximo do blob de blocos<br />
<sup>2</sup> Inclui arquivos de recurso e variáveis de ambiente

## <a name="view-batch-quotas"></a>Exibir cotas do Lote
Exibir suas cotas de conta de lote no hello [portal do Azure][portal].

1. Selecione **contas de lote** no portal de Olá, selecione conta de lote Olá você está interessado.
2. Selecione **propriedades** na folha de menu da conta do lote de saudação.
3. folha de propriedades de saudação exibe Olá **cotas** aplicadas toohello conta do lote
   
    ![Cotas para conta do Lote][account_quotas]

Para uma conta de lote criada no modo de usuário de assinatura, Olá de exibição relacionados cotas de assinatura no hello Portal do Azure.

1. Selecione **assinaturas**e selecione a assinatura Olá que você está usando para Olá conta do lote.

2. Em Olá **assinatura** folha, selecione **uso + cotas**.



## <a name="increase-a-quota"></a>Aumentar uma cota
Siga essas toorequest etapas aumentar uma cota para a conta de lote ou sua assinatura usando Olá [portal do Azure][portal]. tipo de saudação do aumento da cota depende do modo de alocação de pool de saudação da sua conta do lote.

### <a name="increase-a-batch-cores-quota"></a>Aumentar a cota de núcleos de lote 

Se sua conta em lotes foi criada no **serviço de lote** modo, siga essas etapas toorequest um aumento de cota de núcleos de lote:

1. Selecione Olá **ajuda + suporte** lado a lado em seu painel do portal ou Olá ponto de interrogação (**?**) no canto superior direito de saudação do portal de saudação.
2. Selecione **Nova solicitação de suporte** > **Fundamentos**.
3. Em Olá **Noções básicas sobre** folha:
   
    a. **Tipo de Problema** > **Cota**
   
    b. Selecione sua assinatura.
   
    c. **Tipo de cota** > **Lote**
   
    d. **Plano de suporte** > **Suporte da cota - Incluído**
   
    Clique em **Avançar**.
4. Em Olá **problema** folha:
   
    a. Selecione um **severidade** tooyour de acordo com [impacto nos negócios][support_sev].
   
    b. Em **detalhes**, especifique cada cota que você deseja toochange, nome da conta em lotes hello e novo limite de saudação.
   
    Clique em **Avançar**.
5. Em Olá **informações de contato** folha:
   
    a. Selecione um **método de contato preferencial**.
   
    b. Verifique e insira os detalhes de contato Olá necessário.
   
    Clique em **criar** toosubmit Olá o suporte da solicitação.

Depois que a solicitação de suporte foi enviada, o suporte do Azure entrará em contato com você. Observe que concluir solicitação Olá poderá levar até too2 dias.

### <a name="increase-a-subscription-cores-quota"></a>Aumentar a cota de núcleos de assinatura

Se sua conta do Lote foi criada no modo **assinatura do usuário** e você precisa de núcleos regionais adicionais ou de família VM, solicite um aumento de cota em sua assinatura. Para as etapas, consulte [Solicitações de aumento da cota de núcleo do Gerenciador de recursos](../azure-supportability/resource-manager-core-quotas-request.md).



## <a name="related-topics"></a>Tópicos relacionados
* [Criar uma conta de lote do Azure usando Olá portal do Azure](batch-account-create-portal.md)
* [Visão geral dos recursos do Lote do Azure](batch-api-basics.md)
* [Assinatura do Azure e limite de serviços, cotas e restrições](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
