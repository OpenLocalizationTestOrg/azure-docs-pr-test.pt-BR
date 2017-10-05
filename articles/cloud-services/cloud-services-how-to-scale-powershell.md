---
title: "Dimensionar um serviço de nuvem do Azure no Windows PowerShell | Microsoft Docs"
description: "(clássico) Aprenda a usar o PowerShell para escalar ou reduzir horizontalmente uma função Web ou função de trabalho no Azure."
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
ms.openlocfilehash: a7ae8ff202d403dff19b8c9a6a09492235db27ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-a-cloud-service-in-powershell"></a><span data-ttu-id="f235c-103">Como escalar um serviço de nuvem no PowerShell</span><span class="sxs-lookup"><span data-stu-id="f235c-103">How to scale a cloud service in PowerShell</span></span>

<span data-ttu-id="f235c-104">Você pode usar o Windows PowerShell para escalar ou reduzir uma função Web ou função de trabalho adicionando ou removendo instâncias.</span><span class="sxs-lookup"><span data-stu-id="f235c-104">You can use Windows PowerShell to scale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-to-azure"></a><span data-ttu-id="f235c-105">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="f235c-105">Log in to Azure</span></span>

<span data-ttu-id="f235c-106">Antes de executar qualquer operação na sua assinatura por meio do PowerShell, você deve fazer logon:</span><span class="sxs-lookup"><span data-stu-id="f235c-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="f235c-107">Se você tiver várias assinaturas associadas à sua conta, você precisará alterar a assinatura atual dependendo de onde reside o seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="f235c-107">If you have multiple subscriptions associated with your account, you may need to change the current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="f235c-108">Para verificar a assinatura atual, execute:</span><span class="sxs-lookup"><span data-stu-id="f235c-108">To check the current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="f235c-109">Se você precisar alterar a assinatura atual, execute:</span><span class="sxs-lookup"><span data-stu-id="f235c-109">If you need to change the current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-the-current-instance-count-for-your-role"></a><span data-ttu-id="f235c-110">Verificar a contagem de instâncias atual da sua função</span><span class="sxs-lookup"><span data-stu-id="f235c-110">Check the current instance count for your role</span></span>

<span data-ttu-id="f235c-111">Para verificar o estado atual da sua função, execute:</span><span class="sxs-lookup"><span data-stu-id="f235c-111">To check the current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="f235c-112">Você deve receber informações sobre a função, incluindo sua versão de sistema operacional atual e contagem de instância atuais.</span><span class="sxs-lookup"><span data-stu-id="f235c-112">You should get back information about the role, including its current OS version and instance count.</span></span> <span data-ttu-id="f235c-113">Nesse caso, a função tem uma única instância.</span><span class="sxs-lookup"><span data-stu-id="f235c-113">In this case, the role has a single instance.</span></span>

![Informações sobre a função](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-the-role-by-adding-more-instances"></a><span data-ttu-id="f235c-115">Escalar horizontalmente a função adicionando mais instâncias</span><span class="sxs-lookup"><span data-stu-id="f235c-115">Scale out the role by adding more instances</span></span>

<span data-ttu-id="f235c-116">Para escalar horizontalmente sua função, passe o número desejado de instâncias como o parâmetro **Contagem** do cmdlet **Set-AzureRole**:</span><span class="sxs-lookup"><span data-stu-id="f235c-116">To scale out your role, pass the desired number of instances as the **Count** parameter to the **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="f235c-117">Os cmdlet é bloqueado momentaneamente enquanto as novas instâncias são provisionadas e iniciadas.</span><span class="sxs-lookup"><span data-stu-id="f235c-117">The cmdlet blocks momentarily while the new instances are provisioned and started.</span></span> <span data-ttu-id="f235c-118">Nesse momento, se você abrir uma nova janela do PowerShell e chamar **Get-AzureRole** conforme mostrado anteriormente, verá a nova contagem de instância de destino.</span><span class="sxs-lookup"><span data-stu-id="f235c-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see the new target instance count.</span></span> <span data-ttu-id="f235c-119">E se você inspecionar o status da função no portal, deverá ver a nova instância de sendo inicializada:</span><span class="sxs-lookup"><span data-stu-id="f235c-119">And if you inspect the role status in the portal, you should see the new instance starting up:</span></span>

![Instância VM aberta no portal](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="f235c-121">Depois que as novas instâncias forem iniciadas, o cmdlet as retornará com êxito:</span><span class="sxs-lookup"><span data-stu-id="f235c-121">Once the new instances have started, the cmdlet will return successfully:</span></span>

![Aumentar o êxito da instância de função](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-the-role-by-removing-instances"></a><span data-ttu-id="f235c-123">Reduzir horizontalmente a função removendo instâncias</span><span class="sxs-lookup"><span data-stu-id="f235c-123">Scale in the role by removing instances</span></span>

<span data-ttu-id="f235c-124">Você pode reduzir horizontalmente uma função removendo instâncias da mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="f235c-124">You can scale in a role by removing instances in the same way.</span></span> <span data-ttu-id="f235c-125">Defina o parâmetro **Contagem** em **Set-AzureRole** para o número de instâncias que você deseja ter após a conclusão da operação de redução horizontal.</span><span class="sxs-lookup"><span data-stu-id="f235c-125">Set the **Count** parameter on **Set-AzureRole** to the number of instances you want to have after the scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f235c-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f235c-126">Next steps</span></span>

<span data-ttu-id="f235c-127">Não é possível configurar o dimensionamento automático para serviços de nuvem do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f235c-127">It is not possible to configure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="f235c-128">Para fazer isso, veja [Como dimensionar automaticamente um serviço de nuvem](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f235c-128">To do that, see [How to auto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
