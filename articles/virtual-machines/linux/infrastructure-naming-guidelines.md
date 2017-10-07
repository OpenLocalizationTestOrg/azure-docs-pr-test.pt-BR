---
title: diretrizes - Linux de nomenclatura de infraestrutura de aaaAzure | Microsoft Docs
description: "Saiba mais sobre Olá design e implementação diretrizes importantes para nomear nos serviços de infraestrutura do Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a>Diretrizes de nomenclatura de infraestrutura do Azure para VMs Linux 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Este artigo se concentra em entender como tooapproach convenções de nomenclatura para todos os seus toobuild vários recursos do Azure a lógica e facilmente identificável conjunto de recursos em seu ambiente.

## <a name="implementation-guidelines-for-naming-conventions"></a>Diretrizes de implementação de convenções de nomenclatura
Decisões:

* Quais são as suas convenções de nomenclatura de recursos do Azure?

Tarefas:

* Defina o hello afixos toouse em sua consistência toomaintain de recursos.
* Defina a conta de armazenamento nomes Olá requisito para que eles toobe globalmente exclusivo.
* Saudação de documento toobe de convenção de nomenclatura usada e distribuir tooall partes envolvidas tooensure consistência em implantações.

## <a name="naming-conventions"></a>Convenções de nomenclatura
Você deve ter uma boa convenção de nomenclatura definida para criar qualquer coisa no Azure. Uma convenção de nomenclatura garante que todos os recursos de saudação tenham um nome previsível, o que ajuda a menor sobrecarga administrativa de saudação associada ao gerenciamento desses recursos.

Você pode escolher um conjunto específico de convenções de nomenclatura definidas para toda a organização ou para uma assinatura do Azure específica ou uma conta de toofollow. Embora seja fácil para pessoas físicas em regras implícitas de tooestablish organizações ao trabalhar com recursos do Azure, você precisa tooscale capaz de toobe para equipes que trabalham juntas no Azure.

Entrem em um acordo sobre um conjunto de convenções de nomenclatura antecipadamente. Há algumas considerações sobre convenções de nomenclatura que abrangem vários conjuntos de regras.

## <a name="affixes"></a>Afixos
Como analisar toodefine uma convenção de nomenclatura, uma decisão é se afixo Olá em:

* início de saudação do nome de saudação (prefixo)
* final de saudação do nome de saudação (sufixo)

Por exemplo, aqui estão dois nomes possíveis para um grupo de recursos usando Olá `rg` fixar:

* Rg-WebApp (prefixo)
* WebApp-Rg (sufixo)

Afixos podem se referir a toodifferent aspectos que descrevem recursos específicos de saudação. Olá tabela a seguir mostra alguns exemplos usados normalmente.

| Aspecto | Exemplos | Observações |
|:--- |:--- |:--- |
| Ambiente |dev, stg, prod |Dependendo da finalidade hello e o nome de cada ambiente. |
| Local |usw (Oeste dos EUA), use (Leste dos EUA 2) |Dependendo da região de saudação do datacenter hello ou região de saudação da organização hello. |
| Componente, serviço ou produto do Azure |Rg para o grupo de recursos, VNet para a rede virtual |Dependendo do produto Olá para qual Olá recursos oferece suporte. |
| Função |db, app, web |Dependendo da função hello da máquina virtual de saudação. |
| Instância |01, 02, 03 etc. |Para recursos com mais de uma instância. Por exemplo, servidores Web com balanceamento de carga em um serviço de nuvem. |

Ao estabelecer convenções de nomenclatura, certifique-se de que elas determinam claramente que affixes toouse para cada tipo de recurso e em qual posição (prefixo sufixo do vs).

## <a name="dates"></a>Datas
Geralmente é data de saudação toodetermine importante da criação do nome de saudação de um recurso. Recomendamos que o formato de data Olá AAAAMMDD. Esse formato garante que não só Olá completo data é registrada, mas também que dois recursos cujos nomes são diferentes apenas em data Olá são classificados em ordem alfabética e em ordem cronológica.

## <a name="naming-resources"></a>Recursos de nomenclatura
Defina cada tipo de recurso na convenção de nomenclatura hello, que deve ter regras que definem como tooassign nomes de recurso de tooeach que é criado. Essas regras devem se aplicam a tipos de tooall de recursos, por exemplo:

* Assinaturas
* Contas
* Contas de armazenamento
* Redes virtuais
* Sub-redes
* Conjuntos de disponibilidade
* Grupos de recursos
* Máquinas virtuais
* Pontos de extremidade
* Grupos de segurança de rede
* Funções

tooensure que Olá nome fornece recursos de toowhich suficientes informações toodetermine refere-se, você deve usar nomes descritivos.

## <a name="computer-names"></a>Nomes de computadores
Quando você cria uma máquina virtual (VM), o Azure requer um nome de VM do too64 caracteres que é usado para o nome do recurso hello. Azure usa Olá mesmo nome para o sistema operacional de saudação instalado na VM de saudação. No entanto, esses nomes podem não sempre ser Olá mesmo.

Se uma VM é criada a partir de um arquivo de imagem. vhd que já contém um sistema operacional, nome da VM Olá no Azure pode diferir da saudação nome de computador do sistema operacional da VM. Essa situação pode adicionar um grau de gerenciamento de tooVM dificuldade, que, portanto, não é recomendável. Atribua Olá Olá do recurso de VM do Azure mesmo nome como nome do computador Olá que você atribua toohello sistema de operacional da VM.

É recomendável que esse nome de VM do Azure Olá é Olá igual a saudação subjacente de nome de computador do sistema operacional.

## <a name="storage-account-names"></a>Nomes de contas de armazenamento
Esta seção não se aplica muito[discos gerenciado do Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), pois você não criar uma conta de armazenamento separada. Para discos não gerenciados, as contas de armazenamento têm regras especiais que regem seus nomes. Você pode usar apenas letras minúsculas e números. Para obter mais informações, consulte [Criar uma conta de armazenamento](../../storage/storage-create-storage-account.md#create-a-storage-account). Além disso, o nome de conta de armazenamento hello, com t, deve ser um nome DNS global válido e exclusivo. Por exemplo, se a conta de armazenamento Olá é chamada mystorageaccount, hello nomes DNS resultantes a seguir devem ser exclusivos:

* minhacontadearmazenamento.blob.core.windows.net
* minhacontadearmazenamento.table.core.windows.net
* minhacontadearmazenamento.queue.core.windows.net

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

