---
title: "aaaSet a ambientes de preparo para aplicativos web no serviço de aplicativo do Azure | Microsoft Docs"
description: "Saiba como toouse preparado a publicação de aplicativos web no serviço de aplicativo do Azure."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="67ce4-103">Configurar ambientes de preparo no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="67ce4-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="67ce4-104">Quando você implanta seu aplicativo web, o aplicativo web no Linux, móvel back-end e aplicativo de API muito[do serviço de aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714), você pode implantar tooa slot de implantação separado em vez de slot de produção saudação padrão durante a execução no hello **padrão**ou **Premium** modo do plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="67ce4-104">When you deploy your web app, web app on Linux, mobile back end, and API app too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy tooa separate deployment slot instead of hello default production slot when running in hello **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="67ce4-105">Os slots de implantação são, na verdade, aplicativos online com seus próprios nomes de host.</span><span class="sxs-lookup"><span data-stu-id="67ce4-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="67ce4-106">Elementos de conteúdo e as configurações de aplicativo podem ser trocados entre os dois slots de implantação, incluindo o slot de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="67ce4-106">App content and configurations elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="67ce4-107">Implantar o slot de implantação do aplicativo tooa tem Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="67ce4-107">Deploying your application tooa deployment slot has hello following benefits:</span></span>

* <span data-ttu-id="67ce4-108">Você pode validar as alterações de aplicativo em um slot de implantação de preparo antes de trocá-lo com o slot de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="67ce4-108">You can validate app changes in a staging deployment slot before swapping it with hello production slot.</span></span>
* <span data-ttu-id="67ce4-109">Implantando um slot de tooa aplicativo pela primeira vez e trocá-lo em produção garantem que todas as instâncias do slot de saudação são aquecidas antes de ser trocadas em produção.</span><span class="sxs-lookup"><span data-stu-id="67ce4-109">Deploying an app tooa slot first and swapping it into production ensures that all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="67ce4-110">Isso elimina o tempo de inatividade quando você for implantar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="67ce4-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="67ce4-111">Olá redirecionamento do tráfego é contínuo e nenhuma solicitação é descartada como resultado de operações de troca.</span><span class="sxs-lookup"><span data-stu-id="67ce4-111">hello traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="67ce4-112">Todo esse fluxo de trabalho pode ser automatizado por meio da configuração de [Permuta Automática](#Auto-Swap) quando a validação de pré-permuta não é necessária.</span><span class="sxs-lookup"><span data-stu-id="67ce4-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="67ce4-113">Após uma troca slot Olá com aplicativo preparado anteriormente agora tem Olá aplicativo de produção anterior.</span><span class="sxs-lookup"><span data-stu-id="67ce4-113">After a swap, hello slot with previously staged app now has hello previous production app.</span></span> <span data-ttu-id="67ce4-114">Se alterações Olá trocadas no slot de produção de hello estiverem não conforme o esperado, você pode executar Olá que mesma troca imediatamente tooget o "último site conhecido" de volta.</span><span class="sxs-lookup"><span data-stu-id="67ce4-114">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good site" back.</span></span>

