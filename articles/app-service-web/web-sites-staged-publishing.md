---
title: "Configurar ambientes de preparo para aplicativos Web no Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Saiba como usar a publicação em estágios para aplicativos Web no Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: ca27c55eaaceb3109b1450c550330dfc416fdf55
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="fed3a-103">Configurar ambientes de preparo no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="fed3a-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="fed3a-104">Ao implantar seu aplicativo Web, aplicativo Web no Linux, back-end móvel e aplicativo de API no [Serviço de Aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714), você pode implantar em um slot de implantação separado em vez de no slot de produção padrão quando estiver executando no modo do plano do Serviço de Aplicativo **Standard** ou **Premium**.</span><span class="sxs-lookup"><span data-stu-id="fed3a-104">When you deploy your web app, web app on Linux, mobile back end, and API app to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy to a separate deployment slot instead of the default production slot when running in the **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="fed3a-105">Os slots de implantação são, na verdade, aplicativos online com seus próprios nomes de host.</span><span class="sxs-lookup"><span data-stu-id="fed3a-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="fed3a-106">Os elementos de configurações e conteúdo de aplicativo podem ser trocados entre dois slots de implantação, incluindo o slot de produção.</span><span class="sxs-lookup"><span data-stu-id="fed3a-106">App content and configurations elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="fed3a-107">Implantar o seu aplicativo em um slot de implantação tem os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="fed3a-107">Deploying your application to a deployment slot has the following benefits:</span></span>

