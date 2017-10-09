---
title: aaaManage Azure Analysis Services | Microsoft Docs
description: Saiba como toomanage um Analysis Services server no Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="761a7-103">Gerenciar o Analysis Services</span><span class="sxs-lookup"><span data-stu-id="761a7-103">Manage Analysis Services</span></span>
<span data-ttu-id="761a7-104">Depois de criar um servidor do Analysis Services no Azure, pode haver algumas tarefas de administração, você precisa tooperform imediatamente ou em trânsito de saudação algum tempo para baixo.</span><span class="sxs-lookup"><span data-stu-id="761a7-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need tooperform right away or sometime down hello road.</span></span> <span data-ttu-id="761a7-105">Por exemplo, execute o processamento toohello de atualização de dados, controlar quem pode acessar os modelos de saudação do servidor ou monitorar a integridade do servidor.</span><span class="sxs-lookup"><span data-stu-id="761a7-105">For example, run processing toohello refresh data, control who can access hello models on your server, or monitor your server's health.</span></span> <span data-ttu-id="761a7-106">Algumas tarefas de gerenciamento só podem ser executadas no Portal do Azure, outras no SQL Server Management Studio (SSMS) e algumas tarefas podem ser executadas em ambos.</span><span class="sxs-lookup"><span data-stu-id="761a7-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="761a7-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="761a7-107">Azure portal</span></span>
<span data-ttu-id="761a7-108">[Portal do Azure](http://portal.azure.com/) é onde você pode criar e excluir servidores, monitorar os recursos do servidor, alterar o tamanho e gerenciar o acesso tooyour servidores.</span><span class="sxs-lookup"><span data-stu-id="761a7-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access tooyour servers.</span></span>  <span data-ttu-id="761a7-109">Se você estiver enfrentando problemas, também poderá enviar uma solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="761a7-109">If you're having some problems, you can also submit a support request.</span></span>

![Obter o nome do servidor no Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="761a7-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="761a7-111">SQL Server Management Studio</span></span>
<span data-ttu-id="761a7-112">Conectando o servidor tooyour no Azure é como conectar-se a instância de servidor tooa em sua própria organização.</span><span class="sxs-lookup"><span data-stu-id="761a7-112">Connecting tooyour server in Azure is just like connecting tooa server instance in your own organization.</span></span> <span data-ttu-id="761a7-113">No SSMS, você pode executar muitas das Olá mesmo tarefas como processar dados ou criar um script de processamento, gerenciar funções e usar o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="761a7-113">From SSMS, you can perform many of hello same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="761a7-115">Baixar e instalar o SSMS</span><span class="sxs-lookup"><span data-stu-id="761a7-115">Download and install SSMS</span></span>
<span data-ttu-id="761a7-116">tooget todos Olá experiência mais suave hello e recursos mais recentes ao conectar-se o servidor de serviços de análise do Azure tooyour, certifique-se de que você está usando a versão mais recente de saudação do SSMS.</span><span class="sxs-lookup"><span data-stu-id="761a7-116">tooget all hello latest features, and hello smoothest experience when connecting tooyour Azure Analysis Services server, be sure you're using hello latest version of SSMS.</span></span> 

<span data-ttu-id="761a7-117">[Baixar o SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="761a7-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="tooconnect-with-ssms"></a><span data-ttu-id="761a7-118">tooconnect com SSMS</span><span class="sxs-lookup"><span data-stu-id="761a7-118">tooconnect with SSMS</span></span>
 <span data-ttu-id="761a7-119">Ao usar o SSMS, antes de saudação do servidor conectado tooyour primeira vez, verifique se que seu nome de usuário está incluído no grupo de administradores de serviços de análise de saudação.</span><span class="sxs-lookup"><span data-stu-id="761a7-119">When using SSMS, before connecting tooyour server hello first time, make sure your username is included in hello Analysis Services Admins group.</span></span> <span data-ttu-id="761a7-120">mais, consulte toolearn [os administradores de servidor](#server-administrators) posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="761a7-120">toolearn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="761a7-121">Antes de você se conectar, é necessário tooget nome do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="761a7-121">Before you connect, you need tooget hello server name.</span></span> <span data-ttu-id="761a7-122">Em **portal do Azure** > servidor > **visão geral** > **nome do servidor**, nome do servidor de saudação de cópia.</span><span class="sxs-lookup"><span data-stu-id="761a7-122">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Obter o nome do servidor no Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="761a7-124">No SSMS > **Pesquisador de Objetos**, clique em **Conectar** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="761a7-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="761a7-125">Em Olá **conectar tooServer** colar em nome do servidor de saudação, em seguida, na caixa de diálogo **autenticação**, escolha um dos seguintes tipos de autenticação de saudação:</span><span class="sxs-lookup"><span data-stu-id="761a7-125">In hello **Connect tooServer** dialog box, paste in hello server name, then in **Authentication**, choose one of hello following authentication types:</span></span>
   
    <span data-ttu-id="761a7-126">**Autenticação do Windows** toouse suas credenciais de domínio ome de usuário e senha do Windows.</span><span class="sxs-lookup"><span data-stu-id="761a7-126">**Windows Authentication** toouse your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="761a7-127">**A autenticação de senha do Active Directory** toouse uma conta organizacional.</span><span class="sxs-lookup"><span data-stu-id="761a7-127">**Active Directory Password Authentication** toouse an organizational account.</span></span> <span data-ttu-id="761a7-128">Por exemplo, ao conectar-se de um computador que não ingressou em um domínio.</span><span class="sxs-lookup"><span data-stu-id="761a7-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="761a7-129">**Autenticação do Active Directory Universal** toouse [autenticação multifator ou não interativo](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="761a7-129">**Active Directory Universal Authentication** toouse [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Conectar-se no SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="761a7-131">Administradores de servidor e usuários de banco de dados</span><span class="sxs-lookup"><span data-stu-id="761a7-131">Server administrators and database users</span></span>
<span data-ttu-id="761a7-132">Nos Azure Analysis Services, há dois tipos de usuários, administradores de servidor e usuários de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="761a7-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="761a7-133">Os dois tipos de usuários devem estar no Azure Active Directory e devem ser especificados por endereços de email organizacionais ou UPN.</span><span class="sxs-lookup"><span data-stu-id="761a7-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="761a7-134">mais, consulte toolearn [permissões de usuário e autenticação](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="761a7-134">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="761a7-135">Solucionar problemas de conexão</span><span class="sxs-lookup"><span data-stu-id="761a7-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="761a7-136">Ao se conectar usando o SSMS, se você tiver problemas, talvez seja necessário tooclear cache de logon de saudação.</span><span class="sxs-lookup"><span data-stu-id="761a7-136">When connecting using SSMS, if you run into problems, you may need tooclear hello login cache.</span></span> <span data-ttu-id="761a7-137">Nada é armazenado em cache toodisc.</span><span class="sxs-lookup"><span data-stu-id="761a7-137">Nothing is cached toodisc.</span></span> <span data-ttu-id="761a7-138">tooclear Olá de cache, feche e reinicialização Olá conectam processo.</span><span class="sxs-lookup"><span data-stu-id="761a7-138">tooclear hello cache, close and restart hello connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="761a7-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="761a7-139">Next steps</span></span>
<span data-ttu-id="761a7-140">Se você já não tiver implantado um novo servidor de modelo de tabela tooyour, agora é um bom momento.</span><span class="sxs-lookup"><span data-stu-id="761a7-140">If you haven't already deployed a tabular model tooyour new server, now is a good time.</span></span> <span data-ttu-id="761a7-141">mais, consulte toolearn [implantar serviços de análise de tooAzure](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="761a7-141">toolearn more, see [Deploy tooAzure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="761a7-142">Se você implantou um servidor de tooyour de modelo, você está pronto tooconnect tooit usando um cliente ou navegador.</span><span class="sxs-lookup"><span data-stu-id="761a7-142">If you've deployed a model tooyour server, you're ready tooconnect tooit using a client or browser.</span></span> <span data-ttu-id="761a7-143">mais, consulte toolearn [obter dados do servidor do Azure Analysis Services](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="761a7-143">toolearn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

