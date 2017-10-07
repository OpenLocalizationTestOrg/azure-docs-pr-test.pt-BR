---
title: aaaUse Azure DevTest Labs para treinamento | Microsoft Docs
description: "Saiba como toouse Azure DevTest Labs para cenários de treinamento."
services: devtest-lab,virtual-machines
documentationcenter: na
author: steved0x
manager: douge
editor: 
ms.assetid: 57ff4e30-7e33-453f-9867-e19b3fdb9fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: sdanie
ms.openlocfilehash: 4a5f44a282d8f6a58849c730ff89237ccff39ca8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-training"></a>Usar o Azure DevTest Labs para treinamento
Azure DevTest Labs pode ser usado tooimplement muitos cenários de chave em adição toodev/teste. Um desses cenários é tooset um laboratório para treinamento. DevTest Labs do Azure permite que você toocreate um laboratório em que você pode fornecer modelos personalizados que cada estagiário pode usar ambientes idênticos e isolado de toocreate para treinamento. Você pode aplicar políticas tooensure que ambientes de treinamento são estagiário tooeach disponível somente quando precisar deles e contêm recursos suficientes - como máquinas virtuais – necessários para treinamento hello. Por fim, você pode compartilhar facilmente laboratório Olá com estagiários, o que eles podem acessar em um único clique.

![Usar o DevTest Labs para treinamento](./media/devtest-lab-training-lab/devtest-lab-training.png)

Azure DevTest Labs atende Olá requisitos de treinamento necessário tooconduct em qualquer ambiente virtual a seguir: 

* Os estagiários não conseguem ver VMs criadas por outros estagiários
* Todas as máquinas de treinamento devem ser idênticas
* Os estagiários podem provisionar seus ambientes de treinamento rapidamente
* Controlar os custos, garantindo que estagiários não é possível obter VMs mais do que o necessário para treinamento hello e também o desligamento de máquinas virtuais quando eles não estiverem usando
* Compartilhe facilmente o laboratório de treinamento Olá com cada estagiário
* Reutilizar o laboratório de treinamento Olá repetidamente

Neste artigo, você aprenderá sobre vários recursos do Azure DevTest Labs que podem ser usados toomeet Olá descrito anteriormente requisitos de treinamento e etapas detalhadas que você pode seguir tooset um laboratório para treinamento.  

## <a name="implementing-training-with-azure-devtest-labs"></a>Implementação de treinamento com Azure DevTest Labs
1. **Criar um laboratório de saudação** 
   
    Laboratórios são Olá ponto de partida no Azure DevTest Labs. Depois de criar um laboratório, você pode executar tarefas tais como adicionar laboratório toohello de usuários (estagiários), definir políticas toocontrol custos, definem imagens da VM que podem criar rapidamente e muito mais.   
   
    Saiba mais, basta clicar em links Olá Olá a tabela a seguir:
   
   | Tarefa | O que você aprenderá |
   | --- | --- |
   | [Criar Laboratórios de Desenvolvimento/Teste do Azure](devtest-lab-create-lab.md) |Saiba como toocreate um laboratório no Azure DevTest Labs em Olá portal do Azure. |
2. **Criar VMs de treinamento em minutos usando imagens prontas do marketplace e imagens personalizadas** 
   
    Você pode escolher imagens prontas de uma ampla variedade de imagens em hello Azure Marketplace e disponibilizá-las para estagiários Olá laboratório Olá. Se imagens prontas Olá não atenderem às suas necessidades, você pode criar uma imagem personalizada, criando um VM usando uma imagem pronta do Azure Marketplace, instalando todos os softwares de saudação que é necessário para treinamento hello e salvando Olá VM como imagem personalizada no laboratório de saudação do laboratório. 
   
    Saiba mais, basta clicar em links Olá Olá a tabela a seguir:
   
   | Tarefa | O que você aprenderá |
   | --- | --- |
   | [Configurar imagens do Marketplace](devtest-lab-configure-marketplace-images.md) |Saiba como é possível imagens do Azure Marketplace de lista de permissões; Tornar disponível para seleção única Olá imagens você deseja para treinamento hello. |
   | [Criar uma imagem personalizada](devtest-lab-create-template.md) |Crie uma imagem personalizada, pré-instalando o software de saudação que é necessário para treinamento Olá para que estagiários podem criar rapidamente uma máquina virtual usando a imagem personalizada hello. |
