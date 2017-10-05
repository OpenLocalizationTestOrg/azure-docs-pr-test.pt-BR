---
title: Gateway de Gerenciamento de Dados para Data Factory | Microsoft Docs
description: Configure um gateway de dados para mover dados entre o local e a nuvem. Use o Gateway de Gerenciamento de Dados no Azure Data Factory para mover os dados.
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 9e40eba285aeb1cce6b77311d1b69a6b96967a0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="data-management-gateway"></a><span data-ttu-id="94527-104">Gateway de gerenciamento de dados</span><span class="sxs-lookup"><span data-stu-id="94527-104">Data Management Gateway</span></span>
<span data-ttu-id="94527-105">O Gateway de Gerenciamento de Dados é um agente cliente que você deve instalar no seu ambiente local para copiar dados entre a nuvem e os repositórios de dados locais.</span><span class="sxs-lookup"><span data-stu-id="94527-105">The Data management gateway is a client agent that you must install in your on-premises environment to copy data between cloud and on-premises data stores.</span></span> <span data-ttu-id="94527-106">Os repositórios de dados locais compatíveis com o Data Factory estão listados na seção [Fontes de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats) .</span><span class="sxs-lookup"><span data-stu-id="94527-106">The on-premises data stores supported by Data Factory are listed in the [Supported data sources](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span></span>

<span data-ttu-id="94527-107">Este artigo complementa o passo a passo do artigo [Mover dados entre repositórios de dados locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="94527-107">This article complements the walkthrough in the [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="94527-108">Neste passo a passo, você cria um pipeline que usa o gateway para mover dados de um banco de dados SQL Server local para um blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="94527-108">In the walkthrough, you create a pipeline that uses the gateway to move data from an on-premises SQL Server database to an Azure blob.</span></span> <span data-ttu-id="94527-109">Este artigo fornece informações detalhadas sobre o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="94527-109">This article provides detailed in-depth information about the data management gateway.</span></span> 

<span data-ttu-id="94527-110">Você pode escalar horizontalmente um Gateway de Gerenciamento de Dados por meio da associação de vários computadores locais com o gateway.</span><span class="sxs-lookup"><span data-stu-id="94527-110">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span></span> <span data-ttu-id="94527-111">Você pode escalar verticalmente com o aumento do número de trabalhos de movimentação de dados que podem ser executados simultaneamente em um nó.</span><span class="sxs-lookup"><span data-stu-id="94527-111">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="94527-112">Esse recurso também está disponível para um gateway lógico com um único nó.</span><span class="sxs-lookup"><span data-stu-id="94527-112">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="94527-113">Consulte o artigo [Escalar o Gateway de Gerenciamento de Dados no Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="94527-113">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>

> [!NOTE]
> <span data-ttu-id="94527-114">Atualmente, o gateway suporta apenas a atividade de cópia e a atividade de procedimento armazenado no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="94527-114">Currently, gateway supports only the copy activity and stored procedure activity in Data Factory.</span></span> <span data-ttu-id="94527-115">Não é possível usar o gateway de uma atividade personalizada para acessar fontes de dados locais.</span><span class="sxs-lookup"><span data-stu-id="94527-115">It is not possible to use the gateway from a custom activity to access on-premises data sources.</span></span>      

## <a name="overview"></a><span data-ttu-id="94527-116">Visão geral</span><span class="sxs-lookup"><span data-stu-id="94527-116">Overview</span></span>
### <a name="capabilities-of-data-management-gateway"></a><span data-ttu-id="94527-117">Funcionalidades do Gateway de Gerenciamento de Dados</span><span class="sxs-lookup"><span data-stu-id="94527-117">Capabilities of data management gateway</span></span>
<span data-ttu-id="94527-118">O Gateway de Gerenciamento de Dados fornece as seguintes funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="94527-118">Data management gateway provides the following capabilities:</span></span>

* <span data-ttu-id="94527-119">Modelar fontes de dados locais e fontes de dados em nuvem na mesma data factory e mover dados.</span><span class="sxs-lookup"><span data-stu-id="94527-119">Model on-premises data sources and cloud data sources within the same data factory and move data.</span></span>
* <span data-ttu-id="94527-120">Ter um único painel de monitoramento e gerenciamento com visibilidade do status do gateway da página do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="94527-120">Have a single pane of glass for monitoring and management with visibility into gateway status from the Data Factory page.</span></span>
* <span data-ttu-id="94527-121">Gerenciar o acesso a fontes de dados locais com segurança.</span><span class="sxs-lookup"><span data-stu-id="94527-121">Manage access to on-premises data sources securely.</span></span>
  * <span data-ttu-id="94527-122">Não são necessárias alterações no firewall corporativo.</span><span class="sxs-lookup"><span data-stu-id="94527-122">No changes required to corporate firewall.</span></span> <span data-ttu-id="94527-123">O gateway faz apenas conexões de saída baseadas em HTTP para a Internet aberta.</span><span class="sxs-lookup"><span data-stu-id="94527-123">Gateway only makes outbound HTTP-based connections to open internet.</span></span>
  * <span data-ttu-id="94527-124">Criptografar credenciais para seus armazenamentos de dados locais com seu certificado.</span><span class="sxs-lookup"><span data-stu-id="94527-124">Encrypt credentials for your on-premises data stores with your certificate.</span></span>
* <span data-ttu-id="94527-125">Mover dados com eficiência: os dados são transferidos em paralelo, resilientes a problemas de rede intermitente com lógica de repetição automática.</span><span class="sxs-lookup"><span data-stu-id="94527-125">Move data efficiently – data is transferred in parallel, resilient to intermittent network issues with auto retry logic.</span></span>

### <a name="command-flow-and-data-flow"></a><span data-ttu-id="94527-126">Fluxo de comando e fluxo de dados</span><span class="sxs-lookup"><span data-stu-id="94527-126">Command flow and data flow</span></span>
<span data-ttu-id="94527-127">Quando você usa uma atividade de cópia para copiar dados entre repositórios locais e a nuvem, a atividade usa um gateway para transferir dados da fonte de dados local para a nuvem, e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="94527-127">When you use a copy activity to copy data between on-premises and cloud, the activity uses a gateway to transfer data from on-premises data source to cloud and vice versa.</span></span>

<span data-ttu-id="94527-128">Aqui está o fluxo de dados de alto nível e o resumo das etapas para a cópia com o gateway de dados: ![Fluxo de dados usando o gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span><span class="sxs-lookup"><span data-stu-id="94527-128">Here is the high-level data flow for and summary of steps for copy with data gateway: ![Data flow using gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span></span>

1. <span data-ttu-id="94527-129">O desenvolvedor de dados cria um gateway para uma Azure Data Factory usando o [Portal do Azure](https://portal.azure.com) ou [Cmdlet do PowerShell](https://msdn.microsoft.com/library/dn820234.aspx).</span><span class="sxs-lookup"><span data-stu-id="94527-129">Data developer creates a gateway for an Azure Data Factory using either the [Azure portal](https://portal.azure.com) or [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span></span>
2. <span data-ttu-id="94527-130">O desenvolvedor de dados cria um serviço vinculado para um armazenamento de dados local ao especificar o gateway.</span><span class="sxs-lookup"><span data-stu-id="94527-130">Data developer creates a linked service for an on-premises data store by specifying the gateway.</span></span> <span data-ttu-id="94527-131">Como parte da configuração de dados do serviço vinculado, o desenvolvedor usa o aplicativo Configurando Credenciais para especificar as credenciais e tipos de autenticação.</span><span class="sxs-lookup"><span data-stu-id="94527-131">As part of setting up the linked service, data developer uses the Setting Credentials application to specify authentication types and credentials.</span></span>  <span data-ttu-id="94527-132">O diálogo do aplicativo Configurando Credenciais se comunica com o armazenamento de dados para testar a conexão e o gateway para salvar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="94527-132">The Setting Credentials application dialog communicates with the data store to test connection and the gateway to save credentials.</span></span>
3. <span data-ttu-id="94527-133">O gateway criptografa credenciais com o certificado associado ao gateway (fornecido pelo desenvolvedor de dados) antes de salvar as credenciais na nuvem.</span><span class="sxs-lookup"><span data-stu-id="94527-133">Gateway encrypts the credentials with the certificate associated with the gateway (supplied by data developer), before saving the credentials in the cloud.</span></span>
4. <span data-ttu-id="94527-134">O serviço Data Factory se comunica com o gateway para o agendamento e o gerenciamento de trabalhos por meio de um canal de controle que usa uma fila do Barramento de Serviço do Azure compartilhado.</span><span class="sxs-lookup"><span data-stu-id="94527-134">Data Factory service communicates with the gateway for scheduling & management of jobs via a control channel that uses a shared Azure service bus queue.</span></span> <span data-ttu-id="94527-135">Quando o trabalho de atividade de cópia precisa ser inicializado, o Data Factory enfileira a solicitação junto com as informações de credencial.</span><span class="sxs-lookup"><span data-stu-id="94527-135">When a copy activity job needs to be kicked off, Data Factory queues the request along with credential information.</span></span> <span data-ttu-id="94527-136">O gateway inicia o trabalho depois de sondar a fila.</span><span class="sxs-lookup"><span data-stu-id="94527-136">Gateway kicks off the job after polling the queue.</span></span>
5. <span data-ttu-id="94527-137">O gateway descriptografa as credenciais com o mesmo certificado e se conecta ao armazenamento de dados local com o tipo de autenticação e as credenciais adequadas.</span><span class="sxs-lookup"><span data-stu-id="94527-137">The gateway decrypts the credentials with the same certificate and then connects to the on-premises data store with proper authentication type and credentials.</span></span>
6. <span data-ttu-id="94527-138">O gateway copia dados de um repositório local para um armazenamento na nuvem, ou vice-versa, dependendo de como a Atividade de Cópia estiver configurada no pipeline de dados.</span><span class="sxs-lookup"><span data-stu-id="94527-138">The gateway copies data from an on-premises store to a cloud storage, or vice versa depending on how the Copy Activity is configured in the data pipeline.</span></span> <span data-ttu-id="94527-139">Para esta etapa, o gateway se comunica diretamente com os serviços de armazenamento baseado na nuvem, como Armazenamento de Blobs do Azure por um canal seguro (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="94527-139">For this step, the gateway directly communicates with cloud-based storage services such as Azure Blob Storage over a secure (HTTPS) channel.</span></span>

### <a name="considerations-for-using-gateway"></a><span data-ttu-id="94527-140">Considerações para o uso do gateway</span><span class="sxs-lookup"><span data-stu-id="94527-140">Considerations for using gateway</span></span>
* <span data-ttu-id="94527-141">Uma única instância do Gateway de Gerenciamento de Dados pode ser usada para várias fontes de dados locais.</span><span class="sxs-lookup"><span data-stu-id="94527-141">A single instance of data management gateway can be used for multiple on-premises data sources.</span></span> <span data-ttu-id="94527-142">No entanto, **uma única instância do gateway é vinculada apenas a um Azure Data Factory** e não pode ser compartilhada com outro Data Factory.</span><span class="sxs-lookup"><span data-stu-id="94527-142">However, **a single gateway instance is tied to only one Azure data factory** and cannot be shared with another data factory.</span></span>
* <span data-ttu-id="94527-143">Você pode ter **apenas uma instância do Gateway de Gerenciamento de Dados** instalada em um único computador.</span><span class="sxs-lookup"><span data-stu-id="94527-143">You can have **only one instance of data management gateway** installed on a single machine.</span></span> <span data-ttu-id="94527-144">Supondo que você tenha dois data factories que precisam acessar fontes de dados locais, você precisará instalar gateways em dois computadores locais.</span><span class="sxs-lookup"><span data-stu-id="94527-144">Suppose, you have two data factories that need to access on-premises data sources, you need to install gateways on two on-premises computers.</span></span> <span data-ttu-id="94527-145">Em outras palavras, um gateway é associado a um data factory específico</span><span class="sxs-lookup"><span data-stu-id="94527-145">In other words, a gateway is tied to a specific data factory</span></span>
* <span data-ttu-id="94527-146">O **gateway não precisa estar no mesmo computador que a fonte de dados**.</span><span class="sxs-lookup"><span data-stu-id="94527-146">The **gateway does not need to be on the same machine as the data source**.</span></span> <span data-ttu-id="94527-147">No entanto, com o gateway mais próximo da fonte de dados, menor é o tempo para o gateway se conectar à fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="94527-147">However, having gateway closer to the data source reduces the time for the gateway to connect to the data source.</span></span> <span data-ttu-id="94527-148">É recomendável instalar o gateway em um computador que seja diferente daquele que hospeda a fonte de dados local.</span><span class="sxs-lookup"><span data-stu-id="94527-148">We recommend that you install the gateway on a machine that is different from the one that hosts on-premises data source.</span></span> <span data-ttu-id="94527-149">Quando o gateway e a fonte de dados estiverem em computadores diferentes, o gateway não disputará os recursos com a fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="94527-149">When the gateway and data source are on different machines, the gateway does not compete for resources with data source.</span></span>
* <span data-ttu-id="94527-150">Você pode ter **vários gateways em diferentes computadores conectados à mesma fonte de dados local**.</span><span class="sxs-lookup"><span data-stu-id="94527-150">You can have **multiple gateways on different machines connecting to the same on-premises data source**.</span></span> <span data-ttu-id="94527-151">Por exemplo, você pode ter dois gateways servindo duas data factories, mas a mesma fonte de dados local é registrada com ambas as data factories.</span><span class="sxs-lookup"><span data-stu-id="94527-151">For example, you may have two gateways serving two data factories but the same on-premises data source is registered with both the data factories.</span></span>
* <span data-ttu-id="94527-152">Se você já tiver um gateway instalado no computador atendendo um cenário do **Power BI**, instale um gateway **separado para o Azure Data Factory** em outro computador.</span><span class="sxs-lookup"><span data-stu-id="94527-152">If you already have a gateway installed on your computer serving a **Power BI** scenario, install a **separate gateway for Azure Data Factory** on another machine.</span></span>
* <span data-ttu-id="94527-153">O gateway deve ser usado mesmo quando você usar o **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="94527-153">Gateway must be used even when you use **ExpressRoute**.</span></span>
* <span data-ttu-id="94527-154">Trate a fonte de dados como local (isto é, protegida por um firewall) mesmo quando você usar o **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="94527-154">Treat your data source as an on-premises data source (that is behind a firewall) even when you use **ExpressRoute**.</span></span> <span data-ttu-id="94527-155">Use o gateway para estabelecer conectividade entre o serviço e a fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="94527-155">Use the gateway to establish connectivity between the service and the data source.</span></span>
* <span data-ttu-id="94527-156">Você deverá **usar o gateway** mesmo se o armazenamento de dados estiver na nuvem em um **VM IaaS do Azure**.</span><span class="sxs-lookup"><span data-stu-id="94527-156">You must **use the gateway** even if the data store is in the cloud on an **Azure IaaS VM**.</span></span>

## <a name="installation"></a><span data-ttu-id="94527-157">Instalação</span><span class="sxs-lookup"><span data-stu-id="94527-157">Installation</span></span>
### <a name="prerequisites"></a><span data-ttu-id="94527-158">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="94527-158">Prerequisites</span></span>
* <span data-ttu-id="94527-159">As versões de **Sistema Operacional** com suporte são Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="94527-159">The supported **Operating System** versions are Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span></span> <span data-ttu-id="94527-160">Instalação do Gateway de Gerenciamento de Dados em um controlador de domínio não tem suporte atualmente.</span><span class="sxs-lookup"><span data-stu-id="94527-160">Installation of the data management gateway on a domain controller is currently not supported.</span></span>
* <span data-ttu-id="94527-161">O .NET framework 4.5.1 ou superior é necessário.</span><span class="sxs-lookup"><span data-stu-id="94527-161">.NET Framework 4.5.1 or above is required.</span></span> <span data-ttu-id="94527-162">Se você estiver instalando o gateway em um computador com Windows 7, instale o .NET Framework 4.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="94527-162">If you are installing gateway on a Windows 7 machine, install .NET Framework 4.5 or later.</span></span> <span data-ttu-id="94527-163">Confira [Requisitos de sistema do .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="94527-163">See [.NET Framework System Requirements](https://msdn.microsoft.com/library/8z6watww.aspx) for details.</span></span>
* <span data-ttu-id="94527-164">A **configuração** recomendada para o computador do gateway é de, no mínimo, 2 GHz, 4 núcleos, 8 GB de RAM e 80 GB de disco.</span><span class="sxs-lookup"><span data-stu-id="94527-164">The recommended **configuration** for the gateway machine is at least 2 GHz, 4 cores, 8-GB RAM, and 80-GB disk.</span></span>
* <span data-ttu-id="94527-165">Se o computador host hibernar, o gateway não responderá às solicitações de dados.</span><span class="sxs-lookup"><span data-stu-id="94527-165">If the host machine hibernates, the gateway does not respond to data requests.</span></span> <span data-ttu-id="94527-166">Portanto, configure um **plano de energia** adequado no computador antes de instalar o gateway.</span><span class="sxs-lookup"><span data-stu-id="94527-166">Therefore, configure an appropriate **power plan** on the computer before installing the gateway.</span></span> <span data-ttu-id="94527-167">Se o computador estiver configurado para hibernar, a instalação do gateway exibirá uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="94527-167">If the machine is configured to hibernate, the gateway installation prompts a message.</span></span>
* <span data-ttu-id="94527-168">Você deve ser um administrador no computador local para instalar e configurar com êxito o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="94527-168">You must be an administrator on the machine to install and configure the data management gateway successfully.</span></span> <span data-ttu-id="94527-169">Você pode acrescentar usuários adicionais ao grupo local de usuários do **Gateway de Gerenciamento de dados do Windows**.</span><span class="sxs-lookup"><span data-stu-id="94527-169">You can add additional users to the **data management gateway Users** local Windows group.</span></span> <span data-ttu-id="94527-170">Os membros desse grupo podem usar a ferramenta **Gerenciador de Configurações do Gateway de Gerenciamento de Dados** para configurar o gateway.</span><span class="sxs-lookup"><span data-stu-id="94527-170">The members of this group are able to use the **Data Management Gateway Configuration Manager** tool to configure the gateway.</span></span>

<span data-ttu-id="94527-171">Como as execuções da atividade de cópia ocorrem em uma frequência específica, o uso de recursos (CPU, memória) no computador também segue o mesmo padrão com tempos ociosos e de pico.</span><span class="sxs-lookup"><span data-stu-id="94527-171">As copy activity runs happen on a specific frequency, the resource usage (CPU, memory) on the machine also follows the same pattern with peak and idle times.</span></span> <span data-ttu-id="94527-172">A utilização de recursos também depende muito da quantidade de dados sendo movida.</span><span class="sxs-lookup"><span data-stu-id="94527-172">Resource utilization also depends heavily on the amount of data being moved.</span></span> <span data-ttu-id="94527-173">Quando vários trabalhos de cópia estiverem em andamento, você verá o uso do recurso aumentar durante horários de pico.</span><span class="sxs-lookup"><span data-stu-id="94527-173">When multiple copy jobs are in progress, you see resource usage go up during peak times.</span></span>

### <a name="installation-options"></a><span data-ttu-id="94527-174">Opções de instalação</span><span class="sxs-lookup"><span data-stu-id="94527-174">Installation options</span></span>
<span data-ttu-id="94527-175">O Gateway de Gerenciamento de Dados pode ser instalado das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="94527-175">Data management gateway can be installed in the following ways:</span></span>

* <span data-ttu-id="94527-176">Baixando um pacote de instalação do MSI no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="94527-176">By downloading an MSI setup package from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>  <span data-ttu-id="94527-177">O MSI também pode ser usado para atualizar o Gateway de Gerenciamento de Dados existente para a versão mais recente, com todas as configurações preservadas.</span><span class="sxs-lookup"><span data-stu-id="94527-177">The MSI can also be used to upgrade existing data management gateway to the latest version, with all settings preserved.</span></span>
* <span data-ttu-id="94527-178">Clicando no link **Baixar e instalar o gateway de dados** em INSTALAÇÃO MANUAL ou **Instalar diretamente neste computador** em INSTALAÇÃO EXPRESSA.</span><span class="sxs-lookup"><span data-stu-id="94527-178">By clicking **Download and install data gateway** link under MANUAL SETUP or **Install directly on this computer** under EXPRESS SETUP.</span></span> <span data-ttu-id="94527-179">Veja o artigo [Mover dados entre locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo sobre como usar a instalação expressa.</span><span class="sxs-lookup"><span data-stu-id="94527-179">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on using express setup.</span></span> <span data-ttu-id="94527-180">A etapa manual o leva até o centro de download.</span><span class="sxs-lookup"><span data-stu-id="94527-180">The manual step takes you to the download center.</span></span>  <span data-ttu-id="94527-181">As instruções para baixar e instalar o gateway do centro de download estão na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="94527-181">The instructions for downloading and installing the gateway from download center are in the next section.</span></span>

### <a name="installation-best-practices"></a><span data-ttu-id="94527-182">Práticas recomendadas de instalação:</span><span class="sxs-lookup"><span data-stu-id="94527-182">Installation best practices:</span></span>
1. <span data-ttu-id="94527-183">Configure o plano de energia no computador host para o gateway para que o computador não hiberne.</span><span class="sxs-lookup"><span data-stu-id="94527-183">Configure power plan on the host machine for the gateway so that the machine does not hibernate.</span></span> <span data-ttu-id="94527-184">Se o computador host hibernar, o gateway não responderá às solicitações de dados.</span><span class="sxs-lookup"><span data-stu-id="94527-184">If the host machine hibernates, the gateway does not respond to data requests.</span></span>
2. <span data-ttu-id="94527-185">Faça backup do certificado associado ao gateway.</span><span class="sxs-lookup"><span data-stu-id="94527-185">Back up the certificate associated with the gateway.</span></span>

### <a name="install-the-gateway-from-download-center"></a><span data-ttu-id="94527-186">Instalar o gateway do centro de download</span><span class="sxs-lookup"><span data-stu-id="94527-186">Install the gateway from download center</span></span>
1. <span data-ttu-id="94527-187">Navegue até a [página de download do Gateway de Gerenciamento de Dados da Microsoft](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="94527-187">Navigate to [Microsoft Data Management Gateway download page](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>
2. <span data-ttu-id="94527-188">Clique em **Baixar**, selecione a versão apropriada (**32 bits** v. **64 bits**) e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="94527-188">Click **Download**, select the appropriate version (**32-bit** vs. **64-bit**), and click **Next**.</span></span>
3. <span data-ttu-id="94527-189">Execute o **MSI** diretamente ou salve-o em seu disco rígido e execute-o.</span><span class="sxs-lookup"><span data-stu-id="94527-189">Run the **MSI** directly or save it to your hard disk and run.</span></span>
4. <span data-ttu-id="94527-190">Na página de **Boas-vindas**, selecione um **idioma** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="94527-190">On the **Welcome** page, select a **language** click **Next**.</span></span>
5. <span data-ttu-id="94527-191">**Aceite** os Termos de Licença e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="94527-191">**Accept** the End-User License Agreement and click **Next**.</span></span>
6. <span data-ttu-id="94527-192">Selecione **pasta** para instalar o gateway e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="94527-192">Select **folder** to install the gateway and click **Next**.</span></span>
7. <span data-ttu-id="94527-193">Na página **Pronto para instalar**, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="94527-193">On the **Ready to install** page, click **Install**.</span></span>
8. <span data-ttu-id="94527-194">Clique em **Concluir** para finalizar a instalação.</span><span class="sxs-lookup"><span data-stu-id="94527-194">Click **Finish** to complete installation.</span></span>
9. <span data-ttu-id="94527-195">Obtenha a chave no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="94527-195">Get the key from the Azure portal.</span></span> <span data-ttu-id="94527-196">Consulte a próxima seção para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="94527-196">See the next section for step-by-step instructions.</span></span>
10. <span data-ttu-id="94527-197">Na página **Registrar gateway** do **Gerenciador de Configurações do Gateway de Gerenciamento de Dados** em execução no computador, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="94527-197">On the **Register gateway** page of **Data Management Gateway Configuration Manager** running on your machine, do the following steps:</span></span>
    1. <span data-ttu-id="94527-198">Cole a chave no texto.</span><span class="sxs-lookup"><span data-stu-id="94527-198">Paste the key in the text.</span></span>
    2. <span data-ttu-id="94527-199">Se preferir, clique em **Mostrar chave do gateway** para ver o texto da chave.</span><span class="sxs-lookup"><span data-stu-id="94527-199">Optionally, click **Show gateway key** to see the key text.</span></span>
    3. <span data-ttu-id="94527-200">Clique em **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="94527-200">Click **Register**.</span></span>

### <a name="register-gateway-using-key"></a><span data-ttu-id="94527-201">Registrar gateway usando chave</span><span class="sxs-lookup"><span data-stu-id="94527-201">Register gateway using key</span></span>
#### <a name="if-you-havent-already-created-a-logical-gateway-in-the-portal"></a><span data-ttu-id="94527-202">Se você ainda não tiver criado um gateway lógico no portal</span><span class="sxs-lookup"><span data-stu-id="94527-202">If you haven't already created a logical gateway in the portal</span></span>
<span data-ttu-id="94527-203">Para criar um gateway no portal e obter a chave na página **Configurar**, siga as etapas do passo a passo no artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="94527-203">To create a gateway in the portal and get the key from the **Configure** page, Follow steps from walkthrough in the [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>    

#### <a name="if-you-have-already-created-the-logical-gateway-in-the-portal"></a><span data-ttu-id="94527-204">Se você já tiver criado o gateway lógico no portal</span><span class="sxs-lookup"><span data-stu-id="94527-204">If you have already created the logical gateway in the portal</span></span>
1. <span data-ttu-id="94527-205">No Portal do Azure, navegue até a página **Data Factory** e clique no bloco **Serviços Vinculados**.</span><span class="sxs-lookup"><span data-stu-id="94527-205">In Azure portal, navigate to the **Data Factory** page, and click **Linked Services** tile.</span></span>

    ![Página Data Factory](media/data-factory-data-management-gateway/data-factory-blade.png)
2. <span data-ttu-id="94527-207">Na página **Serviços Vinculados**, selecione o **gateway** lógico criado no portal.</span><span class="sxs-lookup"><span data-stu-id="94527-207">In the **Linked Services** page, select the logical **gateway** you created in the portal.</span></span>

    ![gateway lógico](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. <span data-ttu-id="94527-209">Na página **Gateway de Dados**, clique em **Baixar e instalar o gateway de dados**.</span><span class="sxs-lookup"><span data-stu-id="94527-209">In the **Data Gateway** page, click **Download and install data gateway**.</span></span>

    ![Baixar o link no portal](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. <span data-ttu-id="94527-211">Na página **Configurar**, clique em **Recriar chave**.</span><span class="sxs-lookup"><span data-stu-id="94527-211">In the **Configure** page, click **Recreate key**.</span></span> <span data-ttu-id="94527-212">Clique em Sim na mensagem de aviso depois de ler com cuidado.</span><span class="sxs-lookup"><span data-stu-id="94527-212">Click Yes on the warning message after reading it carefully.</span></span>

    ![Recriar chave](media/data-factory-data-management-gateway/recreate-key-button.png)
5. <span data-ttu-id="94527-214">Clique no botão Copiar ao lado da chave.</span><span class="sxs-lookup"><span data-stu-id="94527-214">Click Copy button next to the key.</span></span> <span data-ttu-id="94527-215">A chave é copiada para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="94527-215">The key is copied to the clipboard.</span></span>

    ![Copiar chave](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a><span data-ttu-id="94527-217">Ícones/notificações da bandeja do sistema</span><span class="sxs-lookup"><span data-stu-id="94527-217">System tray icons/ notifications</span></span>
<span data-ttu-id="94527-218">A imagem a seguir mostra alguns dos ícones da bandeja que você vê.</span><span class="sxs-lookup"><span data-stu-id="94527-218">The following image shows some of the tray icons that you see.</span></span>

![ícones da bandeja do sistema](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

<span data-ttu-id="94527-220">Se mover o cursor sobre o ícone de bandeja do sistema/mensagem de notificação, você vê detalhes sobre o estado do gateway/da operação de atualização em uma janela pop-up.</span><span class="sxs-lookup"><span data-stu-id="94527-220">If you move cursor over the system tray icon/notification message, you see details about the state of the gateway/update operation in a popup window.</span></span>

### <a name="ports-and-firewall"></a><span data-ttu-id="94527-221">Portas e firewall</span><span class="sxs-lookup"><span data-stu-id="94527-221">Ports and firewall</span></span>
<span data-ttu-id="94527-222">Há dois firewalls que você precisa levar em consideração: o **firewall corporativo** em execução no roteador central da organização e o **Firewall do Windows** configurado como um daemon no computador local em que o gateway está instalado.</span><span class="sxs-lookup"><span data-stu-id="94527-222">There are two firewalls you need to consider: **corporate firewall** running on the central router of the organization, and **Windows firewall** configured as a daemon on the local machine where the gateway is installed.</span></span>  

![firewalls](./media/data-factory-data-management-gateway/firewalls2.png)

<span data-ttu-id="94527-224">No nível do firewall corporativo, você precisa configurar os seguintes domínios e portas de saída:</span><span class="sxs-lookup"><span data-stu-id="94527-224">At corporate firewall level, you need configure the following domains and outbound ports:</span></span>

| <span data-ttu-id="94527-225">Nomes de domínio</span><span class="sxs-lookup"><span data-stu-id="94527-225">Domain names</span></span> | <span data-ttu-id="94527-226">Portas</span><span class="sxs-lookup"><span data-stu-id="94527-226">Ports</span></span> | <span data-ttu-id="94527-227">Descrição</span><span class="sxs-lookup"><span data-stu-id="94527-227">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="94527-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="94527-228">*.servicebus.windows.net</span></span> |<span data-ttu-id="94527-229">443, 80</span><span class="sxs-lookup"><span data-stu-id="94527-229">443, 80</span></span> |<span data-ttu-id="94527-230">Usado para comunicação com o back-end do Serviço de Movimentação de Dados</span><span class="sxs-lookup"><span data-stu-id="94527-230">Used for communication with Data Movement Service backend</span></span> |
| <span data-ttu-id="94527-231">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="94527-231">*.core.windows.net</span></span> |<span data-ttu-id="94527-232">443</span><span class="sxs-lookup"><span data-stu-id="94527-232">443</span></span> |<span data-ttu-id="94527-233">Usado para cópia em etapas usando Blobs do Azure (se estiver configurado)</span><span class="sxs-lookup"><span data-stu-id="94527-233">Used for Staged copy using Azure Blob (if configured)</span></span>|
| <span data-ttu-id="94527-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="94527-234">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="94527-235">443</span><span class="sxs-lookup"><span data-stu-id="94527-235">443</span></span> |<span data-ttu-id="94527-236">Usado para comunicação com o back-end do Serviço de Movimentação de Dados</span><span class="sxs-lookup"><span data-stu-id="94527-236">Used for communication with Data Movement Service backend</span></span> |


<span data-ttu-id="94527-237">No nível do Firewall do Windows, essas portas de saída normalmente são habilitadas.</span><span class="sxs-lookup"><span data-stu-id="94527-237">At Windows firewall level, these outbound ports are normally enabled.</span></span> <span data-ttu-id="94527-238">Se não forem, você poderá configurar as portas e os domínios adequadamente no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="94527-238">If not, you can configure the domains and ports accordingly on gateway machine.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="94527-239">Com base em sua origem/coletores, talvez você precise incluir domínios adicionais na lista de permissões e as portas de saída em seu Firewall do Windows/corporativo.</span><span class="sxs-lookup"><span data-stu-id="94527-239">Based on your source/ sinks, you may have to whitelist additional domains and outbound ports in your corporate/Windows firewall.</span></span>
> 2. <span data-ttu-id="94527-240">Para alguns bancos de dados na nuvem (por exemplo: [Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access) etc.), talvez seja necessário incluir o endereço IP do computador do Gateway na lista de permissões na configuração do firewall deles.</span><span class="sxs-lookup"><span data-stu-id="94527-240">For some Cloud Databases (For example: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), you may need to whitelist IP address of Gateway machine on their firewall configuration.</span></span>
>
>


#### <a name="copy-data-from-a-source-data-store-to-a-sink-data-store"></a><span data-ttu-id="94527-241">Copiar dados de um repositório de dados de origem para um repositório de dados de coletor</span><span class="sxs-lookup"><span data-stu-id="94527-241">Copy data from a source data store to a sink data store</span></span>
<span data-ttu-id="94527-242">Verifique se as regras de firewall estão habilitadas corretamente no firewall corporativo, no Firewall do Windows no computador do gateway e no próprio repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="94527-242">Ensure that the firewall rules are enabled properly on the corporate firewall, Windows firewall on the gateway machine, and the data store itself.</span></span> <span data-ttu-id="94527-243">Habilitar essas regras permite ao gateway se conectar com êxito à fonte e ao coletor.</span><span class="sxs-lookup"><span data-stu-id="94527-243">Enabling these rules allows the gateway to connect to both source and sink successfully.</span></span> <span data-ttu-id="94527-244">Habilite as regras para cada repositório de dados que esteja envolvido na operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="94527-244">Enable rules for each data store that is involved in the copy operation.</span></span>

<span data-ttu-id="94527-245">Por exemplo, para copiar de **um repositório de dados local para um coletor do Banco de Dados SQL do Azure ou um coletor do SQL Data Warehouse do Azure**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="94527-245">For example, to copy from **an on-premises data store to an Azure SQL Database sink or an Azure SQL Data Warehouse sink**, do the following steps:</span></span>

* <span data-ttu-id="94527-246">Permitir a comunicação **TCP** de saída na porta **1433** para o firewall do Windows e o firewall corporativo.</span><span class="sxs-lookup"><span data-stu-id="94527-246">Allow outbound **TCP** communication on port **1433** for both Windows firewall and corporate firewall.</span></span>
* <span data-ttu-id="94527-247">Configurar as definições de firewall do SQL Server do Azure para adicionar o endereço IP do computador do gateway à lista de endereços IP permitidos.</span><span class="sxs-lookup"><span data-stu-id="94527-247">Configure the firewall settings of Azure SQL server to add the IP address of the gateway machine to the list of allowed IP addresses.</span></span>

> [!NOTE]
> <span data-ttu-id="94527-248">Se o firewall não permitir a porta de saída 1433, o Gateway não poderá acessar diretamente o Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="94527-248">If your firewall does not allow outbound port 1433, Gateway can't access Azure SQL directly.</span></span> <span data-ttu-id="94527-249">Nesse caso, use [Cópia em Etapas](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) para o Banco de Dados SQL do Azure/DW SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="94527-249">In this case, you may use [Staged Copy](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) to SQL Azure Database/ SQL Azure DW.</span></span> <span data-ttu-id="94527-250">Neste cenário, você exigiria apenas HTTPS (porta 443) para a movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="94527-250">In this scenario, you would only require HTTPS (port 443) for the data movement.</span></span>
>
>


### <a name="proxy-server-considerations"></a><span data-ttu-id="94527-251">Considerações do servidor proxy</span><span class="sxs-lookup"><span data-stu-id="94527-251">Proxy server considerations</span></span>
<span data-ttu-id="94527-252">Se o ambiente de rede corporativo usar um servidor proxy para acessar a Internet, configure o Gateway de Gerenciamento de Dados para usar as definições de proxy apropriadas.</span><span class="sxs-lookup"><span data-stu-id="94527-252">If your corporate network environment uses a proxy server to access the internet, configure data management gateway to use appropriate proxy settings.</span></span> <span data-ttu-id="94527-253">Você pode definir o proxy durante a fase de registro inicial.</span><span class="sxs-lookup"><span data-stu-id="94527-253">You can set the proxy during the initial registration phase.</span></span>

![Definir proxy durante o registro](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

<span data-ttu-id="94527-255">O gateway usa o servidor proxy para se conectar ao serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="94527-255">Gateway uses the proxy server to connect to the cloud service.</span></span> <span data-ttu-id="94527-256">Clique no link **Alteração** durante a configuração inicial.</span><span class="sxs-lookup"><span data-stu-id="94527-256">Click **Change** link during initial setup.</span></span> <span data-ttu-id="94527-257">Você verá a caixa de diálogo **configuração de proxy** .</span><span class="sxs-lookup"><span data-stu-id="94527-257">You see the **proxy setting** dialog.</span></span>

![Definir proxy usando o gerenciador de configurações](media/data-factory-data-management-gateway/SetProxySettings.png)

<span data-ttu-id="94527-259">Há três opções de configuração:</span><span class="sxs-lookup"><span data-stu-id="94527-259">There are three configuration options:</span></span>

* <span data-ttu-id="94527-260">**Não usar proxy**: o gateway não usa explicitamente qualquer proxy para se conectar aos serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="94527-260">**Do not use proxy**: Gateway does not explicitly use any proxy to connect to cloud services.</span></span>
* <span data-ttu-id="94527-261">**Usar proxy do sistema**: o gateway usa a configuração de proxy que é definida em diahost.exe.config e em diawp.exe.config.  Se nenhum proxy estiver configurado em diahost.exe.config e em diawp.exe.config, o gateway se conectará ao serviço de nuvem diretamente sem passar pelo proxy.</span><span class="sxs-lookup"><span data-stu-id="94527-261">**Use system proxy**: Gateway uses the proxy setting that is configured in diahost.exe.config and diawp.exe.config.  If no proxy is configured in diahost.exe.config and diawp.exe.config, gateway connects to cloud service directly without going through proxy.</span></span>
* <span data-ttu-id="94527-262">**Usar proxy personalizado**: configure a definição do proxy HTTP a ser usado pelo gateway, em vez de usar as configurações em diahost.exe.config e diawp.exe.config.  Endereço e porta são necessários.</span><span class="sxs-lookup"><span data-stu-id="94527-262">**Use custom proxy**: Configure the HTTP proxy setting to use for gateway, instead of using configurations in diahost.exe.config and diawp.exe.config.  Address and Port are required.</span></span>  <span data-ttu-id="94527-263">O Nome de Usuário e a Senha são opcionais, dependendo da configuração de autenticação do seu proxy.</span><span class="sxs-lookup"><span data-stu-id="94527-263">User Name and Password are optional depending on your proxy’s authentication setting.</span></span>  <span data-ttu-id="94527-264">Todas as configurações são criptografadas com o certificado de credencial do gateway e armazenadas localmente no computador host do gateway.</span><span class="sxs-lookup"><span data-stu-id="94527-264">All settings are encrypted with the credential certificate of the gateway and stored locally on the gateway host machine.</span></span>

<span data-ttu-id="94527-265">O Serviço de Host do Gateway de Gerenciamento de Dados é reiniciado automaticamente depois que você salva as configurações de proxy atualizadas.</span><span class="sxs-lookup"><span data-stu-id="94527-265">The data management gateway Host Service restarts automatically after you save the updated proxy settings.</span></span>

<span data-ttu-id="94527-266">Depois que o gateway tiver sido registrado com êxito, se você quiser exibir ou atualizar as configurações de proxy, use o Gerenciador de Configurações do Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="94527-266">After gateway has been successfully registered, if you want to view or update proxy settings, use Data Management Gateway Configuration Manager.</span></span>

1. <span data-ttu-id="94527-267">Iniciar o **Gerenciador de Configuração de Gateway de Gerenciamento de Dados**.</span><span class="sxs-lookup"><span data-stu-id="94527-267">Launch **Data Management Gateway Configuration Manager**.</span></span>
2. <span data-ttu-id="94527-268">Alterne para a guia **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="94527-268">Switch to the **Settings** tab.</span></span>
3. <span data-ttu-id="94527-269">Clique no link **Alterar** na seção **Proxy HTTP** para iniciar a caixa de diálogo **Configurar Proxy HTTP**.</span><span class="sxs-lookup"><span data-stu-id="94527-269">Click **Change** link in **HTTP Proxy** section to launch the **Set HTTP Proxy** dialog.</span></span>  
4. <span data-ttu-id="94527-270">Depois de clicar no botão **Avançar** , você verá uma caixa de diálogo de aviso solicitando sua permissão para salvar a configuração de proxy e reiniciar o Serviço de Host do Gateway.</span><span class="sxs-lookup"><span data-stu-id="94527-270">After you click the **Next** button, you see a warning dialog asking for your permission to save the proxy setting and restart the Gateway Host Service.</span></span>

<span data-ttu-id="94527-271">Você pode exibir e atualizar o proxy HTTP usando a ferramenta Gerenciador de Configurações.</span><span class="sxs-lookup"><span data-stu-id="94527-271">You can view and update HTTP proxy by using Configuration Manager tool.</span></span>

![Definir proxy usando o gerenciador de configurações](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> <span data-ttu-id="94527-273">Se você configurar um servidor proxy com autenticação NTLM, o Serviço de Host do Gateway será executado sob a conta de domínio.</span><span class="sxs-lookup"><span data-stu-id="94527-273">If you set up a proxy server with NTLM authentication, Gateway Host Service runs under the domain account.</span></span> <span data-ttu-id="94527-274">Se você alterar a senha da conta de domínio posteriormente, lembre-se de atualizar as definições de configuração para o serviço e reiniciá-lo adequadamente.</span><span class="sxs-lookup"><span data-stu-id="94527-274">If you change the password for the domain account later, remember to update configuration settings for the service and restart it accordingly.</span></span> <span data-ttu-id="94527-275">Por conta desse requisito, sugerimos o uso de uma conta de domínio dedicada para acessar o servidor proxy que não exija a atualização da senha com frequência.</span><span class="sxs-lookup"><span data-stu-id="94527-275">Due to this requirement, we suggest you use a dedicated domain account to access the proxy server that does not require you to update the password frequently.</span></span>
>
>

### <a name="configure-proxy-server-settings"></a><span data-ttu-id="94527-276">Definir configurações do servidor proxy</span><span class="sxs-lookup"><span data-stu-id="94527-276">Configure proxy server settings</span></span>
<span data-ttu-id="94527-277">Se você escolher a configuração **Usar proxy do sistema** para o proxy HTTP, o gateway usará a configuração de proxy em diahost.exe.config e diawp.exe.config.  Se nenhum proxy for especificado em diahost.exe.config., o gateway se conectará ao serviço de nuvem diretamente sem passar pelo proxy.</span><span class="sxs-lookup"><span data-stu-id="94527-277">If you select **Use system proxy** setting for the HTTP proxy, gateway uses the proxy setting in diahost.exe.config and diawp.exe.config.  If no proxy is specified in diahost.exe.config and diawp.exe.config, gateway connects to cloud service directly without going through proxy.</span></span> <span data-ttu-id="94527-278">O procedimento a seguir fornece instruções para atualizar o arquivo diahost.exe.config.</span><span class="sxs-lookup"><span data-stu-id="94527-278">The following procedure provides instructions for updating the diahost.exe.config file.</span></span>  

1. <span data-ttu-id="94527-279">No Explorador de Arquivos, faça uma cópia de segurança de C:\Arquivos de Programas\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config para fazer backup do arquivo original.</span><span class="sxs-lookup"><span data-stu-id="94527-279">In File Explorer, make a safe copy of C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config to back up the original file.</span></span>
2. <span data-ttu-id="94527-280">Inicie o Notepad.exe executando como administrador e abra o arquivo de texto "C:\Arquivos de Programas\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config." Você pode encontrar a marcação padrão para system.net conforme mostrado no código abaixo:</span><span class="sxs-lookup"><span data-stu-id="94527-280">Launch Notepad.exe running as administrator, and open text file “C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. You find the default tag for system.net as shown in the following code:</span></span>

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   <span data-ttu-id="94527-281">Em seguida, você pode adicionar detalhes do servidor proxy, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="94527-281">You can then add proxy server details as shown in the following example:</span></span>

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   <span data-ttu-id="94527-282">Propriedades adicionais são permitidas dentro da marca de proxy para especificar as configurações necessárias como scriptLocation.</span><span class="sxs-lookup"><span data-stu-id="94527-282">Additional properties are allowed inside the proxy tag to specify the required settings like scriptLocation.</span></span> <span data-ttu-id="94527-283">Confira [proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) (Elemento proxy [Configurações de Rede]) na sintaxe.</span><span class="sxs-lookup"><span data-stu-id="94527-283">Refer to [proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on syntax.</span></span>

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. <span data-ttu-id="94527-284">Salve o arquivo de configuração no local original e reinicie o Serviço de Host do Gateway de Gerenciamento de Dados, que assimila as alterações.</span><span class="sxs-lookup"><span data-stu-id="94527-284">Save the configuration file into the original location, then restart the Data Management Gateway Host service, which picks up the changes.</span></span> <span data-ttu-id="94527-285">Para reiniciar o serviço: use o miniaplicativo de serviços no painel de controle ou no Gerenciador de **Configurações do Gateway de Gerenciamento de Dados** > clique no botão **Parar Serviço** e depois em **Iniciar Serviço**.</span><span class="sxs-lookup"><span data-stu-id="94527-285">To restart the service: use services applet from the control panel, or from the **Data Management Gateway Configuration Manager** > click the **Stop Service** button, then click the **Start Service**.</span></span> <span data-ttu-id="94527-286">Se o serviço não iniciar, é provável que uma sintaxe de marca XML incorreta tenha sido adicionada ao arquivo de configuração de aplicativo que foi editado.</span><span class="sxs-lookup"><span data-stu-id="94527-286">If the service does not start, it is likely that an incorrect XML tag syntax has been added into the application configuration file that was edited.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94527-287">Não se esqueça de atualizar **ambos** diahost.exe.config e diawp.exe.config.</span><span class="sxs-lookup"><span data-stu-id="94527-287">Do not forget to update **both** diahost.exe.config and diawp.exe.config.</span></span>  


<span data-ttu-id="94527-288">Além dos desses pontos, você também precisa verificar se o Microsoft Azure está lista de autorizados da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="94527-288">In addition to these points, you also need to make sure Microsoft Azure is in your company’s whitelist.</span></span> <span data-ttu-id="94527-289">Baixe a lista de endereços IP válidos do Microsoft Azure no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="94527-289">The list of valid Microsoft Azure IP addresses can be downloaded from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a><span data-ttu-id="94527-290">Possíveis sintomas de problemas relacionados ao firewall e ao servidor proxy</span><span class="sxs-lookup"><span data-stu-id="94527-290">Possible symptoms for firewall and proxy server-related issues</span></span>
<span data-ttu-id="94527-291">Se você encontrar erros similares aos descritos a seguir, eles provavelmente se deverão à configuração incorreta do servidor proxy ou firewall, que impedirá o gateway de se conectar ao Data Factory para se autenticar.</span><span class="sxs-lookup"><span data-stu-id="94527-291">If you encounter errors similar to the following ones, it is likely due to improper configuration of the firewall or proxy server, which blocks gateway from connecting to Data Factory to authenticate itself.</span></span> <span data-ttu-id="94527-292">Confira a seção anterior para garantir que seu firewall e servidor proxy estejam configurados corretamente.</span><span class="sxs-lookup"><span data-stu-id="94527-292">Refer to previous section to ensure your firewall and proxy server are properly configured.</span></span>

1. <span data-ttu-id="94527-293">Ao tentar registrar o gateway, você recebe o seguinte erro: "Falha ao registrar a chave do gateway.</span><span class="sxs-lookup"><span data-stu-id="94527-293">When you try to register the gateway, you receive the following error: "Failed to register the gateway key.</span></span> <span data-ttu-id="94527-294">Antes de tentar registrar a chave do gateway novamente, confirme se o Gateway de Gerenciamento de Dados está em um estado conectado e o Serviço de Host do Gateway de Gerenciamento de Dados está iniciado."</span><span class="sxs-lookup"><span data-stu-id="94527-294">Before trying to register the gateway key again, confirm that the data management gateway is in a connected state and the Data Management Gateway Host Service is Started."</span></span>
2. <span data-ttu-id="94527-295">Ao abrir o Gerenciador de Configurações, você vê o status "Desconectado" ou "Conectando".</span><span class="sxs-lookup"><span data-stu-id="94527-295">When you open Configuration Manager, you see status as “Disconnected” or “Connecting.”</span></span> <span data-ttu-id="94527-296">Ao exibir os logs de eventos do Windows, em "Visualizar eventos" > "Logs de Aplicativos e Serviços" > "Gateway de Gerenciamento de Dados", você vê mensagens de erro como as do seguinte: `Unable to connect to the remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span><span class="sxs-lookup"><span data-stu-id="94527-296">When viewing Windows event logs, under “Event Viewer” > “Application and Services Logs” > “Data Management Gateway”, you see error messages such as the following error: `Unable to connect to the remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span></span>

### <a name="open-port-8050-for-credential-encryption"></a><span data-ttu-id="94527-297">Abrir a porta 8050 para criptografia de credencial</span><span class="sxs-lookup"><span data-stu-id="94527-297">Open port 8050 for credential encryption</span></span>
<span data-ttu-id="94527-298">O aplicativo **Definindo Credenciais** usa a porta de entrada **8050** para retransmitir credenciais ao gateway quando você configura um serviço vinculado local no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="94527-298">The **Setting Credentials** application uses the inbound port **8050** to relay credentials to the gateway when you set up an on-premises linked service in the Azure portal.</span></span> <span data-ttu-id="94527-299">Durante a instalação do gateway, por padrão, a instalação do gateway o abre no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="94527-299">During gateway setup, by default, the gateway installation opens it on the gateway machine.</span></span>

<span data-ttu-id="94527-300">Se estiver usando um firewall de terceiros, você poderá abrir manualmente a porta 8050.</span><span class="sxs-lookup"><span data-stu-id="94527-300">If you are using a third-party firewall, you can manually open the port 8050.</span></span> <span data-ttu-id="94527-301">Se tiver problemas de firewall durante a configuração do gateway, você poderá tentar usar o comando a seguir para instalar o gateway sem configurar o firewall.</span><span class="sxs-lookup"><span data-stu-id="94527-301">If you run into firewall issue during gateway setup, you can try using the following command to install the gateway without configuring the firewall.</span></span>

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

<span data-ttu-id="94527-302">Se optar por não abrir a porta 8050 no computador do gateway, use mecanismos diferentes do aplicativo **Definindo Credenciais** para configurar as credenciais do armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="94527-302">If you choose not to open the port 8050 on the gateway machine, use mechanisms other than using the **Setting Credentials** application to configure data store credentials.</span></span> <span data-ttu-id="94527-303">Por exemplo, você pode usar o cmdlet do PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) .</span><span class="sxs-lookup"><span data-stu-id="94527-303">For example, you could use [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="94527-304">Confira a seção [Definir Credenciais e Segurança](#set-credentials-and-securityy) para saber como as credenciais do armazenamento de dados podem ser definidas.</span><span class="sxs-lookup"><span data-stu-id="94527-304">See [Setting Credentials and Security](#set-credentials-and-securityy) section on how data store credentials can be set.</span></span>

## <a name="update"></a><span data-ttu-id="94527-305">Atualização</span><span class="sxs-lookup"><span data-stu-id="94527-305">Update</span></span>
<span data-ttu-id="94527-306">Por padrão, o Gateway de Gerenciamento de Dados é atualizado automaticamente quando uma versão mais recente do gateway está disponível.</span><span class="sxs-lookup"><span data-stu-id="94527-306">By default, data management gateway is automatically updated when a newer version of the gateway is available.</span></span> <span data-ttu-id="94527-307">O gateway não é atualizado até que todas as tarefas agendadas sejam concluídas.</span><span class="sxs-lookup"><span data-stu-id="94527-307">The gateway is not updated until all the scheduled tasks are done.</span></span> <span data-ttu-id="94527-308">Nenhuma tarefa adicional é processada pelo gateway até que a operação de atualização seja concluída.</span><span class="sxs-lookup"><span data-stu-id="94527-308">No further tasks are processed by the gateway until the update operation is completed.</span></span> <span data-ttu-id="94527-309">Se a atualização falhar, o gateway será revertido para a versão antiga.</span><span class="sxs-lookup"><span data-stu-id="94527-309">If the update fails, gateway is rolled back to the old version.</span></span>

<span data-ttu-id="94527-310">Você vê a hora de atualização agendada nos seguintes locais:</span><span class="sxs-lookup"><span data-stu-id="94527-310">You see the scheduled update time in the following places:</span></span>

* <span data-ttu-id="94527-311">Na página de propriedades do gateway no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="94527-311">The gateway properties page in the Azure portal.</span></span>
* <span data-ttu-id="94527-312">Na home page do Gerenciador de Configurações do Gateway de Gerenciador de Dados</span><span class="sxs-lookup"><span data-stu-id="94527-312">Home page of the Data Management Gateway Configuration Manager</span></span>
* <span data-ttu-id="94527-313">Na mensagem de notificação da bandeja do sistema.</span><span class="sxs-lookup"><span data-stu-id="94527-313">System tray notification message.</span></span>

<span data-ttu-id="94527-314">A guia Página Inicial do Gerenciador de Configurações do Gateway de Gerenciamento de Dados exibe a agenda de atualização e a última vez em que o gateway foi instalado/atualizado.</span><span class="sxs-lookup"><span data-stu-id="94527-314">The Home tab of the Data Management Gateway Configuration Manager displays the update schedule and the last time the gateway was installed/updated.</span></span>

![Agende atualizações](media/data-factory-data-management-gateway/UpdateSection.png)

<span data-ttu-id="94527-316">Você pode instalar a atualização imediatamente ou aguardar até que o gateway seja atualizado automaticamente no horário agendado.</span><span class="sxs-lookup"><span data-stu-id="94527-316">You can install the update right away or wait for the gateway to be automatically updated at the scheduled time.</span></span> <span data-ttu-id="94527-317">Por exemplo, a imagem a seguir mostra a mensagem de notificação exibida no Gerenciador de Configurações do Gateway com o botão Atualizar, que pode ser clicado para instalar a atualização imediatamente.</span><span class="sxs-lookup"><span data-stu-id="94527-317">For example, the following image shows you the notification message shown in the Gateway Configuration Manager along with the Update button that you can click to install it immediately.</span></span>

![Atualizar no Gerenciador de Configurações DMG](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

<span data-ttu-id="94527-319">A mensagem de notificação na bandeja do sistema seria semelhante à mostrada na imagem abaixo:</span><span class="sxs-lookup"><span data-stu-id="94527-319">The notification message in the system tray would look as shown in the following image:</span></span>

![Mensagem da bandeja do sistema](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

<span data-ttu-id="94527-321">Você vê o status da operação de atualização (manual ou automática) na bandeja do sistema.</span><span class="sxs-lookup"><span data-stu-id="94527-321">You see the status of update operation (manual or automatic) in the system tray.</span></span> <span data-ttu-id="94527-322">Ao iniciar o Gerenciador de Configurações do Gateway na próxima vez, você verá uma mensagem na barra de notificação indicando que o gateway foi atualizado, com um link para o [tópico de novidades](data-factory-gateway-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="94527-322">When you launch Gateway Configuration Manager next time, you see a message on the notification bar that the gateway has been updated along with a link to [what's new topic](data-factory-gateway-release-notes.md).</span></span>

### <a name="to-disableenable-auto-update-feature"></a><span data-ttu-id="94527-323">Para habilitar/desabilitar o recurso de atualização automática</span><span class="sxs-lookup"><span data-stu-id="94527-323">To disable/enable auto-update feature</span></span>
<span data-ttu-id="94527-324">Você pode habilitar/desabilitar o recurso de atualização automática seguindo as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="94527-324">You can disable/enable the auto-update feature by doing the following steps:</span></span>

<span data-ttu-id="94527-325">[Para o gateway de nó único]</span><span class="sxs-lookup"><span data-stu-id="94527-325">[For single node gateway]</span></span>
1. <span data-ttu-id="94527-326">Inicie o Windows PowerShell no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="94527-326">Launch Windows PowerShell on the gateway machine.</span></span>
2. <span data-ttu-id="94527-327">Mude para a pasta C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript.</span><span class="sxs-lookup"><span data-stu-id="94527-327">Switch to the C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="94527-328">Execute o seguinte comando para DESATIVAR (desabilitar) o recurso de atualização automática.</span><span class="sxs-lookup"><span data-stu-id="94527-328">Run the following command to turn the auto-update feature OFF (disable).</span></span>   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. <span data-ttu-id="94527-329">Para ativá-la novamente:</span><span class="sxs-lookup"><span data-stu-id="94527-329">To turn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
<span data-ttu-id="94527-330">[[Para vários nó altamente disponíveis e gateway dimensionável(versão prévia)](data-factory-data-management-gateway-high-availability-scalability.md)]</span><span class="sxs-lookup"><span data-stu-id="94527-330">[[For multi-node highly available and scalable gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]</span></span>
1. <span data-ttu-id="94527-331">Inicie o Windows PowerShell no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="94527-331">Launch Windows PowerShell on the gateway machine.</span></span>
2. <span data-ttu-id="94527-332">Mude para a pasta C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript.</span><span class="sxs-lookup"><span data-stu-id="94527-332">Switch to the C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="94527-333">Execute o seguinte comando para DESATIVAR (desabilitar) o recurso de atualização automática.</span><span class="sxs-lookup"><span data-stu-id="94527-333">Run the following command to turn the auto-update feature OFF (disable).</span></span>   

    <span data-ttu-id="94527-334">Para o gateway com o recurso de alta disponibilidade (versão prévia), um parâmetro AuthKey adicional é necessário.</span><span class="sxs-lookup"><span data-stu-id="94527-334">For gateway with high availability feature (preview), an extra AuthKey param is required.</span></span>
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. <span data-ttu-id="94527-335">Para ativá-la novamente:</span><span class="sxs-lookup"><span data-stu-id="94527-335">To turn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install the gateway, you can launch Data Management Gateway Configuration Manager in one of the following ways:

1. In the **Search** window, type **Data Management Gateway** to access this utility.
2. Run the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
The Home page allows you to do the following actions:

* View status of the gateway (connected to the cloud service etc.).
* **Register** using a key from the portal.
* **Stop** and start the **Data Management Gateway Host service** on the gateway machine.
* **Schedule updates** at a specific time of the days.
* View the date when the gateway was **last updated**.

### Settings page
The Settings page allows you to do the following actions:

* View, change, and export **certificate** used by the gateway. This certificate is used to encrypt data source credentials.
* Change **HTTPS port** for the endpoint. The gateway opens a port for setting the data source credentials.
* **Status** of the endpoint
* View **SSL certificate** is used for SSL communication between portal and the gateway to set credentials for data sources.  

### Diagnostics page
The Diagnostics page allows you to do the following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs to Microsoft if there was a failure.
* **Test connection** to a data source.  

### Help page
The Help page displays the following information:  

* Brief description of the gateway
* Version number
* Links to online help, privacy statement, and license agreement.  

## Monitor gateway in the portal
In the Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate to the home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select the **gateway** in the **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In the **Gateway** page, you can see the memory and CPU usage of the gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** to see more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

The following table provides descriptions of columns in the **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of the logical gateway and nodes associated with the gateway. Node is an on-premises Windows machine that has the gateway installed on it. For information on having more than one node (up to four nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of the logical gateway and the gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows the version of the logical gateway and each gateway node. The version of the logical gateway is determined based on version of majority of nodes in the group. If there are nodes with different versions in the logical gateway setup, only the nodes with the same version number as the logical gateway function properly. Others are in the limited mode and need to be manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies the maximum concurrent jobs for each node. This value is defined based on the machine size. You can increase the limit to scale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when the scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used to execute jobs. There is only one dispatcher node, which is used to pull tasks/jobs from cloud services and dispatch them to different worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in the gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
The following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected to Data Factory service.
Offline | Node is offline.
Upgrading | The node is being auto-updated.
Limited | Due to Connectivity issue. May be due to HTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from the configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect to other nodes. 


The following table provides possible statuses of a **logical gateway**. The gateway status depends on statuses of the gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered to this logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due to credential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure the number of **concurrent data movement jobs** that can run on a node to scale up the capability of moving data between on-premises and cloud data stores. 

When the available memory and CPU are not utilized well, but the idle capacity is 0, you should scale up by increasing the number of concurrent jobs that can run on a node. You may also want to scale up when activities are timing out because the gateway is overloaded. In the advanced settings of a gateway node, you can increase the maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using the data management gateway.  

## Move gateway from one machine to another
This section provides steps for moving gateway client from one machine to another machine.

1. In the portal, navigate to the **Data Factory home page**, and click the **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in the **DATA GATEWAYS** section of the **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In the **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In the **Configure** page, click **Download and install data gateway**, and follow instructions to install the data gateway on the machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep the **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In the **Configure** page in the portal, click **Recreate key** on the command bar, and click **Yes** for the warning message. Click **copy button** next to key text that copies the key to the clipboard. The gateway on the old machine stops functioning as soon you recreate the key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste the **key** into text box in the **Register Gateway** page of the **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box to see the key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** to register the gateway with the cloud service.
9. On the **Settings** tab, click **Change** to select the same certificate that was used with the old gateway, enter the **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from the old gateway by doing the following steps: launch Data Management Gateway Configuration Manager on the old machine, switch to the **Certificate** tab, click **Export** button and follow the instructions.
10. After successful registration of the gateway, you should see the **Registration** set to **Registered** and **Status** set to **Started** on the Home page of the Gateway Configuration Manager.

## Encrypting credentials
To encrypt credentials in the Data Factory Editor, do the following steps:

1. Launch web browser on the **gateway machine**, navigate to [Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in the **DATA FACTORY** page and then click **Author & Deploy** to launch Data Factory Editor.   
2. Click an existing **linked service** in the tree view to see its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In the JSON editor, for the **gatewayName** property, enter the name of the gateway.
4. Enter server name for the **Data Source** property in the **connectionString**.
5. Enter database name for the **Initial Catalog** property in the **connectionString**.    
6. Click **Encrypt** button on the command bar that launches the click-once **Credential Manager** application. You should see the **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In the **Setting Credentials** dialog box, do the following steps:
   1. Select **authentication** that you want the Data Factory service to use to connect to the database.
   2. Enter name of the user who has access to the database for the **USERNAME** setting.
   3. Enter password for the user for the **PASSWORD** setting.  
   4. Click **OK** to encrypt credentials and close the dialog box.
8. You should see a **encryptedCredential** property in the **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
<span data-ttu-id="94527-336">Se você acessar o portal de um computador diferente do computador do gateway, você deve garantir que o aplicativo Gerenciador de credenciais possa se conectar ao computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="94527-336">If you access the portal from a machine that is different from the gateway machine, you must make sure that the Credentials Manager application can connect to the gateway machine.</span></span> <span data-ttu-id="94527-337">Se o aplicativo não puder acessar o computador do gateway, ele não permitirá que você defina credenciais da fonte de dados teste a conexão à fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="94527-337">If the application cannot reach the gateway machine, it does not allow you to set credentials for the data source and to test connection to the data source.</span></span>  

<span data-ttu-id="94527-338">Quando você usa o aplicativo **Definindo Credenciais**, o portal criptografa as credenciais com o certificado especificado na guia **Certificado** do **Gerenciador de Configurações do Gateway** no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="94527-338">When you use the **Setting Credentials** application, the portal encrypts the credentials with the certificate specified in the **Certificate** tab of the **Gateway Configuration Manager** on the gateway machine.</span></span>

<span data-ttu-id="94527-339">Se estiver procurando uma abordagem baseada em API para criptografar as credenciais, você poderá usar o cmdlet [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) do PowerShell para criptografar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="94527-339">If you are looking for an API-based approach for encrypting the credentials, you can use the [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet to encrypt credentials.</span></span> <span data-ttu-id="94527-340">O cmdlet usa o certificado que esse gateway está configurado para usar para criptografar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="94527-340">The cmdlet uses the certificate that gateway is configured to use to encrypt the credentials.</span></span> <span data-ttu-id="94527-341">Você adiciona credenciais criptografadas ao elemento **EncryptedCredential** da **connectionString** no JSON.</span><span class="sxs-lookup"><span data-stu-id="94527-341">You add encrypted credentials to the **EncryptedCredential** element of the **connectionString** in the JSON.</span></span> <span data-ttu-id="94527-342">Você usa o JSON com o cmdlet [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) ou no Editor do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="94527-342">You use the JSON with the [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet or in the Data Factory Editor.</span></span>

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

<span data-ttu-id="94527-343">Há mais uma abordagem para definir as credenciais usando o Editor Data Factory.</span><span class="sxs-lookup"><span data-stu-id="94527-343">There is one more approach for setting credentials using Data Factory Editor.</span></span> <span data-ttu-id="94527-344">Se você criar um serviço vinculado do SQL Server usando o editor e inserir credenciais em texto sem formatação, as credenciais serão criptografadas usando um certificado que é de propriedade do serviço Data Factory.</span><span class="sxs-lookup"><span data-stu-id="94527-344">If you create a SQL Server linked service by using the editor and you enter credentials in plain text, the credentials are encrypted using a certificate that the Data Factory service owns.</span></span> <span data-ttu-id="94527-345">Ele NÃO usará o certificado que o gateway está configurado para usar.</span><span class="sxs-lookup"><span data-stu-id="94527-345">It does NOT use the certificate that gateway is configured to use.</span></span> <span data-ttu-id="94527-346">Embora essa abordagem possa ser um pouco mais rápida em alguns casos, ela é menos segura.</span><span class="sxs-lookup"><span data-stu-id="94527-346">While this approach might be a little faster in some cases, it is less secure.</span></span> <span data-ttu-id="94527-347">Portanto, é recomendável que você siga essa abordagem somente para fins de desenvolvimento/teste.</span><span class="sxs-lookup"><span data-stu-id="94527-347">Therefore, we recommend that you follow this approach only for development/testing purposes.</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="94527-348">Cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="94527-348">PowerShell cmdlets</span></span>
<span data-ttu-id="94527-349">Esta seção descreve como criar e registrar um gateway usando cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="94527-349">This section describes how to create and register a gateway using Azure PowerShell cmdlets.</span></span>

1. <span data-ttu-id="94527-350">Inicie o **PowerShell do Azure** no modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="94527-350">Launch **Azure PowerShell** in administrator mode.</span></span>
2. <span data-ttu-id="94527-351">Faça logon na sua conta do Azure executando o seguinte comando e digitando suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="94527-351">Log in to your Azure account by running the following command and entering your Azure credentials.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="94527-352">Use o cmdlet **New-AzureRmDataFactoryGateway** para criar um gateway lógico da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="94527-352">Use the **New-AzureRmDataFactoryGateway** cmdlet to create a logical gateway as follows:</span></span>

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    <span data-ttu-id="94527-353">**Exemplo de comando e saída**:</span><span class="sxs-lookup"><span data-stu-id="94527-353">**Example command and output**:</span></span>

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. <span data-ttu-id="94527-354">No Azure PowerShell, mude para a pasta: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span><span class="sxs-lookup"><span data-stu-id="94527-354">In Azure PowerShell, switch to the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span></span> <span data-ttu-id="94527-355">Execute **RegisterGateway.ps1** associado à variável local **$Key**, conforme mostrado no comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="94527-355">Run **RegisterGateway.ps1** associated with the local variable **$Key** as shown in the following command.</span></span> <span data-ttu-id="94527-356">Esse script registra o agente cliente instalado no computador com o gateway lógico criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="94527-356">This script registers the client agent installed on your machine with the logical gateway you create earlier.</span></span>

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    <span data-ttu-id="94527-357">Você pode registrar o gateway em um computador remoto usando o parâmetro IsRegisterOnRemoteMachine.</span><span class="sxs-lookup"><span data-stu-id="94527-357">You can register the gateway on a remote machine by using the IsRegisterOnRemoteMachine parameter.</span></span> <span data-ttu-id="94527-358">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="94527-358">Example:</span></span>

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. <span data-ttu-id="94527-359">Você pode usar o cmdlet **Get-AzureRmDataFactoryGateway** para obter a lista de gateways no data factory.</span><span class="sxs-lookup"><span data-stu-id="94527-359">You can use the **Get-AzureRmDataFactoryGateway** cmdlet to get the list of Gateways in your data factory.</span></span> <span data-ttu-id="94527-360">Quando o **Status** mostra **online**, isso significa que seu gateway está pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="94527-360">When the **Status** shows **online**, it means your gateway is ready to use.</span></span>

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
<span data-ttu-id="94527-361">Você pode remover um gateway usando o cmdlet **Remove-AzureRmDataFactoryGateway** e atualizar a descrição de um gateway com os cmdlets **Set-AzureRmDataFactoryGateway** cmdlets.</span><span class="sxs-lookup"><span data-stu-id="94527-361">You can remove a gateway using the **Remove-AzureRmDataFactoryGateway** cmdlet and update description for a gateway using the **Set-AzureRmDataFactoryGateway** cmdlets.</span></span> <span data-ttu-id="94527-362">Para sintaxe e outros detalhes sobre esses cmdlets, consulte Referência de Cmdlet de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="94527-362">For syntax and other details about these cmdlets, see Data Factory Cmdlet Reference.</span></span>  

### <a name="list-gateways-using-powershell"></a><span data-ttu-id="94527-363">Listar gateways usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="94527-363">List gateways using PowerShell</span></span>

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a><span data-ttu-id="94527-364">Remover gateways usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="94527-364">Remove gateway using PowerShell</span></span>

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a><span data-ttu-id="94527-365">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="94527-365">Next steps</span></span>
* <span data-ttu-id="94527-366">Consulte o artigo [Mover os dados entre os armazenamentos de dados local e de nuvem](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="94527-366">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="94527-367">Neste passo a passo, você cria um pipeline que usa o gateway para mover dados de um banco de dados SQL Server local para um blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="94527-367">In the walkthrough, you create a pipeline that uses the gateway to move data from an on-premises SQL Server database to an Azure blob.</span></span>  
