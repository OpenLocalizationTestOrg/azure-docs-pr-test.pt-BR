---
title: "aaaPermissions na Central de segurança do Azure | Microsoft Docs"
description: "Este artigo explica como a Central de segurança do Azure usa toousers de permissões de tooassign de controle de acesso baseado em função e identifica Olá permitido ações para cada função."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a>Permissões na Central de Segurança do Azure

Central de segurança do Azure usa [controle de acesso baseado em função (RBAC)](../active-directory/role-based-access-control-configure.md), que fornece [funções internas](../active-directory/role-based-access-built-in-roles.md) que podem ser atribuídos toousers, grupos e serviços no Azure.

Central de segurança avalia a configuração de saudação de vulnerabilidades e problemas de segurança de tooidentify de recursos. Na Central de segurança, você ver apenas as informações relacionadas tooa recurso quando foi atribuída a função de saudação do leitor, colaborador ou proprietário para Olá assinatura ou grupo de recursos que o recurso pertence.

Funções de toothese adição, há duas funções específicas da Central de segurança:

* **Leitor de segurança**: um usuário que pertence a função toothis tem direitos tooSecurity Centro de exibição. usuário Olá pode exibir as recomendações, alertas, uma política de segurança e estados de segurança, mas não é possível fazer alterações.
* **Administrador de segurança**: um usuário que pertence a função toothis Olá mesmo direitos como Olá leitor de segurança e pode também atualizar a política de segurança hello e ignorar alertas e recomendações.

> [!NOTE]
> funções de segurança Hello, leitor de segurança e o administrador de segurança, tem acesso somente na Central de segurança. funções de segurança de saudação não tem acesso tooother áreas de serviço do Azure como armazenamento, Web e móveis ou Internet das coisas.
>
>

## <a name="roles-and-allowed-actions"></a>Funções e ações permitidas

Olá tabela a seguir exibe as funções e ações permitidas na Central de segurança. Um X indica que a ação de saudação é permitida para essa função.

| Função | Editar política de segurança | Aplicar as recomendações de segurança a um recurso | Ignorar alertas e recomendações | Exibir alertas e recomendações |
|:--- |:---:|:---:|:---:|:---:|
| Proprietário da assinatura | X | X | X | X |
| Colaborador da assinatura | X | X | X | X |
| Proprietário do Grupo de Recursos | -- | X | -- | X |
| Colaborador do Grupo de Recursos | -- | X | -- | X |
| Leitor | -- | -- | -- | X |
| Administrador de segurança | X | -- | X | X |
| Leitor de segurança | -- | -- | -- | X |

> [!NOTE]
> É recomendável que você atribua Olá função menos permissiva necessários para os usuários toocomplete suas tarefas. Por exemplo, atribua Olá leitor função toousers que precisam apenas informações de tooview sobre a integridade da segurança Olá de um recurso, mas não tome uma ação, como aplicar recomendações ou edição de políticas.
>
>

## <a name="next-steps"></a>Próximas etapas
Este artigo explicou como a Central de segurança usa RBAC tooassign permissões toousers e identificado Olá permitido ações para cada função. Agora que você está familiarizado com as atribuições de função hello necessário toomonitor Olá estado de segurança de sua assinatura, editar políticas de segurança e aplicar recomendações, saiba como:

- [Configurar políticas de segurança na Central de Segurança do Azure](security-center-policies.md)
- [Gerenciando recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md)
- [Monitorar a integridade da segurança Olá de seus recursos do Azure](security-center-monitoring.md)
- [Gerenciar e responder a alertas toosecurity na Central de segurança](security-center-managing-and-responding-alerts.md)
- [Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) (Monitorando soluções de parceiros com a Central de Segurança do Azure)
