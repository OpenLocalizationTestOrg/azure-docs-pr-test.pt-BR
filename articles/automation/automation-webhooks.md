---
title: "um runbook de automação do Azure com um webhook de aaaStarting | Microsoft Docs"
description: "Um webhook que permite que um cliente toostart um runbook na automação do Azure de uma chamada HTTP.  Este artigo descreve como um webhook de toocreate e como toocall uma toostart um runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="0a09f-104">Iniciar um runbook de Automação do Azure com um webhook</span><span class="sxs-lookup"><span data-stu-id="0a09f-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="0a09f-105">Um *webhook* permite toostart um determinado runbook na automação do Azure por meio de uma única solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="0a09f-105">A *webhook* allows you toostart a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="0a09f-106">Isso permite que os serviços externos, como o Visual Studio Team Services, GitHub, análise de logs do Microsoft Operations Management Suite ou aplicativos personalizados toostart runbooks sem implementar uma solução completa usando Olá API de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a09f-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications toostart runbooks without implementing a full solution using hello Azure Automation API.</span></span>  
<span data-ttu-id="0a09f-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="0a09f-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="0a09f-108">Você pode comparar webhooks tooother métodos de iniciar um runbook [iniciando um runbook na automação do Azure](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="0a09f-108">You can compare webhooks tooother methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="0a09f-109">Detalhes de um webhook</span><span class="sxs-lookup"><span data-stu-id="0a09f-109">Details of a webhook</span></span>
<span data-ttu-id="0a09f-110">Olá, tabela a seguir descreve as propriedades de saudação que devem ser configuradas para um webhook.</span><span class="sxs-lookup"><span data-stu-id="0a09f-110">hello following table describes hello properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="0a09f-111">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0a09f-111">Property</span></span> | <span data-ttu-id="0a09f-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="0a09f-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0a09f-113">Nome</span><span class="sxs-lookup"><span data-stu-id="0a09f-113">Name</span></span> |<span data-ttu-id="0a09f-114">Você pode fornecer qualquer nome desejado para um webhook como essa é não exposta toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="0a09f-114">You can provide any name you want for a webhook since this is not exposed toohello client.</span></span>  <span data-ttu-id="0a09f-115">Ele é usado somente para você tooidentify Olá runbook na automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a09f-115">It is only used for you tooidentify hello runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="0a09f-116">Como prática recomendada, você deve dar Olá webhook um cliente de toohello relacionados de nome que irá usá-la.</span><span class="sxs-lookup"><span data-stu-id="0a09f-116">As a best practice, you should give hello webhook a name related toohello client that will use it.</span></span> |
| <span data-ttu-id="0a09f-117">URL</span><span class="sxs-lookup"><span data-stu-id="0a09f-117">URL</span></span> |<span data-ttu-id="0a09f-118">Olá URL de webhook Olá é vinculado de endereço exclusivo de saudação que um cliente chama com um runbook de saudação do HTTP POST toostart toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="0a09f-118">hello URL of hello webhook is hello unique address that a client calls with an HTTP POST toostart hello runbook linked toohello webhook.</span></span>  <span data-ttu-id="0a09f-119">Ele é gerado automaticamente quando você criar o webhook hello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-119">It is automatically generated when you create hello webhook.</span></span>  <span data-ttu-id="0a09f-120">Você não pode especificar uma URL personalizada.</span><span class="sxs-lookup"><span data-stu-id="0a09f-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="0a09f-121">Olá URL contém um token de segurança que permite Olá runbook toobe invocado por um sistema de terceiros com nenhuma autenticação adicional.</span><span class="sxs-lookup"><span data-stu-id="0a09f-121">hello URL contains a security token that allows hello runbook toobe invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="0a09f-122">Por esse motivo, ele deve ser tratado como uma senha.</span><span class="sxs-lookup"><span data-stu-id="0a09f-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="0a09f-123">Por motivos de segurança, você pode apenas Olá exibição que URL no hello portal do Azure em Olá tempo Olá webhook é criado.</span><span class="sxs-lookup"><span data-stu-id="0a09f-123">For security reasons, you can only view hello URL in hello Azure portal at hello time hello webhook is created.</span></span> <span data-ttu-id="0a09f-124">Você deve observar Olá URL em um local seguro para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="0a09f-124">You should note hello URL in a secure location for future use.</span></span> |
| <span data-ttu-id="0a09f-125">Data de validade</span><span class="sxs-lookup"><span data-stu-id="0a09f-125">Expiration date</span></span> |<span data-ttu-id="0a09f-126">Como um certificado, cada webhook tem uma data de validade após a qual ele não pode mais ser usado.</span><span class="sxs-lookup"><span data-stu-id="0a09f-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="0a09f-127">A data de validade pode ser modificada depois Olá webhook é criado.</span><span class="sxs-lookup"><span data-stu-id="0a09f-127">This expiration date can be modified after hello webhook is created.</span></span> |
| <span data-ttu-id="0a09f-128">habilitado</span><span class="sxs-lookup"><span data-stu-id="0a09f-128">Enabled</span></span> |<span data-ttu-id="0a09f-129">Um webhook é habilitado por padrão quando ele é criado.</span><span class="sxs-lookup"><span data-stu-id="0a09f-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="0a09f-130">Se você definir tooDisabled, nenhum cliente será capaz de toouse-lo.</span><span class="sxs-lookup"><span data-stu-id="0a09f-130">If you set it tooDisabled, then no client will be able toouse it.</span></span>  <span data-ttu-id="0a09f-131">Você pode definir Olá **habilitado** é criado quando você criar o webhook hello ou a qualquer momento uma vez.</span><span class="sxs-lookup"><span data-stu-id="0a09f-131">You can set hello **Enabled** property when you create hello webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="0a09f-132">parâmetros</span><span class="sxs-lookup"><span data-stu-id="0a09f-132">Parameters</span></span>
<span data-ttu-id="0a09f-133">Um webhook pode definir valores para parâmetros de runbook que são usados quando Olá runbook for iniciado por esse webhook.</span><span class="sxs-lookup"><span data-stu-id="0a09f-133">A webhook can define values for runbook parameters that are used when hello runbook is started by that webhook.</span></span> <span data-ttu-id="0a09f-134">Olá webhook deve incluir valores para todos os parâmetros obrigatórios de runbook hello e pode incluir valores de parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="0a09f-134">hello webhook must include values for any mandatory parameters of hello runbook and may include values for optional parameters.</span></span> <span data-ttu-id="0a09f-135">Um webhook de tooa do valor configurado de parâmetro pode ser modificado até mesmo depois de criar webhoook hello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-135">A parameter value configured tooa webhook can be modified even after creating hello webhoook.</span></span> <span data-ttu-id="0a09f-136">Vários webhooks vinculado tooa único runbook pode usar valores de parâmetros diferentes.</span><span class="sxs-lookup"><span data-stu-id="0a09f-136">Multiple webhooks linked tooa single runbook can each use different parameter values.</span></span>

<span data-ttu-id="0a09f-137">Quando um cliente inicia um runbook usando um webhook, ele não pode substituir valores de parâmetro de saudação definidos no hello webhook.</span><span class="sxs-lookup"><span data-stu-id="0a09f-137">When a client starts a runbook using a webhook, it cannot override hello parameter values defined in hello webhook.</span></span>  <span data-ttu-id="0a09f-138">tooreceive dados de cliente hello, Olá runbook pode aceitar um parâmetro único chamado **$WebhookData** do tipo [object] que contém dados que o cliente Olá inclui na solicitação POST hello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-138">tooreceive data from hello client, hello runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that hello client includes in hello POST request.</span></span>

![Propriedades de Webhookdata](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="0a09f-140">Olá **$WebhookData** objeto terá Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a09f-140">hello **$WebhookData** object will have hello following properties:</span></span>

| <span data-ttu-id="0a09f-141">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0a09f-141">Property</span></span> | <span data-ttu-id="0a09f-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="0a09f-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0a09f-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="0a09f-143">WebhookName</span></span> |<span data-ttu-id="0a09f-144">nome de saudação do webhook hello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-144">hello name of hello webhook.</span></span> |
| <span data-ttu-id="0a09f-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="0a09f-145">RequestHeader</span></span> |<span data-ttu-id="0a09f-146">Tabela de hash que contém Olá cabeçalhos de solicitação POST de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-146">Hash table containing hello headers of hello incoming POST request.</span></span> |
| <span data-ttu-id="0a09f-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="0a09f-147">RequestBody</span></span> |<span data-ttu-id="0a09f-148">corpo de saudação de solicitação POST de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-148">hello body of hello incoming POST request.</span></span>  <span data-ttu-id="0a09f-149">Isso manterá qualquer formatação, como a cadeia de caracteres, JSON, XML ou os dados codificados de formulário.</span><span class="sxs-lookup"><span data-stu-id="0a09f-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="0a09f-150">Olá runbook deve ser escrito toowork com formato de dados de saudação é esperado.</span><span class="sxs-lookup"><span data-stu-id="0a09f-150">hello runbook must be written toowork with hello data format that is expected.</span></span> |

<span data-ttu-id="0a09f-151">Não há nenhuma configuração de Olá webhook toosupport necessário Olá **$WebhookData** parâmetro, e Olá runbook não é necessário tooaccept-lo.</span><span class="sxs-lookup"><span data-stu-id="0a09f-151">There is no configuration of hello webhook required toosupport hello **$WebhookData** parameter, and hello runbook is not required tooaccept it.</span></span>  <span data-ttu-id="0a09f-152">Se o runbook Olá não define parâmetro hello, quaisquer detalhes de solicitação de saudação enviada do cliente de saudação é ignorado.</span><span class="sxs-lookup"><span data-stu-id="0a09f-152">If hello runbook does not define hello parameter, then any details of hello request sent from hello client is ignored.</span></span>

<span data-ttu-id="0a09f-153">Se você especificar um valor para $WebhookData quando você cria o webhook hello, esse valor será substituída quando webhook Olá Olá runbook é iniciado com dados de saudação da solicitação POST do cliente Olá, mesmo se o cliente Olá não inclui todos os dados no corpo da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a09f-153">If you specify a value for $WebhookData when you create hello webhook, that value will be overriden when hello webhook starts hello runbook with hello data from hello client POST request, even if hello client does not include any data in hello request body.</span></span>  <span data-ttu-id="0a09f-154">Se você iniciar um runbook com $WebhookData usando um método que não seja um webhook, você pode fornecer um valor para $Webhookdata será reconhecido pelo runbook hello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by hello runbook.</span></span>  <span data-ttu-id="0a09f-155">Esse valor deve ser um objeto com hello mesmo [propriedades](#details-of-a-webhook) como $Webhookdata para esse runbook Olá possa funcionar corretamente com ele como se ele estava trabalhando com WebhookData real passado por um webhook.</span><span class="sxs-lookup"><span data-stu-id="0a09f-155">This value should be an object with hello same [properties](#details-of-a-webhook) as $Webhookdata so that hello runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="0a09f-156">Por exemplo, se você estiver iniciando Olá após o runbook Olá Portal do Azure e deseja toopass alguns exemplos de WebhookData para teste, como WebhookData é um objeto, ele deve ser passado como JSON em Olá da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="0a09f-156">For example, if you are starting hello following runbook from hello Azure Portal and want toopass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in hello UI.</span></span>

![Parâmetro WebhookData da interface do usuário](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="0a09f-158">Para Olá acima runbook, se você tiver Olá seguintes propriedades para o parâmetro de WebhookData hello:</span><span class="sxs-lookup"><span data-stu-id="0a09f-158">For hello above runbook, if you have hello following properties for hello WebhookData parameter:</span></span>

1. <span data-ttu-id="0a09f-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="0a09f-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="0a09f-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="0a09f-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="0a09f-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="0a09f-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="0a09f-162">Em seguida, você passaria Olá valor JSON em hello da interface do usuário para o parâmetro de WebhookData hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a09f-162">Then you would pass hello following JSON value in hello UI for hello WebhookData parameter:</span></span>  

* <span data-ttu-id="0a09f-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="0a09f-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Iniciar o parâmetro WebhookData na interface do usuário](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="0a09f-165">os valores de todos os parâmetros de entrada Hello são registrados com o trabalho de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-165">hello values of all input parameters are logged with hello runbook job.</span></span>  <span data-ttu-id="0a09f-166">Isso significa que qualquer entrada fornecida pelo cliente Olá na solicitação de webhook hello serão tooanyone conectado e disponível com o trabalho de automação de toohello de acesso.</span><span class="sxs-lookup"><span data-stu-id="0a09f-166">This means that any input provided by hello client in hello webhook request will be logged and available tooanyone with access toohello automation job.</span></span>  <span data-ttu-id="0a09f-167">Por esse motivo, você deve ter cuidado ao incluir informações confidenciais em chamadas webhook.</span><span class="sxs-lookup"><span data-stu-id="0a09f-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="0a09f-168">Segurança</span><span class="sxs-lookup"><span data-stu-id="0a09f-168">Security</span></span>
<span data-ttu-id="0a09f-169">segurança de saudação de um webhook depende de privacidade Olá de sua URL que contém um token de segurança que lhe permite toobe invocado.</span><span class="sxs-lookup"><span data-stu-id="0a09f-169">hello security of a webhook relies on hello privacy of its URL which contains a security token that allows it toobe invoked.</span></span> <span data-ttu-id="0a09f-170">Automação do Azure não executa nenhuma autenticação na solicitação Olá desde que ela se torna a URL correta do toohello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-170">Azure Automation does not perform any authentication on hello request as long as it is made toohello correct URL.</span></span> <span data-ttu-id="0a09f-171">Por esse motivo, webhooks não deve ser usado para runbooks que executam funções altamente confidenciais sem usar um meio alternativo de validação de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a09f-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating hello request.</span></span>

<span data-ttu-id="0a09f-172">Você pode incluir lógica no hello runbook toodetermine que foi chamada por um webhook verificando Olá **WebhookName** propriedade do parâmetro hello $WebhookData.</span><span class="sxs-lookup"><span data-stu-id="0a09f-172">You can include logic within hello runbook toodetermine that it was called by a webhook by checking hello **WebhookName** property of hello $WebhookData parameter.</span></span> <span data-ttu-id="0a09f-173">Olá runbook pode executar uma validação adicional, procurando por informações específicas no hello **RequestHeader** ou **RequestBody** propriedades.</span><span class="sxs-lookup"><span data-stu-id="0a09f-173">hello runbook could perform further validation by looking for particular information in hello **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="0a09f-174">Outra estratégia é toohave Olá runbook executar alguma validação de uma condição externa quando ele recebeu uma solicitação de webhook.</span><span class="sxs-lookup"><span data-stu-id="0a09f-174">Another strategy is toohave hello runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="0a09f-175">Por exemplo, considere um runbook que é chamado pelo GitHub sempre que há um novo repositório GitHub de tooa confirmação.</span><span class="sxs-lookup"><span data-stu-id="0a09f-175">For example, consider a runbook that is called by GitHub whenever there is a new commit tooa GitHub repository.</span></span>  <span data-ttu-id="0a09f-176">Olá runbook pode se conectar a toovalidate tooGitHub que uma nova confirmação apenas ocorreu antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="0a09f-176">hello runbook might connect tooGitHub toovalidate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="0a09f-177">Criando um webhook</span><span class="sxs-lookup"><span data-stu-id="0a09f-177">Creating a webhook</span></span>
<span data-ttu-id="0a09f-178">Use Olá seguindo o procedimento toocreate um novo runbook tooa webhook vinculado no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a09f-178">Use hello following procedure toocreate a new webhook linked tooa runbook in hello Azure portal.</span></span>

1. <span data-ttu-id="0a09f-179">De saudação **Runbooks folha** no hello portal do Azure, clique em runbook Olá Olá webhook iniciar tooview folha seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="0a09f-179">From hello **Runbooks blade** in hello Azure portal, click hello runbook that hello webhook will start tooview its detail blade.</span></span>
2. <span data-ttu-id="0a09f-180">Clique em **Webhook** na parte superior da saudação de saudação do hello folha tooopen **Webhook adicionar** folha.</span><span class="sxs-lookup"><span data-stu-id="0a09f-180">Click **Webhook** at hello top of hello blade tooopen hello **Add Webhook** blade.</span></span> <br><span data-ttu-id="0a09f-181">
   ![Botão Webhooks](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="0a09f-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="0a09f-182">Clique em **criar nova webhook** tooopen Olá **criar folha de webhook**.</span><span class="sxs-lookup"><span data-stu-id="0a09f-182">Click **Create new webhook** tooopen hello **Create webhook blade**.</span></span>
4. <span data-ttu-id="0a09f-183">Especifique um **nome**, **data de expiração** para webhook hello e se ele deve ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="0a09f-183">Specify a **Name**, **Expiration Date** for hello webhook and whether it should be enabled.</span></span> <span data-ttu-id="0a09f-184">Consulte [Detalhes de um webhook](#details-of-a-webhook) para obter mais informações sobre essas propriedades.</span><span class="sxs-lookup"><span data-stu-id="0a09f-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="0a09f-185">Clique Olá ícone para copiar e pressione Ctrl + C toocopy Olá URL de webhook hello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-185">Click hello copy icon and press Ctrl+C toocopy hello URL of hello webhook.</span></span>  <span data-ttu-id="0a09f-186">Em seguida, anote-o em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="0a09f-186">Then record it in a safe place.</span></span>  <span data-ttu-id="0a09f-187">**Depois de criar o webhook hello, você não pode recuperar a URL de saudação novamente.**</span><span class="sxs-lookup"><span data-stu-id="0a09f-187">**Once you create hello webhook, you cannot retrieve hello URL again.**</span></span> <br><span data-ttu-id="0a09f-188">
   ![URL de Webhook](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="0a09f-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="0a09f-189">Clique em **parâmetros** tooprovide valores para parâmetros de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-189">Click **Parameters** tooprovide values for hello runbook parameters.</span></span>  <span data-ttu-id="0a09f-190">Se Olá runbook tiver parâmetros obrigatórios, em seguida, não será capaz de toocreate Olá webhook, a menos que os valores são fornecidos.</span><span class="sxs-lookup"><span data-stu-id="0a09f-190">If hello runbook has mandatory parameters, then you will not be able toocreate hello webhook unless values are provided.</span></span>
7. <span data-ttu-id="0a09f-191">Clique em **criar** toocreate Olá webhook.</span><span class="sxs-lookup"><span data-stu-id="0a09f-191">Click **Create** toocreate hello webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="0a09f-192">Usando um webhook</span><span class="sxs-lookup"><span data-stu-id="0a09f-192">Using a webhook</span></span>
<span data-ttu-id="0a09f-193">toouse um webhook após ela ter sido criada, seu aplicativo cliente deverá emitir um HTTP POST com URL Olá Olá webhook.</span><span class="sxs-lookup"><span data-stu-id="0a09f-193">toouse a webhook after it has been created, your client application must issue an HTTP POST with hello URL for hello webhook.</span></span>  <span data-ttu-id="0a09f-194">sintaxe de saudação do webhook Olá será em Olá formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="0a09f-194">hello syntax of hello webhook will be in hello following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="0a09f-195">cliente Olá receberá uma das Olá seguindo códigos de retorno da solicitação POST hello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-195">hello client will receive one of hello following return codes from hello POST request.</span></span>  

| <span data-ttu-id="0a09f-196">Código</span><span class="sxs-lookup"><span data-stu-id="0a09f-196">Code</span></span> | <span data-ttu-id="0a09f-197">Texto</span><span class="sxs-lookup"><span data-stu-id="0a09f-197">Text</span></span> | <span data-ttu-id="0a09f-198">Descrição</span><span class="sxs-lookup"><span data-stu-id="0a09f-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0a09f-199">202</span><span class="sxs-lookup"><span data-stu-id="0a09f-199">202</span></span> |<span data-ttu-id="0a09f-200">Aceita</span><span class="sxs-lookup"><span data-stu-id="0a09f-200">Accepted</span></span> |<span data-ttu-id="0a09f-201">Olá solicitação foi aceita e Olá runbook foi enfileirada com êxito.</span><span class="sxs-lookup"><span data-stu-id="0a09f-201">hello request was accepted, and hello runbook was successfully queued.</span></span> |
| <span data-ttu-id="0a09f-202">400</span><span class="sxs-lookup"><span data-stu-id="0a09f-202">400</span></span> |<span data-ttu-id="0a09f-203">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="0a09f-203">Bad Request</span></span> |<span data-ttu-id="0a09f-204">solicitação de saudação não foi aceita para uma saudação motivos a seguir.</span><span class="sxs-lookup"><span data-stu-id="0a09f-204">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="0a09f-205">Olá webhook expirou.</span><span class="sxs-lookup"><span data-stu-id="0a09f-205">hello webhook has expired.</span></span></li> <li><span data-ttu-id="0a09f-206">Olá webhook está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="0a09f-206">hello webhook is disabled.</span></span></li> <li><span data-ttu-id="0a09f-207">token Olá Olá URL é inválido.</span><span class="sxs-lookup"><span data-stu-id="0a09f-207">hello token in hello URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="0a09f-208">404</span><span class="sxs-lookup"><span data-stu-id="0a09f-208">404</span></span> |<span data-ttu-id="0a09f-209">Não encontrado</span><span class="sxs-lookup"><span data-stu-id="0a09f-209">Not Found</span></span> |<span data-ttu-id="0a09f-210">solicitação de saudação não foi aceita para uma saudação motivos a seguir.</span><span class="sxs-lookup"><span data-stu-id="0a09f-210">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="0a09f-211">Olá webhook não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="0a09f-211">hello webhook was not found.</span></span></li> <li><span data-ttu-id="0a09f-212">Olá runbook não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="0a09f-212">hello runbook was not found.</span></span></li> <li><span data-ttu-id="0a09f-213">Olá conta não foi encontrada.</span><span class="sxs-lookup"><span data-stu-id="0a09f-213">hello account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="0a09f-214">500</span><span class="sxs-lookup"><span data-stu-id="0a09f-214">500</span></span> |<span data-ttu-id="0a09f-215">Erro interno do servidor</span><span class="sxs-lookup"><span data-stu-id="0a09f-215">Internal Server Error</span></span> |<span data-ttu-id="0a09f-216">Olá URL era válida, mas ocorreu um erro.</span><span class="sxs-lookup"><span data-stu-id="0a09f-216">hello URL was valid, but an error occurred.</span></span>  <span data-ttu-id="0a09f-217">Reenvie a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a09f-217">Please resubmit hello request.</span></span> |

<span data-ttu-id="0a09f-218">Supondo que Olá solicitação for bem-sucedida, resposta de webhook Olá contém id de trabalho Olá no formato JSON da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="0a09f-218">Assuming hello request is successful, hello webhook response contains hello job id in JSON format as follows.</span></span> <span data-ttu-id="0a09f-219">Ele conterá uma id de trabalho único, mas o formato JSON de saudação permite possíveis aprimoramentos futuros.</span><span class="sxs-lookup"><span data-stu-id="0a09f-219">It will contain a single job id, but hello JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="0a09f-220">cliente Olá não pode determinar quando conclui o trabalho de runbook hello ou seu status de conclusão de webhook hello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-220">hello client cannot determine when hello runbook job completes or its completion status from hello webhook.</span></span>  <span data-ttu-id="0a09f-221">Ele pode determinar essas informações usando a id do trabalho Olá com outro método, como [do Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) ou hello [API de automação do Azure](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a09f-221">It can determine this information using hello job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or hello [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="0a09f-222">Exemplo</span><span class="sxs-lookup"><span data-stu-id="0a09f-222">Example</span></span>
<span data-ttu-id="0a09f-223">Olá exemplo a seguir usa o Windows PowerShell toostart um runbook com um webhook.</span><span class="sxs-lookup"><span data-stu-id="0a09f-223">hello following example uses Windows PowerShell toostart a runbook with a webhook.</span></span>  <span data-ttu-id="0a09f-224">Observe que qualquer linguagem que possa fazer uma solicitação HTTP pode usar um webhook; o Windows PowerShell é usado aqui apenas como um exemplo.</span><span class="sxs-lookup"><span data-stu-id="0a09f-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="0a09f-225">Olá runbook está esperando uma lista de máquinas virtuais formatada em JSON no corpo de saudação de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a09f-225">hello runbook is expecting a list of virtual machines formatted in JSON in hello body of hello request.</span></span> <span data-ttu-id="0a09f-226">Também incluímos informações sobre quem está iniciando runbook Olá Olá e data que ele está sendo iniciado no cabeçalho de saudação de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a09f-226">We also are including information about who is starting hello runbook and hello date and time it is being started in hello header of hello request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="0a09f-227">Olá, imagem a seguir mostra as informações de cabeçalho de saudação (usando um [Fiddler](http://www.telerik.com/fiddler) rastreamento) desta solicitação.</span><span class="sxs-lookup"><span data-stu-id="0a09f-227">hello following image shows hello header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="0a09f-228">Isso inclui cabeçalhos padrão de uma solicitação HTTP em adição toohello personalizado de data e dos cabeçalhos que foi adicionada.</span><span class="sxs-lookup"><span data-stu-id="0a09f-228">This includes standard headers of an HTTP request in addition toohello custom Date and From headers that we added.</span></span>  <span data-ttu-id="0a09f-229">Cada um desses valores é runbook toohello disponíveis no hello **RequestHeaders** propriedade **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="0a09f-229">Each of these values is available toohello runbook in hello **RequestHeaders** property of **WebhookData**.</span></span>

![Botão Webhooks](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="0a09f-231">Olá, imagem a seguir mostra Olá corpo da solicitação de saudação (usando um [Fiddler](http://www.telerik.com/fiddler) rastreamento) que é toohello disponível runbook no hello **RequestBody** propriedade de **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="0a09f-231">hello following image shows hello body of hello request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available toohello runbook in hello **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="0a09f-232">Isso é formatado como JSON, pois esse era o formato de saudação que foi incluído no corpo de saudação de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a09f-232">This is formatted as JSON because that was hello format that was included in hello body of hello request.</span></span>     

![Botão Webhooks](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="0a09f-234">Olá imagem a seguir mostra solicitação Olá enviada do Windows PowerShell e a resposta resultante de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a09f-234">hello following image shows hello request being sent from Windows PowerShell and hello resulting response.</span></span>  <span data-ttu-id="0a09f-235">id do trabalho Olá é extraído da resposta hello e cadeia de caracteres tooa convertido.</span><span class="sxs-lookup"><span data-stu-id="0a09f-235">hello job id is extracted from hello response and converted tooa string.</span></span>

![Botão Webhooks](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="0a09f-237">Olá seguinte exemplo de runbook aceita a solicitação anterior de exemplo hello e inicia a máquinas virtuais de saudação especificadas no corpo da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a09f-237">hello following sample runbook accepts hello previous example request and starts hello virtual machines specified in hello request body.</span></span>

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate tooAzure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a><span data-ttu-id="0a09f-238">Iniciar runbooks em alertas de tooAzure de resposta</span><span class="sxs-lookup"><span data-stu-id="0a09f-238">Starting runbooks in response tooAzure alerts</span></span>
<span data-ttu-id="0a09f-239">Runbooks de Webhook pode ser usado tooreact muito[alertas do Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="0a09f-239">Webhook-enabled runbooks can be used tooreact too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="0a09f-240">Recursos do Azure podem ser monitorados por coletar estatísticas de saudação como desempenho, disponibilidade e o uso com a Ajuda de saudação de alertas do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a09f-240">Resources in Azure can be monitored by collecting hello statistics like performance, availability and usage with hello help of Azure alerts.</span></span> <span data-ttu-id="0a09f-241">Você pode receber um alerta com base em métricas de monitoramento ou em eventos para seus recursos do Azure. No momento, as Contas de Automação oferecem suporte apenas para métricas.</span><span class="sxs-lookup"><span data-stu-id="0a09f-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="0a09f-242">Quando o valor de saudação de uma métrica especificada excede limite Olá atribuído ou se Olá configurado evento é disparado uma notificação é enviada toohello serviço admin coadministradores tooresolve Olá alerta ou, para obter mais informações sobre as métricas e eventos, consulte muito[ Alertas do Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="0a09f-242">When hello value of a specified metric exceeds hello threshold assigned or if hello configured event is triggered then a notification is sent toohello service admin or co-admins tooresolve hello alert, for more information on metrics and events please refer too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="0a09f-243">Além de usar os alertas do Azure como um sistema de notificação, você também pode disparar runbooks no tooalerts de resposta.</span><span class="sxs-lookup"><span data-stu-id="0a09f-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response tooalerts.</span></span> <span data-ttu-id="0a09f-244">Automação do Azure fornece Olá recurso toorun habilitado webhook runbooks com alertas do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a09f-244">Azure Automation provides hello capability toorun webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="0a09f-245">Quando uma métrica excede Olá configurado valor de limite de regra de alerta de saudação se torna ativa e gatilhos Olá webhook de automação que por sua vez executa runbook hello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-245">When a metric exceeds hello configured threshold value then hello alert rule becomes active and triggers hello automation webhook which in turn executes hello runbook.</span></span>

![Webhooks](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="0a09f-247">Contexto do alerta</span><span class="sxs-lookup"><span data-stu-id="0a09f-247">Alert context</span></span>
<span data-ttu-id="0a09f-248">Considere um recurso do Azure como uma máquina virtual, a utilização da CPU do computador é uma métrica de desempenho chave hello.</span><span class="sxs-lookup"><span data-stu-id="0a09f-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of hello key performance metric.</span></span> <span data-ttu-id="0a09f-249">Se Olá utilização da CPU é 100% ou mais de uma determinada quantidade por longo período de tempo, talvez seja o problema de saudação do toorestart Olá máquina virtual toofix.</span><span class="sxs-lookup"><span data-stu-id="0a09f-249">If hello CPU utilization is 100% or more than a certain amount for long period of time, you might want toorestart hello virtual machine toofix hello problem.</span></span> <span data-ttu-id="0a09f-250">Isso pode ser resolvido por meio da configuração de uma máquina de virtual toohello regra de alerta e essa regra usa a porcentagem de CPU como sua métrica.</span><span class="sxs-lookup"><span data-stu-id="0a09f-250">This can be solved by configuring an alert rule toohello virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="0a09f-251">Porcentagem de CPU é aceito apenas como um exemplo, mas há muitas outras métricas que você pode configurar tooyour Azure recursos e reiniciar a máquina virtual de saudação é uma ação que é feito toofix esse problema, você pode configurar Olá runbook tootake outras ações.</span><span class="sxs-lookup"><span data-stu-id="0a09f-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure tooyour Azure resources and restarting hello virtual machine is an action that is taken toofix this issue, you can configure hello runbook tootake other actions.</span></span>

<span data-ttu-id="0a09f-252">Quando esta regra de alerta de saudação se torna ativa e gatilhos Olá runbook webhook habilitado, ele envia Olá contexto de alerta toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="0a09f-252">When this hello alert rule becomes active and triggers hello webhook-enabled runbook, it sends hello alert context toohello runbook.</span></span> <span data-ttu-id="0a09f-253">[Contexto de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contém os detalhes incluindo **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** e **Timestamp** que são necessário para o recurso de saudação do hello runbook tooidentify em que ele irá realizar ação.</span><span class="sxs-lookup"><span data-stu-id="0a09f-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span> <span data-ttu-id="0a09f-254">Alerta de contexto é inserido na parte de corpo de saudação do hello **WebhookData** toohello enviados runbook do objeto e pode ser acessado com **Webhook.RequestBody** propriedade</span><span class="sxs-lookup"><span data-stu-id="0a09f-254">Alert context is embedded in hello body part of hello **WebhookData** object sent toohello runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="0a09f-255">Exemplo</span><span class="sxs-lookup"><span data-stu-id="0a09f-255">Example</span></span>
<span data-ttu-id="0a09f-256">Criar uma máquina virtual do Azure em sua assinatura e associar um [toomonitor CPU Porcentagem métrica de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="0a09f-256">Create an Azure virtual machine in your subscription and associate an [alert toomonitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="0a09f-257">Durante a criação de alerta de saudação Verifique se que você preencher o campo de webhook de saudação com hello URL de webhook Olá que foi gerada ao criar o webhook Olá.</span><span class="sxs-lookup"><span data-stu-id="0a09f-257">While creating hello alert make sure you populate hello webhook field with hello URL of hello webhook which was generated while creating hello webhook.</span></span>

<span data-ttu-id="0a09f-258">seguinte exemplo de runbook Hello é disparado quando a regra de alerta de saudação se torna ativa e coleta parâmetros de contexto de alerta de saudação que são necessários para o recurso de saudação do hello runbook tooidentify em que ele irá realizar ação.</span><span class="sxs-lookup"><span data-stu-id="0a09f-258">hello following sample runbook is triggered when hello alert rule becomes active and it collects hello Alert context parameters which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span>

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="0a09f-259">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0a09f-259">Next steps</span></span>
* <span data-ttu-id="0a09f-260">Para obter detalhes sobre diferentes maneiras toostart um runbook, consulte [iniciando um Runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="0a09f-260">For details on different ways toostart a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="0a09f-261">Para obter informações sobre Olá exibindo Status de um Runbook Job, consulte muito[execução de Runbook na automação do Azure](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="0a09f-261">For information on viewing hello Status of a Runbook Job, refer too[Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="0a09f-262">toolearn como toouse ação de tootake de automação do Azure em alertas do Azure, consulte [corrigir alertas de VM do Azure com Runbooks de automação](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="0a09f-262">toolearn how toouse Azure Automation tootake action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
