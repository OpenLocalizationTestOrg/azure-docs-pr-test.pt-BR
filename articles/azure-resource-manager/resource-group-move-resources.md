---
title: aaaMove recursos do Azure toonew assinatura ou grupo de recursos | Microsoft Docs
description: Use o Gerenciador de recursos do Azure toomove recursos tooa novo grupo de recursos ou assinatura.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a>Mover grupo de recursos toonew de recursos ou assinatura
Este tópico mostra como toomove recursos tooeither uma nova assinatura ou um novo recurso de grupo no hello mesma assinatura. Você pode usar o portal hello, o PowerShell, CLI do Azure ou Olá recursos de toomove da API REST. operações de movimentação de saudação neste tópico são tooyou disponível sem qualquer assistência do suporte do Azure.

Ao mover recursos, grupo de saudação de origem e o grupo de destino Olá são bloqueadas durante a operação de saudação. Gravar e operações de exclusão estão bloqueados em grupos de recursos de saudação até que seja concluída Olá move. Esse bloqueio significa que você não pode adicionar, atualizar ou excluir recursos em grupos de recursos de saudação, mas isso não significa que recursos Olá congelados. Por exemplo, se você mover um SQL Server e seu banco de dados tooa novo grupo de recursos, um aplicativo que usa o banco de dados de saudação experiências sem tempo de inatividade. Ele pode ler e gravar toohello banco de dados.

Você não pode alterar o local de saudação do recurso de saudação. Mover um recurso só move tooa novo grupo de recursos. Olá novo grupo de recursos pode ter um local diferente, mas que não altera a localização de saudação do recurso de saudação.

> [!NOTE]
> Este artigo descreve como a conta ofertas toomove recursos dentro do Azure existente. Se você realmente quiser toochange sua conta do Azure, oferecendo (como atualizar do pagamento de toopre pré-pago) enquanto continua toowork com recursos existentes, consulte [alternar sua oferta de assinatura do Azure tooanother](../billing/billing-how-to-switch-azure-offer.md).
>
>

## <a name="checklist-before-moving-resources"></a>Lista de verificação antes de mover recursos
Há algumas etapas importantes tooperform antes de mover um recurso. Ao verificar essas condições, é possível evitar erros.

