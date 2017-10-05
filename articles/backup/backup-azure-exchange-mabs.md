---
title: Fazer backup de um servidor do Exchange no Backup do Azure com o Servidor de Backup do Azure | Microsoft Docs
description: Saiba como fazer backup de um servidor do Exchange no Backup do Azure usando o Servidor de Backup do Azure
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 60b784fd00013c2b9504f8635c6b5c4c592563be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-azure-backup-server"></a><span data-ttu-id="a0df8-103">Fazer backup de um servidor do Exchange no Backup do Azure com o Servidor de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="a0df8-103">Back up an Exchange server to Azure Backup with Azure Backup Server</span></span>
<span data-ttu-id="a0df8-104">Este artigo descreve como configurar o Servidor de Backup do Microsoft Azure (MABS) para fazer backup de um servidor do Microsoft Exchange no Azure.</span><span class="sxs-lookup"><span data-stu-id="a0df8-104">This article describes how to configure Microsoft Azure Backup Server (MABS) to back up a Microsoft Exchange server to Azure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="a0df8-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a0df8-105">Prerequisites</span></span>
<span data-ttu-id="a0df8-106">Antes de continuar, verifique se o Servidor de Backup do Azure está [instalado e preparado](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="a0df8-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="a0df8-107">Agente de proteção do MABS</span><span class="sxs-lookup"><span data-stu-id="a0df8-107">MABS protection agent</span></span>
<span data-ttu-id="a0df8-108">Execute estas etapas para instalar o agente de proteção do MABS no servidor do Exchange:</span><span class="sxs-lookup"><span data-stu-id="a0df8-108">To install the MABS protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="a0df8-109">Verifique se os firewalls estão configurados corretamente.</span><span class="sxs-lookup"><span data-stu-id="a0df8-109">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="a0df8-110">Confira [Configurar exceções de firewall do agente](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0df8-110">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="a0df8-111">Instale o agente no servidor do Exchange clicando em **Gerenciamento > Agentes > Instalar** no Console do Administrador do MABS.</span><span class="sxs-lookup"><span data-stu-id="a0df8-111">Install the agent on the Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="a0df8-112">Confira [Instalar o agente de proteção do MABS](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) para conhecer as etapas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="a0df8-112">See [Install the MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="a0df8-113">Criar um grupo de proteção do Exchange server</span><span class="sxs-lookup"><span data-stu-id="a0df8-113">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="a0df8-114">No Console do Administrador do MABS, clique em **Proteção** e, em seguida, clique em **Novo** na faixa de opções de ferramenta para abrir o assistente **Criar Novo Grupo de Proteção**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-114">In the MABS Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="a0df8-115">Na tela de **Boas-vindas** do assistente, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-115">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="a0df8-116">Na tela **Selecionar tipo do grupo de proteção**, escolha **Servidores** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-116">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="a0df8-117">Escolha o banco de dados do servidor do Exchange que você quer proteger e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-117">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a0df8-118">Se você estiver protegendo o Exchange 2013, verifique os [pré-requisitos do Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0df8-118">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="a0df8-119">No exemplo abaixo, o banco de dados do Exchange 2010 foi selecionado.</span><span class="sxs-lookup"><span data-stu-id="a0df8-119">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Selecionar membros do grupo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="a0df8-121">Selecione o método de proteção de dados.</span><span class="sxs-lookup"><span data-stu-id="a0df8-121">Select the data protection method.</span></span>

    <span data-ttu-id="a0df8-122">Dê um nome ao grupo de proteção e escolha as duas opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0df8-122">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="a0df8-123">Desejo a proteção de curto prazo usando Disco.</span><span class="sxs-lookup"><span data-stu-id="a0df8-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="a0df8-124">Desejo a proteção online.</span><span class="sxs-lookup"><span data-stu-id="a0df8-124">I want online protection.</span></span>
6. <span data-ttu-id="a0df8-125">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-125">Click **Next**.</span></span>
7. <span data-ttu-id="a0df8-126">Escolha a opção **Executar Eseutil para verificar a integridade dos dados** se você quiser verificar a integridade dos bancos de dados do Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="a0df8-126">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="a0df8-127">Depois de escolher essa opção, a verificação de consistência do backup será executada no MABS a fim de evitar o tráfego de E/S gerado pela execução do comando **eseutil** no servidor Exchange.</span><span class="sxs-lookup"><span data-stu-id="a0df8-127">After you select this option, backup consistency checking will be run on MABS to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a0df8-128">Para usar essa opção, você deve copiar os arquivos Ese.dll e Eseutil.exe no diretório C:\Arquivos de Programas\Backup do Microsoft Azure\DPM\DPM\bin no servidor MAB.</span><span class="sxs-lookup"><span data-stu-id="a0df8-128">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on the MAB server.</span></span> <span data-ttu-id="a0df8-129">Caso contrário, o seguinte erro será disparado: </span><span class="sxs-lookup"><span data-stu-id="a0df8-129">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="a0df8-130">![erro de eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="a0df8-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="a0df8-131">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-131">Click **Next**.</span></span>
9. <span data-ttu-id="a0df8-132">Escolha o banco de dados para **Copiar o Backup** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-132">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a0df8-133">Se você não escolher "Backup completo" para pelo menos uma cópia de DAG de um banco de dados, os registros não ficarão truncados.</span><span class="sxs-lookup"><span data-stu-id="a0df8-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="a0df8-134">Configure as metas de **Backup de Curto Prazo** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-134">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="a0df8-135">Confira o espaço em disco disponível e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-135">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="a0df8-136">Escolha a hora na qual o servidor MAB criará a replicação inicial e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-136">Select the time at which the MAB Server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="a0df8-137">Escolha as opções de verificação de consistência e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-137">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="a0df8-138">Escolha o banco de dados do qual você deseja fazer backup no Azure e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-138">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="a0df8-139">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a0df8-139">For example:</span></span>

    ![Especificar dados de proteção online](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="a0df8-141">Defina o cronograma do **Backup do Azure** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-141">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="a0df8-142">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a0df8-142">For example:</span></span>

    ![Especifique o cronograma do backup online](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="a0df8-144">Observe que os Pontos de recuperação online têm base nos pontos de recuperação completos expressos.</span><span class="sxs-lookup"><span data-stu-id="a0df8-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="a0df8-145">Portanto, você deve agendar o ponto de recuperação online após o período especificado para o ponto de recuperação completo expresso.</span><span class="sxs-lookup"><span data-stu-id="a0df8-145">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="a0df8-146">Configure a política de retenção para o **Backup do Azure** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-146">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="a0df8-147">Escolha uma opção de replicação online e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="a0df8-148">Se você tiver um banco de dados de grande porte, talvez a criação do backup inicial na rede demore bastante.</span><span class="sxs-lookup"><span data-stu-id="a0df8-148">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="a0df8-149">Para evitar esse problema, crie um backup offline.</span><span class="sxs-lookup"><span data-stu-id="a0df8-149">To avoid this issue, you can create an offline backup.</span></span>  

    ![Especificar política de retenção online](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="a0df8-151">Confirme as configurações e clique em **Criar Grupo**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-151">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="a0df8-152">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="a0df8-152">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="a0df8-153">Recuperar o banco de dados do Exchange</span><span class="sxs-lookup"><span data-stu-id="a0df8-153">Recover the Exchange database</span></span>
1. <span data-ttu-id="a0df8-154">Para recuperar um banco de dados do Exchange, clique em **Recuperação** no Console do Administrador do MABS.</span><span class="sxs-lookup"><span data-stu-id="a0df8-154">To recover an Exchange database, click **Recovery** in the MABS Administrator Console.</span></span>
2. <span data-ttu-id="a0df8-155">Localize o banco de dados do Exchange que você deseja recuperar.</span><span class="sxs-lookup"><span data-stu-id="a0df8-155">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="a0df8-156">Selecione um ponto de recuperação online na lista suspensa *tempo de recuperação* .</span><span class="sxs-lookup"><span data-stu-id="a0df8-156">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="a0df8-157">Clique em **Recuperar** para iniciar o **Assistente de Recuperação**.</span><span class="sxs-lookup"><span data-stu-id="a0df8-157">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="a0df8-158">Há cinco tipos de recuperação para os pontos de recuperação online:</span><span class="sxs-lookup"><span data-stu-id="a0df8-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="a0df8-159">**Recuperar no local original do Exchange Server:** os dados serão recuperados no servidor original do Exchange.</span><span class="sxs-lookup"><span data-stu-id="a0df8-159">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="a0df8-160">**Recuperar em outro banco de dados em um servidor do Exchange:** os dados serão recuperados em outro banco de dados, em outro servidor do Exchange.</span><span class="sxs-lookup"><span data-stu-id="a0df8-160">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="a0df8-161">**Recuperar um Banco de Dados de Recuperação:** os dados serão recuperados em um RDB (Banco de Dados de Recuperação do Exchange).</span><span class="sxs-lookup"><span data-stu-id="a0df8-161">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="a0df8-162">**Copiar em uma pasta de rede:** os dados serão recuperados em uma pasta de rede.</span><span class="sxs-lookup"><span data-stu-id="a0df8-162">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="a0df8-163">**Cópia em fita:** se você tiver uma biblioteca de fitas ou uma unidade de fita autônoma conectada e configurada no MABS, o ponto de recuperação será copiado em uma fita livre.</span><span class="sxs-lookup"><span data-stu-id="a0df8-163">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, the recovery point will be copied to a free tape.</span></span>

    ![Escolher a replicação online](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="a0df8-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a0df8-165">Next steps</span></span>
* [<span data-ttu-id="a0df8-166">Backup do Azure - Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="a0df8-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
