---
title: "aaaConnect tooDynamics 365 (online) de aplicativos do Azure lógica | Microsoft Docs"
description: "Criar lógica de fluxos de trabalho do aplicativo gerenciar entidades de Dynamics 365 (online) por meio de saudação API fornecida pelo conector Olá Dynamics 365"
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
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a><span data-ttu-id="72426-103">Conecte-se tooDynamics 365 dos fluxos de trabalho de aplicativo de lógica</span><span class="sxs-lookup"><span data-stu-id="72426-103">Connect tooDynamics 365 from logic app workflows</span></span>

<span data-ttu-id="72426-104">Com lógica de aplicativos, você pode se conectar tooDynamics 365 (online) e criar fluxos de negócios útil criar registros, atualizar itens ou retornam uma lista de registros.</span><span class="sxs-lookup"><span data-stu-id="72426-104">With Logic Apps, you can connect tooDynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="72426-105">Com o conector de saudação do Dynamics 365, você pode:</span><span class="sxs-lookup"><span data-stu-id="72426-105">With hello Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="72426-106">Crie o fluxo de negócios com base em dados Olá obtido Dynamics 365 (online).</span><span class="sxs-lookup"><span data-stu-id="72426-106">Build your business flow based on hello data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="72426-107">Use as ações que uma resposta de obtenção e saída de hello tornar disponível para outras ações.</span><span class="sxs-lookup"><span data-stu-id="72426-107">Use actions that get a response and then make hello output available for other actions.</span></span> <span data-ttu-id="72426-108">Por exemplo, quando um item é atualizado no Dynamics 365 (online), você pode enviar um e-mail usando o Office 365.</span><span class="sxs-lookup"><span data-stu-id="72426-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="72426-109">Este tópico mostra como toocreate um lógica de aplicativo que cria uma tarefa no Dynamics 365 sempre que um novo cliente potencial é criado no Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="72426-109">This topic shows you how toocreate a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72426-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="72426-110">Prerequisites</span></span>
* <span data-ttu-id="72426-111">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="72426-111">An Azure account.</span></span>
* <span data-ttu-id="72426-112">Uma conta do Dynamics 365 (online).</span><span class="sxs-lookup"><span data-stu-id="72426-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="72426-113">Criar uma tarefa sempre que um novo cliente em potencial é criado no Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="72426-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="72426-114">[Entrar tooAzure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="72426-114">[Sign in tooAzure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="72426-115">Na caixa de pesquisa do Azure hello, digite `Logic apps`, e pressione ENTER.</span><span class="sxs-lookup"><span data-stu-id="72426-115">In hello Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Localizar aplicativos lógicos](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="72426-117">Em **Aplicativos lógicos**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="72426-117">Under **Logic apps**, click **Add**.</span></span>

      ![Adicionar LogicApp](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="72426-119">aplicativo lógico do hello toocreate, Olá completa **nome**, **assinatura**, **grupo de recursos**, e **local** campos e, em seguida, clique em  **Criar**.</span><span class="sxs-lookup"><span data-stu-id="72426-119">toocreate hello logic app, complete hello **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="72426-120">Selecione Olá novo aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="72426-120">Select hello new logic app.</span></span> <span data-ttu-id="72426-121">Quando você receber Olá **implantação bem-sucedida** notificação, clique em **atualizar**.</span><span class="sxs-lookup"><span data-stu-id="72426-121">When you receive hello **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="72426-122">Em **Ferramentas de Desenvolvimento**, clique em **Designer de Aplicativo Lógico**.</span><span class="sxs-lookup"><span data-stu-id="72426-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="72426-123">Na lista de modelos de saudação, clique em **aplicativo lógica em branco**.</span><span class="sxs-lookup"><span data-stu-id="72426-123">In hello template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="72426-124">Na caixa de pesquisa hello, digite `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="72426-124">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="72426-125">No hello Dynamics 365 dispara lista, selecione **Dynamics 365 – quando um registro é criado**.</span><span class="sxs-lookup"><span data-stu-id="72426-125">From hello Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="72426-126">Se você for solicitado toosign em tooDynamics 365, faça isso agora.</span><span class="sxs-lookup"><span data-stu-id="72426-126">If you are prompted toosign in tooDynamics 365, do so now.</span></span>

9.  <span data-ttu-id="72426-127">Nos detalhes de gatilho hello, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="72426-127">In hello trigger details, enter hello following information:</span></span>

  * <span data-ttu-id="72426-128">**Nome da organização**.</span><span class="sxs-lookup"><span data-stu-id="72426-128">**Organization Name**.</span></span> <span data-ttu-id="72426-129">Selecione Olá Dynamics 365 instância que você deseja Olá lógica aplicativo toolisten para.</span><span class="sxs-lookup"><span data-stu-id="72426-129">Select hello Dynamics 365 instance that you want hello logic app toolisten to.</span></span>

  * <span data-ttu-id="72426-130">**Nome da entidade**.</span><span class="sxs-lookup"><span data-stu-id="72426-130">**Entity Name**.</span></span> <span data-ttu-id="72426-131">Selecione a entidade de saudação que você deseja toolisten para.</span><span class="sxs-lookup"><span data-stu-id="72426-131">Select hello entity that you want toolisten to.</span></span> <span data-ttu-id="72426-132">Esse evento atua como um aplicativo de lógica do gatilho toostart hello.</span><span class="sxs-lookup"><span data-stu-id="72426-132">This event acts as a trigger toostart hello logic app.</span></span> 
  <span data-ttu-id="72426-133">Neste passo a passo, **Clientes em potencial** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="72426-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="72426-134">**Com que frequência você deseja toocheck para itens?**</span><span class="sxs-lookup"><span data-stu-id="72426-134">**How often do you want toocheck for items?**</span></span> <span data-ttu-id="72426-135">Esses valores são definidos como geralmente Olá lógica aplicativo verifica para gatilho de toohello relacionados de atualizações.</span><span class="sxs-lookup"><span data-stu-id="72426-135">These values set how often hello logic app checks for updates related toohello trigger.</span></span> <span data-ttu-id="72426-136">configuração de padrão de saudação é toocheck para atualizações a cada três minutos.</span><span class="sxs-lookup"><span data-stu-id="72426-136">hello default setting is toocheck for updates every three minutes.</span></span>

    * <span data-ttu-id="72426-137">**Frequência**.</span><span class="sxs-lookup"><span data-stu-id="72426-137">**Frequency**.</span></span> <span data-ttu-id="72426-138">Selecione segundos, minutos, horas ou dias.</span><span class="sxs-lookup"><span data-stu-id="72426-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="72426-139">**Intervalo**.</span><span class="sxs-lookup"><span data-stu-id="72426-139">**Interval**.</span></span> <span data-ttu-id="72426-140">Insira o número de saudação de segundos, minutos, horas ou dias que você deseja toopass antes da próxima verificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="72426-140">Enter hello number of seconds, minutes, hours, or days that you want toopass before hello next check.</span></span>

      ![Detalhes do Gatilho de Aplicativo Lógico](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="72426-142">Clique na caixa **Nova etapa** e depois clique em **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="72426-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="72426-143">Na caixa de pesquisa hello, digite `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="72426-143">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="72426-144">Na lista de ações de saudação, selecione **Dynamics 365 – criar um novo registro**.</span><span class="sxs-lookup"><span data-stu-id="72426-144">From hello actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="72426-145">Digite hello informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="72426-145">Enter hello following information:</span></span>

    * <span data-ttu-id="72426-146">**Nome da organização**.</span><span class="sxs-lookup"><span data-stu-id="72426-146">**Organization Name**.</span></span> <span data-ttu-id="72426-147">Selecione a instância de saudação do Dynamics 365 onde você deseja que o registro de Olá Olá fluxo toocreate.</span><span class="sxs-lookup"><span data-stu-id="72426-147">Select hello Dynamics 365 instance where you want hello flow toocreate hello record.</span></span> 
    <span data-ttu-id="72426-148">Observe que essa instância não tem toobe Olá mesmo instância onde o evento de saudação é disparado do.</span><span class="sxs-lookup"><span data-stu-id="72426-148">Notice that this instance doesn’t have toobe hello same instance where hello event is triggered from.</span></span>

    * <span data-ttu-id="72426-149">**Nome da entidade**.</span><span class="sxs-lookup"><span data-stu-id="72426-149">**Entity Name**.</span></span> <span data-ttu-id="72426-150">Selecione a entidade de saudação que você deseja toocreate um registro quando Olá evento for disparado.</span><span class="sxs-lookup"><span data-stu-id="72426-150">Select hello entity that you want toocreate a record when hello event is triggered.</span></span> 
    <span data-ttu-id="72426-151">Neste passo a passo, **Tarefas** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="72426-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="72426-152">Clique em Olá **assunto** caixa que aparece.</span><span class="sxs-lookup"><span data-stu-id="72426-152">Click in hello **Subject** box that appears.</span></span> <span data-ttu-id="72426-153">Olá dinâmico conteúdo lista que aparece, você pode selecionar qualquer um desses campos:</span><span class="sxs-lookup"><span data-stu-id="72426-153">From hello dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="72426-154">**Sobrenome**.</span><span class="sxs-lookup"><span data-stu-id="72426-154">**Last Name**.</span></span> <span data-ttu-id="72426-155">Selecionar este campo insere Olá sobrenome Olá lead campo assunto Olá tarefa Olá, quando Olá tarefa registro é criado.</span><span class="sxs-lookup"><span data-stu-id="72426-155">Selecting this field inserts hello last name for hello lead into hello Subject field for hello task, when hello task record is created.</span></span>
    * <span data-ttu-id="72426-156">**Tópico**.</span><span class="sxs-lookup"><span data-stu-id="72426-156">**Topic**.</span></span> <span data-ttu-id="72426-157">Selecionar este campo inserções Olá tópico campo cliente potencial de saudação no campo de assunto Olá para tarefa Olá, quando Olá tarefa registro é criado.</span><span class="sxs-lookup"><span data-stu-id="72426-157">Selecting this field inserts hello Topic field for hello lead into hello Subject field for hello task, when hello task record is created.</span></span> 
    <span data-ttu-id="72426-158">Clique em **tópico** tooadd que toohello **assunto** caixa.</span><span class="sxs-lookup"><span data-stu-id="72426-158">Click **Topic** tooadd that toohello **Subject** box.</span></span>

      ![Criar novos detalhes do registro do Aplicativo Lógico](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="72426-160">Na barra de ferramentas de Designer de lógica do aplicativo hello, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="72426-160">On hello Logic App Designer toolbar, click **Save**.</span></span>

    ![Barra de ferramentas do Designer do Aplicativo Lógico Salvar](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="72426-162">Olá toostart lógica de aplicativo, clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="72426-162">toostart hello Logic App, click **Run**.</span></span>

    ![Barra de ferramentas do Designer do Aplicativo Lógico Salvar](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="72426-164">Agora, crie um registro de cliente em potencial no Dynamics 365 para Vendas e veja seu fluxo em ação!</span><span class="sxs-lookup"><span data-stu-id="72426-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="72426-165">Definir opções avançadas para uma etapa de aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="72426-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="72426-166">toospecify como toofilter dados em uma etapa de aplicativo lógica, clique em **Mostrar opções avançadas** essa etapa, em seguida, adicionar um filtro ou a ordem pela consulta.</span><span class="sxs-lookup"><span data-stu-id="72426-166">toospecify how toofilter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="72426-167">Por exemplo, você pode usar um filtro consulta tooget somente as contas ativas e Ordenar por nome de conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="72426-167">For example, you can use a filter query tooget only active accounts and order by hello account name.</span></span> <span data-ttu-id="72426-168">tooperform tarefas, insira a consulta de filtro OData Olá `statuscode eq 1`e selecione **nome da conta** na lista de conteúdo dinâmico Olá.</span><span class="sxs-lookup"><span data-stu-id="72426-168">tooperform this task, enter hello OData filter query `statuscode eq 1`, and select **Account Name** from hello dynamic content list.</span></span> <span data-ttu-id="72426-169">Mais informações: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) e [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span><span class="sxs-lookup"><span data-stu-id="72426-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Opções avançadas de aplicativo lógico](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="72426-171">Práticas recomendadas ao usar o opções avançadas</span><span class="sxs-lookup"><span data-stu-id="72426-171">Best practices when using advanced options</span></span>

<span data-ttu-id="72426-172">Quando você adiciona um campo de valor de tooa, você deve corresponder o tipo de campo de saudação se você digitar um valor ou selecione um valor na lista de conteúdo dinâmico Olá.</span><span class="sxs-lookup"><span data-stu-id="72426-172">When you add a value tooa field, you must match hello field type whether you type a value or select a value from hello dynamic content list.</span></span>

<span data-ttu-id="72426-173">Tipo de campo</span><span class="sxs-lookup"><span data-stu-id="72426-173">Field type</span></span>  |<span data-ttu-id="72426-174">Como toouse</span><span class="sxs-lookup"><span data-stu-id="72426-174">How toouse</span></span>  |<span data-ttu-id="72426-175">Onde toofind</span><span class="sxs-lookup"><span data-stu-id="72426-175">Where toofind</span></span>  |<span data-ttu-id="72426-176">Nome</span><span class="sxs-lookup"><span data-stu-id="72426-176">Name</span></span>  |<span data-ttu-id="72426-177">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="72426-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="72426-178">Campos de texto</span><span class="sxs-lookup"><span data-stu-id="72426-178">Text fields</span></span>|<span data-ttu-id="72426-179">Campos de texto exigem uma única linha de texto ou conteúdo dinâmico que seja um campo de tipo de texto.</span><span class="sxs-lookup"><span data-stu-id="72426-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="72426-180">Exemplos incluem campos de categoria e subcategoria hello.</span><span class="sxs-lookup"><span data-stu-id="72426-180">Examples include hello Category and Sub-Category fields.</span></span>|<span data-ttu-id="72426-181">Configurações > personalizações > Personalizar Olá System > entidades > tarefa > campos</span><span class="sxs-lookup"><span data-stu-id="72426-181">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="72426-182">categoria</span><span class="sxs-lookup"><span data-stu-id="72426-182">category</span></span> |<span data-ttu-id="72426-183">Linha única de texto</span><span class="sxs-lookup"><span data-stu-id="72426-183">Single Line of Text</span></span>        
<span data-ttu-id="72426-184">Campos de número inteiro</span><span class="sxs-lookup"><span data-stu-id="72426-184">Integer fields</span></span> | <span data-ttu-id="72426-185">Alguns campos exigem conteúdo inteiro ou dinâmico que seja um campo de tipo inteiro.</span><span class="sxs-lookup"><span data-stu-id="72426-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="72426-186">Exemplos incluem Porcentagem concluída e Duração.</span><span class="sxs-lookup"><span data-stu-id="72426-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="72426-187">Configurações > personalizações > Personalizar Olá System > entidades > tarefa > campos</span><span class="sxs-lookup"><span data-stu-id="72426-187">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="72426-188">percentcomplete</span><span class="sxs-lookup"><span data-stu-id="72426-188">percentcomplete</span></span> |<span data-ttu-id="72426-189">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="72426-189">Whole Number</span></span>         
<span data-ttu-id="72426-190">Campos de data</span><span class="sxs-lookup"><span data-stu-id="72426-190">Date fields</span></span> | <span data-ttu-id="72426-191">Alguns campos exigem a data inserida no formato dd/mm/aaaa ou conteúdo dinâmico que seja um campo do tipo data.</span><span class="sxs-lookup"><span data-stu-id="72426-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="72426-192">Exemplos incluem Criado em, Data de início, Início real, Último tempo de espera, Término real e Data de vencimento.</span><span class="sxs-lookup"><span data-stu-id="72426-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="72426-193">Configurações > personalizações > Personalizar Olá System > entidades > tarefa > campos</span><span class="sxs-lookup"><span data-stu-id="72426-193">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="72426-194">createdon</span><span class="sxs-lookup"><span data-stu-id="72426-194">createdon</span></span> |<span data-ttu-id="72426-195">Data e hora</span><span class="sxs-lookup"><span data-stu-id="72426-195">Date and Time</span></span>
<span data-ttu-id="72426-196">Campos que exigem um registro de ID e tipo de pesquisa</span><span class="sxs-lookup"><span data-stu-id="72426-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="72426-197">Alguns campos que fazem referência a outro registro de entidade requerem Olá ID do registro e o tipo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="72426-197">Some fields that reference another entity record require both hello record ID and hello lookup type.</span></span> |<span data-ttu-id="72426-198">Configurações > personalizações > Personalizar Olá System > entidades > conta > campos</span><span class="sxs-lookup"><span data-stu-id="72426-198">Settings > Customizations > Customize hello System > Entities > Account > Fields</span></span>  | <span data-ttu-id="72426-199">accountid</span><span class="sxs-lookup"><span data-stu-id="72426-199">accountid</span></span>  | <span data-ttu-id="72426-200">Chave primária</span><span class="sxs-lookup"><span data-stu-id="72426-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="72426-201">Mais exemplos de campos que exigem uma ID de registro e tipo de pesquisa</span><span class="sxs-lookup"><span data-stu-id="72426-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="72426-202">Expandindo a tabela anterior Olá, aqui estão mais exemplos de campos que não funcionam com os valores selecionados da lista de conteúdo dinâmico Olá.</span><span class="sxs-lookup"><span data-stu-id="72426-202">Expanding on hello previous table, here are more examples of fields that don't work with values selected from hello dynamic content list.</span></span> <span data-ttu-id="72426-203">Em vez disso, esses campos exigem ambos os uma pesquisa e a ID de tipo de registro inserido nos campos de saudação em PowerApps.</span><span class="sxs-lookup"><span data-stu-id="72426-203">Instead, these fields require both a record ID and lookup type entered into hello fields in PowerApps.</span></span>  
* <span data-ttu-id="72426-204">Proprietário e Tipo de proprietário.</span><span class="sxs-lookup"><span data-stu-id="72426-204">Owner and Owner Type.</span></span> <span data-ttu-id="72426-205">campo de proprietário Olá deve ser uma ID válida. registro de usuário ou da equipe</span><span class="sxs-lookup"><span data-stu-id="72426-205">hello Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="72426-206">Olá tipo proprietário deve ser **systemusers** ou **equipes**.</span><span class="sxs-lookup"><span data-stu-id="72426-206">hello Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="72426-207">Cliente e Tipo de cliente.</span><span class="sxs-lookup"><span data-stu-id="72426-207">Customer and Customer Type.</span></span> <span data-ttu-id="72426-208">campo de saudação do cliente deve ser uma conta válida ou entre em contato com a ID de registro.</span><span class="sxs-lookup"><span data-stu-id="72426-208">hello Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="72426-209">Olá tipo proprietário deve ser **contas** ou **contatos**.</span><span class="sxs-lookup"><span data-stu-id="72426-209">hello Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="72426-210">Referente e Referente ao tipo.</span><span class="sxs-lookup"><span data-stu-id="72426-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="72426-211">Olá sobre o campo deve ser uma ID de registro válida, como uma conta ou entre em contato com a ID de registro.</span><span class="sxs-lookup"><span data-stu-id="72426-211">hello Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="72426-212">Hello em relação ao tipo deve ser tipo de pesquisa Olá para registro Olá, como **contas** ou **contatos**.</span><span class="sxs-lookup"><span data-stu-id="72426-212">hello Regarding Type must be hello lookup type for hello record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="72426-213">Olá seguinte exemplo de ação de criação de tarefa adiciona um registro de conta que corresponde a ID do registro toohello adicioná-lo toohello sobre o campo de tarefa hello.</span><span class="sxs-lookup"><span data-stu-id="72426-213">hello following task creation action example adds an account record that corresponds toohello record ID adding it toohello regarding field of hello task.</span></span>

![Fluxo recordId e conta tipo](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="72426-215">Este exemplo também atribui Olá tarefa tooa usuário específico com base na ID de registro. do usuário hello</span><span class="sxs-lookup"><span data-stu-id="72426-215">This example also assigns hello task tooa specific user based on hello user's record ID.</span></span>

![Fluxo recordId e conta tipo](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="72426-217">toofind um registro da ID, consulte Olá seção a seguir: *localizar a ID de registro de saudação*</span><span class="sxs-lookup"><span data-stu-id="72426-217">toofind a record's ID, see hello following section: *Find hello record ID*</span></span>

## <a name="find-hello-record-id"></a><span data-ttu-id="72426-218">Localizar a ID de registro de saudação</span><span class="sxs-lookup"><span data-stu-id="72426-218">Find hello record ID</span></span>

1. <span data-ttu-id="72426-219">Abra um registro, como um registro de conta.</span><span class="sxs-lookup"><span data-stu-id="72426-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="72426-220">Na barra de ferramentas do hello ações, clique em **Pop-Out** ![pop-up registro](./media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="72426-220">On hello actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="72426-221">Como alternativa, na barra de ferramentas de ações de hello, toocopy Olá a URL completa em seu programa de email padrão, clique em **EMAIL um LINK**.</span><span class="sxs-lookup"><span data-stu-id="72426-221">Alternatively, on hello actions toolbar, toocopy hello full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="72426-222">ID do registro Olá é exibida entre Olá % 7b e %7 d codificação de caracteres da URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="72426-222">hello record ID is displayed in between hello %7b and %7d encoding characters of hello URL.</span></span>

   ![Fluxo recordId e conta tipo](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="72426-224">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="72426-224">Troubleshooting</span></span>
<span data-ttu-id="72426-225">tootroubleshoot uma etapa com falha em um aplicativo de lógica, exibir detalhes de status saudação do evento hello.</span><span class="sxs-lookup"><span data-stu-id="72426-225">tootroubleshoot a failed step in a logic app, view hello status details of hello event.</span></span>

1. <span data-ttu-id="72426-226">Em **Aplicativos Lógicos**, clique no seu aplicativo lógico e, em seguida, em **Visão geral**.</span><span class="sxs-lookup"><span data-stu-id="72426-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="72426-227">Olá área Resumo é mostrado e fornece o status de saudação executar para o aplicativo de lógica de saudação.</span><span class="sxs-lookup"><span data-stu-id="72426-227">hello Summary area is shown and provides hello run status for hello logic app.</span></span> 

   ![Status de execução do aplicativo lógico](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="72426-229">tooview obter mais informações sobre todas as execuções com falha, clique em Olá Falha ao evento.</span><span class="sxs-lookup"><span data-stu-id="72426-229">tooview more information about any failed runs, click hello failed event.</span></span> <span data-ttu-id="72426-230">tooexpand uma etapa com falha, clique nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="72426-230">tooexpand a failed step, click that step.</span></span>

   ![Expandir etapa com falha](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="72426-232">detalhes da etapa Olá aparecem e podem ajudar a solucionar Olá causa da falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="72426-232">hello step details appear and can help troubleshoot hello cause of hello failure.</span></span>

   ![Detalhes da etapa com falha](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="72426-234">Para obter mais informações sobre como solucionar problemas de aplicativos lógicos, consulte [Diagnosticando falhas do aplicativo lógico](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="72426-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="72426-235">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="72426-235">Connector-specific details</span></span>

<span data-ttu-id="72426-236">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/crm/).</span><span class="sxs-lookup"><span data-stu-id="72426-236">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="72426-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="72426-237">Next steps</span></span>
<span data-ttu-id="72426-238">Explorar Olá outros conectores disponíveis na lógica de aplicativos no nosso [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="72426-238">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
