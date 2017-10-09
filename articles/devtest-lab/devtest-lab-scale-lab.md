---
title: "aaaScale cotas e limites de seu laboratório no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como tooscale um laboratório no Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="9012a-103">Dimensionar cotas e limites no DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="9012a-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="9012a-104">Enquanto você trabalha no DevTest Labs, talvez Observe que há certa toosome de limites padrão recursos do Azure, o que podem afetar o serviço do DevTest Labs hello.</span><span class="sxs-lookup"><span data-stu-id="9012a-104">As you work in DevTest Labs, you might notice that there are certain default limits toosome Azure resources, which can affect hello DevTest Labs service.</span></span> <span data-ttu-id="9012a-105">Esses limites são chamados tooas **cotas**.</span><span class="sxs-lookup"><span data-stu-id="9012a-105">These limits are referred tooas **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="9012a-106">Olá serviço DevTest Labs não impor cotas.</span><span class="sxs-lookup"><span data-stu-id="9012a-106">hello DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="9012a-107">As cotas que podem ser encontrados são restrições de padrão de saudação assinatura geral do Azure.</span><span class="sxs-lookup"><span data-stu-id="9012a-107">Any quotas you might encounter are default constraints of hello overall Azure subscription.</span></span>

<span data-ttu-id="9012a-108">Você pode usar cada recurso do Azure até atingir sua cota.</span><span class="sxs-lookup"><span data-stu-id="9012a-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="9012a-109">Cada assinatura tem cotas separadas e seu uso é controlado por assinatura.</span><span class="sxs-lookup"><span data-stu-id="9012a-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="9012a-110">Por exemplo, cada assinatura tem uma cota padrão de 20 núcleos.</span><span class="sxs-lookup"><span data-stu-id="9012a-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="9012a-111">Portanto, se você estiver criando VMs em seu laboratório com quatro núcleos cada, você poderá criar apenas cinco VMs.</span><span class="sxs-lookup"><span data-stu-id="9012a-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="9012a-112">[Azure assinatura e limites de serviço](https://docs.microsoft.com/azure/azure-subscription-service-limits) lista algumas das cotas de hello mais comuns para recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9012a-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of hello most common quotas for Azure resources.</span></span> <span data-ttu-id="9012a-113">Olá recursos mais comumente usados em um laboratório e para que você pode encontrar cotas, incluir núcleos VM, endereços IP públicos, interface de rede, discos gerenciados, atribuição de função RBAC e circuitos do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9012a-113">hello resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="9012a-114">Exibir seu uso e cotas</span><span class="sxs-lookup"><span data-stu-id="9012a-114">View your usage and quotas</span></span>
<span data-ttu-id="9012a-115">Estas etapas mostram como tooview Olá cotas atuais em sua assinatura para recursos específicos do Azure e toosee o percentual de cada cota que você usou.</span><span class="sxs-lookup"><span data-stu-id="9012a-115">These steps show you how tooview hello current quotas in your subscription for specific Azure resources, and toosee what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="9012a-116">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="9012a-116">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="9012a-117">Selecione **mais serviços**e, em seguida, selecione **cobrança** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="9012a-117">Select **More Services**, and then select **Billing** from hello list.</span></span>
1. <span data-ttu-id="9012a-118">Na folha de cobrança hello, selecione uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="9012a-118">In hello Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="9012a-119">Selecione **Uso + cotas**.</span><span class="sxs-lookup"><span data-stu-id="9012a-119">Select **Usage + quotas**.</span></span>

   ![Botão Uso e cotas](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="9012a-121">Olá uso + cotas folha é exibida, listando os diferentes recursos disponíveis nessa porcentagem de assinatura e hello da cota de saudação que está sendo usada por recurso.</span><span class="sxs-lookup"><span data-stu-id="9012a-121">hello Usage + quotas blade appears, listing different resources available in that subscription and hello percentage of hello quota that is being used per resource.</span></span>

   ![Cotas e uso](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="9012a-123">Solicitar mais recursos na sua assinatura</span><span class="sxs-lookup"><span data-stu-id="9012a-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="9012a-124">Se você atingir um limite de cota, o limite padrão de saudação de um recurso em uma assinatura pode ser aumentado o limite máximo de tooa, conforme descrito em [assinatura do Azure e limites de serviço](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="9012a-124">If you reach a quota cap, hello default limit of a resource in a subscription can be increased up tooa maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="9012a-125">Estas etapas mostram como toorequest uma cota de aumentar a saudação [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="9012a-125">These steps show you how toorequest a quota increase through hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="9012a-126">Selecione **Mais Serviços**, selecione **Cobrança** e, em seguida, selecione **Uso + cotas**.</span><span class="sxs-lookup"><span data-stu-id="9012a-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="9012a-127">No uso de saudação + folha de cotas, selecione Olá **solicitar aumentar** botão.</span><span class="sxs-lookup"><span data-stu-id="9012a-127">In hello Usage + quotas blade, select hello **Request Increase** button.</span></span>

   ![Botão Solicitar aumento](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="9012a-129">toocomplete e enviar solicitação de hello, preencha as informações de saudação necessária em todas as três guias de saudação **nova solicitação de suporte** formulário.</span><span class="sxs-lookup"><span data-stu-id="9012a-129">toocomplete and submit hello request, fill out hello required information on all three tabs of hello **New support request** form.</span></span>

   ![Formulário de solicitação de aumento](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="9012a-131">[Noções básicas sobre os limites do Azure e aumenta](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) fornece mais informações sobre como entrar em contato com o suporte do Azure toorequest uma cota de aumento.</span><span class="sxs-lookup"><span data-stu-id="9012a-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support toorequest a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="9012a-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9012a-132">Next steps</span></span>
* <span data-ttu-id="9012a-133">Explorar Olá [Galeria de modelos do DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="9012a-133">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
