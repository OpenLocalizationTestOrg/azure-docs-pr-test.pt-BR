---
title: "Sincronização do Azure AD Connect: considerações e tarefas operacionais | Microsoft Docs"
description: "Este tópico descreve as tarefas operacionais para a sincronização do Azure AD Connect e como tooprepare para a operação neste componente."
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
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="062ab-103">Sincronização do Azure AD Connect: considerações e tarefas operacionais</span><span class="sxs-lookup"><span data-stu-id="062ab-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="062ab-104">Olá objetivo deste tópico é toodescribe as tarefas operacionais para a sincronização do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="062ab-104">hello objective of this topic is toodescribe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="062ab-105">Modo de preparo</span><span class="sxs-lookup"><span data-stu-id="062ab-105">Staging mode</span></span>
<span data-ttu-id="062ab-106">O modo de teste pode ser usado para vários cenários, incluindo:</span><span class="sxs-lookup"><span data-stu-id="062ab-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="062ab-107">Alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="062ab-107">High availability.</span></span>
* <span data-ttu-id="062ab-108">Teste e implantação de novas alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="062ab-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="062ab-109">Introduz um novo servidor e encerrar Olá antigo.</span><span class="sxs-lookup"><span data-stu-id="062ab-109">Introduce a new server and decommission hello old.</span></span>

<span data-ttu-id="062ab-110">Com um servidor no modo de preparo, você pode fazer alterações toohello configuração e visualizar Olá alterações antes de você ativar o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="062ab-110">With a server in staging mode, you can make changes toohello configuration and preview hello changes before you make hello server active.</span></span> <span data-ttu-id="062ab-111">Ele também permite importação completa toorun e sincronização completa tooverify que todas as alterações são esperadas antes de fazer essas alterações em seu ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="062ab-111">It also allows you toorun full import and full synchronization tooverify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="062ab-112">Durante a instalação, você pode selecionar Olá server toobe em **modo de preparo**.</span><span class="sxs-lookup"><span data-stu-id="062ab-112">During installation, you can select hello server toobe in **staging mode**.</span></span> <span data-ttu-id="062ab-113">Esta ação ativa de importação e sincronização de servidor de saudação, mas não executa qualquer exportações.</span><span class="sxs-lookup"><span data-stu-id="062ab-113">This action makes hello server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="062ab-114">Um servidor no modo de preparo não executa a sincronização de senha ou o write-back de senha, mesmo que esses recursos sejam selecionados durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="062ab-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="062ab-115">Quando você desabilita o modo de preparo, o servidor de saudação inicia a exportação, permite a sincronização de senha e permite que o write-back de senha.</span><span class="sxs-lookup"><span data-stu-id="062ab-115">When you disable staging mode, hello server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="062ab-116">Você ainda pode forçar uma exportação usando o Gerenciador de serviço de sincronização de saudação.</span><span class="sxs-lookup"><span data-stu-id="062ab-116">You can still force an export by using hello synchronization service manager.</span></span>

<span data-ttu-id="062ab-117">Um servidor no modo de preparo continua tooreceive alterações do Active Directory e o AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="062ab-117">A server in staging mode continues tooreceive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="062ab-118">Ele sempre tem uma cópia das alterações mais recentes hello e podem levar muito rápido sobre responsabilidades de saudação do outro servidor.</span><span class="sxs-lookup"><span data-stu-id="062ab-118">It always has a copy of hello latest changes and can very fast take over hello responsibilities of another server.</span></span> <span data-ttu-id="062ab-119">Se você tornar o servidor primário de tooyour de alterações de configuração, é sua responsabilidade toomake Olá mesmo servidor toohello de alterações no modo de preparo.</span><span class="sxs-lookup"><span data-stu-id="062ab-119">If you make configuration changes tooyour primary server, it is your responsibility toomake hello same changes toohello server in staging mode.</span></span>

<span data-ttu-id="062ab-120">Para aqueles com conhecimento das tecnologias mais antigas de sincronização, Olá modo de preparo é diferente porque o servidor de saudação tem seu próprio banco de dados do SQL.</span><span class="sxs-lookup"><span data-stu-id="062ab-120">For those of you with knowledge of older sync technologies, hello staging mode is different since hello server has its own SQL database.</span></span> <span data-ttu-id="062ab-121">Essa arquitetura permite Olá modo servidor toobe localizado em um datacenter diferente de preparo.</span><span class="sxs-lookup"><span data-stu-id="062ab-121">This architecture allows hello staging mode server toobe located in a different datacenter.</span></span>