<span data-ttu-id="67ce4-115">Cada modo de plano do Serviço de Aplicativo dá suporte a um número diferente de slots de implantação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="67ce4-116">toofind número Olá de slots modo do aplicativo oferece suporte, consulte [preços do serviço de aplicativo](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="67ce4-116">toofind out hello number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="67ce4-117">Quando seu aplicativo tiver vários slots, você não pode alterar o modo de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-117">When your app has multiple slots, you cannot change hello mode.</span></span>
* <span data-ttu-id="67ce4-118">O dimensionamento não está disponível para slots de não produção.</span><span class="sxs-lookup"><span data-stu-id="67ce4-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="67ce4-119">O gerenciamento de recurso vinculado não tem suporte para slots de não produção.</span><span class="sxs-lookup"><span data-stu-id="67ce4-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="67ce4-120">Em Olá [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715) somente, você pode evitar esse impacto potencial em um slot de produção movendo temporariamente o modo de planejamento do hello slot de produção não tooa diferente do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="67ce4-120">In hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving hello non-production slot tooa different App Service plan mode.</span></span> <span data-ttu-id="67ce4-121">Observe que esse slot de não produção de hello novamente deve compartilhar a saudação mesmo modo com o slot de produção de hello antes que você pode trocar os slots de saudação dois.</span><span class="sxs-lookup"><span data-stu-id="67ce4-121">Note that hello non-production slot must once again share hello same mode with hello production slot before you can swap hello two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="67ce4-122">Adicionar um slot de implantação</span><span class="sxs-lookup"><span data-stu-id="67ce4-122">Add a deployment slot</span></span>
<span data-ttu-id="67ce4-123">aplicativo Hello deve estar em execução Olá **padrão** ou **Premium** modo na ordem para você tooenable vários slots de implantação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-123">hello app must be running in hello **Standard** or **Premium** mode in order for you tooenable multiple deployment slots.</span></span>

1. <span data-ttu-id="67ce4-124">Em Olá [Portal do Azure](https://portal.azure.com/), abra o aplicativo [folha de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="67ce4-124">In hello [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="67ce4-125">Escolha Olá **slots de implantação** opção e, em seguida, clique em **adicionar Slot**.</span><span class="sxs-lookup"><span data-stu-id="67ce4-125">Choose hello **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Adicionar um novo slot de implantação][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="67ce4-127">Se Olá aplicativo não ainda estiver no hello **padrão** ou **Premium** modo, você receberá uma mensagem indicando modos de saudação tem suportada para habilitar a publicação de preparação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-127">If hello app is not already in hello **Standard** or **Premium** mode, you will receive a message indicating hello supported modes for enabling staged publishing.</span></span> <span data-ttu-id="67ce4-128">Neste ponto, você tem Olá opção tooselect **atualização** e navegue toohello **escala** guia do aplicativo antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="67ce4-128">At this point, you have hello option tooselect **Upgrade** and navigate toohello **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="67ce4-129">Em Olá **adicionar um slot** folha, dê um nome de slot hello e selecionar se tooclone configuração do aplicativo de outro slot de implantação existente.</span><span class="sxs-lookup"><span data-stu-id="67ce4-129">In hello **Add a slot** blade, give hello slot a name, and select whether tooclone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="67ce4-130">Clique em Olá toocontinue de marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="67ce4-130">Click hello check mark toocontinue.</span></span>
   
    ![Fonte de configuração][ConfigurationSource1]
   
    <span data-ttu-id="67ce4-132">Olá primeira vez que você adicionar um slot, você terá apenas duas opções: configuração de clone do slot de padrão de saudação em produção ou não.</span><span class="sxs-lookup"><span data-stu-id="67ce4-132">hello first time you add a slot, you will only have two choices: clone configuration from hello default slot in production or not at all.</span></span>
    <span data-ttu-id="67ce4-133">Depois que você criou vários slots, será capaz de tooclone configuração de um slot diferente de saudação em produção:</span><span class="sxs-lookup"><span data-stu-id="67ce4-133">After you have created several slots, you will be able tooclone configuration from a slot other than hello one in production:</span></span>
   
    ![Fontes de configuração][MultipleConfigurationSources]
4. <span data-ttu-id="67ce4-135">Na folha de recursos do aplicativo, clique em **slots de implantação**, em seguida, clique em um tooopen do slot de implantação folha de recursos do que slot, com um conjunto de métricas e configuração, assim como qualquer outro aplicativo.</span><span class="sxs-lookup"><span data-stu-id="67ce4-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot tooopen that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="67ce4-136">Olá nome do slot de saudação é mostrado na parte superior de saudação do hello folha tooremind que você está exibindo Olá slot de implantação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-136">hello name of hello slot is shown at hello top of hello blade tooremind you that you are viewing hello deployment slot.</span></span>
   
    ![Título do slot de implantação][StagingTitle]
5. <span data-ttu-id="67ce4-138">Clique em URL do aplicativo hello na folha do slot hello.</span><span class="sxs-lookup"><span data-stu-id="67ce4-138">Click hello app URL in hello slot's blade.</span></span> <span data-ttu-id="67ce4-139">Observe que o slot de implantação Olá tem seu próprio nome de host e também é um aplicativo em tempo real.</span><span class="sxs-lookup"><span data-stu-id="67ce4-139">Notice hello deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="67ce4-140">slot de implantação da toohello toolimit acesso público, consulte [aplicativo Web do serviço de aplicativo – slots de implantação de produção toonon do bloco da web acesso](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="67ce4-140">toolimit public access toohello deployment slot, see [App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="67ce4-141">Não há nenhum conteúdo após a criação do slot de implantação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="67ce4-142">Você pode implantar o slot toohello de uma ramificação do repositório diferente, ou um repositório diferente.</span><span class="sxs-lookup"><span data-stu-id="67ce4-142">You can deploy toohello slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="67ce4-143">Você também pode alterar a configuração do slot de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-143">You can also change hello slot's configuration.</span></span> <span data-ttu-id="67ce4-144">Olá Use publicar perfil ou implantação as credenciais associadas Olá slot de implantação para atualizações de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="67ce4-144">Use hello publish profile or deployment credentials associated with hello deployment slot for content updates.</span></span>  <span data-ttu-id="67ce4-145">Por exemplo, você pode [publicar toothis slot com o git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="67ce4-145">For example, you can [publish toothis slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="67ce4-146">Configuração de slots de implantação</span><span class="sxs-lookup"><span data-stu-id="67ce4-146">Configuration for deployment slots</span></span>
<span data-ttu-id="67ce4-147">Quando você clona a configuração de outro slot de implantação, configuração clonado Olá é editável.</span><span class="sxs-lookup"><span data-stu-id="67ce4-147">When you clone configuration from another deployment slot, hello cloned configuration is editable.</span></span> <span data-ttu-id="67ce4-148">Além disso, alguns elementos de configuração seguirá conteúdo Olá em uma troca (não slot específico) enquanto outros elementos de configuração permanecerão no hello mesmo slot após uma troca (slot específico).</span><span class="sxs-lookup"><span data-stu-id="67ce4-148">Furthermore, some configuration elements will follow hello content across a swap (not slot specific) while other configuration elements will stay in hello same slot after a swap (slot specific).</span></span> <span data-ttu-id="67ce4-149">Hello listas a seguir mostram configuração Olá que mudará quando você troca os slots.</span><span class="sxs-lookup"><span data-stu-id="67ce4-149">hello following lists show hello configuration that will change when you swap slots.</span></span>

<span data-ttu-id="67ce4-150">**Configurações que são permutadas**:</span><span class="sxs-lookup"><span data-stu-id="67ce4-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="67ce4-151">Configurações gerais - como a versão do framework, 32/64 bits, Web sockets</span><span class="sxs-lookup"><span data-stu-id="67ce4-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="67ce4-152">Configurações do aplicativo (pode ser configurado toostick tooa slot)</span><span class="sxs-lookup"><span data-stu-id="67ce4-152">App settings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="67ce4-153">Cadeias de caracteres de Conexão (pode ser configurado toostick tooa slot)</span><span class="sxs-lookup"><span data-stu-id="67ce4-153">Connection strings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="67ce4-154">Mapeamentos de manipulador</span><span class="sxs-lookup"><span data-stu-id="67ce4-154">Handler mappings</span></span>
* <span data-ttu-id="67ce4-155">Configurações de monitoramento e diagnóstico</span><span class="sxs-lookup"><span data-stu-id="67ce4-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="67ce4-156">Conteúdo de Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="67ce4-156">WebJobs content</span></span>

<span data-ttu-id="67ce4-157">**Configurações que não são permutadas**:</span><span class="sxs-lookup"><span data-stu-id="67ce4-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="67ce4-158">Pontos de extremidade de publicação</span><span class="sxs-lookup"><span data-stu-id="67ce4-158">Publishing endpoints</span></span>
* <span data-ttu-id="67ce4-159">Nomes de domínio personalizados</span><span class="sxs-lookup"><span data-stu-id="67ce4-159">Custom Domain Names</span></span>
* <span data-ttu-id="67ce4-160">Associações e certificados SSL</span><span class="sxs-lookup"><span data-stu-id="67ce4-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="67ce4-161">Configurações de escala</span><span class="sxs-lookup"><span data-stu-id="67ce4-161">Scale settings</span></span>
* <span data-ttu-id="67ce4-162">Agendadores de Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="67ce4-162">WebJobs schedulers</span></span>

<span data-ttu-id="67ce4-163">tooconfigure uma configuração ou conexão cadeia de caracteres toostick tooa slot do aplicativo (não trocado), Olá acesso **configurações do aplicativo** folha para um slot específico, em seguida, selecione Olá **configuração do Slot** caixa Olá elementos de configuração que devem preferir slot hello.</span><span class="sxs-lookup"><span data-stu-id="67ce4-163">tooconfigure an app setting or connection string toostick tooa slot (not swapped), access hello **Application Settings** blade for a specific slot, then select hello **Slot Setting** box for hello configuration elements that should stick hello slot.</span></span> <span data-ttu-id="67ce4-164">Observe que marcar um elemento de configuração específicos de slot tem o efeito de saudação do estabelecimento de elemento como não swap em todos os slots de implantação Olá associados ao aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="67ce4-164">Note that marking a configuration element as slot specific has hello effect of establishing that element as not swappable across all hello deployment slots associated with hello app.</span></span>

![Configurações de slot][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="67ce4-166">Permute slots de implantação</span><span class="sxs-lookup"><span data-stu-id="67ce4-166">Swap deployment slots</span></span> 
<span data-ttu-id="67ce4-167">Você pode trocar os slots de implantação Olá **visão geral** ou **slots de implantação** exibição da folha de recursos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="67ce4-167">You can swap deployment slots in hello **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67ce4-168">Antes de você troca um aplicativo a partir de um slot de implantação em produção, certifique-se de que todas as configurações específicas de slot não são configuradas exatamente como você deseja toohave-lo no destino da troca hello.</span><span class="sxs-lookup"><span data-stu-id="67ce4-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want toohave it in hello swap target.</span></span>
> 
> 

1. <span data-ttu-id="67ce4-169">tooswap slots de implantação, clique em Olá **trocar** botão na barra de comandos de saudação do aplicativo hello, ou na barra de comandos de saudação de um slot de implantação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-169">tooswap deployment slots, click hello **Swap** button in hello command bar of hello app or in hello command bar of a deployment slot.</span></span>
   
    ![Botão permutar][SwapButtonBar]

2. <span data-ttu-id="67ce4-171">Certifique-se de destino Olá permuta origem e de troca estão definidas corretamente.</span><span class="sxs-lookup"><span data-stu-id="67ce4-171">Make sure that hello swap source and swap target are set properly.</span></span> <span data-ttu-id="67ce4-172">Geralmente, o destino da troca Olá é slot de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="67ce4-172">Usually, hello swap target is hello production slot.</span></span> <span data-ttu-id="67ce4-173">Clique em **Okey** toocomplete operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-173">Click **OK** toocomplete hello operation.</span></span> <span data-ttu-id="67ce4-174">Quando a conclusão da operação de hello, slots de implantação Olá foram trocados.</span><span class="sxs-lookup"><span data-stu-id="67ce4-174">When hello operation finishes, hello deployment slots have been swapped.</span></span>

    ![Troca completa](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="67ce4-176">Para Olá **troca com visualização** trocar o tipo, consulte [troca com visualização (troca de várias fase)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="67ce4-176">For hello **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="67ce4-177">Troca com visualização (troca de várias fases)</span><span class="sxs-lookup"><span data-stu-id="67ce4-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="67ce4-178">Troca com visualização, ou troca de várias fases, simplifica a validação de elementos de configuração específicos ao slot, como cadeias de conexão.</span><span class="sxs-lookup"><span data-stu-id="67ce4-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="67ce4-179">Para cargas de trabalho de missão crítica, você deseja toovalidate que Olá aplicativo se comporta conforme o esperado quando a configuração do slot de produção de hello for aplicada, e você deve executar essa validação *antes de* aplicativo hello é alternado para a produção.</span><span class="sxs-lookup"><span data-stu-id="67ce4-179">For mission-critical workloads, you want toovalidate that hello app behaves as expected when hello production slot's configuration is applied, and you must perform such validation *before* hello app is swapped into production.</span></span> <span data-ttu-id="67ce4-180">A troca com visualização é o que você precisa.</span><span class="sxs-lookup"><span data-stu-id="67ce4-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="67ce4-181">Não há suporte para a troca com visualização em aplicativos Web no Linux.</span><span class="sxs-lookup"><span data-stu-id="67ce4-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="67ce4-182">Quando você usa Olá **troca com visualização** opção (consulte [trocar slots de implantação](#Swap)), serviço de aplicativo hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="67ce4-182">When you use hello **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does hello following:</span></span>

- <span data-ttu-id="67ce4-183">Mantém Olá destino slot inalterada para que os carga de trabalho em que slot (por exemplo, produção) não é afetada.</span><span class="sxs-lookup"><span data-stu-id="67ce4-183">Keeps hello destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="67ce4-184">Aplica-se elementos de configuração de saudação da saudação slot toohello fonte do slot de destino, incluindo cadeias de caracteres de conexão específicos de slot hello e configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="67ce4-184">Applies hello configuration elements of hello destination slot toohello source slot, including hello slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="67ce4-185">Reinicia os processos de trabalho de saudação no slot de origem hello usando esses elementos de configuração mencionados acima.</span><span class="sxs-lookup"><span data-stu-id="67ce4-185">Restarts hello worker processes on hello source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="67ce4-186">Quando você concluir troca Olá: move slot de origem warmed-up Olá no slot de destino hello.</span><span class="sxs-lookup"><span data-stu-id="67ce4-186">When you complete hello swap: Moves hello pre-warmed-up source slot into hello destination slot.</span></span> <span data-ttu-id="67ce4-187">slot de destino Olá é movido para o slot de origem hello como em uma troca manual.</span><span class="sxs-lookup"><span data-stu-id="67ce4-187">hello destination slot is moved into hello source slot as in a manual swap.</span></span>
- <span data-ttu-id="67ce4-188">Quando você cancela a troca de saudação: reaplica elementos de configuração de saudação do slot de origem toohello do slot de origem hello.</span><span class="sxs-lookup"><span data-stu-id="67ce4-188">When you cancel hello swap: Reapplies hello configuration elements of hello source slot toohello source slot.</span></span>

<span data-ttu-id="67ce4-189">Você pode visualizar exatamente como Olá aplicativo se comportará com a configuração do slot de destino hello.</span><span class="sxs-lookup"><span data-stu-id="67ce4-189">You can preview exactly how hello app will behave with hello destination slot's configuration.</span></span> <span data-ttu-id="67ce4-190">Depois de concluir a validação, você concluir troca de saudação em uma etapa separada.</span><span class="sxs-lookup"><span data-stu-id="67ce4-190">Once you complete validation, you complete hello swap in a separate step.</span></span> <span data-ttu-id="67ce4-191">Esta etapa tem Olá vantagem adicional que o slot de origem Olá já é aquecido com a configuração desejada hello e os clientes não terão nenhum tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="67ce4-191">This step has hello added advantage that hello source slot is already warmed up with hello desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="67ce4-192">Exemplos de saudação cmdlets do PowerShell do Azure disponíveis para a troca de várias fase são incluídos no hello cmdlets do PowerShell do Azure para a seção de slots de implantação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-192">Samples for hello Azure PowerShell cmdlets available for multi-phase swap are included in hello Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="67ce4-193">Configurar a troca automática</span><span class="sxs-lookup"><span data-stu-id="67ce4-193">Configure Auto Swap</span></span>
<span data-ttu-id="67ce4-194">Simplifica de troca automática DevOps cenários em que você deseja toocontinuously implanta seu aplicativo com zero inicialização a frio e tempo de inatividade zero para clientes finais do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="67ce4-194">Auto Swap streamlines DevOps scenarios where you want toocontinuously deploy your app with zero cold start and zero downtime for end customers of hello app.</span></span> <span data-ttu-id="67ce4-195">Quando um slot de implantação é configurado para a troca automática em produção, sempre que você enviar por push o slot de toothat de atualização de código, do serviço de aplicativo automaticamente alternará Olá aplicativo em produção após já ter aquecido no slot de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update toothat slot, App Service will automatically swap hello app into production after it has already warmed up in hello slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67ce4-196">Quando você habilitar a troca automática para um slot, certifique-se de configuração do slot de saudação é exatamente configuração Olá destinada ao slot de destino da saudação (geralmente slot de produção de hello).</span><span class="sxs-lookup"><span data-stu-id="67ce4-196">When you enable Auto Swap for a slot, make sure hello slot configuration is exactly hello configuration intended for hello target slot (usually hello production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="67ce4-197">Não há suporte para a troca automática em aplicativos Web no Linux.</span><span class="sxs-lookup"><span data-stu-id="67ce4-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="67ce4-198">Configurar a Permuta Automática para um slot é fácil.</span><span class="sxs-lookup"><span data-stu-id="67ce4-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="67ce4-199">Siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="67ce4-199">Follow hello steps below:</span></span>

1. <span data-ttu-id="67ce4-200">Em **Slots de Implantação**, selecione um slot que não esteja em produção e escolha **Configurações do Aplicativo** na folha de recursos do slot.</span><span class="sxs-lookup"><span data-stu-id="67ce4-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="67ce4-201">Selecione **na** para **troca automática**, selecione slot de destino desejado Olá em **Slot de troca automática**e clique em **salvar** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-201">Select **On** for **Auto Swap**, select hello desired target slot in **Auto Swap Slot**, and click **Save** in hello command bar.</span></span> <span data-ttu-id="67ce4-202">Certifique-se de configuração para o slot de saudação é exatamente configuração Olá destinada ao slot de destino hello.</span><span class="sxs-lookup"><span data-stu-id="67ce4-202">Make sure configuration for hello slot is exactly hello configuration intended for hello target slot.</span></span>
   
    <span data-ttu-id="67ce4-203">Olá **notificações** guia pisca uma verde **êxito** após a conclusão da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-203">hello **Notifications** tab will flash a green **SUCCESS** once hello operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="67ce4-204">tootest troca automática para seu aplicativo, primeiro você poderá selecionar um slot de destino não seja de produção em **Slot de troca automática** toobecome familiarizado com o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-204">tootest Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** toobecome familiar with hello feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="67ce4-205">Execute um slot de implantação de toothat de envio por push de código.</span><span class="sxs-lookup"><span data-stu-id="67ce4-205">Execute a code push toothat deployment slot.</span></span> <span data-ttu-id="67ce4-206">Troca automática ocorrerá após um curto período de tempo e atualização hello será refletida na URL do seu slot de destino.</span><span class="sxs-lookup"><span data-stu-id="67ce4-206">Auto Swap will happen after a short time and hello update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a><span data-ttu-id="67ce4-207">um aplicativo de produção após a troca de toorollback</span><span class="sxs-lookup"><span data-stu-id="67ce4-207">toorollback a production app after swap</span></span>
<span data-ttu-id="67ce4-208">Se qualquer erro for identificado na produção após uma troca de slot, reverter slots Olá tootheir back pré-permuta estados trocando slots de saudação mesmo dois imediatamente.</span><span class="sxs-lookup"><span data-stu-id="67ce4-208">If any errors are identified in production after a slot swap, roll hello slots back tootheir pre-swap states by swapping hello same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="67ce4-209">Aquecimento personalizado antes da permuta</span><span class="sxs-lookup"><span data-stu-id="67ce4-209">Custom warm-up before swap</span></span>
<span data-ttu-id="67ce4-210">Alguns aplicativos podem exigir ações personalizadas de aquecimento.</span><span class="sxs-lookup"><span data-stu-id="67ce4-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="67ce4-211">Olá `applicationInitialization` elemento de configuração no Web. config permite que você toospecify inicialização personalizada ações toobe executada antes que uma solicitação é recebida.</span><span class="sxs-lookup"><span data-stu-id="67ce4-211">hello `applicationInitialization` configuration element in web.config allows you toospecify custom initialization actions toobe performed before a request is received.</span></span> <span data-ttu-id="67ce4-212">operação de permuta Olá aguardará esse toocomplete aquecimento personalizado.</span><span class="sxs-lookup"><span data-stu-id="67ce4-212">hello swap operation will wait for this custom warm-up toocomplete.</span></span> <span data-ttu-id="67ce4-213">Este é está um exemplo fragmento do web.config.</span><span class="sxs-lookup"><span data-stu-id="67ce4-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a><span data-ttu-id="67ce4-214">toodelete um slot de implantação</span><span class="sxs-lookup"><span data-stu-id="67ce4-214">toodelete a deployment slot</span></span>
<span data-ttu-id="67ce4-215">Na folha de saudação para um slot de implantação, folha do slot de implantação Olá aberto, clique em **visão geral** (página de saudação padrão) e clique em **excluir** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-215">In hello blade for a deployment slot, open hello deployment slot's blade, click **Overview** (hello default page), and click **Delete** in hello command bar.</span></span>  

![Excluir um slot de implantação][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="67ce4-217">Cmdlets do PowerShell do Azure para slots de implantação</span><span class="sxs-lookup"><span data-stu-id="67ce4-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="67ce4-218">PowerShell do Azure é um módulo que fornece cmdlets toomanage Azure através do Windows PowerShell, incluindo suporte para gerenciar os slots de implantação no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ce4-218">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="67ce4-219">Para obter informações sobre como instalar e configurar o PowerShell do Azure e sobre a autenticação do Azure PowerShell com sua assinatura do Azure, consulte [como tooinstall e configurar o Microsoft Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="67ce4-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How tooinstall and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="67ce4-220">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="67ce4-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="67ce4-221">Criar um slot de implantação</span><span class="sxs-lookup"><span data-stu-id="67ce4-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a><span data-ttu-id="67ce4-222">Inicia uma troca de revisão (troca de várias fase) e aplique o slot de toosource de configuração de slot de destino</span><span class="sxs-lookup"><span data-stu-id="67ce4-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration toosource slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="67ce4-223">Cancelar uma troca pendente (troca com revisão) e restaurar a configuração do slot de origem</span><span class="sxs-lookup"><span data-stu-id="67ce4-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="67ce4-224">Permute slots de implantação</span><span class="sxs-lookup"><span data-stu-id="67ce4-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="67ce4-225">Exclua um slot de implantação</span><span class="sxs-lookup"><span data-stu-id="67ce4-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="67ce4-226">Comandos da interface de linha de comando do Azure (CLI do Azure) para slots de implantação</span><span class="sxs-lookup"><span data-stu-id="67ce4-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="67ce4-227">Olá CLI do Azure fornece comandos de plataforma cruzada para trabalhar com o Azure, incluindo suporte para o gerenciamento de slots de implantação do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="67ce4-227">hello Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="67ce4-228">Para obter instruções sobre como instalar e configurar o hello CLI do Azure, incluindo informações sobre como tooconnect CLI do Azure tooyour assinatura do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="67ce4-228">For instructions on installing and configuring hello Azure CLI, including information on how tooconnect Azure CLI tooyour Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="67ce4-229">comandos de saudação do toolist disponíveis para o serviço de aplicativo do Azure no hello CLI do Azure, chame `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="67ce4-229">toolist hello commands available for Azure App Service in hello Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="67ce4-230">Para obter os comandos da [CLI 2.0 do Azure](https://github.com/Azure/azure-cli) para slots de implantação, confira [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="67ce4-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="67ce4-231">azure site list</span><span class="sxs-lookup"><span data-stu-id="67ce4-231">azure site list</span></span>
<span data-ttu-id="67ce4-232">Para obter informações sobre aplicativos de saudação na assinatura atual hello, chame **a lista de sites do azure**, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-232">For information about hello apps in hello current subscription, call **azure site list**, as in hello following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="67ce4-233">azure site create</span><span class="sxs-lookup"><span data-stu-id="67ce4-233">azure site create</span></span>
<span data-ttu-id="67ce4-234">toocreate um slot de implantação, chame **criar site do azure** e especifique o nome de saudação de um aplicativo existente e nome de saudação do hello slot toocreate, como no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-234">toocreate a deployment slot, call **azure site create** and specify hello name of an existing app and hello name of hello slot toocreate, as in hello following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="67ce4-235">tooenable de controle de origem para o novo slot hello, use Olá **– git** opção, como no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-235">tooenable source control for hello new slot, use hello **--git** option, as in hello following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="67ce4-236">azure site swap</span><span class="sxs-lookup"><span data-stu-id="67ce4-236">azure site swap</span></span>
<span data-ttu-id="67ce4-237">toomake Olá aplicativo de produção de hello de slot de implantação atualizada, use Olá **troca de site do azure** comando tooperform uma operação de permuta, como no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-237">toomake hello updated deployment slot hello production app, use hello **azure site swap** command tooperform a swap operation, as in hello following example.</span></span> <span data-ttu-id="67ce4-238">aplicativo de produção de Hello não terá nenhum tempo de inatividade, nem passará uma inicialização a frio.</span><span class="sxs-lookup"><span data-stu-id="67ce4-238">hello production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="67ce4-239">azure site delete</span><span class="sxs-lookup"><span data-stu-id="67ce4-239">azure site delete</span></span>
<span data-ttu-id="67ce4-240">toodelete um slot de implantação que não é mais necessário, use Olá **exclusão de site do azure** comando, como no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-240">toodelete a deployment slot that is no longer needed, use hello **azure site delete** command, as in hello following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="67ce4-241">Veja um aplicativo Web em ação.</span><span class="sxs-lookup"><span data-stu-id="67ce4-241">See a web app in action.</span></span> <span data-ttu-id="67ce4-242">[Experimente o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/) imediatamente e crie um aplicativo inicializador de curta duração, sem necessidade de cartão de crédito e sem compromisso.</span><span class="sxs-lookup"><span data-stu-id="67ce4-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="67ce4-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="67ce4-243">Next Steps</span></span>
<span data-ttu-id="67ce4-244">[Azure serviço de aplicativo Web aplicativo – bloquear slots de implantação de produção toonon web access](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[tooApp Introdução serviço no Linux](./app-service-linux-intro.md)
[avaliação gratuita do Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="67ce4-244">[Azure App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction tooApp Service on Linux](./app-service-linux-intro.md)
[Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