* <span data-ttu-id="fed3a-108">É possível validar as alterações no aplicativo em um slot de implantação de preparo antes de permutá-lo pelo slot de produção.</span><span class="sxs-lookup"><span data-stu-id="fed3a-108">You can validate app changes in a staging deployment slot before swapping it with the production slot.</span></span>
* <span data-ttu-id="fed3a-109">Implantar um aplicativo em um slot inicial e depois permutá-lo, enviando-o para produção, garante que todas as instâncias do slot estejam prontas antes dessa troca.</span><span class="sxs-lookup"><span data-stu-id="fed3a-109">Deploying an app to a slot first and swapping it into production ensures that all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="fed3a-110">Isso elimina o tempo de inatividade quando você for implantar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fed3a-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="fed3a-111">O redirecionamento do tráfego é contínuo e nenhuma solicitação é descartada como resultado de operações de permuta.</span><span class="sxs-lookup"><span data-stu-id="fed3a-111">The traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="fed3a-112">Todo esse fluxo de trabalho pode ser automatizado por meio da configuração de [Permuta Automática](#Auto-Swap) quando a validação de pré-permuta não é necessária.</span><span class="sxs-lookup"><span data-stu-id="fed3a-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="fed3a-113">Após a troca, o slot com o aplicativo de preparo anterior terá o aplicativo de produção anterior.</span><span class="sxs-lookup"><span data-stu-id="fed3a-113">After a swap, the slot with previously staged app now has the previous production app.</span></span> <span data-ttu-id="fed3a-114">Se as alterações permutadas no slot de produção não forem o que você esperava, é possível fazer a mesma permuta imediatamente para ter o "último site bom" de volta.</span><span class="sxs-lookup"><span data-stu-id="fed3a-114">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good site" back.</span></span>

<span data-ttu-id="fed3a-115">Cada modo de plano do Serviço de Aplicativo dá suporte a um número diferente de slots de implantação.</span><span class="sxs-lookup"><span data-stu-id="fed3a-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="fed3a-116">Para descobrir o número de slots ao qual seu aplicativo dá suporte, consulte [Preços do Serviço de Aplicativo](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="fed3a-116">To find out the number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="fed3a-117">Quando seu aplicativo tem vários slots, você não pode alterar o modo.</span><span class="sxs-lookup"><span data-stu-id="fed3a-117">When your app has multiple slots, you cannot change the mode.</span></span>
* <span data-ttu-id="fed3a-118">O dimensionamento não está disponível para slots de não produção.</span><span class="sxs-lookup"><span data-stu-id="fed3a-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="fed3a-119">O gerenciamento de recurso vinculado não tem suporte para slots de não produção.</span><span class="sxs-lookup"><span data-stu-id="fed3a-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="fed3a-120">Somente no [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715) você pode evitar esse impacto potencial em um slot de produção, mudando temporariamente o slot de não produção para um modo de plano do Serviço de Aplicativo diferente.</span><span class="sxs-lookup"><span data-stu-id="fed3a-120">In the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving the non-production slot to a different App Service plan mode.</span></span> <span data-ttu-id="fed3a-121">Observe que o slot de não produção deve uma vez mais compartilhar o mesmo modo com o slot de produção antes que você possa alternar os dois slots.</span><span class="sxs-lookup"><span data-stu-id="fed3a-121">Note that the non-production slot must once again share the same mode with the production slot before you can swap the two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="fed3a-122">Adicionar um slot de implantação</span><span class="sxs-lookup"><span data-stu-id="fed3a-122">Add a deployment slot</span></span>
<span data-ttu-id="fed3a-123">O aplicativo deve estar em execução no modo **Standard** ou **Premium** para que você habilite vários slots de implantação.</span><span class="sxs-lookup"><span data-stu-id="fed3a-123">The app must be running in the **Standard** or **Premium** mode in order for you to enable multiple deployment slots.</span></span>

1. <span data-ttu-id="fed3a-124">No [Portal do Azure](https://portal.azure.com/), abra a [folha de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources) de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fed3a-124">In the [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="fed3a-125">Escolha a opção **Slots de implantação** e clique em **Adicionar Slot**.</span><span class="sxs-lookup"><span data-stu-id="fed3a-125">Choose the **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Adicionar um novo slot de implantação][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="fed3a-127">Se o aplicativo ainda não estiver no modo **Standard** ou **Premium**, você receberá uma mensagem indicando os modos compatíveis para habilitar a publicação em etapas.</span><span class="sxs-lookup"><span data-stu-id="fed3a-127">If the app is not already in the **Standard** or **Premium** mode, you will receive a message indicating the supported modes for enabling staged publishing.</span></span> <span data-ttu-id="fed3a-128">Neste momento, você tem a opção de selecionar **Atualizar** e navegar para a guia **Escala** do aplicativo antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="fed3a-128">At this point, you have the option to select **Upgrade** and navigate to the **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="fed3a-129">Na folha **Adicionar um slot**, nomeie o slot e opte por clonar a configuração de aplicativo por meio de outro slot de implantação existente.</span><span class="sxs-lookup"><span data-stu-id="fed3a-129">In the **Add a slot** blade, give the slot a name, and select whether to clone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="fed3a-130">Clique na marca de seleção para continuar.</span><span class="sxs-lookup"><span data-stu-id="fed3a-130">Click the check mark to continue.</span></span>
   
    ![Fonte de configuração][ConfigurationSource1]
   
    <span data-ttu-id="fed3a-132">Na primeira vez em que você adicionar um slot, você terá somente duas opções: clonar configuração do slot padrão em produção ou não clonar.</span><span class="sxs-lookup"><span data-stu-id="fed3a-132">The first time you add a slot, you will only have two choices: clone configuration from the default slot in production or not at all.</span></span>
    <span data-ttu-id="fed3a-133">Se já tiver criado vários slots, você poderá clonar a configuração de um slot diferente do que estiver em produção:</span><span class="sxs-lookup"><span data-stu-id="fed3a-133">After you have created several slots, you will be able to clone configuration from a slot other than the one in production:</span></span>
   
    ![Fontes de configuração][MultipleConfigurationSources]
4. <span data-ttu-id="fed3a-135">Na folha de recursos do aplicativo, clique em **Slots de implantação**, clique em um slot de implantação para abrir a folha de recursos desse slot, que contém um conjunto de métricas e configuração como qualquer outro aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fed3a-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot to open that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="fed3a-136">O nome do slot é exibido na parte superior da folha para lembrar que você está visualizando o slot de implantação.</span><span class="sxs-lookup"><span data-stu-id="fed3a-136">The name of the slot is shown at the top of the blade to remind you that you are viewing the deployment slot.</span></span>
   
    ![Título do slot de implantação][StagingTitle]
5. <span data-ttu-id="fed3a-138">Clique na URL do aplicativo, na folha do slot.</span><span class="sxs-lookup"><span data-stu-id="fed3a-138">Click the app URL in the slot's blade.</span></span> <span data-ttu-id="fed3a-139">Observe que o slot de implantação tem seu próprio nome de host e também é um aplicativo em tempo real.</span><span class="sxs-lookup"><span data-stu-id="fed3a-139">Notice the deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="fed3a-140">Para limitar o acesso público ao slot de implantação, consulte [Aplicativo Web do Serviço de Aplicativo - bloquear acesso via Web a slots de implantação de não produção](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="fed3a-140">To limit public access to the deployment slot, see [App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="fed3a-141">Não há nenhum conteúdo após a criação do slot de implantação.</span><span class="sxs-lookup"><span data-stu-id="fed3a-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="fed3a-142">É possível implantar no slot a partir de uma ramificação diferente do repositório, ou mesmo de um repositório diferente.</span><span class="sxs-lookup"><span data-stu-id="fed3a-142">You can deploy to the slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="fed3a-143">Você também pode alterar a configuração do slot.</span><span class="sxs-lookup"><span data-stu-id="fed3a-143">You can also change the slot's configuration.</span></span> <span data-ttu-id="fed3a-144">Use o perfil de publicação ou as credenciais de implantação associadas ao slot de implantação para atualizar o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="fed3a-144">Use the publish profile or deployment credentials associated with the deployment slot for content updates.</span></span>  <span data-ttu-id="fed3a-145">Por exemplo, você pode [publicar neste slot com o git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="fed3a-145">For example, you can [publish to this slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="fed3a-146">Configuração de slots de implantação</span><span class="sxs-lookup"><span data-stu-id="fed3a-146">Configuration for deployment slots</span></span>
<span data-ttu-id="fed3a-147">Quando você clona a configuração de outro slot de implantação, a configuração clonada é editável.</span><span class="sxs-lookup"><span data-stu-id="fed3a-147">When you clone configuration from another deployment slot, the cloned configuration is editable.</span></span> <span data-ttu-id="fed3a-148">Além disso, alguns elementos de configuração seguirão o conteúdo em uma permuta (não específicos do slot) enquanto outros elementos de configuração permanecerão no mesmo slot após uma permuta (específicos do slot).</span><span class="sxs-lookup"><span data-stu-id="fed3a-148">Furthermore, some configuration elements will follow the content across a swap (not slot specific) while other configuration elements will stay in the same slot after a swap (slot specific).</span></span> <span data-ttu-id="fed3a-149">A lista a seguir mostra a configuração que será alterada com a permuta de slots.</span><span class="sxs-lookup"><span data-stu-id="fed3a-149">The following lists show the configuration that will change when you swap slots.</span></span>

<span data-ttu-id="fed3a-150">**Configurações que são permutadas**:</span><span class="sxs-lookup"><span data-stu-id="fed3a-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="fed3a-151">Configurações gerais - como a versão do framework, 32/64 bits, Web sockets</span><span class="sxs-lookup"><span data-stu-id="fed3a-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="fed3a-152">Configurações do aplicativo (podem ser configuradas para fixarem-se a um slot)</span><span class="sxs-lookup"><span data-stu-id="fed3a-152">App settings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="fed3a-153">Cadeias de conexão (podem ser configuradas para fixarem-se a um slot)</span><span class="sxs-lookup"><span data-stu-id="fed3a-153">Connection strings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="fed3a-154">Mapeamentos de manipulador</span><span class="sxs-lookup"><span data-stu-id="fed3a-154">Handler mappings</span></span>
* <span data-ttu-id="fed3a-155">Configurações de monitoramento e diagnóstico</span><span class="sxs-lookup"><span data-stu-id="fed3a-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="fed3a-156">Conteúdo de Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="fed3a-156">WebJobs content</span></span>

<span data-ttu-id="fed3a-157">**Configurações que não são permutadas**:</span><span class="sxs-lookup"><span data-stu-id="fed3a-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="fed3a-158">Pontos de extremidade de publicação</span><span class="sxs-lookup"><span data-stu-id="fed3a-158">Publishing endpoints</span></span>
* <span data-ttu-id="fed3a-159">Nomes de domínio personalizados</span><span class="sxs-lookup"><span data-stu-id="fed3a-159">Custom Domain Names</span></span>
* <span data-ttu-id="fed3a-160">Associações e certificados SSL</span><span class="sxs-lookup"><span data-stu-id="fed3a-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="fed3a-161">Configurações de escala</span><span class="sxs-lookup"><span data-stu-id="fed3a-161">Scale settings</span></span>
* <span data-ttu-id="fed3a-162">Agendadores de Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="fed3a-162">WebJobs schedulers</span></span>

<span data-ttu-id="fed3a-163">Para definir uma cadeia de conexão ou configuração de aplicativo a fim de fixar um slot (não trocado), acesse a folha **Configurações do aplicativo** de um slot específico e marque a caixa **Configuração do Slot** para os elementos de configuração que devem se fixar ao slot.</span><span class="sxs-lookup"><span data-stu-id="fed3a-163">To configure an app setting or connection string to stick to a slot (not swapped), access the **Application Settings** blade for a specific slot, then select the **Slot Setting** box for the configuration elements that should stick the slot.</span></span> <span data-ttu-id="fed3a-164">Observe que marcar um elemento de configuração como específico do slot tem o efeito de estabelecer esse elemento como não passível de troca, em todos os slots de implantação associados ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fed3a-164">Note that marking a configuration element as slot specific has the effect of establishing that element as not swappable across all the deployment slots associated with the app.</span></span>

![Configurações de slot][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="fed3a-166">Permute slots de implantação</span><span class="sxs-lookup"><span data-stu-id="fed3a-166">Swap deployment slots</span></span> 
<span data-ttu-id="fed3a-167">Você pode trocar os slots de implantação na exibição **Visão geral** ou **Slots de implantação** da folha de recursos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fed3a-167">You can swap deployment slots in the **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fed3a-168">Antes de trocar um aplicativo por meio de um slot de implantação para produção, verifique se todas as configurações específicas de slot estão configuradas exatamente como você deseja tê-las no destino da troca.</span><span class="sxs-lookup"><span data-stu-id="fed3a-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want to have it in the swap target.</span></span>
> 
> 

1. <span data-ttu-id="fed3a-169">Para trocar slots de implantação, clique no botão **Trocar** na barra de comandos do aplicativo ou na barra de comandos de um slot de implantação.</span><span class="sxs-lookup"><span data-stu-id="fed3a-169">To swap deployment slots, click the **Swap** button in the command bar of the app or in the command bar of a deployment slot.</span></span>
   
    ![Botão permutar][SwapButtonBar]

2. <span data-ttu-id="fed3a-171">Verifique se a origem e o destino da permuta estão definidos corretamente.</span><span class="sxs-lookup"><span data-stu-id="fed3a-171">Make sure that the swap source and swap target are set properly.</span></span> <span data-ttu-id="fed3a-172">Geralmente, o destino da troca é o slot de produção.</span><span class="sxs-lookup"><span data-stu-id="fed3a-172">Usually, the swap target is the production slot.</span></span> <span data-ttu-id="fed3a-173">Clique em **OK** para concluir a operação.</span><span class="sxs-lookup"><span data-stu-id="fed3a-173">Click **OK** to complete the operation.</span></span> <span data-ttu-id="fed3a-174">Quando a operação for concluída, os slots de implantação terão sido permutados.</span><span class="sxs-lookup"><span data-stu-id="fed3a-174">When the operation finishes, the deployment slots have been swapped.</span></span>

    ![Troca completa](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="fed3a-176">Para o tipo de troca **Troca com visualização**, veja [Troca com visualização (troca de várias fases)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="fed3a-176">For the **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="fed3a-177">Troca com visualização (troca de várias fases)</span><span class="sxs-lookup"><span data-stu-id="fed3a-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="fed3a-178">Troca com visualização, ou troca de várias fases, simplifica a validação de elementos de configuração específicos ao slot, como cadeias de conexão.</span><span class="sxs-lookup"><span data-stu-id="fed3a-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="fed3a-179">Para cargas de trabalho críticas, convém validar se o aplicativo está se comportando conforme o esperado quando a configuração do slot de produção é aplicada, e você deve executar essa validação *antes* de o aplicativo ser trocado para produção.</span><span class="sxs-lookup"><span data-stu-id="fed3a-179">For mission-critical workloads, you want to validate that the app behaves as expected when the production slot's configuration is applied, and you must perform such validation *before* the app is swapped into production.</span></span> <span data-ttu-id="fed3a-180">A troca com visualização é o que você precisa.</span><span class="sxs-lookup"><span data-stu-id="fed3a-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="fed3a-181">Não há suporte para a troca com visualização em aplicativos Web no Linux.</span><span class="sxs-lookup"><span data-stu-id="fed3a-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="fed3a-182">Quando você usa a opção **Troca com visualização** (consulte [Trocar slots de implantação](#Swap)), o Serviço de Aplicativo faz o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fed3a-182">When you use the **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does the following:</span></span>

- <span data-ttu-id="fed3a-183">Mantém o slot de destino inalterado para que a carga de trabalho existente nesse slot (por exemplo, produção) não seja afetada.</span><span class="sxs-lookup"><span data-stu-id="fed3a-183">Keeps the destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="fed3a-184">Aplica os elementos de configuração do slot de destino ao slot de origem, incluindo as configurações de aplicativo e as cadeias de conexão específicas ao slot.</span><span class="sxs-lookup"><span data-stu-id="fed3a-184">Applies the configuration elements of the destination slot to the source slot, including the slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="fed3a-185">Reinicia os processos de trabalho no slot de origem usando esses elementos de configuração mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fed3a-185">Restarts the worker processes on the source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="fed3a-186">Quando você conclui a troca: move o slot de origem pré-preparado para o slot de destino.</span><span class="sxs-lookup"><span data-stu-id="fed3a-186">When you complete the swap: Moves the pre-warmed-up source slot into the destination slot.</span></span> <span data-ttu-id="fed3a-187">O slot de destino é movido para o slot de origem como em uma troca manual.</span><span class="sxs-lookup"><span data-stu-id="fed3a-187">The destination slot is moved into the source slot as in a manual swap.</span></span>
- <span data-ttu-id="fed3a-188">Quando você cancela a troca: reaplica os elementos de configuração do slot de origem ao slot de origem.</span><span class="sxs-lookup"><span data-stu-id="fed3a-188">When you cancel the swap: Reapplies the configuration elements of the source slot to the source slot.</span></span>

<span data-ttu-id="fed3a-189">Você pode visualizar exatamente como o aplicativo se comportará com a configuração do slot de destino.</span><span class="sxs-lookup"><span data-stu-id="fed3a-189">You can preview exactly how the app will behave with the destination slot's configuration.</span></span> <span data-ttu-id="fed3a-190">Após a conclusão da validação, você poderá completar a troca em outra etapa.</span><span class="sxs-lookup"><span data-stu-id="fed3a-190">Once you complete validation, you complete the swap in a separate step.</span></span> <span data-ttu-id="fed3a-191">Essa etapa tem a vantagem adicional de que o slot de origem já está preparado com a configuração desejada, e os clientes não enfrentarão qualquer tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="fed3a-191">This step has the added advantage that the source slot is already warmed up with the desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="fed3a-192">Exemplos de cmdlets do Azure PowerShell disponíveis para permuta multifase são incluídos nos cmdlets do Azure PowerShell para a seção de slots de implantação.</span><span class="sxs-lookup"><span data-stu-id="fed3a-192">Samples for the Azure PowerShell cmdlets available for multi-phase swap are included in the Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="fed3a-193">Configurar a troca automática</span><span class="sxs-lookup"><span data-stu-id="fed3a-193">Configure Auto Swap</span></span>
<span data-ttu-id="fed3a-194">A Troca Automática simplifica cenários DevOps em q você deseja implantar continuamente seu aplicativo, sem nenhuma inicialização a frio nem tempo de inatividade para clientes finais do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fed3a-194">Auto Swap streamlines DevOps scenarios where you want to continuously deploy your app with zero cold start and zero downtime for end customers of the app.</span></span> <span data-ttu-id="fed3a-195">Quando um slot de implantação estiver configurado para Troca Automática para produção, sempre que você enviar por push a atualização de código para esse slot, o Serviço de Aplicativo trocará automaticamente o aplicativo para produção depois que ele já tiver feito sido preparado no slot.</span><span class="sxs-lookup"><span data-stu-id="fed3a-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update to that slot, App Service will automatically swap the app into production after it has already warmed up in the slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fed3a-196">Ao habilitar a Permuta Automática para um slot, verifique se a configuração do slot é exatamente a configuração pretendida para o slot de destino (geralmente o slot de produção).</span><span class="sxs-lookup"><span data-stu-id="fed3a-196">When you enable Auto Swap for a slot, make sure the slot configuration is exactly the configuration intended for the target slot (usually the production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="fed3a-197">Não há suporte para a troca automática em aplicativos Web no Linux.</span><span class="sxs-lookup"><span data-stu-id="fed3a-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="fed3a-198">Configurar a Permuta Automática para um slot é fácil.</span><span class="sxs-lookup"><span data-stu-id="fed3a-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="fed3a-199">Siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="fed3a-199">Follow the steps below:</span></span>

1. <span data-ttu-id="fed3a-200">Em **Slots de Implantação**, selecione um slot que não esteja em produção e escolha **Configurações do Aplicativo** na folha de recursos do slot.</span><span class="sxs-lookup"><span data-stu-id="fed3a-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="fed3a-201">Selecione **Ativar** para **Troca Automática**, escolha o slot de destino desejado em **Slot de Troca Automática** e clique em **Salvar** na barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="fed3a-201">Select **On** for **Auto Swap**, select the desired target slot in **Auto Swap Slot**, and click **Save** in the command bar.</span></span> <span data-ttu-id="fed3a-202">Verifique se a configuração para o slot é exatamente igual à configuração desejada para o slot de destino.</span><span class="sxs-lookup"><span data-stu-id="fed3a-202">Make sure configuration for the slot is exactly the configuration intended for the target slot.</span></span>
   
    <span data-ttu-id="fed3a-203">A guia **Notificações** piscará **SUCESSO** em verde quando a operação for concluída.</span><span class="sxs-lookup"><span data-stu-id="fed3a-203">The **Notifications** tab will flash a green **SUCCESS** once the operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="fed3a-204">Para testar a Troca Automática para seu aplicativo, primeiro você poderá selecionar um slot de destino que não seja de produção em **Slot de Troca Automática** para se familiarizar com o recurso.</span><span class="sxs-lookup"><span data-stu-id="fed3a-204">To test Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** to become familiar with the feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="fed3a-205">Execute um envio de código por push para esse slot de implantação.</span><span class="sxs-lookup"><span data-stu-id="fed3a-205">Execute a code push to that deployment slot.</span></span> <span data-ttu-id="fed3a-206">A Permuta Automática ocorrerá após um curto período de tempo e a atualização será refletida na URL do seu slot de destino.</span><span class="sxs-lookup"><span data-stu-id="fed3a-206">Auto Swap will happen after a short time and the update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="to-rollback-a-production-app-after-swap"></a><span data-ttu-id="fed3a-207">Para reverter um aplicativo de produção após a permuta</span><span class="sxs-lookup"><span data-stu-id="fed3a-207">To rollback a production app after swap</span></span>
<span data-ttu-id="fed3a-208">Se algum erro for identificado na produção após uma permuta de slot, reverta os slots para os estados pré-permuta permutando ambos os slots imediatamente.</span><span class="sxs-lookup"><span data-stu-id="fed3a-208">If any errors are identified in production after a slot swap, roll the slots back to their pre-swap states by swapping the same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="fed3a-209">Aquecimento personalizado antes da permuta</span><span class="sxs-lookup"><span data-stu-id="fed3a-209">Custom warm-up before swap</span></span>
<span data-ttu-id="fed3a-210">Alguns aplicativos podem exigir ações personalizadas de aquecimento.</span><span class="sxs-lookup"><span data-stu-id="fed3a-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="fed3a-211">O elemento de configuração `applicationInitialization` no web.config permite que você especifique ações de inicialização personalizadas a serem executadas antes de uma solicitação ser recebida.</span><span class="sxs-lookup"><span data-stu-id="fed3a-211">The `applicationInitialization` configuration element in web.config allows you to specify custom initialization actions to be performed before a request is received.</span></span> <span data-ttu-id="fed3a-212">A operação de permuta aguardará esse aquecimento personalizado ser concluído.</span><span class="sxs-lookup"><span data-stu-id="fed3a-212">The swap operation will wait for this custom warm-up to complete.</span></span> <span data-ttu-id="fed3a-213">Este é está um exemplo fragmento do web.config.</span><span class="sxs-lookup"><span data-stu-id="fed3a-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="to-delete-a-deployment-slot"></a><span data-ttu-id="fed3a-214">Para excluir um slot de implantação</span><span class="sxs-lookup"><span data-stu-id="fed3a-214">To delete a deployment slot</span></span>
<span data-ttu-id="fed3a-215">Na folha de um slot de implantação, abra a folha do slot de implantação, clique em **Visão geral** (a página padrão) e clique em **Excluir** na barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="fed3a-215">In the blade for a deployment slot, open the deployment slot's blade, click **Overview** (the default page), and click **Delete** in the command bar.</span></span>  

![Excluir um slot de implantação][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="fed3a-217">Cmdlets do PowerShell do Azure para slots de implantação</span><span class="sxs-lookup"><span data-stu-id="fed3a-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="fed3a-218">O Azure PowerShell é um módulo que fornece cmdlets para gerenciar o Azure por meio do Windows PowerShell, incluindo suporte ao gerenciamento de slots de implantação no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="fed3a-218">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="fed3a-219">Para obter mais informações sobre como instalar e configurar o PowerShell do Azure, e como autenticar o PowerShell do Azure com sua assinatura do Azure, consulte [Como instalar e configurar o PowerShell do Microsoft Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fed3a-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How to install and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="fed3a-220">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="fed3a-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="fed3a-221">Criar um slot de implantação</span><span class="sxs-lookup"><span data-stu-id="fed3a-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-to-source-slot"></a><span data-ttu-id="fed3a-222">Iniciar uma troca com revisão (troca de várias fases) e aplicar a configuração do slot de destino ao slot de origem</span><span class="sxs-lookup"><span data-stu-id="fed3a-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration to source slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="fed3a-223">Cancelar uma troca pendente (troca com revisão) e restaurar a configuração do slot de origem</span><span class="sxs-lookup"><span data-stu-id="fed3a-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="fed3a-224">Permute slots de implantação</span><span class="sxs-lookup"><span data-stu-id="fed3a-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="fed3a-225">Exclua um slot de implantação</span><span class="sxs-lookup"><span data-stu-id="fed3a-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="fed3a-226">Comandos da interface de linha de comando do Azure (CLI do Azure) para slots de implantação</span><span class="sxs-lookup"><span data-stu-id="fed3a-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="fed3a-227">A CLI do Azure fornece comandos entre plataformas para trabalhar com o Azure, incluindo suporte ao gerenciamento de slots de implantação do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fed3a-227">The Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="fed3a-228">Para obter instruções sobre como instalar e configurar a CLI do Azure, incluindo informações sobre como conectar a CLI do Azure com sua assinatura do Azure, consulte [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="fed3a-228">For instructions on installing and configuring the Azure CLI, including information on how to connect Azure CLI to your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="fed3a-229">Para listar os comandos disponíveis para o Serviço de Aplicativo do Azure na CLI do Azure, chame `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="fed3a-229">To list the commands available for Azure App Service in the Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="fed3a-230">Para obter os comandos da [CLI 2.0 do Azure](https://github.com/Azure/azure-cli) para slots de implantação, confira [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="fed3a-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="fed3a-231">azure site list</span><span class="sxs-lookup"><span data-stu-id="fed3a-231">azure site list</span></span>
<span data-ttu-id="fed3a-232">Para obter informações sobre aplicativos na assinatura atual, chame **azure site list**, como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="fed3a-232">For information about the apps in the current subscription, call **azure site list**, as in the following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="fed3a-233">azure site create</span><span class="sxs-lookup"><span data-stu-id="fed3a-233">azure site create</span></span>
<span data-ttu-id="fed3a-234">Para criar um slot de implantação, chame **azure site create** e especifique o nome de um aplicativo existente e o nome do slot para criar, como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="fed3a-234">To create a deployment slot, call **azure site create** and specify the name of an existing app and the name of the slot to create, as in the following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="fed3a-235">Para habilitar o controle do código-fonte para o novo slot, use a opção **--git** , como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="fed3a-235">To enable source control for the new slot, use the **--git** option, as in the following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="fed3a-236">azure site swap</span><span class="sxs-lookup"><span data-stu-id="fed3a-236">azure site swap</span></span>
<span data-ttu-id="fed3a-237">Para fazer com que o slot de implantação atualizado se torne o aplicativo de produção, use o comando **azure site swap** para executar uma operação de permuta, como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="fed3a-237">To make the updated deployment slot the production app, use the **azure site swap** command to perform a swap operation, as in the following example.</span></span> <span data-ttu-id="fed3a-238">O aplicativo de produção não passará por nenhuma experiência de tempo de inatividade, nem passará por uma inicialização a frio.</span><span class="sxs-lookup"><span data-stu-id="fed3a-238">The production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="fed3a-239">azure site delete</span><span class="sxs-lookup"><span data-stu-id="fed3a-239">azure site delete</span></span>
<span data-ttu-id="fed3a-240">Para excluir um slot de implantação que não seja mais necessário, use o comando **excluir de site azure** , como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="fed3a-240">To delete a deployment slot that is no longer needed, use the **azure site delete** command, as in the following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="fed3a-241">Veja um aplicativo Web em ação.</span><span class="sxs-lookup"><span data-stu-id="fed3a-241">See a web app in action.</span></span> <span data-ttu-id="fed3a-242">[Experimente o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/) imediatamente e crie um aplicativo inicializador de curta duração, sem necessidade de cartão de crédito e sem compromisso.</span><span class="sxs-lookup"><span data-stu-id="fed3a-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fed3a-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fed3a-243">Next Steps</span></span>
<span data-ttu-id="fed3a-244">[Aplicativo Web do Serviço de Aplicativo do Azure – bloquear o acesso via Web a slots de implantação de não produção](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introdução ao Serviço de Aplicativo no Linux](./app-service-linux-intro.md)
[Avaliação gratuita do Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="fed3a-244">[Azure App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction to App Service on Linux](./app-service-linux-intro.md)
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

