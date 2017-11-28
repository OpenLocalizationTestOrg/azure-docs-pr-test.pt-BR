---
title: aaaProtect sua API com gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como tooprotect sua API com cotas e políticas (limite de taxa) de limitação."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="19fd2-103">Proteja sua API com limites de taxa usando o Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="19fd2-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="19fd2-104">Este guia mostra como é fácil tooadd proteção para a API de back-end, configurando políticas de cota e de limite de taxa ao gerenciamento de API do Azure.</span><span class="sxs-lookup"><span data-stu-id="19fd2-104">This guide shows you how easy it is tooadd protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="19fd2-105">Neste tutorial, você criará um produto de "Avaliação gratuita" API que permite aos desenvolvedores toomake too10 chamadas por minuto e backup tooa máximo de 200 chamadas por semana tooyour API usando Olá [limitar a taxa de chamada por assinatura](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) e [ Definir a cota de uso por assinatura](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) políticas.</span><span class="sxs-lookup"><span data-stu-id="19fd2-105">In this tutorial, you will create a "Free Trial" API product that allows developers toomake up too10 calls per minute and up tooa maximum of 200 calls per week tooyour API using hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="19fd2-106">Você, em seguida, publicar Olá API e testar a política de limite de taxa de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-106">You will then publish hello API and test hello rate limit policy.</span></span>

