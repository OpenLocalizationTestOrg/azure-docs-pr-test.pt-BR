---
title: "Exemplos do Azure PowerShell – Service Fabric | Microsoft Docs"
description: "Exemplos do Azure PowerShell – Service Fabric"
services: service-fabric
documentationcenter: service-fabric
author: rwike77
manager: timlt
editor: 
tags: 
ms.assetid: b48d1137-8c04-46e0-b430-101e07d7e470
ms.service: service-fabric
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: service-fabric
ms.date: 12/13/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 1825b2a58e1022f22c71395477a5fca54c715455
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="azure-powershell-samples"></a>Exemplos do Azure PowerShell

A tabela a seguir contém links para exemplos de scripts do PowerShell que criam e gerenciam clusters, aplicativos e serviços do Service Fabric.

[!INCLUDE [links to azure cli and service fabric cli](../../includes/service-fabric-powershell.md)]

| | |
|-|-|
| **Criar cluster** ||
| [Criar um cluster (Azure)](./scripts/service-fabric-powershell-create-secure-cluster-cert.md)| Cria um cluster do Azure Service Fabric. |
|[Criar um cluster de teste (Azure)](./scripts/service-fabric-powershell-create-test-cluster.md)| Cria um cluster Service Fabric de teste de três nós no Azure.|
| **Gerenciar o cluster, os nós e a infraestrutura** ||
| [Adicionar um certificado de aplicativo](./scripts/service-fabric-powershell-add-application-certificate.md)| Adiciona um certificado X.509 de aplicativo a todos os nós em um cluster. |
| [Atualizar o intervalo da porta RDP nas VMs do cluster](./scripts/service-fabric-powershell-change-rdp-port-range.md)|Altera o intervalo de porta do RDP nas VMs do nó de cluster em um cluster implantado.|
| [Atualizar o usuário administrador e a senha para as VMs do nó de cluster](./scripts/service-fabric-powershell-change-rdp-user-and-pw.md) | Atualiza o nome de usuário administrador e a senha para as VMs do nó de cluster. |
| [Abrir uma porta no balanceador de carga](./scripts/service-fabric-powershell-open-port-in-load-balancer.md) | Abra uma porta de aplicativo no balanceador de carga do Azure para permitir o tráfego de entrada em uma porta específica. |
| [Criar uma regra de grupo de segurança de rede de entrada](./scripts/service-fabric-powershell-add-nsg-rule.md) | Crie uma regra de grupo de segurança de rede de entrada para permitir o tráfego de entrada para o cluster em uma porta específica. |
| **Gerenciar aplicativos** ||
| [Implantar um aplicativo](./scripts/service-fabric-powershell-deploy-application.md)| Implantar um aplicativo em um cluster.|
| [Atualizar um aplicativo](./scripts/service-fabric-powershell-upgrade-application.md)| Atualize um aplicativo.|
| [Remover um aplicativo](./scripts/service-fabric-powershell-remove-application.md)| Remover um aplicativo de um cluster.|
