---
title: Fazer backup de um servidor do Exchange no Backup do Azure com o System Center 2012 R2 DPM | Microsoft Docs
description: Saiba como fazer backup de um servidor do Exchange no Backup do Azure usando o System Center 2012 R2 DPM
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: 2a0e416440e55cfde70cbd20d40c99fb29b4229c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="1b833-103">Fazer backup de um servidor do Exchange no Backup do Azure com o System Center 2012 R2 DPM</span><span class="sxs-lookup"><span data-stu-id="1b833-103">Back up an Exchange server to Azure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="1b833-104">Este artigo descreve como configurar um servidor do System Center 2012 R2 DPM (Data Protection Manager) para fazer backup de um servidor do Microsoft Exchange no Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b833-104">This article describes how to configure a System Center 2012 R2 Data Protection Manager (DPM) server to back up a Microsoft Exchange server to  Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="1b833-105">Atualizações</span><span class="sxs-lookup"><span data-stu-id="1b833-105">Updates</span></span>
<span data-ttu-id="1b833-106">Para registrar o servidor DPM no Backup do Azure, você deve instalar o pacote cumulativo de atualizações mais recente do System Center 2012 R2 DPM e a versão mais recente do Agente de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b833-106">To successfully register the DPM server with Azure Backup, you must install the latest update rollup for System Center 2012 R2 DPM and the latest version of the Azure Backup Agent.</span></span> <span data-ttu-id="1b833-107">Obtenha o pacote cumulativo de atualizações mais recente no [Catálogo da Microsoft](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="1b833-107">Get the latest update rollup from the [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="1b833-108">Para os exemplos neste artigo, a versão 2.0.8719.0 do Agente de Backup do Azure está instalada, e Atualização Cumulativa 6 está instalada no System Center 2012 R2 DPM.</span><span class="sxs-lookup"><span data-stu-id="1b833-108">For the examples in this article, version 2.0.8719.0 of the Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="1b833-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1b833-109">Prerequisites</span></span>
<span data-ttu-id="1b833-110">Antes de continuar, verifique se todos os [pré-requisitos](backup-azure-dpm-introduction.md#prerequisites) para uso do Backup do Microsoft Azure como proteção às cargas de trabalho foram atendidos.</span><span class="sxs-lookup"><span data-stu-id="1b833-110">Before you continue, make sure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span></span> <span data-ttu-id="1b833-111">Esses pré-requisitos incluem os seguintes:</span><span class="sxs-lookup"><span data-stu-id="1b833-111">These prerequisites include the following:</span></span>

* <span data-ttu-id="1b833-112">Criação de um cofre de backup no site do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b833-112">A backup vault on the Azure site has been created.</span></span>
* <span data-ttu-id="1b833-113">Download das credenciais do agente e do cofre no servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="1b833-113">Agent and vault credentials have been downloaded to the DPM server.</span></span>
* <span data-ttu-id="1b833-114">Instalação do agente no servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="1b833-114">The agent is installed on the DPM server.</span></span>
* <span data-ttu-id="1b833-115">Uso das credenciais do cofre para registro no servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="1b833-115">The vault credentials were used to register the DPM server.</span></span>
* <span data-ttu-id="1b833-116">Se você estiver protegendo o Exchange 2016, atualize para o DPM 2012 R2 UR9 ou posterior</span><span class="sxs-lookup"><span data-stu-id="1b833-116">If you are protecting Exchange 2016, please upgrade to DPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="1b833-117">Agente de proteção do DPM</span><span class="sxs-lookup"><span data-stu-id="1b833-117">DPM protection agent</span></span>
<span data-ttu-id="1b833-118">Execute estas etapas para instalar o agente de proteção do DPM no servidor do Exchange:</span><span class="sxs-lookup"><span data-stu-id="1b833-118">To install the DPM protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="1b833-119">Verifique se os firewalls estão configurados corretamente.</span><span class="sxs-lookup"><span data-stu-id="1b833-119">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="1b833-120">Confira [Configurar exceções de firewall do agente](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b833-120">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="1b833-121">Instale o agente no servidor do Exchange clicando em **Gerenciamento > Agentes > Instalar** no Console do Administrador do DPM.</span><span class="sxs-lookup"><span data-stu-id="1b833-121">Install the agent on the Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="1b833-122">Confira [Instalar o agente de proteção do DPM](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) para conhecer as etapas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="1b833-122">See [Install the DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="1b833-123">Criar um grupo de proteção do Exchange server</span><span class="sxs-lookup"><span data-stu-id="1b833-123">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="1b833-124">No Console do Administrador do DPM, clique em **Proteção** e, em seguida, clique em **Novo** na faixa de opções de ferramenta para abrir o assistente **Criar Novo Grupo de Proteção**.</span><span class="sxs-lookup"><span data-stu-id="1b833-124">In the DPM Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="1b833-125">Na tela de **Boas-vindas** do assistente, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="1b833-125">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="1b833-126">Na tela **Selecionar tipo do grupo de proteção**, escolha **Servidores** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="1b833-126">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="1b833-127">Escolha o banco de dados do servidor do Exchange que você quer proteger e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="1b833-127">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1b833-128">Se você estiver protegendo o Exchange 2013, verifique os [pré-requisitos do Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b833-128">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="1b833-129">No exemplo abaixo, o banco de dados do Exchange 2010 foi selecionado.</span><span class="sxs-lookup"><span data-stu-id="1b833-129">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Selecionar membros do grupo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="1b833-131">Selecione o método de proteção de dados.</span><span class="sxs-lookup"><span data-stu-id="1b833-131">Select the data protection method.</span></span>

    <span data-ttu-id="1b833-132">Dê um nome ao grupo de proteção e escolha as duas opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b833-132">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="1b833-133">Desejo a proteção de curto prazo usando Disco.</span><span class="sxs-lookup"><span data-stu-id="1b833-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="1b833-134">Desejo a proteção online.</span><span class="sxs-lookup"><span data-stu-id="1b833-134">I want online protection.</span></span>
6. <span data-ttu-id="1b833-135">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="1b833-135">Click **Next**.</span></span>
7. <span data-ttu-id="1b833-136">Escolha a opção **Executar Eseutil para verificar a integridade dos dados** se você quiser verificar a integridade dos bancos de dados do Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="1b833-136">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="1b833-137">Depois de escolher essa opção, a verificação de consistência do backup será executada no servidor DPM a fim de evitar o tráfego de E/S gerado pela execução do comando **eseutil** no servidor Exchange.</span><span class="sxs-lookup"><span data-stu-id="1b833-137">After you select this option, backup consistency checking will be run on the DPM server to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1b833-138">Para usar essa opção, você deve copiar os arquivos Ese.dll e Eseutil.exe no diretório C:\Arquivos de Programas\Microsoft System Center 2012 R2\DPM\DPM\bin no servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="1b833-138">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on the DPM server.</span></span> <span data-ttu-id="1b833-139">Caso contrário, o seguinte erro será disparado: </span><span class="sxs-lookup"><span data-stu-id="1b833-139">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="1b833-140">![erro de eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="1b833-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="1b833-141">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="1b833-141">Click **Next**.</span></span>
9. <span data-ttu-id="1b833-142">Escolha o banco de dados para **Copiar o Backup** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="1b833-142">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1b833-143">Se você não escolher "Backup completo" para pelo menos uma cópia de DAG de um banco de dados, os registros não ficarão truncados.</span><span class="sxs-lookup"><span data-stu-id="1b833-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="1b833-144">Configure as metas de **Backup de Curto Prazo** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="1b833-144">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="1b833-145">Confira o espaço em disco disponível e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="1b833-145">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="1b833-146">Escolha a hora na qual o servidor DPM criará a replicação inicial e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="1b833-146">Select the time at which the DPM server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="1b833-147">Escolha as opções de verificação de consistência e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="1b833-147">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="1b833-148">Escolha o banco de dados do qual você deseja fazer backup no Azure e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="1b833-148">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="1b833-149">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1b833-149">For example:</span></span>

    ![Especificar dados de proteção online](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="1b833-151">Defina o cronograma do **Backup do Azure** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="1b833-151">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="1b833-152">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1b833-152">For example:</span></span>

    ![Especifique o cronograma do backup online](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="1b833-154">Observe que os Pontos de recuperação online têm base nos pontos de recuperação completos expressos.</span><span class="sxs-lookup"><span data-stu-id="1b833-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="1b833-155">Portanto, você deve agendar o ponto de recuperação online após o período especificado para o ponto de recuperação completo expresso.</span><span class="sxs-lookup"><span data-stu-id="1b833-155">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="1b833-156">Configure a política de retenção para o **Backup do Azure** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="1b833-156">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="1b833-157">Escolha uma opção de replicação online e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="1b833-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="1b833-158">Se você tiver um banco de dados de grande porte, talvez a criação do backup inicial na rede demore bastante.</span><span class="sxs-lookup"><span data-stu-id="1b833-158">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="1b833-159">Para evitar esse problema, crie um backup offline.</span><span class="sxs-lookup"><span data-stu-id="1b833-159">To avoid this issue, you can create an offline backup.</span></span>  

    ![Especificar política de retenção online](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="1b833-161">Confirme as configurações e clique em **Criar Grupo**.</span><span class="sxs-lookup"><span data-stu-id="1b833-161">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="1b833-162">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="1b833-162">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="1b833-163">Recuperar o banco de dados do Exchange</span><span class="sxs-lookup"><span data-stu-id="1b833-163">Recover the Exchange database</span></span>
1. <span data-ttu-id="1b833-164">Para recuperar um banco de dados do Exchange, clique em **Recuperação** no Console do Administrador do DPM.</span><span class="sxs-lookup"><span data-stu-id="1b833-164">To recover an Exchange database, click **Recovery** in the DPM Administrator Console.</span></span>
2. <span data-ttu-id="1b833-165">Localize o banco de dados do Exchange que você deseja recuperar.</span><span class="sxs-lookup"><span data-stu-id="1b833-165">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="1b833-166">Selecione um ponto de recuperação online na lista suspensa *tempo de recuperação* .</span><span class="sxs-lookup"><span data-stu-id="1b833-166">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="1b833-167">Clique em **Recuperar** para iniciar o **Assistente de Recuperação**.</span><span class="sxs-lookup"><span data-stu-id="1b833-167">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="1b833-168">Há cinco tipos de recuperação para os pontos de recuperação online:</span><span class="sxs-lookup"><span data-stu-id="1b833-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="1b833-169">**Recuperar no local original do Exchange Server:** os dados serão recuperados no servidor original do Exchange.</span><span class="sxs-lookup"><span data-stu-id="1b833-169">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="1b833-170">**Recuperar em outro banco de dados em um servidor do Exchange:** os dados serão recuperados em outro banco de dados, em outro servidor do Exchange.</span><span class="sxs-lookup"><span data-stu-id="1b833-170">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="1b833-171">**Recuperar um Banco de Dados de Recuperação:** os dados serão recuperados em um RDB (Banco de Dados de Recuperação do Exchange).</span><span class="sxs-lookup"><span data-stu-id="1b833-171">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="1b833-172">**Copiar em uma pasta de rede:** os dados serão recuperados em uma pasta de rede.</span><span class="sxs-lookup"><span data-stu-id="1b833-172">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="1b833-173">**Cópia em fita:** se você tiver uma biblioteca de fitas ou uma unidade de fita autônoma conectada e configurada no servidor DPM, o ponto de recuperação será copiado em uma fita livre.</span><span class="sxs-lookup"><span data-stu-id="1b833-173">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on the DPM server, the recovery point will be copied to a free tape.</span></span>

    ![Escolher a replicação online](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="1b833-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1b833-175">Next steps</span></span>
* [<span data-ttu-id="1b833-176">Backup do Azure - Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="1b833-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
