---
title: "conceitos de laboratórios aaaDevTest | Microsoft Docs"
description: "Aprenda os conceitos básicos de saudação do DevTest Labs e como ele pode tornar fácil toocreate, gerenciar e monitorar as máquinas virtuais do Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 105919e8-3617-4ce3-a29f-a289fa608fb2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: d9f1d948002c4d3121e5bdd4e65eb8b54cd91f9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="devtest-labs-concepts"></a>Conceitos dos Laboratórios de Desenvolvimento/Teste
## <a name="overview"></a>Visão geral
Olá lista a seguir contém definições e principais conceitos do DevTest Labs:

## <a name="labs"></a>Laboratórios
Um laboratório é a infraestrutura de saudação que abrange um grupo de recursos, como máquinas virtuais (VMs), que lhe permite melhor gerenciar esses recursos, especificando limites e cotas.

## <a name="virtual-machine"></a>Máquina virtual
Uma VM do Azure é um dos vários tipos de [recursos de computação sob demanda escalonáveis](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm) oferecidos pelo Azure. Dê de VMs do Azure Olá flexibilidade da virtualização sem a necessidade de toobuy e manter o hardware físico de saudação que executa, embora ainda seja necessário toomaintain Olá VM executando determinadas tarefas, como configurar, corrigir e instalar o software de saudação que será executado nele.

[Visão geral das máquinas virtuais do Windows no Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview) fornece informações sobre o que você deve considerar antes de criar uma VM, como criá-la e como gerenciá-la.

## <a name="claimable-vm"></a>VM Declarável
Uma VM Declarável do Azure é uma máquina virtual que está disponível para uso por qualquer usuário do laboratório com permissões. Um administrador de laboratório pode preparar as máquinas virtuais com artefatos e imagens específicas de base e salvá-los pool tooa compartilhado. Um usuário de laboratório, em seguida, pode solicitar um VM do pool de saudação do trabalho quando eles precisarem de um com essa configuração específica.

Uma VM que está claimable não está atribuída inicialmente tooany determinado usuário, mas será exibido na lista de todos os usuários em "Máquinas de virtuais Claimable". Depois de uma VM é solicitada por um usuário, ele é movido para cima tootheir área de "Minhas máquinas virtuais" e não está mais claimable por nenhum outro usuário.

## <a name="environment"></a>Ambiente
DevTest Labs, um ambiente refere-se tooa coleção de recursos do Azure em um laboratório. [Esta postagem de blog](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/) discute como ambientes de várias VMs toocreate de seus modelos do Gerenciador de recursos do Azure.

## <a name="base-images"></a>Imagens base
Imagens de base são imagens VM com todas as ferramentas de saudação e configurações pré-instalado e configurado tooquickly criar uma máquina virtual. Você pode provisionar uma VM escolhendo uma base existente e adicionando um artefato tooinstall seu agente de teste. Você pode, em seguida, salve Olá provisionado VM como uma base de dados de forma que hello base pode ser usada sem a necessidade de agente de teste de saudação tooreinstall para cada configuração de VM hello.

## <a name="artifacts"></a>Artefatos
Artefatos são usado toodeploy e configurar seu aplicativo depois que uma VM é provisionada. Os artefatos podem ser:

* Ferramentas que você deseja tooinstall em Olá VM - como agentes, Fiddler e Visual Studio.
* Ações que você deseja toorun em Olá VM - como clonar um repositório.
* Aplicativos que você deseja tootest.

Artefatos de [do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) arquivos JSON que contêm a implantação de tooperform instruções e aplicam a configuração.

## <a name="artifact-repositories"></a>Repositórios de artefatos
Repositórios de artefatos são repositórios git nos quais os artefatos são verificados. Repositórios de artefato podem ser adicionados toomultiple labs em sua organização, permitindo a reutilização e compartilhamento.

