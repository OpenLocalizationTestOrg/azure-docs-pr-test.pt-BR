---
title: "depuração remota com o fornecimento contínuo de aaaEnable | Microsoft Docs"
description: "Saiba como depuração remota tooenable ao usar a entrega contínua toodeploy tooAzure"
services: cloud-services
documentationcenter: .net
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d423639-3b2f-4ca5-ac5a-9ac19a217c29
ms.service: cloud-services
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: d9d9d1cfe5304c9526586a9164f172746a448e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a><span data-ttu-id="cabb4-103">Habilitar a depuração remota ao usar a entrega contínua toopublish tooAzure</span><span class="sxs-lookup"><span data-stu-id="cabb4-103">Enable remote debugging when using continuous delivery toopublish tooAzure</span></span>
<span data-ttu-id="cabb4-104">Você pode habilitar a depuração remota no Azure, para os serviços de nuvem ou máquinas virtuais, quando você usa [fornecimento contínuo](cloud-services-dotnet-continuous-delivery.md) tooAzure toopublish seguindo estas etapas.</span><span class="sxs-lookup"><span data-stu-id="cabb4-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) toopublish tooAzure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="cabb4-105">Habilitando a depuração remota para serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="cabb4-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="cabb4-106">No agente de compilação hello, configurar saudação inicial ambiente do Azure conforme descrito na [de linha de comando de compilação para Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span><span class="sxs-lookup"><span data-stu-id="cabb4-106">On hello build agent, set up hello initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="cabb4-107">Como tempo de execução de depuração remota de saudação (msvsmon.exe) é necessário para o pacote de saudação, instalar Olá **ferramentas remotas para Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="cabb4-107">Because hello remote debug runtime (msvsmon.exe) is required for hello package, install hello **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="cabb4-108">Ferramentas Remotas para Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="cabb4-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="cabb4-109">Ferramentas Remotas para Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="cabb4-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="cabb4-110">Ferramentas Remotas para Visual Studio 2013 Atualização 5</span><span class="sxs-lookup"><span data-stu-id="cabb4-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="cabb4-111">Como alternativa, você pode copiar os binários de depuração remota de saudação de um sistema que tenha instalado o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cabb4-111">As an alternative, you can copy hello remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="cabb4-112">Crie um certificado conforme descrito em [Visão geral sobre certificados para os Serviços de Nuvem do Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="cabb4-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="cabb4-113">Mantenha. Olá pfx e a impressão digital do certificado RDP e carregar o serviço de nuvem de destino do hello certificado toohello.</span><span class="sxs-lookup"><span data-stu-id="cabb4-113">Keep hello .pfx and RDP certificate thumbprint and upload hello certificate toohello target cloud service.</span></span>
4. <span data-ttu-id="cabb4-114">Use Olá opções a seguir na toobuild de linha de comando do MSBuild hello e pacote com a depuração remota habilitada.</span><span class="sxs-lookup"><span data-stu-id="cabb4-114">Use hello following options in hello MSBuild command line toobuild and package with remote debug enabled.</span></span> <span data-ttu-id="cabb4-115">(Substitua caminhos reais tooyour sistema e arquivos de projeto para itens de colchetes angulares Olá).</span><span class="sxs-lookup"><span data-stu-id="cabb4-115">(Substitute actual paths tooyour system and project files for hello angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    <span data-ttu-id="cabb4-116">`VSX64RemoteDebuggerPath`Olá caminho toohello pasta é que contém msvsmon.exe em Olá Remote Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cabb4-116">`VSX64RemoteDebuggerPath` is hello path toohello folder containing msvsmon.exe in hello Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="cabb4-117">`RemoteDebuggerConnectorVersion`é a versão do SDK do Azure de saudação em seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cabb4-117">`RemoteDebuggerConnectorVersion` is hello Azure SDK version in your cloud service.</span></span> <span data-ttu-id="cabb4-118">Ele também deve corresponder a versão Olá instalado com o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cabb4-118">It should also match hello version installed with Visual Studio.</span></span>
5. <span data-ttu-id="cabb4-119">Publica toohello serviço de nuvem de destino usando o arquivo de pacote e. cscfg do hello gerado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="cabb4-119">Publish toohello target cloud service by using hello package and .cscfg file generated in hello previous step.</span></span>
6. <span data-ttu-id="cabb4-120">Importar Olá certificado (arquivo. pfx) toohello máquina que tenha o Visual Studio com o SDK do Azure para .NET instalado.</span><span class="sxs-lookup"><span data-stu-id="cabb4-120">Import hello certificate (.pfx file) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="cabb4-121">Certifique-se de que toohello de tooimport `CurrentUser\My` repositório de certificados, caso contrário, anexando depurador toohello no Visual Studio falhará.</span><span class="sxs-lookup"><span data-stu-id="cabb4-121">Make sure tooimport toohello `CurrentUser\My` certificate store, otherwise attaching toohello debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="cabb4-122">Habilitando a depuração remota para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="cabb4-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="cabb4-123">Crie uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="cabb4-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="cabb4-124">Consulte [Criar uma Máquina Virtual Executando o Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Criar e Gerenciar Máquinas Virtuais do Azure no Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cabb4-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="cabb4-125">Em Olá [página do portal clássica do Azure](http://go.microsoft.com/fwlink/p/?LinkID=269851), exibir painel toosee Olá máquina virtual do hello máquina virtual **impressão digital do certificado RDP**.</span><span class="sxs-lookup"><span data-stu-id="cabb4-125">On hello [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view hello virtual machine's dashboard toosee hello virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="cabb4-126">Esse valor é usado para Olá `ServerThumbprint` valor na configuração da extensão hello.</span><span class="sxs-lookup"><span data-stu-id="cabb4-126">This value is used for hello `ServerThumbprint` value in hello extension configuration.</span></span>
3. <span data-ttu-id="cabb4-127">Criar um certificado de cliente, conforme descrito na [visão geral de certificados para serviços de nuvem do Azure](cloud-services-certs-create.md) (mantenha. Olá pfx e a impressão digital do certificado RDP).</span><span class="sxs-lookup"><span data-stu-id="cabb4-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep hello .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="cabb4-128">Instale o Azure Powershell (versão 0.7.4 ou posterior) conforme descrito na [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cabb4-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="cabb4-129">Execute Olá extensão do script tooenable Olá RemoteDebug a seguir.</span><span class="sxs-lookup"><span data-stu-id="cabb4-129">Run hello following script tooenable hello RemoteDebug extension.</span></span> <span data-ttu-id="cabb4-130">Substitua dados pessoais e caminhos de saudação com seus próprios, como o nome da assinatura, o nome do serviço e a impressão digital.</span><span class="sxs-lookup"><span data-stu-id="cabb4-130">Replace hello paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cabb4-131">Esse script é configurado para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="cabb4-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="cabb4-132">Se você estiver usando o Visual Studio 2013 ou o Visual Studio de 2017, modificar Olá `$referenceName` e `$extensionName` atribuições abaixo muito`RemoteDebugVS2013` ou `RemoteDebugVS2017`.</span><span class="sxs-lookup"><span data-stu-id="cabb4-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify hello `$referenceName` and `$extensionName` assignments below too`RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

    ```powershell   
    Add-AzureAccount

    Select-AzureSubscription "My Microsoft Subscription"

    $vm = Get-AzureVM -ServiceName "mytestvm1" -Name "mytestvm1"

    $endpoints = @(
                    ,@{Name="RDConnVS2013"; PublicPort=30400; PrivatePort=30398}
                    ,@{Name="RDFwdrVS2013"; PublicPort=31400; PrivatePort=31398}
                )

    foreach($endpoint in $endpoints)
    {
        Add-AzureEndpoint -VM $vm -Name $endpoint.Name -Protocol tcp -PublicPort $endpoint.PublicPort -LocalPort $endpoint.PrivatePort
    }

    $referenceName = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug.RemoteDebugVS2015"
    $publisher = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug"
    $extensionName = "RemoteDebugVS2015"
    $version = "1.*"
    $publicConfiguration = "<PublicConfig><Connector.Enabled>true</Connector.Enabled><ClientThumbprint>56D7D1B25B472268E332F7FC0C87286458BFB6B2</ClientThumbprint><ServerThumbprint>E7DCB00CB916C468CC3228261D6E4EE45C8ED3C6</ServerThumbprint><ConnectorPort>30398</ConnectorPort><ForwarderPort>31398</ForwarderPort></PublicConfig>"

    $vm | Set-AzureVMExtension -ReferenceName $referenceName -Publisher $publisher -ExtensionName $extensionName -Version $version -PublicConfiguration $publicConfiguration

    foreach($extension in $vm.VM.ResourceExtensionReferences)
    {
        if(($extension.ReferenceName -eq $referenceName) `
        -and ($extension.Publisher -eq $publisher) `
        -and ($extension.Name -eq $extensionName) `
        -and ($extension.Version -eq $version))
        {
            $extension.ResourceExtensionParameterValues[0].Key = 'config.txt'
            break
        }
    }

    $vm | Update-AzureVM
    ```

6. <span data-ttu-id="cabb4-133">Importar Olá certificado (. pfx) toohello máquina que tenha o Visual Studio com o SDK do Azure para .NET instalado.</span><span class="sxs-lookup"><span data-stu-id="cabb4-133">Import hello certificate (.pfx) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

