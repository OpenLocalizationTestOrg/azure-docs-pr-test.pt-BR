---
title: Usar o servidor de backup do Azure para fazer backup de um farm do SharePoint no Azure | Microsoft Docs
description: "Use o Servidor de Backup do Azure para fazer backup e restaurar seus dados do SharePoint. Este artigo fornece informações para configurar seu farm do SharePoint para que os dados desejados possam ser armazenados no Azure. Você pode restaurar dados protegidos do SharePoint do disco ou do Azure."
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
ms.openlocfilehash: 3ed000affd326eb1bd7c99773ec021ad6e03cc3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-a-sharepoint-farm-to-azure"></a><span data-ttu-id="82e11-105">Fazer backup do farm do SharePoint para o Azure</span><span class="sxs-lookup"><span data-stu-id="82e11-105">Back up a SharePoint farm to Azure</span></span>
<span data-ttu-id="82e11-106">Faça backup de um farm do SharePoint para o Microsoft Azure usando o MABS (Servidor de Backup do Microsoft Azure) da mesma maneira que você faz backup de outras fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="82e11-106">You back up a SharePoint farm to Microsoft Azure by using Microsoft Azure Backup Server (MABS) in much the same way that you back up other data sources.</span></span> <span data-ttu-id="82e11-107">O Backup do Azure fornece flexibilidade no agendamento de backup para criar pontos de backup diariamente, semanalmente, mensalmente ou anualmente e fornece opções de política de retenção para diversos pontos de backup.</span><span class="sxs-lookup"><span data-stu-id="82e11-107">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="82e11-108">Ele também fornece a capacidade de armazenar cópias de disco locais para obter RTOs (Objetivos de Tempo de Recuperação) rápidos e armazenar cópias no Azure para uma retenção econômica e de longo prazo.</span><span class="sxs-lookup"><span data-stu-id="82e11-108">It also provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="82e11-109">Versões do SharePoint com suporte e cenários de proteção relacionados</span><span class="sxs-lookup"><span data-stu-id="82e11-109">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="82e11-110">O Backup do Azure para DPM dá suporte aos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="82e11-110">Azure Backup for DPM supports the following scenarios:</span></span>

| <span data-ttu-id="82e11-111">Carga de trabalho</span><span class="sxs-lookup"><span data-stu-id="82e11-111">Workload</span></span> | <span data-ttu-id="82e11-112">Versão</span><span class="sxs-lookup"><span data-stu-id="82e11-112">Version</span></span> | <span data-ttu-id="82e11-113">Implantação do SharePoint</span><span class="sxs-lookup"><span data-stu-id="82e11-113">SharePoint deployment</span></span> | <span data-ttu-id="82e11-114">Proteção e recuperação</span><span class="sxs-lookup"><span data-stu-id="82e11-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="82e11-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="82e11-115">SharePoint</span></span> |<span data-ttu-id="82e11-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="82e11-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="82e11-117">SharePoint implantado como um servidor físico ou em uma máquina virtual Hyper-V/VMware </span><span class="sxs-lookup"><span data-stu-id="82e11-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="82e11-118">AlwaysOn do SQL</span><span class="sxs-lookup"><span data-stu-id="82e11-118">SQL AlwaysOn</span></span> | <span data-ttu-id="82e11-119">Opções recuperação para proteger o Farm do SharePoint: farm de recuperação, banco de dados e um arquivo ou item de lista dos pontos de recuperação de disco.</span><span class="sxs-lookup"><span data-stu-id="82e11-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="82e11-120">Recuperação do farm e do banco de dados dos pontos de recuperação do Azure.</span><span class="sxs-lookup"><span data-stu-id="82e11-120">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="82e11-121">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="82e11-121">Before you start</span></span>
<span data-ttu-id="82e11-122">Há alguns elementos que você precisa confirmar antes de fazer o backup de um farm do SharePoint para o Azure.</span><span class="sxs-lookup"><span data-stu-id="82e11-122">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="82e11-123">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="82e11-123">Prerequisites</span></span>
<span data-ttu-id="82e11-124">Antes de continuar, certifique-se de ter [instalado e preparado o Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md) para proteger as cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="82e11-124">Before you proceed, make sure that you have [installed and prepared the Azure Backup Server](backup-azure-microsoft-azure-backup.md) to protect workloads.</span></span>

