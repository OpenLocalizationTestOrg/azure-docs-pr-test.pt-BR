---
title: "Sincronização do Azure AD Connect: considerações e tarefas operacionais | Microsoft Docs"
description: "Este tópico descreve as tarefas operacionais para a sincronização do Azure Connect AD e como preparar para operar esse componente."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: b7583a1556bb1113f349a78890768451e39c6878
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="8322b-103">Sincronização do Azure AD Connect: considerações e tarefas operacionais</span><span class="sxs-lookup"><span data-stu-id="8322b-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="8322b-104">O objetivo deste tópico é descrever as tarefas operacionais da sincronização do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8322b-104">The objective of this topic is to describe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="8322b-105">Modo de preparo</span><span class="sxs-lookup"><span data-stu-id="8322b-105">Staging mode</span></span>
<span data-ttu-id="8322b-106">O modo de teste pode ser usado para vários cenários, incluindo:</span><span class="sxs-lookup"><span data-stu-id="8322b-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="8322b-107">Alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="8322b-107">High availability.</span></span>
* <span data-ttu-id="8322b-108">Teste e implantação de novas alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="8322b-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="8322b-109">Introdução de um novo servidor e encerramento do antigo.</span><span class="sxs-lookup"><span data-stu-id="8322b-109">Introduce a new server and decommission the old.</span></span>

<span data-ttu-id="8322b-110">Com um servidor no modo de preparo, você pode fazer alterações na configuração e visualizar as alterações antes de tornar o servidor ativo.</span><span class="sxs-lookup"><span data-stu-id="8322b-110">With a server in staging mode, you can make changes to the configuration and preview the changes before you make the server active.</span></span> <span data-ttu-id="8322b-111">Ele também permite executar sincronização e importação totais para verificar se todas as alterações são esperadas antes de você fazê-las em seu ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8322b-111">It also allows you to run full import and full synchronization to verify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="8322b-112">Durante a instalação, você pode selecionar o servidor em **modo de preparo**.</span><span class="sxs-lookup"><span data-stu-id="8322b-112">During installation, you can select the server to be in **staging mode**.</span></span> <span data-ttu-id="8322b-113">Essa ação ativa o servidor de importação e sincronização, mas não executa qualquer exportação.</span><span class="sxs-lookup"><span data-stu-id="8322b-113">This action makes the server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="8322b-114">Um servidor no modo de preparo não executa a sincronização de senha ou o write-back de senha, mesmo que esses recursos sejam selecionados durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="8322b-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="8322b-115">Quando você desabilita o modo de preparo, o servidor inicia a exportação e habilita a sincronização de senha e o write-back de senha.</span><span class="sxs-lookup"><span data-stu-id="8322b-115">When you disable staging mode, the server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="8322b-116">Você ainda pode forçar uma exportação usando o Synchronization Service Manager.</span><span class="sxs-lookup"><span data-stu-id="8322b-116">You can still force an export by using the synchronization service manager.</span></span>

<span data-ttu-id="8322b-117">Um servidor em modo de preparo continua a receber alterações do Active Directory e do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8322b-117">A server in staging mode continues to receive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="8322b-118">Ele sempre tem uma cópia das alterações mais recentes e pode assumir as responsabilidades de outro servidor rapidamente.</span><span class="sxs-lookup"><span data-stu-id="8322b-118">It always has a copy of the latest changes and can very fast take over the responsibilities of another server.</span></span> <span data-ttu-id="8322b-119">Se você fizer alterações de configuração no servidor primário, será sua responsabilidade fazer as mesmas alterações no servidor em modo de preparo.</span><span class="sxs-lookup"><span data-stu-id="8322b-119">If you make configuration changes to your primary server, it is your responsibility to make the same changes to the server in staging mode.</span></span>

<span data-ttu-id="8322b-120">Para aqueles com conhecimento das tecnologias mais antigas de sincronização, o modo de preparo é diferente, pois o servidor tem seu próprio banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="8322b-120">For those of you with knowledge of older sync technologies, the staging mode is different since the server has its own SQL database.</span></span> <span data-ttu-id="8322b-121">Essa arquitetura permite que o servidor de modo de preparo esteja localizado em um datacenter diferente.</span><span class="sxs-lookup"><span data-stu-id="8322b-121">This architecture allows the staging mode server to be located in a different datacenter.</span></span>

