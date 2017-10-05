---
title: "Iniciar um runbook de Automação do Azure com um webhook | Microsoft Docs"
description: "Um webhook que permite que um cliente inicie um runbook na Automação do Azure a partir de uma chamada HTTP.  Este artigo descreve como criar um webhook e como chamar um para iniciar um runbook."
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
ms.openlocfilehash: 6c65427fcd18e41a90dfb872aa9525f758b17b87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="faf47-104">Iniciar um runbook de Automação do Azure com um webhook</span><span class="sxs-lookup"><span data-stu-id="faf47-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="faf47-105">O *webhook* permite que você inicie um runbook específico na Automação do Azure por meio de uma única solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="faf47-105">A *webhook* allows you to start a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="faf47-106">Isso permite que os serviços externos, como o Visual Studio Team Services, GitHub, Microsoft Operations Management Suite, Log Analytics ou aplicativos personalizados iniciem runbooks sem implementar uma solução completa usando a API da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="faf47-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications to start runbooks without implementing a full solution using the Azure Automation API.</span></span>  
<span data-ttu-id="faf47-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="faf47-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="faf47-108">Você pode comparar os webhooks a outros métodos para iniciar um runbook em [Como iniciar um Runbook na Automação do Azure](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="faf47-108">You can compare webhooks to other methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="faf47-109">Detalhes de um webhook</span><span class="sxs-lookup"><span data-stu-id="faf47-109">Details of a webhook</span></span>
<span data-ttu-id="faf47-110">A tabela a seguir descreve as propriedades que devem ser configuradas para um webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-110">The following table describes the properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="faf47-111">Propriedade</span><span class="sxs-lookup"><span data-stu-id="faf47-111">Property</span></span> | <span data-ttu-id="faf47-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="faf47-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="faf47-113">Nome</span><span class="sxs-lookup"><span data-stu-id="faf47-113">Name</span></span> |<span data-ttu-id="faf47-114">Você pode fornecer qualquer nome que desejar para um webhook já que o mesmo não aparece para o cliente.</span><span class="sxs-lookup"><span data-stu-id="faf47-114">You can provide any name you want for a webhook since this is not exposed to the client.</span></span>  <span data-ttu-id="faf47-115">Ele é usado apenas por você para identificar o runbook na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="faf47-115">It is only used for you to identify the runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="faf47-116">Como prática recomendada, você deve atribuir ao webhook um nome relacionado ao cliente que irá usá-lo.</span><span class="sxs-lookup"><span data-stu-id="faf47-116">As a best practice, you should give the webhook a name related to the client that will use it.</span></span> |
| <span data-ttu-id="faf47-117">URL</span><span class="sxs-lookup"><span data-stu-id="faf47-117">URL</span></span> |<span data-ttu-id="faf47-118">A URL do webhook é o endereço exclusivo que um cliente chama um HTTP POST para iniciar o runbook vinculado ao webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-118">The URL of the webhook is the unique address that a client calls with an HTTP POST to start the runbook linked to the webhook.</span></span>  <span data-ttu-id="faf47-119">Ele é gerado automaticamente quando você cria o webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-119">It is automatically generated when you create the webhook.</span></span>  <span data-ttu-id="faf47-120">Você não pode especificar uma URL personalizada.</span><span class="sxs-lookup"><span data-stu-id="faf47-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="faf47-121">A URL contém um token de segurança que permite que o runbook seja invocado por um sistema de terceiros sem autenticação adicional.</span><span class="sxs-lookup"><span data-stu-id="faf47-121">The URL contains a security token that allows the runbook to be invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="faf47-122">Por esse motivo, ele deve ser tratado como uma senha.</span><span class="sxs-lookup"><span data-stu-id="faf47-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="faf47-123">Por motivos de segurança, você pode exibir apenas a URL no Portal do Azure no momento em que o webhook é criado.</span><span class="sxs-lookup"><span data-stu-id="faf47-123">For security reasons, you can only view the URL in the Azure portal at the time the webhook is created.</span></span> <span data-ttu-id="faf47-124">Você deve anotar a URL em um local seguro para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="faf47-124">You should note the URL in a secure location for future use.</span></span> |
| <span data-ttu-id="faf47-125">Data de validade</span><span class="sxs-lookup"><span data-stu-id="faf47-125">Expiration date</span></span> |<span data-ttu-id="faf47-126">Como um certificado, cada webhook tem uma data de validade após a qual ele não pode mais ser usado.</span><span class="sxs-lookup"><span data-stu-id="faf47-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="faf47-127">A data de validade pode ser modificada após a criação do webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-127">This expiration date can be modified after the webhook is created.</span></span> |
| <span data-ttu-id="faf47-128">Habilitado</span><span class="sxs-lookup"><span data-stu-id="faf47-128">Enabled</span></span> |<span data-ttu-id="faf47-129">Um webhook é habilitado por padrão quando ele é criado.</span><span class="sxs-lookup"><span data-stu-id="faf47-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="faf47-130">Se você defini-lo como Desabilitado, nenhum cliente poderá usá-lo.</span><span class="sxs-lookup"><span data-stu-id="faf47-130">If you set it to Disabled, then no client will be able to use it.</span></span>  <span data-ttu-id="faf47-131">Você pode definir a propriedade **Habilitado** quando você cria o webhook ou a qualquer momento quando ele é criado.</span><span class="sxs-lookup"><span data-stu-id="faf47-131">You can set the **Enabled** property when you create the webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="faf47-132">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="faf47-132">Parameters</span></span>
<span data-ttu-id="faf47-133">Um webhook pode definir valores para parâmetros de runbook que são usados quando o runbook é iniciado por esse webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-133">A webhook can define values for runbook parameters that are used when the runbook is started by that webhook.</span></span> <span data-ttu-id="faf47-134">O webhook deve incluir valores de quaisquer parâmetros obrigatórios do runbook e pode incluir valores de parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="faf47-134">The webhook must include values for any mandatory parameters of the runbook and may include values for optional parameters.</span></span> <span data-ttu-id="faf47-135">Um valor de parâmetro configurado para um Webhook pode ser modificado até mesmo depois da criação do Webhoook.</span><span class="sxs-lookup"><span data-stu-id="faf47-135">A parameter value configured to a webhook can be modified even after creating the webhoook.</span></span> <span data-ttu-id="faf47-136">Vários webhooks vinculados a um único runbook podem usar valores de parâmetros diferentes.</span><span class="sxs-lookup"><span data-stu-id="faf47-136">Multiple webhooks linked to a single runbook can each use different parameter values.</span></span>

<span data-ttu-id="faf47-137">Quando um cliente inicia um runbook usando um webhook, ele não pode substituir os valores de parâmetro definidos no webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-137">When a client starts a runbook using a webhook, it cannot override the parameter values defined in the webhook.</span></span>  <span data-ttu-id="faf47-138">Para receber dados do cliente, o runbook pode aceitar um parâmetro único chamado **$WebhookData** do tipo [objeto] que conterá os dados que o cliente inclui na solicitação POST.</span><span class="sxs-lookup"><span data-stu-id="faf47-138">To receive data from the client, the runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that the client includes in the POST request.</span></span>

![Propriedades de Webhookdata](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="faf47-140">O objeto **$WebhookData** terá as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="faf47-140">The **$WebhookData** object will have the following properties:</span></span>

| <span data-ttu-id="faf47-141">Propriedade</span><span class="sxs-lookup"><span data-stu-id="faf47-141">Property</span></span> | <span data-ttu-id="faf47-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="faf47-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="faf47-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="faf47-143">WebhookName</span></span> |<span data-ttu-id="faf47-144">O nome do webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-144">The name of the webhook.</span></span> |
| <span data-ttu-id="faf47-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="faf47-145">RequestHeader</span></span> |<span data-ttu-id="faf47-146">Tabela de hash contendo os cabeçalhos da solicitação de POST de entrada.</span><span class="sxs-lookup"><span data-stu-id="faf47-146">Hash table containing the headers of the incoming POST request.</span></span> |
| <span data-ttu-id="faf47-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="faf47-147">RequestBody</span></span> |<span data-ttu-id="faf47-148">O corpo da solicitação de POST de entrada.</span><span class="sxs-lookup"><span data-stu-id="faf47-148">The body of the incoming POST request.</span></span>  <span data-ttu-id="faf47-149">Isso manterá qualquer formatação, como a cadeia de caracteres, JSON, XML ou os dados codificados de formulário.</span><span class="sxs-lookup"><span data-stu-id="faf47-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="faf47-150">O runbook deve ser escrito para trabalhar com o formato de dados esperado. O runbook deve ser escrito para trabalhar com o formato de dados esperado.</span><span class="sxs-lookup"><span data-stu-id="faf47-150">The runbook must be written to work with the data format that is expected.</span></span> |

<span data-ttu-id="faf47-151">Nenhuma configuração do webhook é necessária para suporte ao parâmetro **$WebhookData** e o runbook não é necessário para aceitá-lo.</span><span class="sxs-lookup"><span data-stu-id="faf47-151">There is no configuration of the webhook required to support the **$WebhookData** parameter, and the runbook is not required to accept it.</span></span>  <span data-ttu-id="faf47-152">Se o runbook não definir o parâmetro, os detalhes da solicitação enviada pelo cliente são ignorados.</span><span class="sxs-lookup"><span data-stu-id="faf47-152">If the runbook does not define the parameter, then any details of the request sent from the client is ignored.</span></span>

<span data-ttu-id="faf47-153">Se você especificar um valor para $WebhookData quando você cria o webhook, esse valor será substituído quando o webhook inicia o runbook com os dados da solicitação POST do cliente, mesmo que o cliente não inclua todos os dados no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="faf47-153">If you specify a value for $WebhookData when you create the webhook, that value will be overriden when the webhook starts the runbook with the data from the client POST request, even if the client does not include any data in the request body.</span></span>  <span data-ttu-id="faf47-154">Se você iniciar um runbook que tenha $WebhookData usando um método que não seja um webhook, você pode fornecer um valor para $Webhookdata que será reconhecidos pelo runbook.</span><span class="sxs-lookup"><span data-stu-id="faf47-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by the runbook.</span></span>  <span data-ttu-id="faf47-155">Esse valor deve ser um objeto com as mesmas [propriedades](#details-of-a-webhook) que $Webhookdata, para que o runbook possa trabalhar corretamente com ele como se estivesse trabalhando com o WebhookData real transmitido por um webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-155">This value should be an object with the same [properties](#details-of-a-webhook) as $Webhookdata so that the runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="faf47-156">Por exemplo, se você estiver iniciando o runbook a seguir no Portal do Azure e desejar transmitir algum exemplo de WebhookData para teste, como WebhookData é um objeto, ele deve ser transmitido como JSON na interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="faf47-156">For example, if you are starting the following runbook from the Azure Portal and want to pass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in the UI.</span></span>

![Parâmetro WebhookData da interface do usuário](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="faf47-158">Para o runbook acima, se você tiver as seguintes propriedades para o parâmetro WebhookData:</span><span class="sxs-lookup"><span data-stu-id="faf47-158">For the above runbook, if you have the following properties for the WebhookData parameter:</span></span>

1. <span data-ttu-id="faf47-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="faf47-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="faf47-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="faf47-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="faf47-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="faf47-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="faf47-162">Em seguida, você transmitiria o seguinte valor JSON na interface do usuário para o parâmetro WebhookData:</span><span class="sxs-lookup"><span data-stu-id="faf47-162">Then you would pass the following JSON value in the UI for the WebhookData parameter:</span></span>  

* <span data-ttu-id="faf47-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="faf47-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Iniciar o parâmetro WebhookData na interface do usuário](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="faf47-165">Os valores de todos os parâmetros de entrada são registrados com o trabalho de runbook.</span><span class="sxs-lookup"><span data-stu-id="faf47-165">The values of all input parameters are logged with the runbook job.</span></span>  <span data-ttu-id="faf47-166">Isso significa que qualquer entrada fornecida pelo cliente na solicitação webhook será conectada e estará disponível para qualquer pessoa com acesso ao trabalho de automação.</span><span class="sxs-lookup"><span data-stu-id="faf47-166">This means that any input provided by the client in the webhook request will be logged and available to anyone with access to the automation job.</span></span>  <span data-ttu-id="faf47-167">Por esse motivo, você deve ter cuidado ao incluir informações confidenciais em chamadas webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="faf47-168">Segurança</span><span class="sxs-lookup"><span data-stu-id="faf47-168">Security</span></span>
<span data-ttu-id="faf47-169">A segurança de um webhook conta com a privacidade da sua URL que contém um token de segurança que permite que ele seja invocado.</span><span class="sxs-lookup"><span data-stu-id="faf47-169">The security of a webhook relies on the privacy of its URL which contains a security token that allows it to be invoked.</span></span> <span data-ttu-id="faf47-170">A Automação do Azure não executa nenhuma autenticação na solicitação desde que ela seja feita para a URL correta.</span><span class="sxs-lookup"><span data-stu-id="faf47-170">Azure Automation does not perform any authentication on the request as long as it is made to the correct URL.</span></span> <span data-ttu-id="faf47-171">Por esse motivo, os webhooks não devem ser usados para runbooks que executam funções altamente confidenciais sem usar um meio alternativo de validar a solicitação.</span><span class="sxs-lookup"><span data-stu-id="faf47-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating the request.</span></span>

<span data-ttu-id="faf47-172">Você pode incluir a lógica no runbook para determinar o que foi chamado por um webhook verificando a propriedade **WebhookName** do parâmetro $WebhookData.</span><span class="sxs-lookup"><span data-stu-id="faf47-172">You can include logic within the runbook to determine that it was called by a webhook by checking the **WebhookName** property of the $WebhookData parameter.</span></span> <span data-ttu-id="faf47-173">O runbook pode executar uma validação adicional procurando por informações específicas nas propriedades **RequestHeader** ou **RequestBody**.</span><span class="sxs-lookup"><span data-stu-id="faf47-173">The runbook could perform further validation by looking for particular information in the **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="faf47-174">Outra estratégia é o runbook realizar alguma validação de uma condição externa quando ele receber uma solicitação webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-174">Another strategy is to have the runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="faf47-175">Por exemplo, considere um runbook que é chamado pelo GitHub sempre que houver uma nova confirmação para um repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="faf47-175">For example, consider a runbook that is called by GitHub whenever there is a new commit to a GitHub repository.</span></span>  <span data-ttu-id="faf47-176">O runbook pode se conectar ao GitHub para validar que uma nova confirmação realmente ocorreu antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="faf47-176">The runbook might connect to GitHub to validate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="faf47-177">Criando um webhook</span><span class="sxs-lookup"><span data-stu-id="faf47-177">Creating a webhook</span></span>
<span data-ttu-id="faf47-178">Use o procedimento a seguir para criar um novo webhook vinculado a um runbook no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="faf47-178">Use the following procedure to create a new webhook linked to a runbook in the Azure portal.</span></span>

1. <span data-ttu-id="faf47-179">Na **folha de Runbooks** no Portal do Azure, clique no runbook que o webhook começará a exibir a sua folha de detalhes.</span><span class="sxs-lookup"><span data-stu-id="faf47-179">From the **Runbooks blade** in the Azure portal, click the runbook that the webhook will start to view its detail blade.</span></span>
2. <span data-ttu-id="faf47-180">Clique em **Webhook** na parte superior da folha para abrir a folha **Adicionar webhook**.</span><span class="sxs-lookup"><span data-stu-id="faf47-180">Click **Webhook** at the top of the blade to open the **Add Webhook** blade.</span></span> <br><span data-ttu-id="faf47-181">
   ![Botão Webhooks](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="faf47-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="faf47-182">Clique em **Criar novo webhook** para abrir a **folha Criar webhook**.</span><span class="sxs-lookup"><span data-stu-id="faf47-182">Click **Create new webhook** to open the **Create webhook blade**.</span></span>
4. <span data-ttu-id="faf47-183">Especifique um **Nome** e uma **Data de validade** para o webhook e se ele deve ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="faf47-183">Specify a **Name**, **Expiration Date** for the webhook and whether it should be enabled.</span></span> <span data-ttu-id="faf47-184">Consulte [Detalhes de um webhook](#details-of-a-webhook) para obter mais informações sobre essas propriedades.</span><span class="sxs-lookup"><span data-stu-id="faf47-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="faf47-185">Clique no ícone copiar e pressione Ctrl + C para copiar a URL do webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-185">Click the copy icon and press Ctrl+C to copy the URL of the webhook.</span></span>  <span data-ttu-id="faf47-186">Em seguida, anote-o em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="faf47-186">Then record it in a safe place.</span></span>  <span data-ttu-id="faf47-187">**Quando você cria o webhook, não é possível recuperar a URL novamente.**</span><span class="sxs-lookup"><span data-stu-id="faf47-187">**Once you create the webhook, you cannot retrieve the URL again.**</span></span> <br><span data-ttu-id="faf47-188">
   ![URL de Webhook](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="faf47-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="faf47-189">Clique em **Parâmetros** para fornecer valores para os parâmetros do runbook.</span><span class="sxs-lookup"><span data-stu-id="faf47-189">Click **Parameters** to provide values for the runbook parameters.</span></span>  <span data-ttu-id="faf47-190">Se o runbook tiver parâmetros obrigatórios, não será possível criar o webhook, a menos que os valores sejam fornecidos.</span><span class="sxs-lookup"><span data-stu-id="faf47-190">If the runbook has mandatory parameters, then you will not be able to create the webhook unless values are provided.</span></span>
7. <span data-ttu-id="faf47-191">Clique em **Criar** para criar o webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-191">Click **Create** to create the webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="faf47-192">Usando um webhook</span><span class="sxs-lookup"><span data-stu-id="faf47-192">Using a webhook</span></span>
<span data-ttu-id="faf47-193">Para usar um webhook após ele ter sido criado, o aplicativo cliente deve emitir um POST HTTP com a URL para o webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-193">To use a webhook after it has been created, your client application must issue an HTTP POST with the URL for the webhook.</span></span>  <span data-ttu-id="faf47-194">A sintaxe do webhook será no formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="faf47-194">The syntax of the webhook will be in the following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="faf47-195">O cliente receberá um dos seguintes códigos de retorno da solicitação POST.</span><span class="sxs-lookup"><span data-stu-id="faf47-195">The client will receive one of the following return codes from the POST request.</span></span>  

| <span data-ttu-id="faf47-196">Código</span><span class="sxs-lookup"><span data-stu-id="faf47-196">Code</span></span> | <span data-ttu-id="faf47-197">Texto</span><span class="sxs-lookup"><span data-stu-id="faf47-197">Text</span></span> | <span data-ttu-id="faf47-198">Descrição</span><span class="sxs-lookup"><span data-stu-id="faf47-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="faf47-199">202</span><span class="sxs-lookup"><span data-stu-id="faf47-199">202</span></span> |<span data-ttu-id="faf47-200">Aceita</span><span class="sxs-lookup"><span data-stu-id="faf47-200">Accepted</span></span> |<span data-ttu-id="faf47-201">A solicitação foi aceita e o runbook foi enfileirado com êxito.</span><span class="sxs-lookup"><span data-stu-id="faf47-201">The request was accepted, and the runbook was successfully queued.</span></span> |
| <span data-ttu-id="faf47-202">400</span><span class="sxs-lookup"><span data-stu-id="faf47-202">400</span></span> |<span data-ttu-id="faf47-203">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="faf47-203">Bad Request</span></span> |<span data-ttu-id="faf47-204">A solicitação não foi aceita por um dos motivos a seguir.</span><span class="sxs-lookup"><span data-stu-id="faf47-204">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="faf47-205">O webhook expirou.</span><span class="sxs-lookup"><span data-stu-id="faf47-205">The webhook has expired.</span></span></li> <li><span data-ttu-id="faf47-206">O webhook está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="faf47-206">The webhook is disabled.</span></span></li> <li><span data-ttu-id="faf47-207">O token na URL é inválido.</span><span class="sxs-lookup"><span data-stu-id="faf47-207">The token in the URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="faf47-208">404</span><span class="sxs-lookup"><span data-stu-id="faf47-208">404</span></span> |<span data-ttu-id="faf47-209">Não encontrado</span><span class="sxs-lookup"><span data-stu-id="faf47-209">Not Found</span></span> |<span data-ttu-id="faf47-210">A solicitação não foi aceita por um dos motivos a seguir.</span><span class="sxs-lookup"><span data-stu-id="faf47-210">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="faf47-211">O webhook não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="faf47-211">The webhook was not found.</span></span></li> <li><span data-ttu-id="faf47-212">O runbook não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="faf47-212">The runbook was not found.</span></span></li> <li><span data-ttu-id="faf47-213">A conta não foi encontrada.</span><span class="sxs-lookup"><span data-stu-id="faf47-213">The account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="faf47-214">500</span><span class="sxs-lookup"><span data-stu-id="faf47-214">500</span></span> |<span data-ttu-id="faf47-215">Erro interno do servidor</span><span class="sxs-lookup"><span data-stu-id="faf47-215">Internal Server Error</span></span> |<span data-ttu-id="faf47-216">A URL era válida, mas ocorreu um erro.</span><span class="sxs-lookup"><span data-stu-id="faf47-216">The URL was valid, but an error occurred.</span></span>  <span data-ttu-id="faf47-217">Envie a solicitação novamente.</span><span class="sxs-lookup"><span data-stu-id="faf47-217">Please resubmit the request.</span></span> |

<span data-ttu-id="faf47-218">Supondo que a solicitação seja bem-sucedida, a resposta webhook contém a ID de trabalho no formato JSON da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="faf47-218">Assuming the request is successful, the webhook response contains the job id in JSON format as follows.</span></span> <span data-ttu-id="faf47-219">Ela conterá uma ID de trabalho única, mas o formato JSON permite possíveis aprimoramentos futuros.</span><span class="sxs-lookup"><span data-stu-id="faf47-219">It will contain a single job id, but the JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="faf47-220">O cliente não pode determinar o status da conclusão do webhook ou quando o trabalho de runbook é concluído.</span><span class="sxs-lookup"><span data-stu-id="faf47-220">The client cannot determine when the runbook job completes or its completion status from the webhook.</span></span>  <span data-ttu-id="faf47-221">Ele pode determinar essas informações usando a ID de trabalho com outro método como [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) ou[ API de Automação do Azure](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="faf47-221">It can determine this information using the job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or the [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="faf47-222">Exemplo</span><span class="sxs-lookup"><span data-stu-id="faf47-222">Example</span></span>
<span data-ttu-id="faf47-223">O exemplo a seguir usa o Windows PowerShell para iniciar um runbook com um webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-223">The following example uses Windows PowerShell to start a runbook with a webhook.</span></span>  <span data-ttu-id="faf47-224">Observe que qualquer linguagem que possa fazer uma solicitação HTTP pode usar um webhook; o Windows PowerShell é usado aqui apenas como um exemplo.</span><span class="sxs-lookup"><span data-stu-id="faf47-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="faf47-225">O runbook está esperando uma lista de máquinas virtuais formatadas em JSON no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="faf47-225">The runbook is expecting a list of virtual machines formatted in JSON in the body of the request.</span></span> <span data-ttu-id="faf47-226">Também incluímos informações sobre quem está iniciando o runbook e a data e a hora que ele está sendo iniciado no cabeçalho da solicitação.</span><span class="sxs-lookup"><span data-stu-id="faf47-226">We also are including information about who is starting the runbook and the date and time it is being started in the header of the request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="faf47-227">A imagem a seguir mostra as informações de cabeçalho (usando um rastreamento [Fiddler](http://www.telerik.com/fiddler) ) desta solicitação.</span><span class="sxs-lookup"><span data-stu-id="faf47-227">The following image shows the header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="faf47-228">Isso inclui os cabeçalhos padrão de uma solicitação HTTP, além dos cabeçalhos personalizados de Data e Origem que adicionamos.</span><span class="sxs-lookup"><span data-stu-id="faf47-228">This includes standard headers of an HTTP request in addition to the custom Date and From headers that we added.</span></span>  <span data-ttu-id="faf47-229">Cada um desses valores está disponível para o runbook na propriedade **RequestHeaders** de **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="faf47-229">Each of these values is available to the runbook in the **RequestHeaders** property of **WebhookData**.</span></span>

![Botão Webhooks](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="faf47-231">A imagem a seguir mostra o corpo da solicitação (usando um rastreamento [Fiddler](http://www.telerik.com/fiddler)) que está disponível para o runbook na propriedade **RequestBody** do **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="faf47-231">The following image shows the body of the request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available to the runbook in the **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="faf47-232">Ela é formatada como JSON, pois esse era o formato que foi incluído no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="faf47-232">This is formatted as JSON because that was the format that was included in the body of the request.</span></span>     

![Botão Webhooks](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="faf47-234">A imagem a seguir mostra a solicitação sendo enviada do Windows PowerShell e a resposta resultante.</span><span class="sxs-lookup"><span data-stu-id="faf47-234">The following image shows the request being sent from Windows PowerShell and the resulting response.</span></span>  <span data-ttu-id="faf47-235">A ID do trabalho é extraída da resposta e convertida em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="faf47-235">The job id is extracted from the response and converted to a string.</span></span>

![Botão Webhooks](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="faf47-237">O seguinte exemplo de runbook aceita a solicitação do exemplo anterior e inicia as máquinas virtuais especificadas no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="faf47-237">The following sample runbook accepts the previous example request and starts the virtual machines specified in the request body.</span></span>

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

            # Authenticate to Azure resources
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
            Write-Error "Runbook mean to be started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-to-azure-alerts"></a><span data-ttu-id="faf47-238">Iniciar runbooks em resposta a um alerta do Azure</span><span class="sxs-lookup"><span data-stu-id="faf47-238">Starting runbooks in response to Azure alerts</span></span>
<span data-ttu-id="faf47-239">Runbooks habilitados para Webhook podem ser usados para reagir a [alertas do Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="faf47-239">Webhook-enabled runbooks can be used to react to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="faf47-240">Recursos no Azure podem ser monitorados por meio da coleta de estatísticas, como desempenho, disponibilidade e uso, com a ajuda dos alertas do Azure.</span><span class="sxs-lookup"><span data-stu-id="faf47-240">Resources in Azure can be monitored by collecting the statistics like performance, availability and usage with the help of Azure alerts.</span></span> <span data-ttu-id="faf47-241">Você pode receber um alerta com base em métricas de monitoramento ou em eventos para seus recursos do Azure. No momento, as Contas de Automação oferecem suporte apenas para métricas.</span><span class="sxs-lookup"><span data-stu-id="faf47-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="faf47-242">Quando o valor de uma métrica especificada ultrapassar o limite atribuído ou se o evento configurado for disparado e uma notificação for enviada ao administrador ou coadministradores do serviço para resolver o alerta, consulte [alertas do Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) para obter mais informações sobre eventos e métricas.</span><span class="sxs-lookup"><span data-stu-id="faf47-242">When the value of a specified metric exceeds the threshold assigned or if the configured event is triggered then a notification is sent to the service admin or co-admins to resolve the alert, for more information on metrics and events please refer to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="faf47-243">Além de usar alertas do Azure como um sistema de notificação, você também pode disparar runbooks em resposta a alertas.</span><span class="sxs-lookup"><span data-stu-id="faf47-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response to alerts.</span></span> <span data-ttu-id="faf47-244">A Automação do Azure fornece a capacidade de executar runbooks habilitados para webhook com alertas do Azure.</span><span class="sxs-lookup"><span data-stu-id="faf47-244">Azure Automation provides the capability to run webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="faf47-245">Quando uma métrica excede o valor do limite configurado, a regra do alerta fica ativa e dispara o webhook de automação, que por sua vez executa o runbook.</span><span class="sxs-lookup"><span data-stu-id="faf47-245">When a metric exceeds the configured threshold value then the alert rule becomes active and triggers the automation webhook which in turn executes the runbook.</span></span>

![Webhooks](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="faf47-247">Contexto do alerta</span><span class="sxs-lookup"><span data-stu-id="faf47-247">Alert context</span></span>
<span data-ttu-id="faf47-248">Considere um recurso do Azure como uma máquina virtual, a utilização da CPU dessa máquina é uma das principais métricas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="faf47-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of the key performance metric.</span></span> <span data-ttu-id="faf47-249">Se a utilização da CPU for 100% ou mais do que uma determinada quantidade por longo período de tempo, talvez você queira reiniciar a máquina virtual para corrigir o problema.</span><span class="sxs-lookup"><span data-stu-id="faf47-249">If the CPU utilization is 100% or more than a certain amount for long period of time, you might want to restart the virtual machine to fix the problem.</span></span> <span data-ttu-id="faf47-250">Isso pode ser resolvido por meio da configuração de uma regra de alerta para a máquina virtual e essa regra usa o percentual de CPU como sua métrica.</span><span class="sxs-lookup"><span data-stu-id="faf47-250">This can be solved by configuring an alert rule to the virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="faf47-251">O percentual de CPU aqui é usado apenas como um exemplo, mas existem muitas outras métricas que podem ser configuradas para os recursos do Azure, e reiniciar a máquina virtual é uma ação executada para corrigir esse problema. Você pode configurar o runbook para executar outras ações.</span><span class="sxs-lookup"><span data-stu-id="faf47-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure to your Azure resources and restarting the virtual machine is an action that is taken to fix this issue, you can configure the runbook to take other actions.</span></span>

<span data-ttu-id="faf47-252">Quando esta regra de alerta é ativada e dispara o runbook habilitado para webhook, ela envia o contexto do alerta para o runbook.</span><span class="sxs-lookup"><span data-stu-id="faf47-252">When this the alert rule becomes active and triggers the webhook-enabled runbook, it sends the alert context to the runbook.</span></span> <span data-ttu-id="faf47-253">O [contexto de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contém detalhes que incluem **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** e **Timestamp**, que são necessários para o runbook identificar o recurso em que ele realizará a ação.</span><span class="sxs-lookup"><span data-stu-id="faf47-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for the runbook to identify the resource on which it will be taking action.</span></span> <span data-ttu-id="faf47-254">O contexto do alerta é inserido na parte de corpo do objeto **WebhookData** enviado para o runbook e pode ser acessado com a propriedade **Webhook.RequestBody**</span><span class="sxs-lookup"><span data-stu-id="faf47-254">Alert context is embedded in the body part of the **WebhookData** object sent to the runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="faf47-255">Exemplo</span><span class="sxs-lookup"><span data-stu-id="faf47-255">Example</span></span>
<span data-ttu-id="faf47-256">Crie uma máquina virtual do Azure em sua assinatura e associe um [alerta para monitorar a métrica de percentual de CPU](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="faf47-256">Create an Azure virtual machine in your subscription and associate an [alert to monitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="faf47-257">Ao criar o alerta, certifique-se de preencher o campo webhook com a URL do webhook que foi gerada durante a criação do webhook.</span><span class="sxs-lookup"><span data-stu-id="faf47-257">While creating the alert make sure you populate the webhook field with the URL of the webhook which was generated while creating the webhook.</span></span>

<span data-ttu-id="faf47-258">O seguinte exemplo de runbook é acionado quando a regra de alerta é ativada e coleta os parâmetros de contexto do Alerta que são necessários para o runbook identificar o recurso em que ele vai realizar ação.</span><span class="sxs-lookup"><span data-stu-id="faf47-258">The following sample runbook is triggered when the alert rule becomes active and it collects the Alert context parameters which are required for the runbook to identify the resource on which it will be taking action.</span></span>

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

            # Outputs information on the webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain the WebhookBody containing the AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain the AlertContext     
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

            # Act on the AlertContext data, in our case restarting the VM.
            # Authenticate to your Azure subscription using Organization ID to be able to restart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check the status property of the VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart the VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant to only be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="faf47-259">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="faf47-259">Next steps</span></span>
* <span data-ttu-id="faf47-260">Para obter detalhes sobre diferentes maneiras de iniciar um runbook, confira [Iniciar um runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="faf47-260">For details on different ways to start a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="faf47-261">Para saber mais sobre como exibir o Status de um Trabalho de Runbook, consulte [Execução de runbook na Automação do Azure](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="faf47-261">For information on viewing the Status of a Runbook Job, refer to [Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="faf47-262">Para saber como usar a Automação do Azure para agir em Alertas do Azure, veja [Corrigir alertas de VM do Azure com runbooks da Automação](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="faf47-262">To learn how to use Azure Automation to take action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
