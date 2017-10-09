---
title: "recuperação de aaaDisaster para conta de integração B2B - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Recuperação de desastre dos Aplicativos Lógicos B2B"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="24061-103">Recuperação de desastre de região cruzada dos Aplicativos Lógicos B2B</span><span class="sxs-lookup"><span data-stu-id="24061-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="24061-104">As cargas de trabalho B2B envolvem transações de dinheiro como pedidos e faturas.</span><span class="sxs-lookup"><span data-stu-id="24061-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="24061-105">Durante um evento de desastre, é essencial para uma saudação de toomeet business tooquickly recuperar que SLAs de nível de negócios acordados com seus parceiros.</span><span class="sxs-lookup"><span data-stu-id="24061-105">During a disaster event, it's critical for a business tooquickly recover toomeet hello business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="24061-106">Este artigo demonstra como planejar toobuild uma continuidade de negócios B2B cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="24061-106">This article demonstrates how toobuild a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="24061-107">Prontidão para recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="24061-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="24061-108">Failover de região toosecondary durante um evento de desastre</span><span class="sxs-lookup"><span data-stu-id="24061-108">Fail over toosecondary region during a disaster event</span></span> 
* <span data-ttu-id="24061-109">Voltar região tooprimary após um evento de desastre</span><span class="sxs-lookup"><span data-stu-id="24061-109">Fall back tooprimary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="24061-110">Prontidão para recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="24061-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="24061-111">Identificar uma região secundária e criar um [conta integration](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) na região secundária hello.</span><span class="sxs-lookup"><span data-stu-id="24061-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in hello secondary region.</span></span>

2. <span data-ttu-id="24061-112">Adicione parceiros, esquemas e os contratos para fluxos de mensagens de saudação necessário onde Olá status de execução precisa toobe replicada toosecondary região integração conta.</span><span class="sxs-lookup"><span data-stu-id="24061-112">Add partners, schemas, and agreements for hello required message flows where hello run status needs toobe replicated toosecondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="24061-113">Verifique se há consistência na convenção de nomenclatura do artefato de conta para a integração Olá entre regiões.</span><span class="sxs-lookup"><span data-stu-id="24061-113">Make sure there's consistency in hello integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="24061-114">Olá toopull status da execução da região primária do hello, crie um aplicativo de lógica na região secundária hello.</span><span class="sxs-lookup"><span data-stu-id="24061-114">toopull hello run status from hello primary region, create a logic app in hello secondary region.</span></span> 

   <span data-ttu-id="24061-115">Esse aplicativo lógico deve ter um *gatilho* e uma *ação*.</span><span class="sxs-lookup"><span data-stu-id="24061-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="24061-116">gatilho Olá deve se conectar a conta de integração de região tooprimary e ação Olá deve se conectar a conta de integração de região toosecondary.</span><span class="sxs-lookup"><span data-stu-id="24061-116">hello trigger should connect tooprimary region integration account, and hello action should connect toosecondary region integration account.</span></span> 
   <span data-ttu-id="24061-117">Com base no intervalo de tempo de saudação, gatilho Olá pesquisa a tabela de status de região primária executar hello e recebe novos registros de hello, se houver.</span><span class="sxs-lookup"><span data-stu-id="24061-117">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> <span data-ttu-id="24061-118">ação de saudação atualiza toosecondary conta de integração de região.</span><span class="sxs-lookup"><span data-stu-id="24061-118">hello action updates them toosecondary region integration account.</span></span> 
   <span data-ttu-id="24061-119">Isso ajuda a tooget em tempo de execução incremental da região de toosecondary região primária.</span><span class="sxs-lookup"><span data-stu-id="24061-119">This helps tooget incremental runtime status from primary region toosecondary region.</span></span>

4. <span data-ttu-id="24061-120">Continuidade de negócios em aplicativos de lógica de conta de integração é projetado toosupport com base em protocolos B2B - X12, AS2 e EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="24061-120">Business continuity in Logic Apps integration account is designed toosupport based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="24061-121">toofind obter etapas detalhadas, selecione Olá respectivos links.</span><span class="sxs-lookup"><span data-stu-id="24061-121">toofind detailed steps, select hello respective links.</span></span>

