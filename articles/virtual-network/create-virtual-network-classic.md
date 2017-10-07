---
title: "uma rede virtual do Azure (clássica) com várias sub-redes do aaaCreate | Microsoft Docs"
description: "Saiba como toocreate uma rede virtual (clássica) com várias sub-redes no Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a>Criar uma rede virtual (clássica) com várias sub-redes

> [!IMPORTANT]
> O Azure tem dois [modelos de implantação diferentes](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) para criar e trabalhar com recursos: Resource Manager e clássico. Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda criar a maioria das novas redes virtuais por meio de saudação [Gerenciador de recursos de](virtual-networks-create-vnet-arm-pportal.md) modelo de implantação.

Neste tutorial, saiba como toocreate uma básica rede virtual do Azure (clássica) que tem separada subredes públicas e privadas. Você pode criar recursos do Azure, como Máquinas virtuais e Serviços de nuvem em uma sub-rede. Recursos criados em redes virtuais (clássico) podem se comunicar entre si e com recursos em outra rede virtual de tooa conectado de redes.

Saiba mais sobre todas as configurações de [rede virtual](virtual-network-manage-network.md) e [sub-rede](virtual-network-manage-subnet.md).

> [!WARNING]
> Redes virtuais (clássicas) são excluídas imediatamente pelo Azure quando uma [assinatura é desabilitada](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit). Redes virtuais (clássicas) serão excluídas independentemente de existirem recursos na rede virtual hello. Se você habilitar mais tarde novamente assinatura hello, recursos que existiam na rede virtual Olá devem ser recriados.

