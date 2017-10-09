---
title: aaaUse DevTest Labs do Azure para desenvolvedores | Microsoft Docs
description: "Saiba como toouse Azure DevTest Labs para cenários de desenvolvedor."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 22e070e5-3d1a-49fe-9d4c-5e07cb0b7fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: tarcher
ms.openlocfilehash: 16a3ef47c9fcbca3050dd50db5b472a9a1e3c62c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a>Usar o Azure DevTest Labs para desenvolvedores
Azure DevTest Labs pode ser usado tooimplement muitos cenários de chave, mas um dos principais cenários de saudação envolve o uso de computadores de desenvolvimento do DevTest Labs toohost para desenvolvedores. Neste cenário, o DevTest Labs oferece estes benefícios:

- Os desenvolvedores podem provisionar rapidamente seus computadores de desenvolvimento sob demanda.
- Os desenvolvedores podem personalizar facilmente seus computadores de desenvolvimento sempre que for necessário.
- Os administradores podem controlar os custos garantindo que:
  - Os desenvolvedores não podem utilizar mais VMs do que o necessário para o desenvolvimento.
  - As VMs ficam fechadas quando não estão em uso. 

![Usar o DevTest Labs para treinamento](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

Neste artigo, você aprenderá sobre vários recursos do Azure DevTest Labs que podem ser usados toomeet requisitos de desenvolvedor e Olá etapas detalhadas que você pode seguir tooset um laboratório.

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a>Implementando ambientes de desenvolvedor com o Azure DevTest Labs
1. **Criar um laboratório de saudação** 
   
    Laboratórios são Olá ponto de partida no Azure DevTest Labs. Depois de criar um laboratório, você pode executar tarefas como a adição de laboratório de toohello usuários (desenvolvedores), custos de toocontrol de políticas de configuração, definindo imagens da VM que podem criar rapidamente e muito mais.  
   
    Saiba mais, basta clicar em links Olá Olá a tabela a seguir:
   
   | Tarefa | O que você aprenderá |
   | --- | --- |
   | [Criar Laboratórios de Desenvolvimento/Teste do Azure](devtest-lab-create-lab.md) |Saiba como toocreate um laboratório no Azure DevTest Labs em Olá portal do Azure. |
2. **Criar VMs em minutos usando imagens prontas do marketplace e imagens personalizadas** 
   
    Você pode escolher imagens prontas de uma ampla variedade de imagens em hello Azure Marketplace e disponibilizá-los no laboratório de saudação. Se imagens prontas Olá não atenderem às suas necessidades, você pode criar uma imagem personalizada, criando um VM usando uma imagem pronta do Azure Marketplace, instalar todos os softwares de saudação que você precisa, e salvando hello VM como uma imagem personalizada no laboratório de saudação do laboratório.

    Se você estiver usando imagens personalizadas, considere o uso de um toocreate da fábrica de imagem e distribuir as imagens. Uma fábrica de imagem é uma solução de configuração como código que normalmente cria e distribui suas imagens configuradas automaticamente. Este toomanually de tempo necessário Olá salva configurar o sistema de saudação depois que uma máquina virtual foi criada com hello base do sistema operacional.
  
    Saiba mais, basta clicar em links Olá Olá a tabela a seguir:
   
   | Tarefa | O que você aprenderá |
   | --- | --- |
   | [Configurar imagens do Marketplace](devtest-lab-configure-marketplace-images.md) |Saiba como é possível lista branca imagens do Azure Marketplace, tornando disponível para seleção única Olá imagens desejado para os desenvolvedores de saudação.|
   | [Criar uma imagem personalizada](devtest-lab-create-template.md) |Crie uma imagem personalizada, pré-instalando o software de saudação que é necessário para que os desenvolvedores podem criar rapidamente uma máquina virtual usando a imagem personalizada hello.|
   | [Saiba mais sobre a fábrica de imagem](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |Assista a um vídeo que descreve como tooset up e use uma imagem de fábrica.|

3. **Criar modelos reutilizáveis para máquinas de desenvolvedor** 
   
    Uma fórmula no Azure DevTest Labs é que uma lista de valores de propriedade padrão usadas toocreate uma VM. Você pode criar uma fórmula no laboratório Olá selecionando uma imagem, um tamanho VM (uma combinação de CPU e RAM) e uma rede virtual. Cada desenvolvedor pode ver fórmula Olá laboratório hello e use-a como toocreate uma VM. 
   
    Saiba mais, basta clicar em links Olá Olá a tabela a seguir:
   
   | Tarefa | O que você aprenderá |
   | --- | --- |
   | [Gerenciar DevTest Labs fórmulas toocreate VMs](devtest-lab-manage-formulas.md) |Saiba como você pode criar uma fórmula selecionando uma imagem, um tamanho de VM (uma combinação de CPU e RAM) e uma rede virtual.|

4. **Criar artefatos tooenable flexível VM personalização**

   Artefatos são usado toodeploy e configurar seu aplicativo depois que uma VM é provisionada. Os artefatos podem ser:

   - Ferramentas que você deseja tooinstall em Olá VM - como agentes, Fiddler e Visual Studio.
   - Ações que você deseja toorun em Olá VM - como clonar um repositório.
   - Aplicativos que você deseja tootest.

   Muitos artefatos já estão disponíveis prontos. Você pode criar seus próprios artefatos personalizados se quiser mais personalização para suas necessidades específicas.

   Saiba mais, basta clicar em links Olá Olá a tabela a seguir:
   
   | Tarefa | O que você aprenderá |
   | --- | --- |
   | [Criar artefatos personalizados para suas VM dos Laboratórios de Desenvolvimento/Teste](devtest-lab-artifact-author.md) |Crie seus próprio artefatos personalizados para máquinas virtuais de saudação no laboratório.|
   | [Adicionar um artefatos do Git repositório toostore personalizados e modelos do Gerenciador de recursos do Azure para usar no Azure DevTest Labs](devtest-lab-add-artifact-repo.md) |Saiba como toostore seus artefatos personalizados em seu próprio repositório Git particular.|

5. **Controlar os custos**
   
    DevTest Labs do Azure permite que você tooset uma política Olá laboratório toospecify Olá número máximo de máquinas virtuais que podem ser criadas por um desenvolvedor em laboratório hello. 
   
    Se sua equipe de desenvolvedor tem um conjunto a agenda de trabalho e você deseja toostop todas as VMs de saudação em um determinado período do dia hello e, em seguida, automaticamente reiniciá-los Olá após o dia, você pode fazer isso facilmente pelas políticas de desligamento automático e o início automático definindo laboratório hello. 
   
    Finalmente, quando o desenvolvimento de aplicativos for concluído, você pode excluir todas as VMs de saudação ao mesmo tempo, executando um único script do PowerShell. 
   
    Saiba mais, basta clicar em links Olá Olá a tabela a seguir:
   
   | Tarefa | O que você aprenderá |
   | --- | --- |
   | [Definir políticas de laboratório](devtest-lab-set-lab-policy.md) |Controlar os custos, definindo políticas de laboratório hello. |
   | [Excluir o laboratório de saudação todas as máquinas virtuais usando um script do PowerShell](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Exclua todos os laboratórios de saudação em uma única operação quando o desenvolvimento é concluído.|

1. **Adicionar uma tooa de rede virtual VM** 
   
    O DevTest Labs cria uma nova rede virtual (VNET) sempre que um laboratório for criado. Se você configurou sua rede virtual – por exemplo, usando o rota expressa ou VPN site a site – você pode adicionar configurações de rede virtual do laboratório de tooyour essa rede virtual para que ele esteja disponível quando criar máquinas virtuais.

    Além disso, há um artefato de junção de domínio Active Directory do Azure disponível que serão ingressar em um domínio de tooa VM quando Olá VM está sendo criado. 
   
    Saiba mais, basta clicar em links Olá Olá a tabela a seguir:
   
   | Tarefa | O que você aprenderá |
   | --- | --- |
   | [Configurar uma rede virtual no Azure DevTest Labs](devtest-lab-configure-vnet.md) |Saiba como tooconfigure uma rede virtual no Azure DevTest Labs usando Olá portal do Azure.|

6. **Laboratório de saudação do compartilhamento com cada desenvolvedor**
   
    Os laboratórios podem ser acessados diretamente usando um link que você compartilha com seus desenvolvedores. Eles não ainda tem toohave uma conta do Azure, desde que elas tenham uma [conta da Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account). Os desenvolvedores não conseguem ver VMs criadas por outros desenvolvedores.  
   
    Saiba mais, basta clicar em links Olá Olá a tabela a seguir:
   
   | Tarefa | O que você aprenderá |
   | --- | --- |
   | [Adicionar um laboratório de tooa do desenvolvedor no Azure DevTest Labs](devtest-lab-add-devtest-user.md) |Use laboratório de tooyour de desenvolvedores Olá tooadd portal do Azure.|
   | [Adicionar o laboratório de toohello desenvolvedores usando um script do PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Use o PowerShell tooautomate adicionando o laboratório de tooyour de desenvolvedores. |
   | [Obter um laboratório de toohello link](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Saiba como os desenvolvedores podem acessar diretamente um laboratório por meio de um hiperlink.|

7. **Automatizar a criação de laboratório para mais equipes** 
   
    Você pode automatizar a criação de laboratório, incluindo configurações personalizadas, criando um modelo do Gerenciador de recursos e usando laboratórios idênticos toocreate repetidamente. 
   
    Saiba mais, basta clicar em links Olá Olá a tabela a seguir:
   
   | Tarefa | O que você aprenderá |
   | --- | --- |
   | [Criar um laboratório usando um modelo do Resource Manager](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Crie laboratórios no Azure DevTest Labs usando modelos do Resource Manager. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

