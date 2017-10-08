---
title: "modos de aaaResource Manager e o gerenciamento de serviços de implantação (clássico) | Microsoft Docs"
description: "Conhecer as diferenças de saudação entre modelos de implantação clássico e o Gerenciador de recursos."
services: virtual-network
documentationcenter: 
author: telmosampaio
manager: carmonm
editor: 
tags: azure-resource-manager,azure-service-management
redirect_url: ./azure-resource-manager/resource-manager-deployment-model
ms.assetid: 18a235d8-38ac-4886-9e56-b3855c73ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: telmos
ms.openlocfilehash: e14f815ba9d79d9dd8f83b45bda78d0eba0bec56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-deployment-models"></a>Modelos de implantação do Azure
Olá plataforma Windows Azure está em transição.  Se você for novo tooAzure ou têm usado por anos, é importante toounderstand algumas das alterações principais Olá estamos disponibilizando toohello plataforma durante essa transição.

Todos os recursos do Azure oferecem suporte a uma ou ambas Olá modelos de implantação a seguir:

* **Gerenciador de recursos:** este é o modelo de implantação mais recente Olá para recursos do Azure. A maioria dos recursos mais recentes já dão suporte a esse modelo de implantação e, por fim, todos os recursos oferecerão.   
* **Clássico:** esse modelo tem suporte atualmente pela maioria dos recursos do Azure existentes. Novos recursos adicionados tooAzure não dará suporte a esse modelo.

documentação de saudação para cada detalhes de recurso do Azure qual serviço de modelos pode ser criada com.

## <a name="why-does-this-matter"></a>Por que isso importa?
Isso é importante para Olá motivos a seguir:

