---
title: "Olá aaaDeploy serviço de mobilidade de recuperação de Site com DSC de automação do Azure | Microsoft Docs"
description: "Descreve como toouse DSC de automação do Azure tooautomatically implantar o serviço de mobilidade do Azure Site Recovery hello e agente do Azure para VM do VMware e tooAzure de replicação de servidor físico"
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
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="230b9-103">Implantar o serviço de mobilidade Olá com DSC de automação do Azure para a replicação de VM</span><span class="sxs-lookup"><span data-stu-id="230b9-103">Deploy hello Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="230b9-104">No Operations Management Suite, oferecemos uma solução abrangente de backup e recuperação de desastre que pode ser usada como parte de seu plano de continuidade de negócios.</span><span class="sxs-lookup"><span data-stu-id="230b9-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="230b9-105">Começamos esta jornada com o Hyper-V, usando a Réplica do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="230b9-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="230b9-106">Mas, temos toosupport expandida de uma instalação heterogênea porque os clientes têm vários hipervisores e plataformas em suas nuvens.</span><span class="sxs-lookup"><span data-stu-id="230b9-106">But we have expanded toosupport a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="230b9-107">Se você estiver executando cargas de trabalho do VMware e/ou servidores físicos hoje, um servidor de gerenciamento executa todos os Olá componentes do Azure Site Recovery em seu ambiente toohandle Olá comunicação e replicação de dados com o Azure, quando o Azure é o destino.</span><span class="sxs-lookup"><span data-stu-id="230b9-107">If you are running VMware workloads and/or physical servers today, a management server runs all of hello Azure Site Recovery components in your environment toohandle hello communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="230b9-108">Implantar o serviço de mobilidade de recuperação de Site hello usando DSC de automação</span><span class="sxs-lookup"><span data-stu-id="230b9-108">Deploy hello Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="230b9-109">Vamos começar fazendo uma análise rápida do que este servidor de gerenciamento faz.</span><span class="sxs-lookup"><span data-stu-id="230b9-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="230b9-110">servidor de gerenciamento Olá executa várias funções de servidor.</span><span class="sxs-lookup"><span data-stu-id="230b9-110">hello management server runs several server roles.</span></span> <span data-ttu-id="230b9-111">Uma dessas funções é a de *configuração*, que coordena a comunicação e gerencia os processos de replicação e recuperação de dados.</span><span class="sxs-lookup"><span data-stu-id="230b9-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="230b9-112">Além disso, Olá *processo* função atua como um gateway de replicação.</span><span class="sxs-lookup"><span data-stu-id="230b9-112">In addition, hello *process* role acts as a replication gateway.</span></span> <span data-ttu-id="230b9-113">Essa função recebe dados de replicação das máquinas de origem protegido, otimizá-lo com o cache, a compactação e criptografia e, em seguida, envia tooan conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="230b9-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it tooan Azure storage account.</span></span> <span data-ttu-id="230b9-114">Uma das funções de saudação para a função do processo de saudação também é toopush instalação de máquinas de tooprotected de serviço de mobilidade hello e executar a descoberta automática de máquinas virtuais do VMware.</span><span class="sxs-lookup"><span data-stu-id="230b9-114">One of hello functions for hello process role is also toopush installation of hello Mobility service tooprotected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="230b9-115">Se houver um failback do Azure, Olá *destino mestre* função manipulará os dados de replicação de saudação como parte dessa operação.</span><span class="sxs-lookup"><span data-stu-id="230b9-115">If there's a failback from Azure, hello *master target* role will handle hello replication data as part of this operation.</span></span>

