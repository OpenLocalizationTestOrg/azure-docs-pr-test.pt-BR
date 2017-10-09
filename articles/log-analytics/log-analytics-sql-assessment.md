---
title: aaaOptimize seu ambiente SQL Server com o Azure Log Analytics | Microsoft Docs
description: "Com análise de logs do Azure, você pode usar o hello solução tooassess Olá risco e a integridade de seus ambientes do SQL server em um intervalo regular de avaliação do SQL."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="289d8-103">Otimizar seu ambiente SQL Server com hello solução de avaliação do SQL na análise de Log</span><span class="sxs-lookup"><span data-stu-id="289d8-103">Optimize your SQL Server environment with hello SQL Assessment solution in Log Analytics</span></span>

![Símbolo da Avaliação do SQL](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="289d8-105">Você pode usar o hello avaliação SQL tooassess solução Olá risco e a integridade de seus ambientes de servidor em um intervalo regular.</span><span class="sxs-lookup"><span data-stu-id="289d8-105">You can use hello SQL Assessment solution tooassess hello risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="289d8-106">Este artigo o ajudará a instalar a solução Olá para que você pode executar ações corretivas para problemas potenciais.</span><span class="sxs-lookup"><span data-stu-id="289d8-106">This article will help you install hello solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="289d8-107">Essa solução fornece uma lista priorizada de infraestrutura de servidor implantado recomendações tooyour específico.</span><span class="sxs-lookup"><span data-stu-id="289d8-107">This solution provides a prioritized list of recommendations specific tooyour deployed server infrastructure.</span></span> <span data-ttu-id="289d8-108">Olá recomendações são categorizadas em seis foco áreas que ajudar você a entender Olá risco e tomar uma ação corretiva.</span><span class="sxs-lookup"><span data-stu-id="289d8-108">hello recommendations are categorized across six focus areas which help you quickly understand hello risk and take corrective action.</span></span>

<span data-ttu-id="289d8-109">recomendações Olá baseiam-se no conhecimento hello e experiência obtidas pelos engenheiros da Microsoft em milhares de visitas a clientes.</span><span class="sxs-lookup"><span data-stu-id="289d8-109">hello recommendations made are based on hello knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="289d8-110">Cada recomendação fornece diretrizes sobre por que uma questão pode ser relevante tooyou e como o tooimplement Olá alterações sugeridas.</span><span class="sxs-lookup"><span data-stu-id="289d8-110">Each recommendation provides guidance about why an issue might matter tooyou and how tooimplement hello suggested changes.</span></span>

<span data-ttu-id="289d8-111">Você pode escolher áreas de foco que são mais importante organização de tooyour e acompanham seu progresso em direção a um ambiente íntegro e livre de risco.</span><span class="sxs-lookup"><span data-stu-id="289d8-111">You can choose focus areas that are most important tooyour organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="289d8-112">Depois que você adicionou a solução hello e uma avaliação é concluído, resumo informações para as áreas de foco são mostradas na Olá **avaliação SQL** painel de infraestrutura de saudação em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="289d8-112">After you've added hello solution and an assessment is completed, summary information for focus areas is shown on hello **SQL Assessment** dashboard for hello infrastructure in your environment.</span></span> <span data-ttu-id="289d8-113">Olá seções a seguir descrevem como toouse Olá informações sobre Olá **avaliação SQL** painel, onde você pode exibir e executar as ações recomendadas para sua infraestrutura do SQL server.</span><span class="sxs-lookup"><span data-stu-id="289d8-113">hello following sections describe how toouse hello information on hello **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![imagem do bloco de Avaliação do SQL](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![imagem do painel de avaliação do SQL](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="289d8-116">Instalando e configurando a solução Olá</span><span class="sxs-lookup"><span data-stu-id="289d8-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="289d8-117">Avaliação do SQL funciona com todas as versões com suporte no momento do SQL Server para as edições Enterprise, Standard e Developer do hello.</span><span class="sxs-lookup"><span data-stu-id="289d8-117">SQL Assessment works with all currently supported versions of SQL Server for hello Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="289d8-118">Use Olá tooinstall informações a seguir e configurar a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="289d8-118">Use hello following information tooinstall and configure hello solution.</span></span>

* <span data-ttu-id="289d8-119">Agentes devem ser instalados em servidores que têm o SQL Server instalado.</span><span class="sxs-lookup"><span data-stu-id="289d8-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="289d8-120">Olá solução de avaliação do SQL requer uma versão com suporte do .NET Framework 4 instalado em cada computador que tenha um agente do OMS.</span><span class="sxs-lookup"><span data-stu-id="289d8-120">hello SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="289d8-121">Na solução de saudação do tooinstall de ordem, o usuário Olá deve ser um administrador ou colaborador toohello assinatura do Azure quando usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="289d8-121">In order tooinstall hello solution, hello user must be an administrator or contributor toohello Azure subscription when using hello Azure portal.</span></span> <span data-ttu-id="289d8-122">Além disso, o usuário de saudação deve ser um membro da saudação OMS espaço de trabalho Colaborador ou o administrador de função no portal do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="289d8-122">In addition, hello user must be a member of hello OMS workspace contributor or administrator role in hello OMS portal.</span></span>
* <span data-ttu-id="289d8-123">Ao usar o agente do Operations Manager Olá com a avaliação do SQL, você precisará toouse uma conta Run-As do Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="289d8-123">When using hello Operations Manager agent with SQL Assessment, you'll need toouse an Operations Manager Run-As account.</span></span> <span data-ttu-id="289d8-124">Consulte [Contas Executar como do Operations Manager para OMS](#operations-manager-run-as-accounts-for-oms) , abaixo, para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="289d8-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="289d8-125">agente MMA Olá não oferece suporte a contas do Operations Manager Run-As.</span><span class="sxs-lookup"><span data-stu-id="289d8-125">hello MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="289d8-126">Adicionar tooyour de solução de avaliação do SQL Olá espaço de trabalho do OMS usando Olá processo descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="289d8-126">Add hello SQL Assessment solution tooyour OMS workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="289d8-127">Não é necessária nenhuma configuração.</span><span class="sxs-lookup"><span data-stu-id="289d8-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="289d8-128">Depois que você adicionou a solução hello, arquivo AdvisorAssessment.exe de saudação é adicionado tooservers com agentes.</span><span class="sxs-lookup"><span data-stu-id="289d8-128">After you've added hello solution, hello AdvisorAssessment.exe file is added tooservers with agents.</span></span> <span data-ttu-id="289d8-129">Dados de configuração lidos e, em seguida, enviados toohello serviço do OMS na nuvem Olá para processamento.</span><span class="sxs-lookup"><span data-stu-id="289d8-129">Configuration data is read and then sent toohello OMS service in hello cloud for processing.</span></span> <span data-ttu-id="289d8-130">Lógica é aplicada toohello recebida dados e o serviço de nuvem Olá registra dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="289d8-130">Logic is applied toohello received data and hello cloud service records hello data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="289d8-131">Detalhes de coleta de dados da Avaliação de SQL</span><span class="sxs-lookup"><span data-stu-id="289d8-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="289d8-132">Avaliação do SQL coleta dados do WMI, dados de registro, dados de desempenho e resultados de exibição de gerenciamento dinâmico do SQL Server usando Olá agentes que você tiver habilitado.</span><span class="sxs-lookup"><span data-stu-id="289d8-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using hello agents that you have enabled.</span></span>

<span data-ttu-id="289d8-133">Olá tabela a seguir mostra os métodos de coleta de dados para os agentes se Operations Manager (SCOM) é necessária e como geralmente os dados são coletados por um agente.</span><span class="sxs-lookup"><span data-stu-id="289d8-133">hello following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="289d8-134">plataforma</span><span class="sxs-lookup"><span data-stu-id="289d8-134">platform</span></span> | <span data-ttu-id="289d8-135">Agente direto</span><span class="sxs-lookup"><span data-stu-id="289d8-135">Direct Agent</span></span> | <span data-ttu-id="289d8-136">Agente SCOM</span><span class="sxs-lookup"><span data-stu-id="289d8-136">SCOM agent</span></span> | <span data-ttu-id="289d8-137">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="289d8-137">Azure Storage</span></span> | <span data-ttu-id="289d8-138">SCOM necessário?</span><span class="sxs-lookup"><span data-stu-id="289d8-138">SCOM required?</span></span> | <span data-ttu-id="289d8-139">Os dados do agente SCOM enviados por meio do grupo de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="289d8-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="289d8-140">frequência de coleta</span><span class="sxs-lookup"><span data-stu-id="289d8-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="289d8-141">Windows</span><span class="sxs-lookup"><span data-stu-id="289d8-141">Windows</span></span> | <span data-ttu-id="289d8-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="289d8-142">&#8226;</span></span> | <span data-ttu-id="289d8-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="289d8-143">&#8226;</span></span> |  |  | <span data-ttu-id="289d8-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="289d8-144">&#8226;</span></span> |<span data-ttu-id="289d8-145">7 dias</span><span class="sxs-lookup"><span data-stu-id="289d8-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="289d8-146">Contas Executar como do Operations Manager para OMS</span><span class="sxs-lookup"><span data-stu-id="289d8-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="289d8-147">Análise de log no OMS usa hello agente do Operations Manager e toocollect do grupo de gerenciamento e envia dados toohello OMS service.</span><span class="sxs-lookup"><span data-stu-id="289d8-147">Log Analytics in OMS uses hello Operations Manager agent and management group toocollect and send data toohello OMS service.</span></span> <span data-ttu-id="289d8-148">OMS criado com base nos pacotes de gerenciamento para cargas de trabalho tooprovide serviços de valor agregado.</span><span class="sxs-lookup"><span data-stu-id="289d8-148">OMS builds upon management packs for workloads tooprovide value-add services.</span></span> <span data-ttu-id="289d8-149">Cada carga de trabalho requer pacotes de gerenciamento de toorun de privilégios de carga de trabalho específica em um contexto de segurança diferente, como uma conta de domínio.</span><span class="sxs-lookup"><span data-stu-id="289d8-149">Each workload requires workload-specific privileges toorun management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="289d8-150">É necessário tooprovide informações de credenciais Configurando uma conta executar como do Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="289d8-150">You need tooprovide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="289d8-151">Use Olá seguindo informações tooset saudação do Operations Manager conta executar como para avaliação do SQL.</span><span class="sxs-lookup"><span data-stu-id="289d8-151">Use hello following information tooset hello Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-hello-run-as-account-for-sql-assessment"></a><span data-ttu-id="289d8-152">Definir Olá a conta executar como para avaliação do SQL</span><span class="sxs-lookup"><span data-stu-id="289d8-152">Set hello Run As account for SQL assessment</span></span>
 <span data-ttu-id="289d8-153">Se você já estiver usando Olá pacote de gerenciamento do SQL Server, você deve usar essa conta executar como.</span><span class="sxs-lookup"><span data-stu-id="289d8-153">If you are already using hello SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a><span data-ttu-id="289d8-154">Olá tooconfigure conta executar como do SQL no console de operações de saudação</span><span class="sxs-lookup"><span data-stu-id="289d8-154">tooconfigure hello SQL Run As account in hello Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="289d8-155">Se você estiver usando hello OMS direto agente, em vez de agente do SCOM hello, pacote de gerenciamento Olá sempre é executado no contexto de segurança de saudação do hello conta Sistema Local.</span><span class="sxs-lookup"><span data-stu-id="289d8-155">If you are using hello OMS direct agent, rather than hello SCOM agent, hello management pack always runs in hello security context of hello Local System account.</span></span> <span data-ttu-id="289d8-156">Ignorar as etapas 1 a 5 abaixo e execute ou Olá exemplo de T-SQL ou o Powershell, especificando NT AUTHORITY\SYSTEM como nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="289d8-156">Skip steps 1-5 below, and run either hello T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as hello user name.</span></span>
>
>

1. <span data-ttu-id="289d8-157">No Operations Manager, abra o console de operações hello e, em seguida, clique em **administração**.</span><span class="sxs-lookup"><span data-stu-id="289d8-157">In Operations Manager, open hello Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="289d8-158">Em **Configuração Executar como**, clique em **Perfis** e abra **Perfil Executar como da Avaliação SQL do OMS**.</span><span class="sxs-lookup"><span data-stu-id="289d8-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="289d8-159">Em Olá **contas executar como** , clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="289d8-159">On hello **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="289d8-160">Selecione uma conta executar como do Windows que contenha Olá credenciais necessárias para o SQL Server, ou clique em **novo** toocreate um.</span><span class="sxs-lookup"><span data-stu-id="289d8-160">Select a Windows Run As account that contains hello credentials needed for SQL Server, or click **New** toocreate one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="289d8-161">Olá executar como tipo de conta deve ser Windows.</span><span class="sxs-lookup"><span data-stu-id="289d8-161">hello Run As account type must be Windows.</span></span> <span data-ttu-id="289d8-162">Olá conta executar como também deve fazer parte do grupo de administradores locais em todos os servidores Windows que hospedam instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="289d8-162">hello Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="289d8-163">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="289d8-163">Click **Save**.</span></span>
6. <span data-ttu-id="289d8-164">Modifique e, em seguida, execute Olá exemplo de T-SQL a seguir no tooRun necessário cada instância do SQL Server toogrant permissões mínimas tooperform conta como avaliação do SQL.</span><span class="sxs-lookup"><span data-stu-id="289d8-164">Modify and then execute hello following T-SQL sample on each SQL Server Instance toogrant minimum permissions required tooRun As Account tooperform SQL Assessment.</span></span> <span data-ttu-id="289d8-165">No entanto, você não precisa toodo isso se uma conta executar como já fizer parte da função de servidor sysadmin Olá em instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="289d8-165">However, you don’t need toodo this if a Run As Account is already part of hello sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="289d8-166">Olá tooconfigure conta executar como do SQL usando o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="289d8-166">tooconfigure hello SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="289d8-167">Abra uma janela do PowerShell e execute o script a seguir depois de atualizá-lo com suas informações de saudação:</span><span class="sxs-lookup"><span data-stu-id="289d8-167">Open a PowerShell window and run hello following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="289d8-168">Compreendendo como as recomendações são priorizadas</span><span class="sxs-lookup"><span data-stu-id="289d8-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="289d8-169">Cada recomendação feita recebe um valor de ponderação que identifica Olá a importância relativa da recomendação hello.</span><span class="sxs-lookup"><span data-stu-id="289d8-169">Every recommendation made is given a weighting value that identifies hello relative importance of hello recommendation.</span></span> <span data-ttu-id="289d8-170">Olá apenas dez recomendações mais importantes são mostradas.</span><span class="sxs-lookup"><span data-stu-id="289d8-170">Only hello ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="289d8-171">Como os pesos são calculados</span><span class="sxs-lookup"><span data-stu-id="289d8-171">How weights are calculated</span></span>
<span data-ttu-id="289d8-172">Os pesos são valores agregados com base em três fatores principais:</span><span class="sxs-lookup"><span data-stu-id="289d8-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="289d8-173">Olá *probabilidade* que um problema identificado cause problemas.</span><span class="sxs-lookup"><span data-stu-id="289d8-173">hello *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="289d8-174">Uma probabilidade mais alta é igual a pontuação geral maior de tooa de recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="289d8-174">A higher probability equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="289d8-175">Olá *impacto* do problema de saudação na sua organização se ela causar um problema.</span><span class="sxs-lookup"><span data-stu-id="289d8-175">hello *impact* of hello issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="289d8-176">Um impacto maior é igual a pontuação geral maior de tooa de recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="289d8-176">A higher impact equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="289d8-177">Olá *esforço* necessário tooimplement recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="289d8-177">hello *effort* required tooimplement hello recommendation.</span></span> <span data-ttu-id="289d8-178">Um esforço maior é igual a pontuação geral menor de tooa de recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="289d8-178">A higher effort equates tooa smaller overall score for hello recommendation.</span></span>

<span data-ttu-id="289d8-179">Olá peso de cada recomendação é expressa como um percentual da pontuação total da saudação disponíveis para cada área de foco.</span><span class="sxs-lookup"><span data-stu-id="289d8-179">hello weighting for each recommendation is expressed as a percentage of hello total score available for each focus area.</span></span> <span data-ttu-id="289d8-180">Por exemplo, se uma recomendação na hello segurança e área de foco de conformidade tiver uma pontuação de 5%, implementar essa recomendação aumentará a segurança e conformidade pontuação geral por 5%.</span><span class="sxs-lookup"><span data-stu-id="289d8-180">For example, if a recommendation in hello Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="289d8-181">Áreas de foco</span><span class="sxs-lookup"><span data-stu-id="289d8-181">Focus areas</span></span>
<span data-ttu-id="289d8-182">**Segurança e conformidade** - essa área de foco mostra recomendações para possíveis ameaças de segurança e violações, políticas corporativas, bem como os requisitos de conformidade técnica, legal e regulatória.</span><span class="sxs-lookup"><span data-stu-id="289d8-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="289d8-183">**Disponibilidade e continuidade dos negócios** - essa área de foco mostra as recomendações para a disponibilidade de serviço, resiliência de sua infraestrutura e proteção dos negócios.</span><span class="sxs-lookup"><span data-stu-id="289d8-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="289d8-184">**Desempenho e escalabilidade** -essa área de foco mostra recomendações toohelp da sua organização crescer de infraestrutura de TI, certifique-se de que seu ambiente de TI atende aos requisitos de desempenho atuais e é capaz de toorespond toochanging precisa de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="289d8-184">**Performance and Scalability** - This focus area shows recommendations toohelp your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able toorespond toochanging infrastructure needs.</span></span>

<span data-ttu-id="289d8-185">**Atualização, implantação e migração** – essa área de foco mostra recomendações toohelp atualizar, migrar e implantar a infraestrutura existente do SQL Server tooyour.</span><span class="sxs-lookup"><span data-stu-id="289d8-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations toohelp you upgrade, migrate, and deploy SQL Server tooyour existing infrastructure.</span></span>

<span data-ttu-id="289d8-186">**Operações e monitoramento** - essa área de foco mostra recomendações toohelp simplificar as operações de TI, implementar manutenção preventiva e maximizar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="289d8-186">**Operations and Monitoring** - This focus area shows recommendations toohelp streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="289d8-187">**Gerenciamento de alterações e configuração** -essa área de foco mostra recomendações toohelp proteger as operações diárias, verifique se as alterações não negativamente afetam sua infraestrutura, estabelecer procedimentos de controle de alterações e tootrack e auditoria configurações do sistema.</span><span class="sxs-lookup"><span data-stu-id="289d8-187">**Change and Configuration Management** - This focus area shows recommendations toohelp protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and tootrack and audit system configurations.</span></span>

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a><span data-ttu-id="289d8-188">Você deve visar tooscore 100% em cada área de foco?</span><span class="sxs-lookup"><span data-stu-id="289d8-188">Should you aim tooscore 100% in every focus area?</span></span>
<span data-ttu-id="289d8-189">Não necessariamente.</span><span class="sxs-lookup"><span data-stu-id="289d8-189">Not necessarily.</span></span> <span data-ttu-id="289d8-190">recomendações de saudação baseiam-se no conhecimento do hello e experiências obtidas pelos engenheiros da Microsoft em milhares de visitas a clientes.</span><span class="sxs-lookup"><span data-stu-id="289d8-190">hello recommendations are based on hello knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="289d8-191">No entanto, nenhuma infraestrutura de servidor é Olá mesmo e recomendações específicas podem ser mais ou menos relevante tooyou.</span><span class="sxs-lookup"><span data-stu-id="289d8-191">However, no two server infrastructures are hello same, and specific recommendations may be more or less relevant tooyou.</span></span> <span data-ttu-id="289d8-192">Por exemplo, algumas recomendações de segurança podem ser menos relevantes se as máquinas virtuais não são toohello exposto à Internet.</span><span class="sxs-lookup"><span data-stu-id="289d8-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed toohello Internet.</span></span> <span data-ttu-id="289d8-193">Algumas recomendações de disponibilidade podem ser menos relevantes para os serviços que fornecem relatórios e coleta de dados ad hoc de baixa prioridade.</span><span class="sxs-lookup"><span data-stu-id="289d8-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="289d8-194">Problemas de empresas maduras tooa importante podem ser menos importante inicialização de tooa.</span><span class="sxs-lookup"><span data-stu-id="289d8-194">Issues that are important tooa mature business may be less important tooa start-up.</span></span> <span data-ttu-id="289d8-195">Você pode desejar tooidentify quais áreas de foco são suas prioridades e depois examinar como suas pontuações mudam ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="289d8-195">You may want tooidentify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="289d8-196">Cada recomendação inclui diretrizes sobre sua importância.</span><span class="sxs-lookup"><span data-stu-id="289d8-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="289d8-197">Você deve usar essa orientação tooevaluate se implementar Olá recomendação é adequada para você, considerando a natureza Olá seu IT services e hello necessidades de negócios da sua organização.</span><span class="sxs-lookup"><span data-stu-id="289d8-197">You should use this guidance tooevaluate whether implementing hello recommendation is appropriate for you, given hello nature of your IT services and hello business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="289d8-198">Use as recomendações de área de foco de avaliação</span><span class="sxs-lookup"><span data-stu-id="289d8-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="289d8-199">Antes de usar uma solução de avaliação no OMS, você deve ter a solução Olá instalada.</span><span class="sxs-lookup"><span data-stu-id="289d8-199">Before you can use an assessment solution in OMS, you must have hello solution installed.</span></span> <span data-ttu-id="289d8-200">tooread mais informações sobre a instalação de soluções, consulte [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="289d8-200">tooread more about installing solutions, see [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="289d8-201">Após a instalação, você pode exibir o resumo de saudação das recomendações usando o bloco de avaliação SQL Olá na página de visão geral de saudação do OMS.</span><span class="sxs-lookup"><span data-stu-id="289d8-201">After it is installed, you can view hello summary of recommendations by using hello SQL Assessment tile on hello Overview page in OMS.</span></span>

<span data-ttu-id="289d8-202">Saudação de exibição resumida avaliações de conformidade para sua infraestrutura e detalhada das recomendações.</span><span class="sxs-lookup"><span data-stu-id="289d8-202">View hello summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="289d8-203">recomendações de tooview para um foco área e take corretivas</span><span class="sxs-lookup"><span data-stu-id="289d8-203">tooview recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="289d8-204">Em Olá **visão geral** , clique em Olá **avaliação SQL** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="289d8-204">On hello **Overview** page, click hello **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="289d8-205">Em Olá **avaliação SQL** página, examine as informações de resumo de saudação em uma saudação foco das folhas da área e, em seguida, clique em um tooview recomendações para a área de foco.</span><span class="sxs-lookup"><span data-stu-id="289d8-205">On hello **SQL Assessment** page, review hello summary information in one of hello focus area blades and then click one tooview recommendations for that focus area.</span></span>
3. <span data-ttu-id="289d8-206">Em qualquer uma das páginas da área de foco hello, você pode exibir as recomendações de saudação priorizada para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="289d8-206">On any of hello focus area pages, you can view hello prioritized recommendations made for your environment.</span></span> <span data-ttu-id="289d8-207">Clique em uma recomendação em **objetos afetados** tooview detalhes sobre por que Olá recomendação foi feita.</span><span class="sxs-lookup"><span data-stu-id="289d8-207">Click a recommendation under **Affected Objects** tooview details about why hello recommendation is made.</span></span>  
    <span data-ttu-id="289d8-208">![imagem de recomendações da Avaliação do SQL](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="289d8-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="289d8-209">É possível executar as ações corretivas sugeridas em **Ações Sugeridas**.</span><span class="sxs-lookup"><span data-stu-id="289d8-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="289d8-210">Quando o item de saudação tiver sido resolvido, avaliações posteriores gravarão que recomendado ações foram executadas e sua pontuação de conformidade aumentará.</span><span class="sxs-lookup"><span data-stu-id="289d8-210">When hello item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="289d8-211">Os itens corrigido aparecem como **Objetos Passados**.</span><span class="sxs-lookup"><span data-stu-id="289d8-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="289d8-212">Ignorar as recomendações</span><span class="sxs-lookup"><span data-stu-id="289d8-212">Ignore recommendations</span></span>
<span data-ttu-id="289d8-213">Se tiver recomendações que você deseja tooignore, você pode criar um arquivo de texto que o OMS usará tooprevent as recomendações apareçam nos resultados da avaliação.</span><span class="sxs-lookup"><span data-stu-id="289d8-213">If you have recommendations that you want tooignore, you can create a text file that OMS will use tooprevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a><span data-ttu-id="289d8-214">recomendações de tooidentify que você irá ignorar</span><span class="sxs-lookup"><span data-stu-id="289d8-214">tooidentify recommendations that you will ignore</span></span>
1. <span data-ttu-id="289d8-215">Entre no espaço de trabalho tooyour e abra a pesquisa de Log.</span><span class="sxs-lookup"><span data-stu-id="289d8-215">Sign in tooyour workspace and open Log Search.</span></span> <span data-ttu-id="289d8-216">Use Olá consulta toolist recomendações que falharam para computadores em seu ambiente a seguir.</span><span class="sxs-lookup"><span data-stu-id="289d8-216">Use hello following query toolist recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="289d8-217">Aqui está uma consulta de pesquisa de Log de saudação de captura de tela mostrando: ![falha recomendações](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="289d8-217">Here's a screen shot showing hello Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="289d8-218">Escolha as recomendações que você deseja tooignore.</span><span class="sxs-lookup"><span data-stu-id="289d8-218">Choose recommendations that you want tooignore.</span></span> <span data-ttu-id="289d8-219">Você usará os valores hello para RecommendationId no próximo procedimento de saudação.</span><span class="sxs-lookup"><span data-stu-id="289d8-219">You’ll use hello values for RecommendationId in hello next procedure.</span></span>

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="289d8-220">toocreate e usar um arquivo de texto IgnoreRecommendations.txt</span><span class="sxs-lookup"><span data-stu-id="289d8-220">toocreate and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="289d8-221">Crie um arquivo chamado IgnoreRecommendations.txt.</span><span class="sxs-lookup"><span data-stu-id="289d8-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="289d8-222">Cole ou digite cada RecommendationId de cada recomendação que você deseja tooignore OMS em uma linha separada e salve e feche o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="289d8-222">Paste or type each RecommendationId for each recommendation that you want OMS tooignore on a separate line and then save and close hello file.</span></span>
3. <span data-ttu-id="289d8-223">Arquivo hello PUT na Olá pasta a seguir em cada computador onde você deseja que as recomendações de tooignore do OMS.</span><span class="sxs-lookup"><span data-stu-id="289d8-223">Put hello file in hello following folder on each computer where you want OMS tooignore recommendations.</span></span>
   * <span data-ttu-id="289d8-224">Em computadores com hello Microsoft Monitoring Agent (conectado diretamente ou por meio do Operations Manager) - *SystemDrive*: \Program Files\Microsoft Monitoring Agent\Agent</span><span class="sxs-lookup"><span data-stu-id="289d8-224">On computers with hello Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="289d8-225">No servidor de gerenciamento do Operations Manager Olá - *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="289d8-225">On hello Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="tooverify-that-recommendations-are-ignored"></a><span data-ttu-id="289d8-226">tooverify que as recomendações são ignoradas</span><span class="sxs-lookup"><span data-stu-id="289d8-226">tooverify that recommendations are ignored</span></span>
1. <span data-ttu-id="289d8-227">Depois de ser executado Olá próxima avaliação agendada, por padrão a cada 7 dias, Olá especificado recomendações são marcadas como ignoradas e não serão exibidos no painel de avaliação de saudação.</span><span class="sxs-lookup"><span data-stu-id="289d8-227">After hello next scheduled assessment runs, by default every 7 days, hello specified recommendations are marked Ignored and will not appear on hello assessment dashboard.</span></span>
2. <span data-ttu-id="289d8-228">Você pode usar o hello toolist de consultas de pesquisa de Log a seguir todas as recomendações de saudação ignorada.</span><span class="sxs-lookup"><span data-stu-id="289d8-228">You can use hello following Log Search queries toolist all hello ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="289d8-229">Se você decidir posteriormente que deseja toosee ignorado recomendações, remova os arquivos IgnoreRecommendations.txt ou remova as RecommendationIDs deles.</span><span class="sxs-lookup"><span data-stu-id="289d8-229">If you decide later that you want toosee ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="289d8-230">Perguntas frequentes sobre soluções de Avaliação de SQL</span><span class="sxs-lookup"><span data-stu-id="289d8-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="289d8-231">*Com que frequência uma avaliação é executada?*</span><span class="sxs-lookup"><span data-stu-id="289d8-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="289d8-232">Olá avaliação é executada a cada 7 dias.</span><span class="sxs-lookup"><span data-stu-id="289d8-232">hello assessment runs every 7 days.</span></span>

<span data-ttu-id="289d8-233">*Há um tooconfigure de maneira com que frequência Olá avaliação é executada?*</span><span class="sxs-lookup"><span data-stu-id="289d8-233">*Is there a way tooconfigure how often hello assessment runs?*</span></span>

* <span data-ttu-id="289d8-234">Não no momento.</span><span class="sxs-lookup"><span data-stu-id="289d8-234">Not at this time.</span></span>

<span data-ttu-id="289d8-235">*Se outro servidor for descoberto após ter adicionado Olá solução de avaliação do SQL, ele será avaliado?*</span><span class="sxs-lookup"><span data-stu-id="289d8-235">*If another server is discovered after I’ve added hello SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="289d8-236">Sim, assim que for descoberto, ele é avaliado a partir de então a cada sete dias.</span><span class="sxs-lookup"><span data-stu-id="289d8-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="289d8-237">*Se um servidor for encerrado, quando ele será removido da avaliação de Olá?*</span><span class="sxs-lookup"><span data-stu-id="289d8-237">*If a server is decommissioned, when will it be removed from hello assessment?*</span></span>

* <span data-ttu-id="289d8-238">Se um servidor não enviar dados por três semanas, ele será removido.</span><span class="sxs-lookup"><span data-stu-id="289d8-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="289d8-239">*O que é o nome de saudação do processo Olá Olá a coleta de dados?*</span><span class="sxs-lookup"><span data-stu-id="289d8-239">*What is hello name of hello process that does hello data collection?*</span></span>

* <span data-ttu-id="289d8-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="289d8-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="289d8-241">*Quanto tempo leva para toobe dados coletado?*</span><span class="sxs-lookup"><span data-stu-id="289d8-241">*How long does it take for data toobe collected?*</span></span>

* <span data-ttu-id="289d8-242">coleta de dados reais de saudação no servidor de saudação leva aproximadamente 1 hora.</span><span class="sxs-lookup"><span data-stu-id="289d8-242">hello actual data collection on hello server takes about 1 hour.</span></span> <span data-ttu-id="289d8-243">Pode levar mais tempo em servidores que têm um grande número de instâncias ou bancos de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="289d8-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="289d8-244">*Que tipo de dados é coletado?*</span><span class="sxs-lookup"><span data-stu-id="289d8-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="289d8-245">Olá seguintes tipos de dados é coletado:</span><span class="sxs-lookup"><span data-stu-id="289d8-245">hello following types of data are collected:</span></span>
  * <span data-ttu-id="289d8-246">WMI</span><span class="sxs-lookup"><span data-stu-id="289d8-246">WMI</span></span>
  * <span data-ttu-id="289d8-247">Registro</span><span class="sxs-lookup"><span data-stu-id="289d8-247">Registry</span></span>
  * <span data-ttu-id="289d8-248">Contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="289d8-248">Performance counters</span></span>
  * <span data-ttu-id="289d8-249">Exibições de gerenciamento dinâmico SQL (DMV).</span><span class="sxs-lookup"><span data-stu-id="289d8-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="289d8-250">*Há uma maneira tooconfigure quando os dados são coletados?*</span><span class="sxs-lookup"><span data-stu-id="289d8-250">*Is there a way tooconfigure when data is collected?*</span></span>

* <span data-ttu-id="289d8-251">Não no momento.</span><span class="sxs-lookup"><span data-stu-id="289d8-251">Not at this time.</span></span>

<span data-ttu-id="289d8-252">*Por que tenho tooconfigure uma conta executar como?*</span><span class="sxs-lookup"><span data-stu-id="289d8-252">*Why do I have tooconfigure a Run As Account?*</span></span>

* <span data-ttu-id="289d8-253">Para o SQL Server, um pequeno número de consultas SQL é executado.</span><span class="sxs-lookup"><span data-stu-id="289d8-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="289d8-254">Para que eles toorun, uma conta executar como com tooSQL de permissões Exibir estado do servidor deve ser usado.</span><span class="sxs-lookup"><span data-stu-id="289d8-254">In order for them toorun, a Run As Account with VIEW SERVER STATE permissions tooSQL must be used.</span></span>  <span data-ttu-id="289d8-255">Além disso, em ordem tooquery WMI, as credenciais de administrador local são necessárias.</span><span class="sxs-lookup"><span data-stu-id="289d8-255">In addition, in order tooquery WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="289d8-256">*Por que apenas Olá 10 principais recomendações são exibidas?*</span><span class="sxs-lookup"><span data-stu-id="289d8-256">*Why display only hello top 10 recommendations?*</span></span>

* <span data-ttu-id="289d8-257">Em vez de apresentar uma lista exaustiva de tarefas, é recomendável que você se concentre em tratar as recomendações de saudação priorizada primeiro.</span><span class="sxs-lookup"><span data-stu-id="289d8-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing hello prioritized recommendations first.</span></span> <span data-ttu-id="289d8-258">Depois de tratar dessas recomendações, recomendações adicionais serão disponibilizadas.</span><span class="sxs-lookup"><span data-stu-id="289d8-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="289d8-259">Se você preferir a lista detalhada de saudação toosee, você pode exibir todas as recomendações usando a pesquisa de log OMS hello.</span><span class="sxs-lookup"><span data-stu-id="289d8-259">If you prefer toosee hello detailed list, you can view all recommendations using hello OMS log search.</span></span>

<span data-ttu-id="289d8-260">*Há uma maneira tooignore uma recomendação?*</span><span class="sxs-lookup"><span data-stu-id="289d8-260">*Is there a way tooignore a recommendation?*</span></span>

* <span data-ttu-id="289d8-261">Sim, confira a seção [Ignorar recomendações](#ignore-recommendations) acima.</span><span class="sxs-lookup"><span data-stu-id="289d8-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="289d8-262">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="289d8-262">Next steps</span></span>
* <span data-ttu-id="289d8-263">[Pesquisar logs](log-analytics-log-searches.md) tooview obter dados de avaliação do SQL e as recomendações.</span><span class="sxs-lookup"><span data-stu-id="289d8-263">[Search logs](log-analytics-log-searches.md) tooview detailed SQL Assessment data and recommendations.</span></span>
