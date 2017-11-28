---
title: "instrução aaaSwitch para ações diferentes em aplicativos do Azure lógica | Microsoft Docs"
description: "Escolha tooperform ações diferentes em aplicativos de lógica com base nos valores de expressão, usando uma instrução switch"
services: logic-apps
keywords: "Instrução switch"
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="c7e8e-104">Executar diferentes ações nos aplicativos lógicos com uma instrução switch</span><span class="sxs-lookup"><span data-stu-id="c7e8e-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="c7e8e-105">Ao criar um fluxo de trabalho, você geralmente tem tootake ações diferentes com base no valor de saudação de um objeto ou uma expressão.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-105">When authoring a workflow, you often have tootake different actions based on hello value of an object or expression.</span></span> <span data-ttu-id="c7e8e-106">Por exemplo, convém toobehave de aplicativo sua lógica diferente com base no código de status de saudação de uma solicitação HTTP, ou uma opção selecionada em um email.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-106">For example, you might want your logic app toobehave differently based on hello status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="c7e8e-107">Você pode usar um tooimplement de instrução switch esses cenários.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-107">You can use a switch statement tooimplement these scenarios.</span></span> <span data-ttu-id="c7e8e-108">Seu aplicativo lógico pode avaliar um token ou uma expressão e escolha caso Olá Olá Olá de tooexecute do mesmo valor especificado de ações.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-108">Your logic app can evaluate a token or expression, and choose hello case with hello same value tooexecute hello specified actions.</span></span> <span data-ttu-id="c7e8e-109">Apenas um caso deve coincidir com a instrução de comutador hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-109">Only one case should match hello switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="c7e8e-110">Assim como ocorre em todas as linguagens de programação, as instruções switch só dão suporte a operadores de igualdade.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="c7e8e-111">Se precisar de outros operadores relacionais, como “maior que”, use uma instrução de condição.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="c7e8e-112">comportamento de execução determinística tooensure, casos devem conter um valor exclusivo e estático em vez de tokens dinâmicos ou uma expressão.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-112">tooensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7e8e-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c7e8e-113">Prerequisites</span></span>

- <span data-ttu-id="c7e8e-114">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-114">An active Azure subscription.</span></span> <span data-ttu-id="c7e8e-115">Se você não tiver uma assinatura ativa do Azure, [criar uma conta gratuita](https://azure.microsoft.com/free/), ou tente [Aplicativos Lógicos gratuitamente](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c7e8e-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="c7e8e-116">Conhecimento básico sobre aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="c7e8e-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a><span data-ttu-id="c7e8e-117">Adicionar um fluxo de trabalho de tooyour de instrução switch</span><span class="sxs-lookup"><span data-stu-id="c7e8e-117">Add a switch statement tooyour workflow</span></span>

<span data-ttu-id="c7e8e-118">tooshow como uma instrução switch funciona, este exemplo cria um aplicativo lógico monitora arquivos carregados tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-118">tooshow how a switch statement works, this example creates a logic app that monitors files uploaded tooDropbox.</span></span> <span data-ttu-id="c7e8e-119">Quando novos arquivos de saudação forem carregados, o aplicativo de lógica de saudação envia aprovador tooan email escolhe se tootransfer tooSharePoint esses arquivos.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-119">When hello new files are uploaded, hello logic app sends email tooan approver who chooses whether tootransfer those files tooSharePoint.</span></span> <span data-ttu-id="c7e8e-120">aplicativo Hello usa uma instrução switch que executa ações diferentes com base no valor de Olá Olá aprovador seleciona.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-120">hello app uses a switch statement that performs different actions based on hello value that hello approver selects.</span></span>

