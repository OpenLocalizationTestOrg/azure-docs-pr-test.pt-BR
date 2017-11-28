---
title: "aaaData Gateway de gerenciamento de fábrica de dados | Microsoft Docs"
description: Configurar um gateway toomove de dados entre locais e hello nuvem. Use o Gateway de gerenciamento de dados no Azure Data Factory toomove seus dados.
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
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a><span data-ttu-id="7b10b-104">Gateway de gerenciamento de dados</span><span class="sxs-lookup"><span data-stu-id="7b10b-104">Data Management Gateway</span></span>
<span data-ttu-id="7b10b-105">gateway de gerenciamento de dados de saudação é um agente de cliente que você deve instalar em seus dados de toocopy do ambiente local entre armazenamentos de dados locais e de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7b10b-105">hello Data management gateway is a client agent that you must install in your on-premises environment toocopy data between cloud and on-premises data stores.</span></span> <span data-ttu-id="7b10b-106">Olá dados repositórios com suporte pela fábrica de dados são listados no hello local [suporte para fontes de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) seção.</span><span class="sxs-lookup"><span data-stu-id="7b10b-106">hello on-premises data stores supported by Data Factory are listed in hello [Supported data sources](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span></span>

<span data-ttu-id="7b10b-107">Este artigo complementa Olá passo a passo em Olá [mover dados entre locais e na nuvem armazenamentos de dados](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="7b10b-107">This article complements hello walkthrough in hello [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="7b10b-108">Olá instruções passo a passo, você criará um pipeline que usa Olá gateway toomove dados de um tooan de banco de dados do SQL Server local BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b10b-108">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span> <span data-ttu-id="7b10b-109">Este artigo fornece informações detalhadas de detalhada sobre o gateway de gerenciamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b10b-109">This article provides detailed in-depth information about hello data management gateway.</span></span> 

<span data-ttu-id="7b10b-110">Você pode expandir um gateway de gerenciamento de dados por meio da associação várias máquinas locais com o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b10b-110">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="7b10b-111">Você pode escalar verticalmente com o aumento do número de trabalhos de movimentação de dados que podem ser executados simultaneamente em um nó.</span><span class="sxs-lookup"><span data-stu-id="7b10b-111">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="7b10b-112">Esse recurso também está disponível para um gateway lógico com um único nó.</span><span class="sxs-lookup"><span data-stu-id="7b10b-112">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="7b10b-113">Consulte o artigo [Escalar o Gateway de Gerenciamento de Dados no Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="7b10b-113">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>

> [!NOTE]
> <span data-ttu-id="7b10b-114">Atualmente, o gateway suporta apenas a atividade de cópia de saudação e a atividade de procedimento armazenado na fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="7b10b-114">Currently, gateway supports only hello copy activity and stored procedure activity in Data Factory.</span></span> <span data-ttu-id="7b10b-115">Não é possível toouse gateway de saudação uma atividade personalizada tooaccess locais de fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="7b10b-115">It is not possible toouse hello gateway from a custom activity tooaccess on-premises data sources.</span></span>      

## <a name="overview"></a><span data-ttu-id="7b10b-116">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7b10b-116">Overview</span></span>
### <a name="capabilities-of-data-management-gateway"></a><span data-ttu-id="7b10b-117">Funcionalidades do Gateway de Gerenciamento de Dados</span><span class="sxs-lookup"><span data-stu-id="7b10b-117">Capabilities of data management gateway</span></span>
<span data-ttu-id="7b10b-118">Gateway de gerenciamento de dados fornece Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b10b-118">Data management gateway provides hello following capabilities:</span></span>

* <span data-ttu-id="7b10b-119">Modelo de fontes de dados locais e fontes de dados de nuvem dentro Olá mesma fábrica de dados e movem dados.</span><span class="sxs-lookup"><span data-stu-id="7b10b-119">Model on-premises data sources and cloud data sources within hello same data factory and move data.</span></span>
* <span data-ttu-id="7b10b-120">Ter um único painel de controle para monitoramento e gerenciamento com visibilidade do status do gateway da página de fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-120">Have a single pane of glass for monitoring and management with visibility into gateway status from hello Data Factory page.</span></span>
* <span data-ttu-id="7b10b-121">Gerencie fontes de dados do access tooon local com segurança.</span><span class="sxs-lookup"><span data-stu-id="7b10b-121">Manage access tooon-premises data sources securely.</span></span>
  * <span data-ttu-id="7b10b-122">Nenhuma alteração necessária toocorporate firewall.</span><span class="sxs-lookup"><span data-stu-id="7b10b-122">No changes required toocorporate firewall.</span></span> <span data-ttu-id="7b10b-123">Gateway faz apenas conexões de saída com base em HTTP tooopen internet.</span><span class="sxs-lookup"><span data-stu-id="7b10b-123">Gateway only makes outbound HTTP-based connections tooopen internet.</span></span>
  * <span data-ttu-id="7b10b-124">Criptografar credenciais para seus armazenamentos de dados locais com seu certificado.</span><span class="sxs-lookup"><span data-stu-id="7b10b-124">Encrypt credentials for your on-premises data stores with your certificate.</span></span>
* <span data-ttu-id="7b10b-125">Mover dados com eficiência – os dados são transferidos no toointermittent paralela e resiliente a problemas de rede com lógica de repetição automática.</span><span class="sxs-lookup"><span data-stu-id="7b10b-125">Move data efficiently – data is transferred in parallel, resilient toointermittent network issues with auto retry logic.</span></span>

### <a name="command-flow-and-data-flow"></a><span data-ttu-id="7b10b-126">Fluxo de comando e fluxo de dados</span><span class="sxs-lookup"><span data-stu-id="7b10b-126">Command flow and data flow</span></span>
<span data-ttu-id="7b10b-127">Quando você usa um copiar atividade toocopy dados entre locais e na nuvem, a atividade de saudação usa dados de tootransfer um gateway do toocloud de fonte de dados local e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="7b10b-127">When you use a copy activity toocopy data between on-premises and cloud, hello activity uses a gateway tootransfer data from on-premises data source toocloud and vice versa.</span></span>

<span data-ttu-id="7b10b-128">Aqui está Olá fluxo de dados de alto nível para e resumo das etapas para a cópia com o gateway de dados: ![fluxo de dados usando o gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span><span class="sxs-lookup"><span data-stu-id="7b10b-128">Here is hello high-level data flow for and summary of steps for copy with data gateway: ![Data flow using gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span></span>

1. <span data-ttu-id="7b10b-129">Desenvolvedor de dados cria um gateway para uma fábrica de dados do Azure usando o hello [portal do Azure](https://portal.azure.com) ou [Cmdlet do PowerShell](https://msdn.microsoft.com/library/dn820234.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b10b-129">Data developer creates a gateway for an Azure Data Factory using either hello [Azure portal](https://portal.azure.com) or [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span></span>
2. <span data-ttu-id="7b10b-130">Desenvolvedor de dados cria um serviço vinculado para um repositório de dados local, especificando o gateway hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-130">Data developer creates a linked service for an on-premises data store by specifying hello gateway.</span></span> <span data-ttu-id="7b10b-131">Como parte da configuração saudação do serviço vinculado, o desenvolvedor de dados usa as credenciais e tipos de autenticação Olá definindo credenciais aplicativo toospecify.</span><span class="sxs-lookup"><span data-stu-id="7b10b-131">As part of setting up hello linked service, data developer uses hello Setting Credentials application toospecify authentication types and credentials.</span></span>  <span data-ttu-id="7b10b-132">caixa de diálogo do aplicativo se comunica com dados de saudação do Hello definindo credenciais armazenar tootest conexão e hello toosave credenciais do gateway.</span><span class="sxs-lookup"><span data-stu-id="7b10b-132">hello Setting Credentials application dialog communicates with hello data store tootest connection and hello gateway toosave credentials.</span></span>
3. <span data-ttu-id="7b10b-133">Gateway criptografa credenciais Olá com certificado Olá associado gateway hello (fornecido pelo desenvolvedor de dados), antes de salvar credenciais Olá na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-133">Gateway encrypts hello credentials with hello certificate associated with hello gateway (supplied by data developer), before saving hello credentials in hello cloud.</span></span>
4. <span data-ttu-id="7b10b-134">Serviço de fábrica de dados se comunica com o gateway Olá para agendamento e gerenciamento de trabalhos através de um canal de controle que usa uma fila do barramento do serviço compartilhado do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b10b-134">Data Factory service communicates with hello gateway for scheduling & management of jobs via a control channel that uses a shared Azure service bus queue.</span></span> <span data-ttu-id="7b10b-135">Quando um trabalho de atividade de cópia precisa toobe foi iniciada, Data Factory filas solicitação Olá juntamente com informações de credenciais.</span><span class="sxs-lookup"><span data-stu-id="7b10b-135">When a copy activity job needs toobe kicked off, Data Factory queues hello request along with credential information.</span></span> <span data-ttu-id="7b10b-136">Gateway inicia o trabalho de saudação após sondagem Olá fila.</span><span class="sxs-lookup"><span data-stu-id="7b10b-136">Gateway kicks off hello job after polling hello queue.</span></span>
5. <span data-ttu-id="7b10b-137">gateway Olá descriptografa as credenciais de saudação com hello mesmo certificado e, em seguida, conecta-se o repositório de dados do local de toohello com as credenciais e o tipo de autenticação adequada.</span><span class="sxs-lookup"><span data-stu-id="7b10b-137">hello gateway decrypts hello credentials with hello same certificate and then connects toohello on-premises data store with proper authentication type and credentials.</span></span>
6. <span data-ttu-id="7b10b-138">gateway Olá copia dados de um armazenamento de nuvem no local repositório tooa, ou vice-versa dependendo de como hello atividade de cópia é configurado no pipeline de saudação de dados.</span><span class="sxs-lookup"><span data-stu-id="7b10b-138">hello gateway copies data from an on-premises store tooa cloud storage, or vice versa depending on how hello Copy Activity is configured in hello data pipeline.</span></span> <span data-ttu-id="7b10b-139">Nesta etapa, gateway Olá se comunica diretamente com os serviços de armazenamento baseado em nuvem, como o armazenamento de BLOBs do Azure por um canal seguro de (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="7b10b-139">For this step, hello gateway directly communicates with cloud-based storage services such as Azure Blob Storage over a secure (HTTPS) channel.</span></span>

### <a name="considerations-for-using-gateway"></a><span data-ttu-id="7b10b-140">Considerações para o uso do gateway</span><span class="sxs-lookup"><span data-stu-id="7b10b-140">Considerations for using gateway</span></span>
* <span data-ttu-id="7b10b-141">Uma única instância do Gateway de Gerenciamento de Dados pode ser usada para várias fontes de dados locais.</span><span class="sxs-lookup"><span data-stu-id="7b10b-141">A single instance of data management gateway can be used for multiple on-premises data sources.</span></span> <span data-ttu-id="7b10b-142">No entanto, **uma única instância do gateway é uma fábrica de dados do Azure associado tooonly** e não pode ser compartilhada com outro fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="7b10b-142">However, **a single gateway instance is tied tooonly one Azure data factory** and cannot be shared with another data factory.</span></span>
* <span data-ttu-id="7b10b-143">Você pode ter **apenas uma instância do Gateway de Gerenciamento de Dados** instalada em um único computador.</span><span class="sxs-lookup"><span data-stu-id="7b10b-143">You can have **only one instance of data management gateway** installed on a single machine.</span></span> <span data-ttu-id="7b10b-144">Suponha que, você tem duas fábricas de dados que precisam de fontes de dados do tooaccess no local, você precisa tooinstall gateways em computadores de dois locais.</span><span class="sxs-lookup"><span data-stu-id="7b10b-144">Suppose, you have two data factories that need tooaccess on-premises data sources, you need tooinstall gateways on two on-premises computers.</span></span> <span data-ttu-id="7b10b-145">Em outras palavras, um gateway é tooa empatados fábrica de dados específicos</span><span class="sxs-lookup"><span data-stu-id="7b10b-145">In other words, a gateway is tied tooa specific data factory</span></span>
* <span data-ttu-id="7b10b-146">Olá **gateway não precisa toobe em Olá mesmo computador como fonte de dados Olá**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-146">hello **gateway does not need toobe on hello same machine as hello data source**.</span></span> <span data-ttu-id="7b10b-147">No entanto, com a fonte de dados de toohello mais próximo do gateway reduz o tempo de Olá Olá gateway tooconnect toohello fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="7b10b-147">However, having gateway closer toohello data source reduces hello time for hello gateway tooconnect toohello data source.</span></span> <span data-ttu-id="7b10b-148">É recomendável que você instale o gateway de saudação em um computador diferente do hello uma fonte de dados local hosts.</span><span class="sxs-lookup"><span data-stu-id="7b10b-148">We recommend that you install hello gateway on a machine that is different from hello one that hosts on-premises data source.</span></span> <span data-ttu-id="7b10b-149">Quando Olá gateway e fonte de dados estiverem em computadores diferentes, o gateway de saudação não disputam os recursos com a fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="7b10b-149">When hello gateway and data source are on different machines, hello gateway does not compete for resources with data source.</span></span>
* <span data-ttu-id="7b10b-150">Você pode ter **vários gateways em máquinas diferentes conectando toohello mesma fonte de dados local**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-150">You can have **multiple gateways on different machines connecting toohello same on-premises data source**.</span></span> <span data-ttu-id="7b10b-151">Por exemplo, você pode ter dois gateways que atende as fábricas de duas dados mas Olá a mesma fonte de dados local está registrado com ambas as fábricas de dados hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-151">For example, you may have two gateways serving two data factories but hello same on-premises data source is registered with both hello data factories.</span></span>
* <span data-ttu-id="7b10b-152">Se você já tiver um gateway instalado no computador atendendo um cenário do **Power BI**, instale um gateway **separado para o Azure Data Factory** em outro computador.</span><span class="sxs-lookup"><span data-stu-id="7b10b-152">If you already have a gateway installed on your computer serving a **Power BI** scenario, install a **separate gateway for Azure Data Factory** on another machine.</span></span>
* <span data-ttu-id="7b10b-153">O gateway deve ser usado mesmo quando você usar o **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-153">Gateway must be used even when you use **ExpressRoute**.</span></span>
* <span data-ttu-id="7b10b-154">Trate a fonte de dados como local (isto é, protegida por um firewall) mesmo quando você usar o **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-154">Treat your data source as an on-premises data source (that is behind a firewall) even when you use **ExpressRoute**.</span></span> <span data-ttu-id="7b10b-155">Use Olá gateway tooestablish conectividade entre o serviço hello e fonte de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b10b-155">Use hello gateway tooestablish connectivity between hello service and hello data source.</span></span>
* <span data-ttu-id="7b10b-156">Você deve **usar gateway Olá** mesmo se Olá repositório de dados está na nuvem de saudação em uma **Azure IaaS VM**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-156">You must **use hello gateway** even if hello data store is in hello cloud on an **Azure IaaS VM**.</span></span>

## <a name="installation"></a><span data-ttu-id="7b10b-157">Instalação</span><span class="sxs-lookup"><span data-stu-id="7b10b-157">Installation</span></span>
### <a name="prerequisites"></a><span data-ttu-id="7b10b-158">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7b10b-158">Prerequisites</span></span>
* <span data-ttu-id="7b10b-159">Olá suportada **sistema operacional** versões são Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="7b10b-159">hello supported **Operating System** versions are Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span></span> <span data-ttu-id="7b10b-160">Instalação do gateway de gerenciamento de dados de saudação em um controlador de domínio não é suportada atualmente.</span><span class="sxs-lookup"><span data-stu-id="7b10b-160">Installation of hello data management gateway on a domain controller is currently not supported.</span></span>
* <span data-ttu-id="7b10b-161">O .NET framework 4.5.1 ou superior é necessário.</span><span class="sxs-lookup"><span data-stu-id="7b10b-161">.NET Framework 4.5.1 or above is required.</span></span> <span data-ttu-id="7b10b-162">Se você estiver instalando o gateway em um computador com Windows 7, instale o .NET Framework 4.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7b10b-162">If you are installing gateway on a Windows 7 machine, install .NET Framework 4.5 or later.</span></span> <span data-ttu-id="7b10b-163">Confira [Requisitos de sistema do .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="7b10b-163">See [.NET Framework System Requirements](https://msdn.microsoft.com/library/8z6watww.aspx) for details.</span></span>
* <span data-ttu-id="7b10b-164">Olá recomendado **configuração** máquina de gateway de saudação é pelo menos 2 GHz, 4 núcleos, 8 GB de RAM e 80 GB de disco.</span><span class="sxs-lookup"><span data-stu-id="7b10b-164">hello recommended **configuration** for hello gateway machine is at least 2 GHz, 4 cores, 8-GB RAM, and 80-GB disk.</span></span>
* <span data-ttu-id="7b10b-165">Se a máquina de host Olá hibernação, gateway Olá não responde solicitações toodata.</span><span class="sxs-lookup"><span data-stu-id="7b10b-165">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span> <span data-ttu-id="7b10b-166">Portanto, configurar adequados **plano de energia** no computador de saudação antes de instalar o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b10b-166">Therefore, configure an appropriate **power plan** on hello computer before installing hello gateway.</span></span> <span data-ttu-id="7b10b-167">Se máquina Olá for toohibernate configurado, instalação do gateway Olá solicita uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="7b10b-167">If hello machine is configured toohibernate, hello gateway installation prompts a message.</span></span>
* <span data-ttu-id="7b10b-168">Você deve ser um administrador no hello máquina tooinstall e configurar o gateway de gerenciamento de dados de saudação com êxito.</span><span class="sxs-lookup"><span data-stu-id="7b10b-168">You must be an administrator on hello machine tooinstall and configure hello data management gateway successfully.</span></span> <span data-ttu-id="7b10b-169">Você pode adicionar usuários adicionais toohello **gateway de gerenciamento de dados usuários** grupo local do Windows.</span><span class="sxs-lookup"><span data-stu-id="7b10b-169">You can add additional users toohello **data management gateway Users** local Windows group.</span></span> <span data-ttu-id="7b10b-170">membros desse grupo Olá são Olá capaz de toouse **Gerenciador de configuração de Gateway de gerenciamento de dados** gateway de saudação tooconfigure ferramenta.</span><span class="sxs-lookup"><span data-stu-id="7b10b-170">hello members of this group are able toouse hello **Data Management Gateway Configuration Manager** tool tooconfigure hello gateway.</span></span>

<span data-ttu-id="7b10b-171">Como copiar atividade executa acontecer em uma frequência específica, hello uso de recursos (CPU, memória) no computador de saudação também segue Olá mesmo padrão com o horário de pico e ocioso.</span><span class="sxs-lookup"><span data-stu-id="7b10b-171">As copy activity runs happen on a specific frequency, hello resource usage (CPU, memory) on hello machine also follows hello same pattern with peak and idle times.</span></span> <span data-ttu-id="7b10b-172">Utilização de recursos também depende intensamente Olá quantidade de dados que está sendo movidos.</span><span class="sxs-lookup"><span data-stu-id="7b10b-172">Resource utilization also depends heavily on hello amount of data being moved.</span></span> <span data-ttu-id="7b10b-173">Quando vários trabalhos de cópia estiverem em andamento, você verá o uso do recurso aumentar durante horários de pico.</span><span class="sxs-lookup"><span data-stu-id="7b10b-173">When multiple copy jobs are in progress, you see resource usage go up during peak times.</span></span>

### <a name="installation-options"></a><span data-ttu-id="7b10b-174">Opções de instalação</span><span class="sxs-lookup"><span data-stu-id="7b10b-174">Installation options</span></span>
<span data-ttu-id="7b10b-175">Gateway de gerenciamento de dados pode ser instalado em Olá maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b10b-175">Data management gateway can be installed in hello following ways:</span></span>

* <span data-ttu-id="7b10b-176">Ao baixar um pacote de instalação do MSI da saudação [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="7b10b-176">By downloading an MSI setup package from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>  <span data-ttu-id="7b10b-177">Olá MSI também pode ser usado tooupgrade existente dados gerenciamento gateway toohello versão mais recente, com todas as configurações preservadas.</span><span class="sxs-lookup"><span data-stu-id="7b10b-177">hello MSI can also be used tooupgrade existing data management gateway toohello latest version, with all settings preserved.</span></span>
* <span data-ttu-id="7b10b-178">Clicando no link **Baixar e instalar o gateway de dados** em INSTALAÇÃO MANUAL ou **Instalar diretamente neste computador** em INSTALAÇÃO EXPRESSA.</span><span class="sxs-lookup"><span data-stu-id="7b10b-178">By clicking **Download and install data gateway** link under MANUAL SETUP or **Install directly on this computer** under EXPRESS SETUP.</span></span> <span data-ttu-id="7b10b-179">Veja o artigo [Mover dados entre locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo sobre como usar a instalação expressa.</span><span class="sxs-lookup"><span data-stu-id="7b10b-179">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on using express setup.</span></span> <span data-ttu-id="7b10b-180">etapa manual Olá leva toohello Centro de download.</span><span class="sxs-lookup"><span data-stu-id="7b10b-180">hello manual step takes you toohello download center.</span></span>  <span data-ttu-id="7b10b-181">Olá instruções para baixar e instalar o gateway de saudação do Centro de download são na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="7b10b-181">hello instructions for downloading and installing hello gateway from download center are in hello next section.</span></span>

### <a name="installation-best-practices"></a><span data-ttu-id="7b10b-182">Práticas recomendadas de instalação:</span><span class="sxs-lookup"><span data-stu-id="7b10b-182">Installation best practices:</span></span>
1. <span data-ttu-id="7b10b-183">Configure plano de energia no computador de host Olá para o gateway de saudação para que hello máquina não entra em hibernação.</span><span class="sxs-lookup"><span data-stu-id="7b10b-183">Configure power plan on hello host machine for hello gateway so that hello machine does not hibernate.</span></span> <span data-ttu-id="7b10b-184">Se a máquina de host Olá hibernação, gateway Olá não responde solicitações toodata.</span><span class="sxs-lookup"><span data-stu-id="7b10b-184">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span>
2. <span data-ttu-id="7b10b-185">Fazer backup de certificado Olá associado Olá gateway.</span><span class="sxs-lookup"><span data-stu-id="7b10b-185">Back up hello certificate associated with hello gateway.</span></span>

### <a name="install-hello-gateway-from-download-center"></a><span data-ttu-id="7b10b-186">Instalar o gateway de saudação do Centro de download</span><span class="sxs-lookup"><span data-stu-id="7b10b-186">Install hello gateway from download center</span></span>
1. <span data-ttu-id="7b10b-187">Navegue muito[página de download da Microsoft Data Management Gateway](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="7b10b-187">Navigate too[Microsoft Data Management Gateway download page](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>
2. <span data-ttu-id="7b10b-188">Clique em **baixar**, selecione Olá versão apropriada (**32-bit** vs. **64 bits**) e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-188">Click **Download**, select hello appropriate version (**32-bit** vs. **64-bit**), and click **Next**.</span></span>
3. <span data-ttu-id="7b10b-189">Executar Olá **MSI** diretamente ou salvá-lo tooyour disco e execute.</span><span class="sxs-lookup"><span data-stu-id="7b10b-189">Run hello **MSI** directly or save it tooyour hard disk and run.</span></span>
4. <span data-ttu-id="7b10b-190">Em Olá **bem-vindo** página, selecione um **idioma** clique **próximo**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-190">On hello **Welcome** page, select a **language** click **Next**.</span></span>
5. <span data-ttu-id="7b10b-191">**Aceitar** Olá contrato de licença de usuário final e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-191">**Accept** hello End-User License Agreement and click **Next**.</span></span>
6. <span data-ttu-id="7b10b-192">Selecione **pasta** tooinstall Olá gateway e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-192">Select **folder** tooinstall hello gateway and click **Next**.</span></span>
7. <span data-ttu-id="7b10b-193">Em Olá **tooinstall pronto** , clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-193">On hello **Ready tooinstall** page, click **Install**.</span></span>
8. <span data-ttu-id="7b10b-194">Clique em **concluir** toocomplete instalação.</span><span class="sxs-lookup"><span data-stu-id="7b10b-194">Click **Finish** toocomplete installation.</span></span>
9. <span data-ttu-id="7b10b-195">Obter chave de saudação do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b10b-195">Get hello key from hello Azure portal.</span></span> <span data-ttu-id="7b10b-196">Consulte a próxima seção Olá para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="7b10b-196">See hello next section for step-by-step instructions.</span></span>
10. <span data-ttu-id="7b10b-197">Em Olá **registrar gateway** página de **Gerenciador de configuração de Gateway de gerenciamento de dados** em execução no seu computador, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7b10b-197">On hello **Register gateway** page of **Data Management Gateway Configuration Manager** running on your machine, do hello following steps:</span></span>
    1. <span data-ttu-id="7b10b-198">Cole a chave de saudação em texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b10b-198">Paste hello key in hello text.</span></span>
    2. <span data-ttu-id="7b10b-199">Opcionalmente, clique em **chave do gateway Mostrar** texto da tecla toosee hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-199">Optionally, click **Show gateway key** toosee hello key text.</span></span>
    3. <span data-ttu-id="7b10b-200">Clique em **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-200">Click **Register**.</span></span>

### <a name="register-gateway-using-key"></a><span data-ttu-id="7b10b-201">Registrar gateway usando chave</span><span class="sxs-lookup"><span data-stu-id="7b10b-201">Register gateway using key</span></span>
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a><span data-ttu-id="7b10b-202">Se você já não criou um gateway lógico no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="7b10b-202">If you haven't already created a logical gateway in hello portal</span></span>
<span data-ttu-id="7b10b-203">toocreate um gateway na chave de saudação de portal e get hello da saudação **configurar** página, execute estas etapas do passo a passo em Olá [mover dados entre locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="7b10b-203">toocreate a gateway in hello portal and get hello key from hello **Configure** page, Follow steps from walkthrough in hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a><span data-ttu-id="7b10b-204">Se você já tiver criado o gateway lógico Olá no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="7b10b-204">If you have already created hello logical gateway in hello portal</span></span>
1. <span data-ttu-id="7b10b-205">No portal do Azure, navegue até toohello **Data Factory** página e, em seguida, clique em **serviços vinculados** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="7b10b-205">In Azure portal, navigate toohello **Data Factory** page, and click **Linked Services** tile.</span></span>

    ![Página Data Factory](media/data-factory-data-management-gateway/data-factory-blade.png)
2. <span data-ttu-id="7b10b-207">Em Olá **serviços vinculados** página, selecione Olá lógica **gateway** criado no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b10b-207">In hello **Linked Services** page, select hello logical **gateway** you created in hello portal.</span></span>

    ![gateway lógico](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. <span data-ttu-id="7b10b-209">Em Olá **Gateway de dados** , clique em **baixar e instalar o gateway de dados**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-209">In hello **Data Gateway** page, click **Download and install data gateway**.</span></span>

    ![Baixe o link no portal de saudação](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. <span data-ttu-id="7b10b-211">Em Olá **configurar** , clique em **chave recrie**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-211">In hello **Configure** page, click **Recreate key**.</span></span> <span data-ttu-id="7b10b-212">Clique em Sim na mensagem de saudação do aviso depois de ler cuidadosamente.</span><span class="sxs-lookup"><span data-stu-id="7b10b-212">Click Yes on hello warning message after reading it carefully.</span></span>

    ![Recriar chave](media/data-factory-data-management-gateway/recreate-key-button.png)
5. <span data-ttu-id="7b10b-214">Clique em copiar botão Avançar toohello chave.</span><span class="sxs-lookup"><span data-stu-id="7b10b-214">Click Copy button next toohello key.</span></span> <span data-ttu-id="7b10b-215">chave de saudação é toohello copiado na área de transferência.</span><span class="sxs-lookup"><span data-stu-id="7b10b-215">hello key is copied toohello clipboard.</span></span>

    ![Copiar chave](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a><span data-ttu-id="7b10b-217">Ícones/notificações da bandeja do sistema</span><span class="sxs-lookup"><span data-stu-id="7b10b-217">System tray icons/ notifications</span></span>
<span data-ttu-id="7b10b-218">Olá imagem a seguir mostra algumas das Olá ícones da bandeja do que você vê.</span><span class="sxs-lookup"><span data-stu-id="7b10b-218">hello following image shows some of hello tray icons that you see.</span></span>

![ícones da bandeja do sistema](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

<span data-ttu-id="7b10b-220">Se você mover o cursor sobre a mensagem de ícone e notificação da bandeja de sistema hello, você verá detalhes sobre o estado de saudação da operação de atualização do gateway de saudação em uma janela pop-up.</span><span class="sxs-lookup"><span data-stu-id="7b10b-220">If you move cursor over hello system tray icon/notification message, you see details about hello state of hello gateway/update operation in a popup window.</span></span>

### <a name="ports-and-firewall"></a><span data-ttu-id="7b10b-221">Portas e firewall</span><span class="sxs-lookup"><span data-stu-id="7b10b-221">Ports and firewall</span></span>
<span data-ttu-id="7b10b-222">Há dois firewalls, você precisa tooconsider: **firewall corporativo** em execução no roteador central de saudação da organização Olá, e **firewall do Windows** configurado como um daemon na máquina local Olá onde hello gateway está instalado.</span><span class="sxs-lookup"><span data-stu-id="7b10b-222">There are two firewalls you need tooconsider: **corporate firewall** running on hello central router of hello organization, and **Windows firewall** configured as a daemon on hello local machine where hello gateway is installed.</span></span>  

![firewalls](./media/data-factory-data-management-gateway/firewalls2.png)

<span data-ttu-id="7b10b-224">No nível do firewall corporativo, você precisa configurar o seguinte Olá domínios e portas de saída:</span><span class="sxs-lookup"><span data-stu-id="7b10b-224">At corporate firewall level, you need configure hello following domains and outbound ports:</span></span>

| <span data-ttu-id="7b10b-225">Nomes de domínio</span><span class="sxs-lookup"><span data-stu-id="7b10b-225">Domain names</span></span> | <span data-ttu-id="7b10b-226">Portas</span><span class="sxs-lookup"><span data-stu-id="7b10b-226">Ports</span></span> | <span data-ttu-id="7b10b-227">Descrição</span><span class="sxs-lookup"><span data-stu-id="7b10b-227">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b10b-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="7b10b-228">*.servicebus.windows.net</span></span> |<span data-ttu-id="7b10b-229">443, 80</span><span class="sxs-lookup"><span data-stu-id="7b10b-229">443, 80</span></span> |<span data-ttu-id="7b10b-230">Usado para comunicação com o back-end do Serviço de Movimentação de Dados</span><span class="sxs-lookup"><span data-stu-id="7b10b-230">Used for communication with Data Movement Service backend</span></span> |
| <span data-ttu-id="7b10b-231">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="7b10b-231">*.core.windows.net</span></span> |<span data-ttu-id="7b10b-232">443</span><span class="sxs-lookup"><span data-stu-id="7b10b-232">443</span></span> |<span data-ttu-id="7b10b-233">Usado para cópia em etapas usando Blobs do Azure (se estiver configurado)</span><span class="sxs-lookup"><span data-stu-id="7b10b-233">Used for Staged copy using Azure Blob (if configured)</span></span>|
| <span data-ttu-id="7b10b-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="7b10b-234">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="7b10b-235">443</span><span class="sxs-lookup"><span data-stu-id="7b10b-235">443</span></span> |<span data-ttu-id="7b10b-236">Usado para comunicação com o back-end do Serviço de Movimentação de Dados</span><span class="sxs-lookup"><span data-stu-id="7b10b-236">Used for communication with Data Movement Service backend</span></span> |


<span data-ttu-id="7b10b-237">No nível do Firewall do Windows, essas portas de saída normalmente são habilitadas.</span><span class="sxs-lookup"><span data-stu-id="7b10b-237">At Windows firewall level, these outbound ports are normally enabled.</span></span> <span data-ttu-id="7b10b-238">Se não, você pode configurar portas e domínios Olá adequadamente no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="7b10b-238">If not, you can configure hello domains and ports accordingly on gateway machine.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="7b10b-239">Com base em sua origem / coletores, você pode ter domínios adicionais toowhitelist e portas de saída em sua empresa/firewall do Windows.</span><span class="sxs-lookup"><span data-stu-id="7b10b-239">Based on your source/ sinks, you may have toowhitelist additional domains and outbound ports in your corporate/Windows firewall.</span></span>
> 2. <span data-ttu-id="7b10b-240">Para alguns bancos de dados de nuvem (por exemplo: [banco de dados do SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), talvez seja necessário toowhitelist endereço IP do computador do Gateway em sua configuração de firewall.</span><span class="sxs-lookup"><span data-stu-id="7b10b-240">For some Cloud Databases (For example: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), you may need toowhitelist IP address of Gateway machine on their firewall configuration.</span></span>
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a><span data-ttu-id="7b10b-241">Copiar dados de um repositório de dados fonte dados repositório tooa coletor</span><span class="sxs-lookup"><span data-stu-id="7b10b-241">Copy data from a source data store tooa sink data store</span></span>
<span data-ttu-id="7b10b-242">Verifique se as regras de firewall Olá estão habilitadas corretamente no firewall corporativo hello, firewall do Windows no computador do gateway Olá, e do repositório de dados de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="7b10b-242">Ensure that hello firewall rules are enabled properly on hello corporate firewall, Windows firewall on hello gateway machine, and hello data store itself.</span></span> <span data-ttu-id="7b10b-243">Essas regras permite Olá fonte do gateway tooconnect tooboth e coletar com êxito.</span><span class="sxs-lookup"><span data-stu-id="7b10b-243">Enabling these rules allows hello gateway tooconnect tooboth source and sink successfully.</span></span> <span data-ttu-id="7b10b-244">Habilite regras para cada repositório de dados que está envolvido na operação de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b10b-244">Enable rules for each data store that is involved in hello copy operation.</span></span>

<span data-ttu-id="7b10b-245">Por exemplo, toocopy de **um coletor de banco de dados SQL local dados repositório tooan ou um coletor do Azure SQL Data Warehouse**, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7b10b-245">For example, toocopy from **an on-premises data store tooan Azure SQL Database sink or an Azure SQL Data Warehouse sink**, do hello following steps:</span></span>

* <span data-ttu-id="7b10b-246">Permitir a comunicação **TCP** de saída na porta **1433** para o firewall do Windows e o firewall corporativo.</span><span class="sxs-lookup"><span data-stu-id="7b10b-246">Allow outbound **TCP** communication on port **1433** for both Windows firewall and corporate firewall.</span></span>
* <span data-ttu-id="7b10b-247">Definir configurações de firewall de saudação do endereço IP saudação do SQL Azure server tooadd de saudação gateway máquina toohello a lista de endereços IP permitidos.</span><span class="sxs-lookup"><span data-stu-id="7b10b-247">Configure hello firewall settings of Azure SQL server tooadd hello IP address of hello gateway machine toohello list of allowed IP addresses.</span></span>

> [!NOTE]
> <span data-ttu-id="7b10b-248">Se o firewall não permitir a porta de saída 1433, o Gateway não poderá acessar diretamente o Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="7b10b-248">If your firewall does not allow outbound port 1433, Gateway can't access Azure SQL directly.</span></span> <span data-ttu-id="7b10b-249">Nesse caso, você pode usar [cópia preparados](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL banco de dados do Azure / DW do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7b10b-249">In this case, you may use [Staged Copy](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Azure Database/ SQL Azure DW.</span></span> <span data-ttu-id="7b10b-250">Nesse cenário, exigiria apenas HTTPS (porta 443) Olá para movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="7b10b-250">In this scenario, you would only require HTTPS (port 443) for hello data movement.</span></span>
>
>


### <a name="proxy-server-considerations"></a><span data-ttu-id="7b10b-251">Considerações do servidor proxy</span><span class="sxs-lookup"><span data-stu-id="7b10b-251">Proxy server considerations</span></span>
<span data-ttu-id="7b10b-252">Se seu ambiente de rede corporativa usar um proxy server tooaccess Olá da internet, definir configurações de proxy adequadas toouse do gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="7b10b-252">If your corporate network environment uses a proxy server tooaccess hello internet, configure data management gateway toouse appropriate proxy settings.</span></span> <span data-ttu-id="7b10b-253">Você pode definir o proxy Olá durante a fase de registro inicial hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-253">You can set hello proxy during hello initial registration phase.</span></span>

![Definir proxy durante o registro](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

<span data-ttu-id="7b10b-255">O gateway usa o serviço de nuvem do hello proxy server tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-255">Gateway uses hello proxy server tooconnect toohello cloud service.</span></span> <span data-ttu-id="7b10b-256">Clique no link **Alteração** durante a configuração inicial.</span><span class="sxs-lookup"><span data-stu-id="7b10b-256">Click **Change** link during initial setup.</span></span> <span data-ttu-id="7b10b-257">Consulte Olá **configuração de proxy** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7b10b-257">You see hello **proxy setting** dialog.</span></span>

![Definir proxy usando o gerenciador de configurações](media/data-factory-data-management-gateway/SetProxySettings.png)

<span data-ttu-id="7b10b-259">Há três opções de configuração:</span><span class="sxs-lookup"><span data-stu-id="7b10b-259">There are three configuration options:</span></span>

* <span data-ttu-id="7b10b-260">**Não use proxy**: Gateway não usa qualquer serviço do proxy tooconnect toocloud explicitamente.</span><span class="sxs-lookup"><span data-stu-id="7b10b-260">**Do not use proxy**: Gateway does not explicitly use any proxy tooconnect toocloud services.</span></span>
* <span data-ttu-id="7b10b-261">**Use o proxy do sistema**: o Gateway usa o proxy Olá configuração que é configurado no diahost.exe.config e diawp.exe.config.  Se nenhum proxy está configurado no diahost.exe.config e diawp.exe.config, o gateway conecta toocloud serviço diretamente, sem passar por meio do proxy.</span><span class="sxs-lookup"><span data-stu-id="7b10b-261">**Use system proxy**: Gateway uses hello proxy setting that is configured in diahost.exe.config and diawp.exe.config.  If no proxy is configured in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span>
* <span data-ttu-id="7b10b-262">**Usar proxy personalizado**: configurar Olá HTTP toouse de configuração de proxy para o gateway, em vez de usar as configurações no diahost.exe.config e diawp.exe.config.  Endereço e porta são necessários.</span><span class="sxs-lookup"><span data-stu-id="7b10b-262">**Use custom proxy**: Configure hello HTTP proxy setting toouse for gateway, instead of using configurations in diahost.exe.config and diawp.exe.config.  Address and Port are required.</span></span>  <span data-ttu-id="7b10b-263">O Nome de Usuário e a Senha são opcionais, dependendo da configuração de autenticação do seu proxy.</span><span class="sxs-lookup"><span data-stu-id="7b10b-263">User Name and Password are optional depending on your proxy’s authentication setting.</span></span>  <span data-ttu-id="7b10b-264">Todas as configurações são criptografadas com o certificado de credencial de saudação do gateway hello e armazenadas localmente no computador de host do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b10b-264">All settings are encrypted with hello credential certificate of hello gateway and stored locally on hello gateway host machine.</span></span>

<span data-ttu-id="7b10b-265">gateway de gerenciamento de dados Olá Host de serviço é reiniciado automaticamente depois de salvar as configurações de proxy Olá atualizado.</span><span class="sxs-lookup"><span data-stu-id="7b10b-265">hello data management gateway Host Service restarts automatically after you save hello updated proxy settings.</span></span>

<span data-ttu-id="7b10b-266">Depois que o gateway foi registrado com sucesso, se você quiser tooview ou atualizar as configurações de proxy, use o Gerenciador de configuração de Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="7b10b-266">After gateway has been successfully registered, if you want tooview or update proxy settings, use Data Management Gateway Configuration Manager.</span></span>

1. <span data-ttu-id="7b10b-267">Iniciar o **Gerenciador de Configuração de Gateway de Gerenciamento de Dados**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-267">Launch **Data Management Gateway Configuration Manager**.</span></span>
2. <span data-ttu-id="7b10b-268">Alternar toohello **configurações** guia.</span><span class="sxs-lookup"><span data-stu-id="7b10b-268">Switch toohello **Settings** tab.</span></span>
3. <span data-ttu-id="7b10b-269">Clique em **alteração** link no **HTTP Proxy** Olá de toolaunch seção **definir Proxy HTTP** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7b10b-269">Click **Change** link in **HTTP Proxy** section toolaunch hello **Set HTTP Proxy** dialog.</span></span>  
4. <span data-ttu-id="7b10b-270">Depois de clicar em Olá **próximo** botão, verá uma caixa de diálogo de aviso solicitando sua permissão toosave Olá configuração do proxy e a reinicialização Olá serviço de Host do Gateway.</span><span class="sxs-lookup"><span data-stu-id="7b10b-270">After you click hello **Next** button, you see a warning dialog asking for your permission toosave hello proxy setting and restart hello Gateway Host Service.</span></span>

<span data-ttu-id="7b10b-271">Você pode exibir e atualizar o proxy HTTP usando a ferramenta Gerenciador de Configurações.</span><span class="sxs-lookup"><span data-stu-id="7b10b-271">You can view and update HTTP proxy by using Configuration Manager tool.</span></span>

![Definir proxy usando o gerenciador de configurações](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> <span data-ttu-id="7b10b-273">Se você configurar um servidor proxy com autenticação NTLM, o serviço de Host do Gateway é executado na conta de domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b10b-273">If you set up a proxy server with NTLM authentication, Gateway Host Service runs under hello domain account.</span></span> <span data-ttu-id="7b10b-274">Se você alterar a senha Olá Olá conta de domínio mais tarde, lembre-se de tooupdate definições de configuração para serviço hello e reiniciá-lo adequadamente.</span><span class="sxs-lookup"><span data-stu-id="7b10b-274">If you change hello password for hello domain account later, remember tooupdate configuration settings for hello service and restart it accordingly.</span></span> <span data-ttu-id="7b10b-275">Devido a requisitos de toothis, sugerimos que você usar um servidor de proxy de saudação domínio dedicada conta tooaccess que não exigir senha de saudação tooupdate com frequência.</span><span class="sxs-lookup"><span data-stu-id="7b10b-275">Due toothis requirement, we suggest you use a dedicated domain account tooaccess hello proxy server that does not require you tooupdate hello password frequently.</span></span>
>
>

### <a name="configure-proxy-server-settings"></a><span data-ttu-id="7b10b-276">Definir configurações do servidor proxy</span><span class="sxs-lookup"><span data-stu-id="7b10b-276">Configure proxy server settings</span></span>
<span data-ttu-id="7b10b-277">Se você selecionar **usar o proxy do sistema** configuração proxy Olá HTTP, o gateway usa Olá configuração do proxy no diahost.exe.config e diawp.exe.config.  Se nenhum proxy for especificado em diahost.exe.config e diawp.exe.config, o gateway conecta toocloud serviço diretamente, sem passar por meio do proxy.</span><span class="sxs-lookup"><span data-stu-id="7b10b-277">If you select **Use system proxy** setting for hello HTTP proxy, gateway uses hello proxy setting in diahost.exe.config and diawp.exe.config.  If no proxy is specified in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span> <span data-ttu-id="7b10b-278">Olá procedimento a seguir fornece instruções para atualizar o arquivo de diahost.exe.config hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-278">hello following procedure provides instructions for updating hello diahost.exe.config file.</span></span>  

1. <span data-ttu-id="7b10b-279">No Explorador de arquivos, faça uma cópia de segurança do C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config tooback backup do arquivo original hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-279">In File Explorer, make a safe copy of C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config tooback up hello original file.</span></span>
2. <span data-ttu-id="7b10b-280">Inicie o Notepad.exe executando como administrador e abra o arquivo de texto "C:\Arquivos de Programas\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config." Você localizar a marca de padrão de saudação para system.net conforme Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b10b-280">Launch Notepad.exe running as administrator, and open text file “C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. You find hello default tag for system.net as shown in hello following code:</span></span>

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   <span data-ttu-id="7b10b-281">Em seguida, você pode adicionar detalhes do servidor proxy, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="7b10b-281">You can then add proxy server details as shown in hello following example:</span></span>

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   <span data-ttu-id="7b10b-282">Propriedades adicionais são permitidas em Olá proxy marca toospecify Olá necessárias configurações como scriptLocation.</span><span class="sxs-lookup"><span data-stu-id="7b10b-282">Additional properties are allowed inside hello proxy tag toospecify hello required settings like scriptLocation.</span></span> <span data-ttu-id="7b10b-283">Consulte também[proxy (configurações de rede) do elemento](https://msdn.microsoft.com/library/sa91de1e.aspx) na sintaxe.</span><span class="sxs-lookup"><span data-stu-id="7b10b-283">Refer too[proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on syntax.</span></span>

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. <span data-ttu-id="7b10b-284">Salve o arquivo de configuração de saudação no local original Olá, reiniciar Olá serviço de Host do Gateway de gerenciamento de dados, que seleciona Olá alterações.</span><span class="sxs-lookup"><span data-stu-id="7b10b-284">Save hello configuration file into hello original location, then restart hello Data Management Gateway Host service, which picks up hello changes.</span></span> <span data-ttu-id="7b10b-285">serviço de saudação toorestart: usar o miniaplicativo Serviços Olá no painel de controle ou de saudação **Gerenciador de configuração de Gateway de gerenciamento de dados** > clique Olá **parar serviço** e clique em Olá **Iniciar serviço**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-285">toorestart hello service: use services applet from hello control panel, or from hello **Data Management Gateway Configuration Manager** > click hello **Stop Service** button, then click hello **Start Service**.</span></span> <span data-ttu-id="7b10b-286">Se o serviço de saudação não iniciar, é provável que uma sintaxe de marca XML incorreta foi adicionada ao arquivo de configuração do aplicativo hello foi editado.</span><span class="sxs-lookup"><span data-stu-id="7b10b-286">If hello service does not start, it is likely that an incorrect XML tag syntax has been added into hello application configuration file that was edited.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b10b-287">Não se esqueça de tooupdate **ambos** diahost.exe.config e diawp.exe.config.</span><span class="sxs-lookup"><span data-stu-id="7b10b-287">Do not forget tooupdate **both** diahost.exe.config and diawp.exe.config.</span></span>  


<span data-ttu-id="7b10b-288">Além disso pontos toothese, você também precisa toomake se o que Microsoft Azure está na lista de permissões da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="7b10b-288">In addition toothese points, you also need toomake sure Microsoft Azure is in your company’s whitelist.</span></span> <span data-ttu-id="7b10b-289">lista de saudação de endereços IP do Microsoft Azure válidos pode ser baixada do hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="7b10b-289">hello list of valid Microsoft Azure IP addresses can be downloaded from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a><span data-ttu-id="7b10b-290">Possíveis sintomas de problemas relacionados ao firewall e ao servidor proxy</span><span class="sxs-lookup"><span data-stu-id="7b10b-290">Possible symptoms for firewall and proxy server-related issues</span></span>
<span data-ttu-id="7b10b-291">Se você encontrar erros toohello semelhante à seguir, é provável devido a configuração de tooimproper de saudação firewall ou servidor proxy, que bloqueia o gateway de conexão tooauthenticate tooData de fábrica em si.</span><span class="sxs-lookup"><span data-stu-id="7b10b-291">If you encounter errors similar toohello following ones, it is likely due tooimproper configuration of hello firewall or proxy server, which blocks gateway from connecting tooData Factory tooauthenticate itself.</span></span> <span data-ttu-id="7b10b-292">Consulte tooprevious seção tooensure seu servidor de firewall e proxy estão configurados corretamente.</span><span class="sxs-lookup"><span data-stu-id="7b10b-292">Refer tooprevious section tooensure your firewall and proxy server are properly configured.</span></span>

1. <span data-ttu-id="7b10b-293">Quando você tenta tooregister gateway de saudação, você receberá Olá erro a seguir: "chave do gateway falha tooregister hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-293">When you try tooregister hello gateway, you receive hello following error: "Failed tooregister hello gateway key.</span></span> <span data-ttu-id="7b10b-294">Antes de tentar novamente a chave do gateway tooregister hello, confirme se Olá gateway de gerenciamento de dados está em um estado conectado e hello serviço de Host do Gateway de gerenciamento de dados é iniciado."</span><span class="sxs-lookup"><span data-stu-id="7b10b-294">Before trying tooregister hello gateway key again, confirm that hello data management gateway is in a connected state and hello Data Management Gateway Host Service is Started."</span></span>
2. <span data-ttu-id="7b10b-295">Ao abrir o Gerenciador de Configurações, você vê o status "Desconectado" ou "Conectando".</span><span class="sxs-lookup"><span data-stu-id="7b10b-295">When you open Configuration Manager, you see status as “Disconnected” or “Connecting.”</span></span> <span data-ttu-id="7b10b-296">Ao exibir os logs de eventos do Windows, em "Visualizador de eventos" > "Logs de aplicativos e serviços" > "Gateway de gerenciamento de dados", ver mensagens de erro como Olá erro a seguir:`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span><span class="sxs-lookup"><span data-stu-id="7b10b-296">When viewing Windows event logs, under “Event Viewer” > “Application and Services Logs” > “Data Management Gateway”, you see error messages such as hello following error: `Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span></span>

### <a name="open-port-8050-for-credential-encryption"></a><span data-ttu-id="7b10b-297">Abrir a porta 8050 para criptografia de credencial</span><span class="sxs-lookup"><span data-stu-id="7b10b-297">Open port 8050 for credential encryption</span></span>
<span data-ttu-id="7b10b-298">Olá **definindo credenciais** aplicativo usa a porta de entrada de Olá **8050** toorelay gateway de toohello credenciais ao configurar um local vinculado de serviço no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b10b-298">hello **Setting Credentials** application uses hello inbound port **8050** toorelay credentials toohello gateway when you set up an on-premises linked service in hello Azure portal.</span></span> <span data-ttu-id="7b10b-299">Durante a instalação do gateway, por padrão, instalação do gateway Olá abre-o no computador do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-299">During gateway setup, by default, hello gateway installation opens it on hello gateway machine.</span></span>

<span data-ttu-id="7b10b-300">Se você estiver usando um firewall de terceiros, você pode abrir porta Olá 8050 manualmente.</span><span class="sxs-lookup"><span data-stu-id="7b10b-300">If you are using a third-party firewall, you can manually open hello port 8050.</span></span> <span data-ttu-id="7b10b-301">Se você tiver problema de firewall durante a instalação do gateway, você pode tentar usar Olá seguindo o gateway de saudação do comando tooinstall sem configurar o firewall hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-301">If you run into firewall issue during gateway setup, you can try using hello following command tooinstall hello gateway without configuring hello firewall.</span></span>

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

<span data-ttu-id="7b10b-302">Se você escolher não tooopen porta Olá 8050 no computador do gateway hello, usar mecanismos diferentes do uso Olá **definindo credenciais** dados tooconfigure de aplicativo armazenam credenciais.</span><span class="sxs-lookup"><span data-stu-id="7b10b-302">If you choose not tooopen hello port 8050 on hello gateway machine, use mechanisms other than using hello **Setting Credentials** application tooconfigure data store credentials.</span></span> <span data-ttu-id="7b10b-303">Por exemplo, você pode usar o cmdlet do PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) .</span><span class="sxs-lookup"><span data-stu-id="7b10b-303">For example, you could use [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="7b10b-304">Confira a seção [Definir Credenciais e Segurança](#set-credentials-and-securityy) para saber como as credenciais do armazenamento de dados podem ser definidas.</span><span class="sxs-lookup"><span data-stu-id="7b10b-304">See [Setting Credentials and Security](#set-credentials-and-securityy) section on how data store credentials can be set.</span></span>

## <a name="update"></a><span data-ttu-id="7b10b-305">Atualização</span><span class="sxs-lookup"><span data-stu-id="7b10b-305">Update</span></span>
<span data-ttu-id="7b10b-306">Por padrão, o gateway de gerenciamento de dados é atualizado automaticamente quando uma versão mais recente do gateway hello está disponível.</span><span class="sxs-lookup"><span data-stu-id="7b10b-306">By default, data management gateway is automatically updated when a newer version of hello gateway is available.</span></span> <span data-ttu-id="7b10b-307">gateway de saudação não é atualizado até que todas as tarefas agendada de saudação terminar.</span><span class="sxs-lookup"><span data-stu-id="7b10b-307">hello gateway is not updated until all hello scheduled tasks are done.</span></span> <span data-ttu-id="7b10b-308">Nenhuma tarefa adicional é processada pelo gateway Olá até a conclusão da operação de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b10b-308">No further tasks are processed by hello gateway until hello update operation is completed.</span></span> <span data-ttu-id="7b10b-309">Se Olá atualização falhar, gateway será revertido toohello uma versão antiga.</span><span class="sxs-lookup"><span data-stu-id="7b10b-309">If hello update fails, gateway is rolled back toohello old version.</span></span>

<span data-ttu-id="7b10b-310">Consulte o tempo de atualização de saudação agendada em Olá locais a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b10b-310">You see hello scheduled update time in hello following places:</span></span>

* <span data-ttu-id="7b10b-311">página de propriedades de gateway de saudação no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b10b-311">hello gateway properties page in hello Azure portal.</span></span>
* <span data-ttu-id="7b10b-312">Home page do Gerenciador de configuração de Gateway de gerenciamento de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="7b10b-312">Home page of hello Data Management Gateway Configuration Manager</span></span>
* <span data-ttu-id="7b10b-313">Na mensagem de notificação da bandeja do sistema.</span><span class="sxs-lookup"><span data-stu-id="7b10b-313">System tray notification message.</span></span>

<span data-ttu-id="7b10b-314">Guia de início de saudação do hello Gerenciador de configuração de Gateway de gerenciamento de dados exibe a agenda de atualização de saudação e gateway do hello última hora Olá foi instalado e atualizado.</span><span class="sxs-lookup"><span data-stu-id="7b10b-314">hello Home tab of hello Data Management Gateway Configuration Manager displays hello update schedule and hello last time hello gateway was installed/updated.</span></span>

![Agende atualizações](media/data-factory-data-management-gateway/UpdateSection.png)

<span data-ttu-id="7b10b-316">Você pode instalar atualização Olá imediatamente ou aguardar Olá gateway toobe atualizada automaticamente em tempo de saudação agendado.</span><span class="sxs-lookup"><span data-stu-id="7b10b-316">You can install hello update right away or wait for hello gateway toobe automatically updated at hello scheduled time.</span></span> <span data-ttu-id="7b10b-317">Por exemplo, hello imagem mostra Olá mostrada no hello Gateway Configuration Manager juntamente com o botão de atualização de saudação que você pode clicar em tooinstall-lo imediatamente de mensagem de notificação a seguir.</span><span class="sxs-lookup"><span data-stu-id="7b10b-317">For example, hello following image shows you hello notification message shown in hello Gateway Configuration Manager along with hello Update button that you can click tooinstall it immediately.</span></span>

![Atualizar no Gerenciador de Configurações DMG](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

<span data-ttu-id="7b10b-319">mensagem de notificação de saudação na bandeja do sistema Olá seria conforme Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b10b-319">hello notification message in hello system tray would look as shown in hello following image:</span></span>

![Mensagem da bandeja do sistema](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

<span data-ttu-id="7b10b-321">Você ver o status de saudação da operação de atualização (manual ou automática) na bandeja do sistema hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-321">You see hello status of update operation (manual or automatic) in hello system tray.</span></span> <span data-ttu-id="7b10b-322">Quando você inicia o Gerenciador de configuração de Gateway próxima vez, verá uma mensagem de saudação de barra de notificação gateway Olá foi atualizada juntamente com um link muito[o que há de novo tópico](data-factory-gateway-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="7b10b-322">When you launch Gateway Configuration Manager next time, you see a message on hello notification bar that hello gateway has been updated along with a link too[what's new topic](data-factory-gateway-release-notes.md).</span></span>

### <a name="toodisableenable-auto-update-feature"></a><span data-ttu-id="7b10b-323">toodisable/ativar o recurso de atualização automática</span><span class="sxs-lookup"><span data-stu-id="7b10b-323">toodisable/enable auto-update feature</span></span>
<span data-ttu-id="7b10b-324">Você pode desabilitar/habilitar o recurso de atualização automática de saudação fazendo Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b10b-324">You can disable/enable hello auto-update feature by doing hello following steps:</span></span>

<span data-ttu-id="7b10b-325">[Para o gateway de nó único]</span><span class="sxs-lookup"><span data-stu-id="7b10b-325">[For single node gateway]</span></span>
1. <span data-ttu-id="7b10b-326">Inicie o Windows PowerShell no computador do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-326">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="7b10b-327">Alternar toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript pasta.</span><span class="sxs-lookup"><span data-stu-id="7b10b-327">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="7b10b-328">Olá execução após o comando tooturn Olá a atualização automática de recursos desativado (desativar).</span><span class="sxs-lookup"><span data-stu-id="7b10b-328">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. <span data-ttu-id="7b10b-329">tooturn-a novamente:</span><span class="sxs-lookup"><span data-stu-id="7b10b-329">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
<span data-ttu-id="7b10b-330">[[Para vários nó altamente disponíveis e gateway dimensionável(versão prévia)](data-factory-data-management-gateway-high-availability-scalability.md)]</span><span class="sxs-lookup"><span data-stu-id="7b10b-330">[[For multi-node highly available and scalable gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]</span></span>
1. <span data-ttu-id="7b10b-331">Inicie o Windows PowerShell no computador do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-331">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="7b10b-332">Alternar toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript pasta.</span><span class="sxs-lookup"><span data-stu-id="7b10b-332">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="7b10b-333">Olá execução após o comando tooturn Olá a atualização automática de recursos desativado (desativar).</span><span class="sxs-lookup"><span data-stu-id="7b10b-333">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    <span data-ttu-id="7b10b-334">Para o gateway com o recurso de alta disponibilidade (versão prévia), um parâmetro AuthKey adicional é necessário.</span><span class="sxs-lookup"><span data-stu-id="7b10b-334">For gateway with high availability feature (preview), an extra AuthKey param is required.</span></span>
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. <span data-ttu-id="7b10b-335">tooturn-a novamente:</span><span class="sxs-lookup"><span data-stu-id="7b10b-335">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

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
<span data-ttu-id="7b10b-336">Se você acessar o portal de saudação de um computador diferente do computador do gateway hello, você deve garantir que aplicativo do Gerenciador de credenciais hello pode se conectar a máquina de gateway toohello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-336">If you access hello portal from a machine that is different from hello gateway machine, you must make sure that hello Credentials Manager application can connect toohello gateway machine.</span></span> <span data-ttu-id="7b10b-337">Se o aplicativo hello não conseguem acessar o computador do gateway hello, ele não permite tooset credenciais para a fonte de dados de saudação e fonte de dados de toohello tootest conexão.</span><span class="sxs-lookup"><span data-stu-id="7b10b-337">If hello application cannot reach hello gateway machine, it does not allow you tooset credentials for hello data source and tootest connection toohello data source.</span></span>  

<span data-ttu-id="7b10b-338">Quando você usa Olá **definindo credenciais** aplicativo, o portal Olá criptografa credenciais Olá com hello certificado especificado no hello **certificado** guia da saudação **Gateway Gerenciador de configuração** no computador do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-338">When you use hello **Setting Credentials** application, hello portal encrypts hello credentials with hello certificate specified in hello **Certificate** tab of hello **Gateway Configuration Manager** on hello gateway machine.</span></span>

<span data-ttu-id="7b10b-339">Se você estiver procurando uma abordagem baseada em API para criptografar credenciais hello, você pode usar o hello [AzureRmDataFactoryEncryptValue novo](https://msdn.microsoft.com/library/mt603802.aspx) credenciais de tooencrypt de cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b10b-339">If you are looking for an API-based approach for encrypting hello credentials, you can use hello [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt credentials.</span></span> <span data-ttu-id="7b10b-340">Olá cmdlet usa o certificado de saudação que gateway é configurado toouse tooencrypt Olá credenciais.</span><span class="sxs-lookup"><span data-stu-id="7b10b-340">hello cmdlet uses hello certificate that gateway is configured toouse tooencrypt hello credentials.</span></span> <span data-ttu-id="7b10b-341">Adicionar credenciais criptografadas toohello **EncryptedCredential** elemento de saudação **connectionString** em Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="7b10b-341">You add encrypted credentials toohello **EncryptedCredential** element of hello **connectionString** in hello JSON.</span></span> <span data-ttu-id="7b10b-342">Use Olá JSON com hello [AzureRmDataFactoryLinkedService novo](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet ou em Olá Editor da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="7b10b-342">You use hello JSON with hello [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet or in hello Data Factory Editor.</span></span>

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

<span data-ttu-id="7b10b-343">Há mais uma abordagem para definir as credenciais usando o Editor Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7b10b-343">There is one more approach for setting credentials using Data Factory Editor.</span></span> <span data-ttu-id="7b10b-344">Se você criar um SQL Server vinculado serviço usando o editor de saudação e insira as credenciais em texto sem formatação, credenciais de saudação são criptografadas usando um certificado de serviço da fábrica de dados Olá possui.</span><span class="sxs-lookup"><span data-stu-id="7b10b-344">If you create a SQL Server linked service by using hello editor and you enter credentials in plain text, hello credentials are encrypted using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="7b10b-345">Não usa certificados Olá que gateway é configurado toouse.</span><span class="sxs-lookup"><span data-stu-id="7b10b-345">It does NOT use hello certificate that gateway is configured toouse.</span></span> <span data-ttu-id="7b10b-346">Embora essa abordagem possa ser um pouco mais rápida em alguns casos, ela é menos segura.</span><span class="sxs-lookup"><span data-stu-id="7b10b-346">While this approach might be a little faster in some cases, it is less secure.</span></span> <span data-ttu-id="7b10b-347">Portanto, é recomendável que você siga essa abordagem somente para fins de desenvolvimento/teste.</span><span class="sxs-lookup"><span data-stu-id="7b10b-347">Therefore, we recommend that you follow this approach only for development/testing purposes.</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="7b10b-348">Cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b10b-348">PowerShell cmdlets</span></span>
<span data-ttu-id="7b10b-349">Esta seção descreve como toocreate e registrar um gateway usando cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b10b-349">This section describes how toocreate and register a gateway using Azure PowerShell cmdlets.</span></span>

1. <span data-ttu-id="7b10b-350">Inicie o **PowerShell do Azure** no modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="7b10b-350">Launch **Azure PowerShell** in administrator mode.</span></span>
2. <span data-ttu-id="7b10b-351">Faça logon no tooyour conta do Azure executando Olá comando a seguir e inserir suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b10b-351">Log in tooyour Azure account by running hello following command and entering your Azure credentials.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="7b10b-352">Saudação de uso **AzureRmDataFactoryGateway novo** cmdlet toocreate um gateway lógico da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="7b10b-352">Use hello **New-AzureRmDataFactoryGateway** cmdlet toocreate a logical gateway as follows:</span></span>

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    <span data-ttu-id="7b10b-353">**Exemplo de comando e saída**:</span><span class="sxs-lookup"><span data-stu-id="7b10b-353">**Example command and output**:</span></span>

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

1. <span data-ttu-id="7b10b-354">No PowerShell do Azure, alternar pasta toohello: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span><span class="sxs-lookup"><span data-stu-id="7b10b-354">In Azure PowerShell, switch toohello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span></span> <span data-ttu-id="7b10b-355">Executar **RegisterGateway.ps1** associado à variável local Olá **$Key** conforme mostrado no comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b10b-355">Run **RegisterGateway.ps1** associated with hello local variable **$Key** as shown in hello following command.</span></span> <span data-ttu-id="7b10b-356">Esse script registra o agente de cliente Olá instalado em seu computador com o gateway de lógica Olá que criar anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7b10b-356">This script registers hello client agent installed on your machine with hello logical gateway you create earlier.</span></span>

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    <span data-ttu-id="7b10b-357">Você pode registrar o gateway de saudação em um computador remoto usando o parâmetro de IsRegisterOnRemoteMachine hello.</span><span class="sxs-lookup"><span data-stu-id="7b10b-357">You can register hello gateway on a remote machine by using hello IsRegisterOnRemoteMachine parameter.</span></span> <span data-ttu-id="7b10b-358">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="7b10b-358">Example:</span></span>

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. <span data-ttu-id="7b10b-359">Você pode usar o hello **Get-AzureRmDataFactoryGateway** lista de saudação tooget cmdlet gateways na fábrica dados.</span><span class="sxs-lookup"><span data-stu-id="7b10b-359">You can use hello **Get-AzureRmDataFactoryGateway** cmdlet tooget hello list of Gateways in your data factory.</span></span> <span data-ttu-id="7b10b-360">Olá quando **Status** mostra **online**, isso significa que o gateway é toouse pronto.</span><span class="sxs-lookup"><span data-stu-id="7b10b-360">When hello **Status** shows **online**, it means your gateway is ready toouse.</span></span>

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
<span data-ttu-id="7b10b-361">Você pode remover um gateway usando Olá **remover AzureRmDataFactoryGateway** descrição de cmdlet e a atualização para um gateway usando Olá **AzureRmDataFactoryGateway conjunto** cmdlets.</span><span class="sxs-lookup"><span data-stu-id="7b10b-361">You can remove a gateway using hello **Remove-AzureRmDataFactoryGateway** cmdlet and update description for a gateway using hello **Set-AzureRmDataFactoryGateway** cmdlets.</span></span> <span data-ttu-id="7b10b-362">Para sintaxe e outros detalhes sobre esses cmdlets, consulte Referência de Cmdlet de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7b10b-362">For syntax and other details about these cmdlets, see Data Factory Cmdlet Reference.</span></span>  

### <a name="list-gateways-using-powershell"></a><span data-ttu-id="7b10b-363">Listar gateways usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b10b-363">List gateways using PowerShell</span></span>

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a><span data-ttu-id="7b10b-364">Remover gateways usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b10b-364">Remove gateway using PowerShell</span></span>

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a><span data-ttu-id="7b10b-365">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7b10b-365">Next steps</span></span>
* <span data-ttu-id="7b10b-366">Consulte o artigo [Mover os dados entre os armazenamentos de dados local e de nuvem](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="7b10b-366">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="7b10b-367">Olá instruções passo a passo, você criará um pipeline que usa Olá gateway toomove dados de um tooan de banco de dados do SQL Server local BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b10b-367">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span>  
