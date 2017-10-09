---
title: "aaaDesired configuração de estado para visão geral do Azure | Microsoft Docs"
description: "Visão geral para usar o manipulador de extensão do Microsoft Azure Olá para configuração de estado desejado do PowerShell. Incluindo pré-requisitos, arquitetura e cmdlets."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a>Manipulador de extensão de configuração de estado desejado do Azure de toohello de Introdução
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Hello Azure VM Agent e as extensões associadas são parte do hello serviços de infraestrutura do Microsoft Azure. Extensões de VM são componentes de software que estendem a funcionalidade VM hello e simplificam a várias operações de gerenciamento de VM. Por exemplo, Olá extensão VMAccess pode ser usado tooreset uma senha de administrador ou Olá Script personalizado extensão pode ser usado tooexecute um script em Olá VM.

Este artigo apresenta Olá extensão de configuração de estado de desejado (DSC) do PowerShell para VMs do Azure como parte da saudação SDK do Azure PowerShell. Você pode usar o novo tooupload de cmdlets e aplicar uma configuração de DSC do PowerShell em uma VM do Azure habilitado com hello extensão de DSC do PowerShell. chamadas de extensão de DSC do PowerShell Olá em saudação do PowerShell DSC tooenact recebeu a configuração de DSC em Olá VM. Essa funcionalidade também está disponível por meio de saudação portal do Azure.

## <a name="prerequisites"></a>Pré-requisitos
**Máquina local** toointeract com hello extensão VM do Azure, você precisa toouse ou Olá portal do Azure ou Olá SDK do Azure PowerShell. 

**O agente convidado** Olá VM do Azure que é configurado por configuração Olá DSC precisa toobe um sistema operacional que suporta o Windows Management Framework (WMF) 4.0 ou 5.0. lista completa de Olá das versões de sistema operacional com suporte pode ser encontrada no hello [histórico de versão da extensão DSC](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).

## <a name="terms-and-concepts"></a>Termos e conceitos
Este guia presume familiaridade com hello conceitos a seguir:

Configuração - um documento de configuração DSC. 

Nó - um destino para uma configuração de DSC. Neste documento, "nó" sempre se refere a tooan VM do Azure.

Dados de configuração - um arquivo .psd1 contendo dados ambientais para uma configuração

## <a name="architectural-overview"></a>Visão geral da arquitetura
Olá extensão de DSC do Azure usa hello Azure VM Agent do framework toodeliver, aplicar e relatar as configurações de DSC em execução em máquinas virtuais do Azure. Olá extensão DSC espera um arquivo. zip que contém pelo menos um documento de configuração e um conjunto de parâmetros fornecido por meio de saudação SDK do Azure PowerShell ou Olá portal do Azure.

Quando a extensão de saudação é chamado para Olá primeira vez, ele executa um processo de instalação. Esse processo instala a versão de hello Windows Management Framework (WMF) usando Olá lógica a seguir:

1. Se Olá sistema operacional da VM do Azure for Windows Server 2016, nenhuma ação é executada. Windows Server 2016 já tem a versão mais recente de saudação do PowerShell instalado.
2. Se hello `wmfVersion` propriedade for especificada, essa versão do hello WMF é instalado, a menos que é incompatível com o sistema operacional da VM hello.
3. Se nenhum `wmfVersion` propriedade for especificada, hello mais recente versão aplicável do hello WMF está instalado.

Instalação do hello WMF requer uma reinicialização. Depois da reinicialização, extensão Olá downloads arquivo. zip de saudação especificado no hello `modulesUrl` propriedade. Se este local estiver no armazenamento de BLOBs do Azure, um token SAS pode ser especificado em Olá `sasToken` propriedade tooaccess Olá arquivo. Após Olá ZIP é baixado e desempacotados, Olá função configuração definida no `configurationFunction` é executar o arquivo MOF do toogenerate hello. em seguida, executa uma extensão de saudação `Start-DscConfiguration -Force` no arquivo MOF de saudação gerado. extensão de saudação captura a saída e grava-toohello canal de Status do Azure. Desse ponto em hello LCM do DSC trata de monitoramento e correção como normal. 

## <a name="powershell-cmdlets"></a>Cmdlets do PowerShell
Cmdlets do PowerShell pode ser usados com o Gerenciador de recursos do Azure ou Olá toopackage do modelo de implantação clássico, publicar e monitorar implantações de extensão de DSC. cmdlets a seguir listados Hello são módulos de implantação clássico hello, mas "Azure" pode ser substituída pelo modelo do "AzureRm" toouse hello Azure Resource Manager. Por exemplo, `Publish-AzureVMDscConfiguration` usa Olá modelo de implantação clássico, onde `Publish-AzureRmVMDscConfiguration` usa o Gerenciador de recursos do Azure. 

`Publish-AzureVMDscConfiguration`usa um arquivo de configuração, ele procura recursos dependentes da DSC e cria um arquivo. zip que contém a configuração de saudação e configuração de saudação do DSC recursos tooenact necessários. Ele também pode criar pacote hello localmente usando Olá `-ConfigurationArchivePath` parâmetro. Caso contrário, ela publica o armazenamento de BLOBs do hello. ZIP arquivo tooAzure e protege-o com um token SAS.

