---
title: Otimizar seu ambiente do SQL Server com o Azure Log Analytics | Microsoft Docs
description: "Com o Azure Log Analytics, você pode usar a solução de Avaliação de SQL para avaliar o risco e a integridade de seus ambientes de servidor SQL em intervalos regulares."
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
ms.openlocfilehash: d2aed3315fe60ace46dfb4176dc13aa417257b0c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="optimize-your-sql-server-environment-with-the-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="2331b-103">Otimizar seu ambiente do SQL Server com a solução de Avaliação de SQL da Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2331b-103">Optimize your SQL Server environment with the SQL Assessment solution in Log Analytics</span></span>

![Símbolo da Avaliação do SQL](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="2331b-105">Você pode usar a solução de Avaliação de SQL para avaliar o risco e a integridade de seus ambientes de servidor em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="2331b-105">You can use the SQL Assessment solution to assess the risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="2331b-106">Este artigo ajudará você a instalar a solução para que você possa tomar ações corretivas para potenciais problemas.</span><span class="sxs-lookup"><span data-stu-id="2331b-106">This article will help you install the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="2331b-107">Esta solução fornece uma lista priorizada de recomendações específicas para sua infraestrutura de servidor implantado.</span><span class="sxs-lookup"><span data-stu-id="2331b-107">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="2331b-108">As recomendações são categorizadas em seis áreas de foco que ajudarão a entender o risco e tomar uma ação corretiva.</span><span class="sxs-lookup"><span data-stu-id="2331b-108">The recommendations are categorized across six focus areas which help you quickly understand the risk and take corrective action.</span></span>

<span data-ttu-id="2331b-109">As recomendações baseiam-se no conhecimento e na experiências obtidas pelos engenheiros da Microsoft em milhares de visitas a clientes.</span><span class="sxs-lookup"><span data-stu-id="2331b-109">The recommendations made are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="2331b-110">Cada recomendação fornece diretrizes sobre por que um problema pode ser relevante para você e como implementar as alterações sugeridas.</span><span class="sxs-lookup"><span data-stu-id="2331b-110">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="2331b-111">Você pode escolher as áreas de foco que são mais importantes para sua organização e acompanhar seu progresso no sentido de executar um ambiente íntegro e sem riscos.</span><span class="sxs-lookup"><span data-stu-id="2331b-111">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="2331b-112">Após terminar de adicionar a solução e a avaliação ser concluída, as informações resumidas para áreas de foco são mostradas no painel **Avaliação de SQL** para a infraestrutura no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="2331b-112">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **SQL Assessment** dashboard for the infrastructure in your environment.</span></span> <span data-ttu-id="2331b-113">As seções a seguir descrevem como usar as informações no painel **Avaliação de SQL** , em que é possível exibir e executar as ações recomendadas para sua infraestrutura de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2331b-113">The following sections describe how to use the information on the **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![imagem do bloco de Avaliação do SQL](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![imagem do painel de avaliação do SQL](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="2331b-116">Instalando e configurando a solução</span><span class="sxs-lookup"><span data-stu-id="2331b-116">Installing and configuring the solution</span></span>
<span data-ttu-id="2331b-117">A Avaliação de SQL trabalha com todas as versões do SQL Server com suporte atualmente para as edições Standard, Developer e Enterprise.</span><span class="sxs-lookup"><span data-stu-id="2331b-117">SQL Assessment works with all currently supported versions of SQL Server for the Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="2331b-118">Use as informações a seguir para instalar e configurar a solução.</span><span class="sxs-lookup"><span data-stu-id="2331b-118">Use the following information to install and configure the solution.</span></span>

* <span data-ttu-id="2331b-119">Agentes devem ser instalados em servidores que têm o SQL Server instalado.</span><span class="sxs-lookup"><span data-stu-id="2331b-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="2331b-120">A solução de Avaliação do SQL requer uma versão do .NET Framework 4 com suporte instalada em cada computador que tem um agente do OMS.</span><span class="sxs-lookup"><span data-stu-id="2331b-120">The SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="2331b-121">Para instalar a solução, o usuário deve ser um administrador ou colaborador da assinatura do Azure ao usar o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2331b-121">In order to install the solution, the user must be an administrator or contributor to the Azure subscription when using the Azure portal.</span></span> <span data-ttu-id="2331b-122">Além disso, o usuário deve ser membro da função de colaborador ou administrador do espaço de trabalho OMS no portal do OMS.</span><span class="sxs-lookup"><span data-stu-id="2331b-122">In addition, the user must be a member of the OMS workspace contributor or administrator role in the OMS portal.</span></span>
* <span data-ttu-id="2331b-123">Ao usar o agente do Operations Manager com a Avaliação do SQL, você precisará usar uma conta Executar como do Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="2331b-123">When using the Operations Manager agent with SQL Assessment, you'll need to use an Operations Manager Run-As account.</span></span> <span data-ttu-id="2331b-124">Consulte [Contas Executar como do Operations Manager para OMS](#operations-manager-run-as-accounts-for-oms) , abaixo, para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="2331b-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="2331b-125">O agente MMA não dá suporte a contas Executar como do Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="2331b-125">The MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="2331b-126">Adicionar a solução da Avaliação do SQL ao seu espaço de trabalho do OMS usando o processo descrito em [Adicionar soluções do Log Analytics da Galeria de Soluções](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="2331b-126">Add the SQL Assessment solution to your OMS workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="2331b-127">Não é necessária nenhuma configuração.</span><span class="sxs-lookup"><span data-stu-id="2331b-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="2331b-128">Depois de adicionar a solução, o arquivo AdvisorAssessment.exe é adicionado aos servidores com agentes.</span><span class="sxs-lookup"><span data-stu-id="2331b-128">After you've added the solution, the AdvisorAssessment.exe file is added to servers with agents.</span></span> <span data-ttu-id="2331b-129">Os dados de configuração são lidos e, em seguida, enviados para o serviço OMS na nuvem para processamento.</span><span class="sxs-lookup"><span data-stu-id="2331b-129">Configuration data is read and then sent to the OMS service in the cloud for processing.</span></span> <span data-ttu-id="2331b-130">A lógica é aplicada aos dados recebidos e o serviço de nuvem registra os dados.</span><span class="sxs-lookup"><span data-stu-id="2331b-130">Logic is applied to the received data and the cloud service records the data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="2331b-131">Detalhes de coleta de dados da Avaliação de SQL</span><span class="sxs-lookup"><span data-stu-id="2331b-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="2331b-132">A Avaliação do SQL coletará dados WMI, dados de registro, dados de desempenho e resultados de exibição do gerenciamento dinâmico do SQL Server que estiverem usand os agentes que você tiver habilitado.</span><span class="sxs-lookup"><span data-stu-id="2331b-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using the agents that you have enabled.</span></span>

<span data-ttu-id="2331b-133">A tabela a seguir mostra os métodos de coleta de dados dos agentes, se o SCOM (Operations Manager) é necessário e com que frequência os dados são coletados por um agente.</span><span class="sxs-lookup"><span data-stu-id="2331b-133">The following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="2331b-134">plataforma</span><span class="sxs-lookup"><span data-stu-id="2331b-134">platform</span></span> | <span data-ttu-id="2331b-135">Agente direto</span><span class="sxs-lookup"><span data-stu-id="2331b-135">Direct Agent</span></span> | <span data-ttu-id="2331b-136">Agente SCOM</span><span class="sxs-lookup"><span data-stu-id="2331b-136">SCOM agent</span></span> | <span data-ttu-id="2331b-137">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2331b-137">Azure Storage</span></span> | <span data-ttu-id="2331b-138">SCOM necessário?</span><span class="sxs-lookup"><span data-stu-id="2331b-138">SCOM required?</span></span> | <span data-ttu-id="2331b-139">Os dados do agente SCOM enviados por meio do grupo de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="2331b-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="2331b-140">frequência de coleta</span><span class="sxs-lookup"><span data-stu-id="2331b-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="2331b-141">Windows</span><span class="sxs-lookup"><span data-stu-id="2331b-141">Windows</span></span> | <span data-ttu-id="2331b-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="2331b-142">&#8226;</span></span> | <span data-ttu-id="2331b-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="2331b-143">&#8226;</span></span> |  |  | <span data-ttu-id="2331b-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="2331b-144">&#8226;</span></span> |<span data-ttu-id="2331b-145">7 dias</span><span class="sxs-lookup"><span data-stu-id="2331b-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="2331b-146">Contas Executar como do Operations Manager para OMS</span><span class="sxs-lookup"><span data-stu-id="2331b-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="2331b-147">O Log Analytics no OMS usa o grupo de gerenciamento e o agente do Operations Manager para coletar e enviar dados para o serviço do OMS.</span><span class="sxs-lookup"><span data-stu-id="2331b-147">Log Analytics in OMS uses the Operations Manager agent and management group to collect and send data to the OMS service.</span></span> <span data-ttu-id="2331b-148">O OMS é criado com base nos pacotes de gerenciamento para cargas de trabalho para fornecer serviços com valor agregado.</span><span class="sxs-lookup"><span data-stu-id="2331b-148">OMS builds upon management packs for workloads to provide value-add services.</span></span> <span data-ttu-id="2331b-149">Cada carga de trabalho exige privilégios específicos da carga de trabalho para executar pacotes de gerenciamento em um contexto de segurança diferente, como uma conta de domínio.</span><span class="sxs-lookup"><span data-stu-id="2331b-149">Each workload requires workload-specific privileges to run management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="2331b-150">Você precisa fornecer informações de credenciais configurando uma conta Executar como do Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="2331b-150">You need to provide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="2331b-151">Use as informações a seguir para definir a conta Executar como do Operations Manager para Avaliação de SQL.</span><span class="sxs-lookup"><span data-stu-id="2331b-151">Use the following information to set the Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-the-run-as-account-for-sql-assessment"></a><span data-ttu-id="2331b-152">Definir a conta Executar como para avaliação do SQL</span><span class="sxs-lookup"><span data-stu-id="2331b-152">Set the Run As account for SQL assessment</span></span>
 <span data-ttu-id="2331b-153">Se você já estiver usando o pacote de gerenciamento do SQL Server, deve usar essa conta Executar como.</span><span class="sxs-lookup"><span data-stu-id="2331b-153">If you are already using the SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="to-configure-the-sql-run-as-account-in-the-operations-console"></a><span data-ttu-id="2331b-154">Para configurar a conta Executar como do SQL no console Operações</span><span class="sxs-lookup"><span data-stu-id="2331b-154">To configure the SQL Run As account in the Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="2331b-155">Se você estiver usando o agente direto do OMS em vez do agente do SCOM, o pacote de gerenciamento será sempre executado no contexto de segurança da conta de Sistema Local.</span><span class="sxs-lookup"><span data-stu-id="2331b-155">If you are using the OMS direct agent, rather than the SCOM agent, the management pack always runs in the security context of the Local System account.</span></span> <span data-ttu-id="2331b-156">Ignore as etapas 1 a 5 abaixo e execute o exemplo do T-SQL ou Powershell, especificando NT AUTHORITY\SYSTEM como o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="2331b-156">Skip steps 1-5 below, and run either the T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as the user name.</span></span>
>
>

1. <span data-ttu-id="2331b-157">No Operations Manager, abra o console Operações e clique em **Administração**.</span><span class="sxs-lookup"><span data-stu-id="2331b-157">In Operations Manager, open the Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="2331b-158">Em **Configuração Executar como**, clique em **Perfis** e abra **Perfil Executar como da Avaliação SQL do OMS**.</span><span class="sxs-lookup"><span data-stu-id="2331b-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="2331b-159">Na página **Contas Executar como**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2331b-159">On the **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="2331b-160">Selecione uma conta Executar como do Windows que contenha as credenciais necessárias para o SQL Server ou clique em **Nova** para criar uma.</span><span class="sxs-lookup"><span data-stu-id="2331b-160">Select a Windows Run As account that contains the credentials needed for SQL Server, or click **New** to create one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2331b-161">O tipo de conta Executar Como deve ser Windows.</span><span class="sxs-lookup"><span data-stu-id="2331b-161">The Run As account type must be Windows.</span></span> <span data-ttu-id="2331b-162">A conta Executar como também deve fazer parte do grupo de administradores locais em todos os servidores Windows que hospedam instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2331b-162">The Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="2331b-163">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2331b-163">Click **Save**.</span></span>
6. <span data-ttu-id="2331b-164">Modifique e, em seguida, execute o seguinte exemplo de T-SQL em cada instância do SQL Server para conceder as permissões mínimas necessárias para a conta Executar como para realizar uma avaliação de SQL.</span><span class="sxs-lookup"><span data-stu-id="2331b-164">Modify and then execute the following T-SQL sample on each SQL Server Instance to grant minimum permissions required to Run As Account to perform SQL Assessment.</span></span> <span data-ttu-id="2331b-165">No entanto, você não precisa fazer isso se uma conta Executar como já fizer parte da função de servidor sysadmin em instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2331b-165">However, you don’t need to do this if a Run As Account is already part of the sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with the actual user name being used as Run As Account.
    USE master

    -- Create login for the user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions to user.
    GRANT VIEW SERVER STATE TO [<UserName>]
    GRANT VIEW ANY DEFINITION TO [<UserName>]
    GRANT VIEW ANY DATABASE TO [<UserName>]

    -- Add database user for all the databases on SQL Server Instance, this is required for connecting to individual databases.
    -- NOTE: This command must be run anytime new databases are added to SQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="to-configure-the-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="2331b-166">Para configurar a conta Executar como do SQL usando o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2331b-166">To configure the SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="2331b-167">Abra uma janela do PowerShell e execute o script a seguir depois de atualizá-lo com as suas informações:</span><span class="sxs-lookup"><span data-stu-id="2331b-167">Open a PowerShell window and run the following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="2331b-168">Compreendendo como as recomendações são priorizadas</span><span class="sxs-lookup"><span data-stu-id="2331b-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="2331b-169">Cada recomendação feita recebe um valor de ponderação que identifica a importância relativa da recomendação.</span><span class="sxs-lookup"><span data-stu-id="2331b-169">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="2331b-170">Somente as dez recomendações mais importantes são mostradas.</span><span class="sxs-lookup"><span data-stu-id="2331b-170">Only the ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="2331b-171">Como os pesos são calculados</span><span class="sxs-lookup"><span data-stu-id="2331b-171">How weights are calculated</span></span>
<span data-ttu-id="2331b-172">Os pesos são valores agregados com base em três fatores principais:</span><span class="sxs-lookup"><span data-stu-id="2331b-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="2331b-173">A *probabilidade* de que um problema identificado cause problemas.</span><span class="sxs-lookup"><span data-stu-id="2331b-173">The *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="2331b-174">Uma probabilidade mais alta é igual a uma pontuação geral maior para a recomendação.</span><span class="sxs-lookup"><span data-stu-id="2331b-174">A higher probability equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="2331b-175">O *impacto* da questão na sua organização se ela causar um problema.</span><span class="sxs-lookup"><span data-stu-id="2331b-175">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="2331b-176">Um impacto maior é igual a uma pontuação geral maior para a recomendação.</span><span class="sxs-lookup"><span data-stu-id="2331b-176">A higher impact equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="2331b-177">O *esforço* necessário para implementar a recomendação.</span><span class="sxs-lookup"><span data-stu-id="2331b-177">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="2331b-178">Um esforço maior é igual a uma pontuação geral menor para a recomendação.</span><span class="sxs-lookup"><span data-stu-id="2331b-178">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="2331b-179">A importância de cada recomendação é expressa como um percentual da pontuação total disponível para todas as áreas de foco.</span><span class="sxs-lookup"><span data-stu-id="2331b-179">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="2331b-180">Por exemplo, se uma recomendação na área de foco de segurança e conformidade tiver uma pontuação de 5%, implementar essa recomendação aumentará sua pontuação geral de segurança e conformidade em 5%.</span><span class="sxs-lookup"><span data-stu-id="2331b-180">For example, if a recommendation in the Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="2331b-181">Áreas de foco</span><span class="sxs-lookup"><span data-stu-id="2331b-181">Focus areas</span></span>
<span data-ttu-id="2331b-182">**Segurança e conformidade** - essa área de foco mostra recomendações para possíveis ameaças de segurança e violações, políticas corporativas, bem como os requisitos de conformidade técnica, legal e regulatória.</span><span class="sxs-lookup"><span data-stu-id="2331b-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="2331b-183">**Disponibilidade e continuidade dos negócios** - essa área de foco mostra as recomendações para a disponibilidade de serviço, resiliência de sua infraestrutura e proteção dos negócios.</span><span class="sxs-lookup"><span data-stu-id="2331b-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="2331b-184">**Desempenho e escalabilidade** - essa área de foco mostra recomendações para ajudar a expansão da infraestrutura de TI de sua organização, garantir que seu ambiente de TI atende aos requisitos de desempenho atuais e estar apta a responder às necessidades de infraestrutura em constante mudança.</span><span class="sxs-lookup"><span data-stu-id="2331b-184">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="2331b-185">**Atualização, implantação e migração** - essa área de foco mostra recomendações para ajudá-lo a atualizar, migrar e implantar o SQL Server em sua infraestrutura existente.</span><span class="sxs-lookup"><span data-stu-id="2331b-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy SQL Server to your existing infrastructure.</span></span>

<span data-ttu-id="2331b-186">**Operações e monitoramento** - essa área de foco mostra recomendações que ajudam a simplificar as operações de TI, implementar manutenção preventiva e maximizar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="2331b-186">**Operations and Monitoring** - This focus area shows recommendations to help streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="2331b-187">**Gerenciamento de alterações e configuração** - essa área de foco mostra as recomendações para ajudar a proteger as operações diárias, garantir que as alterações não afetem sua infraestrutura negativamente, estabelecer procedimentos de controle de alterações, bem como para controlar e auditar as configurações do sistema.</span><span class="sxs-lookup"><span data-stu-id="2331b-187">**Change and Configuration Management** - This focus area shows recommendations to help protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and to track and audit system configurations.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="2331b-188">Você deve visar à pontuação de 100% em cada área de foco?</span><span class="sxs-lookup"><span data-stu-id="2331b-188">Should you aim to score 100% in every focus area?</span></span>
<span data-ttu-id="2331b-189">Não necessariamente.</span><span class="sxs-lookup"><span data-stu-id="2331b-189">Not necessarily.</span></span> <span data-ttu-id="2331b-190">As recomendações baseiam-se no conhecimento e nas experiências adquiridas pelos engenheiros da Microsoft em milhares de visitas a clientes.</span><span class="sxs-lookup"><span data-stu-id="2331b-190">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="2331b-191">No entanto, nenhuma infraestrutura de servidor é igual à outra, assim, recomendações específicas podem ser mais ou menos relevantes para você.</span><span class="sxs-lookup"><span data-stu-id="2331b-191">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="2331b-192">Por exemplo, algumas recomendações de segurança poderão ser menos relevantes se as máquinas virtuais não estiverem expostas à Internet.</span><span class="sxs-lookup"><span data-stu-id="2331b-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="2331b-193">Algumas recomendações de disponibilidade podem ser menos relevantes para os serviços que fornecem relatórios e coleta de dados ad hoc de baixa prioridade.</span><span class="sxs-lookup"><span data-stu-id="2331b-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="2331b-194">Problemas importantes para empresas maduras podem ser menos importantes para uma empresa start-up.</span><span class="sxs-lookup"><span data-stu-id="2331b-194">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="2331b-195">Você pode preferir identificar quais áreas de foco são suas prioridades e depois examinar como suas pontuações mudam ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="2331b-195">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="2331b-196">Cada recomendação inclui diretrizes sobre sua importância.</span><span class="sxs-lookup"><span data-stu-id="2331b-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="2331b-197">Você deve usar essas diretrizes para avaliar se é adequado implementar a recomendação considerando a natureza de seus serviços de TI e as necessidades comerciais da sua organização.</span><span class="sxs-lookup"><span data-stu-id="2331b-197">You should use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="2331b-198">Use as recomendações de área de foco de avaliação</span><span class="sxs-lookup"><span data-stu-id="2331b-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="2331b-199">Antes de usar uma solução de avaliação no OMS, é necessário ter a solução instalada.</span><span class="sxs-lookup"><span data-stu-id="2331b-199">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="2331b-200">Para ler mais sobre como instalar as soluções, confira [Adicionar soluções do Log Analytics por meio da Galeria de Soluções](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="2331b-200">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="2331b-201">Após a instalação, é possível exibir o resumo das recomendações usando o bloco Avaliação do SQL na página Visão geral do OMS.</span><span class="sxs-lookup"><span data-stu-id="2331b-201">After it is installed, you can view the summary of recommendations by using the SQL Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="2331b-202">Veja as avaliações de conformidade resumidas para sua infraestrutura e faça uma busca detalhada das recomendações.</span><span class="sxs-lookup"><span data-stu-id="2331b-202">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="2331b-203">Para exibir as recomendações para uma área de foco e tomar uma ação corretiva</span><span class="sxs-lookup"><span data-stu-id="2331b-203">To view recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="2331b-204">Na página **Visão Geral**, clique no bloco **Avaliação do SQL**.</span><span class="sxs-lookup"><span data-stu-id="2331b-204">On the **Overview** page, click the **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="2331b-205">Na página **Avaliação do SQL**, analise as informações resumidas em uma das folhas da área de foco e clique em uma para exibir as recomendações para a área de foco.</span><span class="sxs-lookup"><span data-stu-id="2331b-205">On the **SQL Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="2331b-206">Em qualquer uma das páginas da área de foco, você pode exibir as recomendações priorizadas para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="2331b-206">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="2331b-207">Clique em uma recomendação sob **Objetos Afetados** para exibir detalhes sobre o motivo pelo qual a recomendação foi feita.</span><span class="sxs-lookup"><span data-stu-id="2331b-207">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="2331b-208">![imagem de recomendações da Avaliação do SQL](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="2331b-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="2331b-209">É possível executar as ações corretivas sugeridas em **Ações Sugeridas**.</span><span class="sxs-lookup"><span data-stu-id="2331b-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="2331b-210">Quando o item tiver sido resolvido, avaliações posteriores gravarão que essas ações recomendadas foram executadas e sua pontuação de conformidade aumentará.</span><span class="sxs-lookup"><span data-stu-id="2331b-210">When the item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="2331b-211">Os itens corrigido aparecem como **Objetos Passados**.</span><span class="sxs-lookup"><span data-stu-id="2331b-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="2331b-212">Ignorar as recomendações</span><span class="sxs-lookup"><span data-stu-id="2331b-212">Ignore recommendations</span></span>
<span data-ttu-id="2331b-213">Se houver recomendações que deseja ignorar, você poderá criar um arquivo de texto que será usado pelo OMS para impedir que as recomendações sejam exibidas nos resultados da avaliação.</span><span class="sxs-lookup"><span data-stu-id="2331b-213">If you have recommendations that you want to ignore, you can create a text file that OMS will use to prevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="to-identify-recommendations-that-you-will-ignore"></a><span data-ttu-id="2331b-214">Para identificar as recomendações que serão ignoradas</span><span class="sxs-lookup"><span data-stu-id="2331b-214">To identify recommendations that you will ignore</span></span>
1. <span data-ttu-id="2331b-215">Entre em seu espaço de trabalho e abra a Pesquisa de Log.</span><span class="sxs-lookup"><span data-stu-id="2331b-215">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="2331b-216">Use a consulta a seguir para listar as recomendações que falharam para os computadores em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="2331b-216">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="2331b-217">Esta é uma captura de tela mostrando a consulta da Pesquisa de Log: ![recomendações com falha](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="2331b-217">Here's a screen shot showing the Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="2331b-218">Escolha as recomendações que você deseja ignorar.</span><span class="sxs-lookup"><span data-stu-id="2331b-218">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="2331b-219">Você usará os valores para RecommendationId no próximo procedimento.</span><span class="sxs-lookup"><span data-stu-id="2331b-219">You’ll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="2331b-220">Criar e usar um arquivo de texto IgnoreRecommendations.txt</span><span class="sxs-lookup"><span data-stu-id="2331b-220">To create and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="2331b-221">Crie um arquivo chamado IgnoreRecommendations.txt.</span><span class="sxs-lookup"><span data-stu-id="2331b-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="2331b-222">Cole ou digite cada RecommendationId para cada recomendação que você deseja que o OMS ignore em uma linha separada, salve e feche o arquivo.</span><span class="sxs-lookup"><span data-stu-id="2331b-222">Paste or type each RecommendationId for each recommendation that you want OMS to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="2331b-223">Coloque o arquivo na pasta a seguir em cada computador no qual você deseja que o OMS ignore as recomendações.</span><span class="sxs-lookup"><span data-stu-id="2331b-223">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
   * <span data-ttu-id="2331b-224">Em computadores com o Microsoft Monitoring Agent (conectado diretamente ou por meio do Operations Manager) - *SystemDrive*:\Arquivos de Programas\Microsoft Monitoring Agent\Agent</span><span class="sxs-lookup"><span data-stu-id="2331b-224">On computers with the Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="2331b-225">No servidor de gerenciamento do Operations Manager - *SystemDrive*:\Arquivos de Programa\Microsoft System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="2331b-225">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="2331b-226">Para verificar se as recomendações são ignoradas</span><span class="sxs-lookup"><span data-stu-id="2331b-226">To verify that recommendations are ignored</span></span>
1. <span data-ttu-id="2331b-227">Após a execução da próxima avaliação agendada, por padrão a cada 7 dias, as recomendações especificadas são marcadas como Ignoradas e não aparecerão no painel de avaliação.</span><span class="sxs-lookup"><span data-stu-id="2331b-227">After the next scheduled assessment runs, by default every 7 days, the specified recommendations are marked Ignored and will not appear on the assessment dashboard.</span></span>
2. <span data-ttu-id="2331b-228">É possível usar as consultas da Pesquisa de Log a seguir para listar todas as recomendações ignoradas.</span><span class="sxs-lookup"><span data-stu-id="2331b-228">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="2331b-229">Se você decidir posteriormente que deseja ver as recomendações ignoradas, remova todos os arquivos IgnoreRecommendations.txt ou remova as RecommendationIDs deles.</span><span class="sxs-lookup"><span data-stu-id="2331b-229">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="2331b-230">Perguntas frequentes sobre soluções de Avaliação de SQL</span><span class="sxs-lookup"><span data-stu-id="2331b-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="2331b-231">*Com que frequência uma avaliação é executada?*</span><span class="sxs-lookup"><span data-stu-id="2331b-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="2331b-232">A avaliação é executada a cada sete dias.</span><span class="sxs-lookup"><span data-stu-id="2331b-232">The assessment runs every 7 days.</span></span>

<span data-ttu-id="2331b-233">*Há uma maneira de configurar a frequência com que a avaliação é executada?*</span><span class="sxs-lookup"><span data-stu-id="2331b-233">*Is there a way to configure how often the assessment runs?*</span></span>

* <span data-ttu-id="2331b-234">Não no momento.</span><span class="sxs-lookup"><span data-stu-id="2331b-234">Not at this time.</span></span>

<span data-ttu-id="2331b-235">*Se outro servidor for descoberto após ter adicionado a solução de avaliação do SQL, ele será avaliado?*</span><span class="sxs-lookup"><span data-stu-id="2331b-235">*If another server is discovered after I’ve added the SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="2331b-236">Sim, assim que for descoberto, ele é avaliado a partir de então a cada sete dias.</span><span class="sxs-lookup"><span data-stu-id="2331b-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="2331b-237">*Se um servidor for encerrado, quando ele será removido da avaliação?*</span><span class="sxs-lookup"><span data-stu-id="2331b-237">*If a server is decommissioned, when will it be removed from the assessment?*</span></span>

* <span data-ttu-id="2331b-238">Se um servidor não enviar dados por três semanas, ele será removido.</span><span class="sxs-lookup"><span data-stu-id="2331b-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="2331b-239">*Qual é o nome do processo que faz a coleta de dados?*</span><span class="sxs-lookup"><span data-stu-id="2331b-239">*What is the name of the process that does the data collection?*</span></span>

* <span data-ttu-id="2331b-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="2331b-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="2331b-241">*Quanto tempo leva para os dados serem coletados?*</span><span class="sxs-lookup"><span data-stu-id="2331b-241">*How long does it take for data to be collected?*</span></span>

* <span data-ttu-id="2331b-242">A coleta de dados real no servidor leva aproximadamente 1 hora.</span><span class="sxs-lookup"><span data-stu-id="2331b-242">The actual data collection on the server takes about 1 hour.</span></span> <span data-ttu-id="2331b-243">Pode levar mais tempo em servidores que têm um grande número de instâncias ou bancos de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="2331b-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="2331b-244">*Que tipo de dados é coletado?*</span><span class="sxs-lookup"><span data-stu-id="2331b-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="2331b-245">Os seguintes tipos de dados são coletados:</span><span class="sxs-lookup"><span data-stu-id="2331b-245">The following types of data are collected:</span></span>
  * <span data-ttu-id="2331b-246">WMI</span><span class="sxs-lookup"><span data-stu-id="2331b-246">WMI</span></span>
  * <span data-ttu-id="2331b-247">Registro</span><span class="sxs-lookup"><span data-stu-id="2331b-247">Registry</span></span>
  * <span data-ttu-id="2331b-248">Contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="2331b-248">Performance counters</span></span>
  * <span data-ttu-id="2331b-249">Exibições de gerenciamento dinâmico SQL (DMV).</span><span class="sxs-lookup"><span data-stu-id="2331b-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="2331b-250">*Há uma maneira de configurar quando os dados são coletados?*</span><span class="sxs-lookup"><span data-stu-id="2331b-250">*Is there a way to configure when data is collected?*</span></span>

* <span data-ttu-id="2331b-251">Não no momento.</span><span class="sxs-lookup"><span data-stu-id="2331b-251">Not at this time.</span></span>

<span data-ttu-id="2331b-252">*Por que é necessário configurar uma conta Executar como?*</span><span class="sxs-lookup"><span data-stu-id="2331b-252">*Why do I have to configure a Run As Account?*</span></span>

* <span data-ttu-id="2331b-253">Para o SQL Server, um pequeno número de consultas SQL é executado.</span><span class="sxs-lookup"><span data-stu-id="2331b-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="2331b-254">Para elas serem executadas, uma conta Executar como com permissões VIEW SERVER STATE devem ser usadas para SQL.</span><span class="sxs-lookup"><span data-stu-id="2331b-254">In order for them to run, a Run As Account with VIEW SERVER STATE permissions to SQL must be used.</span></span>  <span data-ttu-id="2331b-255">Além disso, para consultar WMI, são necessárias credenciais de administrador local.</span><span class="sxs-lookup"><span data-stu-id="2331b-255">In addition, in order to query WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="2331b-256">*Por que apenas as 10 principais recomendações são exibidas?*</span><span class="sxs-lookup"><span data-stu-id="2331b-256">*Why display only the top 10 recommendations?*</span></span>

* <span data-ttu-id="2331b-257">Em vez de apresentar uma lista exaustiva de tarefas, é recomendável que você se concentre em tratar as recomendações priorizadas primeiro.</span><span class="sxs-lookup"><span data-stu-id="2331b-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="2331b-258">Depois de tratar dessas recomendações, recomendações adicionais serão disponibilizadas.</span><span class="sxs-lookup"><span data-stu-id="2331b-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="2331b-259">Se preferir ver a lista detalhada, exiba todas as recomendações usando a pesquisa de log do OMS.</span><span class="sxs-lookup"><span data-stu-id="2331b-259">If you prefer to see the detailed list, you can view all recommendations using the OMS log search.</span></span>

<span data-ttu-id="2331b-260">*É possível ignorar uma recomendação?*</span><span class="sxs-lookup"><span data-stu-id="2331b-260">*Is there a way to ignore a recommendation?*</span></span>

* <span data-ttu-id="2331b-261">Sim, confira a seção [Ignorar recomendações](#ignore-recommendations) acima.</span><span class="sxs-lookup"><span data-stu-id="2331b-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2331b-262">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2331b-262">Next steps</span></span>
* <span data-ttu-id="2331b-263">[Pesquise nos logs](log-analytics-log-searches.md) para exibir dados detalhados de Avaliação do SQL e recomendações.</span><span class="sxs-lookup"><span data-stu-id="2331b-263">[Search logs](log-analytics-log-searches.md) to view detailed SQL Assessment data and recommendations.</span></span>
