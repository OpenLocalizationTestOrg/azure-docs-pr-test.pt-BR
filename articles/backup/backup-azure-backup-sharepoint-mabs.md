---
title: aaaUse tooback de servidor de Backup do Azure a um tooAzure de farm do SharePoint | Microsoft Docs
description: "Usar o Azure Backup Server tooback e restaurar os dados do SharePoint. Este artigo fornece Olá informações tooconfigure seu farm do SharePoint para que os dados desejados podem ser armazenados no Azure. Você pode restaurar dados protegidos do SharePoint do disco ou do Azure."
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 350c1ac0f3518f400062f3b586bbe9710a79915a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a><span data-ttu-id="4b3fd-105">Fazer backup de um tooAzure de farm do SharePoint</span><span class="sxs-lookup"><span data-stu-id="4b3fd-105">Back up a SharePoint farm tooAzure</span></span>
<span data-ttu-id="4b3fd-106">Fazer backup do SharePoint farm tooMicrosoft do Azure usando o Microsoft Azure Backup Server (MABS) em quantidade Olá mesma maneira que você faz backup de outras fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-106">You back up a SharePoint farm tooMicrosoft Azure by using Microsoft Azure Backup Server (MABS) in much hello same way that you back up other data sources.</span></span> <span data-ttu-id="4b3fd-107">O Backup do Azure oferece a flexibilidade de saudação agendamento de backup toocreate pontos de backup diários, semanais, mensais ou anuais e fornece opções de política de retenção para vários pontos de backup.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-107">Azure Backup provides flexibility in hello backup schedule toocreate daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="4b3fd-108">Ele também fornece Olá recurso toostore disco local cópias para rápido objetivos de tempo de recuperação (RTO) e toostore copia tooAzure para retenção econômica de longo prazo.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-108">It also provides hello capability toostore local disk copies for quick recovery-time objectives (RTO) and toostore copies tooAzure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="4b3fd-109">Versões do SharePoint com suporte e cenários de proteção relacionados</span><span class="sxs-lookup"><span data-stu-id="4b3fd-109">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="4b3fd-110">Backup do Azure para o DPM oferece suporte a saudação os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="4b3fd-110">Azure Backup for DPM supports hello following scenarios:</span></span>

| <span data-ttu-id="4b3fd-111">Carga de trabalho</span><span class="sxs-lookup"><span data-stu-id="4b3fd-111">Workload</span></span> | <span data-ttu-id="4b3fd-112">Versão</span><span class="sxs-lookup"><span data-stu-id="4b3fd-112">Version</span></span> | <span data-ttu-id="4b3fd-113">Implantação do SharePoint</span><span class="sxs-lookup"><span data-stu-id="4b3fd-113">SharePoint deployment</span></span> | <span data-ttu-id="4b3fd-114">Proteção e recuperação</span><span class="sxs-lookup"><span data-stu-id="4b3fd-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="4b3fd-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="4b3fd-115">SharePoint</span></span> |<span data-ttu-id="4b3fd-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="4b3fd-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="4b3fd-117">SharePoint implantado como um servidor físico ou em uma máquina virtual Hyper-V/VMware </span><span class="sxs-lookup"><span data-stu-id="4b3fd-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="4b3fd-118">AlwaysOn do SQL</span><span class="sxs-lookup"><span data-stu-id="4b3fd-118">SQL AlwaysOn</span></span> | <span data-ttu-id="4b3fd-119">Opções recuperação para proteger o Farm do SharePoint: farm de recuperação, banco de dados e um arquivo ou item de lista dos pontos de recuperação de disco.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="4b3fd-120">Recuperação do farm e do banco de dados dos pontos de recuperação do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-120">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="4b3fd-121">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="4b3fd-121">Before you start</span></span>
<span data-ttu-id="4b3fd-122">Há algumas coisas que você precisa tooconfirm antes de você fazer backup de um tooAzure de farm do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-122">There are a few things you need tooconfirm before you back up a SharePoint farm tooAzure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4b3fd-123">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4b3fd-123">Prerequisites</span></span>
<span data-ttu-id="4b3fd-124">Antes de prosseguir, certifique-se de que você tenha [instalado e preparado hello Azure Backup Server](backup-azure-microsoft-azure-backup.md) tooprotect cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-124">Before you proceed, make sure that you have [installed and prepared hello Azure Backup Server](backup-azure-microsoft-azure-backup.md) tooprotect workloads.</span></span>

