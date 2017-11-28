---
title: aaaBack backup de um servidor de Exchange tooAzure Backup com o servidor de Backup do Azure | Microsoft Docs
description: Saiba como tooback a um tooAzure do servidor Exchange Backup usando o servidor de Backup do Azure
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
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a><span data-ttu-id="5bbf1-103">Fazer backup de um servidor de Exchange tooAzure Backup com o servidor de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="5bbf1-103">Back up an Exchange server tooAzure Backup with Azure Backup Server</span></span>
<span data-ttu-id="5bbf1-104">Este artigo descreve como tooback do Microsoft Azure Backup Server (MABS) tooconfigure a um tooAzure de servidor do Microsoft Exchange.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-104">This article describes how tooconfigure Microsoft Azure Backup Server (MABS) tooback up a Microsoft Exchange server tooAzure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="5bbf1-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5bbf1-105">Prerequisites</span></span>
<span data-ttu-id="5bbf1-106">Antes de continuar, verifique se o Servidor de Backup do Azure está [instalado e preparado](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="5bbf1-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="5bbf1-107">Agente de proteção do MABS</span><span class="sxs-lookup"><span data-stu-id="5bbf1-107">MABS protection agent</span></span>
<span data-ttu-id="5bbf1-108">Agente de proteção de MABS tooinstall Olá no servidor do Exchange hello, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="5bbf1-108">tooinstall hello MABS protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="5bbf1-109">Certifique-se de que firewalls Olá estão configurados corretamente.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-109">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="5bbf1-110">Consulte [configurar exceções de firewall Olá agente](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="5bbf1-110">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="5bbf1-111">Instale o agente de saudação no servidor do Exchange Olá clicando **gerenciamento > agentes > instalar** no Console do administrador MABS.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-111">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="5bbf1-112">Consulte [instalar agente de proteção de MABS de saudação](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) para obter etapas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-112">See [Install hello MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="5bbf1-113">Criar um grupo de proteção para o Exchange server de saudação</span><span class="sxs-lookup"><span data-stu-id="5bbf1-113">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="5bbf1-114">No hello MABS Administrator Console, clique em **proteção**e, em seguida, clique em **novo** em Olá Olá de tooopen de faixa de opções de ferramenta **criar novo grupo de proteção** assistente.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-114">In hello MABS Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="5bbf1-115">Em Olá **bem-vindo** tela hello Assistente clique **próximo**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-115">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="5bbf1-116">Em Olá **Selecionar tipo de grupo de proteção** tela, selecione **servidores** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-116">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="5bbf1-117">Selecione Olá Exchange server banco de dados que você deseja tooprotect e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-117">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5bbf1-118">Se você estiver protegendo o Exchange 2013, verifique Olá [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="5bbf1-118">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="5bbf1-119">Saudação de exemplo a seguir, banco de dados de saudação do Exchange 2010 está selecionado.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-119">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Selecionar membros do grupo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="5bbf1-121">Selecione o método de proteção de dados hello.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-121">Select hello data protection method.</span></span>

    <span data-ttu-id="5bbf1-122">Grupo de proteção de saudação do nome e, em seguida, selecione dois Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="5bbf1-122">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="5bbf1-123">Desejo a proteção de curto prazo usando Disco.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="5bbf1-124">Desejo a proteção online.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-124">I want online protection.</span></span>
6. <span data-ttu-id="5bbf1-125">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-125">Click **Next**.</span></span>
7. <span data-ttu-id="5bbf1-126">Selecione Olá **integridade de dados executar Eseutil toocheck** opção se você quiser que a integridade de bancos de dados do Exchange Server Olá Olá toocheck.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-126">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="5bbf1-127">Depois de selecionar essa opção, a verificação de consistência de backup será executada em MABS tooavoid hello e/s o tráfego que é gerado pela execução Olá **eseutil** comando no servidor do Exchange hello.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-127">After you select this option, backup consistency checking will be run on MABS tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5bbf1-128">toouse essa opção, você deve copiar hello Ese.dll e Eseutil.exe arquivos toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin diretório Olá MAB servidor.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-128">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on hello MAB server.</span></span> <span data-ttu-id="5bbf1-129">Caso contrário, é acionado Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="5bbf1-129">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="5bbf1-130">![erro de eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="5bbf1-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="5bbf1-131">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-131">Click **Next**.</span></span>
9. <span data-ttu-id="5bbf1-132">Banco de dados selecione Olá para **Backup de cópia**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-132">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5bbf1-133">Se você não escolher "Backup completo" para pelo menos uma cópia de DAG de um banco de dados, os registros não ficarão truncados.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="5bbf1-134">Configurar metas Olá para **backup de curto prazo**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-134">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="5bbf1-135">Examine o espaço em disco disponível hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-135">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="5bbf1-136">Selecione Olá tempo no qual Olá MAB servidor criar a replicação inicial hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-136">Select hello time at which hello MAB Server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="5bbf1-137">Selecione as opções de verificação de consistência hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-137">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="5bbf1-138">Escolha Olá banco de dados que você deseja tooback backup tooAzure e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-138">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="5bbf1-139">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5bbf1-139">For example:</span></span>

    ![Especificar dados de proteção online](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="5bbf1-141">Definir agendamento Olá para **Backup do Azure**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-141">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="5bbf1-142">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5bbf1-142">For example:</span></span>

    ![Especifique o cronograma do backup online](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="5bbf1-144">Observe que os Pontos de recuperação online têm base nos pontos de recuperação completos expressos.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="5bbf1-145">Portanto, você deve agendar o ponto de recuperação online Olá após um tempo de saudação especificado para Olá express ponto de recuperação completa.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-145">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="5bbf1-146">Configurar a política de retenção Olá para **Backup do Azure**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-146">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="5bbf1-147">Escolha uma opção de replicação online e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="5bbf1-148">Se você tiver um banco de dados grande, pode levar muito tempo para a saudação inicial toobe backup criado pela rede hello.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-148">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="5bbf1-149">tooavoid esse problema, você pode criar um backup offline.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-149">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Especificar política de retenção online](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="5bbf1-151">Confirme as configurações de saudação e, em seguida, clique em **criar grupo**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-151">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="5bbf1-152">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="5bbf1-152">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="5bbf1-153">Recuperar o banco de dados do Exchange Olá</span><span class="sxs-lookup"><span data-stu-id="5bbf1-153">Recover hello Exchange database</span></span>
1. <span data-ttu-id="5bbf1-154">toorecover um banco de dados do Exchange, clique em **recuperação** em Olá MABS Administrator Console.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-154">toorecover an Exchange database, click **Recovery** in hello MABS Administrator Console.</span></span>
2. <span data-ttu-id="5bbf1-155">Localize o banco de dados do Exchange Olá que você deseja toorecover.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-155">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="5bbf1-156">Selecione um ponto de recuperação online de saudação *tempo de recuperação* lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-156">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="5bbf1-157">Clique em **recuperar** toostart Olá **Assistente de recuperação**.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-157">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="5bbf1-158">Há cinco tipos de recuperação para os pontos de recuperação online:</span><span class="sxs-lookup"><span data-stu-id="5bbf1-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="5bbf1-159">**Recuperar o local do Exchange Server toooriginal:** Olá dados sejam recuperados toohello original Exchange server.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-159">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="5bbf1-160">**Recuperar o banco de dados tooanother em um servidor Exchange:** Olá os dados sejam recuperados tooanother banco de dados em outro servidor Exchange.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-160">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="5bbf1-161">**Recuperar o banco de dados de recuperação de tooa:** Olá os dados sejam recuperado tooan banco de dados de recuperação do Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="5bbf1-161">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="5bbf1-162">**Pasta de rede cópia tooa:** Olá os dados sejam recuperados tooa pasta de rede.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-162">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="5bbf1-163">**Copiar tootape:** se você tiver uma biblioteca de fitas ou uma unidade de fita autônoma MABS anexado e configurado no ponto de recuperação hello serão copiados fita livre tooa.</span><span class="sxs-lookup"><span data-stu-id="5bbf1-163">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, hello recovery point will be copied tooa free tape.</span></span>

    ![Escolher a replicação online](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="5bbf1-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5bbf1-165">Next steps</span></span>
* [<span data-ttu-id="5bbf1-166">Backup do Azure - Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="5bbf1-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