### <a name="verify-the-configuration-of-a-server"></a><span data-ttu-id="8322b-122">Verifique a configuração de um servidor</span><span class="sxs-lookup"><span data-stu-id="8322b-122">Verify the configuration of a server</span></span>
<span data-ttu-id="8322b-123">Para aplicar esse método, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="8322b-123">To apply this method, follow these steps:</span></span>

1. [<span data-ttu-id="8322b-124">Preparar</span><span class="sxs-lookup"><span data-stu-id="8322b-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="8322b-125">Configuração</span><span class="sxs-lookup"><span data-stu-id="8322b-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="8322b-126">Importar e sincronizar</span><span class="sxs-lookup"><span data-stu-id="8322b-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="8322b-127">Verificar</span><span class="sxs-lookup"><span data-stu-id="8322b-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="8322b-128">Servidor ativo do comutador</span><span class="sxs-lookup"><span data-stu-id="8322b-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="8322b-129">Preparar</span><span class="sxs-lookup"><span data-stu-id="8322b-129">Prepare</span></span>
1. <span data-ttu-id="8322b-130">Instale o Azure AD Connect, selecione **modo de preparo** e desmarque **Iniciar sincronização** na última página do assistente de instalação.</span><span class="sxs-lookup"><span data-stu-id="8322b-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on the last page in the installation wizard.</span></span> <span data-ttu-id="8322b-131">Esse modo permite que você execute o mecanismo de sincronização manualmente.</span><span class="sxs-lookup"><span data-stu-id="8322b-131">This mode allows you to run the sync engine manually.</span></span>
   <span data-ttu-id="8322b-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="8322b-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="8322b-133">Saia e entre e, no menu Iniciar, selecione **Serviço de Sincronização**.</span><span class="sxs-lookup"><span data-stu-id="8322b-133">Sign off/sign in and from the start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="8322b-134">Configuração</span><span class="sxs-lookup"><span data-stu-id="8322b-134">Configuration</span></span>
<span data-ttu-id="8322b-135">Se você tiver feito alterações personalizadas no servidor primário e deseja comparar a configuração com o servidor de preparo, use o [documentador de configuração do Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="8322b-135">If you have made custom changes to the primary server and want to compare the configuration with the staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="8322b-136">Importar e sincronizar</span><span class="sxs-lookup"><span data-stu-id="8322b-136">Import and Synchronize</span></span>
1. <span data-ttu-id="8322b-137">Selecione **Conectores** e selecione o primeiro conector com o tipo **Active Directory Domain Services**.</span><span class="sxs-lookup"><span data-stu-id="8322b-137">Select **Connectors**, and select the first Connector with the type **Active Directory Domain Services**.</span></span> <span data-ttu-id="8322b-138">Clique em **Executar**, selecione **Importação completa** e **OK**.</span><span class="sxs-lookup"><span data-stu-id="8322b-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="8322b-139">Siga estas etapas para todos os Conectores desse tipo.</span><span class="sxs-lookup"><span data-stu-id="8322b-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="8322b-140">Selecione o Conector com o tipo **Active Directory do Azure (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="8322b-140">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="8322b-141">Clique em **Executar**, selecione **Importação completa** e **OK**.</span><span class="sxs-lookup"><span data-stu-id="8322b-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="8322b-142">Verifique se a guia Conectores ainda está selecionada.</span><span class="sxs-lookup"><span data-stu-id="8322b-142">Make sure the tab Connectors is still selected.</span></span> <span data-ttu-id="8322b-143">Para cada Conector com tipo **Active Directory Domain Services**, clique em **Executar**, selecione **Sincronização Delta** e **OK**.</span><span class="sxs-lookup"><span data-stu-id="8322b-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="8322b-144">Selecione o Conector com o tipo **Active Directory do Azure (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="8322b-144">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="8322b-145">Clique em **Executar**, selecione **Sincronização Delta** e **OK**.</span><span class="sxs-lookup"><span data-stu-id="8322b-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="8322b-146">Você agora preparou a exportação das alterações para o Azure AD e AD local (se estiver usando implantação híbrida do Exchange).</span><span class="sxs-lookup"><span data-stu-id="8322b-146">You have now staged export changes to Azure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="8322b-147">As próximas etapas permitem que você inspecione o que está prestes a ser alterado antes de realmente começar a exportação para os diretórios.</span><span class="sxs-lookup"><span data-stu-id="8322b-147">The next steps allow you to inspect what is about to change before you actually start the export to the directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="8322b-148">Verificar</span><span class="sxs-lookup"><span data-stu-id="8322b-148">Verify</span></span>
1. <span data-ttu-id="8322b-149">Inicie um prompt de comando e vá para `%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="8322b-149">Start a cmd prompt and go to `%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="8322b-150">Execute: `csexport "Name of Connector" %temp%\export.xml /f:x` o nome do Conector pode ser encontrado no Serviço de Sincronização.</span><span class="sxs-lookup"><span data-stu-id="8322b-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` The name of the Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="8322b-151">Ele tem um nome semelhante a "contoso.com – AAD" para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8322b-151">It has a name similar to "contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="8322b-152">Copie o script do PowerShell da seção [CSAnalyzer](#appendix-csanalyzer) para um arquivo chamado `csanalyzer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="8322b-152">Copy the PowerShell script from the section [CSAnalyzer](#appendix-csanalyzer) to a file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="8322b-153">Abra uma janela do PowerShell e procure a pasta em que você criou o script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8322b-153">Open a PowerShell window and browse to the folder where you created the PowerShell script.</span></span>
5. <span data-ttu-id="8322b-154">Execute: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="8322b-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="8322b-155">Agora você tem um arquivo chamado **processedusers1.csv** que pode ser examinado no Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="8322b-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="8322b-156">Todas as alterações preparadas para serem exportadas para o Azure AD são encontradas nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="8322b-156">All changes staged to be exported to Azure AD are found in this file.</span></span>
7. <span data-ttu-id="8322b-157">Faça as alterações necessárias na configuração ou nos dados e execute essas etapas novamente (importar, sincronizar e verificar) até o momento estimado para que as alterações a serem exportadas ocorram.</span><span class="sxs-lookup"><span data-stu-id="8322b-157">Make necessary changes to the data or configuration and run these steps again (Import and Synchronize and Verify) until the changes that are about to be exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="8322b-158">Servidor ativo do comutador</span><span class="sxs-lookup"><span data-stu-id="8322b-158">Switch active server</span></span>
1. <span data-ttu-id="8322b-159">No servidor atualmente ativo, desligue o servidor (FIM/DirSync/Azure AD Sync) para que ele não exporte para o Azure AD ou defina-o no modo de preparação (Azure AD Connect).</span><span class="sxs-lookup"><span data-stu-id="8322b-159">On the currently active server, either turn off the server (DirSync/FIM/Azure AD Sync) so it is not exporting to Azure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="8322b-160">Execute o assistente de instalação no servidor no **modo de preparo** e desabilite o **modo de preparo**.</span><span class="sxs-lookup"><span data-stu-id="8322b-160">Run the installation wizard on the server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="8322b-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="8322b-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="8322b-162">Recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="8322b-162">Disaster recovery</span></span>
<span data-ttu-id="8322b-163">Parte do design de implementação é planejar o que fazer em caso de desastre, quando você perde o servidor de sincronização.</span><span class="sxs-lookup"><span data-stu-id="8322b-163">Part of the implementation design is to plan for what to do in case there is a disaster where you lose the sync server.</span></span> <span data-ttu-id="8322b-164">Há modelos diferentes para uso e qual deles usar depende de vários fatores, incluindo:</span><span class="sxs-lookup"><span data-stu-id="8322b-164">There are different models to use and which one to use depends on several factors including:</span></span>

* <span data-ttu-id="8322b-165">Quão tolerável é para você não poder fazer alterações em objetos no Azure AD durante o tempo de inatividade?</span><span class="sxs-lookup"><span data-stu-id="8322b-165">What is your tolerance for not being able make changes to objects in Azure AD during the downtime?</span></span>
* <span data-ttu-id="8322b-166">Se você usar a sincronização de senha, os usuários aceitarão que devem usar a senha antiga no Azure AD se a alterarem no local?</span><span class="sxs-lookup"><span data-stu-id="8322b-166">If you use password synchronization, do the users accept that they have to use the old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="8322b-167">Você tem uma dependência em operações em tempo real, como write-back de senha?</span><span class="sxs-lookup"><span data-stu-id="8322b-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="8322b-168">Dependendo das respostas a essas perguntas e da política da sua organização, uma das estratégias abaixo pode ser implementada:</span><span class="sxs-lookup"><span data-stu-id="8322b-168">Depending on the answers to these questions and your organization’s policy, one of the following strategies can be implemented:</span></span>

* <span data-ttu-id="8322b-169">Recriar quando necessário.</span><span class="sxs-lookup"><span data-stu-id="8322b-169">Rebuild when needed.</span></span>
* <span data-ttu-id="8322b-170">Ter um servidor em espera reserva, conhecido como **modo de preparo**.</span><span class="sxs-lookup"><span data-stu-id="8322b-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="8322b-171">Usar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8322b-171">Use virtual machines.</span></span>

<span data-ttu-id="8322b-172">Se não usar o banco de dados interno do SQL Express, você também deverá examinar a seção [Alta disponibilidade do SQL](#sql-high-availability) .</span><span class="sxs-lookup"><span data-stu-id="8322b-172">If you do not use the built-in SQL Express database, then you should also review the [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="8322b-173">Recriar quando necessário</span><span class="sxs-lookup"><span data-stu-id="8322b-173">Rebuild when needed</span></span>
<span data-ttu-id="8322b-174">Uma estratégia viável é planejar para a recriação do servidor quando necessário.</span><span class="sxs-lookup"><span data-stu-id="8322b-174">A viable strategy is to plan for a server rebuild when needed.</span></span> <span data-ttu-id="8322b-175">Geralmente, a instalação do mecanismo de sincronização, a importação e a sincronização inicial podem ser concluídas em algumas horas.</span><span class="sxs-lookup"><span data-stu-id="8322b-175">Usually, installing the sync engine and do the initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="8322b-176">Se não houver um servidor reserva disponível, é possível usar temporariamente um controlador de domínio para hospedar o mecanismo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="8322b-176">If there isn’t a spare server available, it is possible to temporarily use a domain controller to host the sync engine.</span></span>

<span data-ttu-id="8322b-177">O servidor do mecanismo de sincronização não armazena qualquer estado sobre os objetos para que o banco de dados possa ser reconstruído com os dados no Active Directory e no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8322b-177">The sync engine server does not store any state about the objects so the database can be rebuilt from the data in Active Directory and Azure AD.</span></span> <span data-ttu-id="8322b-178">O atributo **sourceAnchor** é usado para unir os objetos do local e da nuvem.</span><span class="sxs-lookup"><span data-stu-id="8322b-178">The **sourceAnchor** attribute is used to join the objects from on-premises and the cloud.</span></span> <span data-ttu-id="8322b-179">Se você recriar o servidor com objetos locais existentes e a nuvem, o mecanismo de sincronização fará a correspondência entre esses objetos novamente na reinstalação.</span><span class="sxs-lookup"><span data-stu-id="8322b-179">If you rebuild the server with existing objects on-premises and the cloud, then the sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="8322b-180">As coisas que você precisa documentar e salvar são as alterações de configuração feitas no servidor, como regras de sincronização e de filtragem.</span><span class="sxs-lookup"><span data-stu-id="8322b-180">The things you need to document and save are the configuration changes made to the server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="8322b-181">Essas configurações personalizadas devem ser reaplicadas antes que você inicie a sincronização.</span><span class="sxs-lookup"><span data-stu-id="8322b-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="8322b-182">Ter um servidor em espera reserva - modo de preparo</span><span class="sxs-lookup"><span data-stu-id="8322b-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="8322b-183">Se você tiver um ambiente mais complexo, é recomendável ter um ou mais servidores em espera.</span><span class="sxs-lookup"><span data-stu-id="8322b-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="8322b-184">Durante a instalação, você pode habilitar um servidor em **modo de preparo**.</span><span class="sxs-lookup"><span data-stu-id="8322b-184">During installation, you can enable a server to be in **staging mode**.</span></span>

<span data-ttu-id="8322b-185">Para obter mais informações, consulte [Modo de preparo](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="8322b-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="8322b-186">Usar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="8322b-186">Use virtual machines</span></span>
<span data-ttu-id="8322b-187">Um método comum e com suporte é a execução do mecanismo de sincronização em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8322b-187">A common and supported method is to run the sync engine in a virtual machine.</span></span> <span data-ttu-id="8322b-188">Se o host tiver um problema, a imagem com o servidor do mecanismo de sincronização pode ser migrada para outro servidor.</span><span class="sxs-lookup"><span data-stu-id="8322b-188">In case the host has an issue, the image with the sync engine server can be migrated to another server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="8322b-189">Alta disponibilidade do SQL</span><span class="sxs-lookup"><span data-stu-id="8322b-189">SQL High Availability</span></span>
<span data-ttu-id="8322b-190">Se você não estiver usando o SQL Server Express que vem com o Azure AD Connect, a alta disponibilidade do SQL Server também deverá ser considerada.</span><span class="sxs-lookup"><span data-stu-id="8322b-190">If you are not using the SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="8322b-191">As soluções de alta disponibilidade com suporte incluem o clustering de SQL e AOA (Grupos de Disponibilidade AlwaysOn).</span><span class="sxs-lookup"><span data-stu-id="8322b-191">The high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="8322b-192">Soluções sem suporte incluem espelhamento.</span><span class="sxs-lookup"><span data-stu-id="8322b-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="8322b-193">Suporte para SQL AOA foi adicionado ao Azure AD Connect versão 1.1.524.0.</span><span class="sxs-lookup"><span data-stu-id="8322b-193">Support for SQL AOA was added to Azure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="8322b-194">Você deve habilitar o SQL AOA antes de instalar o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8322b-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="8322b-195">Durante a instalação, o Azure AD Connect detecta se a instância do SQL fornecida está habilitada para SQL AOA ou não.</span><span class="sxs-lookup"><span data-stu-id="8322b-195">During installation, Azure AD Connect detects whether the SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="8322b-196">Se o SQL AOA estiver habilitado, o Azure AD Connect descobrirá melhor se o AOA SQL está configurado para usar replicação síncrona ou replicação assíncrona.</span><span class="sxs-lookup"><span data-stu-id="8322b-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured to use synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="8322b-197">Ao configurar o Ouvinte do Grupo de Disponibilidade, é recomendável definir a propriedade RegisterAllProvidersIP como 0.</span><span class="sxs-lookup"><span data-stu-id="8322b-197">When setting up the Availability Group Listener, it is recommended that you set the RegisterAllProvidersIP property to 0.</span></span> <span data-ttu-id="8322b-198">Isso ocorre porque o Azure AD Connect atualmente usa o SQL Native Client para conectar-se ao SQL, e o SQL Native Client não dá suporte ao uso da propriedade MultiSubNetFailover.</span><span class="sxs-lookup"><span data-stu-id="8322b-198">This is because Azure AD Connect currently uses SQL Native Client to connect to SQL and SQL Native Client does not support the use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="8322b-199">Apêndice: CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="8322b-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="8322b-200">Consulte a seção [Verificar](#verify) para saber como usar esse script.</span><span class="sxs-lookup"><span data-stu-id="8322b-200">See the section [verify](#verify) on how to use this script.</span></span>

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve the file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader to deal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create the object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have the basics, go get the details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump the processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit the maximum users processed without completion... -ForegroundColor Yellow

        #export the collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment the output file counter
        $outputfilecount+=1

        #reset the collection and the user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need to bail out of the loop if no more users to process
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need to write out any users that didn't get picked up in a batch of 1000
#export the collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="8322b-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8322b-201">Next steps</span></span>
<span data-ttu-id="8322b-202">**Tópicos de visão geral**</span><span class="sxs-lookup"><span data-stu-id="8322b-202">**Overview topics**</span></span>  

* [<span data-ttu-id="8322b-203">Sincronização do Azure AD Connect: compreender e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="8322b-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="8322b-204">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8322b-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
