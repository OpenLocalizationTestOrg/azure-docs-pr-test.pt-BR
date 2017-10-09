---
title: "aaaConnect tooAzure repositório Data Lake do VNETs | Microsoft Docs"
description: "Conecte-se o repositório tooAzure Data Lake do Azure VNETs"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c695dcf49fe4e1a87a90729cf085a938f3b51fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a>Acessar o Azure Data Lake Store por VMs em uma Rede Virtual do Azure
O Azure Data Lake Store é um serviço de PaaS executado em endereços de IP de Internet públicos. Qualquer servidor que pode se conectar pode de Internet pública toohello normalmente conectar tooAzure repositório Data Lake pontos de extremidade também. Por padrão, todas as máquinas virtuais que estão em VNETs do Azure podem acessar a saudação da Internet e, portanto, podem acessar o repositório Azure Data Lake. No entanto, é possível tooconfigure VMs em uma rede virtual toonot ter toohello de acesso à Internet. Para essas VMs, repositório Data Lake do acesso tooAzure é restrito também. Bloquear o acesso público à Internet para máquinas virtuais em VNETs do Azure pode ser feito usando qualquer um dos Olá abordagem a seguir.

* Configurando NSGs (Grupos de Segurança de Rede)
* Configurando UDRs (Rotas Definidas pelo Usuário)
* Trocando rotas por meio de BGP (protocolo padrão da indústria dinâmico roteamento) quando a rota expressa é usada esse bloco acessar toohello da Internet

Neste artigo, você aprenderá como tooenable acessar o repositório toohello Azure Data Lake de VMs do Azure que foram tooaccess restrito usando um dos três métodos de saudação os recursos listados acima.

## <a name="enabling-connectivity-tooazure-data-lake-store-from-vms-with-restricted-connectivity"></a>Habilitando a conectividade tooAzure repositório Data Lake de VMs com conectividade restrita
tooaccess do Azure Data Lake armazenar essas VMs, você deve configurar endereço IP de saudação tooaccess onde Olá conta do repositório Azure Data Lake está disponível. Você pode identificar os endereços IP de saudação para suas contas do repositório Data Lake Resolvendo nomes DNS Olá das suas contas (`<account>.azuredatalakestore.net`). Para isso, use ferramentas como **nslookup**. Abra um prompt de comando no computador e execute Olá comando a seguir.

    nslookup mydatastore.azuredatalakestore.net

saída de Hello é semelhante a seguinte hello. Olá valor contra **endereço** propriedade é o endereço IP hello associado à sua conta do repositório Data Lake.

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a>Habilitando a conectividade em VMs restritas usando o NSG
Quando uma regra NSG é usada tooblock acesso toohello Internet, em seguida, você pode criar outro NSG que permite acesso toohello endereço de IP de repositório Data Lake. Mais informações sobre as regras do NSG estão disponíveis em [O que é um Grupo de Segurança de Rede?](../virtual-network/virtual-networks-nsg.md). Para obter instruções sobre como ver toocreate NSGs [como toomanage NSGs usando Olá portal do Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a>Habilitando a conectividade em VMs restritas usando a UDR ou o ExpressRoute
Quando rotas, UDRs ou trocados BGP rotas, são usadas tooblock toohello de acesso à Internet, uma rota especial deve toobe configurado de forma que as VMs nessas sub-redes podem acessar pontos de extremidade do repositório Data Lake. Para obter mais informações, consulte [O que são Rotas Definidas pelo Usuário?](../virtual-network/virtual-networks-udr-overview.md). Para obter instruções sobre como criar UDRs, consulte [Criar UDRs no Gerenciador de Recursos](../virtual-network/virtual-network-create-udr-arm-ps.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a>Habilitando a conectividade em VMs restritas usando o ExpressRoute
Quando um circuito de rota expressa é configurado, servidores de locais de saudação podem acessar o repositório Data Lake por meio de emparelhamento público. Mais detalhes sobre como configurar o emparelhamento público no ExpressRoute está disponível em [Perguntas frequentes sobre o ExpressRoute](../expressroute/expressroute-faqs.md).

## <a name="see-also"></a>Confira também
* [Visão geral do Repositório Azure Data Lake](data-lake-store-overview.md)
* [Protegendo os dados armazenados no Azure Data Lake Store](data-lake-store-security-overview.md)

