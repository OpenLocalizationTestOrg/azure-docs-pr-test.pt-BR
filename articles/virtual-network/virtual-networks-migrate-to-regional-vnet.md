---
title: "aaaMigrate uma rede virtual do Azure (clássica) de uma área do grupo de afinidade tooa | Microsoft Docs"
description: "Saiba como toomigrate uma rede virtual (clássica) de uma afinidade agrupar tooa região."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a>Migrar de uma rede virtual (clássica) de uma região de tooa do grupo de afinidade

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo de implantação do Gerenciador de recursos de saudação.

Grupos de afinidade Certifique-se de que os recursos criados no mesmo grupo de afinidade fisicamente hospedadas por servidores que estão próximos uns dos outros, permitindo que essas toocommunicate recursos mais rápida de saudação. Em Olá passado, grupos de afinidade eram um requisito para criar redes virtuais (clássico). Nesse momento, serviço de Gerenciador de rede Olá gerenciados redes virtuais (clássico) funcionaria apenas dentro de um conjunto de servidores físicos ou unidade de escala. Melhorias na arquitetura aumentaram o escopo de saudação da região de tooa de gerenciamento de rede.

Como resultado dessas melhorias na arquitetura, os grupos de afinidade não são mais recomendados nem obrigatórios para redes virtuais (clássicas). uso de saudação de grupos de afinidade para redes virtuais (clássico) é substituído por regiões. Redes virtuais (clássicas) associadas a regiões são chamadas de redes virtuais regionais.

Recomendamos que você não use grupos de afinidades em geral. Além de requisito de rede virtual hello, grupos de afinidade também foram toouse importante tooensure recursos, como (clássico) de computação e armazenamento (clássico), foram colocados próximos um do outro. No entanto, com a arquitetura de rede do Azure atual hello, esses requisitos de colocação não são mais necessários.

> [!IMPORTANT]
> Embora seja tecnicamente possível toocreate uma rede virtual que está associada um grupo de afinidade, não há nenhum toodo motivo convincente para. Muitos recursos de rede virtual, como grupos de segurança de rede, estão disponíveis somente com o uso de uma rede virtual regional e não estão disponíveis para redes virtuais associadas a grupos de afinidades.
> 
> 

## <a name="edit-hello-network-configuration-file"></a>Editar o arquivo de configuração de rede Olá

1. Exporte arquivo de configuração de rede hello. toolearn como tooexport uma configuração de rede de arquivo usando o PowerShell ou hello Azure interface de linha de comando (CLI) 1.0, consulte [configurar uma rede virtual usando um arquivo de configuração de rede](virtual-networks-using-network-configuration-file.md#export).
2. Editar o arquivo de configuração de rede hello, substituindo **AffinityGroup** com **local**. Especifique uma [região](https://azure.microsoft.com/regions) do Azure para **Local**.
   
   > [!NOTE]
   > Olá **local** é Olá região que você especificou para o grupo de afinidade Olá associado a sua rede virtual (clássica). Por exemplo, se sua rede virtual (clássica) é associado um grupo de afinidade que está localizado no Oeste dos EUA, quando você migra, sua **local** deve apontar tooWest dos EUA. 
   > 
   > 
   
    Edite saudação linhas no arquivo de configuração de rede a seguir, substituindo valores hello com seu próprio: 
   
    **Valor antigo:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\> 
   
    **Novo valor:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\>
3. Salve suas alterações e [importar](virtual-networks-using-network-configuration-file.md#import) Olá tooAzure de configuração de rede.

> [!NOTE]
> Essa migração não causa nenhum tempo de inatividade tooyour serviços.
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a>Quais toodo se você tiver uma VM (clássico) em um grupo de afinidade
Máquinas virtuais (clássicos) que estão atualmente em um grupo de afinidade não é necessário toobe removido do grupo de afinidade de saudação. Depois de uma VM é implantada, é implantado tooa unidade de escala única. Grupos de afinidade pode restringir o conjunto de saudação de tamanhos VM disponíveis para uma nova implantação de VM, mas qualquer VM existente que é implantado já está restrita tamanhos de conjunto de toohello de VM disponível na unidade de escala Olá quais Olá VM é implantada. Como Olá que VM já está implantada tooa unidade de escala, remover uma máquina virtual de um grupo de afinidade não tem efeito sobre Olá VM.
