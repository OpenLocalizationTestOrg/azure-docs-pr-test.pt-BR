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
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a>Habilitar a depuração remota ao usar a entrega contínua toopublish tooAzure
Você pode habilitar a depuração remota no Azure, para os serviços de nuvem ou máquinas virtuais, quando você usa [fornecimento contínuo](cloud-services-dotnet-continuous-delivery.md) tooAzure toopublish seguindo estas etapas.

## <a name="enabling-remote-debugging-for-cloud-services"></a>Habilitando a depuração remota para serviços de nuvem
1. No agente de compilação hello, configurar saudação inicial ambiente do Azure conforme descrito na [de linha de comando de compilação para Azure](http://msdn.microsoft.com/library/hh535755.aspx).
2. Como tempo de execução de depuração remota de saudação (msvsmon.exe) é necessário para o pacote de saudação, instalar Olá **ferramentas remotas para Visual Studio**.

    * [Ferramentas Remotas para Visual Studio 2017](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [Ferramentas Remotas para Visual Studio 2015](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [Ferramentas Remotas para Visual Studio 2013 Atualização 5](https://www.microsoft.com/download/details.aspx?id=48156)
    
    Como alternativa, você pode copiar os binários de depuração remota de saudação de um sistema que tenha instalado o Visual Studio.

3. Crie um certificado conforme descrito em [Visão geral sobre certificados para os Serviços de Nuvem do Azure](cloud-services-certs-create.md). Mantenha. Olá pfx e a impressão digital do certificado RDP e carregar o serviço de nuvem de destino do hello certificado toohello.
4. Use Olá opções a seguir na toobuild de linha de comando do MSBuild hello e pacote com a depuração remota habilitada. (Substitua caminhos reais tooyour sistema e arquivos de projeto para itens de colchetes angulares Olá).
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    `VSX64RemoteDebuggerPath`Olá caminho toohello pasta é que contém msvsmon.exe em Olá Remote Tools para Visual Studio.
    `RemoteDebuggerConnectorVersion`é a versão do SDK do Azure de saudação em seu serviço de nuvem. Ele também deve corresponder a versão Olá instalado com o Visual Studio.
5. Publica toohello serviço de nuvem de destino usando o arquivo de pacote e. cscfg do hello gerado na etapa anterior hello.
6. Importar Olá certificado (arquivo. pfx) toohello máquina que tenha o Visual Studio com o SDK do Azure para .NET instalado. Certifique-se de que toohello de tooimport `CurrentUser\My` repositório de certificados, caso contrário, anexando depurador toohello no Visual Studio falhará.

## <a name="enabling-remote-debugging-for-virtual-machines"></a>Habilitando a depuração remota para máquinas virtuais
1. Crie uma máquina virtual do Azure. Consulte [Criar uma Máquina Virtual Executando o Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Criar e Gerenciar Máquinas Virtuais do Azure no Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
2. Em Olá [página do portal clássica do Azure](http://go.microsoft.com/fwlink/p/?LinkID=269851), exibir painel toosee Olá máquina virtual do hello máquina virtual **impressão digital do certificado RDP**. Esse valor é usado para Olá `ServerThumbprint` valor na configuração da extensão hello.
3. Criar um certificado de cliente, conforme descrito na [visão geral de certificados para serviços de nuvem do Azure](cloud-services-certs-create.md) (mantenha. Olá pfx e a impressão digital do certificado RDP).
4. Instale o Azure Powershell (versão 0.7.4 ou posterior) conforme descrito na [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).
5. Execute Olá extensão do script tooenable Olá RemoteDebug a seguir. Substitua dados pessoais e caminhos de saudação com seus próprios, como o nome da assinatura, o nome do serviço e a impressão digital.
   
   > [!NOTE]
   > Esse script é configurado para o Visual Studio 2015. Se você estiver usando o Visual Studio 2013 ou o Visual Studio de 2017, modificar Olá `$referenceName` e `$extensionName` atribuições abaixo muito`RemoteDebugVS2013` ou `RemoteDebugVS2017`.

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

6. Importar Olá certificado (. pfx) toohello máquina que tenha o Visual Studio com o SDK do Azure para .NET instalado.

