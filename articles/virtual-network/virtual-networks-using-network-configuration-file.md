---
title: "aaaConfigure uma rede Virtual do Azure (clássica) - arquivo de configuração de rede | Microsoft Docs"
description: "Saiba como toocreate e modificar as redes virtuais (clássico) exportando, alterando e importando um arquivo de configuração de rede."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a>Configurar uma rede virtual (clássico) usando um arquivo de configuração de rede
> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo de implantação do Gerenciador de recursos de saudação.

Você pode criar e configurar uma rede virtual (clássica) com um arquivo de configuração de rede usando hello Azure interface de linha de comando (CLI) 1.0 ou o PowerShell do Azure. Você não pode criar ou modificar uma rede virtual por meio do modelo de implantação do Azure Resource Manager hello usando um arquivo de configuração de rede. Você não pode usar Olá toocreate portal do Azure ou modificar uma rede virtual (clássica) usando um arquivo de configuração de rede, no entanto, você pode usar Olá toocreate portal do Azure uma rede virtual (clássica), sem usar um arquivo de configuração de rede.

Criar e configurar uma rede virtual (clássica) com um arquivo de configuração de rede requer exportar, alterar e importar o arquivo hello.

## <a name="export"></a>Exportar um arquivo de configuração de rede

Você pode usar o PowerShell ou hello CLI do Azure tooexport um arquivo de configuração de rede. PowerShell exporta um arquivo XML, enquanto Olá CLI do Azure exporta um arquivo json.

### <a name="powershell"></a>PowerShell
 
1. [Instale o Azure PowerShell e entrar tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Altere o diretório de saudação (e verifique se ele existir) e o nome do arquivo hello comando como desejado, em seguida, execute Olá comando tooexport Olá rede arquivo de configuração a seguir:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>CLI 1.0 do Azure

1. [Instalar hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Concluir Olá restantes etapas em um prompt de comando do Azure CLI 1.0.
2. Fazer logon tooAzure digitando Olá `azure login` comando.
3. Certifique-se de que você está no modo de asm inserindo Olá `azure config mode asm` comando.
4. Altere o diretório de saudação (e verifique se ele existir) e o nome do arquivo hello comando como desejado, em seguida, execute Olá comando tooexport Olá rede arquivo de configuração a seguir:
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a>Criar ou modificar um arquivo de configuração de rede

Um arquivo de configuração de rede é um arquivo XML (ao usar o PowerShell) ou um arquivo json (ao usar Olá CLI do Azure). Você pode editar o arquivo hello em qualquer texto ou editor XML/json. Olá [configurações de esquema de arquivo de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx) artigo inclui detalhes de todas as configurações. Para obter uma explicação adicional das configurações de hello, consulte [exibir configurações de redes virtuais e](virtual-network-manage-network.md#view-vnet). Olá alterações feitas toohello arquivo:

- Deve estar de acordo com esquema hello, ou de rede de saudação importando o arquivo de configuração falhará.
- Substituirão todas as configurações de rede existentes para sua assinatura, portanto, tenha extremo cuidado ao realizar as modificações. Por exemplo, fazer referência a arquivos configuração de rede de exemplo de hello que seguem. Digamos que o arquivo original Olá contém dois **VirtualNetworkSite** instâncias e é alterado, conforme mostrado nos exemplos de saudação. Quando você importa o arquivo hello, Azure exclui a rede virtual Olá Olá **VirtualNetworkSite** instância removida no arquivo hello. Esse cenário simplificado assume não foram nenhum recurso na rede virtual do hello, como se houvesse, não foi possível excluir a rede virtual hello e importação de saudação falharia.

> [!IMPORTANT]
> O Azure considera uma sub-rede com algo implantado tooit como **em uso**. Quando uma sub-rede estiver em uso, ela não poderá ser modificada. Antes de modificar as informações de sub-rede em um arquivo de configuração de rede, mova qualquer coisa que você implantou toohello sub-rede tooa sub-rede diferente que não está sendo modificada. Consulte [mover uma VM ou instância de função tooa outra sub-rede](virtual-networks-move-vm-role-to-subnet.md) para obter detalhes.

### <a name="example-xml-for-use-with-powershell"></a>Exemplo de XML para uso com o PowerShell

Olá, arquivo de configuração de rede de exemplo a seguir cria uma rede virtual denominada *myVirtualNetwork* com um espaço de endereço de *10.0.0.0/16* em Olá *Leste dos EUA* Azure região. rede virtual Olá contém uma sub-rede denominada *mySubnet* com um prefixo de endereço *10.0.0.0/24*.

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

Se o arquivo de configuração de rede hello exportada não contém nenhum conteúdo, você pode copiar Olá XML no exemplo anterior de saudação e colá-lo em um novo arquivo.

### <a name="example-json-for-use-with-hello-azure-cli-10"></a>Exemplo de JSON para uso com hello 1.0 da CLI do Azure

Olá, arquivo de configuração de rede de exemplo a seguir cria uma rede virtual denominada *myVirtualNetwork* com um espaço de endereço de *10.0.0.0/16* em Olá *Leste dos EUA* Azure região. rede virtual Olá contém uma sub-rede denominada *mySubnet* com um prefixo de endereço *10.0.0.0/24*.

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

Se o arquivo de configuração de rede hello exportada não contém nenhum conteúdo, você pode copiar Olá json no exemplo anterior de saudação e colá-lo em um novo arquivo.

## <a name="import"></a>Importar um arquivo de configuração de rede

Você pode usar o PowerShell ou hello CLI do Azure tooimport um arquivo de configuração de rede. PowerShell importa um arquivo XML, enquanto Olá CLI do Azure importa um arquivo json. Se Olá importação falhar, confirme o arquivo hello está em conformidade com hello [esquema de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx). 

### <a name="powershell"></a>PowerShell
 
1. [Instale o Azure PowerShell e entrar tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Alterar diretório Olá e nome do arquivo hello comando conforme necessário a seguir, execute o arquivo de configuração de rede Olá comando tooimport hello:
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>CLI 1.0 do Azure

1. [Instalar hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Concluir Olá restantes etapas em um prompt de comando do Azure CLI 1.0.
2. Fazer logon tooAzure digitando Olá `azure login` comando.
3. Certifique-se de que você está no modo de asm inserindo Olá `azure config mode asm` comando.
4. Alterar diretório Olá e nome do arquivo hello comando conforme necessário a seguir, execute o arquivo de configuração de rede Olá comando tooimport hello:

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
