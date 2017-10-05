---
title: "Modos de implantação do Resource Manager e Gerenciamento de Serviços (Clássico) | Microsoft Docs"
description: "Entenda as diferenças entre os modelos de implantação do Gerenciador de Recursos e do clássico."
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
ms.openlocfilehash: 0f451efa239dd36d82229f01cc385d6df46654f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-deployment-models"></a>Modelos de implantação do Azure
A plataforma Azure está em transição.  Se você for iniciante no Azure ou usando há anos, é importante entender algumas das principais alterações que estamos fazendo na plataforma durante a transição.

Todos os recursos do Azure dão suporte a um ou ambos os seguintes modelos de implantação:

* **Gerenciador de Recursos:** esse é o modelo de implantação mais recente para recursos do Azure. A maioria dos recursos mais recentes já dão suporte a esse modelo de implantação e, por fim, todos os recursos oferecerão.   
* **Clássico:** esse modelo tem suporte atualmente pela maioria dos recursos do Azure existentes. Novos recursos adicionados ao Azure não darão suporte a esse modelo.

A documentação para obter detalhes sobre cada recurso do Azure para os quais os modelos de serviço podem ser criados.

## <a name="why-does-this-matter"></a>Por que isso importa?
Isso é importante pelos seguintes motivos:

* Os recursos da plataforma Azure que você usa são diferentes entre esses dois modelos.  Por exemplo, os recursos criados usando o modelo de implantação do Gerenciador de Recursos (ou apenas o Gerenciador de Recursos) podem ser criados com [modelos do Azure Resource Manager](azure-resource-manager/resource-group-overview.md#template-deployment), enquanto que os recursos criados com o modelo clássico de implantação não podem.
* Os recursos do Azure individuais ou comportamentos podem ser diferentes entre os dois modelos ou só existem em um modelo ou em outro.  Por exemplo, o tráfego de balanceamento de carga entre máquinas virtuais criadas com o modelo clássico de implantação é *implícito* porque as máquinas virtuais são membros de um serviço de nuvem do Azure e a carga é automaticamente balanceada nas máquinas virtuais em um serviço de nuvem. Máquinas virtuais criadas usando o Gerenciador de Recursos não são membros de um serviço de nuvem e um recurso separado do balanceador de carga do Azure deve ser *explicitamente* criado para tráfego de balanceamento de carga entre várias máquinas virtuais.  
* O modo como criar, configurar e gerenciar os recursos do Azure é diferente entre esses dois modelos.
* Recursos criados usando um modelo de implantação não necessariamente interoperam com recursos criados usando um modelo de implantação diferente. Por exemplo, máquinas virtuais do Azure criadas usando um modelo de implantação somente podem ser conectadas às redes virtuais do Azure criadas usando o mesmo modelo de implantação.    

Cada um dos modelos de implantação é uma API (interface de programação de aplicativo) para cada recurso.  Há uma [API do Gerenciador de Recursos](https://msdn.microsoft.com/library/azure/dn948464.aspx) para o modelo de implantação do Gerenciador de Recursos e uma [API de Gerenciamento de Serviços](https://msdn.microsoft.com/library/azure/ee460799.aspx) para o modelo de implantação clássico. Os desenvolvedores podem escrever o código para interagir com essas APIs *diretamente*.  

Os profissionais de TI, no entanto, normalmente interagem com essas APIs *indiretamente* usando um portal gráfico em um navegador da Web, usando os cmdlets do Azure PowerShell em um computador com Windows ou usando a CLI (Interface de linha de comando) do Azure em um computador com Windows, OS X ou Linux. Todos os três métodos indiretos usados por profissionais de TI interagem diretamente com as APIs. Isso significa que quando a nova funcionalidade é introduzida nos recursos ou plataforma do Microsoft Azure, ela está sempre disponível diretamente por meio da API em primeiro lugar, com os métodos indiretos obtendo suporte para os novos recursos, e por meio de recursos depois que a API é disponibilizada.  

As seções a seguir explicam como os recursos do Azure são configurados usando modelos de implantação diferentes por meio dos três métodos indiretos.

## <a name="portals"></a>Portais
O Azure tem dois portais:

* **[Portal do Azure](https://manage.windowsazure.com):** se usa o Azure por algum tempo, você já usou este portal. Ele é usado para criar e configurar recursos mais antigos do Azure que dão suporte ao modelo de implantação clássica. Você não pode usá-lo para criar ou configurar os recursos que dão suporte apenas ao Gerenciador de Recursos. 
* **[Versão Prévia do Portal do Azure](https://azure.microsoft.com/overview/preview-portal/):** se você estiver usando um recurso mais recente do Azure, você provavelmente usou este portal. Ele pode ser usado para criar e configurar alguns recursos do Azure. Você poderá, por fim, criar e configurar todos os recursos do Azure com ele. Para alguns recursos que dão suporte a ambos os modelos de implantação, esse portal pode ser usado para criar e configurar um recurso usando qualquer um dos modelos de implantação. 

Alguns recursos só podem ser criados e configurados em um portal ou no outro. Alguns recursos (ainda) não podem ser criados ou configurados no portal e só podem ser configurados com o PowerShell, a CLI ou ambos. A documentação para obter detalhes sobre cada recurso do Azure para os quais o método pode ser criado. 

## <a name="powershell"></a>PowerShell
Com o [PowerShell](/powershell/azureps-cmdlets-docs) , você pode usar uma linha de comando ou criar scripts para criar e configurar recursos do Azure de um computador Windows.  Os recursos individuais do Azure têm [cmdlets do Gerenciador de Recursos](/powershell/azure/overview), [cmdlets de Gerenciamento de Serviços](/powershell/azure/overview?view=azuresmps-3.7.0) ou ambos.  Alguns recursos só podem ser criados e/ou configurados usando o PowerShell ou a CLI. Ao usar os cmdlets do PowerShell do Gerenciador de Recursos, dependendo do recurso, você terá duas opções para criar e configurar recursos do Azure:

* **Somente os cmdlets do PowerShell:** você pode criar e configurar cada recurso do Azure individualmente usando os cmdlets para cada recurso. Você pode fazer isso em uma linha de comando ou com a inclusão de vários comandos em um script do PowerShell que você pode armazenar e criar versão.
* **Cmdlets do PowerShell com um modelo do Gerenciador de Recursos do Azure:** você pode usar o PowerShell para criar recursos do Azure usando um modelo do Gerenciador de Recursos do Azure. Os modelos podem ser salvos e versões podem ser criadas. Saiba mais ao ler o artigo [Implantar um aplicativo com o modelo do Gerenciador de Recursos do Azure](resource-group-template-deploy.md) . Vários [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) existem para soluções comuns, e eles podem ser baixados e também modificados.

## <a name="cli"></a>CLI
Você pode criar e configurar recursos do Azure de computadores com Windows, OS X ou Linux usando a CLI.  Leia o artigo [Instalar a CLI do Azure](cli-install-nodejs.md) para instalar a CLI no sistema operacional de sua escolha. Como o PowerShell, há diferentes comandos que devem ser usados se você estiver criando recursos usando os modelos de implantação do [Gerenciador de Recursos](xplat-cli-azure-resource-manager.md) ou do [Clássico (Gerenciamento de serviço)](virtual-machines/linux/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre o [Gerenciador de Recursos](azure-resource-manager/resource-group-overview.md).
* Entenda como [criar modelos](best-practices-resource-manager-design-templates.md).

