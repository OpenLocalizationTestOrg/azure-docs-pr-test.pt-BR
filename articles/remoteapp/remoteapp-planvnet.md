---
title: "aaaHow tooplan sua rede virtual para uma coleção do RemoteApp do Azure | Microsoft Docs"
description: "Saiba como tooplan sua rede virtual para uma coleção do RemoteApp do Azure."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: ad9aff0e-f374-49c0-951d-4a7be1c36de0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: d7eeefc3c66815b18f9338e2e428585e6f81a12a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooplan-your-virtual-network-for-azure-remoteapp"></a>Como tooplan sua rede virtual do Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Este documento descreve como tooset a sua rede virtual do Azure (VNET) e a sub-rede de saudação do Azure RemoteApp. Se você estiver familiarizado com redes virtuais do Azure, esse é um recurso que ajuda você toovirtualize sua rede toohello toocreate e nuvem híbrida soluções de infraestrutura com o Azure e seus recursos locais. Saiba mais sobre isso [aqui](../virtual-network/virtual-networks-overview.md).

Se você quiser toodefine políticas de segurança para tráfego (entrado e saído) em sua rede virtual em que você está implantando o Azure RemoteApp, é altamente recomendável criar uma sub-rede separada para o Azure RemoteApp do restante da saudação suas implantações em hello Azure rede virtual. Para obter mais informações sobre como toodefine diretivas de segurança do Azure virtual sub-rede de rede, leia [o que é um grupo de segurança de rede (NSG)?](../virtual-network/virtual-networks-nsg.md).

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a>Tipos de coleções do RemoteApp do Azure com redes virtuais do Azure
Olá gráficos a seguir mostram Olá duas opções diferentes de coleção quando desejar toouse uma rede virtual.

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a>Coleção de nuvem do RemoteApp do Azure com VNET
 ![RemoteApp do Azure - Coleção de nuvem do RemoteApp do Azure com uma VNET](./media/remoteapp-planvpn/ra-cloudvpn.png)

Isso representa uma coleção do RemoteApp do Azure em que todos os recursos de saudação hosts da sessão RemoteApp Olá necessário tooaccess são implantados no Azure. Eles podem estar no hello mesmo VNET como Olá VNET do RemoteApp ou uma rede virtual diferente no Azure.

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a>Coleção híbrida do RemoteApp do Azure com VNET
![RemoteApp do Azure - Coleção híbrida com uma VNET](./media/remoteapp-planvpn/ra-hybridvpn.png)

Isso representa uma coleção do RemoteApp do Azure em que alguns dos recursos de saudação hosts da sessão RemoteApp Olá necessário tooaccess são implantados no local. Olá VNET do RemoteApp é vinculado toohello rede de local usando tecnologias de híbrido do Azure como VPN site a site ou rota expressa.

## <a name="how-hello-system-works"></a>Como funciona o sistema Olá
Sob as coberturas de saudação do Azure RemoteApp implanta sub-rede da rede virtual toohello máquinas virtuais do Azure (com a sua imagem carregada) que você escolheu durante o provisionamento. Se você tiver optado por uma coleção híbrida, tentamos tooresolve Olá FQDN do controlador de domínio Olá inserido no hello provisionamento de fluxo de trabalho com o servidor DNS Olá fornecido na rede virtual hello.  
Se você estiver se conectando a rede virtual existente do tooan, certifique-se de que tooexpose Olá as portas necessárias em seus grupos de segurança de rede em sua sub-rede do Azure RemoteApp. 

Recomendamos que você use uma [sub-rede suficientemente grande para o Azure RemoteApp](remoteapp-vnetsizing.md). Olá maior suportada pela rede Virtual do Azure é/8 (usando definições de subrede CIDR). Sua sub-rede deve ser grande o suficiente tooaccommodate todas as VMs de RemoteApp do Azure Olá durante a expansão vertical quando mais usuários acessam aplicativos hello. 

A seguir é coisas Olá precisará tooenable em sua sub-rede da rede virtual: 

1. O tráfego de saída da sub-rede Olá deve ser permitido na porta intervalo 10101 10175 toocommunicate com um dos serviços do Azure RemoteApp internos de saudação.
2. O tráfego de saída deve ter permissão de tooAzure de tooconnect sua sub-rede armazenamento na porta 443
3. Se você tiver o Active Directory hospedado no Azure, certifique-se de que qualquer VM na sub-rede da rede virtual Olá para o Azure RemoteApp é controlador de domínio pode tooconnect toothat. Olá DNS na rede virtual Olá deve ser capaz de tooresolve Olá FQDN deste controlador de domínio.

## <a name="virtual-network-with-forced-tunneling"></a>Rede virtual com túnel forçado
[túnel forçado](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) para todas as novas coleções do RemoteApp do Azure. No momento não oferecemos suporte migração Olá de um toosupport de coleção existente túnel forçado.  Você terá toodelete todas as suas coleções existentes usando Olá VNET que você está vinculando tooAzure RemoteApp e crie um novo um tooget habilitado em suas coleções de túnel forçado. 

