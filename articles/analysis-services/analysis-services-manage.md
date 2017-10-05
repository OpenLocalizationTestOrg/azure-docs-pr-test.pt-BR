---
title: Gerenciar o Azure Analysis Services | Microsoft Docs
description: Saiba como gerenciar um servidor do Analysis Services no Azure.
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
ms.openlocfilehash: b897e81351ebee11c292e67ac76ba8202a6f0108
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="32a6d-103">Gerenciar o Analysis Services</span><span class="sxs-lookup"><span data-stu-id="32a6d-103">Manage Analysis Services</span></span>
<span data-ttu-id="32a6d-104">Depois de criar um servidor do Analysis Services no Azure, talvez seja necessário executar algumas tarefas de administração e gerenciamento imediatamente ou em algum momento no futuro.</span><span class="sxs-lookup"><span data-stu-id="32a6d-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need to perform right away or sometime down the road.</span></span> <span data-ttu-id="32a6d-105">Por exemplo, executar o processamento nos dados atualizados, controlar quem pode acessar os modelos em seu servidor ou monitorar a integridade do servidor.</span><span class="sxs-lookup"><span data-stu-id="32a6d-105">For example, run processing to the refresh data, control who can access the models on your server, or monitor your server's health.</span></span> <span data-ttu-id="32a6d-106">Algumas tarefas de gerenciamento só podem ser executadas no Portal do Azure, outras no SQL Server Management Studio (SSMS) e algumas tarefas podem ser executadas em ambos.</span><span class="sxs-lookup"><span data-stu-id="32a6d-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="32a6d-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="32a6d-107">Azure portal</span></span>
<span data-ttu-id="32a6d-108">O [Portal do Azure](http://portal.azure.com/) é o local em que você pode criar e excluir servidores, monitorar recursos de servidor, alterar o tamanho e gerenciar quem tem acesso aos seus servidores.</span><span class="sxs-lookup"><span data-stu-id="32a6d-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access to your servers.</span></span>  <span data-ttu-id="32a6d-109">Se você estiver enfrentando problemas, também poderá enviar uma solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="32a6d-109">If you're having some problems, you can also submit a support request.</span></span>

![Obter o nome do servidor no Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="32a6d-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="32a6d-111">SQL Server Management Studio</span></span>
<span data-ttu-id="32a6d-112">Conectar-se ao seu servidor no Azure é como se conectar a uma instância de servidor em sua própria organização.</span><span class="sxs-lookup"><span data-stu-id="32a6d-112">Connecting to your server in Azure is just like connecting to a server instance in your own organization.</span></span> <span data-ttu-id="32a6d-113">No SSMS, você pode executar algumas tarefas como processar dados ou criar um script de processamento, gerenciar funções e usar o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32a6d-113">From SSMS, you can perform many of the same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="32a6d-115">Baixar e instalar o SSMS</span><span class="sxs-lookup"><span data-stu-id="32a6d-115">Download and install SSMS</span></span>
<span data-ttu-id="32a6d-116">Para obter todos os recursos mais recentes e a melhor experiência ao se conectar ao servidor do Azure Analysis Services, certifique-se de que está usando a versão mais recente do SSMS.</span><span class="sxs-lookup"><span data-stu-id="32a6d-116">To get all the latest features, and the smoothest experience when connecting to your Azure Analysis Services server, be sure you're using the latest version of SSMS.</span></span> 

<span data-ttu-id="32a6d-117">[Baixar o SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="32a6d-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="to-connect-with-ssms"></a><span data-ttu-id="32a6d-118">Para conectar-se com o SSMS</span><span class="sxs-lookup"><span data-stu-id="32a6d-118">To connect with SSMS</span></span>
 <span data-ttu-id="32a6d-119">Ao usar o SSMS, antes de se conectar ao servidor na primeira vez, verifique se que seu nome de usuário está incluído no grupo de administradores do Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="32a6d-119">When using SSMS, before connecting to your server the first time, make sure your username is included in the Analysis Services Admins group.</span></span> <span data-ttu-id="32a6d-120">Para obter mais informações, consulte [Administradores de servidor](#server-administrators) posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="32a6d-120">To learn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="32a6d-121">Antes de se conectar, você precisa obter o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="32a6d-121">Before you connect, you need to get the server name.</span></span> <span data-ttu-id="32a6d-122">No **Portal do Azure** > servidor > **Visão geral** > **Nome do servidor**, copie o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="32a6d-122">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Obter o nome do servidor no Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="32a6d-124">No SSMS > **Pesquisador de Objetos**, clique em **Conectar** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="32a6d-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="32a6d-125">Na caixa de diálogo **Conectar ao Servidor**, cole o nome do servidor e, em **Autenticação**, escolha um dos seguintes tipos de autenticação:</span><span class="sxs-lookup"><span data-stu-id="32a6d-125">In the **Connect to Server** dialog box, paste in the server name, then in **Authentication**, choose one of the following authentication types:</span></span>
   
    <span data-ttu-id="32a6d-126">**Autenticação do Windows** para usar suas credenciais de domínio/nome de usuário e senha do Windows.</span><span class="sxs-lookup"><span data-stu-id="32a6d-126">**Windows Authentication** to use your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="32a6d-127">**Autenticação de Senha do Active Directory** para usar uma conta organizacional.</span><span class="sxs-lookup"><span data-stu-id="32a6d-127">**Active Directory Password Authentication** to use an organizational account.</span></span> <span data-ttu-id="32a6d-128">Por exemplo, ao conectar-se de um computador que não ingressou em um domínio.</span><span class="sxs-lookup"><span data-stu-id="32a6d-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="32a6d-129">**Autenticação Universal do Active Directory** para usar [autenticação multifator ou não interativa](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="32a6d-129">**Active Directory Universal Authentication** to use [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Conectar-se no SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="32a6d-131">Administradores de servidor e usuários de banco de dados</span><span class="sxs-lookup"><span data-stu-id="32a6d-131">Server administrators and database users</span></span>
<span data-ttu-id="32a6d-132">Nos Azure Analysis Services, há dois tipos de usuários, administradores de servidor e usuários de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="32a6d-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="32a6d-133">Os dois tipos de usuários devem estar no Azure Active Directory e devem ser especificados por endereços de email organizacionais ou UPN.</span><span class="sxs-lookup"><span data-stu-id="32a6d-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="32a6d-134">Para obter mais informações, consulte [Autenticação e permissões de usuário](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="32a6d-134">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="32a6d-135">Solucionar problemas de conexão</span><span class="sxs-lookup"><span data-stu-id="32a6d-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="32a6d-136">Ao conectar usando o SSMS, se você tiver problemas, talvez seja necessário limpar o cache de logon.</span><span class="sxs-lookup"><span data-stu-id="32a6d-136">When connecting using SSMS, if you run into problems, you may need to clear the login cache.</span></span> <span data-ttu-id="32a6d-137">Nada é armazenado em cache de disco. Para limpar o cache, feche e reinicie o processo de conexão.</span><span class="sxs-lookup"><span data-stu-id="32a6d-137">Nothing is cached to disc. To clear the cache, close and restart the connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="32a6d-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="32a6d-138">Next steps</span></span>
<span data-ttu-id="32a6d-139">Se você ainda não tiver implantado um modelo de tabela em seu novo servidor, agora é um bom momento.</span><span class="sxs-lookup"><span data-stu-id="32a6d-139">If you haven't already deployed a tabular model to your new server, now is a good time.</span></span> <span data-ttu-id="32a6d-140">Para saber mais, confira [Implantar no Azure Analysis Services](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="32a6d-140">To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="32a6d-141">Se você tiver implantado um modelo de tabela para seu servidor, você estará pronto para se conectar usando um cliente ou navegador.</span><span class="sxs-lookup"><span data-stu-id="32a6d-141">If you've deployed a model to your server, you're ready to connect to it using a client or browser.</span></span> <span data-ttu-id="32a6d-142">Para saber mais, confira [Obter dados do servidor do Azure Analysis Services](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="32a6d-142">To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

