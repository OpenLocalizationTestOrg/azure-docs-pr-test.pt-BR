---
title: aaaDeploy QuickBooks no Azure RemoteApp | Microsoft Docs
description: Saiba como tooshare QuickBooks com o Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a>Como implantar o QuickBooks no RemoteApp do Azure?
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Use Olá informações tooshare QuickBooks a seguir como um aplicativo no Azure RemoteApp.

Você pode compartilhar o QuickBooks 2015 Enterprise com o RemoteApp do Azure em uma coleção híbrida ou de nuvem. arquivo de saudação da empresa deve residir em uma máquina virtual que está executando o servidor de banco de dados do QuickBooks que está separado dos servidores do Azure RemoteApp hello. Nunca armazenar arquivo hello da empresa em sua imagem do Azure RemoteApp - perda de dados é esperada se você fizer isso. Somente QuickBooks Enterprise dá suporte a arquivo de QuickBooks Olá hospedagem em um compartilhamento externo com o servidor de banco de dados do QuickBooks acessível por meio de rede padrão do Windows.   

> [!IMPORTANT]
> Olá QuickBooks servidor de banco de dados que está hospedando o arquivo da empresa Olá deve residir em uma VM separada em Olá mesmo VNET como Olá coleção do RemoteApp do Azure.  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a>Etapas toodeploy QuickBooks
1. Criar uma VM do Azure e instale o QuickBooks, servidor de banco de dados do QuickBooks e colocar o arquivo hello da empresa em uma VM do Azure.  Verifique se tooproperly configurar regras de firewall.
2. Instale o QuickBooks em um [imagem personalizada](remoteapp-imageoptions.md) e criar um [coleção do RemoteApp do Azure](remoteapp-collections.md), nuvem ou híbrida, em Olá exato da mesma rede virtual onde Olá VM hospedando Olá servidor de banco de dados do QuickBooks com arquivos da empresa reside. 
3. [Publicar](remoteapp-publish.md) QuickBooks aplicativo toousers
4. Iniciar o cliente do QuickBooks hospedado do Azure RemoteApp hello, navegar usando a rede toohello VM hospedagem Olá QuickBooks servidor banco de dados padrão do Windows e abra o arquivo hello da empresa. 

## <a name="documentation-references"></a>Referências de documentação
* [Configurações com suporte](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)
* [Opções de implantação](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)

Você também pode consultar a apresentação Ignite, [conceitos básicos do Microsoft Azure RemoteApp gerenciamento e administração](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -Avançar too1:02:45 tooget toohello QuickBooks parte.

## <a name="deployment-architecture"></a>Arquitetura de implantação
![Implantação do QuickBooks + RemoteApp do Azure](./media/remoteapp-quickbooks/ra-quickbooks.png)