3. **Criar modelos reutilizáveis para máquinas de treinamento** 
   
    Uma fórmula no Azure DevTest Labs é que uma lista de valores de propriedade padrão usadas toocreate uma VM. Você pode criar uma fórmula no laboratório Olá selecionando uma imagem, um tamanho VM (uma combinação de CPU e RAM) e uma rede virtual. Cada estagiário pode ver fórmula Olá laboratório hello e use-a como toocreate uma VM. 
   
    Saiba mais, basta clicar em links Olá Olá a tabela a seguir:
   
   | Tarefa | O que você aprenderá |
   | --- | --- |
   | [Gerenciar DevTest Labs fórmulas toocreate VMs](devtest-lab-manage-formulas.md) |Saiba como você pode criar uma fórmula selecionando uma imagem, um tamanho de VM (uma combinação de CPU e RAM) e uma rede virtual. |
4. **Controlar os custos**
   
    DevTest Labs do Azure permite que você tooset uma política Olá laboratório toospecify Olá número máximo de máquinas virtuais que podem ser criadas por um estagiário laboratório hello. 
   
    Se você estiver realizando o treinamento de vários dia e deseja toostop todas as VMs de saudação em um determinado período do dia hello e, em seguida, reiniciar automaticamente-los Olá dia a seguir, você pode facilmente fazer isso por desligamento automático configurando e auto-start políticas no laboratório de saudação. 
   
    Finalmente, ao treinamento ser concluído você pode excluir todas as VMs de saudação ao mesmo tempo, executando um único script do PowerShell. 
   
    Saiba mais, basta clicar em links Olá Olá a tabela a seguir:
   
   | Tarefa | O que você aprenderá |
   | --- | --- |
   | [Definir políticas de laboratório](devtest-lab-set-lab-policy.md) |Controlar os custos, definindo políticas de laboratório hello. |
   | [Excluir o laboratório de saudação todas as máquinas virtuais usando um script do PowerShell](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Exclua todos os laboratórios de saudação em uma única operação quando Olá treinamento ser concluído. |
5. **Laboratório de saudação do compartilhamento com cada estagiário**
   
    Os laboratórios podem ser acessados diretamente usando um link que você compartilha com seus estagiários. Seu estagiários mesmo sem toohave uma conta do Azure, desde que elas tenham uma [conta da Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account). Os estagiários não conseguem ver VMs criadas por outros estagiários.  
   
    Saiba mais, basta clicar em links Olá Olá a tabela a seguir:
   
   | Tarefa | O que você aprenderá |
   | --- | --- |
   | [Adicionar um laboratório de tooa estagiário no Azure DevTest Labs](devtest-lab-add-devtest-user.md) |Use o laboratório de treinamento do hello tooadd portal do Azure estagiários tooyour. |
   | [Adicionar o laboratório de toohello estagiários usando um script do PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Use o PowerShell tooautomate adicionando o laboratório de treinamento tooyour estagiários. |
   | [Obter um laboratório de toohello link](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Saiba como um laboratório pode ser acessado diretamente por meio de um hiperlink. |
6. **Reutilizar o laboratório Olá repetidamente** 
   
    Você pode automatizar a criação de laboratório, incluindo configurações personalizadas, criando um modelo do Gerenciador de recursos e usando laboratórios idênticos toocreate repetidamente. 
   
    Saiba mais, basta clicar em links Olá Olá a tabela a seguir:
   
   | Tarefa | O que você aprenderá |
   | --- | --- |
   | [Criar um laboratório usando um modelo do Resource Manager](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Crie laboratórios no Azure DevTest Labs usando modelos do Resource Manager. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