<span data-ttu-id="230b9-116">Para máquinas de saudação protegida, contamos com hello *serviço de mobilidade*.</span><span class="sxs-lookup"><span data-stu-id="230b9-116">For hello protected machines, we rely on hello *Mobility service*.</span></span> <span data-ttu-id="230b9-117">Esse componente é implantado tooevery máquina (VM VMware ou servidor físico) que você deseja tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="230b9-117">This component is deployed tooevery machine (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="230b9-118">Ele captura gravações de dados na máquina de saudação e encaminha-servidor de gerenciamento toohello (função de processo).</span><span class="sxs-lookup"><span data-stu-id="230b9-118">It captures data writes on hello machine and forwards them toohello management server (process role).</span></span>

<span data-ttu-id="230b9-119">Quando você está lidando com continuidade dos negócios, é importante toounderstand suas cargas de trabalho, sua infraestrutura e Olá componentes envolvidos.</span><span class="sxs-lookup"><span data-stu-id="230b9-119">When you're dealing with business continuity, it's important toounderstand your workloads, your infrastructure, and hello components involved.</span></span> <span data-ttu-id="230b9-120">Em seguida, você pode atender aos requisitos de saudação para seu objetivo de tempo de recuperação (RTO) e o objetivo de ponto de recuperação (RPO).</span><span class="sxs-lookup"><span data-stu-id="230b9-120">You can then meet hello requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="230b9-121">Nesse contexto, Olá serviço de mobilidade está tooensuring chave suas cargas de trabalho protegidos conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="230b9-121">In this context, hello Mobility service is key tooensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="230b9-122">Sendo assim, como você pode assegurar, de forma otimizada, que tem uma configuração protegida confiável com a ajuda de alguns componentes do Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="230b9-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="230b9-123">Este artigo fornece um exemplo de como você pode usar o Azure Automation desejado configuração de estado (DSC), junto com a recuperação de Site, tooensure que:</span><span class="sxs-lookup"><span data-stu-id="230b9-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, tooensure that:</span></span>

* <span data-ttu-id="230b9-124">serviço de mobilidade Hello e agente de VM do Azure são implantados toohello máquinas do Windows que você deseja tooprotect.</span><span class="sxs-lookup"><span data-stu-id="230b9-124">hello Mobility service and Azure VM agent are deployed toohello Windows machines that you want tooprotect.</span></span>
* <span data-ttu-id="230b9-125">serviço de mobilidade Hello e agente de VM do Azure sempre em execução quando o Azure é o destino de replicação hello.</span><span class="sxs-lookup"><span data-stu-id="230b9-125">hello Mobility service and Azure VM agent are always running when Azure is hello replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="230b9-126">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="230b9-126">Prerequisites</span></span>
* <span data-ttu-id="230b9-127">Uma configuração do repositório toostore Olá necessária</span><span class="sxs-lookup"><span data-stu-id="230b9-127">A repository toostore hello required setup</span></span>
* <span data-ttu-id="230b9-128">Uma frase secreta tooregister do repositório toostore Olá necessário com o servidor de gerenciamento Olá</span><span class="sxs-lookup"><span data-stu-id="230b9-128">A repository toostore hello required passphrase tooregister with hello management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="230b9-129">Uma senha exclusiva é gerada para cada servidor de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="230b9-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="230b9-130">Se você for toodeploy vários servidores de gerenciamento, você tem tooensure que Olá correto de senha é armazenada no arquivo de passphrase.txt de saudação.</span><span class="sxs-lookup"><span data-stu-id="230b9-130">If you are going toodeploy multiple management servers, you have tooensure that hello correct passphrase is stored in hello passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="230b9-131">WMF Windows Management Framework () 5.0 instalado nos computadores de saudação que você deseja tooenable para proteção (um requisito para DSC de automação)</span><span class="sxs-lookup"><span data-stu-id="230b9-131">Windows Management Framework (WMF) 5.0 installed on hello machines that you want tooenable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="230b9-132">Se você quiser toouse máquinas de DSC do Windows que tem o WMF 4.0 instalado, consulte a seção de saudação [DSC de uso em ambientes desconectados](## Use DSC in disconnected environments).</span><span class="sxs-lookup"><span data-stu-id="230b9-132">If you want toouse DSC for Windows machines that have WMF 4.0 installed, see hello section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="230b9-133">serviço de mobilidade Olá pode ser instalado por meio da linha de comando hello e aceita vários argumentos.</span><span class="sxs-lookup"><span data-stu-id="230b9-133">hello Mobility service can be installed through hello command line and accepts several arguments.</span></span> <span data-ttu-id="230b9-134">É por isso que você precisa de binários de saudação toohave (depois de extrai-los da sua configuração) e armazená-los em um local onde você pode recuperá-los usando uma configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="230b9-134">That’s why you need toohave hello binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="230b9-135">Etapa 1: Extrair os binários</span><span class="sxs-lookup"><span data-stu-id="230b9-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="230b9-136">arquivos de saudação tooextract que você precisa para esta instalação, navegue toohello directory a seguir no servidor de gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="230b9-136">tooextract hello files that you need for this setup, browse toohello following directory on your management server:</span></span>

    <span data-ttu-id="230b9-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="230b9-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="230b9-138">Nessa pasta, você verá um arquivo MSI chamado:</span><span class="sxs-lookup"><span data-stu-id="230b9-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="230b9-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="230b9-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="230b9-140">Use Olá instalador de saudação do tooextract de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="230b9-140">Use hello following command tooextract hello installer:</span></span>

    <span data-ttu-id="230b9-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="230b9-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="230b9-142">Selecione todos os arquivos e enviá-los a pasta compactada (zipada) da tooa.</span><span class="sxs-lookup"><span data-stu-id="230b9-142">Select all files and send them tooa compressed (zipped) folder.</span></span>

<span data-ttu-id="230b9-143">Agora você tem binários Olá que você precisa a instalação do serviço de mobilidade de saudação Olá tooautomate usando DSC de automação.</span><span class="sxs-lookup"><span data-stu-id="230b9-143">You now have hello binaries that you need tooautomate hello setup of hello Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="230b9-144">Senha</span><span class="sxs-lookup"><span data-stu-id="230b9-144">Passphrase</span></span>
<span data-ttu-id="230b9-145">Em seguida, você precisa toodetermine onde você deseja tooplace essa pasta compactada.</span><span class="sxs-lookup"><span data-stu-id="230b9-145">Next, you need toodetermine where you want tooplace this zipped folder.</span></span> <span data-ttu-id="230b9-146">Você pode usar uma conta de armazenamento do Azure, como mostrado posteriormente, toostore Olá frase secreta que você precisa para a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="230b9-146">You can use an Azure storage account, as shown later, toostore hello passphrase that you need for hello setup.</span></span> <span data-ttu-id="230b9-147">agente Olá, em seguida, será registrado no servidor de gerenciamento hello como parte do processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="230b9-147">hello agent will then register with hello management server as part of hello process.</span></span>

<span data-ttu-id="230b9-148">Olá frase secreta que você obteve quando você implantou o servidor de gerenciamento Olá pode ser salvo o arquivo de texto tooa como passphrase.txt.</span><span class="sxs-lookup"><span data-stu-id="230b9-148">hello passphrase that you got when you deployed hello management server can be saved tooa text file as passphrase.txt.</span></span>

<span data-ttu-id="230b9-149">Coloca pasta compactada hello e a frase secreta de saudação em um contêiner dedicado em Olá conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="230b9-149">Place both hello zipped folder and hello passphrase in a dedicated container in hello Azure storage account.</span></span>

![Localização da pasta](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="230b9-151">Se você preferir tookeep esses arquivos em um compartilhamento na rede, você pode fazer isso.</span><span class="sxs-lookup"><span data-stu-id="230b9-151">If you prefer tookeep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="230b9-152">Basta tooensure que recursos Olá DSC que você usará mais tarde tem acesso e podem obter a senha e a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="230b9-152">You just need tooensure that hello DSC resource that you will be using later has access and can get hello setup and passphrase.</span></span>

## <a name="step-2-create-hello-dsc-configuration"></a><span data-ttu-id="230b9-153">Etapa 2: Criar configuração Olá DSC</span><span class="sxs-lookup"><span data-stu-id="230b9-153">Step 2: Create hello DSC configuration</span></span>
<span data-ttu-id="230b9-154">instalação de saudação depende do WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="230b9-154">hello setup depends on WMF 5.0.</span></span> <span data-ttu-id="230b9-155">Para Olá máquina toosuccessfully aplicar configuração Olá por meio da DSC de automação, WMF 5.0 precisa toobe presente.</span><span class="sxs-lookup"><span data-stu-id="230b9-155">For hello machine toosuccessfully apply hello configuration through Automation DSC, WMF 5.0 needs toobe present.</span></span>

<span data-ttu-id="230b9-156">ambiente de saudação usa Olá exemplo de configuração de DSC a seguir:</span><span class="sxs-lookup"><span data-stu-id="230b9-156">hello environment uses hello following example DSC configuration:</span></span>

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
<span data-ttu-id="230b9-157">configuração de saudação fará a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="230b9-157">hello configuration will do hello following:</span></span>

* <span data-ttu-id="230b9-158">variáveis de saudação informará configuração Olá onde tooget Olá binários para o serviço de mobilidade hello e agente de VM do Azure hello, onde tooget Olá frase secreta, e toostore Olá de saída.</span><span class="sxs-lookup"><span data-stu-id="230b9-158">hello variables will tell hello configuration where tooget hello binaries for hello Mobility service and hello Azure VM agent, where tooget hello passphrase, and where toostore hello output.</span></span>
* <span data-ttu-id="230b9-159">Olá configuração vai importar recurso de xPSDesiredStateConfiguration DSC Olá, para que você possa usar `xRemoteFile` arquivos de saudação toodownload do repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="230b9-159">hello configuration will import hello xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` toodownload hello files from hello repository.</span></span>
* <span data-ttu-id="230b9-160">configuração de saudação criará um diretório onde você deseja que os binários de saudação toostore.</span><span class="sxs-lookup"><span data-stu-id="230b9-160">hello configuration will create a directory where you want toostore hello binaries.</span></span>
* <span data-ttu-id="230b9-161">recursos de arquivo Hello extrairá os arquivos de saudação da pasta compactada hello.</span><span class="sxs-lookup"><span data-stu-id="230b9-161">hello archive resource will extract hello files from hello zipped folder.</span></span>
* <span data-ttu-id="230b9-162">recurso de instalação do pacote de saudação instalará o serviço de mobilidade de saudação do hello UNIFIEDAGENT. Instalador do EXE com argumentos de saudação específico.</span><span class="sxs-lookup"><span data-stu-id="230b9-162">hello package Install resource will install hello Mobility service from hello UNIFIEDAGENT.EXE installer with hello specific arguments.</span></span> <span data-ttu-id="230b9-163">(variáveis Olá construir argumentos Olá necessário tooreflect toobe alterado seu ambiente.)</span><span class="sxs-lookup"><span data-stu-id="230b9-163">(hello variables that construct hello arguments need toobe changed tooreflect your environment.)</span></span>
* <span data-ttu-id="230b9-164">pacote de saudação AzureAgent recurso instalará hello Azure VM agent, que é recomendado em cada VM que é executado no Azure.</span><span class="sxs-lookup"><span data-stu-id="230b9-164">hello package AzureAgent resource will install hello Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="230b9-165">Agente de VM do Azure Olá também torna possível tooadd extensões toohello VM após o failover.</span><span class="sxs-lookup"><span data-stu-id="230b9-165">hello Azure VM agent also makes it possible tooadd extensions toohello VM after failover.</span></span>
* <span data-ttu-id="230b9-166">Olá recurso de serviço ou recursos garantirá que Olá relacionados a serviços de mobilidade e hello serviços do Azure sempre estão em execução.</span><span class="sxs-lookup"><span data-stu-id="230b9-166">hello service resource or resources will ensure that hello related Mobility services and hello Azure services are always running.</span></span>

<span data-ttu-id="230b9-167">Salvar configuração hello como **ASRMobilityService**.</span><span class="sxs-lookup"><span data-stu-id="230b9-167">Save hello configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="230b9-168">Lembre-se tooreplace Olá CSIP no servidor de gerenciamento real de configuração tooreflect hello, para que hello agente será conectado corretamente e usará a senha correta da saudação.</span><span class="sxs-lookup"><span data-stu-id="230b9-168">Remember tooreplace hello CSIP in your configuration tooreflect hello actual management server, so that hello agent will be connected correctly and will use hello correct passphrase.</span></span>
>
>

## <a name="step-3-upload-tooautomation-dsc"></a><span data-ttu-id="230b9-169">Etapa 3: Carregar tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="230b9-169">Step 3: Upload tooAutomation DSC</span></span>
<span data-ttu-id="230b9-170">Como configuração Olá DSC feitas importará um módulo de recurso de DSC necessário (xPSDesiredStateConfiguration), é necessário tooimport que o módulo de automação antes de carregar a configuração de saudação DSC.</span><span class="sxs-lookup"><span data-stu-id="230b9-170">Because hello DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need tooimport that module in Automation before you upload hello DSC configuration.</span></span>

<span data-ttu-id="230b9-171">Entrar tooyour conta de automação, procurar muito**ativos** > **módulos**e clique em **procurar galeria**.</span><span class="sxs-lookup"><span data-stu-id="230b9-171">Sign in tooyour Automation account, browse too**Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="230b9-172">Aqui você pode pesquisar Olá módulo e importá-lo tooyour conta.</span><span class="sxs-lookup"><span data-stu-id="230b9-172">Here you can search for hello module and import it tooyour account.</span></span>

![Importar módulo](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="230b9-174">Quando você terminar, vá tooyour máquina onde você tenha instalados os módulos do Azure Resource Manager hello e continuar a configuração de DSC tooimport Olá recém-criado.</span><span class="sxs-lookup"><span data-stu-id="230b9-174">When you finish this, go tooyour machine where you have hello Azure Resource Manager modules installed and proceed tooimport hello newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="230b9-175">Importar cmdlets</span><span class="sxs-lookup"><span data-stu-id="230b9-175">Import cmdlets</span></span>
<span data-ttu-id="230b9-176">No PowerShell, entrar tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="230b9-176">In PowerShell, sign in tooyour Azure subscription.</span></span> <span data-ttu-id="230b9-177">Modificar Olá cmdlets tooreflect seu ambiente e capturar informações de sua conta de automação em uma variável:</span><span class="sxs-lookup"><span data-stu-id="230b9-177">Modify hello cmdlets tooreflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="230b9-178">Carregar Olá configuração tooAutomation DSC usando Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="230b9-178">Upload hello configuration tooAutomation DSC by using hello following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a><span data-ttu-id="230b9-179">Compilar a configuração de saudação no DSC de automação</span><span class="sxs-lookup"><span data-stu-id="230b9-179">Compile hello configuration in Automation DSC</span></span>
<span data-ttu-id="230b9-180">Em seguida, você precisa toocompile configuração de saudação no DSC de automação, para que você possa iniciar tooregister nós tooit.</span><span class="sxs-lookup"><span data-stu-id="230b9-180">Next, you need toocompile hello configuration in Automation DSC, so that you can start tooregister nodes tooit.</span></span> <span data-ttu-id="230b9-181">Para fazer isso executando Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="230b9-181">You achieve that by running hello following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="230b9-182">Isso pode levar alguns minutos, porque você basicamente estiver implantando o serviço de pull de DSC do hello configuração toohello hospedado.</span><span class="sxs-lookup"><span data-stu-id="230b9-182">This can take a few minutes, because you're basically deploying hello configuration toohello hosted DSC pull service.</span></span>

<span data-ttu-id="230b9-183">Depois de compilar a configuração de saudação, você pode recuperar informações de trabalho de hello usando o PowerShell (Get-AzureRmAutomationDscCompilationJob) ou usando Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="230b9-183">After you compile hello configuration, you can retrieve hello job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using hello [Azure portal](https://portal.azure.com/).</span></span>

![Recuperar trabalho](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="230b9-185">Você agora com êxito publicado e carregar sua configuração de DSC tooAutomation DSC.</span><span class="sxs-lookup"><span data-stu-id="230b9-185">You have now successfully published and uploaded your DSC configuration tooAutomation DSC.</span></span>

## <a name="step-4-onboard-machines-tooautomation-dsc"></a><span data-ttu-id="230b9-186">Etapa 4: Carregar máquinas tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="230b9-186">Step 4: Onboard machines tooAutomation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="230b9-187">Um dos pré-requisitos Olá para concluir este cenário é que as máquinas do Windows são atualizadas com a versão mais recente de saudação do WMF.</span><span class="sxs-lookup"><span data-stu-id="230b9-187">One of hello prerequisites for completing this scenario is that your Windows machines are updated with hello latest version of WMF.</span></span> <span data-ttu-id="230b9-188">Você pode baixar e instalar a versão correta do hello para sua plataforma de saudação [Centro de Download](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="230b9-188">You can download and install hello correct version for your platform from hello [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="230b9-189">Agora, você criará um metaconfig para que você aplicará tooyour nós de DSC.</span><span class="sxs-lookup"><span data-stu-id="230b9-189">You will now create a metaconfig for DSC that you will apply tooyour nodes.</span></span> <span data-ttu-id="230b9-190">toosucceed com isso, você precisa tooretrieve Olá ponto de extremidade URL e hello chave primária para sua conta de automação selecionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="230b9-190">toosucceed with this, you need tooretrieve hello endpoint URL and hello primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="230b9-191">Você pode encontrar esses valores em **chaves** em Olá **todas as configurações** folha para Olá conta de automação.</span><span class="sxs-lookup"><span data-stu-id="230b9-191">You can find these values under **Keys** on hello **All settings** blade for hello Automation account.</span></span>

![Valores da chave](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="230b9-193">Neste exemplo, você tem um servidor físico do Windows Server 2012 R2 que você deseja tooprotect usando a recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="230b9-193">In this example, you have a Windows Server 2012 R2 physical server that you want tooprotect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a><span data-ttu-id="230b9-194">Verificar as operações de renomeação de arquivo no registro Olá pendentes</span><span class="sxs-lookup"><span data-stu-id="230b9-194">Check for any pending file rename operations in hello registry</span></span>
<span data-ttu-id="230b9-195">Antes de você iniciar o servidor de saudação do tooassociate com o ponto de extremidade do hello DSC de automação, recomendamos que você verifique as operações de renomeação de arquivo no registro Olá pendentes.</span><span class="sxs-lookup"><span data-stu-id="230b9-195">Before you start tooassociate hello server with hello Automation DSC endpoint, we recommend that you check for any pending file rename operations in hello registry.</span></span> <span data-ttu-id="230b9-196">Eles podem Proibir instalação Olá Concluindo devido tooa uma reinicialização pendente.</span><span class="sxs-lookup"><span data-stu-id="230b9-196">They might prohibit hello setup from finishing due tooa pending reboot.</span></span>

<span data-ttu-id="230b9-197">Execute Olá tooverify cmdlet que não há nenhuma reinicialização pendente no servidor de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="230b9-197">Run hello following cmdlet tooverify that there’s no pending reboot on hello server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="230b9-198">Se isso mostra vazio, você será tooproceed Okey.</span><span class="sxs-lookup"><span data-stu-id="230b9-198">If this shows empty, you are OK tooproceed.</span></span> <span data-ttu-id="230b9-199">Caso contrário, você deve resolver isso, a reinicialização do servidor de saudação durante uma janela de manutenção.</span><span class="sxs-lookup"><span data-stu-id="230b9-199">If not, you should address this by rebooting hello server during a maintenance window.</span></span>

<span data-ttu-id="230b9-200">configuração de saudação tooapply no servidor de saudação, inicie Olá ambiente de script integrado do PowerShell (ISE) e execute Olá script a seguir.</span><span class="sxs-lookup"><span data-stu-id="230b9-200">tooapply hello configuration on hello server, start hello PowerShell Integrated Scripting Environment (ISE) and run hello following script.</span></span> <span data-ttu-id="230b9-201">Isso é essencialmente uma configuração local do DSC que instruem Olá tooregister de mecanismo de Gerenciador de configurações Local com hello service de DSC de automação e recuperar a configuração específica da saudação (ASRMobilityService.localhost).</span><span class="sxs-lookup"><span data-stu-id="230b9-201">This is essentially a DSC local configuration that will instruct hello Local Configuration Manager engine tooregister with hello Automation DSC service and retrieve hello specific configuration (ASRMobilityService.localhost).</span></span>

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

<span data-ttu-id="230b9-202">Essa configuração causará Olá Gerenciador de configurações Local tooregister mecanismo próprio com DSC de automação.</span><span class="sxs-lookup"><span data-stu-id="230b9-202">This configuration will cause hello Local Configuration Manager engine tooregister itself with Automation DSC.</span></span> <span data-ttu-id="230b9-203">Ele também determina como o mecanismo de saudação deve operar, que ele deve fazer se houver uma dessincronização da configuração (ApplyAndAutoCorrect) e como ele deve prosseguir com a configuração de saudação se uma reinicialização é necessária.</span><span class="sxs-lookup"><span data-stu-id="230b9-203">It will also determine how hello engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with hello configuration if a reboot is required.</span></span>

<span data-ttu-id="230b9-204">Depois de executar esse script, o nó Olá deve começar tooregister com DSC de automação.</span><span class="sxs-lookup"><span data-stu-id="230b9-204">After you run this script, hello node should start tooregister with Automation DSC.</span></span>

![Registro de nó em andamento](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="230b9-206">Se você voltar toohello portal do Azure, você pode ver o nó recém-registrados Olá agora aparece no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="230b9-206">If you go back toohello Azure portal, you can see that hello newly registered node has now appeared in hello portal.</span></span>

![Nó registrado no portal de saudação](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="230b9-208">No servidor de saudação, você pode executar Olá PowerShell cmdlet tooverify que Olá nó foi registrado corretamente a seguir:</span><span class="sxs-lookup"><span data-stu-id="230b9-208">On hello server, you can run hello following PowerShell cmdlet tooverify that hello node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="230b9-209">Após a configuração Olá foi desconectado e aplicadas toohello server, você pode verificar isso executando Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="230b9-209">After hello configuration has been pulled and applied toohello server, you can verify this by running hello following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="230b9-210">saída de Hello mostra que servidor Olá foi extraída com êxito sua configuração:</span><span class="sxs-lookup"><span data-stu-id="230b9-210">hello output shows that hello server has successfully pulled its configuration:</span></span>

![Saída](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="230b9-212">Além disso, a instalação de serviço de mobilidade Olá tem seu próprio log que pode ser encontrado em *SystemDrive*\ProgramData\ASRSetupLogs.</span><span class="sxs-lookup"><span data-stu-id="230b9-212">In addition, hello Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="230b9-213">É isso.</span><span class="sxs-lookup"><span data-stu-id="230b9-213">That’s it.</span></span> <span data-ttu-id="230b9-214">Você agora com êxito implantados e registrados de serviço de mobilidade Olá na máquina de saudação que você deseja tooprotect usando a recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="230b9-214">You have now successfully deployed and registered hello Mobility service on hello machine that you want tooprotect by using Site Recovery.</span></span> <span data-ttu-id="230b9-215">DSC garantirá que serviços Olá necessárias sempre estão em execução.</span><span class="sxs-lookup"><span data-stu-id="230b9-215">DSC will make sure that hello required services are always running.</span></span>

![Implantação bem-sucedida](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="230b9-217">Depois que o servidor de gerenciamento de saudação detecta uma implantação bem-sucedida Olá, você pode configurar a proteção e habilitar a replicação na máquina hello usando recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="230b9-217">After hello management server detects hello successful deployment, you can configure protection and enable replication on hello machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="230b9-218">Usar o DSC em ambientes desconectados</span><span class="sxs-lookup"><span data-stu-id="230b9-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="230b9-219">Se seus computadores não toohello conectado à Internet, ainda dependem toodeploy DSC e configurar o serviço de mobilidade Olá em cargas de trabalho de saudação que você deseja tooprotect.</span><span class="sxs-lookup"><span data-stu-id="230b9-219">If your machines aren’t connected toohello Internet, you can still rely on DSC toodeploy and configure hello Mobility service on hello workloads that you want tooprotect.</span></span>

<span data-ttu-id="230b9-220">Você pode instanciar seu próprio servidor de pull de DSC em seu ambiente tooessentially fornecer Olá mesmos recursos que você obteve de DSC de automação.</span><span class="sxs-lookup"><span data-stu-id="230b9-220">You can instantiate your own DSC pull server in your environment tooessentially provide hello same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="230b9-221">Ou seja, clientes Olá extrairá configuração hello (depois de registrado) toohello DSC de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="230b9-221">That is, hello clients will pull hello configuration (after it's registered) toohello DSC endpoint.</span></span> <span data-ttu-id="230b9-222">No entanto, outra opção é máquinas toomanually push Olá DSC configuração tooyour, localmente ou remotamente.</span><span class="sxs-lookup"><span data-stu-id="230b9-222">However, another option is toomanually push hello DSC configuration tooyour machines, either locally or remotely.</span></span>

<span data-ttu-id="230b9-223">Observe que neste exemplo, há um parâmetro adicional para o nome do computador hello.</span><span class="sxs-lookup"><span data-stu-id="230b9-223">Note that in this example, there's an added parameter for hello computer name.</span></span> <span data-ttu-id="230b9-224">arquivos remotos Olá agora estão localizados em um compartilhamento remoto deve ser acessível por máquinas de saudação que você deseja tooprotect.</span><span class="sxs-lookup"><span data-stu-id="230b9-224">hello remote files are now located on a remote share that should be accessible by hello machines that you want tooprotect.</span></span> <span data-ttu-id="230b9-225">fim de saudação do script hello aplica configuração hello e, em seguida, inicia o computador de destino tooapply Olá DSC configuração toohello.</span><span class="sxs-lookup"><span data-stu-id="230b9-225">hello end of hello script enacts hello configuration and then starts tooapply hello DSC configuration toohello target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="230b9-226">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="230b9-226">Prerequisites</span></span>
<span data-ttu-id="230b9-227">Certifique-se de que Olá xPSDesiredStateConfiguration PowerShell o módulo está instalado.</span><span class="sxs-lookup"><span data-stu-id="230b9-227">Make sure that hello xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="230b9-228">Para máquinas do Windows onde o WMF 5.0 está instalado, você pode instalar o módulo xPSDesiredStateConfiguration de saudação executando Olá cmdlet a seguir em computadores de destino hello:</span><span class="sxs-lookup"><span data-stu-id="230b9-228">For Windows machines where WMF 5.0 is installed, you can install hello xPSDesiredStateConfiguration module by running hello following cmdlet on hello target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="230b9-229">Você também pode baixar e salvar o módulo Olá caso você precise toodistribute-tooWindows máquinas que tem o WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="230b9-229">You can also download and save hello module in case you need toodistribute it tooWindows machines that have WMF 4.0.</span></span> <span data-ttu-id="230b9-230">Execute este cmdlet em um computador em que o PowerShellGet (WMF 5.0) está presente:</span><span class="sxs-lookup"><span data-stu-id="230b9-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="230b9-231">Para o WMF 4.0, assegure-se também que Olá [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) esteja instalado nos computadores de saudação.</span><span class="sxs-lookup"><span data-stu-id="230b9-231">Also for WMF 4.0, ensure that hello [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on hello machines.</span></span>

<span data-ttu-id="230b9-232">Olá configuração a seguir pode ser enviada tooWindows máquinas que têm o WMF 5.0 e WMF 4.0:</span><span class="sxs-lookup"><span data-stu-id="230b9-232">hello following configuration can be pushed tooWindows machines that have WMF 5.0 and WMF 4.0:</span></span>

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

<span data-ttu-id="230b9-233">Se você quiser tooinstantiate seu próprio servidor de pull de DSC em seus recursos Olá toomimic de rede corporativa que você pode obter de DSC de automação, consulte [Configurando um servidor de pull da web de DSC](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="230b9-233">If you want tooinstantiate your own DSC pull server on your corporate network toomimic hello capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="230b9-234">Opcional: implantar uma configuração de DSC usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="230b9-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="230b9-235">Este artigo concentra-se em como você pode criar seu próprios tooautomatically de configuração DSC implantar o serviço de mobilidade hello e hello Azure VM Agent – e certifique-se de que eles sejam executados em máquinas de saudação que você deseja tooprotect.</span><span class="sxs-lookup"><span data-stu-id="230b9-235">This article has focused on how you can create your own DSC configuration tooautomatically deploy hello Mobility service and hello Azure VM Agent--and ensure that they are running on hello machines that you want tooprotect.</span></span> <span data-ttu-id="230b9-236">Também temos um modelo de Gerenciador de recursos do Azure que irá implantar essa DSC configuração tooa nova ou existente do Azure conta de automação.</span><span class="sxs-lookup"><span data-stu-id="230b9-236">We also have an Azure Resource Manager template that will deploy this DSC configuration tooa new or existing Azure Automation account.</span></span> <span data-ttu-id="230b9-237">modelo de saudação usará ativos de automação de toocreate de parâmetros de entrada que contém variáveis Olá para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="230b9-237">hello template will use input parameters toocreate Automation assets that will contain hello variables for your environment.</span></span>

<span data-ttu-id="230b9-238">Depois de implantar o modelo hello, você pode simplesmente consultar toostep 4 no tooonboard neste guia suas máquinas.</span><span class="sxs-lookup"><span data-stu-id="230b9-238">After you deploy hello template, you can simply refer toostep 4 in this guide tooonboard your machines.</span></span>

<span data-ttu-id="230b9-239">modelo de saudação fará a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="230b9-239">hello template will do hello following:</span></span>

1. <span data-ttu-id="230b9-240">Usar uma conta existente ou criar uma nova conta de Automação</span><span class="sxs-lookup"><span data-stu-id="230b9-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="230b9-241">Obter parâmetros de entrada para:</span><span class="sxs-lookup"><span data-stu-id="230b9-241">Take input parameters for:</span></span>
   * <span data-ttu-id="230b9-242">ASRRemoteFile – local Olá onde você armazenou a instalação do serviço de mobilidade Olá</span><span class="sxs-lookup"><span data-stu-id="230b9-242">ASRRemoteFile--hello location where you have stored hello Mobility service setup</span></span>
   * <span data-ttu-id="230b9-243">ASRPassphrase – local Olá onde você armazenou o arquivo de passphrase.txt Olá</span><span class="sxs-lookup"><span data-stu-id="230b9-243">ASRPassphrase--hello location where you have stored hello passphrase.txt file</span></span>
   * <span data-ttu-id="230b9-244">ASRCSEndpoint - endereço IP de saudação do servidor de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="230b9-244">ASRCSEndpoint--hello IP address of your management server</span></span>
3. <span data-ttu-id="230b9-245">Importe o módulo do PowerShell xPSDesiredStateConfiguration Olá</span><span class="sxs-lookup"><span data-stu-id="230b9-245">Import hello xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="230b9-246">Criar e compilar a configuração de DSC Olá</span><span class="sxs-lookup"><span data-stu-id="230b9-246">Create and compile hello DSC configuration</span></span>

<span data-ttu-id="230b9-247">Saudação de todas as etapas anteriores ocorrerá na ordem correta do hello, para que você pode iniciar a integração de suas máquinas para proteção.</span><span class="sxs-lookup"><span data-stu-id="230b9-247">All hello preceding steps will happen in hello right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="230b9-248">modelo de Hello, com instruções para implantação, está localizado em [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span><span class="sxs-lookup"><span data-stu-id="230b9-248">hello template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="230b9-249">Implante o modelo de saudação usando o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="230b9-249">Deploy hello template by using PowerShell:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="230b9-250">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="230b9-250">Next steps</span></span>
<span data-ttu-id="230b9-251">Depois de implantar os agentes de serviço de mobilidade hello, você pode [habilitar replicação](site-recovery-vmware-to-azure.md) para máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="230b9-251">After you deploy hello Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for hello virtual machines.</span></span>