1. <span data-ttu-id="c7e8e-121">Crie um aplicativo lógico e selecione este gatilho: **Dropbox – Quando um arquivo é criado**.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Use Dropbox - quando um arquivo é criado um gatilho](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="c7e8e-123">Em gatilho hello, adicione esta ação: **Outlook.com - enviar email de aprovação**</span><span class="sxs-lookup"><span data-stu-id="c7e8e-123">Under hello trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="c7e8e-124">O aplicativos lógicos também dão suporte a cenários de envio de email de aprovação de uma conta do Outlook do Office 365.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="c7e8e-125">Se você não tiver uma conexão existente, será solicitado que você toocreate um.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-125">If you don't have an existing connection, you're prompted toocreate one.</span></span>
   - <span data-ttu-id="c7e8e-126">Preencha os campos de saudação necessário.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-126">Fill in hello required fields.</span></span> <span data-ttu-id="c7e8e-127">Por exemplo, em **para**, especifique Olá endereço de email para enviar email do aprovador hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-127">For example, under **To**, specify hello email address for sending hello approver email.</span></span>
   - <span data-ttu-id="c7e8e-128">Em **User Options**, digite `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Configurar conexão](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="c7e8e-130">Adicione uma instrução switch.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-130">Add a switch statement.</span></span>

   - <span data-ttu-id="c7e8e-131">Selecione **+ Nova etapa** > **... Mais** > **Adicionar um caso de opção**.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="c7e8e-132">Agora, desejamos tooselect Olá ação tooperform com base em Olá `SelectedOptions` de saída de hello *enviar email de aprovação* ação.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-132">Now we want tooselect hello action tooperform based on hello `SelectedOptions` output from hello *Send approval email* action.</span></span> 
   <span data-ttu-id="c7e8e-133">Você pode encontrar esse campo em Olá **adicionar conteúdo dinâmico** seletor.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-133">You can find this field in hello **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="c7e8e-134">Use *caso 1* toohandle quando seleciona aprovador Olá `Approve`.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-134">Use *Case 1* toohandle when hello approver selects `Approve`.</span></span>
     - <span data-ttu-id="c7e8e-135">Se aprovada, copie Olá original arquivo tooSharePoint Online com hello [ **SharePoint Online - criar o arquivo** ação](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="c7e8e-135">If approved, copy hello original file tooSharePoint Online with hello [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="c7e8e-136">Adicione outra ação no hello toonotify caso usuários que um novo arquivo está disponível no SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-136">Add another action within hello case toonotify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="c7e8e-137">Adicionar outro toohandle caso quando o usuário seleciona `Reject`.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-137">Add another case toohandle when user selects `Reject`.</span></span>
     - <span data-ttu-id="c7e8e-138">Se rejeitada, envie um email de notificação informando outros aprovadores que arquivo hello é rejeitado e nenhuma ação adicional é necessária.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-138">If rejected, send a notification email informing other approvers that hello file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="c7e8e-139">`SelectedOptions`fornece apenas duas opções, portanto deixarmos Olá **padrão** caso vazio.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-139">`SelectedOptions` provides only two options, so we can leave hello **Default** case empty.</span></span>

   ![Instrução switch](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="c7e8e-141">Uma instrução switch precisa de pelo menos um caso no caso de padrão de toohello de adição.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-141">A switch statement needs at least one case in addition toohello default case.</span></span>

4. <span data-ttu-id="c7e8e-142">Após a instrução de comutador hello, excluir Olá original arquivo carregado tooDropbox adicionando esta ação: **Dropbox - excluir arquivo**</span><span class="sxs-lookup"><span data-stu-id="c7e8e-142">After hello switch statement, delete hello original file uploaded tooDropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="c7e8e-143">Salve seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-143">Save your logic app.</span></span> <span data-ttu-id="c7e8e-144">Teste seu aplicativo carregando um arquivo tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-144">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="c7e8e-145">Em breve, você deverá receber um email de aprovação.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="c7e8e-146">Selecione uma opção e observar o comportamento da saudação.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-146">Select an option, and observe hello behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="c7e8e-147">Check-out como muito[monitorar seus aplicativos lógicos](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="c7e8e-147">Check out how too[monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-hello-code-behind-switch-statements"></a><span data-ttu-id="c7e8e-148">Entender o código Olá instruções switch</span><span class="sxs-lookup"><span data-stu-id="c7e8e-148">Understand hello code behind switch statements</span></span>

<span data-ttu-id="c7e8e-149">Agora que você criou com êxito um aplicativo lógico usando uma instrução switch, vamos dar uma olhada na definição de código Olá atrás de instrução de comutador hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-149">Now that you successfully created a logic app using a switch statement, let's look at hello code definition behind hello switch statement.</span></span>

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* <span data-ttu-id="c7e8e-150">`"Switch"`é o nome de saudação da instrução de comutador hello, que pode ser renomeado para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-150">`"Switch"` is hello name of hello switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="c7e8e-151">`"type": "Switch"`indica que a ação de saudação é uma instrução switch.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-151">`"type": "Switch"` indicates that hello action is a switch statement.</span></span> 
* <span data-ttu-id="c7e8e-152">`"expression"`é a opção selecionada do aprovador Olá neste exemplo e é avaliado em relação a cada caso declarado posteriormente na definição de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-152">`"expression"` is hello approver's selected option in this example and is evaluated against each case declared later in hello definition.</span></span> 
* <span data-ttu-id="c7e8e-153">`"cases"` pode conter qualquer quantidade de casos.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="c7e8e-154">Para cada caso, `"Case *"` é nome do padrão de saudação do caso de Olá, que pode ser renomeado para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-154">For each case, `"Case *"` is hello default name of hello case, which you can rename for readability.</span></span> 
<span data-ttu-id="c7e8e-155">`"case"`Especifica o rótulo case hello, que Olá usos de expressão de switch para comparação e deve ser um valor constante e exclusivo.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-155">`"case"` specifies hello case label, which hello switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="c7e8e-156">Se nenhum dos casos Olá correspondem a expressão de comutador hello, ações sob `"default"` são executados.</span><span class="sxs-lookup"><span data-stu-id="c7e8e-156">If none of hello cases match hello switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="c7e8e-157">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="c7e8e-157">Get help</span></span>

<span data-ttu-id="c7e8e-158">tooask perguntas, responder a perguntas e veja que outros usuários de aplicativos do Azure lógicos estão fazendo, visite Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="c7e8e-158">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="c7e8e-159">toohelp aprimorar aplicativos do Azure lógica e os conectores, votar ou enviar ideias em Olá [site de comentários do usuário de aplicativos do Azure lógica](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="c7e8e-159">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7e8e-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c7e8e-160">Next steps</span></span>

- <span data-ttu-id="c7e8e-161">Saiba como muito[adicionar condições](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="c7e8e-161">Learn how too[add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="c7e8e-162">Saiba mais sobre [tratamento de erro e exceção](logic-apps-exception-handling.md)</span><span class="sxs-lookup"><span data-stu-id="c7e8e-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="c7e8e-163">Descubra mais [funcionalidades da linguagem do fluxo de trabalho](logic-apps-author-definitions.md)</span><span class="sxs-lookup"><span data-stu-id="c7e8e-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>