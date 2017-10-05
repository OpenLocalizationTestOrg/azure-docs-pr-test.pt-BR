---
title: "Implantar o serviço de Mobilidade do Site Recovery com o DSC de Automação do Azure | Microsoft Docs"
description: "Descreve como usar o DSC de Automação do Azure para implantar automaticamente o Serviço de Mobilidade do Azure Site Recovery e o agente do Azure para VM do VMware e replicação do servidor físico no Azure"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: bcc5f11afbecac8fe63935f3401dd3e2d767e8aa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-the-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="87f48-103">Implantar o serviço de Mobilidade com o DSC de Automação do Azure para replicação da VM</span><span class="sxs-lookup"><span data-stu-id="87f48-103">Deploy the Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="87f48-104">No Operations Management Suite, oferecemos uma solução abrangente de backup e recuperação de desastre que pode ser usada como parte de seu plano de continuidade de negócios.</span><span class="sxs-lookup"><span data-stu-id="87f48-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="87f48-105">Começamos esta jornada com o Hyper-V, usando a Réplica do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="87f48-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="87f48-106">Mas expandimos para dar suporte a uma configuração heterogênea porque os clientes têm vários hipervisores e plataformas em suas nuvens.</span><span class="sxs-lookup"><span data-stu-id="87f48-106">But we have expanded to support a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="87f48-107">Se você estiver executando servidores físicos e/ou cargas de trabalho da VMware, um servidor de gerenciamento executará todos os componentes do Azure Site Recovery no seu ambiente para lidar com a replicação dos dados e a comunicação com o Azure quando ele for seu destino.</span><span class="sxs-lookup"><span data-stu-id="87f48-107">If you are running VMware workloads and/or physical servers today, a management server runs all of the Azure Site Recovery components in your environment to handle the communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-the-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="87f48-108">Implantar o Serviço de Mobilidade do Site Recovery usando o DSC de Automação</span><span class="sxs-lookup"><span data-stu-id="87f48-108">Deploy the Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="87f48-109">Vamos começar fazendo uma análise rápida do que este servidor de gerenciamento faz.</span><span class="sxs-lookup"><span data-stu-id="87f48-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="87f48-110">o servidor de gerenciamento executa várias funções de servidor.</span><span class="sxs-lookup"><span data-stu-id="87f48-110">The management server runs several server roles.</span></span> <span data-ttu-id="87f48-111">Uma dessas funções é a de *configuração*, que coordena a comunicação e gerencia os processos de replicação e recuperação de dados.</span><span class="sxs-lookup"><span data-stu-id="87f48-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="87f48-112">Além disso, a função de *processo* atua como um gateway de replicação.</span><span class="sxs-lookup"><span data-stu-id="87f48-112">In addition, the *process* role acts as a replication gateway.</span></span> <span data-ttu-id="87f48-113">Essa função recebe dados de replicação de computadores de origem protegida, otimiza-os com caching, compactação e criptografia e os envia para uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="87f48-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it to an Azure storage account.</span></span> <span data-ttu-id="87f48-114">Uma das funções da função do processo também é a instalação do Serviço de Mobilidade por push nas máquinas protegidas e a execução da descoberta automática das VMs da VMware.</span><span class="sxs-lookup"><span data-stu-id="87f48-114">One of the functions for the process role is also to push installation of the Mobility service to protected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="87f48-115">No caso de um failback do Azure, a função de *destino mestre* lidará com os dados de replicação como parte dessa operação.</span><span class="sxs-lookup"><span data-stu-id="87f48-115">If there's a failback from Azure, the *master target* role will handle the replication data as part of this operation.</span></span>

