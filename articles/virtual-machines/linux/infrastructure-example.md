---
title: aaaExample passo a passo de infraestrutura do Azure | Microsoft Docs
description: "Saiba mais sobre Olá chave design e implementação diretrizes para implantar uma infraestrutura de exemplo no Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 281fc2c0-b533-45fa-81a3-728c0049c73d
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6b307c0112203aa83e1fada81966fc265397a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a>Passo a passo de infraestrutura do Azure de exemplo para VMs Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Este artigo explica como criar uma infraestrutura de aplicativo de exemplo. Nós de detalhe projetar uma infraestrutura de uma loja online simple que reúne todas as diretrizes de saudação e decisões relacionadas a convenções de nomenclatura, conjuntos de disponibilidade, redes virtuais e balanceadores de carga e realmente implantar suas máquinas virtuais (VMs).

## <a name="example-workload"></a>Carga de trabalho de exemplo
A Adventure Works Cycles deseja toobuild um aplicativo da loja online no Azure consiste em:

* Dois servidores nginx executando Olá cliente front-end em uma camada da web
* Dois servidores nginx que processam dados e pedidos em uma camada de aplicativo
* Duas partes de servidores MongoDB de um cluster fragmentado para armazenar dados e pedidos de produtos em uma camada de banco de dados
* Dois controladores de domínio do Active Directory para contas de clientes e fornecedores em uma camada de autenticação
* Todos os servidores de saudação estão localizados em duas sub-redes:
  * uma sub-rede front-end para servidores de web Olá 
  * uma sub-rede de back-end para servidores de aplicativo hello, MongoDB cluster e controladores de domínio

![Diagrama de níveis diferentes de infraestrutura de aplicativos](./media/infrastructure-example/example-tiers.png)

Entrada proteger tráfego da web deve ser balanceamento de carga entre os servidores web hello como clientes procurar repositório online hello. Ordem de processamento do tráfego na forma de saudação do HTTP solicitações da web hello servidores devem ser com balanceamento de carga entre os servidores de aplicativo hello. Além disso, a infraestrutura de saudação deve ser criada para alta disponibilidade.

design resultante Olá deve incorporar:

* Uma assinatura e uma conta do Azure
* Um único grupo de recursos
* Azure Managed Disks
* Uma rede virtual com duas sub-redes
* Conjuntos de disponibilidade para Olá VMs com funções semelhantes
* Máquinas virtuais

Todos os Olá acima siga estas convenções de nomenclatura:

* A Adventure Works Cycles usa **[carga de trabalho de TI]-[localização]-[recurso do Azure]** como prefixo
  * Neste exemplo, "**azos**" (repositório online do Azure) é Olá nome da carga de trabalho de TI e "**usar**" (Leste dos EUA 2) é o local de saudação
* As redes virtuais usam AZOS-USE-VN**[número]**
* Os conjuntos de disponibilidade usam azos-use-as-**[função]**
* Os nomes de máquina virtual usam azos-use-vm-**[nomevm]**

## <a name="azure-subscriptions-and-accounts"></a>Assinaturas e contas do Azure
A Adventure Works Cycles é usando sua assinatura do Enterprise, chamada assinatura de empresa Adventure Works, tooprovide cobrança para essa carga de trabalho de TI.

## <a name="storage"></a>Armazenamento
A Adventure Works Cycles determinou que deverá usar o Azure Managed Disks. Ao criar VMs, ambas as camadas de armazenamento disponíveis para o armazenamento são usadas:

* **Armazenamento padrão** para servidores de web hello, servidores de aplicativos e os controladores de domínio e seus discos de dados.
* **Armazenamento Premium** para servidores de cluster fragmentado MongoDB hello e seus discos de dados.

## <a name="virtual-network-and-subnets"></a>Rede virtual e sub-redes
Porque a rede virtual Olá não precisa de rede local do contínuos de conectividade toohello Adventure ciclos de trabalho, eles decidiram em uma rede virtual somente em nuvem.

Criaram uma rede virtual somente em nuvem com hello configurações usando o portal do Azure de saudação a seguir:

* Name: AZOS-USE-VN01
* Local: Leste dos EUA 2
* Espaço de endereço da rede virtual: 10.0.0.0/8
* Primeira sub-rede:
  * Nome: FrontEnd
  * Espaço de endereço: 10.0.1.0/24
* Segunda sub-rede:
  * Nome: BackEnd
  * Espaço de endereço: 10.0.2.0/24

## <a name="availability-sets"></a>Conjuntos de disponibilidade
toomaintain alta disponibilidade de todos os quatro níveis de sua loja online, a Adventure Works Cycles decidiu em quatro conjuntos de disponibilidade:

* **use azos como web** Olá para servidores de web
* **usar azos como aplicativo** Olá para servidores de aplicativos
* **use azos como db** para servidores de saudação em cluster fragmentado do MongoDB Olá
* **use azos como dc** Olá para controladores de domínio

## <a name="virtual-machines"></a>Máquinas virtuais
A Adventure Works Cycles decidido Olá nomes para suas VMs do Azure a seguir:

* **azos-use vm web01** Olá primeiro servidor de web
* **azos-use vm web02** Olá segundo servidor de web
* **azos-use vm app01** Olá primeiro servidor de aplicativos
* **azos-use vm app02** Olá segundo servidor de aplicativos
* **azos-use vm db01** para Olá primeiro MongoDB servidor Olá cluster
* **azos-use vm db02** para Olá segundo MongoDB servidor Olá cluster
* **use azos-dc01 vm** Olá primeiro controlador de domínio
* **azos-uso-vm-dc02** Olá segundo controlador de domínio

Aqui está a configuração resultante hello.

![Infraestrutura final do aplicativo implantada no Azure](./media/infrastructure-example/example-config.png)

Essa configuração inclui:

* Uma rede virtual somente em nuvem com duas sub-redes (front-end e back-end)
* O Azure Managed Disks usando discos Standard e Premium
* Quatro conjuntos de disponibilidade, um para cada camada de armazenamento online Olá
* máquinas virtuais de saudação para as camadas de saudação quatro
* Um conjunto de balanceamento de carga externo para o tráfego da web baseado em HTTPS de servidores de web hello Internet toohello
* Uma carga interna com balanceamento de conjunto para o tráfego da web não criptografada de servidores de aplicativos Olá web servidores toohello
* Um único grupo de recursos