### <a name="protection-agent"></a><span data-ttu-id="4b3fd-125">Agente de proteção</span><span class="sxs-lookup"><span data-stu-id="4b3fd-125">Protection agent</span></span>
<span data-ttu-id="4b3fd-126">Agente de proteção de saudação deve ser instalado no servidor de saudação que está executando o SharePoint, servidores de saudação que executam o SQL Server e todos os outros servidores que fazem parte do farm do SharePoint de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-126">hello Protection agent must be installed on hello server that's running SharePoint, hello servers that are running SQL Server, and all other servers that are part of hello SharePoint farm.</span></span> <span data-ttu-id="4b3fd-127">Para obter mais informações sobre como tooset o agente de proteção de hello, consulte [agente de proteção de instalação](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span><span class="sxs-lookup"><span data-stu-id="4b3fd-127">For more information about how tooset up hello protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="4b3fd-128">Olá uma exceção é que você instale o agente de saudação apenas em um único front-end (WFE) servidor web.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-128">hello one exception is that you install hello agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="4b3fd-129">Como ponto de entrada hello para proteção, o DPM precisa agente Olá em um WFE tooserve de somente de servidor.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-129">DPM needs hello agent on one WFE server only tooserve as hello entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="4b3fd-130">Farm do SharePoint</span><span class="sxs-lookup"><span data-stu-id="4b3fd-130">SharePoint farm</span></span>
<span data-ttu-id="4b3fd-131">Para cada 10 milhões de itens no farm hello, deve haver pelo menos 2 GB de espaço no volume de saudação onde Olá MABS pasta está localizada.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-131">For every 10 million items in hello farm, there must be at least 2 GB of space on hello volume where hello MABS folder is located.</span></span> <span data-ttu-id="4b3fd-132">Esse espaço é necessário para a geração de catálogo.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-132">This space is required for catalog generation.</span></span> <span data-ttu-id="4b3fd-133">Para MABS toorecover itens específicos (coleções de sites, sites, listas, bibliotecas de documentos, pastas, documentos individuais e itens de lista), a geração de catálogo cria uma lista de URLs Olá contidos em cada banco de dados de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-133">For MABS toorecover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of hello URLs that are contained within each content database.</span></span> <span data-ttu-id="4b3fd-134">Você pode exibir a lista de saudação de URLs no painel item recuperável Olá Olá **recuperação** área do Console do administrador do MABS de tarefa.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-134">You can view hello list of URLs in hello recoverable item pane in hello **Recovery** task area of MABS Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="4b3fd-135">SQL Server</span><span class="sxs-lookup"><span data-stu-id="4b3fd-135">SQL Server</span></span>
<span data-ttu-id="4b3fd-136">O MABS é executado como uma conta LocalSystem.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-136">MABS runs as a LocalSystem account.</span></span> <span data-ttu-id="4b3fd-137">tooback backup de bancos de dados do SQL Server, MABS precisa de privilégios de sysadmin nessa conta para o servidor de saudação que está executando o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-137">tooback up SQL Server databases, MABS needs sysadmin privileges on that account for hello server that's running SQL Server.</span></span> <span data-ttu-id="4b3fd-138">Definir Autoridade NT\Sistema muito*sysadmin* no servidor de saudação que está executando o SQL Server antes de fazer seu backup.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-138">Set NT AUTHORITY\SYSTEM too*sysadmin* on hello server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="4b3fd-139">Se o farm do SharePoint Olá tiver bancos de dados do SQL Server que estão configurados com aliases do SQL Server, instale componentes de cliente do SQL Server Olá no servidor Web front-end Olá que MABS irá proteger.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-139">If hello SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install hello SQL Server client components on hello front-end Web server that MABS will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="4b3fd-140">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="4b3fd-140">SharePoint Server</span></span>
<span data-ttu-id="4b3fd-141">Embora o desempenho dependa de muitos fatores tais como o tamanho do farm do SharePoint, as diretrizes gerais são de que um MABS pode ser usado para proteger um farm do SharePoint de 25 TB.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-141">While performance depends on many factors such as size of SharePoint farm, as general guidance one MABS can protect a 25 TB SharePoint farm.</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="4b3fd-142">O que não tem suporte</span><span class="sxs-lookup"><span data-stu-id="4b3fd-142">What's not supported</span></span>
* <span data-ttu-id="4b3fd-143">O MABS que protege um farm do SharePoint não protege os índices de pesquisa ou os bancos de dados do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-143">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="4b3fd-144">Você precisará tooconfigure proteção de saudação desses bancos de dados separadamente.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-144">You will need tooconfigure hello protection of these databases separately.</span></span>
* <span data-ttu-id="4b3fd-145">O MABS não fornece backup dos bancos de dados do SQL Server do SharePoint hospedados em compartilhamento SOFS (Servidor de Arquivos de Escalabilidade Horizontal).</span><span class="sxs-lookup"><span data-stu-id="4b3fd-145">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="4b3fd-146">Configurar a proteção do SharePoint</span><span class="sxs-lookup"><span data-stu-id="4b3fd-146">Configure SharePoint protection</span></span>
<span data-ttu-id="4b3fd-147">Antes de usar MABS tooprotect do SharePoint, você deve configurar o serviço de gravador VSS do SharePoint de saudação (serviço de gravador WSS) usando **ConfigureSharePoint.exe**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-147">Before you can use MABS tooprotect SharePoint, you must configure hello SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="4b3fd-148">Você pode encontrar **ConfigureSharePoint.exe** na pasta \bin de saudação [caminho de instalação MABS] no servidor web front-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-148">You can find **ConfigureSharePoint.exe** in hello [MABS Installation Path]\bin folder on hello front-end web server.</span></span> <span data-ttu-id="4b3fd-149">Essa ferramenta fornece um agente de proteção de saudação com credenciais Olá Olá farm do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-149">This tool provides hello protection agent with hello credentials for hello SharePoint farm.</span></span> <span data-ttu-id="4b3fd-150">Você a executa em um único servidor WFE.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-150">You run it on a single WFE server.</span></span> <span data-ttu-id="4b3fd-151">Se você tiver vários servidores WFE, selecione apenas um ao configurar um grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-151">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a><span data-ttu-id="4b3fd-152">Olá tooconfigure serviço de gravador VSS do SharePoint</span><span class="sxs-lookup"><span data-stu-id="4b3fd-152">tooconfigure hello SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="4b3fd-153">No servidor WFE hello, em um prompt de comando, vá muito \bin\ [local da instalação MABS]</span><span class="sxs-lookup"><span data-stu-id="4b3fd-153">On hello WFE server, at a command prompt, go too[MABS installation location]\bin\\</span></span>
2. <span data-ttu-id="4b3fd-154">Insira ConfigureSharePoint -EnableSharePointProtection.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-154">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="4b3fd-155">Insira as credenciais de administrador de farm hello.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-155">Enter hello farm administrator credentials.</span></span> <span data-ttu-id="4b3fd-156">Essa conta deve ser um membro do grupo de administradores local Olá no servidor WFE hello.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-156">This account should be a member of hello local Administrator group on hello WFE server.</span></span> <span data-ttu-id="4b3fd-157">Se o administrador de farm Olá não é uma saudação de concessão de administrador local as seguintes permissões no servidor WFE hello:</span><span class="sxs-lookup"><span data-stu-id="4b3fd-157">If hello farm administrator isn’t a local admin grant hello following permissions on hello WFE server:</span></span>
   * <span data-ttu-id="4b3fd-158">Grant Olá WSS_Admin_WPG controle total toohello DPM pasta grupo (% programa Files%\Microsoft Azure Backup\DPM).</span><span class="sxs-lookup"><span data-stu-id="4b3fd-158">Grant hello WSS_Admin_WPG group full control toohello DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span></span>
   * <span data-ttu-id="4b3fd-159">Grant Olá WSS_Admin_WPG grupo acesso de leitura toohello DPM chave do registro (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span><span class="sxs-lookup"><span data-stu-id="4b3fd-159">Grant hello WSS_Admin_WPG group read access toohello DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="4b3fd-160">Você precisará toorerun ConfigureSharePoint.exe sempre que houver uma alteração nas credenciais de administrador de farm do SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-160">You’ll need toorerun ConfigureSharePoint.exe whenever there’s a change in hello SharePoint farm administrator credentials.</span></span>
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a><span data-ttu-id="4b3fd-161">Fazer backup de um farm do SharePoint usando o MABS</span><span class="sxs-lookup"><span data-stu-id="4b3fd-161">Back up a SharePoint farm by using MABS</span></span>
<span data-ttu-id="4b3fd-162">Depois que você configurou MABS e hello farm do SharePoint, conforme explicado anteriormente, o SharePoint pode ser protegido por MABS.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-162">After you have configured MABS and hello SharePoint farm as explained previously, SharePoint can be protected by MABS.</span></span>

### <a name="tooprotect-a-sharepoint-farm"></a><span data-ttu-id="4b3fd-163">tooprotect um farm do SharePoint</span><span class="sxs-lookup"><span data-stu-id="4b3fd-163">tooprotect a SharePoint farm</span></span>
1. <span data-ttu-id="4b3fd-164">De saudação **proteção** guia da saudação MABS Administrator Console, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-164">From hello **Protection** tab of hello MABS Administrator Console, click **New**.</span></span>
    <span data-ttu-id="4b3fd-165">![Guia Nova Proteção](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="4b3fd-165">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="4b3fd-166">Em Olá **Selecionar tipo de grupo de proteção** página de saudação **criar novo grupo de proteção** assistente, selecione **servidores**e, em seguida, clique em **próximo** .</span><span class="sxs-lookup"><span data-stu-id="4b3fd-166">On hello **Select Protection Group Type** page of hello **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>

    ![Selecionar o tipo de Grupo de Proteção](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="4b3fd-168">Em Olá **selecionar membros do grupo** tela, caixa de seleção select Olá Olá SharePoint server que deseja tooprotect e clique **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-168">On hello **Select Group Members** screen, select hello check box for hello SharePoint server you want tooprotect and click **Next**.</span></span>

    ![Selecionar membros do grupo](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > <span data-ttu-id="4b3fd-170">Com o agente de proteção Olá instalado, você pode ver servidor Olá no Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-170">With hello protection agent installed, you can see hello server in hello wizard.</span></span> <span data-ttu-id="4b3fd-171">O MABS também mostra sua estrutura.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-171">MABS also shows its structure.</span></span> <span data-ttu-id="4b3fd-172">Porque você executou o ConfigureSharePoint.exe, MABS se comunica com o serviço de gravador VSS do SharePoint hello e seus bancos de dados do SQL Server correspondentes e reconhece a estrutura do farm do SharePoint hello, Olá associado bancos de dados de conteúdo e todos os itens correspondentes.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-172">Because you ran ConfigureSharePoint.exe, MABS communicates with hello SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes hello SharePoint farm structure, hello associated content databases, and any corresponding items.</span></span>
   >
   >
4. <span data-ttu-id="4b3fd-173">Em Olá **Selecionar método de proteção de dados** Insira nome de saudação do hello **grupo de proteção**e selecione sua preferência *métodos de proteção*.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-173">On hello **Select Data Protection Method** page, enter hello name of hello **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="4b3fd-174">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-174">Click **Next**.</span></span>

    ![Selecionar método de proteção de dados](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > <span data-ttu-id="4b3fd-176">método de proteção de disco Hello ajuda toomeet curto objetivos de tempo de recuperação.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-176">hello disk protection method helps toomeet short recovery-time objectives.</span></span>
   >
   >
5. <span data-ttu-id="4b3fd-177">Em Olá **especificar objetivos de curto prazo** , selecione sua preferência **período de retenção** e identificar quando desejar toooccur backups.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-177">On hello **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups toooccur.</span></span>

    ![Especificar objetivos de curto prazo](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > <span data-ttu-id="4b3fd-179">Como a recuperação geralmente é necessária para dados que são menos de cinco dias, é selecionado um período de retenção de cinco dias no disco e garante que o backup Olá acontece durante o horário não seja de produção, para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-179">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that hello backup happens during non-production hours, for this example.</span></span>
   >
   >
6. <span data-ttu-id="4b3fd-180">Examine Olá espaço pool de armazenamento em disco alocado para o grupo de proteção Olá e então clique **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-180">Review hello storage pool disk space allocated for hello protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="4b3fd-181">Para cada grupo de proteção, MABS aloca toostore de espaço em disco e gerenciar réplicas.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-181">For every protection group, MABS allocates disk space toostore and manage replicas.</span></span> <span data-ttu-id="4b3fd-182">Neste ponto, MABS deve criar uma cópia dos dados de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-182">At this point, MABS must create a copy of hello selected data.</span></span> <span data-ttu-id="4b3fd-183">Selecione como e quando você deseja réplica Olá criada e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-183">Select how and when you want hello replica created, and then click **Next**.</span></span>

    ![Escolher método de criação de réplica](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > <span data-ttu-id="4b3fd-185">toomake-se de que o tráfego de rede não é afetado, selecione uma hora fora do horário de produção.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-185">toomake sure that network traffic is not effected, select a time outside production hours.</span></span>
   >
   >
8. <span data-ttu-id="4b3fd-186">MABS garante a integridade de dados executando verificações de consistência na réplica de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-186">MABS ensures data integrity by performing consistency checks on hello replica.</span></span> <span data-ttu-id="4b3fd-187">Há duas opções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-187">There are two available options.</span></span> <span data-ttu-id="4b3fd-188">Você pode definir as verificações de consistência de toorun uma agenda ou o DPM pode executar verificações de consistência automaticamente na réplica de saudação sempre que se torna inconsistente.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-188">You can define a schedule toorun consistency checks, or DPM can run consistency checks automatically on hello replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="4b3fd-189">Selecione sua opção desejada e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-189">Select your preferred option, and then click **Next**.</span></span>

    ![Verificação de consistência](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="4b3fd-191">Em Olá **especificar dados de proteção Online** , selecione o farm do SharePoint de saudação que você deseja tooprotect e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-191">On hello **Specify Online Protection Data** page, select hello SharePoint farm that you want tooprotect, and then click **Next**.</span></span>

    ![Proteção do SharePoint do DPM1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="4b3fd-193">Em Olá **especificar agendamento de Backup Online** página, selecione a agenda desejada e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-193">On hello **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="4b3fd-195">MABS fornece um máximo de dois tooAzure backups diários da saudação ponto backup de disco mais recente disponível.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-195">MABS provides a maximum of two daily backups tooAzure from hello then available latest disk backup point.</span></span> <span data-ttu-id="4b3fd-196">O Backup do Azure também pode controlar a quantidade de saudação de largura de banda WAN que pode ser usada para backups em horário de pico e fora de pico usando [limitação de rede de Backup do Azure](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span><span class="sxs-lookup"><span data-stu-id="4b3fd-196">Azure Backup can also control hello amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    >
    >
11. <span data-ttu-id="4b3fd-197">Dependendo do agendamento de backup Olá que você selecionou no hello **especificar política de retenção Online** página política de retenção de saudação select para pontos de backup diárias, semanais, mensais e anuais.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-197">Depending on hello backup schedule that you selected, on hello **Specify Online Retention Policy** page, select hello retention policy for daily, weekly, monthly, and yearly backup points.</span></span>

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > <span data-ttu-id="4b3fd-199">O MABS usa um esquema de retenção de avô-pai-filho em que uma política de retenção diferente pode ser escolhida para pontos de backup distintos.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-199">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    >
    >
12. <span data-ttu-id="4b3fd-200">Toodisk semelhante, uma réplica de ponto inicial de referência deve toobe criado no Azure.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-200">Similar toodisk, an initial reference point replica needs toobe created in Azure.</span></span> <span data-ttu-id="4b3fd-201">Selecione sua opção preferida de toocreate tooAzure uma cópia de backup inicial e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-201">Select your preferred option toocreate an initial backup copy tooAzure, and then click **Next**.</span></span>

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="4b3fd-203">Examine as configurações selecionadas no hello **resumo** página e, em seguida, clique em **criar grupo**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-203">Review your selected settings on hello **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="4b3fd-204">Você verá uma mensagem de êxito após a criação do grupo de proteção de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-204">You will see a success message after hello protection group has been created.</span></span>

    ![Resumo](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a><span data-ttu-id="4b3fd-206">Restaurar um item do SharePoint do disco usando o MABS</span><span class="sxs-lookup"><span data-stu-id="4b3fd-206">Restore a SharePoint item from disk by using MABS</span></span>
<span data-ttu-id="4b3fd-207">Em Olá exemplo a seguir, Olá *item do SharePoint recuperando* tenha sido excluído acidentalmente e precisa toobe recuperado.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-207">In hello following example, hello *Recovering SharePoint item* has been accidentally deleted and needs toobe recovered.</span></span>
<span data-ttu-id="4b3fd-208">![Proteção do SharePoint do MABS 4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="4b3fd-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="4b3fd-209">Olá abrir **Console do administrador do DPM**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-209">Open hello **DPM Administrator Console**.</span></span> <span data-ttu-id="4b3fd-210">Todos os farms do SharePoint que são protegidos pelo DPM são mostrados no hello **proteção** guia.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-210">All SharePoint farms that are protected by DPM are shown in hello **Protection** tab.</span></span>

    ![Proteção do SharePoint do MABS 3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="4b3fd-212">item de saudação toorecover toobegin, selecione Olá **recuperação** guia.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-212">toobegin toorecover hello item, select hello **Recovery** tab.</span></span>

    ![Proteção do SharePoint do MABS 5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="4b3fd-214">É possível pesquisar no SharePoint para localizar o *item Recuperando SharePoint* usando uma pesquisa baseada em curinga dentro de um intervalo de ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-214">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>

    ![Proteção do SharePoint do MABS 6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="4b3fd-216">Selecione o ponto de recuperação apropriado de Olá Olá dos resultados da pesquisa, item hello e, em seguida, selecione **recuperar**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-216">Select hello appropriate recovery point from hello search results, right-click hello item, and then select **Recover**.</span></span>
5. <span data-ttu-id="4b3fd-217">Você também pode navegar pelos vários pontos de recuperação e selecione toorecover um banco de dados ou item.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-217">You can also browse through various recovery points and select a database or item toorecover.</span></span> <span data-ttu-id="4b3fd-218">Selecione **data > tempo de recuperação**e, em seguida, selecione Olá correto **banco de dados > farm do SharePoint > ponto de recuperação > Item**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-218">Select **Date > Recovery time**, and then select hello correct **Database > SharePoint farm > Recovery point > Item**.</span></span>

    ![Proteção do SharePoint do MABS 7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="4b3fd-220">Item de saudação e, em seguida, selecione **recuperar** tooopen Olá **Assistente de recuperação**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-220">Right-click hello item, and then select **Recover** tooopen hello **Recovery Wizard**.</span></span> <span data-ttu-id="4b3fd-221">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-221">Click **Next**.</span></span>

    ![Rever Seleção de Recuperação](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="4b3fd-223">Selecionar tipo de saudação de recuperação que você deseja tooperform e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-223">Select hello type of recovery that you want tooperform, and then click **Next**.</span></span>

    ![Tipo de Recuperação](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > <span data-ttu-id="4b3fd-225">Olá seleção de **recuperar toooriginal** em Olá exemplo recupera o site do SharePoint para original do hello item toohello.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-225">hello selection of **Recover toooriginal** in hello example recovers hello item toohello original SharePoint site.</span></span>
   >
   >
8. <span data-ttu-id="4b3fd-226">Selecione Olá **processo de recuperação** que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-226">Select hello **Recovery Process** that you want toouse.</span></span>

   * <span data-ttu-id="4b3fd-227">Selecione **recuperar sem usar um farm de recuperação** se o farm do SharePoint de saudação não foi alterado e hello, mesmo que a recuperação de saudação do ponto que é está sendo restaurado.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-227">Select **Recover without using a recovery farm** if hello SharePoint farm has not changed and is hello same as hello recovery point that is being restored.</span></span>
   * <span data-ttu-id="4b3fd-228">Selecione **recuperar usando um farm de recuperação** se o farm do SharePoint Olá foi alterado desde que o ponto de recuperação Olá foi criado.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-228">Select **Recover using a recovery farm** if hello SharePoint farm has changed since hello recovery point was created.</span></span>

     ![Processo de Recuperação](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="4b3fd-230">Forneça um preparação do SQL Server instância local toorecover Olá banco de dados temporariamente e fornecer um compartilhamento de arquivo temporário em MABS e Olá no servidor que está executando o item do SharePoint toorecover hello.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-230">Provide a staging SQL Server instance location toorecover hello database temporarily, and provide a staging file share on MABS and hello server that's running SharePoint toorecover hello item.</span></span>

    ![Local de Preparo1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    <span data-ttu-id="4b3fd-232">MABS anexa Olá conteúdo banco de dados que está hospedando o hello SharePoint item toohello temporária instância do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-232">MABS attaches hello content database that is hosting hello SharePoint item toohello temporary SQL Server instance.</span></span> <span data-ttu-id="4b3fd-233">Do banco de dados de conteúdo hello, ele recupera o item de saudação e a coloca na Olá local do arquivo em MABS de preparo.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-233">From hello content database, it recovers hello item and puts it on hello staging file location on MABS.</span></span> <span data-ttu-id="4b3fd-234">Olá recuperado item que está em Olá local de preparo agora necessidades toobe exportado toohello local no farm do SharePoint de saudação de preparo.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-234">hello recovered item that's on hello staging location now needs toobe exported toohello staging location on hello SharePoint farm.</span></span>

    ![Local de Preparo2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="4b3fd-236">Selecione **especificar opções de recuperação**e aplicar configurações de segurança toohello farm do SharePoint ou aplicar configurações de segurança Olá Olá do ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-236">Select **Specify recovery options**, and apply security settings toohello SharePoint farm or apply hello security settings of hello recovery point.</span></span> <span data-ttu-id="4b3fd-237">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-237">Click **Next**.</span></span>

    ![Opções de Recuperação](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > <span data-ttu-id="4b3fd-239">Você pode escolher o uso de largura de banda de rede toothrottle hello.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-239">You can choose toothrottle hello network bandwidth usage.</span></span> <span data-ttu-id="4b3fd-240">Isso minimiza o servidor de produção do impacto toohello durante o horário de produção.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-240">This minimizes impact toohello production server during production hours.</span></span>
    >
    >
11. <span data-ttu-id="4b3fd-241">Examine as informações de resumo hello e, em seguida, clique em **recuperar** toobegin recuperação de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-241">Review hello summary information, and then click **Recover** toobegin recovery of hello file.</span></span>

    ![Resumo da recuperação](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="4b3fd-243">Agora selecione Olá **monitoramento** guia Olá **Console do administrador do MABS** tooview Olá **Status** de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-243">Now select hello **Monitoring** tab in hello **MABS Administrator Console** tooview hello **Status** of hello recovery.</span></span>

    ![Status da Recuperação](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > <span data-ttu-id="4b3fd-245">arquivo Hello agora é restaurado.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-245">hello file is now restored.</span></span> <span data-ttu-id="4b3fd-246">Você pode atualizar o arquivo do hello SharePoint site toocheck Olá restaurado.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-246">You can refresh hello SharePoint site toocheck hello restored file.</span></span>
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="4b3fd-247">Restaurar um banco de dados do SharePoint do Azure usando o DPM</span><span class="sxs-lookup"><span data-stu-id="4b3fd-247">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="4b3fd-248">toorecover banco de dados de conteúdo um SharePoint, navegue pelos vários pontos de recuperação (conforme mostrado anteriormente) e selecione Olá ponto de recuperação que você deseja toorestore.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-248">toorecover a SharePoint content database, browse through various recovery points (as shown previously), and select hello recovery point that you want toorestore.</span></span>

    ![Proteção do SharePoint do MABS 8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="4b3fd-250">Clique duas vezes em Olá SharePoint recuperação tooshow ponto Olá disponíveis do SharePoint informações do catálogo.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-250">Double-click hello SharePoint recovery point tooshow hello available SharePoint catalog information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4b3fd-251">Porque o farm do SharePoint hello está protegido para retenção de longo prazo no Azure, não há informações de catálogo (metadados) estão disponíveis em MABS.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-251">Because hello SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span></span> <span data-ttu-id="4b3fd-252">Como resultado, sempre que um banco de dados point-in-time do SharePoint conteúdo precisa toobe recuperado, você precisa farm do SharePoint Olá toocatalog novamente.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-252">As a result, whenever a point-in-time SharePoint content database needs toobe recovered, you need toocatalog hello SharePoint farm again.</span></span>
   >
   >
3. <span data-ttu-id="4b3fd-253">Clique em **Recatalogar**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-253">Click **Re-catalog**.</span></span>

    ![Proteção do SharePoint do MABS 10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    <span data-ttu-id="4b3fd-255">Olá **nuvem recatalogar** status janela será aberta.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-255">hello **Cloud Recatalog** status window opens.</span></span>

    ![Proteção do SharePoint do MABS 11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    <span data-ttu-id="4b3fd-257">Depois de catalogação for concluída, o status de Olá muda muito*sucesso*.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-257">After cataloging is finished, hello status changes too*Success*.</span></span> <span data-ttu-id="4b3fd-258">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="4b3fd-258">Click **Close**.</span></span>

    ![Proteção do SharePoint do MABS 12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="4b3fd-260">Clique Olá SharePoint objeto mostrado no hello MABS **recuperação** guia estrutura de banco de dados de conteúdo de saudação do tooget.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-260">Click hello SharePoint object shown in hello MABS **Recovery** tab tooget hello content database structure.</span></span> <span data-ttu-id="4b3fd-261">Clique no item Olá e clique **recuperar**.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-261">Right-click hello item, and then click **Recover**.</span></span>

    ![Proteção do SharePoint do MABS 13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="4b3fd-263">Neste ponto, execute Olá [recuperação as etapas neste artigo](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover um banco de dados de conteúdo no SharePoint do disco.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-263">At this point, follow hello [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="4b3fd-264">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="4b3fd-264">FAQs</span></span>
<span data-ttu-id="4b3fd-265">P: recuperar o local original do item toohello um SharePoint se o SharePoint é configurado usando o AlwaysOn do SQL (com proteção em disco)?</span><span class="sxs-lookup"><span data-stu-id="4b3fd-265">Q: Can I recover a SharePoint item toohello original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="4b3fd-266">R: Sim, o item de saudação pode ser recuperado toohello original do SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-266">A: Yes, hello item can be recovered toohello original SharePoint site.</span></span>

<span data-ttu-id="4b3fd-267">P: é possível recuperar o local original do banco de dados toohello um SharePoint se o SharePoint é configurado usando o AlwaysOn do SQL?</span><span class="sxs-lookup"><span data-stu-id="4b3fd-267">Q: Can I recover a SharePoint database toohello original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="4b3fd-268">R: como bancos de dados do SharePoint são configurados no SQL AlwaysOn, não pode ser modificados, a menos que o grupo de disponibilidade de saudação é removido.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-268">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless hello availability group is removed.</span></span> <span data-ttu-id="4b3fd-269">Como resultado, MABS não é possível restaurar um local original do banco de dados toohello.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-269">As a result, MABS cannot restore a database toohello original location.</span></span> <span data-ttu-id="4b3fd-270">Você pode recuperar uma instância de SQL Server do tooanother de banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4b3fd-270">You can recover a SQL Server database tooanother SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b3fd-271">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4b3fd-271">Next steps</span></span>
* <span data-ttu-id="4b3fd-272">Saiba mais sobre a Proteção do MABS do SharePoint: veja a [Série de vídeos – Proteção do DPM do SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span><span class="sxs-lookup"><span data-stu-id="4b3fd-272">Learn more about MABS Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>
