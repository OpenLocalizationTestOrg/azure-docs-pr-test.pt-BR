---
title: aaaBack backup de um servidor de Exchange tooAzure Backup com o System Center 2012 R2 DPM | Microsoft Docs
description: Saiba como tooback a um tooAzure do servidor Exchange Backup usando o System Center 2012 R2 DPM
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
ms.openlocfilehash: fa99296d095c180333474b6d419ebc5ec727547a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="ee7ea-103">Fazer backup de um servidor de Exchange tooAzure Backup com o System Center 2012 R2 DPM</span><span class="sxs-lookup"><span data-stu-id="ee7ea-103">Back up an Exchange server tooAzure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="ee7ea-104">Este artigo descreve como tooconfigure uma tooback de servidor do System Center 2012 R2 Data Protection Manager (DPM) um servidor Microsoft Exchange Backup muito do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-104">This article describes how tooconfigure a System Center 2012 R2 Data Protection Manager (DPM) server tooback up a Microsoft Exchange server too Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="ee7ea-105">Atualizações</span><span class="sxs-lookup"><span data-stu-id="ee7ea-105">Updates</span></span>
<span data-ttu-id="ee7ea-106">toosuccessfully registro Olá servidor DPM com o Backup do Azure, você deve instalar o hello mais recente update rollup para o System Center 2012 R2 DPM e hello versão mais recente do hello Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-106">toosuccessfully register hello DPM server with Azure Backup, you must install hello latest update rollup for System Center 2012 R2 DPM and hello latest version of hello Azure Backup Agent.</span></span> <span data-ttu-id="ee7ea-107">Obter o pacote cumulativo de atualização mais recente da saudação do hello [catálogo Microsoft](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="ee7ea-107">Get hello latest update rollup from hello [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="ee7ea-108">Para obter exemplos de saudação neste artigo, versão 2.0.8719.0 do hello Azure Backup Agent está instalado e atualização cumulativa 6 está instalado no System Center 2012 R2 DPM.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-108">For hello examples in this article, version 2.0.8719.0 of hello Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="ee7ea-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ee7ea-109">Prerequisites</span></span>
<span data-ttu-id="ee7ea-110">Antes de continuar, certifique-se de que todos os Olá [pré-requisitos](backup-azure-dpm-introduction.md#prerequisites) para usar o Microsoft Azure Backup tooprotect cargas de trabalho foram atendidas.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-110">Before you continue, make sure that all hello [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup tooprotect workloads have been met.</span></span> <span data-ttu-id="ee7ea-111">Esses pré-requisitos incluem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="ee7ea-111">These prerequisites include hello following:</span></span>

* <span data-ttu-id="ee7ea-112">Um cofre de backup Olá site do Azure foi criado.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-112">A backup vault on hello Azure site has been created.</span></span>
* <span data-ttu-id="ee7ea-113">Credenciais de agente e o cofre tem sido baixado toohello servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-113">Agent and vault credentials have been downloaded toohello DPM server.</span></span>
* <span data-ttu-id="ee7ea-114">Olá agente está instalado no servidor DPM hello.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-114">hello agent is installed on hello DPM server.</span></span>
* <span data-ttu-id="ee7ea-115">as credenciais do cofre Olá foram servidor DPM Olá tooregister usado.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-115">hello vault credentials were used tooregister hello DPM server.</span></span>
* <span data-ttu-id="ee7ea-116">Se você estiver protegendo o Exchange 2016, atualize tooDPM 2012 R2 UR9 ou posterior</span><span class="sxs-lookup"><span data-stu-id="ee7ea-116">If you are protecting Exchange 2016, please upgrade tooDPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="ee7ea-117">Agente de proteção do DPM</span><span class="sxs-lookup"><span data-stu-id="ee7ea-117">DPM protection agent</span></span>
<span data-ttu-id="ee7ea-118">Agente de proteção de DPM tooinstall Olá no servidor do Exchange hello, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ee7ea-118">tooinstall hello DPM protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="ee7ea-119">Certifique-se de que firewalls Olá estão configurados corretamente.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-119">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="ee7ea-120">Consulte [configurar exceções de firewall Olá agente](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee7ea-120">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="ee7ea-121">Instale o agente de saudação no servidor do Exchange Olá clicando **gerenciamento > agentes > instalar** no Console do administrador do DPM.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-121">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="ee7ea-122">Consulte [agente de proteção do DPM de saudação de instalação](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) para obter etapas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-122">See [Install hello DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="ee7ea-123">Criar um grupo de proteção para o Exchange server de saudação</span><span class="sxs-lookup"><span data-stu-id="ee7ea-123">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="ee7ea-124">No Console do administrador do DPM de Olá, clique em **proteção**e, em seguida, clique em **novo** em Olá Olá de tooopen de faixa de opções de ferramenta **criar novo grupo de proteção** assistente.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-124">In hello DPM Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="ee7ea-125">Em Olá **bem-vindo** tela hello Assistente clique **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-125">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="ee7ea-126">Em Olá **Selecionar tipo de grupo de proteção** tela, selecione **servidores** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-126">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="ee7ea-127">Selecione Olá Exchange server banco de dados que você deseja tooprotect e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-127">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ee7ea-128">Se você estiver protegendo o Exchange 2013, verifique Olá [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee7ea-128">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="ee7ea-129">Saudação de exemplo a seguir, banco de dados de saudação do Exchange 2010 está selecionado.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-129">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Selecionar membros do grupo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="ee7ea-131">Selecione o método de proteção de dados hello.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-131">Select hello data protection method.</span></span>

    <span data-ttu-id="ee7ea-132">Grupo de proteção de saudação do nome e, em seguida, selecione dois Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee7ea-132">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="ee7ea-133">Desejo a proteção de curto prazo usando Disco.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="ee7ea-134">Desejo a proteção online.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-134">I want online protection.</span></span>
6. <span data-ttu-id="ee7ea-135">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-135">Click **Next**.</span></span>
7. <span data-ttu-id="ee7ea-136">Selecione Olá **integridade de dados executar Eseutil toocheck** opção se você quiser que a integridade de bancos de dados do Exchange Server Olá Olá toocheck.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-136">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="ee7ea-137">Depois de selecionar essa opção, a verificação de consistência de backup será executada em Olá DPM tooavoid hello e/s tráfego do servidor que é gerado pela execução Olá **eseutil** comando no servidor do Exchange hello.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-137">After you select this option, backup consistency checking will be run on hello DPM server tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ee7ea-138">toouse essa opção, você deve copiar hello Ese.dll e Eseutil.exe arquivos toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin diretório Olá DPM servidor.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-138">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on hello DPM server.</span></span> <span data-ttu-id="ee7ea-139">Caso contrário, é acionado Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee7ea-139">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="ee7ea-140">![erro de eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="ee7ea-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="ee7ea-141">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-141">Click **Next**.</span></span>
9. <span data-ttu-id="ee7ea-142">Banco de dados selecione Olá para **Backup de cópia**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-142">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ee7ea-143">Se você não escolher "Backup completo" para pelo menos uma cópia de DAG de um banco de dados, os registros não ficarão truncados.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="ee7ea-144">Configurar metas Olá para **backup de curto prazo**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-144">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="ee7ea-145">Examine o espaço em disco disponível hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-145">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="ee7ea-146">Selecione Olá hora na qual o DPM Olá servidor criar a replicação inicial hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-146">Select hello time at which hello DPM server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="ee7ea-147">Selecione as opções de verificação de consistência hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-147">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="ee7ea-148">Escolha Olá banco de dados que você deseja tooback backup tooAzure e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-148">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="ee7ea-149">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ee7ea-149">For example:</span></span>

    ![Especificar dados de proteção online](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="ee7ea-151">Definir agendamento Olá para **Backup do Azure**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-151">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="ee7ea-152">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ee7ea-152">For example:</span></span>

    ![Especifique o cronograma do backup online](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="ee7ea-154">Observe que os Pontos de recuperação online têm base nos pontos de recuperação completos expressos.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="ee7ea-155">Portanto, você deve agendar o ponto de recuperação online Olá após um tempo de saudação especificado para Olá express ponto de recuperação completa.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-155">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="ee7ea-156">Configurar a política de retenção Olá para **Backup do Azure**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-156">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="ee7ea-157">Escolha uma opção de replicação online e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="ee7ea-158">Se você tiver um banco de dados grande, pode levar muito tempo para a saudação inicial toobe backup criado pela rede hello.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-158">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="ee7ea-159">tooavoid esse problema, você pode criar um backup offline.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-159">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Especificar política de retenção online](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="ee7ea-161">Confirme as configurações de saudação e, em seguida, clique em **criar grupo**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-161">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="ee7ea-162">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="ee7ea-162">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="ee7ea-163">Recuperar o banco de dados do Exchange Olá</span><span class="sxs-lookup"><span data-stu-id="ee7ea-163">Recover hello Exchange database</span></span>
1. <span data-ttu-id="ee7ea-164">toorecover um banco de dados do Exchange, clique em **recuperação** em Olá Console do administrador do DPM.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-164">toorecover an Exchange database, click **Recovery** in hello DPM Administrator Console.</span></span>
2. <span data-ttu-id="ee7ea-165">Localize o banco de dados do Exchange Olá que você deseja toorecover.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-165">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="ee7ea-166">Selecione um ponto de recuperação online de saudação *tempo de recuperação* lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-166">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="ee7ea-167">Clique em **recuperar** toostart Olá **Assistente de recuperação**.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-167">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="ee7ea-168">Há cinco tipos de recuperação para os pontos de recuperação online:</span><span class="sxs-lookup"><span data-stu-id="ee7ea-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="ee7ea-169">**Recuperar o local do Exchange Server toooriginal:** Olá dados sejam recuperados toohello original Exchange server.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-169">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="ee7ea-170">**Recuperar o banco de dados tooanother em um servidor Exchange:** Olá os dados sejam recuperados tooanother banco de dados em outro servidor Exchange.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-170">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="ee7ea-171">**Recuperar o banco de dados de recuperação de tooa:** Olá os dados sejam recuperado tooan banco de dados de recuperação do Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="ee7ea-171">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="ee7ea-172">**Pasta de rede cópia tooa:** Olá os dados sejam recuperados tooa pasta de rede.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-172">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="ee7ea-173">**Copiar tootape:** se você tiver uma biblioteca de fitas ou uma unidade de fita autônoma Olá anexado e configurado no servidor DPM, o ponto de recuperação hello serão copiados fita livre tooa.</span><span class="sxs-lookup"><span data-stu-id="ee7ea-173">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on hello DPM server, hello recovery point will be copied tooa free tape.</span></span>

    ![Escolher a replicação online](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="ee7ea-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ee7ea-175">Next steps</span></span>
* [<span data-ttu-id="ee7ea-176">Backup do Azure - Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="ee7ea-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