1. Olá assinaturas de origem e de destino devem existir no hello mesmo [locatário do Active Directory do Azure](../active-directory/active-directory-howto-tenant.md). toocheck ambas as assinaturas têm Olá mesmo ID de locatário, use o Azure PowerShell ou CLI do Azure.

  Para o Azure PowerShell, use:

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  Para a CLI 2.0 do Azure, use:

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  Se Olá locatário IDs para assinaturas de origem e destino Olá não são Olá mesmo, você pode tentar toochange diretório de saudação para assinatura de saudação. No entanto, essa opção está apenas disponível tooService administradores que está conectado com uma conta da Microsoft (não uma conta organizacional). alterando o diretório hello, login toohello de tooattempt [portal clássico](https://manage.windowsazure.com/)e selecione **configurações**e selecione a assinatura de saudação. Se hello **Editar diretório** ícone estiver disponível, selecione-a como toochange Olá associado do Active Directory do Azure.

  ![editar diretório](./media/resource-group-move-resources/edit-directory.png)

  Se esse ícone não estiver disponível, você deve entrar em contato com o suporte toomove Olá recursos tooa novo locatário.

2. serviço de saudação deve habilitar recursos de toomove de capacidade de saudação. Este tópico lista quais serviços permitem mover os recursos e quais serviços não habilitam a movimentação dos recursos.
3. assinatura de destino Olá deve ser registrada para provedor de recursos de saudação do recurso hello está sendo movido. Se não, você recebe um erro informando que Olá **assinatura não está registrada para um tipo de recurso**. Você pode encontrar esse problema ao mover uma nova assinatura de recursos tooa, mas essa assinatura nunca foi usada com o tipo de recurso. toolearn como toocheck Olá status de registro e registrar provedores de recursos, consulte [provedores de recursos e tipos de](resource-manager-supported-services.md).

## <a name="when-toocall-support"></a>Quando o suporte toocall
Você pode mover a maioria dos recursos por meio de operações de autoatendimento Olá mostradas neste tópico. Use operações de autoatendimento Olá para:

* Mova os recursos do Resource Manager.
* Mover recursos clássicos de acordo com o toohello [limitações de implantação clássico](#classic-deployment-limitations).

Telefonar para o suporte quando você precisa:

* Mova recursos tooa nova conta do Azure (e locatário do Active Directory do Azure).
* Mover recursos clássicos, mas está tendo problemas com as limitações de saudação.

## <a name="services-that-enable-move"></a>Serviços que permitem mover
Por enquanto, serviços de saudação que permitem que um novo grupo de recursos de movimentação tooboth e assinatura são:

* Gerenciamento de API
* Aplicativos do Serviço de Aplicativo (aplicativos Web) - consulte [Limitações do Serviço de Aplicativo](#app-service-limitations)
* Application Insights
* Automação
* Batch
* Bing Mapas
* CDN
* Serviços de Nuvem - veja [Limitações da implantação clássica](#classic-deployment-limitations)
* Serviços Cognitivos
* Content Moderator
* Catálogo de Dados
* Data Factory
* Análises Data Lake
* Repositório Data Lake
* DNS
* Azure Cosmos DB
* Hubs de Eventos
* Clusters HDInsight – veja [Limitações do HDInsight](#hdinsight-limitations)
* Hubs IoT
* Cofre da Chave
* Balanceadores de Carga
* Aplicativos Lógicos
* Machine Learning
* Serviços de mídia
* Engajamento Móvel
* Hubs de Notificação
* Insights Operacionais
* Gerenciamento de Operações
* Power BI
* Cache Redis
* Agendador
* Search
* Gerenciamento do Servidor
* Barramento de Serviço
* Service Fabric
* Armazenamento
* Armazenamento (clássico) - consulte [Limitações da implantação clássica](#classic-deployment-limitations)
* Stream Analytics – os trabalhos do Stream Analytics não podem ser movidos durante o estado de execução.
* Servidor de banco de dados do SQL - Olá banco de dados e o servidor devem residir no hello mesmo grupo de recursos. Quando você move um SQL Server, todos os seus bancos de dados também são movidos.
* Gerenciador de Tráfego
* Máquinas Virtuais
* Máquinas virtuais com o certificado armazenado no cofre de chaves - Mover grupo de recursos de toonew na mesma assinatura é habilitada, mas a movimentação de assinatura cruzada não está habilitada.
* Máquinas virtuais (clássicas) - consulte [Limitações da implantação clássica](#classic-deployment-limitations)
* Conjuntos de Escala de Máquina Virtual
* Redes virtuais — atualmente, uma Rede Virtual emparelhada não pode ser movida até que o emparelhamento da rede virtual tenha sido desabilitado. Quando desabilitado, Olá rede Virtual pode ser movido com êxito e Olá emparelhamento de rede virtual pode ser habilitada. Além disso, uma rede Virtual não pode ser assinatura diferente tooa movido se Olá rede Virtual contém nenhuma sub-rede com links de navegação do recurso. Por exemplo, uma sub-rede da Rede Virtual tem um link de navegação de recurso quando um recurso redis do Cache da Microsoft for implantado nesta sub-rede.
* Gateway de VPN


## <a name="services-that-do-not-enable-move"></a>Serviços que não permitem mover
Olá serviços que atualmente não permite mover um recurso são:

* AD Domain Services
* Serviço de Integridade Híbrida do AD
* Gateway de Aplicativo
* Conjuntos de disponibilidade com Máquinas Virtuais com o Managed Disks
* Serviços do BizTalk
* Serviço de Contêiner
* ExpressRoute
* DevTest Labs - Mover grupo de recursos de toonew na mesma assinatura está habilitado, mas entre movimentação de assinatura não está habilitado.
* Dynamics LCS
* Imagens criadas no Managed Disks
* Managed Disks
* Aplicativos gerenciados
* Cofre de serviços de recuperação - também não move Olá computação, rede e armazenamento recursos associados à Olá a serviços de recuperação de cofre, consulte [limitações de serviços de recuperação](#recovery-services-limitations).
* Segurança
* Instantâneos criados no Managed Disks
* Gerenciador de Dispositivos StorSimple
* Máquinas virtuais com o Managed Disks
* Redes Virtuais (clássicas) - consulte [Limitações da implantação clássica](#classic-deployment-limitations)
* Máquinas Virtuais criadas em recursos do Marketplace — não podem ser movidas entre assinaturas. Recurso precisa toobe desprovisionada na assinatura atual hello e implantada novamente na assinatura nova Olá

## <a name="app-service-limitations"></a>Limitações do Serviço de Aplicativo
Ao trabalhar com aplicativos do Serviço de Aplicativo, você não pode mover um plano de Serviço de Aplicativo. aplicativos de serviço de aplicativo toomove, as opções são:

* Mova hello plano de serviço de aplicativo e todos os outros recursos do serviço de aplicativo em que recursos tooa novo recurso de grupo que ainda não tem recursos de serviço de aplicativo. Esse requisito significa que você deve mover mesmo Olá recursos do serviço de aplicativo que não estão associados com hello plano de serviço de aplicativo.
* Mover grupo de recursos diferente Olá aplicativos tooa, mas manter todos os planos de serviço de aplicativo no grupo de recursos original hello.

Olá plano não precisa tooreside do serviço de aplicativo hello mesmo grupo de recursos aplicativo hello para Olá aplicativo toofunction corretamente.

Por exemplo, se o grupo de recursos contém:

* **web-a** associado a **plan-a**
* **web-b** associado a **plan-b**

Suas opções são:

* Mover **web-a**, **plan-a**, **web-b** e **plan-b**
* Mover **web-a** e **web-b**
* Mover **web-a**
* Mover **web-b**

Todas as outras combinações envolvem deixar para trás um tipo de recurso que não pode ser deixado para trás ao mover um plano do Serviço de Aplicativo (qualquer tipo de recurso do Serviço de Aplicativo).

Se seu aplicativo web reside em um grupo de recursos diferente que seu plano de serviço de aplicativo, mas você deseja toomove ambos tooa novo grupo de recursos, você deve executar Olá mover em duas etapas. Por exemplo:

* **web-a** reside em **web-group**
* **plan-a** reside em **plan-group**
* Você deseja **web-a** e **um plano** tooreside na **grupo combinados**

tooaccomplish isso mover, executar duas operações de movimentação separado em Olá sequência a seguir:

1. Mover Olá **web-a** muito**grupo de plano**
2. Mover **web-a** e **um plano** muito**grupo combinados**.

Você pode mover um certificado de serviço de aplicativo tooa novo grupo de recursos ou a assinatura sem problemas. No entanto, se seu aplicativo da web inclui um certificado SSL que você adquiriu externamente e carregado toohello aplicativo, você deverá excluir o certificado de saudação antes de aplicativo de web móvel hello. Por exemplo, você pode executar Olá etapas a seguir:

1. Excluir o certificado de saudação carregado do aplicativo web de saudação
2. Mover o aplicativo web de saudação
3. Carregar o aplicativo web do hello certificado toohello

## <a name="recovery-services-limitations"></a>Limitações dos Serviços de Recuperação
Mover não está habilitado para armazenamento, rede, ou recursos de computação usada tooset a recuperação de desastres com o Azure Site Recovery.

Por exemplo, suponha que você configurou a replicação de sua conta de armazenamento local máquinas tooa (Storage1) e quiser Olá protegido máquina toocome backup após failover tooAzure como uma máquina virtual (VM1) anexado tooa de rede virtual (Network1). Não é possível mover qualquer um desses recursos do Azure - Storage1, VM1, e Network1 - em recursos grupos dentro de saudação mesma assinatura ou em assinaturas.

## <a name="hdinsight-limitations"></a>Limitações do HDInsight

Você pode mover HDInsight clusters tooa nova assinatura ou grupo de recursos. No entanto, você não pode mover entre Olá assinaturas à rede de cluster do HDInsight toohello vinculado recursos (como a rede virtual hello, NIC ou balanceador de carga). Além disso, você não pode mover o grupo de recursos novos tooa uma NIC que é anexado tooa para cluster hello.

Ao mover uma assinatura de novo de tooa do cluster HDInsight, primeiro mova outros recursos (como a conta de armazenamento Olá). Em seguida, mova o cluster do HDInsight Olá por si só.

## <a name="classic-deployment-limitations"></a>Limitações da implantação clássica
Olá a opções para mover os recursos implantados por meio do modelo clássico Olá diferem com base em se você estiver movendo recursos hello dentro de uma assinatura ou tooa nova assinatura.

### <a name="same-subscription"></a>Mesma assinatura
Ao mover os recursos do grupo de recursos de tooanother de grupo de um recurso dentro Olá a mesma assinatura, Olá restrições a seguir se aplicam:

* Redes virtuais (clássicas) não podem ser movidas.
* Máquinas virtuais (clássicas) devem ser movidas com o serviço de nuvem hello.
* Serviço de nuvem pode ser movido apenas quando mover Olá inclui todas as suas máquinas virtuais.
* Apenas um serviço de nuvem pode ser movido por vez.
* Apenas uma conta de armazenamento (clássica) pode ser movida por vez.
* Conta de armazenamento (clássico) não pode ser movida em Olá mesma operação com uma máquina virtual ou um serviço de nuvem.

toomove recursos clássicos tooa novo grupo de recursos dentro Olá a mesma assinatura, use operações de movimentação padrão Olá por meio de saudação [portal](#use-portal), [Azure PowerShell](#use-powershell), [CLI do Azure](#use-azure-cli), ou [API REST](#use-rest-api). Você usa Olá mesmas operações que você usa para mover os recursos do Gerenciador de recursos.

### <a name="new-subscription"></a>Nova assinatura
Ao mover a nova assinatura de recursos de tooa, Olá restrições a seguir se aplicam:

* Todos os recursos clássicos na assinatura Olá devem ser movidos no hello mesma operação.
* assinatura de destino Olá não deve conter todos os outros recursos clássicos.
* Olá move pode ser solicitado somente por meio de uma API REST separado para move clássico. comandos de movimentação do Gerenciador de recursos padrão Olá não funcionam quando mover recursos clássicos tooa nova assinatura.

toomove recursos clássicos tooa nova assinatura, use Olá REST operações recursos tooclassic específico. toouse REST, execute Olá etapas a seguir:

1. Verifique se a assinatura de origem Olá pode participar de uma assinatura entre mover. Use Olá operação a seguir:

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     No corpo da solicitação de hello, incluem:

  ```json
  {
    "role": "source"
  }
  ```

     resposta de saudação para operação de validação hello está no hello formato a seguir:

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. Verifique se a assinatura de destino Olá pode participar de uma assinatura cruzada mover. Use Olá operação a seguir:

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     No corpo da solicitação de hello, incluem:

  ```json
  {
    "role": "target"
  }
  ```

     resposta de saudação está no hello mesmo formato que a validação de assinatura de origem hello.
3. Se as duas assinaturas passarem na validação, mova todos os recursos clássicos de assinatura de tooanother de uma assinatura com hello operação a seguir:

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    No corpo da solicitação de hello, incluem:

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

operação de saudação pode ser executada por vários minutos.

## <a name="use-portal"></a>Usar o portal
toomove recursos, selecione grupo de recursos de saudação contendo esses recursos e selecione Olá **mover** botão.

![Mover recursos](./media/resource-group-move-resources/select-move.png)

Selecione se você estiver movendo Olá recursos tooa novo grupo de recursos ou uma nova assinatura.

Selecione Olá recursos toomove e o grupo de recursos de destino de saudação. Confirmar que você precisa tooupdate scripts para esses recursos e selecione **Okey**. Se você selecionou o ícone de assinatura de edição de saudação na etapa anterior Olá, você também deve selecionar a assinatura de destino hello.

![selecionar destino](./media/resource-group-move-resources/select-destination.png)

Em **notificações**, você verá que Olá mover a operação está em execução.

![mostrar status da movimentação](./media/resource-group-move-resources/show-status.png)

Quando ele for concluído, você será notificado de resultado de saudação.

![mostrar resultado da movimentação](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a>Usar o PowerShell
toomove existente grupo de recursos tooanother de recursos ou assinatura, use Olá `Move-AzureRmResource` comando.

Olá primeiro exemplo mostra como toomove um recurso tooa novo grupo de recursos.

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

Olá segundo exemplo mostra como toomove vários recursos tooa novo grupo de recursos.

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

toomove tooa nova assinatura, inclua um valor para Olá `DestinationSubscriptionId` parâmetro.

Você será solicitado tooconfirm que você deseja toomove Olá especificado recursos.

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a>Usar a CLI 2.0 do Azure
toomove existente grupo de recursos tooanother de recursos ou assinatura, use Olá `az resource move` comando. Fornece recursos Olá IDs de saudação recursos toomove. Você pode obter IDs de recurso com hello comando a seguir:

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

saudação de exemplo a seguir mostra como a conta toomove um armazenamento tooa novo grupo de recursos. Em Olá `--ids` parâmetro, forneça uma lista separada de saudação toomove de IDs de recurso.

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

toomove tooa nova assinatura, forneça Olá `--destination-subscription-id` parâmetro.

## <a name="use-azure-cli-10"></a>Usar a CLI do Azure 1.0
toomove existente grupo de recursos tooanother de recursos ou assinatura, use Olá `azure resource move` comando. Fornece recursos Olá IDs de saudação recursos toomove. Você pode obter IDs de recurso com hello comando a seguir:

```azurecli
azure resource list -g sourceGroup --json
```

Que retorna Olá formato a seguir:

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

saudação de exemplo a seguir mostra como a conta toomove um armazenamento tooa novo grupo de recursos. Em Olá `-i` parâmetro, fornecer uma lista separada por vírgulas de saudação toomove de IDs de recurso.

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

Você será solicitado tooconfirm que você deseja toomove Olá o recurso especificado.

## <a name="use-rest-api"></a>Usar a API REST
grupo de recursos para toomove existente recursos tooanother ou assinatura, execute:

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

No corpo da solicitação de Olá, especifique o grupo de recursos de destino hello e Olá recursos toomove. Para obter mais informações sobre a operação de REST de movimentação hello, consulte [mover recursos](https://msdn.microsoft.com/library/azure/mt218710.aspx).

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre cmdlets do PowerShell para gerenciar sua assinatura, consulte [usando o PowerShell do Azure com o Gerenciador de recursos](powershell-azure-resource-manager.md).
* toolearn sobre comandos de CLI do Azure para gerenciar sua assinatura, consulte [hello usando a CLI do Azure com o Gerenciador de recursos](xplat-cli-azure-resource-manager.md).
* toolearn sobre recursos do portal para gerenciar sua assinatura, consulte [usando os recursos do Azure toomanage portal Olá](resource-group-portal.md).
* toolearn sobre a aplicação de recursos de tooyour uma organização lógica, consulte [usando marcas tooorganize seus recursos](resource-group-using-tags.md).