arquivo do Hello. zip criado por esse cmdlet tem script de configuração do hello. ps1 na raiz de saudação da pasta de arquivamento de saudação. Os recursos têm pasta do módulo Olá colocada na pasta de arquivo hello. 

`Set-AzureVMDscExtension`Insere as configurações de saudação necessárias por Olá extensão de DSC do PowerShell em um objeto de configuração de VM. No modelo de implantação clássico hello, alterações VM de saudação devem ser aplicada tooan VM do Azure com `Update-AzureVM`. 

`Get-AzureVMDscExtension`recupera o status da extensão DSC saudação de uma VM específica. 

`Get-AzureVMDscExtensionStatus`recupera o status de saudação da configuração de DSC Olá imposta pelo manipulador de extensão de DSC hello. Essa ação pode ser executada em uma única VM ou em um grupo de VMs.

`Remove-AzureVMDscExtension`Remove o manipulador de extensão de saudação de uma determinada máquina virtual. Este cmdlet não **não** remover configuração hello, desinstalar Olá WMF ou alterar configurações de saudação aplicada na máquina virtual de saudação. Ela remove somente o manipulador de extensão de saudação. 

**Principais diferenças nos cmdlets do ASM e do Azure Resource Manager**

* Os cmdlets do Azure Resource Manager são síncronos. Os cmdlets do ASM são assíncronos.
* ResourceGroupName, VMName, ArchiveStorageAccountName, Version e Location são todos parâmetros obrigatórios no Azure Resource Manager.
* ArchiveResourceGroupName é um novo parâmetro opcional para o Azure Resource Manager. Você pode especificar esse parâmetro quando sua conta de armazenamento pertence tooa outro grupo de recursos que Olá um onde a máquina virtual de saudação é criada.
* ConfigurationArchive é chamado de ArchiveBlobName no Azure Resource Manager
* ContainerName é chamado de ArchiveContainerName no Azure Resource Manager
* StorageEndpointSuffix é chamado de ArchiveStorageEndpointSuffix no Azure Resource Manager
* opção de atualização automática de Olá foi adicionada tooAzure tooenable do Gerenciador de recursos de saudação manipulador toohello mais recente versão da extensão como e quando ele está disponível a atualização automática. Observe que esse parâmetro tem possíveis reinicializações de toocause Olá Olá VM quando uma nova versão do hello que WMF é liberado. 

## <a name="azure-portal-functionality"></a>Funcionalidade do portal do Azure
Procure tooa VM. Em Configurações -> Geral, clique em "Extensões". Um novo painel é criado. Clique em "Adicionar" e selecione DSC do PowerShell.

portal de saudação precisa de entrada.
**Script ou módulos de configuração**: esse campo é obrigatório. Requer um arquivo. ps1 que contém um script de configuração ou um arquivo. zip com um script de configuração na raiz de hello. ps1 e todos os recursos dependentes em pastas de módulo em Olá arquivos. zip. Ele pode ser criado com hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` incluído no SDK do Azure PowerShell de saudação do cmdlet. arquivo. zip de saudação é carregado em seu armazenamento de blob de usuário protegido por um token SAS. 

**Arquivo de configuração PSD1 de dados**: esse campo é opcional. Se sua configuração requer um arquivo de dados de configuração em. psd1, use este campo tooselect-lo e carregue-o armazenamento de BLOBs do usuário tooyour, onde ele é protegido por um token SAS. 

**Nome de configuração qualificado por módulo**: os arquivos .ps1 podem ter várias funções de configuração. Digite nome Olá Olá. ps1 do script de configuração seguido por um '\' e Olá nome da função de configuração de saudação. Por exemplo, se seu script. ps1 tem nome hello "configuration.ps1", e a configuração de saudação é "IisInstall", digite:`configuration.ps1\IisInstall`

**Argumentos de configuração**: se a função de configuração Olá utiliza argumentos, digite-os aqui no formato Olá `argumentName1=value1,argumentName2=value2`. Observe que esse formato é diferente daquele como argumentos de configuração são aceitos por meio de cmdlets do PowerShell ou modelos do Resource Manager. 

## <a name="getting-started"></a>Introdução
Olá extensão de DSC do Azure usa documentos de configuração DSC e aplica-los em VMs do Azure. A seguir está um exemplo simples de uma configuração. Salve localmente como "IisInstall.ps1":

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

Olá seguindo as etapas local Olá IisInstall.ps1 script na Olá especificado VM, executar configuração hello e relatar sobre o status.
###<a name="classic-model"></a>Modelo clássico
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a>Modelo do Azure Resource Manager

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a>Registro em log
Os logs são colocados em:

C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Número de versão]

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o PowerShell DSC, [visite o Centro de documentação do PowerShell Olá](https://msdn.microsoft.com/powershell/dsc/overview). 

Examine Olá [modelo do Azure Resource Manager para extensão Olá DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

toofind funcionalidade adicional que você pode gerenciar com o PowerShell DSC, [procurar a Galeria do PowerShell Olá](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) para obter mais recursos de DSC.

Para obter detalhes sobre como passar parâmetros confidenciais em configurações, consulte [gerenciar credenciais com segurança com o manipulador de extensão Olá DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