## <a name="formulas"></a>Fórmulas
Fórmulas em imagens de toobase adição, fornecem um mecanismo para provisionamento rápido de máquina virtual. Uma fórmula em DevTest Labs é uma lista de toocreate usados os valores de propriedade padrão um laboratório de VM.
Com fórmulas, VMs com hello mesmo conjunto de propriedades, como a imagem base, tamanho VM, rede virtual e artefatos - pode ser criado sem a necessidade de toospecify as propriedades de cada vez. Ao criar uma máquina virtual de uma fórmula, os valores padrão de saudação podem ser usados como-é ou modificado.

## <a name="policies"></a>Políticas
Políticas ajudam no controle de custos em seu laboratório. Por exemplo, você pode criar um tooautomatically política desligar VMs com base em um agendamento definido.

## <a name="caps"></a>Limites
Caps é mecanismo toominimize perda no laboratório. Por exemplo, você pode definir um número de saudação do cap toorestrict de máquinas virtuais que podem ser criados por usuário ou em um laboratório.

## <a name="security-levels"></a>Níveis de segurança
O acesso de segurança é determinado pelo RBAC (controle de acesso baseado em função) do Azure. toounderstand acessar como funciona, ele ajuda a toounderstand Olá diferenças uma permissão, a função e um escopo conforme definido pelo RBAC.

* Permissão - uma permissão é uma ação de específico de tooa (máquinas virtuais de acesso de leitura, por exemplo, tooall) de acesso definidas.
* Função – uma função é um conjunto de permissões que podem ser agrupados e tooa usuário atribuído. Por exemplo, Olá *proprietário da assinatura* função tem acesso tooall recursos dentro de uma assinatura.
* Escopo - um escopo é um nível na hierarquia de saudação de um recurso do Azure, como um grupo de recursos, um laboratório único ou a assinatura inteira Olá.

No escopo de saudação do DevTest Labs, há dois tipos de permissões de usuário toodefine funções: usuário de laboratório e de proprietário de laboratório.

* Proprietário do laboratório - um proprietário de laboratório tem os recursos de tooany de acesso no laboratório de saudação. Portanto, o proprietário de um laboratório pode modificar políticas, ler e gravar todas as máquinas virtuais, altere a rede virtual Olá e assim por diante.
* Usuário de laboratório – um usuário de laboratório pode exibir todos os recursos de laboratório, como VMs, políticas e redes virtuais, mas não pode modificar políticas ou as VMs criadas por outros usuários.

toosee como funções personalizadas toocreate DevTest Labs, consulte o artigo toohello, [conceder permissões de usuário políticas de laboratório toospecific](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Como os escopos são hierárquicos, quando um usuário tem permissões em um determinado escopo, ele recebe essas permissões automaticamente em cada escopo de nível inferior que está englobado. Por exemplo, se um usuário está atribuído toohello do proprietário da assinatura, eles têm recursos tooall acesso em uma assinatura, que incluem todas as máquinas virtuais, todas as redes virtuais e todos os laboratórios. Portanto, um proprietário da assinatura herda automaticamente a função hello do proprietário do laboratório. No entanto, Olá oposta não é true. O proprietário de um laboratório tem laboratório tooa de acesso, que é um escopo de menor nível de assinatura de saudação. Portanto, um proprietário de laboratório não será capaz de toosee máquinas de virtuais ou redes virtuais ou todos os recursos que estão fora do laboratório de saudação.

## <a name="azure-resource-manager-templates"></a>Modelos do Gerenciador de Recursos do Azure
Todos Olá conceitos abordados neste artigo podem ser configurados usando modelos do Azure Resource Manager, que lhe permitem definem Olá infraestrutura/de configuração de sua solução do Azure e repetidamente implantação-lo em um estado consistente.

[Entender a estrutura de saudação e a sintaxe de modelos do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format) descreve Olá estrutura de um Gerenciador de recursos do Azure modelo e hello as propriedades que estão disponíveis em diferentes seções Olá de um modelo.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Próximas etapas
[Criar um laboratório no DevTest Labs](devtest-lab-create-lab.md)