5. <span data-ttu-id="24061-122">Olá recomendação é muito toodeploy todos os recursos de região primária em uma região secundária.</span><span class="sxs-lookup"><span data-stu-id="24061-122">hello recommendation is toodeploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="24061-123">Recursos de região primária incluem o banco de dados SQL ou banco de dados do Azure Cosmos, barramento de serviço do Azure e Hubs de eventos do Azure usado para mensagens, gerenciamento de API do Azure e o recurso de aplicativos do Azure lógica de saudação do serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="24061-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and hello Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="24061-124">Estabelece uma conexão de uma região secundária tooa a região primária.</span><span class="sxs-lookup"><span data-stu-id="24061-124">Establish a connection from a primary region tooa secondary region.</span></span> <span data-ttu-id="24061-125">Olá toopull status da execução de uma região primária, crie um aplicativo de lógica em uma região secundária.</span><span class="sxs-lookup"><span data-stu-id="24061-125">toopull hello run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="24061-126">Olá lógica aplicativo deve ter um gatilho e uma ação.</span><span class="sxs-lookup"><span data-stu-id="24061-126">hello logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="24061-127">gatilho Olá deve se conectar a conta de integração do tooa região primária.</span><span class="sxs-lookup"><span data-stu-id="24061-127">hello trigger should connect tooa primary region integration account.</span></span> 
   <span data-ttu-id="24061-128">ação de saudação deve se conectar a conta de integração do tooa região secundária.</span><span class="sxs-lookup"><span data-stu-id="24061-128">hello action should connect tooa secondary region integration account.</span></span> 
   <span data-ttu-id="24061-129">Com base no intervalo de tempo de saudação, gatilho Olá pesquisa a tabela de status de região primária executar hello e recebe novos registros de hello, se houver.</span><span class="sxs-lookup"><span data-stu-id="24061-129">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> 
   <span data-ttu-id="24061-130">ação de saudação atualiza tooa conta de integração de região secundária.</span><span class="sxs-lookup"><span data-stu-id="24061-130">hello action updates them tooa secondary region integration account.</span></span> 
   <span data-ttu-id="24061-131">Esse processo ajuda em tempo de execução incremental tooget da região secundária do toohello Olá região primária.</span><span class="sxs-lookup"><span data-stu-id="24061-131">This process helps tooget incremental runtime status from hello primary region toohello secondary region.</span></span>

<span data-ttu-id="24061-132">Continuidade de negócios em uma conta de integração de aplicativos lógicos fornece suporte baseado em protocolos de B2B Olá X12, AS2 e EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="24061-132">Business continuity in a Logic Apps integration account provides support based on hello B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="24061-133">Para obter etapas detalhadas sobre como usar X12 e AS2, consulte [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) e [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) neste artigo.</span><span class="sxs-lookup"><span data-stu-id="24061-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a><span data-ttu-id="24061-134">Failover de região secundária tooa durante um evento de desastre</span><span class="sxs-lookup"><span data-stu-id="24061-134">Fail over tooa secondary region during a disaster event</span></span>

<span data-ttu-id="24061-135">Durante um evento de desastre, quando a região primária Olá não está disponível para continuidade de negócios, região secundária do tráfego direto toohello.</span><span class="sxs-lookup"><span data-stu-id="24061-135">During a disaster event, when hello primary region is not available for business continuity, direct traffic toohello secondary region.</span></span> <span data-ttu-id="24061-136">Região secundária ajuda a um toorecover negócios rapidamente funções toomeet Olá RPO/RTO acordado por seus parceiros.</span><span class="sxs-lookup"><span data-stu-id="24061-136">A secondary region helps a business toorecover functions quickly toomeet hello RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="24061-137">Ele também minimiza esforços toofail através da região de tooanother de uma região.</span><span class="sxs-lookup"><span data-stu-id="24061-137">It also minimizes efforts toofail over from one region tooanother region.</span></span> 

