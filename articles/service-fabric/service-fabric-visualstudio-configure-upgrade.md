---
title: "atualização de saudação aaaConfigure de um aplicativo de malha do serviço | Microsoft Docs"
description: "Saiba como tooconfigure Olá configurações para atualizar um aplicativo de malha do serviço usando o Microsoft Visual Studio."
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a>Configurar a atualização de saudação de um aplicativo de malha do serviço no Visual Studio
Visual Studio tools para o Azure Service Fabric oferecem suporte à atualização para publicação toolocal ou clusters remotos. Há três cenários em que você deseja tooupgrade sua versão mais recente do aplicativo tooa em vez de substituir o aplicativo hello durante o teste e depuração:

* Dados de aplicativo não serão perdidos durante a atualização de saudação.
* Disponibilidade permanece alta para não haver qualquer interrupção do serviço durante a atualização de hello, se houver que instâncias suficientes serviço espalham em domínios de atualização.
* Os testes podem ser executados em um aplicativo enquanto ele está sendo atualizado.

## <a name="parameters-needed-tooupgrade"></a>Parâmetros necessários tooupgrade
Você pode escolher entre dois tipos de implantação: normal ou atualização. Uma implantação regular apaga quaisquer informações de implantação anterior e os dados no cluster hello, enquanto preserva a ele uma implantação de atualização. Quando você atualizar um aplicativo de malha do serviço no Visual Studio, você precisa parâmetros de atualização de aplicativo tooprovide e políticas de verificação de integridade. Atualização do aplicativo parâmetros ajudam a controlar a atualização de hello, enquanto as políticas de verificação de integridade determinam se a atualização de saudação foi bem-sucedida. Veja [Atualização do aplicativo Service Fabric: atualizar parâmetros](service-fabric-application-upgrade-parameters.md) para obter mais detalhes.

Existem três modos de atualização: *Monitored*, *UnmonitoredAuto* e *UnmonitoredManual*.

* Uma atualização monitorado automatiza a atualização hello e aplicativo verificação de integridade.
* Uma atualização UnmonitoredAuto automatiza a atualização hello, mas ignora Olá verificação de integridade do aplicativo.
* Quando você faz uma atualização UnmonitoredManual, você precisa toomanually atualizar cada domínio de atualização.

Cada modo de atualização requer diferentes conjuntos de parâmetros. Consulte [parâmetros de atualização de aplicativo](service-fabric-application-upgrade-parameters.md) toolearn mais sobre as opções de atualização disponíveis hello.

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a>Atualizar um aplicativo do Service Fabric no Visual Studio
Se você estiver usando saudação do Visual Studio Service Fabric ferramentas tooupgrade um aplicativo de malha do serviço, você pode especificar uma atualização em vez de uma implantação regular um toobe do processo de publicação, verificando Olá **atualizar o aplicativo hello** verificar caixa.

### <a name="tooconfigure-hello-upgrade-parameters"></a>parâmetros de atualização de saudação tooconfigure
1. Clique em Olá **configurações** caixa de seleção do botão próxima toohello. Olá **Editar parâmetros de atualização** caixa de diálogo é exibida. Olá **Editar parâmetros de atualização** caixa de diálogo oferece suporte a modos de atualização monitorado, UnmonitoredAuto e UnmonitoredManual hello.
2. Selecione o modo de atualização de Olá que você deseja toouse e, em seguida, preencha a grade de parâmetro hello.

    Cada parâmetro tem valores padrão. Olá parâmetro opcional *DefaultServiceTypeHealthPolicy* utiliza uma entrada da tabela de hash. Aqui está um exemplo de formato de tabela entrada de hash Olá para *DefaultServiceTypeHealthPolicy*:

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    *ServiceTypeHealthPolicyMap* é outro parâmetro opcional que usa uma entrada de tabela de hash no hello formato a seguir:

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    Aqui está um exemplo da vida real:

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. Se você selecionar o modo de atualização UnmonitoredManual, manualmente deve iniciar um toocontinue do console do PowerShell e concluir o processo de atualização de saudação. Consulte também[atualização do aplicativo do Service Fabric: tópicos avançados](service-fabric-application-upgrade-advanced.md) toolearn manual como atualizar funciona.

## <a name="upgrade-an-application-by-using-powershell"></a>Atualizar um aplicativo usando o PowerShell
Você pode usar o PowerShell cmdlets tooupgrade um aplicativo de malha do serviço. Confira [Tutorial da atualização de aplicativos do Service Fabric](service-fabric-application-upgrade-tutorial.md) e [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) para obter informações detalhadas.

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a>Especificar uma política de verificação de integridade no arquivo de manifesto de aplicativo hello
Cada serviço em um aplicativo de malha do serviço pode ter seus próprios parâmetros de política de integridade que substituem os valores padrão de saudação. Você pode fornecer esses valores de parâmetro no arquivo de manifesto de aplicativo hello.

Olá exemplo a seguir mostra como verificar a diretiva de para cada serviço no manifesto de aplicativo hello tooapply exclusivos de integridade.

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre como implantar um aplicativo, confira [Implantar um aplicativo existente no Service Fabric do Azure](service-fabric-deploy-existing-app.md).