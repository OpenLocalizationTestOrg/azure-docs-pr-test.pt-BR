---
title: "aaaScale um serviço de nuvem do Azure no Windows PowerShell | Microsoft Docs"
description: "(clássico) Saiba como toouse PowerShell tooscale uma função web ou função de trabalho no ou no Azure."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a>Como tooscale uma nuvem de serviço no PowerShell

Você pode usar o Windows PowerShell tooscale uma função web ou função de trabalho ou adicionando ou removendo instâncias.  

## <a name="log-in-tooazure"></a>Faça logon no tooAzure

Antes de executar qualquer operação na sua assinatura por meio do PowerShell, você deve fazer logon:

```powershell
Add-AzureAccount
```

Se você tiver várias assinaturas associadas à sua conta, talvez seja necessário toochange Olá assinatura dependendo de onde reside o serviço de nuvem. toocheck Olá assinatura atual, execute:

```powershell
Get-AzureSubscription -Current
```

Se você precisar de assinatura atual do toochange hello, execute:

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a>Verifique a contagem atual de instâncias Olá para sua função

estado atual do hello toocheck de sua função, execute:

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

Você deve obter novamente obter informações sobre a função hello, incluindo sua contagem de versão e a instância de sistema operacional atual. Nesse caso, a função hello tem uma única instância.

![Informações sobre a função hello](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a>Expansão de função hello adicionando mais instâncias

tooscale sua função, passe Olá desejado número de instâncias como Olá **contagem** parâmetro toohello **Set-AzureRole** cmdlet:

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

blocos de cmdlet Olá momentaneamente ao novas instâncias de saudação são provisionados e iniciados. Durante esse tempo, se você abrir uma nova janela do PowerShell e chamada **Get-AzureRole** conforme mostrado anteriormente, você verá a nova contagem de instância de destino hello. E se você inspecionar o status da função hello no portal de saudação, você deverá ver iniciar nova instância de saudação:

![Instância VM aberta no portal](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

Depois de tem iniciado novas instâncias de saudação, Olá cmdlet retornará com êxito:

![Aumentar o êxito da instância de função](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a>Instâncias de escala na função hello, removendo

Você pode dimensionar em uma função, Removendo instâncias Olá mesma maneira. Olá conjunto **contagem** parâmetro em **Set-AzureRole** toohello número de instâncias que você deseja toohave após a conclusão da escala de saudação em operação.

## <a name="next-steps"></a>Próximas etapas

Não é possível tooconfigure-AutoEscala para serviços de nuvem do PowerShell. toodo que, consulte [como tooauto dimensionar um serviço de nuvem](cloud-services-how-to-scale-portal.md).
