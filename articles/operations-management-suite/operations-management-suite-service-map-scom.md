---
title: "integração com o System Center Operations Manager com o mapa de aaaService | Microsoft Docs"
description: "Mapa de serviço é uma solução Operations Management Suite que detecta automaticamente os componentes do aplicativo no Windows e mapas e sistemas Linux Olá comunicação entre serviços. Este artigo discute o uso do mapa de serviço tooautomatically criar diagramas de aplicativo distribuído no Operations Manager."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="95ce1-104">Integração do Mapa do Serviço com o System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="95ce1-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="95ce1-105">Esse recurso está em uma versão prévia.</span><span class="sxs-lookup"><span data-stu-id="95ce1-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="95ce1-106">Mapa de serviço do Operations Management Suite detecta os componentes de aplicativos em sistemas Windows e Linux e mapeia a comunicação entre serviços Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="95ce1-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="95ce1-107">Mapa de serviço permite que você tooview caminho Olá servidores pensar neles, como sistemas interconectados que fornecem serviços essenciais.</span><span class="sxs-lookup"><span data-stu-id="95ce1-107">Service Map allows you tooview your servers hello way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="95ce1-108">Mapa de serviço mostra conexões entre servidores, processos e portas em qualquer arquitetura conectado por TCP, sem nenhuma configuração necessária além de instalação de saudação de um agente.</span><span class="sxs-lookup"><span data-stu-id="95ce1-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides hello installation of an agent.</span></span> <span data-ttu-id="95ce1-109">Para obter mais informações, consulte Olá [documentação de mapa de serviço](operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="95ce1-109">For more information, see hello [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="95ce1-110">Com essa integração entre o mapa de serviço e o System Center Operations Manager, você pode criar automaticamente diagramas de aplicativo distribuído no Operations Manager que se baseiam em mapas de dependência dinâmica de saudação no mapa de serviço.</span><span class="sxs-lookup"><span data-stu-id="95ce1-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on hello dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95ce1-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="95ce1-111">Prerequisites</span></span>
* <span data-ttu-id="95ce1-112">Um grupo de gerenciamento do Operations Manager que gerencia um conjunto de servidores.</span><span class="sxs-lookup"><span data-stu-id="95ce1-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="95ce1-113">Um espaço de trabalho do Operations Management Suite com hello solução Mapa de serviço habilitada.</span><span class="sxs-lookup"><span data-stu-id="95ce1-113">An Operations Management Suite workspace with hello Service Map solution enabled.</span></span>
* <span data-ttu-id="95ce1-114">Um conjunto de servidores (pelo menos um) que estão sendo gerenciados pelo Operations Manager e enviar dados tooService mapa.</span><span class="sxs-lookup"><span data-stu-id="95ce1-114">A set of servers (at least one) that are being managed by Operations Manager and sending data tooService Map.</span></span> <span data-ttu-id="95ce1-115">Há suporte para servidores Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="95ce1-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="95ce1-116">Uma entidade de serviço com acesso toohello assinatura do Azure que está associada com o espaço de trabalho do hello Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="95ce1-116">A service principal with access toohello Azure subscription that is associated with hello Operations Management Suite workspace.</span></span> <span data-ttu-id="95ce1-117">Para obter mais informações, vá muito[criar uma entidade de serviço](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="95ce1-117">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-hello-service-map-management-pack"></a><span data-ttu-id="95ce1-118">Instalar pacote de gerenciamento de mapa de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="95ce1-118">Install hello Service Map management pack</span></span>
<span data-ttu-id="95ce1-119">Você habilitar a integração de saudação entre o Operations Manager e o mapa de serviço, importando Olá Microsoft.SystemCenter.ServiceMap pacote de gerenciamento (Microsoft.SystemCenter.ServiceMap.mpb).</span><span class="sxs-lookup"><span data-stu-id="95ce1-119">You enable hello integration between Operations Manager and Service Map by importing hello Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="95ce1-120">pacote de saudação contém Olá pacotes de gerenciamento a seguir:</span><span class="sxs-lookup"><span data-stu-id="95ce1-120">hello bundle contains hello following management packs:</span></span>
* <span data-ttu-id="95ce1-121">Exibições de Aplicativo do Mapa do Serviço da Microsoft</span><span class="sxs-lookup"><span data-stu-id="95ce1-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="95ce1-122">Mapa do Serviço Interno do Microsoft System Center</span><span class="sxs-lookup"><span data-stu-id="95ce1-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="95ce1-123">Substituições do Mapa do Serviço do Microsoft System Center</span><span class="sxs-lookup"><span data-stu-id="95ce1-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="95ce1-124">Mapa do Serviço do Microsoft System Center</span><span class="sxs-lookup"><span data-stu-id="95ce1-124">Microsoft System Center Service Map</span></span>

## <a name="configure-hello-service-map-integration"></a><span data-ttu-id="95ce1-125">Configurar a integração do mapa de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="95ce1-125">Configure hello Service Map integration</span></span>
<span data-ttu-id="95ce1-126">Depois de instalar o pacote de gerenciamento de mapa de serviço hello, um novo nó, **mapa de serviço**, é exibido em **Operations Management Suite** em Olá **administração** painel.</span><span class="sxs-lookup"><span data-stu-id="95ce1-126">After you install hello Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in hello **Administration** pane.</span></span> 

<span data-ttu-id="95ce1-127">tooconfigure integração com o mapa de serviço, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="95ce1-127">tooconfigure Service Map integration, do hello following:</span></span>

1. <span data-ttu-id="95ce1-128">Assistente de configuração de saudação do tooopen, do hello **visão geral do mapa de serviço** painel, clique em **adicionar espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="95ce1-128">tooopen hello configuration wizard, in hello **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![Painel Visão Geral do Mapa do Serviço](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="95ce1-130">Em Olá **configuração de Conexão** janela, digite o nome do locatário hello ou ID, ID de aplicativo (também conhecido como nome de usuário de saudação ou clientID) e senha da entidade de serviço hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="95ce1-130">In hello **Connection Configuration** window, enter hello tenant name or ID, application ID (also known as hello username or clientID), and password of hello service principal, and then click **Next**.</span></span> <span data-ttu-id="95ce1-131">Para obter mais informações, vá muito[criar uma entidade de serviço](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="95ce1-131">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

    ![janela de configuração de Conexão de saudação](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="95ce1-133">Em Olá **assinatura seleção** janela, selecione Olá assinatura do Azure, o grupo de recursos do Azure (Olá que contém o espaço de trabalho do hello Operations Management Suite) e o espaço de trabalho do Operations Management Suite e, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="95ce1-133">In hello **Subscription Selection** window, select hello Azure subscription, Azure resource group (hello one that contains hello Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![Olá espaço de trabalho de configuração do Operations Manager](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="95ce1-135">Em Olá **seleção de grupo do computador** janela, que você escolha quais grupos de computadores do mapa de serviço você deseja toosync tooOperations Manager.</span><span class="sxs-lookup"><span data-stu-id="95ce1-135">In hello **Machine Group Selection** window, you choose which Service Map Machine Groups you want toosync tooOperations Manager.</span></span> <span data-ttu-id="95ce1-136">Clique em **adicionar ou remover grupos de computadores**, escolha grupos na lista de saudação do **grupos de computadores disponíveis**e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="95ce1-136">Click **Add/Remove Machine Groups**, choose groups from hello list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="95ce1-137">Quando você terminar de selecionar os grupos, clique em **Okey** toofinish.</span><span class="sxs-lookup"><span data-stu-id="95ce1-137">When you are finished selecting groups, click **Ok** toofinish.</span></span>
    
    ![Olá grupos de máquina de configuração do Operations Manager](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="95ce1-139">Em Olá **seleção de servidor** janela, que você configurar Olá grupo de servidores de mapa de serviço com servidores Olá que você deseja toosync entre o Operations Manager e o mapa de serviço.</span><span class="sxs-lookup"><span data-stu-id="95ce1-139">In hello **Server Selection** window, you configure hello Service Map Servers Group with hello servers that you want toosync between Operations Manager and Service Map.</span></span> <span data-ttu-id="95ce1-140">Clique em **Adicionar/Remover Servidores**.</span><span class="sxs-lookup"><span data-stu-id="95ce1-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="95ce1-141">Para Olá integração toobuild um diagrama de aplicativo distribuído para um servidor, o servidor de saudação deve ser:</span><span class="sxs-lookup"><span data-stu-id="95ce1-141">For hello integration toobuild a distributed application diagram for a server, hello server must be:</span></span>

    * <span data-ttu-id="95ce1-142">Gerenciado pelo Operations Manager</span><span class="sxs-lookup"><span data-stu-id="95ce1-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="95ce1-143">Gerenciado pelo Mapa do Serviço</span><span class="sxs-lookup"><span data-stu-id="95ce1-143">Managed by Service Map</span></span>
    * <span data-ttu-id="95ce1-144">Listado em Olá grupo de servidores de mapa de serviço</span><span class="sxs-lookup"><span data-stu-id="95ce1-144">Listed in hello Service Map Servers Group</span></span>

    ![saudação de grupo de configuração do Operations Manager](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="95ce1-146">Opcional: Selecione toocommunicate de pool de recursos Olá servidor de gerenciamento com o Operations Management Suite e, em seguida, clique em **adicionar espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="95ce1-146">Optional: Select hello Management Server resource pool toocommunicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![saudação de Pool de recursos de configuração do Operations Manager](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="95ce1-148">Ele pode levar um minuto tooconfigure e registrar o espaço de trabalho do hello Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="95ce1-148">It might take a minute tooconfigure and register hello Operations Management Suite workspace.</span></span> <span data-ttu-id="95ce1-149">Depois de configurado, Operations Manager inicia a primeira sincronização de mapa de serviço saudação do Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="95ce1-149">After it is configured, Operations Manager initiates hello first Service Map sync from Operations Management Suite.</span></span>

    ![saudação de Pool de recursos de configuração do Operations Manager](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="95ce1-151">Monitorar o Mapa do Serviço</span><span class="sxs-lookup"><span data-stu-id="95ce1-151">Monitor Service Map</span></span>
<span data-ttu-id="95ce1-152">Depois que o espaço de trabalho do hello Operations Management Suite está conectado, uma nova pasta, o mapa de serviço, é exibida no hello **monitoramento** painel do console do Operations Manager hello.</span><span class="sxs-lookup"><span data-stu-id="95ce1-152">After hello Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in hello **Monitoring** pane of hello Operations Manager console.</span></span>

![Painel de monitoramento do Operations Manager Olá](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="95ce1-154">pasta de mapa de serviço Olá tem quatro nós:</span><span class="sxs-lookup"><span data-stu-id="95ce1-154">hello Service Map folder has four nodes:</span></span>
* <span data-ttu-id="95ce1-155">**Alertas ativos**: lista todos os alertas ativos do hello sobre comunicação Olá entre o Operations Manager e o mapa de serviço.</span><span class="sxs-lookup"><span data-stu-id="95ce1-155">**Active Alerts**: Lists all hello active alerts about hello communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="95ce1-156">Observe que esses alertas não estão sendo sincronizados tooOperations Gerenciador de alertas de Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="95ce1-156">Note that these alerts are not Operations Management Suite alerts being synced tooOperations Manager.</span></span> 

* <span data-ttu-id="95ce1-157">**Servidores**: listas Olá monitorado servidores configurados toosync do mapa de serviço.</span><span class="sxs-lookup"><span data-stu-id="95ce1-157">**Servers**: Lists hello monitored servers that are configured toosync from Service Map.</span></span>

    ![Painel de monitoramento de servidores do Operations Manager Olá](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="95ce1-159">**Exibições de dependência de grupo do computador**: lista todos os grupos de computadores que foram sincronizados de mapa de serviço.</span><span class="sxs-lookup"><span data-stu-id="95ce1-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="95ce1-160">Você pode clicar tooview qualquer grupo seu diagrama de aplicativo distribuído.</span><span class="sxs-lookup"><span data-stu-id="95ce1-160">You can click any group tooview its distributed application diagram.</span></span>

    ![diagrama de aplicativo distribuído do Operations Manager Olá](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="95ce1-162">**Exibições de Dependência de Servidor**: lista todos os servidores sincronizados por meio do Mapa do Serviço.</span><span class="sxs-lookup"><span data-stu-id="95ce1-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="95ce1-163">Você pode clicar tooview qualquer servidor em seu diagrama de aplicativo distribuído.</span><span class="sxs-lookup"><span data-stu-id="95ce1-163">You can click any server tooview its distributed application diagram.</span></span>

    ![diagrama de aplicativo distribuído do Operations Manager Olá](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a><span data-ttu-id="95ce1-165">Editar ou excluir o espaço de trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="95ce1-165">Edit or delete hello workspace</span></span>
<span data-ttu-id="95ce1-166">Você pode editar ou excluir espaço de trabalho de saudação configurado por meio de saudação **visão geral do mapa de serviço** painel (**administração** painel > **Operations Management Suite**  >  **Mapa de serviço**).</span><span class="sxs-lookup"><span data-stu-id="95ce1-166">You can edit or delete hello configured workspace through hello **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="95ce1-167">No momento, é possível configurar apenas um espaço de trabalho do Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="95ce1-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![Painel de espaço de trabalho do Operations Manager Editar Olá](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="95ce1-169">Configurar regras e substituições</span><span class="sxs-lookup"><span data-stu-id="95ce1-169">Configure rules and overrides</span></span>
<span data-ttu-id="95ce1-170">Uma regra, _Microsoft.SystemCenter.ServiceMapImport.Rule_, é criado tooperiodically informações de busca de mapa de serviço.</span><span class="sxs-lookup"><span data-stu-id="95ce1-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created tooperiodically fetch information from Service Map.</span></span> <span data-ttu-id="95ce1-171">intervalos de sincronização de toochange, você pode configurar substituições de regra da saudação (**criação** painel > **regras** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="95ce1-171">toochange sync timings, you can configure overrides of hello rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![janela de propriedades de substituições do Operations Manager Olá](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="95ce1-173">**Enabled**: habilite ou desabilite atualizações automáticas.</span><span class="sxs-lookup"><span data-stu-id="95ce1-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="95ce1-174">**IntervalMinutes**: redefinir o tempo de saudação entre as atualizações.</span><span class="sxs-lookup"><span data-stu-id="95ce1-174">**IntervalMinutes**: Reset hello time between updates.</span></span> <span data-ttu-id="95ce1-175">intervalo padrão de saudação é de uma hora.</span><span class="sxs-lookup"><span data-stu-id="95ce1-175">hello default interval is one hour.</span></span> <span data-ttu-id="95ce1-176">Se você quiser toosync server mapas com mais frequência, você pode alterar o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="95ce1-176">If you want toosync server maps more frequently, you can change hello value.</span></span>
* <span data-ttu-id="95ce1-177">**TimeoutSeconds**: redefinir o comprimento de saudação de tempo antes de solicitação de saudação expira.</span><span class="sxs-lookup"><span data-stu-id="95ce1-177">**TimeoutSeconds**: Reset hello length of time before hello request times out.</span></span> 
* <span data-ttu-id="95ce1-178">**TimeWindowMinutes**: janela de tempo de saudação de redefinição para consultar dados.</span><span class="sxs-lookup"><span data-stu-id="95ce1-178">**TimeWindowMinutes**: Reset hello time window for querying data.</span></span> <span data-ttu-id="95ce1-179">O padrão é uma janela de 60 minutos.</span><span class="sxs-lookup"><span data-stu-id="95ce1-179">Default is a 60-minute window.</span></span> <span data-ttu-id="95ce1-180">valor máximo de saudação permitido pelo mapa de serviço é 60 minutos.</span><span class="sxs-lookup"><span data-stu-id="95ce1-180">hello maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="95ce1-181">Problemas e limitações conhecidos</span><span class="sxs-lookup"><span data-stu-id="95ce1-181">Known issues and limitations</span></span>

<span data-ttu-id="95ce1-182">design atual Hello apresenta seguinte Olá limitações e problemas:</span><span class="sxs-lookup"><span data-stu-id="95ce1-182">hello current design presents hello following issues and limitations:</span></span>
* <span data-ttu-id="95ce1-183">Você só pode se conectar tooa único espaço de trabalho de Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="95ce1-183">You can only connect tooa single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="95ce1-184">Embora seja possível adicionar servidores toohello grupo de servidores de mapa de serviço manualmente por meio de saudação **criação** painel, Olá mapas para os servidores não são sincronizadas imediatamente.</span><span class="sxs-lookup"><span data-stu-id="95ce1-184">Although you can add servers toohello Service Map Servers Group manually through hello **Authoring** pane, hello maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="95ce1-185">Eles serão sincronizados do mapa de serviço durante a saudação próximo ciclo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="95ce1-185">They will be synced from Service Map during hello next sync cycle.</span></span>
* <span data-ttu-id="95ce1-186">Se você fizer alterações toohello distribuídas diagramas de aplicativos criados pelo pacote de gerenciamento hello, essas alterações provavelmente serão substituídas na próxima sincronização Olá com mapa de serviço.</span><span class="sxs-lookup"><span data-stu-id="95ce1-186">If you make any changes toohello Distributed Application Diagrams created by hello management pack, those changes will likely be overwritten on hello next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="95ce1-187">Criar uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="95ce1-187">Create a service principal</span></span>
<span data-ttu-id="95ce1-188">Para obter a documentação oficial do Azure sobre como criar uma entidade de serviço, consulte:</span><span class="sxs-lookup"><span data-stu-id="95ce1-188">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="95ce1-189">Criar uma entidade de serviço usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="95ce1-189">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="95ce1-190">Criar uma entidade de serviço usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="95ce1-190">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="95ce1-191">Criar uma entidade de serviço usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="95ce1-191">Create a service principal by using hello Azure portal</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="95ce1-192">Comentários</span><span class="sxs-lookup"><span data-stu-id="95ce1-192">Feedback</span></span>
<span data-ttu-id="95ce1-193">Você tem algum comentário sobre o Mapa de Serviço ou sobre esta documentação?</span><span class="sxs-lookup"><span data-stu-id="95ce1-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="95ce1-194">Visite nossa [página do User Voice](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), na qual você pode sugerir recursos ou votar em sugestões existentes.</span><span class="sxs-lookup"><span data-stu-id="95ce1-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
