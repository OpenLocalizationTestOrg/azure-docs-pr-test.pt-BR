---
title: toocreate de filtro de pacote do aaaUse FreeBSD um firewall no Azure | Microsoft Docs
description: Saiba como toodeploy um NAT firewall usando do FreeBSD PF no Azure.
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/20/2017
ms.author: kyliel
ms.openlocfilehash: 3d3a5dde2ca03ba6fc384581c786f5eb746e6d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-freebsds-packet-filter-toocreate-a-secure-firewall-in-azure"></a>Como toocreate de filtro de pacote do toouse FreeBSD um firewall seguro no Azure
Este artigo apresenta como toodeploy um firewall NAT usando Packer filtro do FreeBSD por meio do modelo do Gerenciador de recursos do Azure para o cenário de servidor da web comuns.

## <a name="what-is-pf"></a>O que é o PF?
PF (Filtro de Pacote, também grafado pf) é um filtro de pacote com estado licenciado BSD, uma parte central do software de firewall. Desde então, o PF evoluiu rapidamente e agora apresenta várias vantagens sobre outros firewalls disponíveis. Conversão de endereço de rede (NAT) está em PF desde o primeiro dia, em seguida, o Agendador de pacotes e gerenciamento de fila ativa foram integradas ao PF, integrando Olá ALTQ e tornando configuráveis por meio da configuração do PF. Recursos como pfsync e CARP para failover e redundância, authpf para autenticação de sessão e proxy ftp tooease firewall Olá difícil protocolo FTP, também tem estendido PF. Em resumo, o PF é um firewall avançado e repleto de recursos. 

## <a name="get-started"></a>Introdução
Se você estiver interessado em configurar um firewall seguro na nuvem Olá para seus servidores web, vamos começar. Você também pode aplicar scripts Olá usados neste tooset de modelo do Azure Resource Manager sua topologia de rede.
modelo do Gerenciador de recursos do Azure Olá configurar uma máquina virtual de FreeBSD que executa /redirection NAT usando PF duas máquinas virtuais e FreeBSD com o servidor de web de Nginx Olá instalado e configurado. Além disso, tooperforming NAT para os dois servidores de web hello saída tráfego, Olá redirecionamento/NAT virtual machine intercepta solicitações HTTP e redirecioná-los toohello dois servidores web no modo round robin. Olá VNet usa Olá privada não roteáveis IP endereço espaço 10.0.0.2/24 e você pode modificar os parâmetros de saudação do modelo de saudação. modelo do Gerenciador de recursos do Azure Olá também define uma tabela de rotas para Olá VNet inteira, que é uma coleção de rotas individuais usadas toooverride rotas de padrão do Azure com base no endereço IP de destino hello. 

![pf_topology](./media/freebsd-pf-nat/pf_topology.jpg)
    
### <a name="deploy-through-azure-cli"></a>Implantar por meio da CLI do Azure
Você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login). Crie um grupo de recursos com [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um nome de grupo de recursos `myResourceGroup` em Olá `West US` local.

```azurecli
az group create --name myResourceGroup --location westus
```

Em seguida, implante o modelo Olá [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) com [criar implantação de grupo az](/cli/azure/group/deployment#create). Baixar [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json) em Olá mesmo caminho e definir seus próprios valores de recursos, tais como `adminPassword`, `networkPrefix`, e `domainNamePrefix`. 

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeploymentName \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/pf-freebsd-setup/azuredeploy.json \
    --parameters '@azuredeploy.parameters.json' --verbose
```

Depois de cerca de cinco minutos, você obterá informações de saudação do `"provisioningState": "Succeeded"`. Em seguida, você pode ssh toohello front-end VM (NAT) ou acessar o servidor de web Nginx em um navegador usando o endereço IP público de saudação ou FQDN de front-end Olá VM (NAT). Olá exemplo a seguir lista FQDN e o endereço IP público atribuído toohello frontend VM (NAT) em Olá `myResourceGroup` grupo de recursos. 

```azurecli
az network public-ip list --resource-group myResourceGroup
```
    
## <a name="next-steps"></a>Próximas etapas
Você deseja tooset a sua própria NAT no Azure? Software Livre: gratuito mas eficiente? Portanto, o PF é uma boa opção. Usando o modelo de saudação [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup), você só precisa de cinco minutos tooset um firewall NAT com o uso do FreeBSD de balanceamento de carga de round-robin PF no Azure para o cenário de servidor da web comuns. 

Se você quiser toolearn oferta de saudação do FreeBSD no Azure, consulte muito[tooFreeBSD de Introdução no Azure](freebsd-intro-on-azure.md).

Se você quiser tooknow mais sobre PF, consulte muito[FreeBSD manual](https://www.freebsd.org/doc/handbook/firewalls-pf.html) ou [guia do usuário do-PF](https://www.freebsd.org/doc/handbook/firewalls-pf.html).