<span data-ttu-id="19fd2-107">Para mais avançados limitação cenários usando Olá [taxa limite por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) e [cota por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) políticas, consulte [solicitação avançada de limitação com gerenciamento de API do Azure](api-management-sample-flexible-throttling.md).</span><span class="sxs-lookup"><span data-stu-id="19fd2-107">For more advanced throttling scenarios using hello [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="19fd2-108"><a name="create-product"></a>toocreate um produto</span><span class="sxs-lookup"><span data-stu-id="19fd2-108"><a name="create-product"> </a>toocreate a product</span></span>
<span data-ttu-id="19fd2-109">Nesta etapa você criará um produto de avaliação gratuita que não requer aprovação de assinatura.</span><span class="sxs-lookup"><span data-stu-id="19fd2-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="19fd2-110">Se você já tiver um produto configurado e deseja toouse-la para este tutorial, você pode pular muito[configurar políticas de cota e de limite de taxa de chamada] [ Configure call rate limit and quota policies] e siga o tutorial hello a partir daí, usando o produto em vez de produto de avaliação gratuita de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-110">If you already have a product configured and want toouse it for this tutorial, you can jump ahead too[Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow hello tutorial from there using your product in place of hello Free Trial product.</span></span>
> 
> 

<span data-ttu-id="19fd2-111">tooget iniciado, clique em **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="19fd2-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal do editor][api-management-management-console]

> <span data-ttu-id="19fd2-113">Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [gerenciar sua primeira API no gerenciamento de API do Azure] [ Manage your first API in Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="19fd2-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="19fd2-114">Clique em **produtos** em Olá **gerenciamento de API** menu Olá toodisplay esquerdo Olá **produtos** página.</span><span class="sxs-lookup"><span data-stu-id="19fd2-114">Click **Products** in hello **API Management** menu on hello left toodisplay hello **Products** page.</span></span>

![Adicionar produto][api-management-add-product]

<span data-ttu-id="19fd2-116">Clique em **adicionar produto** toodisplay Olá **adicionar novo produto** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="19fd2-116">Click **Add product** toodisplay hello **Add new product** dialog box.</span></span>

![Adicionar novo produto][api-management-new-product-window]

<span data-ttu-id="19fd2-118">Em Olá **título** , digite **avaliação gratuita**.</span><span class="sxs-lookup"><span data-stu-id="19fd2-118">In hello **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="19fd2-119">Em Olá **descrição** caixa, Olá tipo texto a seguir: **assinantes será capaz de toorun 10 chamadas por minuto backup tooa máximo de 200 chamadas/semana após o qual o acesso é negado.**</span><span class="sxs-lookup"><span data-stu-id="19fd2-119">In hello **Description** box, type hello following text: **Subscribers will be able toorun 10 calls/minute up tooa maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="19fd2-120">Os produtos de Gerenciamento de API podem ser protegidos ou abertos.</span><span class="sxs-lookup"><span data-stu-id="19fd2-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="19fd2-121">Produtos protegidos devem ser toobefore inscrito, eles podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="19fd2-121">Protected products must be subscribed toobefore they can be used.</span></span> <span data-ttu-id="19fd2-122">Os produtos abertos podem ser usados sem uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="19fd2-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="19fd2-123">Certifique-se de que **exigir assinatura** é toocreate selecionado um produto protegido que requer uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="19fd2-123">Ensure that **Require subscription** is selected toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="19fd2-124">Essa é a configuração de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-124">This is hello default setting.</span></span>

<span data-ttu-id="19fd2-125">Se você deseja que um administrador tooreview e aceitar ou rejeitar assinatura tentativas toothis produto, selecione **exigirem a aprovação de assinatura**.</span><span class="sxs-lookup"><span data-stu-id="19fd2-125">If you want an administrator tooreview and accept or reject subscription attempts toothis product, select **Require subscription approval**.</span></span> <span data-ttu-id="19fd2-126">Se a caixa de seleção de saudação não estiver selecionada, tentativas de assinatura serão aprovadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="19fd2-126">If hello check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="19fd2-127">Neste exemplo, as assinaturas são automaticamente aprovadas, portanto, não marque a caixa de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-127">In this example, subscriptions are automatically approved, so do not select hello box.</span></span>

<span data-ttu-id="19fd2-128">contas de desenvolvedor tooallow toosubscribe várias vezes toohello novo produto, selecione Olá **permitir várias inscrições simultâneas** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="19fd2-128">tooallow developer accounts toosubscribe multiple times toohello new product, select hello **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="19fd2-129">Este tópico não utiliza várias inscrições simultâneas, por isso deixe-o desmarcado.</span><span class="sxs-lookup"><span data-stu-id="19fd2-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="19fd2-130">Depois que todos os valores são inseridos, clique em **salvar** toocreate produto de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-130">After all values are entered, click **Save** toocreate hello product.</span></span>

![Produto adicionado][api-management-product-added]

<span data-ttu-id="19fd2-132">Por padrão, novos produtos são visíveis toousers em Olá **administradores** grupo.</span><span class="sxs-lookup"><span data-stu-id="19fd2-132">By default, new products are visible toousers in hello **Administrators** group.</span></span> <span data-ttu-id="19fd2-133">Vamos Olá tooadd **desenvolvedores** grupo.</span><span class="sxs-lookup"><span data-stu-id="19fd2-133">We are going tooadd hello **Developers** group.</span></span> <span data-ttu-id="19fd2-134">Clique em **avaliação gratuita**e, em seguida, clique em Olá **visibilidade** guia.</span><span class="sxs-lookup"><span data-stu-id="19fd2-134">Click **Free Trial**, and then click hello **Visibility** tab.</span></span>

> <span data-ttu-id="19fd2-135">No gerenciamento de API, os grupos são usados toomanage Olá visibilidade de produtos toodevelopers.</span><span class="sxs-lookup"><span data-stu-id="19fd2-135">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="19fd2-136">Produtos conceder toogroups de visibilidade, e os desenvolvedores podem exibir e assinar toohello produtos que são grupos de toohello visíveis no qual eles pertencem.</span><span class="sxs-lookup"><span data-stu-id="19fd2-136">Products grant visibility toogroups, and developers can view and subscribe toohello products that are visible toohello groups in which they belong.</span></span> <span data-ttu-id="19fd2-137">Para obter mais informações, consulte [como toocreate e use os grupos no gerenciamento de API do Azure][How toocreate and use groups in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="19fd2-137">For more information, see [How toocreate and use groups in Azure API Management][How toocreate and use groups in Azure API Management].</span></span>
> 
> 

![Adicionar um grupo de desenvolvedores][api-management-add-developers-group]

<span data-ttu-id="19fd2-139">Selecione Olá **desenvolvedores** caixa de seleção e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="19fd2-139">Select hello **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="19fd2-140"><a name="add-api"></a>tooadd uma API toohello produto</span><span class="sxs-lookup"><span data-stu-id="19fd2-140"><a name="add-api"> </a>tooadd an API toohello product</span></span>
<span data-ttu-id="19fd2-141">Nesta etapa do tutorial Olá, vamos adicionar Olá Echo toohello nova avaliação gratuita produto da API.</span><span class="sxs-lookup"><span data-stu-id="19fd2-141">In this step of hello tutorial, we will add hello Echo API toohello new Free Trial product.</span></span>

> <span data-ttu-id="19fd2-142">Cada instância de serviço de gerenciamento de API vem pré-configurada com uma API de eco que podem ser usado tooexperiment com e saiba mais sobre o gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="19fd2-142">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="19fd2-143">Para saber mais, confira [Gerenciar sua primeira API no Gerenciamento de API do Azure][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="19fd2-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="19fd2-144">Clique em **produtos** de saudação **gerenciamento de API** menu saudação à esquerda e clique **avaliação gratuita** tooconfigure produto de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-144">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Configurar produto][api-management-configure-product]

<span data-ttu-id="19fd2-146">Clique em **tooproduct adicionar API**.</span><span class="sxs-lookup"><span data-stu-id="19fd2-146">Click **Add API tooproduct**.</span></span>

![Adicionar tooproduct de API][api-management-add-api]

<span data-ttu-id="19fd2-148">Selecione a **API de Eco** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="19fd2-148">Select **Echo API**, and then click **Save**.</span></span>

![Adicionar API de Eco][api-management-add-echo-api]

## <span data-ttu-id="19fd2-150"><a name="policies"></a>tooconfigure políticas de cota e de limite de taxa de chamada</span><span class="sxs-lookup"><span data-stu-id="19fd2-150"><a name="policies"> </a>tooconfigure call rate limit and quota policies</span></span>
<span data-ttu-id="19fd2-151">Cotas e limites de taxa são configuradas no editor de diretiva de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-151">Rate limits and quotas are configured in hello policy editor.</span></span> <span data-ttu-id="19fd2-152">políticas de saudação dois adicionaremos neste tutorial são Olá [limitar a taxa de chamada por assinatura](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) e [definir cota de uso por assinatura](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) políticas.</span><span class="sxs-lookup"><span data-stu-id="19fd2-152">hello two policies we will be adding in this tutorial are hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="19fd2-153">Essas políticas devem ser aplicadas no escopo do produto hello.</span><span class="sxs-lookup"><span data-stu-id="19fd2-153">These policies must be applied at hello product scope.</span></span>

<span data-ttu-id="19fd2-154">Clique em **políticas** em Olá **gerenciamento de API** menu Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="19fd2-154">Click **Policies** under hello **API Management** menu on hello left.</span></span> <span data-ttu-id="19fd2-155">Em Olá **produto** lista, clique em **avaliação gratuita**.</span><span class="sxs-lookup"><span data-stu-id="19fd2-155">In hello **Product** list, click **Free Trial**.</span></span>

![Política de produtos][api-management-product-policy]

<span data-ttu-id="19fd2-157">Clique em **adicionar política** tooimport Olá modelo de política e começar a criar políticas de cota e de limite de taxa de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-157">Click **Add Policy** tooimport hello policy template and begin creating hello rate limit and quota policies.</span></span>

![Adicionar política][api-management-add-policy]

<span data-ttu-id="19fd2-159">Políticas de cota e de limite de taxa são políticas de entrada, portanto cursor Olá de posição no elemento de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="19fd2-159">Rate limit and quota policies are inbound policies, so position hello cursor in hello inbound element.</span></span>

![Editor de políticas][api-management-policy-editor-inbound]

<span data-ttu-id="19fd2-161">Role a lista de saudação de políticas e localizar Olá **limitar a taxa de chamada por assinatura** entrada da política.</span><span class="sxs-lookup"><span data-stu-id="19fd2-161">Scroll through hello list of policies and locate hello **Limit call rate per subscription** policy entry.</span></span>

![Declarações de políticas][api-management-limit-policies]

<span data-ttu-id="19fd2-163">Após Olá cursor é posicionado na Olá **entrada** elemento de política, clique Olá seta ao lado de **limitar a taxa de chamada por assinatura** tooinsert seu modelo de política.</span><span class="sxs-lookup"><span data-stu-id="19fd2-163">After hello cursor is positioned in hello **inbound** policy element, click hello arrow beside **Limit call rate per subscription** tooinsert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="19fd2-164">Como você pode ver do trecho hello, a política de saudação permite que os limites de configuração para as operações e as APIs do produto hello.</span><span class="sxs-lookup"><span data-stu-id="19fd2-164">As you can see from hello snippet, hello policy allows setting limits for hello product's APIs and operations.</span></span> <span data-ttu-id="19fd2-165">Neste tutorial, não use esse recurso, exclua Olá **api** e **operação** elementos da saudação **limite de taxa** elemento, de modo que apenas Olá externa **limite de taxa** elemento permanece, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-165">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **rate-limit** element, such that only hello outer **rate-limit** element remains, as shown in hello following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="19fd2-166">Produto de avaliação gratuita Olá, taxa de chamada permitido máximo de saudação é 10 chamadas por minuto, digite **10** como valor Olá Olá **chamadas** atributo, e **60** para Olá **período de renovação** atributo.</span><span class="sxs-lookup"><span data-stu-id="19fd2-166">In hello Free Trial product, hello maximum allowable call rate is 10 calls per minute, so type **10** as hello value for hello **calls** attribute, and **60** for hello **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="19fd2-167">Olá tooconfigure **definir cota de uso por assinatura** política, posição o cursor imediatamente abaixo Olá recém-adicionado **limite de taxa** elemento dentro do hello **entrada** elemento, localize e clique em Olá seta à esquerda da toohello de **definir cota de uso por assinatura**.</span><span class="sxs-lookup"><span data-stu-id="19fd2-167">tooconfigure hello **Set usage quota per subscription** policy, position your cursor immediately below hello newly added **rate-limit** element within hello **inbound** element, and then locate and click hello arrow toohello left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="19fd2-168">Da mesma forma toohello **definir cota de uso por assinatura** política, **definir cota de uso por assinatura** política permite definir limites para em operações e APIs do produto hello.</span><span class="sxs-lookup"><span data-stu-id="19fd2-168">Similarly toohello **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on hello product's APIs and operations.</span></span> <span data-ttu-id="19fd2-169">Neste tutorial, não use esse recurso, exclua Olá **api** e **operação** elementos da saudação **cota** elemento, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-169">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **quota** element, as shown in hello following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="19fd2-170">As cotas podem ser com base no número de saudação de chamadas por intervalo, a largura de banda ou ambos.</span><span class="sxs-lookup"><span data-stu-id="19fd2-170">Quotas can be based on hello number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="19fd2-171">Neste tutorial, nós não são limitação com base na largura de banda, exclua Olá **largura de banda** atributo.</span><span class="sxs-lookup"><span data-stu-id="19fd2-171">In this tutorial, we are not throttling based on bandwidth, so delete hello **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="19fd2-172">Produto de avaliação gratuita do hello, a cota de saudação é 200 chamadas por semana.</span><span class="sxs-lookup"><span data-stu-id="19fd2-172">In hello Free Trial product, hello quota is 200 calls per week.</span></span> <span data-ttu-id="19fd2-173">Especifique **200** como valor Olá Olá **chamadas** de atributo e, em seguida, especifique **604800** como valor Olá Olá **período de renovação** atributo.</span><span class="sxs-lookup"><span data-stu-id="19fd2-173">Specify **200** as hello value for hello **calls** attribute, and then specify **604800** as hello value for hello **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="19fd2-174">Os intervalos de política são especificados em segundos.</span><span class="sxs-lookup"><span data-stu-id="19fd2-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="19fd2-175">o intervalo de saudação toocalculate por uma semana, você pode multiplicar Olá quantos dias (7) pelo número de saudação de horas em um dia (24) pelo número de saudação de minutos em uma hora (60) por um número de segundos em um minuto (60) hello: 7 * 24 * 60 * 60 = 604800.</span><span class="sxs-lookup"><span data-stu-id="19fd2-175">toocalculate hello interval for a week, you can multiply hello number of days (7) by hello number of hours in a day (24) by hello number of minutes in an hour (60) by hello number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="19fd2-176">Quando terminar de configurar a política de hello, ele deve corresponder Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="19fd2-176">When you have finished configuring hello policy, it should match hello following example.</span></span>

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

<span data-ttu-id="19fd2-177">Depois de saudação desejado políticas estão configuradas, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="19fd2-177">After hello desired policies are configured, click **Save**.</span></span>

![Salvar política][api-management-policy-save]

## <span data-ttu-id="19fd2-179"><a name="publish-product"></a> produto de saudação toopublish</span><span class="sxs-lookup"><span data-stu-id="19fd2-179"><a name="publish-product"> </a> toopublish hello product</span></span>
<span data-ttu-id="19fd2-180">Agora que hello hello APIs foram adicionadas e Olá políticas estão configuradas, produto Olá deve ser publicado para que ele pode ser usado por desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="19fd2-180">Now that hello hello APIs are added and hello policies are configured, hello product must be published so that it can be used by developers.</span></span> <span data-ttu-id="19fd2-181">Clique em **produtos** de saudação **gerenciamento de API** menu saudação à esquerda e clique **avaliação gratuita** tooconfigure produto de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-181">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Configurar produto][api-management-configure-product]

<span data-ttu-id="19fd2-183">Clique em **publicar**e, em seguida, clique em **Sim, publicá-lo** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="19fd2-183">Click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span>

![Publicar produto][api-management-publish-product]

## <span data-ttu-id="19fd2-185"><a name="subscribe-account"></a>toosubscribe um produto de toohello de conta de desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="19fd2-185"><a name="subscribe-account"> </a>toosubscribe a developer account toohello product</span></span>
<span data-ttu-id="19fd2-186">Agora esse produto Olá é publicado, é tooand toobe disponível assinado usado por desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="19fd2-186">Now that hello product is published, it is available toobe subscribed tooand used by developers.</span></span>

> <span data-ttu-id="19fd2-187">Os administradores de uma instância de gerenciamento de API são automaticamente inscritos tooevery produto.</span><span class="sxs-lookup"><span data-stu-id="19fd2-187">Administrators of an API Management instance are automatically subscribed tooevery product.</span></span> <span data-ttu-id="19fd2-188">Nessa etapa do tutorial, vamos assinará um produto de avaliação gratuita do hello desenvolvedor de não-administrador contas toohello.</span><span class="sxs-lookup"><span data-stu-id="19fd2-188">In this tutorial step, we will subscribe one of hello non-administrator developer accounts toohello Free Trial product.</span></span> <span data-ttu-id="19fd2-189">Se sua conta de desenvolvedor fizer parte da função de administradores hello, você pode prosseguir com esta etapa, mesmo que você já se inscreveu.</span><span class="sxs-lookup"><span data-stu-id="19fd2-189">If your developer account is part of hello Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="19fd2-190">Clique em **usuários** em Olá **gerenciamento de API** menu Olá à esquerda e, em seguida, clique em nome de saudação da sua conta de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="19fd2-190">Click **Users** on hello **API Management** menu on hello left, and then click hello name of your developer account.</span></span> <span data-ttu-id="19fd2-191">Neste exemplo, estamos usando Olá **Clayton Gragg** conta de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="19fd2-191">In this example, we are using hello **Clayton Gragg** developer account.</span></span>

![Configurar desenvolvedor][api-management-configure-developer]

<span data-ttu-id="19fd2-193">Clique em **Adicionar assinatura**.</span><span class="sxs-lookup"><span data-stu-id="19fd2-193">Click **Add Subscription**.</span></span>

![Adicionar assinatura][api-management-add-subscription-menu]

<span data-ttu-id="19fd2-195">Selecione **Avaliação Gratuita** e clique em **Assinar**.</span><span class="sxs-lookup"><span data-stu-id="19fd2-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![Adicionar assinatura][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="19fd2-197">Neste tutorial, várias assinaturas simultâneas não estão habilitadas para o produto de avaliação gratuita de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-197">In this tutorial, multiple simultaneous subscriptions are not enabled for hello Free Trial product.</span></span> <span data-ttu-id="19fd2-198">Se forem, seria tooname solicitadas Olá assinatura, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-198">If they were, you would be prompted tooname hello subscription, as shown in hello following example.</span></span>
> 
> 

![Adicionar assinatura][api-management-add-subscription-multiple]

<span data-ttu-id="19fd2-200">Depois de clicar em **assinar**, produto Olá aparece no hello **assinatura** lista de usuário hello.</span><span class="sxs-lookup"><span data-stu-id="19fd2-200">After clicking **Subscribe**, hello product appears in hello **Subscription** list for hello user.</span></span>

![Assinatura adicionada][api-management-subscription-added]

## <span data-ttu-id="19fd2-202"><a name="test-rate-limit"></a>toocall um limite de taxa de saudação operação e teste</span><span class="sxs-lookup"><span data-stu-id="19fd2-202"><a name="test-rate-limit"> </a>toocall an operation and test hello rate limit</span></span>
<span data-ttu-id="19fd2-203">Agora que hello produto de avaliação gratuita está configurado e publicado, podemos chamar algumas operações e testar a política de limite de taxa de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-203">Now that hello Free Trial product is configured and published, we can call some operations and test hello rate limit policy.</span></span>
<span data-ttu-id="19fd2-204">Portal do desenvolvedor do comutador toohello clicando **portal do desenvolvedor** no menu superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-204">Switch toohello developer portal by clicking **Developer portal** in hello upper-right menu.</span></span>

![Portal do desenvolvedor][api-management-developer-portal-menu]

<span data-ttu-id="19fd2-206">Clique em **APIs** Olá menu superior e, em seguida, clique em **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="19fd2-206">Click **APIs** in hello top menu, and then click **Echo API**.</span></span>

![Portal do desenvolvedor][api-management-developer-portal-api-menu]

<span data-ttu-id="19fd2-208">Clique em **Recurso GET**, em seguida, clique em **Experimentar**.</span><span class="sxs-lookup"><span data-stu-id="19fd2-208">Click **GET Resource**, and then click **Try it**.</span></span>

![Abrir console][api-management-open-console]

<span data-ttu-id="19fd2-210">Mantenha o padrão de saudação valores de parâmetro e, em seguida, selecione a chave de assinatura para o produto de avaliação gratuita de saudação.</span><span class="sxs-lookup"><span data-stu-id="19fd2-210">Keep hello default parameter values, and then select your subscription key for hello Free Trial product.</span></span>

![Chave de assinatura][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="19fd2-212">Se você tiver várias assinaturas, ser se tooselect Olá chave **avaliação gratuita**, ou mais políticas de saudação que foram configuradas nas etapas anteriores Olá não terá efeito.</span><span class="sxs-lookup"><span data-stu-id="19fd2-212">If you have multiple subscriptions, be sure tooselect hello key for **Free Trial**, or else hello policies that were configured in hello previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="19fd2-213">Clique em **enviar**e, em seguida, exibir resposta hello.</span><span class="sxs-lookup"><span data-stu-id="19fd2-213">Click **Send**, and then view hello response.</span></span> <span data-ttu-id="19fd2-214">Saudação de Observação **status da resposta** de **200 Okey**.</span><span class="sxs-lookup"><span data-stu-id="19fd2-214">Note hello **Response status** of **200 OK**.</span></span>

![Resultados da operação][api-management-http-get-results]

<span data-ttu-id="19fd2-216">Clique em **enviar** em uma taxa maior que a política de limite de taxa de saudação de 10 chamadas por minuto.</span><span class="sxs-lookup"><span data-stu-id="19fd2-216">Click **Send** at a rate greater than hello rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="19fd2-217">Depois de política de limite de taxa de saudação for excedida, um status de resposta de **429 muito muitas solicitações** é retornado.</span><span class="sxs-lookup"><span data-stu-id="19fd2-217">After hello rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![Resultados da operação][api-management-http-get-429]

<span data-ttu-id="19fd2-219">Olá **conteúdo de resposta** indica Olá restantes intervalo antes de tentativas será bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="19fd2-219">hello **Response content** indicates hello remaining interval before retries will be successful.</span></span>

<span data-ttu-id="19fd2-220">Quando a política de limite de taxa de saudação de 10 chamadas por minuto está em vigor, as chamadas subsequentes falharão até que 60 segundos decorridos da saudação primeiro de produto de toohello do hello 10 chamadas com êxito antes que o limite de taxa de saudação foi excedido.</span><span class="sxs-lookup"><span data-stu-id="19fd2-220">When hello rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from hello first of hello 10 successful calls toohello product before hello rate limit was exceeded.</span></span> <span data-ttu-id="19fd2-221">Neste exemplo, Olá restantes intervalo é 54 segundos.</span><span class="sxs-lookup"><span data-stu-id="19fd2-221">In this example, hello remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="19fd2-222"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="19fd2-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="19fd2-223">Assista a uma demonstração de definir as cotas e limites de taxa em Olá vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="19fd2-223">Watch a demo of setting rate limits and quotas in hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
