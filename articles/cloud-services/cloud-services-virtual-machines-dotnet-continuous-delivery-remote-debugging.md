---
title: "Habilitar a depuração remota com entrega contínua | Microsoft Docs"
description: "Saiba como habilitar a depuração remota ao utilizar a entrega contínua para implantar no Azure."
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
ms.openlocfilehash: 7a8a853a93e3e9915f687a20c871444e6a0de50d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-to-publish-to-azure"></a><span data-ttu-id="137f6-103">Habilitar a depuração remota ao utilizar a entrega contínua para publicar no Azure</span><span class="sxs-lookup"><span data-stu-id="137f6-103">Enable remote debugging when using continuous delivery to publish to Azure</span></span>
<span data-ttu-id="137f6-104">Você pode habilitar a depuração remota no Azure, para os serviços de nuvem ou máquinas virtuais, ao utilizar a [entrega contínua](cloud-services-dotnet-continuous-delivery.md) para publicar no Azure seguindo as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="137f6-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) to publish to Azure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="137f6-105">Habilitando a depuração remota para serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="137f6-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="137f6-106">No agente de compilação, configure o ambiente inicial para o Azure conforme descrito em [Compilação de linha de comando para Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span><span class="sxs-lookup"><span data-stu-id="137f6-106">On the build agent, set up the initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="137f6-107">Como o tempo de execução de depuração remota (msvsmon.exe) é exigido para o pacote, instale as **Ferramentas Remotas para Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="137f6-107">Because the remote debug runtime (msvsmon.exe) is required for the package, install the **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="137f6-108">Ferramentas Remotas para Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="137f6-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="137f6-109">Ferramentas Remotas para Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="137f6-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="137f6-110">Ferramentas Remotas para Visual Studio 2013 Atualização 5</span><span class="sxs-lookup"><span data-stu-id="137f6-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="137f6-111">Você pode, como alternativa, copiar os binários de depuração remota de um sistema que tiver o Visual Studio instalado.</span><span class="sxs-lookup"><span data-stu-id="137f6-111">As an alternative, you can copy the remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="137f6-112">Crie um certificado conforme descrito em [Visão geral sobre certificados para os Serviços de Nuvem do Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="137f6-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="137f6-113">Mantenha o .pfx e a impressão digital do certificado RDP e carregue o certificado no serviço de nuvem alvo.</span><span class="sxs-lookup"><span data-stu-id="137f6-113">Keep the .pfx and RDP certificate thumbprint and upload the certificate to the target cloud service.</span></span>
4. <span data-ttu-id="137f6-114">Utilize as opções a seguir na linha de comando do MSBuild para compilar e criar o pacote com a depuração remota habilitada.</span><span class="sxs-lookup"><span data-stu-id="137f6-114">Use the following options in the MSBuild command line to build and package with remote debug enabled.</span></span> <span data-ttu-id="137f6-115">(Substitua os caminhos reais até seus arquivos do sistema e de projeto pelos itens entre colchetes angulares.)</span><span class="sxs-lookup"><span data-stu-id="137f6-115">(Substitute actual paths to your system and project files for the angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of the certificate added to the cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path to your VS solution file>"
   
    <span data-ttu-id="137f6-116">`VSX64RemoteDebuggerPath` corresponde ao caminho até a pasta contendo msvsmon.exe em Ferramentas Remotas para o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="137f6-116">`VSX64RemoteDebuggerPath` is the path to the folder containing msvsmon.exe in the Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="137f6-117">`RemoteDebuggerConnectorVersion` é a versão do SDK do Azure no serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="137f6-117">`RemoteDebuggerConnectorVersion` is the Azure SDK version in your cloud service.</span></span> <span data-ttu-id="137f6-118">Ele também deve corresponder à versão instalada com o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="137f6-118">It should also match the version installed with Visual Studio.</span></span>
5. <span data-ttu-id="137f6-119">Publique no serviço de nuvem alvo usando o pacote e o arquivo .cscfg gerado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="137f6-119">Publish to the target cloud service by using the package and .cscfg file generated in the previous step.</span></span>
6. <span data-ttu-id="137f6-120">Importe o certificado (arquivo .pfx) para a máquina que tem o Visual Studio com o SDK do Azure para .NET instalado.</span><span class="sxs-lookup"><span data-stu-id="137f6-120">Import the certificate (.pfx file) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="137f6-121">Certifique-se de importar para o `CurrentUser\My` repositório de certificados; caso contrário, a anexação do depurador do Visual Studio falhará.</span><span class="sxs-lookup"><span data-stu-id="137f6-121">Make sure to import to the `CurrentUser\My` certificate store, otherwise attaching to the debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="137f6-122">Habilitando a depuração remota para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="137f6-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="137f6-123">Crie uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="137f6-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="137f6-124">Consulte [Criar uma Máquina Virtual Executando o Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Criar e Gerenciar Máquinas Virtuais do Azure no Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="137f6-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="137f6-125">Na [página do portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=269851), exiba o painel da máquina virtual para conferir a **IMPRESSÃO DIGITAL DO CERTIFICADO RDP**da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="137f6-125">On the [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view the virtual machine's dashboard to see the virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="137f6-126">Esse valor é usado como o valor de `ServerThumbprint` na configuração da extensão.</span><span class="sxs-lookup"><span data-stu-id="137f6-126">This value is used for the `ServerThumbprint` value in the extension configuration.</span></span>
3. <span data-ttu-id="137f6-127">Crie um certificado cliente conforme descrito em [Visão geral sobre certificados para os Serviços de Nuvem do Azure](cloud-services-certs-create.md) (mantenha o .pfx e a impressão digital do certificado RDP).</span><span class="sxs-lookup"><span data-stu-id="137f6-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep the .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="137f6-128">Instale e configure o Azure PowerShell (versão 0.7.4 ou posterior) conforme descrito em [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="137f6-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="137f6-129">Execute o script a seguir para habilitar a extensão RemoteDebug.</span><span class="sxs-lookup"><span data-stu-id="137f6-129">Run the following script to enable the RemoteDebug extension.</span></span> <span data-ttu-id="137f6-130">Substitua os caminhos e os dados pessoais por seus dados, como seu nome da assinatura, nome do serviço e impressão digital.</span><span class="sxs-lookup"><span data-stu-id="137f6-130">Replace the paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="137f6-131">Esse script é configurado para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="137f6-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="137f6-132">Se você estiver usando o Visual Studio 2013 ou Visual Studio 2017, modifique as atribuições `$referenceName` e `$extensionName` abaixo para `RemoteDebugVS2013` ou `RemoteDebugVS2017`.</span><span class="sxs-lookup"><span data-stu-id="137f6-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify the `$referenceName` and `$extensionName` assignments below to `RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

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

6. <span data-ttu-id="137f6-133">Importe o certificado (.pfx) para a máquina que tem o Visual Studio com o SDK do Azure para .NET instalado.</span><span class="sxs-lookup"><span data-stu-id="137f6-133">Import the certificate (.pfx) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