### <a name="protection-agent"></a><span data-ttu-id="82e11-125">Agente de proteção</span><span class="sxs-lookup"><span data-stu-id="82e11-125">Protection agent</span></span>
<span data-ttu-id="82e11-126">O Agente de proteção deve ser instalado no servidor que executa o SharePoint, os servidores que executam o SQL Server e todos os outros servidores que fazem parte do farm do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="82e11-126">The Protection agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span></span> <span data-ttu-id="82e11-127">Para saber m ais sobre como configurar o agente de proteção, confira [Configurar o Agente de Proteção](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span><span class="sxs-lookup"><span data-stu-id="82e11-127">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="82e11-128">A única exceção é que você instala o agente apenas em um único servidor WFE (Front-end da Web).</span><span class="sxs-lookup"><span data-stu-id="82e11-128">The one exception is that you install the agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="82e11-129">O DPM precisa do agente em um servidor WFE apenas para atuar como o ponto de entrada para proteção.</span><span class="sxs-lookup"><span data-stu-id="82e11-129">DPM needs the agent on one WFE server only to serve as the entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="82e11-130">Farm do SharePoint</span><span class="sxs-lookup"><span data-stu-id="82e11-130">SharePoint farm</span></span>
<span data-ttu-id="82e11-131">Para cada 10 milhões de itens no farm, deve haver pelo menos 2 GB de espaço no volume em que a pasta do MABS está localizada.</span><span class="sxs-lookup"><span data-stu-id="82e11-131">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the MABS folder is located.</span></span> <span data-ttu-id="82e11-132">Esse espaço é necessário para a geração de catálogo.</span><span class="sxs-lookup"><span data-stu-id="82e11-132">This space is required for catalog generation.</span></span> <span data-ttu-id="82e11-133">Para o MABS recuperar itens específicos (coleções de sites, sites, listas, bibliotecas de documentos, pastas, documentos individuais e itens de lista), a geração de catálogo cria uma lista das URLs contidas em cada banco de dados de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="82e11-133">For MABS to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span></span> <span data-ttu-id="82e11-134">Você pode exibir a lista de URLs no painel de item recuperável na área de tarefa **Recuperação** do Console do Administrador do MABS.</span><span class="sxs-lookup"><span data-stu-id="82e11-134">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of MABS Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="82e11-135">SQL Server</span><span class="sxs-lookup"><span data-stu-id="82e11-135">SQL Server</span></span>
<span data-ttu-id="82e11-136">O MABS é executado como uma conta LocalSystem.</span><span class="sxs-lookup"><span data-stu-id="82e11-136">MABS runs as a LocalSystem account.</span></span> <span data-ttu-id="82e11-137">Para fazer backup de bancos de dados do SQL Server, o MABS precisa de privilégios sysadmin nessa conta para o servidor que executa o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="82e11-137">To back up SQL Server databases, MABS needs sysadmin privileges on that account for the server that's running SQL Server.</span></span> <span data-ttu-id="82e11-138">Defina NT AUTHORITY\SYSTEM como *sysadmin* no servidor que executa o SQL Server antes de fazer backup dele.</span><span class="sxs-lookup"><span data-stu-id="82e11-138">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="82e11-139">Se o farm do SharePoint tiver bancos de dados do SQL Server configurados com aliases do SQL Server, instale os componentes de cliente do SQL Server no servidor Web front-end que o MABS protegerá.</span><span class="sxs-lookup"><span data-stu-id="82e11-139">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that MABS will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="82e11-140">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="82e11-140">SharePoint Server</span></span>
<span data-ttu-id="82e11-141">Embora o desempenho dependa de muitos fatores tais como o tamanho do farm do SharePoint, as diretrizes gerais são de que um MABS pode ser usado para proteger um farm do SharePoint de 25 TB.</span><span class="sxs-lookup"><span data-stu-id="82e11-141">While performance depends on many factors such as size of SharePoint farm, as general guidance one MABS can protect a 25 TB SharePoint farm.</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="82e11-142">O que não tem suporte</span><span class="sxs-lookup"><span data-stu-id="82e11-142">What's not supported</span></span>
* <span data-ttu-id="82e11-143">O MABS que protege um farm do SharePoint não protege os índices de pesquisa ou os bancos de dados do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="82e11-143">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="82e11-144">Você precisará configurar a proteção desses bancos de dados separadamente.</span><span class="sxs-lookup"><span data-stu-id="82e11-144">You will need to configure the protection of these databases separately.</span></span>
* <span data-ttu-id="82e11-145">O MABS não fornece backup dos bancos de dados do SQL Server do SharePoint hospedados em compartilhamento SOFS (Servidor de Arquivos de Escalabilidade Horizontal).</span><span class="sxs-lookup"><span data-stu-id="82e11-145">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="82e11-146">Configurar a proteção do SharePoint</span><span class="sxs-lookup"><span data-stu-id="82e11-146">Configure SharePoint protection</span></span>
<span data-ttu-id="82e11-147">Para poder usar o MABS para proteger o SharePoint, você deve configurar o serviço de Gravador VSS do SharePoint (serviço de Gravador WSS) usando o **ConfigureSharePoint.exe**.</span><span class="sxs-lookup"><span data-stu-id="82e11-147">Before you can use MABS to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="82e11-148">Você pode encontrar o **ConfigureSharePoint.exe** na pasta [Caminho de instalação do MABS]\bin no servidor Web de front-end.</span><span class="sxs-lookup"><span data-stu-id="82e11-148">You can find **ConfigureSharePoint.exe** in the [MABS Installation Path]\bin folder on the front-end web server.</span></span> <span data-ttu-id="82e11-149">Essa ferramenta fornece o agente de proteção com as credenciais do farm do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="82e11-149">This tool provides the protection agent with the credentials for the SharePoint farm.</span></span> <span data-ttu-id="82e11-150">Você a executa em um único servidor WFE.</span><span class="sxs-lookup"><span data-stu-id="82e11-150">You run it on a single WFE server.</span></span> <span data-ttu-id="82e11-151">Se você tiver vários servidores WFE, selecione apenas um ao configurar um grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="82e11-151">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="to-configure-the-sharepoint-vss-writer-service"></a><span data-ttu-id="82e11-152">Para configurar o serviço de gravador VSS do SharePoint</span><span class="sxs-lookup"><span data-stu-id="82e11-152">To configure the SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="82e11-153">No servidor WFE, em um prompt de comando, vá para [Local de instalação do MABS]\bin\\</span><span class="sxs-lookup"><span data-stu-id="82e11-153">On the WFE server, at a command prompt, go to [MABS installation location]\bin\\</span></span>
2. <span data-ttu-id="82e11-154">Insira ConfigureSharePoint -EnableSharePointProtection.</span><span class="sxs-lookup"><span data-stu-id="82e11-154">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="82e11-155">Insira as credenciais de administrador do farm.</span><span class="sxs-lookup"><span data-stu-id="82e11-155">Enter the farm administrator credentials.</span></span> <span data-ttu-id="82e11-156">Essa conta deve ser um membro do grupo de administradores local no servidor WFE.</span><span class="sxs-lookup"><span data-stu-id="82e11-156">This account should be a member of the local Administrator group on the WFE server.</span></span> <span data-ttu-id="82e11-157">Se o administrador do farm não for um administrador local, conceda as seguintes permissões no servidor WFE:</span><span class="sxs-lookup"><span data-stu-id="82e11-157">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span></span>
   * <span data-ttu-id="82e11-158">Conceda o controle total do grupo WSS_Admin_WPG para a pasta do DPM (%Arquivos de Programas%\Microsoft Azure Backup\DPM).</span><span class="sxs-lookup"><span data-stu-id="82e11-158">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span></span>
   * <span data-ttu-id="82e11-159">Conceda acesso de leitura do grupo WSS_Admin_WPG à chave do Registro do DPM (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span><span class="sxs-lookup"><span data-stu-id="82e11-159">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="82e11-160">Você precisará executar novamente o ConfigureSharePoint.exe sempre que houver uma alteração nas credenciais de administrador de farm do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="82e11-160">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span></span>
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a><span data-ttu-id="82e11-161">Fazer backup de um farm do SharePoint usando o MABS</span><span class="sxs-lookup"><span data-stu-id="82e11-161">Back up a SharePoint farm by using MABS</span></span>
<span data-ttu-id="82e11-162">Depois de configurar o MABS e o farm do SharePoint conforme explicado anteriormente, o SharePoint pode ser protegido pelo MABS.</span><span class="sxs-lookup"><span data-stu-id="82e11-162">After you have configured MABS and the SharePoint farm as explained previously, SharePoint can be protected by MABS.</span></span>

### <a name="to-protect-a-sharepoint-farm"></a><span data-ttu-id="82e11-163">Para proteger um farm do SharePoint</span><span class="sxs-lookup"><span data-stu-id="82e11-163">To protect a SharePoint farm</span></span>
1. <span data-ttu-id="82e11-164">Na guia **Proteção** do Console do Administrador do MABS clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="82e11-164">From the **Protection** tab of the MABS Administrator Console, click **New**.</span></span>
    <span data-ttu-id="82e11-165">![Guia Nova Proteção](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="82e11-165">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="82e11-166">Na página **Selecionar Tipo do Grupo de Proteção** do assistente **Criar Novo Grupo de Proteção**, selecione **Servidores** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-166">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>

    ![Selecionar o tipo de Grupo de Proteção](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="82e11-168">Na tela **Selecionar Membros do Grupo**, marque a caixa de seleção do servidor do SharePoint que deseja proteger e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-168">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span></span>

    ![Selecionar membros do grupo](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > <span data-ttu-id="82e11-170">Com o agente de proteção instalado, você pode ver o servidor no assistente.</span><span class="sxs-lookup"><span data-stu-id="82e11-170">With the protection agent installed, you can see the server in the wizard.</span></span> <span data-ttu-id="82e11-171">O MABS também mostra sua estrutura.</span><span class="sxs-lookup"><span data-stu-id="82e11-171">MABS also shows its structure.</span></span> <span data-ttu-id="82e11-172">Como você executou o ConfigureSharePoint.exe, o MABS se comunica com o serviço do Gravador VSS do SharePoint e seus bancos de dados do SQL Server correspondentes e reconhece a estrutura de farm do SharePoint, os bancos de dados de conteúdo associados e todos os itens correspondentes.</span><span class="sxs-lookup"><span data-stu-id="82e11-172">Because you ran ConfigureSharePoint.exe, MABS communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span></span>
   >
   >
4. <span data-ttu-id="82e11-173">Na página **Selecionar Método de Proteção de Dados**, insira o nome do **Grupo de Proteção** e selecione seus *métodos de proteção* preferenciais.</span><span class="sxs-lookup"><span data-stu-id="82e11-173">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="82e11-174">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-174">Click **Next**.</span></span>

    ![Selecionar método de proteção de dados](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > <span data-ttu-id="82e11-176">O método de proteção de disco ajuda a atender os objetivos de tempo de recuperação breves.</span><span class="sxs-lookup"><span data-stu-id="82e11-176">The disk protection method helps to meet short recovery-time objectives.</span></span>
   >
   >
5. <span data-ttu-id="82e11-177">Na tela **Especificar Objetivos de Curto Prazo**, selecione seu **Período de retenção** preferencial e identifique quando você deseja que os backups ocorram.</span><span class="sxs-lookup"><span data-stu-id="82e11-177">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span></span>

    ![Especificar objetivos de curto prazo](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > <span data-ttu-id="82e11-179">Como a recuperação é necessária mais frequentemente para dados com menos de cinco dias, selecionamos um período de retenção de cinco dias no disco e garantimos que o backup ocorra fora dos horários de produção para esse exemplo.</span><span class="sxs-lookup"><span data-stu-id="82e11-179">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span></span>
   >
   >
6. <span data-ttu-id="82e11-180">Examine o espaço em disco do pool de armazenamento alocado para o grupo de proteção e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-180">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="82e11-181">Para cada grupo de proteção, o MABS aloca espaço em disco para armazenar e gerenciar réplicas.</span><span class="sxs-lookup"><span data-stu-id="82e11-181">For every protection group, MABS allocates disk space to store and manage replicas.</span></span> <span data-ttu-id="82e11-182">Neste ponto, o MABS deve criar uma cópia dos dados selecionados.</span><span class="sxs-lookup"><span data-stu-id="82e11-182">At this point, MABS must create a copy of the selected data.</span></span> <span data-ttu-id="82e11-183">Selecione como e quando você deseja que a réplica seja criada e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-183">Select how and when you want the replica created, and then click **Next**.</span></span>

    ![Escolher método de criação de réplica](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > <span data-ttu-id="82e11-185">Para garantir que o tráfego de rede não seja afetado, selecione um horário fora do horário de produção.</span><span class="sxs-lookup"><span data-stu-id="82e11-185">To make sure that network traffic is not effected, select a time outside production hours.</span></span>
   >
   >
8. <span data-ttu-id="82e11-186">O MABS assegura a integridade de dados executando verificações de consistência na réplica.</span><span class="sxs-lookup"><span data-stu-id="82e11-186">MABS ensures data integrity by performing consistency checks on the replica.</span></span> <span data-ttu-id="82e11-187">Há duas opções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="82e11-187">There are two available options.</span></span> <span data-ttu-id="82e11-188">Você pode definir um agendamento para executar verificações de consistência ou o DPM pode executar as verificações de consistência automaticamente na réplica sempre que ela ficar inconsistente.</span><span class="sxs-lookup"><span data-stu-id="82e11-188">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="82e11-189">Selecione sua opção desejada e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-189">Select your preferred option, and then click **Next**.</span></span>

    ![Verificação de consistência](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="82e11-191">Na página **Especificar Dados da Proteção Online**, selecione o farm do SharePoint que você deseja proteger e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-191">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span></span>

    ![Proteção do SharePoint do DPM1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="82e11-193">Na página **Especificar o Agendamento do Backup Online**, selecione seu agendamento desejado e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-193">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="82e11-195">O MABS fornece um máximo de dois backups diários para o Azure do ponto de backup de disco mais recente disponível nesses momentos.</span><span class="sxs-lookup"><span data-stu-id="82e11-195">MABS provides a maximum of two daily backups to Azure from the then available latest disk backup point.</span></span> <span data-ttu-id="82e11-196">O Backup do Azure também pode controlar o volume de largura de banda WAN que pode ser usada para backups em horário de pico e fora dos horários de pico usando a [Limitação de Rede do Backup do Azure](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span><span class="sxs-lookup"><span data-stu-id="82e11-196">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    >
    >
11. <span data-ttu-id="82e11-197">Dependendo do agendamento de backup selecionado, na página **Especificar Política de Retenção Online** , selecione a política de retenção para pontos de backup diários, semanais, mensais e anuais.</span><span class="sxs-lookup"><span data-stu-id="82e11-197">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span></span>

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > <span data-ttu-id="82e11-199">O MABS usa um esquema de retenção de avô-pai-filho em que uma política de retenção diferente pode ser escolhida para pontos de backup distintos.</span><span class="sxs-lookup"><span data-stu-id="82e11-199">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    >
    >
12. <span data-ttu-id="82e11-200">Semelhante ao disco, uma réplica do ponto de referência inicial precisa ser criado no Azure.</span><span class="sxs-lookup"><span data-stu-id="82e11-200">Similar to disk, an initial reference point replica needs to be created in Azure.</span></span> <span data-ttu-id="82e11-201">Selecione sua opção desejada para criar uma cópia de backup inicial no Azure e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-201">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span></span>

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="82e11-203">Examine as configurações selecionadas na página **Resumo** e clique em **Criar Grupo**.</span><span class="sxs-lookup"><span data-stu-id="82e11-203">Review your selected settings on the **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="82e11-204">Você verá uma mensagem de êxito depois do grupo de proteção ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="82e11-204">You will see a success message after the protection group has been created.</span></span>

    ![Resumo](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a><span data-ttu-id="82e11-206">Restaurar um item do SharePoint do disco usando o MABS</span><span class="sxs-lookup"><span data-stu-id="82e11-206">Restore a SharePoint item from disk by using MABS</span></span>
<span data-ttu-id="82e11-207">No exemplo a seguir, o *item Recuperando SharePoint* foi excluído acidentalmente e precisa ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="82e11-207">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span></span>
<span data-ttu-id="82e11-208">![Proteção do SharePoint do MABS 4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="82e11-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="82e11-209">Abra o **Console do Administrador do DPM**.</span><span class="sxs-lookup"><span data-stu-id="82e11-209">Open the **DPM Administrator Console**.</span></span> <span data-ttu-id="82e11-210">Todos os farms do SharePoint protegidos pelo DPM são mostrados na guia **Proteção** .</span><span class="sxs-lookup"><span data-stu-id="82e11-210">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span></span>

    ![Proteção do SharePoint do MABS 3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="82e11-212">Para começar a recuperar o item, selecione a guia **Recuperação** .</span><span class="sxs-lookup"><span data-stu-id="82e11-212">To begin to recover the item, select the **Recovery** tab.</span></span>

    ![Proteção do SharePoint do MABS 5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="82e11-214">É possível pesquisar no SharePoint para localizar o *item Recuperando SharePoint* usando uma pesquisa baseada em curinga dentro de um intervalo de ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="82e11-214">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>

    ![Proteção do SharePoint do MABS 6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="82e11-216">Selecione o ponto de recuperação apropriado dentre os resultados da pesquisa, clique com o botão direito do mouse no item e selecione **Recuperar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-216">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span></span>
5. <span data-ttu-id="82e11-217">Você também pode navegar pelos diversos pontos de recuperação e selecionar um banco de dados ou item para recuperar.</span><span class="sxs-lookup"><span data-stu-id="82e11-217">You can also browse through various recovery points and select a database or item to recover.</span></span> <span data-ttu-id="82e11-218">Selecione **Data > Hora da recuperação** e escolha o **Banco de Dados > Farm do SharePoint > Ponto de recuperação > Item** correto.</span><span class="sxs-lookup"><span data-stu-id="82e11-218">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span></span>

    ![Proteção do SharePoint do MABS 7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="82e11-220">Clique com o botão direito do mouse no item e selecione **Recuperar** para abrir o **Assistente de Recuperação**.</span><span class="sxs-lookup"><span data-stu-id="82e11-220">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span></span> <span data-ttu-id="82e11-221">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-221">Click **Next**.</span></span>

    ![Rever Seleção de Recuperação](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="82e11-223">Selecione o tipo de recuperação que você deseja executar e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-223">Select the type of recovery that you want to perform, and then click **Next**.</span></span>

    ![Tipo de Recuperação](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > <span data-ttu-id="82e11-225">A seleção de **Recuperar para o original** no exemplo recupera o item para o site do SharePoint original.</span><span class="sxs-lookup"><span data-stu-id="82e11-225">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span></span>
   >
   >
8. <span data-ttu-id="82e11-226">Selecione o **Processo de Recuperação** que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="82e11-226">Select the **Recovery Process** that you want to use.</span></span>

   * <span data-ttu-id="82e11-227">Selecione **Recuperar sem usar um farm de recuperação** se o farm do SharePoint não tiver sido alterado e for o mesmo que o ponto de recuperação que está sendo restaurado.</span><span class="sxs-lookup"><span data-stu-id="82e11-227">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span></span>
   * <span data-ttu-id="82e11-228">Selecione **Recuperar usando um farm de recuperação** se o farm do SharePoint tiver sido alterado desde que o ponto de recuperação foi criado.</span><span class="sxs-lookup"><span data-stu-id="82e11-228">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span></span>

     ![Processo de Recuperação](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="82e11-230">Forneça um local de preparo da instância do SQL Server para recuperar o banco de dados temporariamente e fornecer um compartilhamento de arquivos de preparo no MABS e no servidor que executa o SharePoint a fim de recuperar o item.</span><span class="sxs-lookup"><span data-stu-id="82e11-230">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on MABS and the server that's running SharePoint to recover the item.</span></span>

    ![Local de Preparo1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    <span data-ttu-id="82e11-232">O MABS anexa o banco de dados de conteúdo que está hospedando o item do SharePoint à instância temporária do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="82e11-232">MABS attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span></span> <span data-ttu-id="82e11-233">Do banco de dados de conteúdo, ele recupera o item e o coloca no local do arquivo de preparo no MABS.</span><span class="sxs-lookup"><span data-stu-id="82e11-233">From the content database, it recovers the item and puts it on the staging file location on MABS.</span></span> <span data-ttu-id="82e11-234">O item recuperado no local de preparo agora precisa ser exportado para o local de preparo no farm do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="82e11-234">The recovered item that's on the staging location now needs to be exported to the staging location on the SharePoint farm.</span></span>

    ![Local de Preparo2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="82e11-236">Selecione **Especificar opções de recuperação**e aplique as configurações de segurança ao farm do SharePoint ou aplique as configurações de segurança do ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="82e11-236">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span></span> <span data-ttu-id="82e11-237">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-237">Click **Next**.</span></span>

    ![Opções de Recuperação](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > <span data-ttu-id="82e11-239">Você pode optar por limitar o uso de largura de banda da rede.</span><span class="sxs-lookup"><span data-stu-id="82e11-239">You can choose to throttle the network bandwidth usage.</span></span> <span data-ttu-id="82e11-240">Isso minimiza o impacto no servidor de produção durante o horário de produção.</span><span class="sxs-lookup"><span data-stu-id="82e11-240">This minimizes impact to the production server during production hours.</span></span>
    >
    >
11. <span data-ttu-id="82e11-241">Examine as informações de resumo e clique em **Recuperar** para iniciar a recuperação do arquivo.</span><span class="sxs-lookup"><span data-stu-id="82e11-241">Review the summary information, and then click **Recover** to begin recovery of the file.</span></span>

    ![Resumo da recuperação](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="82e11-243">Agora selecione a guia **Monitoramento** no **Console do Administrador do MABS** para exibir o **Status** da recuperação.</span><span class="sxs-lookup"><span data-stu-id="82e11-243">Now select the **Monitoring** tab in the **MABS Administrator Console** to view the **Status** of the recovery.</span></span>

    ![Status da Recuperação](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > <span data-ttu-id="82e11-245">Agora o arquivo está restaurado.</span><span class="sxs-lookup"><span data-stu-id="82e11-245">The file is now restored.</span></span> <span data-ttu-id="82e11-246">Você pode atualizar o site do SharePoint para verificar o arquivo restaurado.</span><span class="sxs-lookup"><span data-stu-id="82e11-246">You can refresh the SharePoint site to check the restored file.</span></span>
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="82e11-247">Restaurar um banco de dados do SharePoint do Azure usando o DPM</span><span class="sxs-lookup"><span data-stu-id="82e11-247">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="82e11-248">Para recuperar um banco de dados de conteúdo do SharePoint, navegue pelos vários pontos de recuperação (conforme mostrado acima) e selecione o ponto de recuperação que você deseja recuperar.</span><span class="sxs-lookup"><span data-stu-id="82e11-248">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span></span>

    ![Proteção do SharePoint do MABS 8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="82e11-250">Clique duas vezes no ponto de recuperação do SharePoint para mostrar as informações de catálogo do SharePoint disponíveis.</span><span class="sxs-lookup"><span data-stu-id="82e11-250">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="82e11-251">Como o farm do SharePoint está protegido para retenção de longo prazo no Azure, não há nenhuma informação de catálogo (metadados) disponível no MABS.</span><span class="sxs-lookup"><span data-stu-id="82e11-251">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span></span> <span data-ttu-id="82e11-252">Desta forma, sempre que um banco de dados de conteúdo do SharePoint pontual precisar ser recuperado, será necessário recatalogar o farm do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="82e11-252">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span></span>
   >
   >
3. <span data-ttu-id="82e11-253">Clique em **Recatalogar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-253">Click **Re-catalog**.</span></span>

    ![Proteção do SharePoint do MABS 10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    <span data-ttu-id="82e11-255">A janela de status **Recatalogação de Nuvem** é exibida.</span><span class="sxs-lookup"><span data-stu-id="82e11-255">The **Cloud Recatalog** status window opens.</span></span>

    ![Proteção do SharePoint do MABS 11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    <span data-ttu-id="82e11-257">Após a catalogação ser concluída, o status é alterado para *Êxito*.</span><span class="sxs-lookup"><span data-stu-id="82e11-257">After cataloging is finished, the status changes to *Success*.</span></span> <span data-ttu-id="82e11-258">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="82e11-258">Click **Close**.</span></span>

    ![Proteção do SharePoint do MABS 12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="82e11-260">Clique no objeto do SharePoint mostrado na guia **Recuperação** do MABS para obter a estrutura do banco de dados de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="82e11-260">Click the SharePoint object shown in the MABS **Recovery** tab to get the content database structure.</span></span> <span data-ttu-id="82e11-261">Clique com o botão direito do mouse no item apropriado e em **Recuperar**.</span><span class="sxs-lookup"><span data-stu-id="82e11-261">Right-click the item, and then click **Recover**.</span></span>

    ![Proteção do SharePoint do MABS 13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="82e11-263">Nesse ponto, siga as [etapas de recuperação descritas anteriormente neste artigo](#restore-a-sharepoint-item-from-disk-using-dpm) para recuperar um banco de dados de conteúdo do SharePoint do disco.</span><span class="sxs-lookup"><span data-stu-id="82e11-263">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="82e11-264">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="82e11-264">FAQs</span></span>
<span data-ttu-id="82e11-265">P: Posso recuperar um item do SharePoint para o local original se o SharePoint foi configurado usando o SQL AlwaysOn (com proteção em disco)?</span><span class="sxs-lookup"><span data-stu-id="82e11-265">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="82e11-266">R: Sim, o item pode ser recuperado para o site do SharePoint original.</span><span class="sxs-lookup"><span data-stu-id="82e11-266">A: Yes, the item can be recovered to the original SharePoint site.</span></span>

<span data-ttu-id="82e11-267">P: Posso recuperar um banco de dados do SharePoint no local original se o SharePoint estiver configurado usando o AlwaysOn do SQL?</span><span class="sxs-lookup"><span data-stu-id="82e11-267">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="82e11-268">R: Como os bancos de dados do SharePoint são configurados no SQL AlwaysOn, eles não podem ser modificados a menos que o grupo de disponibilidade seja removido.</span><span class="sxs-lookup"><span data-stu-id="82e11-268">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span></span> <span data-ttu-id="82e11-269">Por isso, o MABS não pode restaurar o banco de dados para o local original.</span><span class="sxs-lookup"><span data-stu-id="82e11-269">As a result, MABS cannot restore a database to the original location.</span></span> <span data-ttu-id="82e11-270">Não é possível recuperar um banco de dados do SQL Server para outra instância do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="82e11-270">You can recover a SQL Server database to another SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82e11-271">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="82e11-271">Next steps</span></span>
* <span data-ttu-id="82e11-272">Saiba mais sobre a Proteção do MABS do SharePoint: veja a [Série de vídeos – Proteção do DPM do SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span><span class="sxs-lookup"><span data-stu-id="82e11-272">Learn more about MABS Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>
