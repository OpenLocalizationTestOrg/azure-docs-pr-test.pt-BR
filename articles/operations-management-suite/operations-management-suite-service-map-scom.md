---
title: "Integração do Mapa do Serviço com o System Center Operations Manager | Microsoft Docs"
description: "O Mapa do Serviço é uma solução do Operations Management Suite que descobre automaticamente os componentes de aplicativos em sistemas Windows e Linux e mapeia a comunicação entre os serviços. Este artigo aborda o uso do Mapa de Serviço para criar automaticamente diagramas de aplicativos distribuídos no Operations Manager."
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
ms.openlocfilehash: a7dbe54ffb4daa941c19b51ba263dd3d23b7a98b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="21670-104">Integração do Mapa do Serviço com o System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="21670-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="21670-105">Esse recurso está em uma versão prévia.</span><span class="sxs-lookup"><span data-stu-id="21670-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="21670-106">O Mapa do Serviço do Operations Management Suite descobre automaticamente os componentes de aplicativos em sistemas Windows e Linux e mapeia a comunicação entre os serviços.</span><span class="sxs-lookup"><span data-stu-id="21670-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="21670-107">O Mapa do Serviço permite que você exiba seus servidores da maneira desejada, como sistemas interconectados que fornecem serviços críticos.</span><span class="sxs-lookup"><span data-stu-id="21670-107">Service Map allows you to view your servers the way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="21670-108">O Mapa do Serviço mostra as conexões entre servidores, processos e portas em qualquer arquitetura conectada a TCP, sem nenhuma configuração necessária além da instalação de um agente.</span><span class="sxs-lookup"><span data-stu-id="21670-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides the installation of an agent.</span></span> <span data-ttu-id="21670-109">Para obter mais informações, consulte a [documentação do Mapa do Serviço](operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="21670-109">For more information, see the [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="21670-110">Com essa integração entre o Mapa do Serviço e o System Center Operations Manager, você pode criar automaticamente diagramas de aplicativos distribuídos no Operations Manager com base em mapas de dependência dinâmica no Mapa do Serviço.</span><span class="sxs-lookup"><span data-stu-id="21670-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on the dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21670-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="21670-111">Prerequisites</span></span>
* <span data-ttu-id="21670-112">Um grupo de gerenciamento do Operations Manager que gerencia um conjunto de servidores.</span><span class="sxs-lookup"><span data-stu-id="21670-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="21670-113">Um espaço de trabalho do Operations Management Suite com a solução Mapa do Serviço habilitada.</span><span class="sxs-lookup"><span data-stu-id="21670-113">An Operations Management Suite workspace with the Service Map solution enabled.</span></span>
* <span data-ttu-id="21670-114">Um conjunto de servidores (pelo menos um) que está sendo gerenciado pelo Operations Manager e enviando dados para o Mapa do Serviço.</span><span class="sxs-lookup"><span data-stu-id="21670-114">A set of servers (at least one) that are being managed by Operations Manager and sending data to Service Map.</span></span> <span data-ttu-id="21670-115">Há suporte para servidores Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="21670-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="21670-116">Uma entidade de serviço com acesso à assinatura do Azure associada ao espaço de trabalho do Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="21670-116">A service principal with access to the Azure subscription that is associated with the Operations Management Suite workspace.</span></span> <span data-ttu-id="21670-117">Para obter mais informações, acesse [Criar uma entidade de serviço](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="21670-117">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-the-service-map-management-pack"></a><span data-ttu-id="21670-118">Instalar o pacote de gerenciamento do Mapa do Serviço</span><span class="sxs-lookup"><span data-stu-id="21670-118">Install the Service Map management pack</span></span>
<span data-ttu-id="21670-119">A integração entre o Operations Manager e o Mapa do Serviço é habilitada pela importação do pacote de gerenciamento Microsoft.SystemCenter.ServiceMap (Microsoft.SystemCenter.ServiceMap.mpb).</span><span class="sxs-lookup"><span data-stu-id="21670-119">You enable the integration between Operations Manager and Service Map by importing the Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="21670-120">O pacote contém os seguintes pacotes de gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="21670-120">The bundle contains the following management packs:</span></span>
* <span data-ttu-id="21670-121">Exibições de Aplicativo do Mapa do Serviço da Microsoft</span><span class="sxs-lookup"><span data-stu-id="21670-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="21670-122">Mapa do Serviço Interno do Microsoft System Center</span><span class="sxs-lookup"><span data-stu-id="21670-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="21670-123">Substituições do Mapa do Serviço do Microsoft System Center</span><span class="sxs-lookup"><span data-stu-id="21670-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="21670-124">Mapa do Serviço do Microsoft System Center</span><span class="sxs-lookup"><span data-stu-id="21670-124">Microsoft System Center Service Map</span></span>

## <a name="configure-the-service-map-integration"></a><span data-ttu-id="21670-125">Configurar a integração do Mapa do Serviço</span><span class="sxs-lookup"><span data-stu-id="21670-125">Configure the Service Map integration</span></span>
<span data-ttu-id="21670-126">Depois de instalar o pacote de gerenciamento do Mapa do Serviço, um novo nó, **Mapa do Serviço**, é exibido em **Operations Management Suite** no painel **Administração**.</span><span class="sxs-lookup"><span data-stu-id="21670-126">After you install the Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in the **Administration** pane.</span></span> 

<span data-ttu-id="21670-127">Para configurar a integração do Mapa do Serviço, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="21670-127">To configure Service Map integration, do the following:</span></span>

1. <span data-ttu-id="21670-128">Para abrir o assistente de configuração, no painel **Visão Geral do Mapa do Serviço**, clique em **Adicionar espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="21670-128">To open the configuration wizard, in the **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![Painel Visão Geral do Mapa do Serviço](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="21670-130">Na janela **Configuração da Conexão**, insira o nome ou a ID do locatário, a ID do aplicativo (também conhecida como o nome de usuário ou a clientID) e a senha da entidade de serviço e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="21670-130">In the **Connection Configuration** window, enter the tenant name or ID, application ID (also known as the username or clientID), and password of the service principal, and then click **Next**.</span></span> <span data-ttu-id="21670-131">Para obter mais informações, acesse [Criar uma entidade de serviço](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="21670-131">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

    ![A janela Configuração da Conexão](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="21670-133">Na janela **Seleção de Assinatura**, selecione a assinatura do Azure, o grupo de recursos do Azure (aquele que contém o espaço de trabalho do Operations Management Suite) e o espaço de trabalho do Operations Management Suite e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="21670-133">In the **Subscription Selection** window, select the Azure subscription, Azure resource group (the one that contains the Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![O espaço de trabalho de configuração do Operations Manager](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="21670-135">No **seleção de grupo do computador** janela, que você escolha quais grupos de máquina do mapa de serviço que deseja sincronizar com o Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="21670-135">In the **Machine Group Selection** window, you choose which Service Map Machine Groups you want to sync to Operations Manager.</span></span> <span data-ttu-id="21670-136">Clique em **adicionar ou remover grupos de computadores**, escolha grupos na lista de **grupos de computadores disponíveis**e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="21670-136">Click **Add/Remove Machine Groups**, choose groups from the list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="21670-137">Quando você terminar de selecionar os grupos, clique em **OK** para concluir.</span><span class="sxs-lookup"><span data-stu-id="21670-137">When you are finished selecting groups, click **Ok** to finish.</span></span>
    
    ![Os grupos de computadores de configuração do Operations Manager](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="21670-139">Na janela **Seleção de Servidor**, você configura o Grupo de Servidores do Mapa do Serviço com os servidores que você deseja sincronizar entre o Operations Manager e o Mapa do Serviço.</span><span class="sxs-lookup"><span data-stu-id="21670-139">In the **Server Selection** window, you configure the Service Map Servers Group with the servers that you want to sync between Operations Manager and Service Map.</span></span> <span data-ttu-id="21670-140">Clique em **Adicionar/Remover Servidores**.</span><span class="sxs-lookup"><span data-stu-id="21670-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="21670-141">Para que a integração crie um diagrama de aplicativo distribuído para um servidor, o servidor deve ser/estar:</span><span class="sxs-lookup"><span data-stu-id="21670-141">For the integration to build a distributed application diagram for a server, the server must be:</span></span>

    * <span data-ttu-id="21670-142">Gerenciado pelo Operations Manager</span><span class="sxs-lookup"><span data-stu-id="21670-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="21670-143">Gerenciado pelo Mapa do Serviço</span><span class="sxs-lookup"><span data-stu-id="21670-143">Managed by Service Map</span></span>
    * <span data-ttu-id="21670-144">Listado no Grupo de Servidores do Mapa do Serviço</span><span class="sxs-lookup"><span data-stu-id="21670-144">Listed in the Service Map Servers Group</span></span>

    ![O grupo de configuração do Operations Manager](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="21670-146">Opcional: selecione o pool de recursos do Servidor de Gerenciamento para se comunicar com o Operations Management Suite e, em seguida, clique em **Adicionar Espaço de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="21670-146">Optional: Select the Management Server resource pool to communicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![O pool de recursos de configuração do Operations Manager](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="21670-148">Pode levar alguns minutos para configurar e registrar o espaço de trabalho do Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="21670-148">It might take a minute to configure and register the Operations Management Suite workspace.</span></span> <span data-ttu-id="21670-149">Depois que ele for configurado, o Operations Manager iniciará a primeira sincronização do Mapa do Serviço por meio do Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="21670-149">After it is configured, Operations Manager initiates the first Service Map sync from Operations Management Suite.</span></span>

    ![O pool de recursos de configuração do Operations Manager](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="21670-151">Monitorar o Mapa do Serviço</span><span class="sxs-lookup"><span data-stu-id="21670-151">Monitor Service Map</span></span>
<span data-ttu-id="21670-152">Depois que o espaço de trabalho do Operations Management Suite estiver conectado, uma nova pasta, Mapa do Serviço, será exibida no painel **Monitoramento** do console do Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="21670-152">After the Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in the **Monitoring** pane of the Operations Manager console.</span></span>

![O painel Monitoramento do Operations Manager](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="21670-154">A pasta do Mapa do Serviço tem quatro nós:</span><span class="sxs-lookup"><span data-stu-id="21670-154">The Service Map folder has four nodes:</span></span>
* <span data-ttu-id="21670-155">**Alertas Ativos**: lista todos os alertas ativos sobre a comunicação entre o Operations Manager e o Mapa do Serviço.</span><span class="sxs-lookup"><span data-stu-id="21670-155">**Active Alerts**: Lists all the active alerts about the communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="21670-156">Observe que esses alertas não estão que sendo sincronizados para o Operations Manager de alertas do Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="21670-156">Note that these alerts are not Operations Management Suite alerts being synced to Operations Manager.</span></span> 

* <span data-ttu-id="21670-157">**Servidores**: lista os servidores monitorados configurados para sincronização por meio do Mapa do Serviço.</span><span class="sxs-lookup"><span data-stu-id="21670-157">**Servers**: Lists the monitored servers that are configured to sync from Service Map.</span></span>

    ![O painel Monitorando Servidores do Operations Manager](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="21670-159">**Exibições de dependência de grupo do computador**: lista todos os grupos de computadores que foram sincronizados de mapa de serviço.</span><span class="sxs-lookup"><span data-stu-id="21670-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="21670-160">É possível clicar em qualquer grupo para exibir seu diagrama de aplicativo distribuído.</span><span class="sxs-lookup"><span data-stu-id="21670-160">You can click any group to view its distributed application diagram.</span></span>

    ![O diagrama de aplicativo distribuído do Operations Manager](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="21670-162">**Exibições de Dependência de Servidor**: lista todos os servidores sincronizados por meio do Mapa do Serviço.</span><span class="sxs-lookup"><span data-stu-id="21670-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="21670-163">É possível clicar em qualquer servidor para exibir seu diagrama de aplicativo distribuído.</span><span class="sxs-lookup"><span data-stu-id="21670-163">You can click any server to view its distributed application diagram.</span></span>

    ![O diagrama de aplicativo distribuído do Operations Manager](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-the-workspace"></a><span data-ttu-id="21670-165">Editar ou excluir o espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="21670-165">Edit or delete the workspace</span></span>
<span data-ttu-id="21670-166">É possível editar ou excluir o espaço de trabalho configurado por meio do painel **Visão Geral do Mapa do Serviço** (painel **Administração** > **Operations Management Suite** > **Mapa do Serviço**).</span><span class="sxs-lookup"><span data-stu-id="21670-166">You can edit or delete the configured workspace through the **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="21670-167">No momento, é possível configurar apenas um espaço de trabalho do Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="21670-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![O painel Editar Espaço de Trabalho do Operations Manager](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="21670-169">Configurar regras e substituições</span><span class="sxs-lookup"><span data-stu-id="21670-169">Configure rules and overrides</span></span>
<span data-ttu-id="21670-170">Uma regra, _Microsoft.SystemCenter.ServiceMapImport.Rule_, é criada para buscar informações periodicamente do Mapa do Serviço.</span><span class="sxs-lookup"><span data-stu-id="21670-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created to periodically fetch information from Service Map.</span></span> <span data-ttu-id="21670-171">Para alterar os intervalos de sincronização, é possível configurar substituições da regra (painel **Criação** > **Regras** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="21670-171">To change sync timings, you can configure overrides of the rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![A janela de propriedades Substituições do Operations Manager](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="21670-173">**Enabled**: habilite ou desabilite atualizações automáticas.</span><span class="sxs-lookup"><span data-stu-id="21670-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="21670-174">**IntervalMinutes**: redefina o tempo entre as atualizações.</span><span class="sxs-lookup"><span data-stu-id="21670-174">**IntervalMinutes**: Reset the time between updates.</span></span> <span data-ttu-id="21670-175">O intervalo padrão é uma hora.</span><span class="sxs-lookup"><span data-stu-id="21670-175">The default interval is one hour.</span></span> <span data-ttu-id="21670-176">Se você desejar sincronizar os mapas do servidor com mais frequência, poderá alterar o valor.</span><span class="sxs-lookup"><span data-stu-id="21670-176">If you want to sync server maps more frequently, you can change the value.</span></span>
* <span data-ttu-id="21670-177">**TimeoutSeconds**: redefina a duração de tempo antes que a solicitação atinja o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="21670-177">**TimeoutSeconds**: Reset the length of time before the request times out.</span></span> 
* <span data-ttu-id="21670-178">**TimeWindowMinutes**: redefina a janela de tempo para consultar os dados.</span><span class="sxs-lookup"><span data-stu-id="21670-178">**TimeWindowMinutes**: Reset the time window for querying data.</span></span> <span data-ttu-id="21670-179">O padrão é uma janela de 60 minutos.</span><span class="sxs-lookup"><span data-stu-id="21670-179">Default is a 60-minute window.</span></span> <span data-ttu-id="21670-180">O valor máximo permitido pelo Mapa do Serviço é 60 minutos.</span><span class="sxs-lookup"><span data-stu-id="21670-180">The maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="21670-181">Problemas e limitações conhecidos</span><span class="sxs-lookup"><span data-stu-id="21670-181">Known issues and limitations</span></span>

<span data-ttu-id="21670-182">O design atual apresenta os seguintes problemas e limitações:</span><span class="sxs-lookup"><span data-stu-id="21670-182">The current design presents the following issues and limitations:</span></span>
* <span data-ttu-id="21670-183">Você só pode se conectar a um único espaço de trabalho do Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="21670-183">You can only connect to a single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="21670-184">Embora você possa adicionar servidores ao Grupo de Servidores do Mapa do Serviço manualmente por meio do painel **Criação**, os mapas desses servidores não são sincronizados imediatamente.</span><span class="sxs-lookup"><span data-stu-id="21670-184">Although you can add servers to the Service Map Servers Group manually through the **Authoring** pane, the maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="21670-185">Eles serão sincronizados do mapa de serviço durante o próximo ciclo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="21670-185">They will be synced from Service Map during the next sync cycle.</span></span>
* <span data-ttu-id="21670-186">Se você fizer alterações para os diagramas de aplicativo distribuído criado pelo pacote de gerenciamento, essas alterações provavelmente serão substituídas na próxima sincronização com o mapa de serviço.</span><span class="sxs-lookup"><span data-stu-id="21670-186">If you make any changes to the Distributed Application Diagrams created by the management pack, those changes will likely be overwritten on the next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="21670-187">Criar uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="21670-187">Create a service principal</span></span>
<span data-ttu-id="21670-188">Para obter a documentação oficial do Azure sobre como criar uma entidade de serviço, consulte:</span><span class="sxs-lookup"><span data-stu-id="21670-188">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="21670-189">Criar uma entidade de serviço usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="21670-189">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="21670-190">Criar uma entidade de serviço usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="21670-190">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="21670-191">Criar uma entidade de serviço usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="21670-191">Create a service principal by using the Azure portal</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="21670-192">Comentários</span><span class="sxs-lookup"><span data-stu-id="21670-192">Feedback</span></span>
<span data-ttu-id="21670-193">Você tem algum comentário sobre o Mapa de Serviço ou sobre esta documentação?</span><span class="sxs-lookup"><span data-stu-id="21670-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="21670-194">Visite nossa [página do User Voice](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), na qual você pode sugerir recursos ou votar em sugestões existentes.</span><span class="sxs-lookup"><span data-stu-id="21670-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