<span data-ttu-id="24061-138">Há uma latência esperada ao copiar os números de controle de uma região secundária tooa a região primária.</span><span class="sxs-lookup"><span data-stu-id="24061-138">There is an expected latency while copying control numbers from a primary region tooa secondary region.</span></span> <span data-ttu-id="24061-139">tooavoid enviar controle gerado duplicados números toopartners durante um evento de desastre, recomendação Olá é tooincrement números de controle de saudação em contratos de região secundária hello usando [cmdlets do PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="24061-139">tooavoid sending duplicate generated control numbers toopartners during a disaster event, hello recommendation is tooincrement hello control numbers in hello secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a><span data-ttu-id="24061-140">Retorno de evento de pós-desastres região primária tooa</span><span class="sxs-lookup"><span data-stu-id="24061-140">Fall back tooa primary region post-disaster event</span></span>

<span data-ttu-id="24061-141">toofall tooa back região primária quando ele estiver disponível, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="24061-141">toofall back tooa primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="24061-142">Pare de aceitar mensagens de parceiros na região secundária hello.</span><span class="sxs-lookup"><span data-stu-id="24061-142">Stop accepting messages from partners in hello secondary region.</span></span>  

2. <span data-ttu-id="24061-143">Incrementar números de controle de saudação gerado para todos os contratos de região primária hello usando [cmdlets do PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="24061-143">Increment hello generated control numbers for all hello primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="24061-144">Tráfego direto da região primária do toohello Olá região secundária.</span><span class="sxs-lookup"><span data-stu-id="24061-144">Direct traffic from hello secondary region toohello primary region.</span></span>

4. <span data-ttu-id="24061-145">Verificar aplicativo hello lógica criado na região secundária do Olá de obter status da execução da região primária Olá está habilitado.</span><span class="sxs-lookup"><span data-stu-id="24061-145">Check that hello logic app created in hello secondary region for pulling run status from hello primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="24061-146">X12</span><span class="sxs-lookup"><span data-stu-id="24061-146">X12</span></span> 

<span data-ttu-id="24061-147">A continuidade dos negócios para documentos EDI X12 tem como base os números de controle:</span><span class="sxs-lookup"><span data-stu-id="24061-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="24061-148">Você também pode usar o hello [X12 rápido iniciar modelo](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate lógica aplicativos.</span><span class="sxs-lookup"><span data-stu-id="24061-148">You can also use hello [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps.</span></span> <span data-ttu-id="24061-149">Criar contas de integração primários e secundários são modelo de saudação toouse pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="24061-149">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="24061-150">Olá modelo ajuda toocreate dois aplicativos de lógica, um para números de controle recebido e outro para os números de controle gerado.</span><span class="sxs-lookup"><span data-stu-id="24061-150">hello template helps toocreate two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="24061-151">Ações e respectivos gatilhos são criadas em aplicativos de lógica de hello, conectando Olá gatilho toohello integração principal contas e Olá ação toohello integração secundário.</span><span class="sxs-lookup"><span data-stu-id="24061-151">Respective triggers and actions are created in hello logic apps, connecting hello trigger toohello primary integration account and hello action toohello secondary integration account.</span></span>

<span data-ttu-id="24061-152">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="24061-152">**Prerequisites**</span></span>

<span data-ttu-id="24061-153">tooenable a recuperação de desastres para mensagens de entrada, selecione Olá duplicados Verifique as configurações em configurações de recebimento do contrato Olá X12.</span><span class="sxs-lookup"><span data-stu-id="24061-153">tooenable disaster recovery for inbound messages, select hello duplicate check settings in hello X12 agreement's Receive Settings.</span></span>

![Selecionar configurações de verificação de duplicadas](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="24061-155">Crie um [aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) em uma região secundária.</span><span class="sxs-lookup"><span data-stu-id="24061-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="24061-156">Pesquise **X12** e selecione **X12 – quando um número de controle é modificado**.</span><span class="sxs-lookup"><span data-stu-id="24061-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![Pesquise por X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="24061-158">gatilho Olá solicita tooestablish uma conta de integração de tooan de conexão.</span><span class="sxs-lookup"><span data-stu-id="24061-158">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="24061-159">Olá gatilho deve estar conectado a conta de integração do tooa região primária.</span><span class="sxs-lookup"><span data-stu-id="24061-159">hello trigger should be connected tooa primary region integration account.</span></span>

3. <span data-ttu-id="24061-160">Insira um nome de conexão, selecione seu *conta de integração da região primária* de saudação lista e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="24061-160">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>   

   ![Nome da conta de integração da região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="24061-162">Olá **sincronização do número de controle DateTime toostart** configuração é opcional.</span><span class="sxs-lookup"><span data-stu-id="24061-162">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="24061-163">Olá **frequência** pode ser definido muito**dia**, **hora**, **minuto**, ou **segundo** com um intervalo.</span><span class="sxs-lookup"><span data-stu-id="24061-163">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![DateTime e Frequency](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="24061-165">Selecione **Nova etapa** > **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="24061-165">Select **New step** > **Add an action**.</span></span>

   ![Nova Etapa, Adicionar uma ação](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="24061-167">Pesquise em **X12** e selecione **X12 – adicionar ou atualizar números de controle**.</span><span class="sxs-lookup"><span data-stu-id="24061-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![Adicionar ou atualizar números de controle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="24061-169">tooconnect tooa região secundária integração conta de ação, selecione **alterar conexão** > **adicionar nova conexão** para obter uma lista de contas de integração disponíveis hello.</span><span class="sxs-lookup"><span data-stu-id="24061-169">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="24061-170">Insira um nome de conexão, selecione seu *conta de integração de região secundária* de saudação lista e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="24061-170">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span> 

   ![Nome da conta de integração da região secundária](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="24061-172">Alternar tooraw entradas clicando no ícone de saudação no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="24061-172">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Opção tooraw entradas](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="24061-174">Selecione corpo do seletor de conteúdo dinâmico Olá e salve o aplicativo lógico de saudação.</span><span class="sxs-lookup"><span data-stu-id="24061-174">Select Body from hello dynamic content picker, and save hello logic app.</span></span>

   ![Campos de conteúdo dinâmico](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="24061-176">Com base no intervalo de tempo de saudação, gatilho Olá pesquisa a tabela de números de controle do hello região primária recebida e recebe novos registros de saudação.</span><span class="sxs-lookup"><span data-stu-id="24061-176">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span> 
   <span data-ttu-id="24061-177">ação Olá atualiza os registros de saudação na conta de integração do hello região secundária.</span><span class="sxs-lookup"><span data-stu-id="24061-177">hello action updates hello records in hello secondary region integration account.</span></span> 
   <span data-ttu-id="24061-178">Se não houver nenhuma atualização, status de gatilho Olá aparece como **ignorados**.</span><span class="sxs-lookup"><span data-stu-id="24061-178">If there are no updates, hello trigger status appears as **Skipped**.</span></span>   

   ![Tabela de números de controle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="24061-180">Com base no intervalo de tempo de saudação, em tempo de execução incremental Olá replica de uma região secundária tooa a região primária.</span><span class="sxs-lookup"><span data-stu-id="24061-180">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="24061-181">Durante um evento de desastre, quando Olá primário região não é disponível de tráfego direto toohello secundário para continuidade de negócios.</span><span class="sxs-lookup"><span data-stu-id="24061-181">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="24061-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="24061-182">EDIFACT</span></span> 

<span data-ttu-id="24061-183">A continuidade dos negócios para documentos EDI EDIFACT tem como base os números de controle.</span><span class="sxs-lookup"><span data-stu-id="24061-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="24061-184">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="24061-184">**Prerequisites**</span></span>

<span data-ttu-id="24061-185">tooenable a recuperação de desastres para mensagens de entrada, selecione Olá duplicados Verifique as configurações em configurações de recebimento do seu contrato EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="24061-185">tooenable disaster recovery for inbound messages, select hello duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![Selecionar configurações de verificação de duplicadas](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="24061-187">Crie um [aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) em uma região secundária.</span><span class="sxs-lookup"><span data-stu-id="24061-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="24061-188">Pesquise **EDIFACT** e selecione **EDIFACT – quando um número de controle é modificado**.</span><span class="sxs-lookup"><span data-stu-id="24061-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![Pesquisar por EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="24061-190">gatilho Olá solicita tooestablish uma conta de integração de tooan de conexão.</span><span class="sxs-lookup"><span data-stu-id="24061-190">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="24061-191">Olá gatilho deve estar conectado a conta de integração do tooa região primária.</span><span class="sxs-lookup"><span data-stu-id="24061-191">hello trigger should be connected tooa primary region integration account.</span></span> 

3. <span data-ttu-id="24061-192">Insira um nome de conexão, selecione seu *conta de integração da região primária* de saudação lista e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="24061-192">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>    

   ![Nome da conta de integração da região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="24061-194">Olá **sincronização do número de controle DateTime toostart** configuração é opcional.</span><span class="sxs-lookup"><span data-stu-id="24061-194">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="24061-195">Olá **frequência** pode ser definido muito**dia**, **hora**, **minuto**, ou **segundo** com um intervalo.</span><span class="sxs-lookup"><span data-stu-id="24061-195">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![DateTime e Frequency](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="24061-197">Selecione **Nova etapa** > **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="24061-197">Select **New step** > **Add an action**.</span></span>    

   ![Nova Etapa, Adicionar uma ação](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="24061-199">Pesquise em **EDIFACT** e selecione **EDIFACT – adicionar ou atualizar números de controle**.</span><span class="sxs-lookup"><span data-stu-id="24061-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![Adicionar ou atualizar números de controle](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="24061-201">tooconnect tooa região secundária integração conta de ação, selecione **alterar conexão** > **adicionar nova conexão** para obter uma lista de contas de integração disponíveis hello.</span><span class="sxs-lookup"><span data-stu-id="24061-201">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="24061-202">Insira um nome de conexão, selecione seu *conta de integração de região secundária* de saudação lista e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="24061-202">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nome da conta de integração da região secundária](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="24061-204">Alternar tooraw entradas clicando no ícone de saudação no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="24061-204">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Opção tooraw entradas](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="24061-206">Selecione corpo do seletor de conteúdo dinâmico Olá e salve o aplicativo lógico de saudação.</span><span class="sxs-lookup"><span data-stu-id="24061-206">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Campos de conteúdo dinâmico](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="24061-208">Com base no intervalo de tempo de saudação, gatilho Olá pesquisa a tabela de números de controle do hello região primária recebida e recebe novos registros de saudação.</span><span class="sxs-lookup"><span data-stu-id="24061-208">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span>
   <span data-ttu-id="24061-209">ação de Olá atualiza a conta de integração do hello registros toohello região secundária.</span><span class="sxs-lookup"><span data-stu-id="24061-209">hello action updates hello records toohello secondary region integration account.</span></span> 
   <span data-ttu-id="24061-210">Se não houver nenhuma atualização, status de gatilho Olá aparece como **ignorados**.</span><span class="sxs-lookup"><span data-stu-id="24061-210">If there are no updates, hello trigger status appears as **Skipped**.</span></span>

   ![Tabela de números de controle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="24061-212">Com base no intervalo de tempo de saudação, em tempo de execução incremental Olá replica de uma região secundária tooa a região primária.</span><span class="sxs-lookup"><span data-stu-id="24061-212">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="24061-213">Durante um evento de desastre, quando Olá primário região não é disponível de tráfego direto toohello secundário para continuidade de negócios.</span><span class="sxs-lookup"><span data-stu-id="24061-213">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="24061-214">AS2</span><span class="sxs-lookup"><span data-stu-id="24061-214">AS2</span></span> 

<span data-ttu-id="24061-215">Continuidade dos negócios para documentos que usam o protocolo do AS2 Olá baseia-se a ID de mensagem de saudação e valor MIC hello.</span><span class="sxs-lookup"><span data-stu-id="24061-215">Business continuity for documents that use hello AS2 protocol is based on hello message ID and hello MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="24061-216">Você também pode usar o hello [modelo de início rápido do AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate lógica aplicativos.</span><span class="sxs-lookup"><span data-stu-id="24061-216">You can also use hello [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps.</span></span> <span data-ttu-id="24061-217">Criar contas de integração primários e secundários são modelo de saudação toouse pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="24061-217">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="24061-218">modelo de saudação ajuda a criar um aplicativo de lógica que tem um gatilho e uma ação.</span><span class="sxs-lookup"><span data-stu-id="24061-218">hello template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="24061-219">Olá lógica aplicativo cria uma conexão de uma conta do gatilho tooa integração principal e conta de ação tooa integração secundário.</span><span class="sxs-lookup"><span data-stu-id="24061-219">hello logic app creates a connection from a trigger tooa primary integration account and an action tooa secondary integration account.</span></span>

1. <span data-ttu-id="24061-220">Criar um [aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) na região secundária hello.</span><span class="sxs-lookup"><span data-stu-id="24061-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in hello secondary region.</span></span>  

2. <span data-ttu-id="24061-221">Pesquise **AS2** e selecione **AS2 – quando um valor de MIC é criado**.</span><span class="sxs-lookup"><span data-stu-id="24061-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![Pesquise por AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="24061-223">Um gatilho solicitará que você tooestablish uma conta de integração de tooan de conexão.</span><span class="sxs-lookup"><span data-stu-id="24061-223">A trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="24061-224">Olá gatilho deve estar conectado a conta de integração do tooa região primária.</span><span class="sxs-lookup"><span data-stu-id="24061-224">hello trigger should be connected tooa primary region integration account.</span></span> 
   
3. <span data-ttu-id="24061-225">Insira um nome de conexão, selecione seu *conta de integração da região primária* de saudação lista e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="24061-225">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nome da conta de integração da região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="24061-227">Olá **sincronização de valor DateTime toostart MIC** configuração é opcional.</span><span class="sxs-lookup"><span data-stu-id="24061-227">hello **DateTime toostart MIC value sync** setting is optional.</span></span> <span data-ttu-id="24061-228">Olá **frequência** pode ser definido muito**dia**, **hora**, **minuto**, ou **segundo** com um intervalo.</span><span class="sxs-lookup"><span data-stu-id="24061-228">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![DateTime e Frequency](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="24061-230">Selecione **Nova etapa** > **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="24061-230">Select **New step** > **Add an action**.</span></span>  

   ![Nova Etapa, Adicionar uma ação](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="24061-232">Pesquise em **AS2** e selecione **AS2 – adicionar ou atualizar conteúdos de MIC**.</span><span class="sxs-lookup"><span data-stu-id="24061-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![Adição ou atualização do MIC](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="24061-234">Selecione tooconnect uma conta de integração secundário ação tooa, **alterar conexão** > **adicionar nova conexão** para obter uma lista de contas de integração disponíveis hello.</span><span class="sxs-lookup"><span data-stu-id="24061-234">tooconnect an action tooa secondary integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="24061-235">Insira um nome de conexão, selecione seu *conta de integração de região secundária* de saudação lista e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="24061-235">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nome da conta de integração da região secundária](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="24061-237">Alternar tooraw entradas clicando no ícone de saudação no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="24061-237">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Opção tooraw entradas](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="24061-239">Selecione corpo do seletor de conteúdo dinâmico Olá e salve o aplicativo lógico de saudação.</span><span class="sxs-lookup"><span data-stu-id="24061-239">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Conteúdo dinâmico](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="24061-241">Com base no intervalo de tempo de saudação, gatilho Olá pesquisa a tabela de região primária hello e recebe novos registros de saudação.</span><span class="sxs-lookup"><span data-stu-id="24061-241">Based on hello time interval, hello trigger polls hello primary region table and pulls hello new records.</span></span> <span data-ttu-id="24061-242">ação de saudação atualiza toohello conta de integração de região secundária.</span><span class="sxs-lookup"><span data-stu-id="24061-242">hello action updates them toohello secondary region integration account.</span></span> 
   <span data-ttu-id="24061-243">Se não houver nenhuma atualização, status de gatilho Olá aparece como **ignorados**.</span><span class="sxs-lookup"><span data-stu-id="24061-243">If there are no updates, hello trigger status appears as **Skipped**.</span></span>  

   ![Tabela da região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="24061-245">Com base no intervalo de tempo de saudação, em tempo de execução incremental Olá replica de região secundária do toohello Olá região primária.</span><span class="sxs-lookup"><span data-stu-id="24061-245">Based on hello time interval, hello incremental runtime status replicates from hello primary region toohello secondary region.</span></span> <span data-ttu-id="24061-246">Durante um evento de desastre, quando Olá primário região não é disponível de tráfego direto toohello secundário para continuidade de negócios.</span><span class="sxs-lookup"><span data-stu-id="24061-246">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="24061-247">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="24061-247">Next steps</span></span>

[<span data-ttu-id="24061-248">Monitorar mensagens do B2B</span><span class="sxs-lookup"><span data-stu-id="24061-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

