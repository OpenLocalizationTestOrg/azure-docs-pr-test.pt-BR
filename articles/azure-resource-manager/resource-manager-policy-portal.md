---
title: "portal de aaaAzure para políticas de recursos | Microsoft Docs"
description: "Descreve como toouse toocreate portal do Azure e gerenciar políticas de Gerenciador de recursos. Políticas podem ser aplicadas a grupos de assinatura ou o recurso de saudação."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a>Usar tooassign portal do Azure e gerenciar políticas de recursos
Olá portal do Azure permite que você tooassign políticas tooresource grupos de recursos e assinaturas. interface do usuário Olá torna fácil tooselect política de saudação que você deseja tooassign e especifica valores de parâmetro para configurações de política que política toocustomize hello. 

tooassign uma política por meio do portal hello, definição de política de saudação já deve existir em sua assinatura. Sua assinatura tem várias definições de políticas internas que estão prontas para você tooassign tooresource grupos ou assinaturas. Você verá essas políticas internas e as políticas personalizadas que você definiu usando Olá tooassign portal políticas. Para uma introdução toopolicies e como toodefine personalizada política, consulte [visão geral do recurso política](resource-manager-policy.md).

As políticas são herdadas por todos os recursos filho. Portanto, se uma política for aplicada tooa grupo de recursos, é aplicável tooall recursos de saudação desse grupo de recursos. Neste artigo, o termo de saudação **escopo** refere-se o grupo de recursos de toohello ou assinatura que é atribuída a política de saudação. 

Políticas são avaliadas durante a criação e atualização de recursos (PUT e operações de PATCHES).

## <a name="assign-a-policy"></a>Atribuir uma política

1. tooassign tooeither uma política um grupo de recursos ou assinatura, selecione esse grupo de recursos ou a assinatura. Em configurações de saudação, selecione **políticas**.

   ![selecionar políticas](./media/resource-manager-policy-portal/select-policies.png)

2. toocreate uma atribuição de diretiva para este escopo, selecione **Adicionar atribuição**.

   ![adicionar atribuição](./media/resource-manager-policy-portal/add-assignment.png)

3. Selecione a política de saudação tooassign desejado. Mesmo se você não adicionou nenhuma assinatura de tooyour de definições de política, você pode ver políticas internas de saudação que estão disponíveis para atribuição. Essas políticas internas abrangem vários cenários comuns.

   ![selecionar definição](./media/resource-manager-policy-portal/select-definition.png)

4. Depois de selecionar uma política, você pode ver uma descrição da política de saudação e os parâmetros para essa política. Por exemplo, hello imagem a seguir mostra Olá **permitido locais** parâmetro, que é necessário para a política de saudação que restringe os locais disponíveis Olá.

   ![mostrar parâmetros](./media/resource-manager-policy-portal/show-parameters.png)

5. Por meio da interface do usuário hello, selecione Olá toospecify de valores para parâmetros de política de saudação (como locais de saudação que podem ser usados para implantação).

   ![selecionar valores do parâmetro](./media/resource-manager-policy-portal/select-parameters.png)

6. Forneça valores para Olá outros parâmetros. escopo de saudação é atribuído automaticamente com base na folha de saudação selecionado ao iniciar a atribuição de diretiva de saudação. Selecione **OK** quando tiver concluído.

   ![definir parâmetros](./media/resource-manager-policy-portal/define-parameters.png)

  Você atribuiu uma política de saudação toohello especificado escopo.

## <a name="view-policy-assignments"></a>Exibir atribuições de política

Depois de atribuir uma política, você vê-lo na lista de saudação de políticas para esse escopo. Olá **detalhes** guia mostra um resumo da atribuição de política de saudação.

![mostrar detalhes](./media/resource-manager-policy-portal/show-details.png)

Olá **regra de atribuição** guia mostra hello JSON para definição de política de saudação.

![mostrar regra de atribuição](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a>Alterar uma atribuição de política existente

toochange uma política, selecione **Editar atribuição de** ou **excluir**

![editar ou excluir atribuição](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a>Atribuir políticas personalizadas

Se você tiver definido as políticas personalizadas em sua assinatura, essas políticas estão disponíveis para atribuição por meio do portal hello. Essas políticas são precedidas por **[Personalizada]**

![políticas personalizadas](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre a sintaxe do hello JSON para definir políticas, consulte [visão geral do recurso política](resource-manager-policy.md).
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).
* esquema de política de saudação é publicado em [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

