---
title: "configurações de aaaCustom para ambientes de serviço de aplicativo"
description: "Definições de configuração personalizadas para Ambientes de Serviço de Aplicativo"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="858a1-103">Definições de configuração personalizadas para Ambientes de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="858a1-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="858a1-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="858a1-104">Overview</span></span>
<span data-ttu-id="858a1-105">Como os ambientes de serviço de aplicativo isolado tooa único cliente, há determinadas definições de configuração que podem ser aplicadas tooApp exclusivamente os ambientes de serviço.</span><span class="sxs-lookup"><span data-stu-id="858a1-105">Because App Service Environments are isolated tooa single customer, there are certain configuration settings that can be applied exclusively tooApp Service Environments.</span></span> <span data-ttu-id="858a1-106">Este artigo documenta Olá várias personalizações específicas que estão disponíveis para ambientes de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="858a1-106">This article documents hello various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="858a1-107">Se você não tiver um ambiente de serviço de aplicativo, consulte [como tooCreate um ambiente de serviço de aplicativo](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="858a1-107">If you do not have an App Service Environment, see [How tooCreate an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="858a1-108">Você pode armazenar as personalizações do ambiente de serviço de aplicativo usando uma matriz em Olá novo **clusterSettings** atributo.</span><span class="sxs-lookup"><span data-stu-id="858a1-108">You can store App Service Environment customizations by using an array in hello new **clusterSettings** attribute.</span></span> <span data-ttu-id="858a1-109">Esse atributo é encontrado no dicionário "Propriedades" Olá Olá *hostingEnvironments* entidade do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="858a1-109">This attribute is found in hello "Properties" dictionary of hello *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="858a1-110">seguinte trecho de modelo do Gerenciador de recursos abreviado Hello mostra Olá **clusterSettings** atributo:</span><span class="sxs-lookup"><span data-stu-id="858a1-110">hello following abbreviated Resource Manager template snippet shows hello **clusterSettings** attribute:</span></span>

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

<span data-ttu-id="858a1-111">Olá **clusterSettings** atributo pode ser incluído em uma saudação de tooupdate de modelo do Gerenciador de recursos o ambiente de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="858a1-111">hello **clusterSettings** attribute can be included in a Resource Manager template tooupdate hello App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a><span data-ttu-id="858a1-112">Use o Gerenciador de recursos do Azure tooupdate um ambiente de serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="858a1-112">Use Azure Resource Explorer tooupdate an App Service Environment</span></span>
<span data-ttu-id="858a1-113">Como alternativa, você pode atualizar Olá ambiente de serviço de aplicativo usando [Gerenciador de recursos do Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="858a1-113">Alternatively, you can update hello App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="858a1-114">No Gerenciador de recursos, vá para o nó de toohello para Olá ambiente de serviço de aplicativo (**assinaturas** > **resourceGroups** > **provedores**  >  **Microsoft** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="858a1-114">In Resource Explorer, go toohello node for hello App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="858a1-115">Clique Olá ambiente de serviço de aplicativo específico que você deseja tooupdate.</span><span class="sxs-lookup"><span data-stu-id="858a1-115">Then click hello specific App Service Environment that you want tooupdate.</span></span>
2. <span data-ttu-id="858a1-116">No painel direito da saudação, clique em **leitura/gravação** no tooallow de barra de ferramentas superior Olá interativo de edição no Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="858a1-116">In hello right pane, click **Read/Write** in hello upper toolbar tooallow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="858a1-117">Clique em Olá azul **editar** modelo Olá de Gerenciador de recursos do toomake botão editável.</span><span class="sxs-lookup"><span data-stu-id="858a1-117">Click hello blue **Edit** button toomake hello Resource Manager template editable.</span></span>
4. <span data-ttu-id="858a1-118">Rolagem toohello parte inferior do painel direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="858a1-118">Scroll toohello bottom of hello right pane.</span></span> <span data-ttu-id="858a1-119">Olá **clusterSettings** atributo é Olá parte mais inferior, onde você pode inserir ou atualizar o seu valor.</span><span class="sxs-lookup"><span data-stu-id="858a1-119">hello **clusterSettings** attribute is at hello very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="858a1-120">Matriz de saudação tipo (ou copiar e colar) de valores de configuração que você deseja no hello **clusterSettings** atributo.</span><span class="sxs-lookup"><span data-stu-id="858a1-120">Type (or copy and paste) hello array of configuration values you want in hello **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="858a1-121">Clique em Olá verde **colocar** botão que foi localizado na parte superior de saudação do hello painel direito toocommit Olá alteração toohello ambiente de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="858a1-121">Click hello green **PUT** button that's located at hello top of hello right pane toocommit hello change toohello App Service Environment.</span></span>

<span data-ttu-id="858a1-122">No entanto, enviar alterações hello, que leva aproximadamente 30 minutos, multiplicados pelo número de saudação do front-ends no hello ambiente de serviço de aplicativo para Olá alterar tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="858a1-122">However you submit hello change, it takes roughly 30 minutes multiplied by hello number of front ends in hello App Service Environment for hello change tootake effect.</span></span>
<span data-ttu-id="858a1-123">Por exemplo, se um ambiente de serviço de aplicativo tem quatro front-ends, levará aproximadamente duas horas para Olá toofinish de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="858a1-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for hello configuration update toofinish.</span></span> <span data-ttu-id="858a1-124">Embora a alteração de configuração hello está sendo revertida, outras operações de dimensionamento ou operações de alteração de configuração podem ocorrer em Olá ambiente de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="858a1-124">While hello configuration change is being rolled out, no other scaling operations or configuration change operations can take place in hello App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="858a1-125">Desabilitar o TLS 1.0</span><span class="sxs-lookup"><span data-stu-id="858a1-125">Disable TLS 1.0</span></span>
<span data-ttu-id="858a1-126">Uma pergunta recorrente de clientes, especialmente os clientes estejam lidando com conformidade PCI auditorias, é como tooexplicitly desabilitar o TLS 1.0 para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="858a1-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how tooexplicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="858a1-127">TLS 1.0 pode ser desabilitado por meio do seguinte Olá **clusterSettings** entrada:</span><span class="sxs-lookup"><span data-stu-id="858a1-127">TLS 1.0 can be disabled through hello following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="858a1-128">Mudar a ordem do pacote de criptografia TLS</span><span class="sxs-lookup"><span data-stu-id="858a1-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="858a1-129">Outra pergunta de clientes é se eles podem modificar a lista Olá codificações negociado por seu servidor e isso pode ser feito por meio de modificação Olá **clusterSettings** conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="858a1-129">Another question from customers is if they can modify hello list of ciphers negotiated by their server and this can be achieved by modifying hello **clusterSettings** as shown below.</span></span> <span data-ttu-id="858a1-130">lista de saudação de conjuntos de codificação disponíveis pode ser recuperada de [este artigo do MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="858a1-130">hello list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="858a1-131">Se forem definidos valores incorretos para o conjunto de codificação de saudação SChannel não é possível entender, todos os servidores de tooyour de comunicação TLS podem parar de funcionar.</span><span class="sxs-lookup"><span data-stu-id="858a1-131">If incorrect values are set for hello cipher suite that SChannel cannot understand, all TLS communication tooyour server might stop functioning.</span></span> <span data-ttu-id="858a1-132">Nesse caso, você precisará Olá tooremove *FrontEndSSLCipherSuiteOrder* entrada do **clusterSettings** e enviar Olá atualizado codificação padrão do Gerenciador de recursos modelo toorevert toohello back configurações de pacote.</span><span class="sxs-lookup"><span data-stu-id="858a1-132">In such a case, you will need tooremove hello *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit hello updated Resource Manager template toorevert back toohello default cipher suite settings.</span></span>  <span data-ttu-id="858a1-133">Use esta funcionalidade com cuidado.</span><span class="sxs-lookup"><span data-stu-id="858a1-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="858a1-134">Introdução</span><span class="sxs-lookup"><span data-stu-id="858a1-134">Get started</span></span>
<span data-ttu-id="858a1-135">site de modelo do Gerenciador de recursos de início rápido do Azure Olá inclui um modelo com a definição base Olá para [criando um ambiente de serviço de aplicativo](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span><span class="sxs-lookup"><span data-stu-id="858a1-135">hello Azure Quickstart Resource Manager template site includes a template with hello base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