### <a name="verify-hello-configuration-of-a-server"></a><span data-ttu-id="062ab-122">Verificar a configuração de saudação de um servidor</span><span class="sxs-lookup"><span data-stu-id="062ab-122">Verify hello configuration of a server</span></span>
<span data-ttu-id="062ab-123">tooapply esse método, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="062ab-123">tooapply this method, follow these steps:</span></span>

1. [<span data-ttu-id="062ab-124">Preparar</span><span class="sxs-lookup"><span data-stu-id="062ab-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="062ab-125">Configuração</span><span class="sxs-lookup"><span data-stu-id="062ab-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="062ab-126">Importar e sincronizar</span><span class="sxs-lookup"><span data-stu-id="062ab-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="062ab-127">Verificar</span><span class="sxs-lookup"><span data-stu-id="062ab-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="062ab-128">Servidor ativo do comutador</span><span class="sxs-lookup"><span data-stu-id="062ab-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="062ab-129">Preparar</span><span class="sxs-lookup"><span data-stu-id="062ab-129">Prepare</span></span>
1. <span data-ttu-id="062ab-130">Instalar o Azure AD Connect, selecione **modo de preparo**e desmarque **iniciar a sincronização** na última página Olá no Assistente de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="062ab-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on hello last page in hello installation wizard.</span></span> <span data-ttu-id="062ab-131">Este modo permite o mecanismo de sincronização de saudação toorun manualmente.</span><span class="sxs-lookup"><span data-stu-id="062ab-131">This mode allows you toorun hello sync engine manually.</span></span>
   <span data-ttu-id="062ab-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="062ab-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="062ab-133">Logoff/logon logon e de saudação iniciar no menu, selecione **serviço de sincronização**.</span><span class="sxs-lookup"><span data-stu-id="062ab-133">Sign off/sign in and from hello start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="062ab-134">Configuração</span><span class="sxs-lookup"><span data-stu-id="062ab-134">Configuration</span></span>
<span data-ttu-id="062ab-135">Se você tiver feito alterações personalizadas toohello primária deseja toocompare Olá configuração e com hello servidor de preparo, em seguida, use [Documentador de configuração do Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="062ab-135">If you have made custom changes toohello primary server and want toocompare hello configuration with hello staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="062ab-136">Importar e sincronizar</span><span class="sxs-lookup"><span data-stu-id="062ab-136">Import and Synchronize</span></span>
1. <span data-ttu-id="062ab-137">Selecione **conectores**, e selecione Olá primeiro conector com o tipo de saudação **serviços de domínio do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="062ab-137">Select **Connectors**, and select hello first Connector with hello type **Active Directory Domain Services**.</span></span> <span data-ttu-id="062ab-138">Clique em **Executar**, selecione **Importação completa** e **OK**.</span><span class="sxs-lookup"><span data-stu-id="062ab-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="062ab-139">Siga estas etapas para todos os Conectores desse tipo.</span><span class="sxs-lookup"><span data-stu-id="062ab-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="062ab-140">Selecione Olá conector com o tipo **do Active Directory do Azure (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="062ab-140">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="062ab-141">Clique em **Executar**, selecione **Importação completa** e **OK**.</span><span class="sxs-lookup"><span data-stu-id="062ab-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="062ab-142">Certifique-se de guia Olá conectores ainda está selecionado.</span><span class="sxs-lookup"><span data-stu-id="062ab-142">Make sure hello tab Connectors is still selected.</span></span> <span data-ttu-id="062ab-143">Para cada Conector com tipo **Active Directory Domain Services**, clique em **Executar**, selecione **Sincronização Delta** e **OK**.</span><span class="sxs-lookup"><span data-stu-id="062ab-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="062ab-144">Selecione Olá conector com o tipo **do Active Directory do Azure (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="062ab-144">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="062ab-145">Clique em **Executar**, selecione **Sincronização Delta** e **OK**.</span><span class="sxs-lookup"><span data-stu-id="062ab-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="062ab-146">Você tem agora exportação preparada altera tooAzure AD e AD local (se você estiver usando a implantação híbrida do Exchange).</span><span class="sxs-lookup"><span data-stu-id="062ab-146">You have now staged export changes tooAzure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="062ab-147">as próximas etapas Olá permitem tooinspect novidades sobre toochange antes de você realmente iniciar Olá exportar toohello diretórios.</span><span class="sxs-lookup"><span data-stu-id="062ab-147">hello next steps allow you tooinspect what is about toochange before you actually start hello export toohello directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="062ab-148">Verificar</span><span class="sxs-lookup"><span data-stu-id="062ab-148">Verify</span></span>
1. <span data-ttu-id="062ab-149">Inicie um prompt de comando e vá muito`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="062ab-149">Start a cmd prompt and go too`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="062ab-150">Executar: `csexport "Name of Connector" %temp%\export.xml /f:x` nome de saudação do hello conector pode ser encontrado no serviço de sincronização.</span><span class="sxs-lookup"><span data-stu-id="062ab-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` hello name of hello Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="062ab-151">Ele tem um too"contoso.com de nome semelhante – AAD" do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="062ab-151">It has a name similar too"contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="062ab-152">Copie o script do PowerShell de saudação da seção Olá [CSAnalyzer](#appendix-csanalyzer) tooa arquivo chamado `csanalyzer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="062ab-152">Copy hello PowerShell script from hello section [CSAnalyzer](#appendix-csanalyzer) tooa file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="062ab-153">Abra uma janela do PowerShell e procurar toohello pasta em que você criou o script do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="062ab-153">Open a PowerShell window and browse toohello folder where you created hello PowerShell script.</span></span>
5. <span data-ttu-id="062ab-154">Execute: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="062ab-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="062ab-155">Agora você tem um arquivo chamado **processedusers1.csv** que pode ser examinado no Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="062ab-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="062ab-156">TooAzure toobe exportado de todas as alterações de teste AD são encontrados nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="062ab-156">All changes staged toobe exported tooAzure AD are found in this file.</span></span>
7. <span data-ttu-id="062ab-157">Faça as alterações necessárias toohello dados ou a configuração e execute estas etapas novamente (importar e sincronizar e verifique se) até Olá alterações sobre toobe exportado são esperadas.</span><span class="sxs-lookup"><span data-stu-id="062ab-157">Make necessary changes toohello data or configuration and run these steps again (Import and Synchronize and Verify) until hello changes that are about toobe exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="062ab-158">Servidor ativo do comutador</span><span class="sxs-lookup"><span data-stu-id="062ab-158">Switch active server</span></span>
1. <span data-ttu-id="062ab-159">No servidor ativo no momento do hello, desative o servidor de saudação (DirSync/FIM/Azure AD Sync) para que ele não esteja exportando tooAzure AD ou defina-o no modo (Azure AD Connect) de preparo.</span><span class="sxs-lookup"><span data-stu-id="062ab-159">On hello currently active server, either turn off hello server (DirSync/FIM/Azure AD Sync) so it is not exporting tooAzure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="062ab-160">Execute o Assistente de instalação de saudação no servidor de saudação em **modo de preparo** e desabilitar **modo de preparo**.</span><span class="sxs-lookup"><span data-stu-id="062ab-160">Run hello installation wizard on hello server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="062ab-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="062ab-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="062ab-162">Recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="062ab-162">Disaster recovery</span></span>
<span data-ttu-id="062ab-163">Parte do design de implementação de saudação é tooplan para quais toodo caso haja um desastre em que você perder o servidor de sincronização de saudação.</span><span class="sxs-lookup"><span data-stu-id="062ab-163">Part of hello implementation design is tooplan for what toodo in case there is a disaster where you lose hello sync server.</span></span> <span data-ttu-id="062ab-164">Há diferentes modelos toouse e quais um toouse depende de vários fatores, incluindo:</span><span class="sxs-lookup"><span data-stu-id="062ab-164">There are different models toouse and which one toouse depends on several factors including:</span></span>

* <span data-ttu-id="062ab-165">Qual é sua tolerância de não ser capaz de fazer alterações de tooobjects no AD do Azure durante o tempo de inatividade Olá?</span><span class="sxs-lookup"><span data-stu-id="062ab-165">What is your tolerance for not being able make changes tooobjects in Azure AD during hello downtime?</span></span>
* <span data-ttu-id="062ab-166">Se você usar a sincronização de senha, os usuários de saudação aceitar que tem senha antiga de saudação toouse no AD do Azure caso eles alteração-lo no local?</span><span class="sxs-lookup"><span data-stu-id="062ab-166">If you use password synchronization, do hello users accept that they have toouse hello old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="062ab-167">Você tem uma dependência em operações em tempo real, como write-back de senha?</span><span class="sxs-lookup"><span data-stu-id="062ab-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="062ab-168">Dependendo da saudação respostas toothese perguntas e a política da sua organização, uma saudação estratégias a seguir pode ser implementada:</span><span class="sxs-lookup"><span data-stu-id="062ab-168">Depending on hello answers toothese questions and your organization’s policy, one of hello following strategies can be implemented:</span></span>

* <span data-ttu-id="062ab-169">Recriar quando necessário.</span><span class="sxs-lookup"><span data-stu-id="062ab-169">Rebuild when needed.</span></span>
* <span data-ttu-id="062ab-170">Ter um servidor em espera reserva, conhecido como **modo de preparo**.</span><span class="sxs-lookup"><span data-stu-id="062ab-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="062ab-171">Usar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="062ab-171">Use virtual machines.</span></span>

<span data-ttu-id="062ab-172">Se você não usar Olá SQL Express banco de dados interno, você também deve revisar Olá [alta disponibilidade do SQL](#sql-high-availability) seção.</span><span class="sxs-lookup"><span data-stu-id="062ab-172">If you do not use hello built-in SQL Express database, then you should also review hello [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="062ab-173">Recriar quando necessário</span><span class="sxs-lookup"><span data-stu-id="062ab-173">Rebuild when needed</span></span>
<span data-ttu-id="062ab-174">Uma estratégia viável é tooplan para a recriação do servidor quando necessário.</span><span class="sxs-lookup"><span data-stu-id="062ab-174">A viable strategy is tooplan for a server rebuild when needed.</span></span> <span data-ttu-id="062ab-175">Geralmente, instalando Olá mecanismo de sincronização e Olá importação inicial e sincronização pode ser concluída dentro de algumas horas.</span><span class="sxs-lookup"><span data-stu-id="062ab-175">Usually, installing hello sync engine and do hello initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="062ab-176">Se não houver um servidor de reserva disponíveis, é possível tootemporarily usar um mecanismo de sincronização de saudação do domínio controlador toohost.</span><span class="sxs-lookup"><span data-stu-id="062ab-176">If there isn’t a spare server available, it is possible tootemporarily use a domain controller toohost hello sync engine.</span></span>

<span data-ttu-id="062ab-177">servidor do mecanismo de sincronização de saudação não armazenam qualquer estado sobre objetos Olá para que o banco de dados de saudação poderá ser reconstruído com dados de saudação no Active Directory e o AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="062ab-177">hello sync engine server does not store any state about hello objects so hello database can be rebuilt from hello data in Active Directory and Azure AD.</span></span> <span data-ttu-id="062ab-178">Olá **sourceAnchor** atributo é usado toojoin Olá objetos do local e Olá nuvem.</span><span class="sxs-lookup"><span data-stu-id="062ab-178">hello **sourceAnchor** attribute is used toojoin hello objects from on-premises and hello cloud.</span></span> <span data-ttu-id="062ab-179">Se você recriar Olá servidor com objetos locais existentes e Olá nuvem, em seguida, o mecanismo de sincronização de saudação corresponde a esses objetos juntos novamente na reinstalação.</span><span class="sxs-lookup"><span data-stu-id="062ab-179">If you rebuild hello server with existing objects on-premises and hello cloud, then hello sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="062ab-180">coisas Olá necessário toodocument e salvar são Olá alterações de configuração toohello server, como regras de sincronização e filtragem.</span><span class="sxs-lookup"><span data-stu-id="062ab-180">hello things you need toodocument and save are hello configuration changes made toohello server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="062ab-181">Essas configurações personalizadas devem ser reaplicadas antes que você inicie a sincronização.</span><span class="sxs-lookup"><span data-stu-id="062ab-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="062ab-182">Ter um servidor em espera reserva - modo de preparo</span><span class="sxs-lookup"><span data-stu-id="062ab-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="062ab-183">Se você tiver um ambiente mais complexo, é recomendável ter um ou mais servidores em espera.</span><span class="sxs-lookup"><span data-stu-id="062ab-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="062ab-184">Durante a instalação, você pode habilitar um toobe de servidor em **modo de preparo**.</span><span class="sxs-lookup"><span data-stu-id="062ab-184">During installation, you can enable a server toobe in **staging mode**.</span></span>

<span data-ttu-id="062ab-185">Para obter mais informações, consulte [Modo de preparo](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="062ab-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="062ab-186">Usar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="062ab-186">Use virtual machines</span></span>
<span data-ttu-id="062ab-187">Um método comum e com suporte é o mecanismo de sincronização de saudação toorun em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="062ab-187">A common and supported method is toorun hello sync engine in a virtual machine.</span></span> <span data-ttu-id="062ab-188">No caso de host Olá tem um problema, a imagem de Olá com o servidor do mecanismo de sincronização de saudação pode ser migrado tooanother server.</span><span class="sxs-lookup"><span data-stu-id="062ab-188">In case hello host has an issue, hello image with hello sync engine server can be migrated tooanother server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="062ab-189">Alta disponibilidade do SQL</span><span class="sxs-lookup"><span data-stu-id="062ab-189">SQL High Availability</span></span>
<span data-ttu-id="062ab-190">Se você não estiver usando o SQL Server Express que vem com o Azure AD Connect de saudação, alta disponibilidade para o SQL Server também deve ser considerada.</span><span class="sxs-lookup"><span data-stu-id="062ab-190">If you are not using hello SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="062ab-191">soluções de alta disponibilidade Olá com suporte incluem o clustering de SQL e AOA (grupos de disponibilidade AlwaysOn).</span><span class="sxs-lookup"><span data-stu-id="062ab-191">hello high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="062ab-192">Soluções sem suporte incluem espelhamento.</span><span class="sxs-lookup"><span data-stu-id="062ab-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="062ab-193">Suporte para SQL AOA foi adicionado tooAzure AD Connect versão 1.1.524.0.</span><span class="sxs-lookup"><span data-stu-id="062ab-193">Support for SQL AOA was added tooAzure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="062ab-194">Você deve habilitar o SQL AOA antes de instalar o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="062ab-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="062ab-195">Durante a instalação, o Azure AD Connect detecta se a instância SQL Olá fornecida está habilitada para SQL AOA, ou não.</span><span class="sxs-lookup"><span data-stu-id="062ab-195">During installation, Azure AD Connect detects whether hello SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="062ab-196">Se SQL AOA estiver habilitado, o Azure AD Connect mais descobre se SQL AOA é replicação síncrona toouse configurado ou replicação assíncrona.</span><span class="sxs-lookup"><span data-stu-id="062ab-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured toouse synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="062ab-197">Ao configurar o ouvinte do grupo de disponibilidade do hello, é recomendável que você defina Olá RegisterAllProvidersIP propriedade too0.</span><span class="sxs-lookup"><span data-stu-id="062ab-197">When setting up hello Availability Group Listener, it is recommended that you set hello RegisterAllProvidersIP property too0.</span></span> <span data-ttu-id="062ab-198">Isso ocorre porque a conexão do AD do Azure atualmente usa o SQL Native Client tooconnect tooSQL e SQL Native Client não dá suporte para uso de saudação da propriedade MultiSubNetFailover.</span><span class="sxs-lookup"><span data-stu-id="062ab-198">This is because Azure AD Connect currently uses SQL Native Client tooconnect tooSQL and SQL Native Client does not support hello use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="062ab-199">Apêndice: CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="062ab-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="062ab-200">Consulte a seção Olá [verificar](#verify) sobre como toouse esse script.</span><span class="sxs-lookup"><span data-stu-id="062ab-200">See hello section [verify](#verify) on how toouse this script.</span></span>

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

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
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

    #now that we have hello basics, go get hello details

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

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="062ab-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="062ab-201">Next steps</span></span>
<span data-ttu-id="062ab-202">**Tópicos de visão geral**</span><span class="sxs-lookup"><span data-stu-id="062ab-202">**Overview topics**</span></span>  

* [<span data-ttu-id="062ab-203">Sincronização do Azure AD Connect: compreender e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="062ab-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="062ab-204">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="062ab-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