<span data-ttu-id="87f48-116">Para os computadores protegidos, podemos contar com a *Serviço de Mobilidade*.</span><span class="sxs-lookup"><span data-stu-id="87f48-116">For the protected machines, we rely on the *Mobility service*.</span></span> <span data-ttu-id="87f48-117">Esse componente é implantado em cada computador (servidor físico ou VM da VMware) que você quiser replicar para o Azure.</span><span class="sxs-lookup"><span data-stu-id="87f48-117">This component is deployed to every machine (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="87f48-118">Ele captura dados gravados no computador e os encaminha para o servidor de gerenciamento (função de processo).</span><span class="sxs-lookup"><span data-stu-id="87f48-118">It captures data writes on the machine and forwards them to the management server (process role).</span></span>

<span data-ttu-id="87f48-119">Quando se trata de continuidade de negócios, é importante compreender suas cargas de trabalho, sua infraestrutura e os componentes envolvidos.</span><span class="sxs-lookup"><span data-stu-id="87f48-119">When you're dealing with business continuity, it's important to understand your workloads, your infrastructure, and the components involved.</span></span> <span data-ttu-id="87f48-120">Assim, é possível atender os requisitos de RTO (objetivo do tempo de recuperação) e RPO (objetivo de ponto de recuperação).</span><span class="sxs-lookup"><span data-stu-id="87f48-120">You can then meet the requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="87f48-121">Nesse contexto, o Serviço de Mobilidade é fundamental para garantir que suas cargas de trabalho sejam protegidas da forma esperada.</span><span class="sxs-lookup"><span data-stu-id="87f48-121">In this context, the Mobility service is key to ensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="87f48-122">Sendo assim, como você pode assegurar, de forma otimizada, que tem uma configuração protegida confiável com a ajuda de alguns componentes do Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="87f48-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="87f48-123">Este artigo fornece um exemplo de como você pode usar a DSC (Configuração de Estado Desejado) da Automação do Azure em conjunto com o Site Recovery para garantir que:</span><span class="sxs-lookup"><span data-stu-id="87f48-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, to ensure that:</span></span>

* <span data-ttu-id="87f48-124">o Serviço de Mobilidade e o agente de VM do Azure sejam implantados nos computadores com Windows que você deseja proteger.</span><span class="sxs-lookup"><span data-stu-id="87f48-124">The Mobility service and Azure VM agent are deployed to the Windows machines that you want to protect.</span></span>
* <span data-ttu-id="87f48-125">o Serviço de Mobilidade e o agente de VM do Azure sempre estejam em execução quando o Azure for o destino de replicação.</span><span class="sxs-lookup"><span data-stu-id="87f48-125">The Mobility service and Azure VM agent are always running when Azure is the replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87f48-126">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="87f48-126">Prerequisites</span></span>
* <span data-ttu-id="87f48-127">Um repositório para armazenar a configuração necessária</span><span class="sxs-lookup"><span data-stu-id="87f48-127">A repository to store the required setup</span></span>
* <span data-ttu-id="87f48-128">Um repositório para armazenar a senha necessária para se registrar no servidor de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="87f48-128">A repository to store the required passphrase to register with the management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="87f48-129">Uma senha exclusiva é gerada para cada servidor de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="87f48-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="87f48-130">Se for implantar vários servidores de gerenciamento, você precisará garantir que a senha correta seja armazenada no arquivo passphrase.txt.</span><span class="sxs-lookup"><span data-stu-id="87f48-130">If you are going to deploy multiple management servers, you have to ensure that the correct passphrase is stored in the passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="87f48-131">O WMF (Windows Management Framework) 5.0 instalado nos computadores que você deseja habilitar para proteção (requisito para o DSC de Automação)</span><span class="sxs-lookup"><span data-stu-id="87f48-131">Windows Management Framework (WMF) 5.0 installed on the machines that you want to enable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="87f48-132">Se você quiser usar o DSC para computadores com Windows que tenham o WMF 4.0 instalado, consulte a seção [Usar o DSC em ambientes desconectados](## Use DSC in disconnected environments).</span><span class="sxs-lookup"><span data-stu-id="87f48-132">If you want to use DSC for Windows machines that have WMF 4.0 installed, see the section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="87f48-133">O Serviço de Mobilidade pode ser instalado por meio da linha de comando e aceita vários argumentos.</span><span class="sxs-lookup"><span data-stu-id="87f48-133">The Mobility service can be installed through the command line and accepts several arguments.</span></span> <span data-ttu-id="87f48-134">É por isso que você precisa ter os binários (após extraí-los de sua configuração) e armazená-los em algum lugar em que possa recuperá-los usando uma configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="87f48-134">That’s why you need to have the binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="87f48-135">Etapa 1: Extrair os binários</span><span class="sxs-lookup"><span data-stu-id="87f48-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="87f48-136">Para extrair os arquivos necessários para esta instalação, navegue até o seguinte diretório no servidor de gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="87f48-136">To extract the files that you need for this setup, browse to the following directory on your management server:</span></span>

    <span data-ttu-id="87f48-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="87f48-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="87f48-138">Nessa pasta, você verá um arquivo MSI chamado:</span><span class="sxs-lookup"><span data-stu-id="87f48-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="87f48-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="87f48-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="87f48-140">Use o seguinte comando para extrair o instalador:</span><span class="sxs-lookup"><span data-stu-id="87f48-140">Use the following command to extract the installer:</span></span>

    <span data-ttu-id="87f48-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="87f48-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="87f48-142">Selecione todos os arquivos e envie-os para uma pasta compactada (zipada).</span><span class="sxs-lookup"><span data-stu-id="87f48-142">Select all files and send them to a compressed (zipped) folder.</span></span>

<span data-ttu-id="87f48-143">Agora, você tem os binários necessários para automatizar a instalação do Serviço de Mobilidade usando o DSC de Automação.</span><span class="sxs-lookup"><span data-stu-id="87f48-143">You now have the binaries that you need to automate the setup of the Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="87f48-144">Senha</span><span class="sxs-lookup"><span data-stu-id="87f48-144">Passphrase</span></span>
<span data-ttu-id="87f48-145">Em seguida, você precisa determinar onde deseja colocar essa pasta compactada.</span><span class="sxs-lookup"><span data-stu-id="87f48-145">Next, you need to determine where you want to place this zipped folder.</span></span> <span data-ttu-id="87f48-146">Você pode usar uma conta de armazenamento do Azure, como mostrado posteriormente, para armazenar a senha de que precisa para a instalação.</span><span class="sxs-lookup"><span data-stu-id="87f48-146">You can use an Azure storage account, as shown later, to store the passphrase that you need for the setup.</span></span> <span data-ttu-id="87f48-147">O agente será registrado no servidor de gerenciamento como parte do processo.</span><span class="sxs-lookup"><span data-stu-id="87f48-147">The agent will then register with the management server as part of the process.</span></span>

<span data-ttu-id="87f48-148">A senha que você recebeu quando implantou o servidor de gerenciamento pode ser salva em um arquivo de texto, como passphrase.txt.</span><span class="sxs-lookup"><span data-stu-id="87f48-148">The passphrase that you got when you deployed the management server can be saved to a text file as passphrase.txt.</span></span>

<span data-ttu-id="87f48-149">Coloque a pasta compactada e a senha em um contêiner dedicado na conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="87f48-149">Place both the zipped folder and the passphrase in a dedicated container in the Azure storage account.</span></span>

![Localização da pasta](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="87f48-151">Se preferir manter esses arquivos em um compartilhamento na rede, você poderá fazer isso.</span><span class="sxs-lookup"><span data-stu-id="87f48-151">If you prefer to keep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="87f48-152">Você só precisa garantir que o recurso de DSC que será usado posteriormente realmente tenha acesso e possa obter a instalação e a senha.</span><span class="sxs-lookup"><span data-stu-id="87f48-152">You just need to ensure that the DSC resource that you will be using later has access and can get the setup and passphrase.</span></span>

## <a name="step-2-create-the-dsc-configuration"></a><span data-ttu-id="87f48-153">Etapa 2: Criar a configuração de DSC</span><span class="sxs-lookup"><span data-stu-id="87f48-153">Step 2: Create the DSC configuration</span></span>
<span data-ttu-id="87f48-154">A instalação depende do WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="87f48-154">The setup depends on WMF 5.0.</span></span> <span data-ttu-id="87f48-155">Para o computador aplicar com êxito a configuração por meio do DSC de Automação, o WMF 5.0 deve estar presente.</span><span class="sxs-lookup"><span data-stu-id="87f48-155">For the machine to successfully apply the configuration through Automation DSC, WMF 5.0 needs to be present.</span></span>

<span data-ttu-id="87f48-156">O ambiente usa o seguinte exemplo de configuração de DSC:</span><span class="sxs-lookup"><span data-stu-id="87f48-156">The environment uses the following example DSC configuration:</span></span>

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
<span data-ttu-id="87f48-157">A configuração fará o seguinte:</span><span class="sxs-lookup"><span data-stu-id="87f48-157">The configuration will do the following:</span></span>

* <span data-ttu-id="87f48-158">As variáveis informarão a configuração sobre onde obter os binários para o Serviço de Mobilidade e o agente de VM do Azure, onde obter a senha e onde armazenar a saída.</span><span class="sxs-lookup"><span data-stu-id="87f48-158">The variables will tell the configuration where to get the binaries for the Mobility service and the Azure VM agent, where to get the passphrase, and where to store the output.</span></span>
* <span data-ttu-id="87f48-159">A configuração importará o recurso de DSC xPSDesiredStateConfiguration para que você possa usar `xRemoteFile` para baixar os arquivos do repositório.</span><span class="sxs-lookup"><span data-stu-id="87f48-159">The configuration will import the xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` to download the files from the repository.</span></span>
* <span data-ttu-id="87f48-160">A configuração criará um diretório no qual você deseja armazenar os binários.</span><span class="sxs-lookup"><span data-stu-id="87f48-160">The configuration will create a directory where you want to store the binaries.</span></span>
* <span data-ttu-id="87f48-161">O recurso de arquivamento extrairá os arquivos da pasta compactada.</span><span class="sxs-lookup"><span data-stu-id="87f48-161">The archive resource will extract the files from the zipped folder.</span></span>
* <span data-ttu-id="87f48-162">O pacote de instalação do recurso instalará o Serviço de Mobilidade do instalador UNIFIEDAGENT.EXE com os argumentos específicos.</span><span class="sxs-lookup"><span data-stu-id="87f48-162">The package Install resource will install the Mobility service from the UNIFIEDAGENT.EXE installer with the specific arguments.</span></span> <span data-ttu-id="87f48-163">(As variáveis que criam os argumentos precisam ser alteradas para refletir seu ambiente).</span><span class="sxs-lookup"><span data-stu-id="87f48-163">(The variables that construct the arguments need to be changed to reflect your environment.)</span></span>
* <span data-ttu-id="87f48-164">O recurso de pacote AzureAgent instalará o agente de VM do Azure, que é recomendado em cada VM executada no Azure.</span><span class="sxs-lookup"><span data-stu-id="87f48-164">The package AzureAgent resource will install the Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="87f48-165">O agente de VM do Azure também torna possível adicionar extensões à VM após o failover.</span><span class="sxs-lookup"><span data-stu-id="87f48-165">The Azure VM agent also makes it possible to add extensions to the VM after failover.</span></span>
* <span data-ttu-id="87f48-166">Os recursos de serviço garantirão que os serviços de Mobilidade relacionados e os serviços do Azure estejam sempre em execução.</span><span class="sxs-lookup"><span data-stu-id="87f48-166">The service resource or resources will ensure that the related Mobility services and the Azure services are always running.</span></span>

<span data-ttu-id="87f48-167">Salve a configuração como **ASRMobilityService**.</span><span class="sxs-lookup"><span data-stu-id="87f48-167">Save the configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="87f48-168">Lembre-se de substituir o CSIP em sua configuração para refletir o servidor de gerenciamento real, para que o agente seja conectado corretamente e use a senha correta.</span><span class="sxs-lookup"><span data-stu-id="87f48-168">Remember to replace the CSIP in your configuration to reflect the actual management server, so that the agent will be connected correctly and will use the correct passphrase.</span></span>
>
>

## <a name="step-3-upload-to-automation-dsc"></a><span data-ttu-id="87f48-169">Etapa 3: Carregar o DSC de Automação</span><span class="sxs-lookup"><span data-stu-id="87f48-169">Step 3: Upload to Automation DSC</span></span>
<span data-ttu-id="87f48-170">Como a configuração DSC que você fez importará um módulo de recursos DSC necessário (xPSDesiredStateConfiguration), você precisa importar esse módulo na Automação antes de carregar a configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="87f48-170">Because the DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need to import that module in Automation before you upload the DSC configuration.</span></span>

<span data-ttu-id="87f48-171">Entre na sua conta de Automação, navegue até **Ativos** >  > **Módulos** e clique em **Procurar na Galeria**.</span><span class="sxs-lookup"><span data-stu-id="87f48-171">Sign in to your Automation account, browse to **Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="87f48-172">Aqui, você pode procurar o módulo e importá-lo para sua conta.</span><span class="sxs-lookup"><span data-stu-id="87f48-172">Here you can search for the module and import it to your account.</span></span>

![Importar módulo](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="87f48-174">Feito isso, vá até o computador no qual os módulos do Azure Resource Manager estão instalados e prossiga para importar a configuração de DSC recém-criada.</span><span class="sxs-lookup"><span data-stu-id="87f48-174">When you finish this, go to your machine where you have the Azure Resource Manager modules installed and proceed to import the newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="87f48-175">Importar cmdlets</span><span class="sxs-lookup"><span data-stu-id="87f48-175">Import cmdlets</span></span>
<span data-ttu-id="87f48-176">No PowerShell, entre em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="87f48-176">In PowerShell, sign in to your Azure subscription.</span></span> <span data-ttu-id="87f48-177">Modifique os cmdlets para refletir seu ambiente e capturar suas informações da conta de Automação em uma variável:</span><span class="sxs-lookup"><span data-stu-id="87f48-177">Modify the cmdlets to reflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="87f48-178">Carregue a configuração no DSC de Automação usando o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="87f48-178">Upload the configuration to Automation DSC by using the following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-the-configuration-in-automation-dsc"></a><span data-ttu-id="87f48-179">Compilar a configuração no DSC de Automação</span><span class="sxs-lookup"><span data-stu-id="87f48-179">Compile the configuration in Automation DSC</span></span>
<span data-ttu-id="87f48-180">Em seguida, é necessário compilar a configuração no DSC de Automação para poder começar a registrar os nós.</span><span class="sxs-lookup"><span data-stu-id="87f48-180">Next, you need to compile the configuration in Automation DSC, so that you can start to register nodes to it.</span></span> <span data-ttu-id="87f48-181">Podemos fazer isso executando o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="87f48-181">You achieve that by running the following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="87f48-182">Isso pode levar alguns minutos, pois você está basicamente implantando a configuração no serviço hospedado de pull do DSC.</span><span class="sxs-lookup"><span data-stu-id="87f48-182">This can take a few minutes, because you're basically deploying the configuration to the hosted DSC pull service.</span></span>

<span data-ttu-id="87f48-183">Após compilar a configuração, você pode recuperar as informações do trabalho usando o PowerShell (Get-AzureRmAutomationDscCompilationJob) ou usando o [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="87f48-183">After you compile the configuration, you can retrieve the job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using the [Azure portal](https://portal.azure.com/).</span></span>

![Recuperar trabalho](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="87f48-185">Agora, você publicou e carregou com êxito sua configuração de DSC no DSC de Automação.</span><span class="sxs-lookup"><span data-stu-id="87f48-185">You have now successfully published and uploaded your DSC configuration to Automation DSC.</span></span>

## <a name="step-4-onboard-machines-to-automation-dsc"></a><span data-ttu-id="87f48-186">Etapa 4: Integrar os computadores no DSC de Automação</span><span class="sxs-lookup"><span data-stu-id="87f48-186">Step 4: Onboard machines to Automation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="87f48-187">Um dos pré-requisitos para concluir esse cenário é que seus computadores com Windows estejam atualizados com a última versão do WMF.</span><span class="sxs-lookup"><span data-stu-id="87f48-187">One of the prerequisites for completing this scenario is that your Windows machines are updated with the latest version of WMF.</span></span> <span data-ttu-id="87f48-188">Você pode baixar e instalar a versão correta para sua plataforma no [Centro de Download](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="87f48-188">You can download and install the correct version for your platform from the [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="87f48-189">Agora, você criará uma metaconfiguração para o DSC que será aplicado em seus nós.</span><span class="sxs-lookup"><span data-stu-id="87f48-189">You will now create a metaconfig for DSC that you will apply to your nodes.</span></span> <span data-ttu-id="87f48-190">Para ter êxito com isso, você precisa recuperar a URL do ponto de extremidade e a chave primária de sua conta de Automação selecionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="87f48-190">To succeed with this, you need to retrieve the endpoint URL and the primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="87f48-191">Esses valores podem ser localizados em **Chaves** na folha **Todas as configurações** da conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="87f48-191">You can find these values under **Keys** on the **All settings** blade for the Automation account.</span></span>

![Valores da chave](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="87f48-193">Nesse exemplo, você tem um servidor físico do Windows Server 2012 R2 que quer proteger usando o Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="87f48-193">In this example, you have a Windows Server 2012 R2 physical server that you want to protect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-the-registry"></a><span data-ttu-id="87f48-194">Verificar quaisquer operações de renomeação de arquivo pendentes no registro</span><span class="sxs-lookup"><span data-stu-id="87f48-194">Check for any pending file rename operations in the registry</span></span>
<span data-ttu-id="87f48-195">Antes de começar a associar o servidor ao ponto de extremidade do DSC de Automação, é recomendável verificar quaisquer operações de renomeação pendentes no Registro.</span><span class="sxs-lookup"><span data-stu-id="87f48-195">Before you start to associate the server with the Automation DSC endpoint, we recommend that you check for any pending file rename operations in the registry.</span></span> <span data-ttu-id="87f48-196">Elas podem impedir que a instalação seja concluída devido a uma reinicialização pendente.</span><span class="sxs-lookup"><span data-stu-id="87f48-196">They might prohibit the setup from finishing due to a pending reboot.</span></span>

<span data-ttu-id="87f48-197">Execute o seguinte cmdlet para verificar se não há nenhuma reinicialização pendente no servidor:</span><span class="sxs-lookup"><span data-stu-id="87f48-197">Run the following cmdlet to verify that there’s no pending reboot on the server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="87f48-198">Se isso não mostrar nada, será OK continuar.</span><span class="sxs-lookup"><span data-stu-id="87f48-198">If this shows empty, you are OK to proceed.</span></span> <span data-ttu-id="87f48-199">Caso contrário, deverá lidar com isso reinicializando o servidor durante uma janela de manutenção.</span><span class="sxs-lookup"><span data-stu-id="87f48-199">If not, you should address this by rebooting the server during a maintenance window.</span></span>

<span data-ttu-id="87f48-200">Para aplicar a configuração no servidor, inicie o ISE (Ambiente de Script Integrado) do PowerShell e execute o script a seguir.</span><span class="sxs-lookup"><span data-stu-id="87f48-200">To apply the configuration on the server, start the PowerShell Integrated Scripting Environment (ISE) and run the following script.</span></span> <span data-ttu-id="87f48-201">Isso é basicamente uma configuração local do DSC que instruirá o mecanismo do Gerenciador de Configurações Local a se registrar no serviço de DSC de Automação e recuperar a configuração específica (ASRMobilityService.localhost).</span><span class="sxs-lookup"><span data-stu-id="87f48-201">This is essentially a DSC local configuration that will instruct the Local Configuration Manager engine to register with the Automation DSC service and retrieve the specific configuration (ASRMobilityService.localhost).</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

<span data-ttu-id="87f48-202">Essa configuração fará com que o mecanismo do Gerenciador de Configurações Local se registre no DSC de Automação.</span><span class="sxs-lookup"><span data-stu-id="87f48-202">This configuration will cause the Local Configuration Manager engine to register itself with Automation DSC.</span></span> <span data-ttu-id="87f48-203">Ela também determinará como o mecanismo deve operar, o que ele deverá fazer se houver falta de sincronia na configuração (ApplyAndAutoCorrect) e como deverá prosseguir com a configuração se uma reinicialização for necessária.</span><span class="sxs-lookup"><span data-stu-id="87f48-203">It will also determine how the engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with the configuration if a reboot is required.</span></span>

<span data-ttu-id="87f48-204">Após você executar o script, o nó deve começar a se registrar no DSC de Automação.</span><span class="sxs-lookup"><span data-stu-id="87f48-204">After you run this script, the node should start to register with Automation DSC.</span></span>

![Registro de nó em andamento](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="87f48-206">Se voltar para o portal do Azure, você poderá ver que o nó recém-registrado agora apareceu no portal.</span><span class="sxs-lookup"><span data-stu-id="87f48-206">If you go back to the Azure portal, you can see that the newly registered node has now appeared in the portal.</span></span>

![Nó registrado no portal](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="87f48-208">No servidor, é possível executar o seguinte cmdlet do PowerShell para verificar se o nó foi registrado corretamente:</span><span class="sxs-lookup"><span data-stu-id="87f48-208">On the server, you can run the following PowerShell cmdlet to verify that the node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="87f48-209">Depois da configuração ter sido extraída e aplicada no servidor, você pode verificar isso executando o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="87f48-209">After the configuration has been pulled and applied to the server, you can verify this by running the following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="87f48-210">A saída mostra que o servidor extraiu com êxito sua configuração:</span><span class="sxs-lookup"><span data-stu-id="87f48-210">The output shows that the server has successfully pulled its configuration:</span></span>

![Saída](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="87f48-212">Além disso, a instalação do Serviço de Mobilidade tem seu próprio log, que pode ser encontrado em *SystemDrive*\ProgramData\ASRSetupLogs.</span><span class="sxs-lookup"><span data-stu-id="87f48-212">In addition, the Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="87f48-213">É isso.</span><span class="sxs-lookup"><span data-stu-id="87f48-213">That’s it.</span></span> <span data-ttu-id="87f48-214">Você implantou e registrou com êxito o Serviço de Mobilidade no computador que deseja proteger usando o Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="87f48-214">You have now successfully deployed and registered the Mobility service on the machine that you want to protect by using Site Recovery.</span></span> <span data-ttu-id="87f48-215">O DSC garantirá que os serviços necessários estejam sempre em execução.</span><span class="sxs-lookup"><span data-stu-id="87f48-215">DSC will make sure that the required services are always running.</span></span>

![Implantação bem-sucedida](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="87f48-217">Após o servidor de gerenciamento detectar a implantação bem-sucedida, você poderá configurar a proteção e habilitar a replicação no computador usando o Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="87f48-217">After the management server detects the successful deployment, you can configure protection and enable replication on the machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="87f48-218">Usar o DSC em ambientes desconectados</span><span class="sxs-lookup"><span data-stu-id="87f48-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="87f48-219">Se seus computadores não estiverem conectados à Internet, você ainda poderá contar com o DSC para implantar e configurar o Serviço de Mobilidade nas cargas de trabalho que gostaria de proteger.</span><span class="sxs-lookup"><span data-stu-id="87f48-219">If your machines aren’t connected to the Internet, you can still rely on DSC to deploy and configure the Mobility service on the workloads that you want to protect.</span></span>

<span data-ttu-id="87f48-220">Você pode instanciar seu próprio servidor de recepção do DSC em seu ambiente para, essencialmente, fornecer os mesmos recursos que obtém com o DSC de Automação.</span><span class="sxs-lookup"><span data-stu-id="87f48-220">You can instantiate your own DSC pull server in your environment to essentially provide the same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="87f48-221">Ou seja, os clientes efetuarão pull da configuração (após o registro) para o ponto de extremidade do DSC.</span><span class="sxs-lookup"><span data-stu-id="87f48-221">That is, the clients will pull the configuration (after it's registered) to the DSC endpoint.</span></span> <span data-ttu-id="87f48-222">No entanto, outra opção é enviar por push manualmente a configuração de DSC por push a seus computadores, local ou remotamente.</span><span class="sxs-lookup"><span data-stu-id="87f48-222">However, another option is to manually push the DSC configuration to your machines, either locally or remotely.</span></span>

<span data-ttu-id="87f48-223">Observe que, neste exemplo, há um parâmetro adicional para o nome do computador.</span><span class="sxs-lookup"><span data-stu-id="87f48-223">Note that in this example, there's an added parameter for the computer name.</span></span> <span data-ttu-id="87f48-224">Agora, os arquivos remotos estão localizados em um compartilhamento remoto deve ser acessível pelos computadores que você deseja proteger.</span><span class="sxs-lookup"><span data-stu-id="87f48-224">The remote files are now located on a remote share that should be accessible by the machines that you want to protect.</span></span> <span data-ttu-id="87f48-225">O final do script coloca a configuração em prática e começa a aplicar a configuração de DSC ao computador de destino.</span><span class="sxs-lookup"><span data-stu-id="87f48-225">The end of the script enacts the configuration and then starts to apply the DSC configuration to the target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="87f48-226">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="87f48-226">Prerequisites</span></span>
<span data-ttu-id="87f48-227">Certifique-se de que o módulo xPSDesiredStateConfiguration do PowerShell esteja instalado.</span><span class="sxs-lookup"><span data-stu-id="87f48-227">Make sure that the xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="87f48-228">Para computadores com Windows em que o WMF 5.0 está instalado, você pode instalar o módulo xPSDesiredStateConfiguration executando o seguinte cmdlet nos computadores de destino:</span><span class="sxs-lookup"><span data-stu-id="87f48-228">For Windows machines where WMF 5.0 is installed, you can install the xPSDesiredStateConfiguration module by running the following cmdlet on the target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="87f48-229">Você também pode baixar e salvar o módulo caso precise distribuí-lo para máquinas do Windows que têm o WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="87f48-229">You can also download and save the module in case you need to distribute it to Windows machines that have WMF 4.0.</span></span> <span data-ttu-id="87f48-230">Execute este cmdlet em um computador em que o PowerShellGet (WMF 5.0) está presente:</span><span class="sxs-lookup"><span data-stu-id="87f48-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="87f48-231">Também para o WMF 4.0, verifique se a [atualização do Windows 8.1 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) está instalado nos computadores.</span><span class="sxs-lookup"><span data-stu-id="87f48-231">Also for WMF 4.0, ensure that the [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on the machines.</span></span>

<span data-ttu-id="87f48-232">A configuração a seguir pode ser enviada por push para computadores com Windows com o WMF 5.0 e 4.0:</span><span class="sxs-lookup"><span data-stu-id="87f48-232">The following configuration can be pushed to Windows machines that have WMF 5.0 and WMF 4.0:</span></span>

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

<span data-ttu-id="87f48-233">Se você quiser criar uma instância de seu próprio servidor de recepção do DSC na rede corporativa para imitar os recursos que você pode obter do DSC de Automação, consulte [Configurando um servidor de pull da Web de DSC](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="87f48-233">If you want to instantiate your own DSC pull server on your corporate network to mimic the capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="87f48-234">Opcional: implantar uma configuração de DSC usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="87f48-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="87f48-235">Neste artigo, o foco é como você pode criar sua própria configuração de DSC para implantar automaticamente o Serviço de Mobilidade e o Agente de VM do Azure – e assegurar que eles estejam em execução nos computadores que você quer proteger.</span><span class="sxs-lookup"><span data-stu-id="87f48-235">This article has focused on how you can create your own DSC configuration to automatically deploy the Mobility service and the Azure VM Agent--and ensure that they are running on the machines that you want to protect.</span></span> <span data-ttu-id="87f48-236">Também temos um modelo do Azure Resource Manager que implantará essa configuração de DSC em uma conta nova ou existente da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="87f48-236">We also have an Azure Resource Manager template that will deploy this DSC configuration to a new or existing Azure Automation account.</span></span> <span data-ttu-id="87f48-237">O modelo usará parâmetros de entrada para criar ativos de Automação que conterão as variáveis para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="87f48-237">The template will use input parameters to create Automation assets that will contain the variables for your environment.</span></span>

<span data-ttu-id="87f48-238">Após implantar o modelo, você pode simplesmente consultar a etapa 4 deste guia para integrar suas máquinas.</span><span class="sxs-lookup"><span data-stu-id="87f48-238">After you deploy the template, you can simply refer to step 4 in this guide to onboard your machines.</span></span>

<span data-ttu-id="87f48-239">O modelo fará o seguinte:</span><span class="sxs-lookup"><span data-stu-id="87f48-239">The template will do the following:</span></span>

1. <span data-ttu-id="87f48-240">Usar uma conta existente ou criar uma nova conta de Automação</span><span class="sxs-lookup"><span data-stu-id="87f48-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="87f48-241">Obter parâmetros de entrada para:</span><span class="sxs-lookup"><span data-stu-id="87f48-241">Take input parameters for:</span></span>
   * <span data-ttu-id="87f48-242">ASRRemoteFile – a localização na qual você armazenou a instalação do Serviço de Mobilidade</span><span class="sxs-lookup"><span data-stu-id="87f48-242">ASRRemoteFile--the location where you have stored the Mobility service setup</span></span>
   * <span data-ttu-id="87f48-243">ASRPassphrase – a localização na qual você armazenou o arquivo passphrase.txt</span><span class="sxs-lookup"><span data-stu-id="87f48-243">ASRPassphrase--the location where you have stored the passphrase.txt file</span></span>
   * <span data-ttu-id="87f48-244">ASRCSEndpoint – o endereço IP do seu servidor de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="87f48-244">ASRCSEndpoint--the IP address of your management server</span></span>
3. <span data-ttu-id="87f48-245">Importar o módulo do PowerShell xPSDesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="87f48-245">Import the xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="87f48-246">Criar e compilar a configuração de DSC</span><span class="sxs-lookup"><span data-stu-id="87f48-246">Create and compile the DSC configuration</span></span>

<span data-ttu-id="87f48-247">Todas as etapas anteriores serão executadas na ordem correta para que você possa começar a integrar suas máquinas para ter proteção.</span><span class="sxs-lookup"><span data-stu-id="87f48-247">All the preceding steps will happen in the right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="87f48-248">O modelo com instruções de implantação está localizado no [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span><span class="sxs-lookup"><span data-stu-id="87f48-248">The template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="87f48-249">Implantar o modelo usando o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="87f48-249">Deploy the template by using PowerShell:</span></span>

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a><span data-ttu-id="87f48-250">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="87f48-250">Next steps</span></span>
<span data-ttu-id="87f48-251">Depois de implantar os agentes do Serviço de Mobilidade, você pode [habilitar a replicação](site-recovery-vmware-to-azure.md) para as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="87f48-251">After you deploy the Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for the virtual machines.</span></span>