* recursos de plataforma do Azure Olá usados são diferentes entre esses dois modelos.  Por exemplo, os recursos criados usando o modelo de implantação do Gerenciador de recursos de hello (ou apenas o Gerenciador de recursos) podem ser criados com [modelos do Azure Resource Manager](azure-resource-manager/resource-group-overview.md#template-deployment), enquanto os recursos criados com o modelo de implantação clássico Olá não é possível.
* Olá individuais de recursos do Azure ou comportamentos podem ser diferentes entre dois modelos de hello, ou só existem em um modelo ou Olá outros.  Por exemplo, o balanceamento de carga tráfego entre máquinas virtuais criadas com o modelo de implantação clássico Olá é *implícita* porque máquinas virtuais são membros de um serviço de nuvem do Azure e a carga é automaticamente balanceada em virtual máquinas em um serviço de nuvem. Máquinas virtuais criadas usando o Gerenciador de recursos não são membros de um serviço de nuvem e um recurso separado do balanceador de carga do Azure deve ser *explicitamente* criado balancear o tráfego tooload entre várias máquinas virtuais.  
* O modo como criar, configurar e gerenciar os recursos do Azure é diferente entre esses dois modelos.
* Recursos criados usando um modelo de implantação não necessariamente interoperam com recursos criados usando um modelo de implantação diferente. Por exemplo, máquinas virtuais do Azure criado usando um modelo de implantação só pode ser criado usando Olá as redes virtuais tooAzure conectado mesmo modelo de implantação.    

Base de cada um dos modelos de implantação de saudação é uma interface de programação de aplicativo (API) para cada recurso.  Há um [API do Gerenciador de recursos de](https://msdn.microsoft.com/library/azure/dn948464.aspx) para modelo de implantação do Gerenciador de recursos de saudação e um [API de gerenciamento de serviço](https://msdn.microsoft.com/library/azure/ee460799.aspx) para modelo de implantação clássico hello. Os desenvolvedores podem escrever código toointeract com essas APIs *diretamente*.  

Os profissionais de TI no entanto, normalmente interagem com essas APIs *indiretamente* usando um portal gráfico em um navegador da web, usando o Azure PowerShell cmdlets em um computador Windows ou usando hello Azure Interface de linha de comando (CLI) em um um Computador Windows, OS X ou Linux. Todos os três métodos indiretos usados pelo Olá profissional de TI interagem diretamente com hello APIs. Isso significa que, quando a nova funcionalidade é apresentada toohello Azure plataforma ou recursos, ele são sempre diretamente disponível por meio de saudação API primeiro, com métodos de indireta Olá tenham suporte para Olá novos recursos e recursos depois Olá API for disponibilizado.  

seções de saudação abaixo explicam como o Azure recursos são configurados usando Olá diferentes modelos de implantação por meio de métodos indireta Olá três.

## <a name="portals"></a>Portais
O Azure tem dois portais:

* **[Portal do Azure](https://manage.windowsazure.com):** se usa o Azure por algum tempo, você já usou este portal. É usado toocreate e configurar os recursos do Azure mais antigos que oferecem suporte ao modelo de implantação clássico hello. Você não pode usá-lo toocreate ou configurar os recursos que só dão suporte ao Gerenciador de recursos. 
* **[Versão Prévia do Portal do Azure](https://azure.microsoft.com/overview/preview-portal/):** se você estiver usando um recurso mais recente do Azure, você provavelmente usou este portal. Ele pode ser usado toocreate e configurar alguns recursos do Azure. Você, eventualmente, ser capaz de toocreate e configurar todos os recursos do Azure com ele. Para alguns recursos que dão suporte a ambos os modelos de implantação, este portal pode ser usado toocreate e configurar um recurso usando o modelo de implantação. 

Alguns recursos e recursos apenas podem ser criados e configurados em um portal ou Olá outros. Alguns recursos ou recursos (ainda) não podem ser criados ou configurada no portal e só podem ser configurados com o PowerShell, Olá CLI ou ambos. documentação de saudação para cada recurso do Azure fornece detalhes sobre qual método pode ser criado com. 

## <a name="powershell"></a>PowerShell
Com [PowerShell](/powershell/azureps-cmdlets-docs) você pode usar um toocreate de scripts de linha de comando ou criar e configurar recursos do Azure de um computador com Windows.  Os recursos individuais do Azure têm [cmdlets do Gerenciador de Recursos](/powershell/azure/overview), [cmdlets de Gerenciamento de Serviços](/powershell/azure/overview?view=azuresmps-3.7.0) ou ambos.  Alguns recursos e os recursos só podem ser criados e/ou configurado usando o PowerShell ou Olá CLI. Dependendo do recurso hello, ao usar os cmdlets do PowerShell do Gerenciador de recursos, você pode ter duas opções para criar e configurar os recursos do Azure:

* **Cmdlets do PowerShell só:** você pode criar e configurar cada recurso do Azure individualmente usando cmdlets de saudação para cada recurso. Você pode fazer isso em uma linha de comando ou com a inclusão de vários comandos em um script do PowerShell que você pode armazenar e criar versão.
* **Cmdlets do PowerShell com um modelo do Azure Resource Manager:** você pode usar o PowerShell toocreate Azure recursos usando um modelo do Gerenciador de recursos do Azure. Os modelos podem ser salvos e versões podem ser criadas. Saiba mais lendo Olá [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md) artigo. Vários [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) existem para soluções comuns, e eles podem ser baixados e também modificados.

## <a name="cli"></a>CLI
Você pode criar e configurar os recursos do Azure de computadores Windows, OS X ou Linux usando Olá CLI.  Saudação de leitura [instalação Olá CLI do Azure](cli-install-nodejs.md) Olá de tooinstall artigo CLI em seu sistema operacional de escolha. Como o PowerShell, há comandos diferentes que devem ser usados dependendo se você estiver criando recursos usando [Gerenciador de recursos de](xplat-cli-azure-resource-manager.md) ou hello [clássico (gerenciamento de serviço)](virtual-machines/linux/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) modelos de implantação.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre o [Gerenciador de Recursos](azure-resource-manager/resource-group-overview.md).
* Entender como muito[criar modelos de](best-practices-resource-manager-design-templates.md).

