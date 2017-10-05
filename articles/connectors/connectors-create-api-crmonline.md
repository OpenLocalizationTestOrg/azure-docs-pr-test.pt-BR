---
title: "Conectar-se ao Dynamics 365 (online) do Aplicativo Lógico do Azure | Microsoft Docs"
description: "Criar fluxos de trabalho de aplicativo lógico que gerenciem entidades (online) do Dynamics 365 por meio da API fornecida pelo conector do Dynamics 365"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: d35647921ff540167a3a591fb489d3bab031a5c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-dynamics-365-from-logic-app-workflows"></a><span data-ttu-id="8ee60-103">Conectar-se ao Dynamics 365 de fluxos de trabalho de aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="8ee60-103">Connect to Dynamics 365 from logic app workflows</span></span>

<span data-ttu-id="8ee60-104">Com Aplicativos Lógicos, você pode se conectar ao Dynamics 365 (online) e criar fluxos de negócios úteis que criam registros, atualizam itens ou retornam uma lista de registros.</span><span class="sxs-lookup"><span data-stu-id="8ee60-104">With Logic Apps, you can connect to Dynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="8ee60-105">Com o conector do Dynamics 365, você pode:</span><span class="sxs-lookup"><span data-stu-id="8ee60-105">With the Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="8ee60-106">Compilar seu fluxo de negócios com base nos dados que obtém do Dynamics 365 (online).</span><span class="sxs-lookup"><span data-stu-id="8ee60-106">Build your business flow based on the data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="8ee60-107">Usar ações que obtêm uma resposta e disponibilizar a saída para outras ações.</span><span class="sxs-lookup"><span data-stu-id="8ee60-107">Use actions that get a response and then make the output available for other actions.</span></span> <span data-ttu-id="8ee60-108">Por exemplo, quando um item é atualizado no Dynamics 365 (online), você pode enviar um e-mail usando o Office 365.</span><span class="sxs-lookup"><span data-stu-id="8ee60-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="8ee60-109">Este tópico mostra como criar um aplicativo lógico que cria uma tarefa no Dynamics 365 sempre que um novo cliente em potencial é criado no Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="8ee60-109">This topic shows you how to create a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ee60-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8ee60-110">Prerequisites</span></span>
* <span data-ttu-id="8ee60-111">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee60-111">An Azure account.</span></span>
* <span data-ttu-id="8ee60-112">Uma conta do Dynamics 365 (online).</span><span class="sxs-lookup"><span data-stu-id="8ee60-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="8ee60-113">Criar uma tarefa sempre que um novo cliente em potencial é criado no Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="8ee60-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="8ee60-114">[Entrar no Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ee60-114">[Sign in to Azure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="8ee60-115">Na caixa de pesquisa do Azure, digite `Logic apps` e pressione ENTER.</span><span class="sxs-lookup"><span data-stu-id="8ee60-115">In the Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Localizar aplicativos lógicos](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="8ee60-117">Em **Aplicativos lógicos**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-117">Under **Logic apps**, click **Add**.</span></span>

      ![Adicionar LogicApp](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="8ee60-119">Para criar o aplicativo lógico, complete os campos **Nome**, **Assinatura**, **Grupo de Recursos** e **Local** e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-119">To create the logic app, complete the **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="8ee60-120">Selecione o novo aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="8ee60-120">Select the new logic app.</span></span> <span data-ttu-id="8ee60-121">Quando você receber a notificação **Implantação bem-sucedida**, clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-121">When you receive the **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="8ee60-122">Em **Ferramentas de Desenvolvimento**, clique em **Designer de Aplicativo Lógico**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="8ee60-123">Na lista de modelos, clique em **Aplicativo Lógico em Branco**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-123">In the template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="8ee60-124">Na caixa de pesquisa, digite `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="8ee60-124">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="8ee60-125">Na lista de disparadores Dynamics 365, selecione **Dynamics 365 – Quando um registro é criado**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-125">From the Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="8ee60-126">Se for solicitado que você entre no Dynamics 365, faça isso agora.</span><span class="sxs-lookup"><span data-stu-id="8ee60-126">If you are prompted to sign in to Dynamics 365, do so now.</span></span>

9.  <span data-ttu-id="8ee60-127">Nos detalhes do gatilho, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="8ee60-127">In the trigger details, enter the following information:</span></span>

  * <span data-ttu-id="8ee60-128">**Nome da organização**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-128">**Organization Name**.</span></span> <span data-ttu-id="8ee60-129">Selecione a instância do Dynamics 365 que você deseja que o aplicativo lógico ouça.</span><span class="sxs-lookup"><span data-stu-id="8ee60-129">Select the Dynamics 365 instance that you want the logic app to listen to.</span></span>

  * <span data-ttu-id="8ee60-130">**Nome da entidade**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-130">**Entity Name**.</span></span> <span data-ttu-id="8ee60-131">Selecione a entidade à qual você deseja escutar.</span><span class="sxs-lookup"><span data-stu-id="8ee60-131">Select the entity that you want to listen to.</span></span> <span data-ttu-id="8ee60-132">Esse evento atua como um gatilho para iniciar o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="8ee60-132">This event acts as a trigger to start the logic app.</span></span> 
  <span data-ttu-id="8ee60-133">Neste passo a passo, **Clientes em potencial** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="8ee60-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="8ee60-134">**Com que frequência você deseja verificar os itens?**</span><span class="sxs-lookup"><span data-stu-id="8ee60-134">**How often do you want to check for items?**</span></span> <span data-ttu-id="8ee60-135">Esses valores definem com que frequência o aplicativo lógico verifica atualizações relacionadas ao gatilho.</span><span class="sxs-lookup"><span data-stu-id="8ee60-135">These values set how often the logic app checks for updates related to the trigger.</span></span> <span data-ttu-id="8ee60-136">A configuração padrão é verificar se há atualizações a cada três minutos.</span><span class="sxs-lookup"><span data-stu-id="8ee60-136">The default setting is to check for updates every three minutes.</span></span>

    * <span data-ttu-id="8ee60-137">**Frequência**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-137">**Frequency**.</span></span> <span data-ttu-id="8ee60-138">Selecione segundos, minutos, horas ou dias.</span><span class="sxs-lookup"><span data-stu-id="8ee60-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="8ee60-139">**Intervalo**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-139">**Interval**.</span></span> <span data-ttu-id="8ee60-140">Insira o número de segundos, minutos, horas ou dias que você deseja que passem antes da próxima verificação.</span><span class="sxs-lookup"><span data-stu-id="8ee60-140">Enter the number of seconds, minutes, hours, or days that you want to pass before the next check.</span></span>

      ![Detalhes do Gatilho de Aplicativo Lógico](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="8ee60-142">Clique na caixa **Nova etapa** e depois clique em **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="8ee60-143">Na caixa de pesquisa, digite `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="8ee60-143">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="8ee60-144">Na lista de ações, selecione **Dynamics 365 – Criar um novo registro**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-144">From the actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="8ee60-145">Insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="8ee60-145">Enter the following information:</span></span>

    * <span data-ttu-id="8ee60-146">**Nome da organização**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-146">**Organization Name**.</span></span> <span data-ttu-id="8ee60-147">Selecione a instância do Dynamics 365 na qual você deseja que o fluxo crie o registro.</span><span class="sxs-lookup"><span data-stu-id="8ee60-147">Select the Dynamics 365 instance where you want the flow to create the record.</span></span> 
    <span data-ttu-id="8ee60-148">Observe que essa instância não precisa ser a mesma instância da qual o evento é disparado.</span><span class="sxs-lookup"><span data-stu-id="8ee60-148">Notice that this instance doesn’t have to be the same instance where the event is triggered from.</span></span>

    * <span data-ttu-id="8ee60-149">**Nome da entidade**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-149">**Entity Name**.</span></span> <span data-ttu-id="8ee60-150">Selecione a entidade que você deseja que crie um registro quando o evento é disparado.</span><span class="sxs-lookup"><span data-stu-id="8ee60-150">Select the entity that you want to create a record when the event is triggered.</span></span> 
    <span data-ttu-id="8ee60-151">Neste passo a passo, **Tarefas** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="8ee60-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="8ee60-152">Clique na caixa **Assunto** que é exibida.</span><span class="sxs-lookup"><span data-stu-id="8ee60-152">Click in the **Subject** box that appears.</span></span> <span data-ttu-id="8ee60-153">Na lista de conteúdo dinâmico que aparece, você pode selecionar qualquer um destes campos:</span><span class="sxs-lookup"><span data-stu-id="8ee60-153">From the dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="8ee60-154">**Sobrenome**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-154">**Last Name**.</span></span> <span data-ttu-id="8ee60-155">Selecionar este campo inserirá o sobrenome do lead no campo Assunto da tarefa quando a tarefa de registro for criada.</span><span class="sxs-lookup"><span data-stu-id="8ee60-155">Selecting this field inserts the last name for the lead into the Subject field for the task, when the task record is created.</span></span>
    * <span data-ttu-id="8ee60-156">**Tópico**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-156">**Topic**.</span></span> <span data-ttu-id="8ee60-157">Selecionar este campo inserirá o campo Tópico do lead no campo Assunto da tarefa quando a tarefa de registro for criada.</span><span class="sxs-lookup"><span data-stu-id="8ee60-157">Selecting this field inserts the Topic field for the lead into the Subject field for the task, when the task record is created.</span></span> 
    <span data-ttu-id="8ee60-158">Clique em **Tópico** para adicioná-lo à caixa **Assunto**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-158">Click **Topic** to add that to the **Subject** box.</span></span>

      ![Criar novos detalhes do registro do Aplicativo Lógico](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="8ee60-160">Clique em **Salvar** na barra de ferramentas do Designer de Aplicativo Lógico.</span><span class="sxs-lookup"><span data-stu-id="8ee60-160">On the Logic App Designer toolbar, click **Save**.</span></span>

    ![Barra de ferramentas do Designer do Aplicativo Lógico Salvar](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="8ee60-162">Para iniciar o Aplicativo Lógico, clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-162">To start the Logic App, click **Run**.</span></span>

    ![Barra de ferramentas do Designer do Aplicativo Lógico Salvar](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="8ee60-164">Agora, crie um registro de cliente em potencial no Dynamics 365 para Vendas e veja seu fluxo em ação!</span><span class="sxs-lookup"><span data-stu-id="8ee60-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="8ee60-165">Definir opções avançadas para uma etapa de aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="8ee60-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="8ee60-166">Para especificar como filtrar dados em uma etapa do aplicativo lógico, clique em **Mostrar opções avançadas** nessa etapa e, em seguida, adicione uma consulta de filtro ou order by.</span><span class="sxs-lookup"><span data-stu-id="8ee60-166">To specify how to filter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="8ee60-167">Por exemplo, você pode usar uma consulta de filtro para obter apenas contas ativas e ordenar pelo nome da conta.</span><span class="sxs-lookup"><span data-stu-id="8ee60-167">For example, you can use a filter query to get only active accounts and order by the account name.</span></span> <span data-ttu-id="8ee60-168">Para fazer isso, insira a consulta de filtro OData `statuscode eq 1` e selecione **Nome da Conta** no painel de conteúdo dinâmico.</span><span class="sxs-lookup"><span data-stu-id="8ee60-168">To perform this task, enter the OData filter query `statuscode eq 1`, and select **Account Name** from the dynamic content list.</span></span> <span data-ttu-id="8ee60-169">Mais informações: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) e [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span><span class="sxs-lookup"><span data-stu-id="8ee60-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Opções avançadas de aplicativo lógico](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="8ee60-171">Práticas recomendadas ao usar o opções avançadas</span><span class="sxs-lookup"><span data-stu-id="8ee60-171">Best practices when using advanced options</span></span>

<span data-ttu-id="8ee60-172">Observe que, ao adicionar um valor a um campo, você deve corresponder ao tipo de campo se digitar um valor ou selecionar um valor da lista de conteúdo dinâmico.</span><span class="sxs-lookup"><span data-stu-id="8ee60-172">When you add a value to a field, you must match the field type whether you type a value or select a value from the dynamic content list.</span></span>

<span data-ttu-id="8ee60-173">Tipo de campo</span><span class="sxs-lookup"><span data-stu-id="8ee60-173">Field type</span></span>  |<span data-ttu-id="8ee60-174">Como usar</span><span class="sxs-lookup"><span data-stu-id="8ee60-174">How to use</span></span>  |<span data-ttu-id="8ee60-175">Onde encontrar</span><span class="sxs-lookup"><span data-stu-id="8ee60-175">Where to find</span></span>  |<span data-ttu-id="8ee60-176">Nome</span><span class="sxs-lookup"><span data-stu-id="8ee60-176">Name</span></span>  |<span data-ttu-id="8ee60-177">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="8ee60-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="8ee60-178">Campos de texto</span><span class="sxs-lookup"><span data-stu-id="8ee60-178">Text fields</span></span>|<span data-ttu-id="8ee60-179">Campos de texto exigem uma única linha de texto ou conteúdo dinâmico que seja um campo de tipo de texto.</span><span class="sxs-lookup"><span data-stu-id="8ee60-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="8ee60-180">Exemplos incluem os campos Categoria e Subcategoria.</span><span class="sxs-lookup"><span data-stu-id="8ee60-180">Examples include the Category and Sub-Category fields.</span></span>|<span data-ttu-id="8ee60-181">Configurações > Personalizações > Personalizar o sistema > Entidades > Tarefa > Campos</span><span class="sxs-lookup"><span data-stu-id="8ee60-181">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="8ee60-182">categoria</span><span class="sxs-lookup"><span data-stu-id="8ee60-182">category</span></span> |<span data-ttu-id="8ee60-183">Linha única de texto</span><span class="sxs-lookup"><span data-stu-id="8ee60-183">Single Line of Text</span></span>        
<span data-ttu-id="8ee60-184">Campos de número inteiro</span><span class="sxs-lookup"><span data-stu-id="8ee60-184">Integer fields</span></span> | <span data-ttu-id="8ee60-185">Alguns campos exigem conteúdo inteiro ou dinâmico que seja um campo de tipo inteiro.</span><span class="sxs-lookup"><span data-stu-id="8ee60-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="8ee60-186">Exemplos incluem Porcentagem concluída e Duração.</span><span class="sxs-lookup"><span data-stu-id="8ee60-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="8ee60-187">Configurações > Personalizações > Personalizar o sistema > Entidades > Tarefa > Campos</span><span class="sxs-lookup"><span data-stu-id="8ee60-187">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="8ee60-188">percentcomplete</span><span class="sxs-lookup"><span data-stu-id="8ee60-188">percentcomplete</span></span> |<span data-ttu-id="8ee60-189">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="8ee60-189">Whole Number</span></span>         
<span data-ttu-id="8ee60-190">Campos de data</span><span class="sxs-lookup"><span data-stu-id="8ee60-190">Date fields</span></span> | <span data-ttu-id="8ee60-191">Alguns campos exigem a data inserida no formato dd/mm/aaaa ou conteúdo dinâmico que seja um campo do tipo data.</span><span class="sxs-lookup"><span data-stu-id="8ee60-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="8ee60-192">Exemplos incluem Criado em, Data de início, Início real, Último tempo de espera, Término real e Data de vencimento.</span><span class="sxs-lookup"><span data-stu-id="8ee60-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="8ee60-193">Configurações > Personalizações > Personalizar o sistema > Entidades > Tarefa > Campos</span><span class="sxs-lookup"><span data-stu-id="8ee60-193">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="8ee60-194">createdon</span><span class="sxs-lookup"><span data-stu-id="8ee60-194">createdon</span></span> |<span data-ttu-id="8ee60-195">Data e hora</span><span class="sxs-lookup"><span data-stu-id="8ee60-195">Date and Time</span></span>
<span data-ttu-id="8ee60-196">Campos que exigem um registro de ID e tipo de pesquisa</span><span class="sxs-lookup"><span data-stu-id="8ee60-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="8ee60-197">Alguns campos que fazem referência a outro registro de entidade exigem a ID do registro e o tipo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="8ee60-197">Some fields that reference another entity record require both the record ID and the lookup type.</span></span> |<span data-ttu-id="8ee60-198">Configurações > Personalizações > Personalizar o sistema > Entidades > Conta > Campos</span><span class="sxs-lookup"><span data-stu-id="8ee60-198">Settings > Customizations > Customize the System > Entities > Account > Fields</span></span>  | <span data-ttu-id="8ee60-199">accountid</span><span class="sxs-lookup"><span data-stu-id="8ee60-199">accountid</span></span>  | <span data-ttu-id="8ee60-200">Chave primária</span><span class="sxs-lookup"><span data-stu-id="8ee60-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="8ee60-201">Mais exemplos de campos que exigem uma ID de registro e tipo de pesquisa</span><span class="sxs-lookup"><span data-stu-id="8ee60-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="8ee60-202">Expandindo a tabela anterior, aqui há mais exemplos de campos que não funcionam com valores selecionados da lista de conteúdo dinâmica.</span><span class="sxs-lookup"><span data-stu-id="8ee60-202">Expanding on the previous table, here are more examples of fields that don't work with values selected from the dynamic content list.</span></span> <span data-ttu-id="8ee60-203">Em vez disso, esses campos exigem que uma ID de registro e o tipo de pesquisa sejam inseridos nos campos no PowerApps.</span><span class="sxs-lookup"><span data-stu-id="8ee60-203">Instead, these fields require both a record ID and lookup type entered into the fields in PowerApps.</span></span>  
* <span data-ttu-id="8ee60-204">Proprietário e Tipo de proprietário.</span><span class="sxs-lookup"><span data-stu-id="8ee60-204">Owner and Owner Type.</span></span> <span data-ttu-id="8ee60-205">O campo Proprietário deve ser uma ID de registro de usuário ou de equipe válida.</span><span class="sxs-lookup"><span data-stu-id="8ee60-205">The Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="8ee60-206">O Tipo de proprietário deve ser **systemusers** ou **equipes**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-206">The Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="8ee60-207">Cliente e Tipo de cliente.</span><span class="sxs-lookup"><span data-stu-id="8ee60-207">Customer and Customer Type.</span></span> <span data-ttu-id="8ee60-208">O campo Cliente deve ser uma ID de registro de contato ou conta válida.</span><span class="sxs-lookup"><span data-stu-id="8ee60-208">The Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="8ee60-209">O Tipo de proprietário deve ser **contas** ou **contatos**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-209">The Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="8ee60-210">Referente e Referente ao tipo.</span><span class="sxs-lookup"><span data-stu-id="8ee60-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="8ee60-211">O campo Referente deve ser uma ID de registro válida, como uma ID de registro de contato ou conta.</span><span class="sxs-lookup"><span data-stu-id="8ee60-211">The Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="8ee60-212">Referente ao tipo deve ser o tipo de pesquisa para o registro, como **contas** ou **contatos**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-212">The Regarding Type must be the lookup type for the record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="8ee60-213">O seguinte exemplo de ação de criação de tarefa adiciona um registro de conta que corresponde à ID de registro que a adiciona ao campo referente da tarefa.</span><span class="sxs-lookup"><span data-stu-id="8ee60-213">The following task creation action example adds an account record that corresponds to the record ID adding it to the regarding field of the task.</span></span>

![Fluxo recordId e conta tipo](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="8ee60-215">Este exemplo também atribui a tarefa a um usuário específico com base na ID de registro do usuário.</span><span class="sxs-lookup"><span data-stu-id="8ee60-215">This example also assigns the task to a specific user based on the user's record ID.</span></span>

![Fluxo recordId e conta tipo](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="8ee60-217">Para localizar uma ID de registro, consulte a seção a seguir: *Localizar a ID de registro*</span><span class="sxs-lookup"><span data-stu-id="8ee60-217">To find a record's ID, see the following section: *Find the record ID*</span></span>

## <a name="find-the-record-id"></a><span data-ttu-id="8ee60-218">Localize a ID de registro</span><span class="sxs-lookup"><span data-stu-id="8ee60-218">Find the record ID</span></span>

1. <span data-ttu-id="8ee60-219">Abra um registro, como um registro de conta.</span><span class="sxs-lookup"><span data-stu-id="8ee60-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="8ee60-220">Na barra de ferramentas Ações, clique em **Pop Out** ![registro de pop-up](./media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="8ee60-220">On the actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="8ee60-221">Como alternativa, na barra de ferramentas Ações, para copiar a URL completa no seu programa de email padrão, clique em **ENVIAR LINK POR EMAIL**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-221">Alternatively, on the actions toolbar, to copy the full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="8ee60-222">A ID de registro é exibida entre os caracteres de codificação % 7b e %7 da URL.</span><span class="sxs-lookup"><span data-stu-id="8ee60-222">The record ID is displayed in between the %7b and %7d encoding characters of the URL.</span></span>

   ![Fluxo recordId e conta tipo](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="8ee60-224">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="8ee60-224">Troubleshooting</span></span>
<span data-ttu-id="8ee60-225">Para solucionar uma falha de uma etapa em um aplicativo lógico, exiba os detalhes de status do evento.</span><span class="sxs-lookup"><span data-stu-id="8ee60-225">To troubleshoot a failed step in a logic app, view the status details of the event.</span></span>

1. <span data-ttu-id="8ee60-226">Em **Aplicativos Lógicos**, clique no seu aplicativo lógico e, em seguida, em **Visão geral**.</span><span class="sxs-lookup"><span data-stu-id="8ee60-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="8ee60-227">A área Resumo é exibida, fornecendo o status de execução do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="8ee60-227">The Summary area is shown and provides the run status for the logic app.</span></span> 

   ![Status de execução do aplicativo lógico](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="8ee60-229">Se houver execuções com falha, clique no evento com falha sobre o qual você deseja exibir mais informações.</span><span class="sxs-lookup"><span data-stu-id="8ee60-229">To view more information about any failed runs, click the failed event.</span></span> <span data-ttu-id="8ee60-230">Para expandir uma etapa com falha, clique nessa etapa.</span><span class="sxs-lookup"><span data-stu-id="8ee60-230">To expand a failed step, click that step.</span></span>

   ![Expandir etapa com falha](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="8ee60-232">Os detalhes da etapa aparecem e podem ajudar a diagnosticar a causa da falha.</span><span class="sxs-lookup"><span data-stu-id="8ee60-232">The step details appear and can help troubleshoot the cause of the failure.</span></span>

   ![Detalhes da etapa com falha](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="8ee60-234">Para obter mais informações sobre como solucionar problemas de aplicativos lógicos, consulte [Diagnosticando falhas do aplicativo lógico](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="8ee60-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="8ee60-235">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="8ee60-235">Connector-specific details</span></span>

<span data-ttu-id="8ee60-236">Exiba os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/crm/).</span><span class="sxs-lookup"><span data-stu-id="8ee60-236">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8ee60-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8ee60-237">Next steps</span></span>
<span data-ttu-id="8ee60-238">Explore os outros conectores disponíveis nos Aplicativos Lógicos em nossa [lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="8ee60-238">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