Você pode criar uma rede virtual (clássica) usando Olá [portal do Azure](#portal), Olá [Azure interface de linha de comando (CLI) 1.0](#azure-cli), ou [PowerShell](#powershell).

## <a name="portal"></a>Portal

1. Em um navegador da Internet, vá toohello [portal do Azure](https://portal.azure.com). Faça logon usando sua [conta do Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se não tiver uma conta do Azure, você poderá assinar uma versão de [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Clique em **+ novo** no portal de saudação.
3. Digite *rede Virtual* em Olá **Olá pesquisa Marketplace** caixa na parte superior de saudação do hello **novo** folha que aparece.  Clique em **rede Virtual** quando ele aparece nos resultados da pesquisa hello.
4. Selecione **clássico** em Olá **selecionar um modelo de implantação** caixa Olá **rede Virtual** folha que aparece, clique **criar**. 
5. Digite hello valores a seguir no hello **criar rede virtual (clássica)** folha e depois clique em **criar**:

    |Configuração|Valor|
    |---|---|
    |Nome|myVnet|
    |Espaço de endereço|10.0.0.0/16|
    |Nome da sub-rede|Público|
    |Intervalo de endereços da sub-rede|10.0.0.0/24|
    |Grupo de recursos|Deixe **Criar novo** selecionado e digite **myResourceGroup**.|
    |Assinatura e localização|Selecione sua assinatura e localização.

    Se você for novo tooAzure, saiba mais sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [assinaturas](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [locais](https://azure.microsoft.com/regions) (também chamado tooas *regiões*).
4. No portal de saudação, você pode criar apenas uma sub-rede quando você criar uma rede virtual. Neste tutorial, você criará uma segunda sub-rede depois que você criar rede virtual hello. Você pode criar mais tarde recursos acessíveis pela Internet Olá **pública** sub-rede. Você também pode criar recursos que não estão acessíveis da saudação da Internet no hello **privada** sub-rede. toocreate Olá segunda sub-rede, insira **myVnet** em Olá **pesquisar recursos** caixa na parte superior de saudação da página de saudação. Clique em **myVnet** quando ele aparece nos resultados da pesquisa hello.
5. Clique em **sub-redes** (no hello **configurações** seção) em Olá **criar rede virtual (clássica)** folha que aparece.
6. Clique em **+ adicionar** em Olá **myVnet - sub-redes** folha que aparece.
7. Digite **privada** para **nome** em Olá **Adicionar sub-rede** folha. Digite **10.0.1.0/24** para **Intervalo de endereços**.  Clique em **OK**.
8. Em Olá **myVnet - sub-redes** folha, você pode ver Olá **pública** e **privada** sub-redes que você criou.
9. **Opcional**: quando você concluir este tutorial, você pode desejar que recursos de saudação toodelete que você criou, para que você não incorrer em encargos de uso:
    - Clique em **visão geral** em Olá **myVnet** folha.
    - Clique em Olá **excluir** ícone Olá **myVnet** folha.
    - exclusão de saudação tooconfirm, clique em **Sim** em Olá **rede virtual Delete** caixa.

## <a name="azure-cli"></a>CLI do Azure

1. Você pode [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), ou use Olá CLI em Olá Shell de nuvem do Azure. Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure. Ele tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta. tooget ajuda para comandos CLI, digite `azure <command> --help`. 
2. Em uma sessão CLI, faça logon em tooAzure com o comando Olá que segue. Se você clicar em **Experimente** na caixa Olá abaixo, um Shell de nuvem é aberta. Você pode fazer logon no tooyour assinatura do Azure, sem inserir Olá comando a seguir:

    ```azurecli-interactive
    azure login
    ```

3. Olá tooensure CLI está no modo de gerenciamento de serviço, digite Olá comando a seguir:

    ```azurecli-interactive
    azure config mode asm
    ```

4. Crie uma rede virtual com uma sub-rede privada:

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. Crie uma sub-rede pública na rede virtual hello:

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. Examinar a rede virtual hello e sub-redes:

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. **Opcional**: você pode desejar que recursos de saudação toodelete que você criou quando você concluir este tutorial, para que você não incorrer em encargos de uso:

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> Embora você não pode especificar um grupo de recursos toocreate uma rede virtual (clássica) usando Olá CLI, Azure cria a rede virtual Olá em um grupo de recursos denominado *rede padrão*.

## <a name="powershell"></a>PowerShell

1. Instale a versão mais recente Olá de saudação do PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) módulo. Se você for novo tooAzure PowerShell, consulte [visão geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Inicie uma sessão do PowerShell.
3. No PowerShell, faça logon no tooAzure digitando Olá `Add-AzureAccount` comando.
4. Alterar Olá seguinte caminho e nome de arquivo, conforme apropriado, em seguida, exportar o arquivo de configuração de rede existente:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. toocreate uma rede virtual com subredes públicas e privadas, use qualquer Olá de tooadd do editor de texto **VirtualNetworkSite** elemento que segue o arquivo de configuração de rede toohello.

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    Saudação de revisão completa [esquema de arquivo de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx).

6. Importar arquivo de configuração de rede hello:

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > Importar um arquivo de configuração de rede alterada pode causar alterações tooexisting de redes virtuais (clássico) na sua assinatura. Verifique se você adicionar apenas a rede virtual anterior de saudação e você não alterar ou remover todas as redes virtuais existentes da sua assinatura. 

7. Examinar a rede virtual hello e sub-redes:

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. **Opcional**: você pode desejar que recursos de saudação toodelete que você criou quando você concluir este tutorial, para que você não incorrer em encargos de uso. toodelete Olá rede virtual, e concluir as etapas de 4 a 6 novamente, Olá de remover esse tempo **VirtualNetworkSite** elemento que você adicionou na etapa 5.
 
> [!NOTE]
> Embora você não pode especificar um grupo de recursos toocreate uma rede virtual (clássica) usando o PowerShell, o Azure cria a rede virtual Olá em um grupo de recursos denominado *rede padrão*.

---

## <a name="next-steps"></a>Próximas etapas

- Consulte toolearn sobre todas as configurações de sub-rede e rede virtual [gerenciar redes virtuais](virtual-network-manage-network.md) e [gerenciar sub-redes de rede virtual](virtual-network-manage-subnet.md). Você tem várias opções para o uso de redes virtuais e sub-redes em uma produção toomeet diferente dos requisitos do ambiente.
- toofilter entrada e saída de tráfego de sub-rede, criar e aplicar [grupos de segurança de rede](virtual-networks-nsg.md) toosubnets.
- Criar um [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou um [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) máquina virtual e, em seguida, conecte-o rede virtual existente do tooan.
- redes virtuais tooconnect dois em Olá mesmo local do Azure, crie um [emparelhamento de rede virtual](create-peering-different-deployment-models.md) entre redes virtuais hello. Você pode emparelhar rede virtual uma rede virtual (Gerenciador de recursos) tooa (clássico), mas não é possível criar um emparelhamento entre duas redes virtuais (clássico).
- Conectar-se a rede de local de tooan Olá rede virtual usando um [Gateway VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [rota expressa do Azure](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuito.
