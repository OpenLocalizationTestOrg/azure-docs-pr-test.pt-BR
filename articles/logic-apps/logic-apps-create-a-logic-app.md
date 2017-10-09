---
title: "aaaCreate seu primeiro fluxo de trabalho entre os serviços de nuvem - Azure lógica de aplicativos e aplicativos de nuvem | Microsoft Docs"
description: "Automatizar os processos de negócios para os cenários de integração de sistemas e integração de aplicativos empresariais (EAI) criando e executando fluxos de trabalho no Aplicativo Lógico do Azure"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "fluxo de trabalho, aplicativos de nuvem, serviços de nuvem, processos de negócios, integração de sistemas, integração de aplicativos empresariais, EAI"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="1a138-104">Criar seu primeiro aplicativo de lógica de processos do fluxo de trabalho tooautomate entre aplicativos de nuvem e os serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="1a138-104">Create your first logic app workflow tooautomate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="1a138-105">Sem escrever nenhum código, você pode automatizar os processos de negócios mais fácil e rapidamente quando cria e executa os fluxos de trabalho com o [Aplicativo Lógico do Azure](logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1a138-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="1a138-106">Este primeiro exemplo mostra como toocreate um fluxo de trabalho de aplicativo lógica básica que verifica um RSS feed para o novo conteúdo em um site.</span><span class="sxs-lookup"><span data-stu-id="1a138-106">This first example shows how toocreate a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="1a138-107">Quando novos itens são exibidos no feed do site hello, Olá lógica aplicativo envia email de uma conta do Outlook ou Gmail.</span><span class="sxs-lookup"><span data-stu-id="1a138-107">When new items appear in hello website's feed, hello logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="1a138-108">toocreate e executar um aplicativo lógico, é necessário estes itens:</span><span class="sxs-lookup"><span data-stu-id="1a138-108">toocreate and run a logic app, you need these items:</span></span>

* <span data-ttu-id="1a138-109">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a138-109">An Azure subscription.</span></span> <span data-ttu-id="1a138-110">Se você não tiver uma assinatura, poderá [iniciar com uma conta gratuita do Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="1a138-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="1a138-111">Caso contrário, você pode [inscrever-se para uma assinatura Pré-paga](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="1a138-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="1a138-112">Sua assinatura do Azure é usada para a cobrança de uso do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1a138-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="1a138-113">Saiba como a [medição de uso](../logic-apps/logic-apps-pricing.md) e os [preços](https://azure.microsoft.com/pricing/details/logic-apps) funcionam para os Aplicativos Lógicos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a138-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="1a138-114">Além disso, este exemplo requer estes itens:</span><span class="sxs-lookup"><span data-stu-id="1a138-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="1a138-115">Uma conta do Gmail, Office 365 Outlook ou Outlook.com</span><span class="sxs-lookup"><span data-stu-id="1a138-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="1a138-116">Se você tiver uma [conta da Microsoft](https://account.microsoft.com/account) pessoal, terá uma conta do Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="1a138-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="1a138-117">Caso contrário, se tiver uma conta corporativa ou de estudante do Azure, terá uma conta do **Outlook do Office 365**.</span><span class="sxs-lookup"><span data-stu-id="1a138-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="1a138-118">Tooa um link RSS do site feed.</span><span class="sxs-lookup"><span data-stu-id="1a138-118">A link tooa website's RSS feed.</span></span> <span data-ttu-id="1a138-119">Este exemplo usa Olá [RSS feed histórias superiores do site do CNN.com Olá](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="1a138-119">This example uses hello [RSS feed for top stories from hello CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="1a138-120">Adicionar um gatilho que inicia o fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="1a138-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="1a138-121">Um [ *gatilho* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) é um evento que inicia o fluxo de trabalho do aplicativo de lógica e é Olá primeiro item que precisa de seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1a138-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is hello first item that your logic app needs.</span></span>

1. <span data-ttu-id="1a138-122">Entrar toohello [portal do Azure](https://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="1a138-122">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="1a138-123">No menu à esquerda do hello, escolha **novo** > **integração corporativa** > **aplicativo lógico** conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="1a138-123">From hello left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Portal do Azure, Novo, Enterprise Integration, Aplicativo Lógico](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="1a138-125">Você também pode escolher **novo**, em seguida, na caixa de pesquisa hello, digite `logic app`, e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="1a138-125">You can also choose **New**, then in hello search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="1a138-126">Então, escolha **Aplicativo Lógico** > **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1a138-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="1a138-127">Nomeie seu aplicativo lógico e selecione sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a138-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="1a138-128">Agora, crie ou selecione um grupo de recursos do Azure, o que ajuda a organizar e gerenciar os recursos do Azure afins.</span><span class="sxs-lookup"><span data-stu-id="1a138-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="1a138-129">Por fim, selecione a localização do datacenter Olá para hospedar seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1a138-129">Finally, select hello datacenter location for hosting your logic app.</span></span> <span data-ttu-id="1a138-130">Quando você estiver pronto, escolha **Pin toodashboard** e **criar**.</span><span class="sxs-lookup"><span data-stu-id="1a138-130">When you're ready, choose **Pin toodashboard** and then **Create**.</span></span>

     ![Detalhes do aplicativo lógico](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="1a138-132">Quando você seleciona **toodashboard Pin**, seu aplicativo lógico será exibido no saudação do painel do Azure após a implantação e é aberto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1a138-132">When you select **Pin toodashboard**, your logic app appears on hello Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="1a138-133">Se seu aplicativo lógico não aparecerá no painel do hello, Olá **todos os recursos** lado a lado, escolha **consulte mais**e selecione o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1a138-133">If your logic app doesn't appear on hello dashboard, on hello **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="1a138-134">Ou, no menu à esquerda do hello, escolha **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="1a138-134">Or on hello left menu, choose **More services**.</span></span> <span data-ttu-id="1a138-135">Em **Enterprise Integration**, escolha **Aplicativos Lógicos** e selecione seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1a138-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="1a138-136">Quando você abre o aplicativo lógico para Olá primeira vez, Olá lógica de aplicativo Designer mostra modelos que você pode usar tooget iniciado.</span><span class="sxs-lookup"><span data-stu-id="1a138-136">When you open your logic app for hello first time, hello Logic App Designer shows templates that you can use tooget started.</span></span> <span data-ttu-id="1a138-137">Por ora, escolha **Aplicativo Lógico em Branco** para poder compilar seu aplicativo lógico do zero.</span><span class="sxs-lookup"><span data-stu-id="1a138-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="1a138-138">Olá lógica de aplicativo Designer é aberto e mostra os serviços disponíveis e *gatilhos* que você pode usar em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1a138-138">hello Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="1a138-139">Na caixa de pesquisa hello, digite `RSS`e selecione esse gatilho: **RSS - quando um item do feed é publicado**</span><span class="sxs-lookup"><span data-stu-id="1a138-139">In hello search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![Gatilho do RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="1a138-141">Insira o link de saudação para RSS feed do site de saudação do que você deseja tootrack.</span><span class="sxs-lookup"><span data-stu-id="1a138-141">Enter hello link for hello website's RSS feed that you want tootrack.</span></span> 

     <span data-ttu-id="1a138-142">Você também pode alterar a **Frequência** e o **Intervalo**.</span><span class="sxs-lookup"><span data-stu-id="1a138-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="1a138-143">Essas configurações determinam a frequência com que o aplicativo lógico verifica se há novos itens e retorna todos os itens encontrados durante esse período de tempo.</span><span class="sxs-lookup"><span data-stu-id="1a138-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="1a138-144">Neste exemplo, vamos verificar todos os dias para principais histórias postadas site CNN toohello.</span><span class="sxs-lookup"><span data-stu-id="1a138-144">For this example, let's check every day for   top stories posted toohello CNN website.</span></span>

     ![Configurar um gatilho com o RSS feed, frequência e intervalo](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="1a138-146">Salve seu trabalho agora.</span><span class="sxs-lookup"><span data-stu-id="1a138-146">Save your work for now.</span></span> <span data-ttu-id="1a138-147">(Na barra de comando designer hello, escolha **salvar**.)</span><span class="sxs-lookup"><span data-stu-id="1a138-147">(On hello designer command bar, choose **Save**.)</span></span>

   ![Salve seu aplicativo lógico](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="1a138-149">Quando você salvar, seu aplicativo lógico fica ativo, mas no momento, seu aplicativo lógico só verificará se há novos itens no hello especificado RSS feed.</span><span class="sxs-lookup"><span data-stu-id="1a138-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in hello specified RSS feed.</span></span> 
   <span data-ttu-id="1a138-150">toomake Este exemplo mais útil, que adicionamos uma ação que executa o aplicativo lógico após o disparador é acionado.</span><span class="sxs-lookup"><span data-stu-id="1a138-150">toomake this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-tooyour-trigger"></a><span data-ttu-id="1a138-151">Adicione uma ação que responde tooyour gatilho</span><span class="sxs-lookup"><span data-stu-id="1a138-151">Add an action that responds tooyour trigger</span></span>

<span data-ttu-id="1a138-152">Uma [*ação*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) é uma tarefa executada pelo fluxo de trabalho do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1a138-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="1a138-153">Depois de adicionar um aplicativo de lógica do gatilho tooyour, você pode adicionar operações de tooperform uma ação com dados gerados por que o disparador.</span><span class="sxs-lookup"><span data-stu-id="1a138-153">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="1a138-154">Para nosso exemplo, agora é adicionar uma ação que envia email quando novos itens são exibidos no feed de RSS do site hello.</span><span class="sxs-lookup"><span data-stu-id="1a138-154">For our example, we now add an action that sends email when new items appear in hello website's RSS feed.</span></span>

1. <span data-ttu-id="1a138-155">No designer de hello, sob o disparador, escolha **nova etapa** > **adicionar uma ação** conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="1a138-155">In hello designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Adicionar uma ação](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="1a138-157">Olá designer mostra [conectores disponíveis](../connectors/apis-list.md) para que você possa selecionar tooperform uma ação quando o disparador é acionado.</span><span class="sxs-lookup"><span data-stu-id="1a138-157">hello designer shows [available connectors](../connectors/apis-list.md) so that you can select an action tooperform when your trigger fires.</span></span>

2. <span data-ttu-id="1a138-158">Com base na sua conta de email, siga as etapas de saudação para Outlook ou Gmail.</span><span class="sxs-lookup"><span data-stu-id="1a138-158">Based on your email account, follow hello steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="1a138-159">email toosend na conta do Outlook, na caixa de pesquisa hello, digite `outlook`.</span><span class="sxs-lookup"><span data-stu-id="1a138-159">toosend email from your Outlook account, in hello search box, enter `outlook`.</span></span> <span data-ttu-id="1a138-160">Em **Serviços**, escolha **Outlook.com** para as contas pessoais da Microsoft ou escolha **Outlook do Office 365** para as contas corporativas ou de estudante do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a138-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="1a138-161">Em **Ações**, selecione **Enviar um email**.</span><span class="sxs-lookup"><span data-stu-id="1a138-161">Under **Actions**, select **Send an email**.</span></span>

       ![Selecionar a ação "Enviar um email" do Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="1a138-163">toosend email da sua conta do Gmail, na caixa de pesquisa hello, digite `gmail`.</span><span class="sxs-lookup"><span data-stu-id="1a138-163">toosend email from your Gmail account, in hello search box, enter `gmail`.</span></span> 
   <span data-ttu-id="1a138-164">Em **Ações**, selecione **Enviar email**.</span><span class="sxs-lookup"><span data-stu-id="1a138-164">Under **Actions**, select **Send email**.</span></span>

       ![Escolher "Gmail - enviar email"](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="1a138-166">Quando você for solicitado a fornecer credenciais, entre Olá username e password para sua conta de email.</span><span class="sxs-lookup"><span data-stu-id="1a138-166">When you're prompted for credentials, sign in with hello username and password for your email account.</span></span> 

4. <span data-ttu-id="1a138-167">Forneça detalhes de saudação para esta ação, como endereço de email de destino Olá e escolher parâmetros Olá Olá dados tooinclude no email Olá, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1a138-167">Provide hello details for this action, like hello destination email address, and choose hello parameters for hello data tooinclude in hello email, for example:</span></span>

   ![Selecione os dados tooinclude no email](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="1a138-169">Portanto, se você escolheu o Outlook, seu aplicativo lógico poderá parecer com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="1a138-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![Aplicativo lógico concluído](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="1a138-171">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="1a138-171">Save your changes.</span></span> <span data-ttu-id="1a138-172">(Na barra de comando designer hello, escolha **salvar**.)</span><span class="sxs-lookup"><span data-stu-id="1a138-172">(On hello designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="1a138-173">Agora, você pode executar manualmente seu aplicativo lógico para testar.</span><span class="sxs-lookup"><span data-stu-id="1a138-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="1a138-174">Na barra de comando designer hello, escolha **executar**.</span><span class="sxs-lookup"><span data-stu-id="1a138-174">On hello designer command bar, choose **Run**.</span></span> <span data-ttu-id="1a138-175">Caso contrário, você pode deixar seu aplicativo lógico verificar Olá especificado feed RSS com base em agendamento Olá que você configurou.</span><span class="sxs-lookup"><span data-stu-id="1a138-175">Otherwise, you can let your logic app check hello specified RSS feed based on hello schedule that you set up.</span></span>

   <span data-ttu-id="1a138-176">Se seu aplicativo lógico localiza novos itens, Olá lógica aplicativo envia email que inclui os dados selecionados.</span><span class="sxs-lookup"><span data-stu-id="1a138-176">If your logic app finds new items, hello logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="1a138-177">Se novos itens não forem encontrado, o aplicativo lógico ignora ação Olá que envia email.</span><span class="sxs-lookup"><span data-stu-id="1a138-177">If no new items are found, your logic app skips hello action that sends email.</span></span>

7. <span data-ttu-id="1a138-178">toomonitor e verifique se seu aplicativo de lógica de execução e disparar histórico, no menu aplicativo lógica, escolha **visão geral**.</span><span class="sxs-lookup"><span data-stu-id="1a138-178">toomonitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Monitorar e verificar a execução de seu aplicativo lógico e o histórico de gatilhos](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="1a138-180">Se você não encontrar dados Olá que você espera que, na barra de comandos hello, tente escolher **atualizar**.</span><span class="sxs-lookup"><span data-stu-id="1a138-180">If you don't find hello data that you expect, on hello command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="1a138-181">toolearn mais sobre o status do seu aplicativo lógica ou execute e disparar histórico ou toodiagnose sua lógica de aplicativo, consulte [solucionar seu aplicativo lógico](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="1a138-181">toolearn more about your logic app's status or run and trigger history, or toodiagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="1a138-182">Seu aplicativo lógico continuará sendo executado até que você desative o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1a138-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="1a138-183">tooturn desativar seu aplicativo agora, no menu aplicativo lógica, escolha **visão geral**.</span><span class="sxs-lookup"><span data-stu-id="1a138-183">tooturn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="1a138-184">Na barra de comandos hello, escolha **desabilitar**.</span><span class="sxs-lookup"><span data-stu-id="1a138-184">On hello command bar, choose **Disable**.</span></span>

<span data-ttu-id="1a138-185">Parabéns, você acabou de configurar e executar seu primeiro aplicativo lógico básico.</span><span class="sxs-lookup"><span data-stu-id="1a138-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="1a138-186">Você também aprendeu como é fácil criar fluxos de trabalho que automatizam os processos e integram os aplicativos e serviços de nuvem - tudo sem código.</span><span class="sxs-lookup"><span data-stu-id="1a138-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="1a138-187">Gerenciar seu aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="1a138-187">Manage your logic app</span></span>

<span data-ttu-id="1a138-188">toomanage seu aplicativo, você pode executar tarefas como verificar o status de saudação, editar, exibir o histórico, desativar ou excluir o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1a138-188">toomanage your app, you can perform tasks like check hello status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="1a138-189">Entrar toohello [portal do Azure](https://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="1a138-189">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="1a138-190">No menu à esquerda do hello, escolha **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="1a138-190">On hello left menu, choose **More services**.</span></span> <span data-ttu-id="1a138-191">Em **Enterprise Integration**, escolha **Aplicativos Lógicos**.</span><span class="sxs-lookup"><span data-stu-id="1a138-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="1a138-192">Selecione seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1a138-192">Select your logic app.</span></span> 

   <span data-ttu-id="1a138-193">No menu de aplicativo do hello lógica, você pode encontrar essas tarefas de gerenciamento de aplicativo lógica:</span><span class="sxs-lookup"><span data-stu-id="1a138-193">In hello logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="1a138-194">Tarefa</span><span class="sxs-lookup"><span data-stu-id="1a138-194">Task</span></span>|<span data-ttu-id="1a138-195">Etapas</span><span class="sxs-lookup"><span data-stu-id="1a138-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="1a138-196">Exibir o status, histórico de execução e informações gerais de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1a138-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="1a138-197">Escolha **Visão Geral**.</span><span class="sxs-lookup"><span data-stu-id="1a138-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="1a138-198">Editar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1a138-198">Edit your app</span></span> | <span data-ttu-id="1a138-199">Escolha **Designer de Aplicativos Lógicos**.</span><span class="sxs-lookup"><span data-stu-id="1a138-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="1a138-200">Exibir a definição JSON do fluxo de trabalho de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1a138-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="1a138-201">Escolha **Exibir Código do Aplicativo Lógico**.</span><span class="sxs-lookup"><span data-stu-id="1a138-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="1a138-202">Exibir as operações executadas em seu aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="1a138-202">View operations performed on your logic app</span></span> | <span data-ttu-id="1a138-203">Escolha **Log de atividades**.</span><span class="sxs-lookup"><span data-stu-id="1a138-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="1a138-204">Exibir as antigas versões de seu aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="1a138-204">View past versions for your logic app</span></span> | <span data-ttu-id="1a138-205">Escolha **Versões**.</span><span class="sxs-lookup"><span data-stu-id="1a138-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="1a138-206">Desativar temporariamente seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1a138-206">Turn off your app temporarily</span></span> | <span data-ttu-id="1a138-207">Escolha **visão geral**, em seguida, na barra de comandos hello, escolha **desabilitar**.</span><span class="sxs-lookup"><span data-stu-id="1a138-207">Choose **Overview**, then on hello command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="1a138-208">Excluir seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1a138-208">Delete your app</span></span> | <span data-ttu-id="1a138-209">Escolha **visão geral**, em seguida, na barra de comandos hello, escolha **excluir**.</span><span class="sxs-lookup"><span data-stu-id="1a138-209">Choose **Overview**, then on hello command bar, choose **Delete**.</span></span> <span data-ttu-id="1a138-210">Insira o nome do seu aplicativo lógico e escolha **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="1a138-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="1a138-211">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="1a138-211">Get help</span></span>

<span data-ttu-id="1a138-212">tooask perguntas, responder às perguntas e saber quais outros aplicativos do Azure lógica os usuários estão fazendo, visite Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="1a138-212">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="1a138-213">toohelp aprimorar aplicativos do Azure lógica e os conectores, votar ou enviar ideias em Olá [site de comentários do usuário de aplicativos do Azure lógica](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="1a138-213">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a138-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1a138-214">Next steps</span></span>

*  [<span data-ttu-id="1a138-215">Adicionar condições e executar fluxos de trabalho</span><span class="sxs-lookup"><span data-stu-id="1a138-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="1a138-216">Modelos de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="1a138-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="1a138-217">Criar aplicativos lógicos a partir dos modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1a138-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
