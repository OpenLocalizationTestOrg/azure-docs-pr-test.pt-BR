---
title: "Criar seu primeiro fluxo de trabalho entre os aplicativos de nuvem e os serviços de nuvem - Aplicativo Lógico do Azure | Microsoft Docs"
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
ms.openlocfilehash: 204bf123509729b60b55c306050cef54aa7fecc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-logic-app-workflow-to-automate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="1e699-104">Criar seu primeiro fluxo de trabalho lógico para automatizar os processos entre os aplicativos de nuvem e os serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="1e699-104">Create your first logic app workflow to automate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="1e699-105">Sem escrever nenhum código, você pode automatizar os processos de negócios mais fácil e rapidamente quando cria e executa os fluxos de trabalho com o [Aplicativo Lógico do Azure](logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1e699-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="1e699-106">Este primeiro exemplo mostra como criar um fluxo de trabalho de aplicativo lógico básico que verifica um RSS feed para o novo conteúdo em um site.</span><span class="sxs-lookup"><span data-stu-id="1e699-106">This first example shows how to create a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="1e699-107">Quando novos itens aparecem no feed do site, o aplicativo lógico envia um email de uma conta do Outlook ou do Gmail.</span><span class="sxs-lookup"><span data-stu-id="1e699-107">When new items appear in the website's feed, the logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="1e699-108">Para criar e executar um aplicativo lógico, você precisa destes itens:</span><span class="sxs-lookup"><span data-stu-id="1e699-108">To create and run a logic app, you need these items:</span></span>

* <span data-ttu-id="1e699-109">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e699-109">An Azure subscription.</span></span> <span data-ttu-id="1e699-110">Se você não tiver uma assinatura, poderá [iniciar com uma conta gratuita do Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="1e699-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="1e699-111">Caso contrário, você pode [inscrever-se para uma assinatura Pré-paga](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="1e699-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="1e699-112">Sua assinatura do Azure é usada para a cobrança de uso do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1e699-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="1e699-113">Saiba como a [medição de uso](../logic-apps/logic-apps-pricing.md) e os [preços](https://azure.microsoft.com/pricing/details/logic-apps) funcionam para os Aplicativos Lógicos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e699-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="1e699-114">Além disso, este exemplo requer estes itens:</span><span class="sxs-lookup"><span data-stu-id="1e699-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="1e699-115">Uma conta do Gmail, Office 365 Outlook ou Outlook.com</span><span class="sxs-lookup"><span data-stu-id="1e699-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="1e699-116">Se você tiver uma [conta da Microsoft](https://account.microsoft.com/account) pessoal, terá uma conta do Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="1e699-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="1e699-117">Caso contrário, se tiver uma conta corporativa ou de estudante do Azure, terá uma conta do **Outlook do Office 365**.</span><span class="sxs-lookup"><span data-stu-id="1e699-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="1e699-118">Um link para o RSS feed de um site.</span><span class="sxs-lookup"><span data-stu-id="1e699-118">A link to a website's RSS feed.</span></span> <span data-ttu-id="1e699-119">Este exemplo usa o [RSS feed para as principais matérias do site CNN.com](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="1e699-119">This example uses the [RSS feed for top stories from the CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="1e699-120">Adicionar um gatilho que inicia o fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="1e699-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="1e699-121">Um [ *gatilho* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) é um evento que inicia o fluxo de trabalho do aplicativo lógico e é o primeiro item que seu aplicativo lógico precisa.</span><span class="sxs-lookup"><span data-stu-id="1e699-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is the first item that your logic app needs.</span></span>

1. <span data-ttu-id="1e699-122">Entre no [portal do Azure](https://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="1e699-122">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="1e699-123">No menu à esquerda, escolha **Novo** > **Enterprise Integration** > **Aplicativo Lógico**, como mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="1e699-123">From the left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Portal do Azure, Novo, Enterprise Integration, Aplicativo Lógico](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="1e699-125">Você também pode escolher **Novo** e, na caixa de pesquisa, digitar `logic app` e pressionar Enter.</span><span class="sxs-lookup"><span data-stu-id="1e699-125">You can also choose **New**, then in the search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="1e699-126">Então, escolha **Aplicativo Lógico** > **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1e699-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="1e699-127">Nomeie seu aplicativo lógico e selecione sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e699-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="1e699-128">Agora, crie ou selecione um grupo de recursos do Azure, o que ajuda a organizar e gerenciar os recursos do Azure afins.</span><span class="sxs-lookup"><span data-stu-id="1e699-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="1e699-129">Por fim, selecione o local do datacenter para hospedar seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1e699-129">Finally, select the datacenter location for hosting your logic app.</span></span> <span data-ttu-id="1e699-130">Quando você estiver pronto, escolha **Fixar no painel** e **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1e699-130">When you're ready, choose **Pin to dashboard** and then **Create**.</span></span>

     ![Detalhes do aplicativo lógico](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="1e699-132">Quando você selecionar **Fixar no painel**, seu aplicativo lógico aparecerá no painel do Azure após a implantação e será aberto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1e699-132">When you select **Pin to dashboard**, your logic app appears on the Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="1e699-133">Se seu aplicativo lógico não aparecer no painel, no bloco **Todos os recursos**, escolha **Ver Mais** e selecione seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1e699-133">If your logic app doesn't appear on the dashboard, on the **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="1e699-134">No menu à esquerda, clique em **Mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="1e699-134">Or on the left menu, choose **More services**.</span></span> <span data-ttu-id="1e699-135">Em **Enterprise Integration**, escolha **Aplicativos Lógicos** e selecione seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1e699-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="1e699-136">Quando você abrir seu aplicativo lógico pela primeira vez, o Designer do Aplicativo Lógico mostrará os modelos que você pode usar para começar.</span><span class="sxs-lookup"><span data-stu-id="1e699-136">When you open your logic app for the first time, the Logic App Designer shows templates that you can use to get started.</span></span> <span data-ttu-id="1e699-137">Por ora, escolha **Aplicativo Lógico em Branco** para poder compilar seu aplicativo lógico do zero.</span><span class="sxs-lookup"><span data-stu-id="1e699-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="1e699-138">A lógica de aplicativo Designer é aberto e mostra os serviços disponíveis e *gatilhos* que você pode usar em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1e699-138">The Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="1e699-139">Na caixa de pesquisa, digite `RSS` e selecione este gatilho: **RSS - quando um item do feed é publicado**</span><span class="sxs-lookup"><span data-stu-id="1e699-139">In the search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![Gatilho do RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="1e699-141">Insira o link do RSS feed do site que você deseja controlar.</span><span class="sxs-lookup"><span data-stu-id="1e699-141">Enter the link for the website's RSS feed that you want to track.</span></span> 

     <span data-ttu-id="1e699-142">Você também pode alterar a **Frequência** e o **Intervalo**.</span><span class="sxs-lookup"><span data-stu-id="1e699-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="1e699-143">Essas configurações determinam a frequência com que o aplicativo lógico verifica se há novos itens e retorna todos os itens encontrados durante esse período de tempo.</span><span class="sxs-lookup"><span data-stu-id="1e699-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="1e699-144">Para este exemplo, iremos verificar todo dia as principais matérias postadas no site da CNN.</span><span class="sxs-lookup"><span data-stu-id="1e699-144">For this example, let's check every day for   top stories posted to the CNN website.</span></span>

     ![Configurar um gatilho com o RSS feed, frequência e intervalo](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="1e699-146">Salve seu trabalho agora.</span><span class="sxs-lookup"><span data-stu-id="1e699-146">Save your work for now.</span></span> <span data-ttu-id="1e699-147">(Na barra de comandos do designer, escolha **Salvar**.)</span><span class="sxs-lookup"><span data-stu-id="1e699-147">(On the designer command bar, choose **Save**.)</span></span>

   ![Salve seu aplicativo lógico](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="1e699-149">Quando você salva, seu aplicativo lógico fica ativo, mas no momento, seu aplicativo lógico só verifica os novos itens no RSS feed especificado.</span><span class="sxs-lookup"><span data-stu-id="1e699-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in the specified RSS feed.</span></span> 
   <span data-ttu-id="1e699-150">Para tornar este exemplo mais útil, adicionamos uma ação que seu aplicativo lógico executa após o gatilho disparar.</span><span class="sxs-lookup"><span data-stu-id="1e699-150">To make this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-to-your-trigger"></a><span data-ttu-id="1e699-151">Adicionar uma ação que responde a seu gatilho</span><span class="sxs-lookup"><span data-stu-id="1e699-151">Add an action that responds to your trigger</span></span>

<span data-ttu-id="1e699-152">Uma [*ação*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) é uma tarefa executada pelo fluxo de trabalho do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1e699-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="1e699-153">Depois de adicionar um gatilho ao seu aplicativo lógico, você poderá adicionar uma ação para executar operações com os dados gerados por esse gatilho.</span><span class="sxs-lookup"><span data-stu-id="1e699-153">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="1e699-154">Para nosso exemplo, agora adicionaremos uma ação que envia email quando novos itens aparecem no RSS feed do site.</span><span class="sxs-lookup"><span data-stu-id="1e699-154">For our example, we now add an action that sends email when new items appear in the website's RSS feed.</span></span>

1. <span data-ttu-id="1e699-155">No designer, no gatilho, escolha **Nova etapa** > **Adicionar uma ação**, como mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="1e699-155">In the designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Adicionar uma ação](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="1e699-157">O designer mostra os [conectores disponíveis](../connectors/apis-list.md) para que você possa selecionar uma ação para executar quando o gatilho disparar.</span><span class="sxs-lookup"><span data-stu-id="1e699-157">The designer shows [available connectors](../connectors/apis-list.md) so that you can select an action to perform when your trigger fires.</span></span>

2. <span data-ttu-id="1e699-158">Com base em sua conta de email, siga as etapas do Outlook ou do Gmail.</span><span class="sxs-lookup"><span data-stu-id="1e699-158">Based on your email account, follow the steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="1e699-159">Para enviar um email de sua conta do Outlook, na caixa de pesquisa, digite `outlook`.</span><span class="sxs-lookup"><span data-stu-id="1e699-159">To send email from your Outlook account, in the search box, enter `outlook`.</span></span> <span data-ttu-id="1e699-160">Em **Serviços**, escolha **Outlook.com** para as contas pessoais da Microsoft ou escolha **Outlook do Office 365** para as contas corporativas ou de estudante do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e699-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="1e699-161">Em **Ações**, selecione **Enviar um email**.</span><span class="sxs-lookup"><span data-stu-id="1e699-161">Under **Actions**, select **Send an email**.</span></span>

       ![Selecionar a ação "Enviar um email" do Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="1e699-163">Para enviar um email de sua conta do Gmail, na caixa de pesquisa, digite `gmail`.</span><span class="sxs-lookup"><span data-stu-id="1e699-163">To send email from your Gmail account, in the search box, enter `gmail`.</span></span> 
   <span data-ttu-id="1e699-164">Em **Ações**, selecione **Enviar email**.</span><span class="sxs-lookup"><span data-stu-id="1e699-164">Under **Actions**, select **Send email**.</span></span>

       ![Escolher "Gmail - enviar email"](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="1e699-166">Quando as credenciais forem solicitadas, entre com o nome de usuário e a senha de sua conta de email.</span><span class="sxs-lookup"><span data-stu-id="1e699-166">When you're prompted for credentials, sign in with the username and password for your email account.</span></span> 

4. <span data-ttu-id="1e699-167">Forneça os detalhes desta ação, como o endereço de email de destino, e escolha os parâmetros para os dados a incluir no email, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1e699-167">Provide the details for this action, like the destination email address, and choose the parameters for the data to include in the email, for example:</span></span>

   ![Selecionar os dados a incluir no email](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="1e699-169">Portanto, se você escolheu o Outlook, seu aplicativo lógico poderá parecer com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="1e699-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![Aplicativo lógico concluído](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="1e699-171">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="1e699-171">Save your changes.</span></span> <span data-ttu-id="1e699-172">(Na barra de comandos do designer, escolha **Salvar**.)</span><span class="sxs-lookup"><span data-stu-id="1e699-172">(On the designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="1e699-173">Agora, você pode executar manualmente seu aplicativo lógico para testar.</span><span class="sxs-lookup"><span data-stu-id="1e699-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="1e699-174">Na barra de comandos do designer, escolha **Executar**.</span><span class="sxs-lookup"><span data-stu-id="1e699-174">On the designer command bar, choose **Run**.</span></span> <span data-ttu-id="1e699-175">Caso contrário, você pode deixar seu aplicativo lógico verificar o RSS feed especificado com base no agendamento configurado.</span><span class="sxs-lookup"><span data-stu-id="1e699-175">Otherwise, you can let your logic app check the specified RSS feed based on the schedule that you set up.</span></span>

   <span data-ttu-id="1e699-176">Se seu aplicativo lógico encontrar novos itens, ele enviará um email que inclui os dados selecionados.</span><span class="sxs-lookup"><span data-stu-id="1e699-176">If your logic app finds new items, the logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="1e699-177">Se nenhum item novo for encontrado, seu aplicativo lógico irá ignorar a ação que envia um email.</span><span class="sxs-lookup"><span data-stu-id="1e699-177">If no new items are found, your logic app skips the action that sends email.</span></span>

7. <span data-ttu-id="1e699-178">Para monitorar e verificar a execução de seu aplicativo lógico e o histórico de gatilhos, no menu do aplicativo lógico, escolha **Visão Geral**.</span><span class="sxs-lookup"><span data-stu-id="1e699-178">To monitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Monitorar e verificar a execução de seu aplicativo lógico e o histórico de gatilhos](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="1e699-180">Se você não encontrar os dados esperados, na barra de comandos, escolha **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="1e699-180">If you don't find the data that you expect, on the command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="1e699-181">Para saber mais sobre o status de seu aplicativo lógico, a execução e o histórico de gatilhos, ou para diagnosticar seu aplicativo lógico, consulte [Solucionar problemas de seu aplicativo lógico](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="1e699-181">To learn more about your logic app's status or run and trigger history, or to diagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="1e699-182">Seu aplicativo lógico continuará sendo executado até que você desative o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1e699-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="1e699-183">Para desativar seu aplicativo agora, no menu de aplicativo lógico, escolha **Visão Geral**.</span><span class="sxs-lookup"><span data-stu-id="1e699-183">To turn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="1e699-184">Na barra de comandos, escolha **Desabilitar**.</span><span class="sxs-lookup"><span data-stu-id="1e699-184">On the command bar, choose **Disable**.</span></span>

<span data-ttu-id="1e699-185">Parabéns, você acabou de configurar e executar seu primeiro aplicativo lógico básico.</span><span class="sxs-lookup"><span data-stu-id="1e699-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="1e699-186">Você também aprendeu como é fácil criar fluxos de trabalho que automatizam os processos e integram os aplicativos e serviços de nuvem - tudo sem código.</span><span class="sxs-lookup"><span data-stu-id="1e699-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="1e699-187">Gerenciar seu aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="1e699-187">Manage your logic app</span></span>

<span data-ttu-id="1e699-188">Para gerenciar seu aplicativo, você pode executar tarefas como verificar o status, editar, exibir histórico, desativar ou excluir seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1e699-188">To manage your app, you can perform tasks like check the status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="1e699-189">Entre no [portal do Azure](https://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="1e699-189">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="1e699-190">No menu à esquerda, clique em **Mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="1e699-190">On the left menu, choose **More services**.</span></span> <span data-ttu-id="1e699-191">Em **Enterprise Integration**, escolha **Aplicativos Lógicos**.</span><span class="sxs-lookup"><span data-stu-id="1e699-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="1e699-192">Selecione seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1e699-192">Select your logic app.</span></span> 

   <span data-ttu-id="1e699-193">No menu do aplicativo lógico, você pode encontrar estas tarefas de gerenciamento do aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="1e699-193">In the logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="1e699-194">Tarefa</span><span class="sxs-lookup"><span data-stu-id="1e699-194">Task</span></span>|<span data-ttu-id="1e699-195">Etapas</span><span class="sxs-lookup"><span data-stu-id="1e699-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="1e699-196">Exibir o status, histórico de execução e informações gerais de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1e699-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="1e699-197">Escolha **Visão Geral**.</span><span class="sxs-lookup"><span data-stu-id="1e699-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="1e699-198">Editar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1e699-198">Edit your app</span></span> | <span data-ttu-id="1e699-199">Escolha **Designer de Aplicativos Lógicos**.</span><span class="sxs-lookup"><span data-stu-id="1e699-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="1e699-200">Exibir a definição JSON do fluxo de trabalho de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1e699-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="1e699-201">Escolha **Exibir Código do Aplicativo Lógico**.</span><span class="sxs-lookup"><span data-stu-id="1e699-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="1e699-202">Exibir as operações executadas em seu aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="1e699-202">View operations performed on your logic app</span></span> | <span data-ttu-id="1e699-203">Escolha **Log de atividades**.</span><span class="sxs-lookup"><span data-stu-id="1e699-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="1e699-204">Exibir as antigas versões de seu aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="1e699-204">View past versions for your logic app</span></span> | <span data-ttu-id="1e699-205">Escolha **Versões**.</span><span class="sxs-lookup"><span data-stu-id="1e699-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="1e699-206">Desativar temporariamente seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1e699-206">Turn off your app temporarily</span></span> | <span data-ttu-id="1e699-207">Escolha **Visão Geral**, em seguida, na barra de comandos, escolha **Desabilitar**.</span><span class="sxs-lookup"><span data-stu-id="1e699-207">Choose **Overview**, then on the command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="1e699-208">Excluir seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1e699-208">Delete your app</span></span> | <span data-ttu-id="1e699-209">Escolha **Visão Geral**, em seguida, na barra de comandos, escolha **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="1e699-209">Choose **Overview**, then on the command bar, choose **Delete**.</span></span> <span data-ttu-id="1e699-210">Insira o nome do seu aplicativo lógico e escolha **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="1e699-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="1e699-211">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="1e699-211">Get help</span></span>

<span data-ttu-id="1e699-212">Para fazer perguntas, responder a perguntas e saber o que os outros usuários dos Aplicativos Lógicos do Azure estão fazendo, visite o [fórum de Aplicativos Lógicos do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="1e699-212">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="1e699-213">Para ajudar a melhorar os Aplicativos Lógicos do Azure e conectores, vote ou envie ideias no [site de comentários do usuário dos Aplicativos Lógicos do Azure](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="1e699-213">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e699-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1e699-214">Next steps</span></span>

*  [<span data-ttu-id="1e699-215">Adicionar condições e executar fluxos de trabalho</span><span class="sxs-lookup"><span data-stu-id="1e699-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="1e699-216">Modelos de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="1e699-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="1e699-217">Criar aplicativos lógicos a partir dos modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1e699-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
