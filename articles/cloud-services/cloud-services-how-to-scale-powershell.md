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
# <a name="how-tooscale-a-cloud-service-in-powershell"></a><span data-ttu-id="de4cb-103">Como tooscale uma nuvem de serviço no PowerShell</span><span class="sxs-lookup"><span data-stu-id="de4cb-103">How tooscale a cloud service in PowerShell</span></span>

<span data-ttu-id="de4cb-104">Você pode usar o Windows PowerShell tooscale uma função web ou função de trabalho ou adicionando ou removendo instâncias.</span><span class="sxs-lookup"><span data-stu-id="de4cb-104">You can use Windows PowerShell tooscale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-tooazure"></a><span data-ttu-id="de4cb-105">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="de4cb-105">Log in tooAzure</span></span>

<span data-ttu-id="de4cb-106">Antes de executar qualquer operação na sua assinatura por meio do PowerShell, você deve fazer logon:</span><span class="sxs-lookup"><span data-stu-id="de4cb-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="de4cb-107">Se você tiver várias assinaturas associadas à sua conta, talvez seja necessário toochange Olá assinatura dependendo de onde reside o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="de4cb-107">If you have multiple subscriptions associated with your account, you may need toochange hello current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="de4cb-108">toocheck Olá assinatura atual, execute:</span><span class="sxs-lookup"><span data-stu-id="de4cb-108">toocheck hello current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="de4cb-109">Se você precisar de assinatura atual do toochange hello, execute:</span><span class="sxs-lookup"><span data-stu-id="de4cb-109">If you need toochange hello current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a><span data-ttu-id="de4cb-110">Verifique a contagem atual de instâncias Olá para sua função</span><span class="sxs-lookup"><span data-stu-id="de4cb-110">Check hello current instance count for your role</span></span>

<span data-ttu-id="de4cb-111">estado atual do hello toocheck de sua função, execute:</span><span class="sxs-lookup"><span data-stu-id="de4cb-111">toocheck hello current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="de4cb-112">Você deve obter novamente obter informações sobre a função hello, incluindo sua contagem de versão e a instância de sistema operacional atual.</span><span class="sxs-lookup"><span data-stu-id="de4cb-112">You should get back information about hello role, including its current OS version and instance count.</span></span> <span data-ttu-id="de4cb-113">Nesse caso, a função hello tem uma única instância.</span><span class="sxs-lookup"><span data-stu-id="de4cb-113">In this case, hello role has a single instance.</span></span>

![Informações sobre a função hello](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a><span data-ttu-id="de4cb-115">Expansão de função hello adicionando mais instâncias</span><span class="sxs-lookup"><span data-stu-id="de4cb-115">Scale out hello role by adding more instances</span></span>

<span data-ttu-id="de4cb-116">tooscale sua função, passe Olá desejado número de instâncias como Olá **contagem** parâmetro toohello **Set-AzureRole** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="de4cb-116">tooscale out your role, pass hello desired number of instances as hello **Count** parameter toohello **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="de4cb-117">blocos de cmdlet Olá momentaneamente ao novas instâncias de saudação são provisionados e iniciados.</span><span class="sxs-lookup"><span data-stu-id="de4cb-117">hello cmdlet blocks momentarily while hello new instances are provisioned and started.</span></span> <span data-ttu-id="de4cb-118">Durante esse tempo, se você abrir uma nova janela do PowerShell e chamada **Get-AzureRole** conforme mostrado anteriormente, você verá a nova contagem de instância de destino hello.</span><span class="sxs-lookup"><span data-stu-id="de4cb-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see hello new target instance count.</span></span> <span data-ttu-id="de4cb-119">E se você inspecionar o status da função hello no portal de saudação, você deverá ver iniciar nova instância de saudação:</span><span class="sxs-lookup"><span data-stu-id="de4cb-119">And if you inspect hello role status in hello portal, you should see hello new instance starting up:</span></span>

![Instância VM aberta no portal](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="de4cb-121">Depois de tem iniciado novas instâncias de saudação, Olá cmdlet retornará com êxito:</span><span class="sxs-lookup"><span data-stu-id="de4cb-121">Once hello new instances have started, hello cmdlet will return successfully:</span></span>

![Aumentar o êxito da instância de função](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a><span data-ttu-id="de4cb-123">Instâncias de escala na função hello, removendo</span><span class="sxs-lookup"><span data-stu-id="de4cb-123">Scale in hello role by removing instances</span></span>

<span data-ttu-id="de4cb-124">Você pode dimensionar em uma função, Removendo instâncias Olá mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="de4cb-124">You can scale in a role by removing instances in hello same way.</span></span> <span data-ttu-id="de4cb-125">Olá conjunto **contagem** parâmetro em **Set-AzureRole** toohello número de instâncias que você deseja toohave após a conclusão da escala de saudação em operação.</span><span class="sxs-lookup"><span data-stu-id="de4cb-125">Set hello **Count** parameter on **Set-AzureRole** toohello number of instances you want toohave after hello scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de4cb-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="de4cb-126">Next steps</span></span>

<span data-ttu-id="de4cb-127">Não é possível tooconfigure-AutoEscala para serviços de nuvem do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de4cb-127">It is not possible tooconfigure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="de4cb-128">toodo que, consulte [como tooauto dimensionar um serviço de nuvem](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="de4cb-128">toodo that, see [How tooauto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
