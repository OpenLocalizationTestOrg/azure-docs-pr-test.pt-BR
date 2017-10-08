---
title: "aaaManage acesso e permissões com RBAC - RBAC do Azure | Microsoft Docs"
description: "Introdução ao gerenciamento de acesso com controle de acesso baseado em função do Azure no hello Portal do Azure. Use permissões de tooassign de atribuições de função em seu diretório."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8f8aadeb-45c9-4d0e-af87-f1f79373e039
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 1c133b2b57b49d85f0e12a318c7997478e095fb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-role-based-access-control-in-hello-azure-portal"></a>Introdução ao controle de acesso baseado em função no hello portal do Azure
As empresas orientadas a segurança devem se concentrar em fornecendo aos funcionários permissões exatas de saudação que precisam. Número excessivo de permissões pode expor uma tooattackers de conta. Permissões insuficientes significa que os funcionários não podem ter seu trabalho feito com eficiência. O RBAC (controle de acesso baseado em função) do Azure ajuda a resolver esse problema ao oferecer o gerenciamento de acesso refinado para o Azure.

Usando o RBAC, você pode separar as tarefas dentro de sua equipe e conceder apenas Olá total acesso toousers que precisam tooperform seus trabalhos. Em vez de apresentar todos irrestrito permissões em sua assinatura do Azure ou recursos, você pode permitir apenas determinadas ações. Por exemplo, use RBAC toolet um funcionário gerenciar máquinas virtuais em uma assinatura, enquanto outro pode gerenciar bancos de dados SQL em Olá mesma assinatura.

## <a name="basics-of-access-management-in-azure"></a>Noções básicas de gerenciamento de acesso no Azure
Cada assinatura do Azure está associada com um diretório do Azure Active Directory (AD). Usuários, grupos e aplicativos do diretório podem gerenciar recursos no hello assinatura do Azure. Atribua esses direitos de acesso usando Olá portal do Azure, as ferramentas de linha de comando do Azure e APIs de gerenciamento do Azure.

Conceda acesso atribuindo Olá apropriado RBAC função toousers, grupos e aplicativos em um determinado escopo. escopo de saudação de uma atribuição de função pode ser uma assinatura, um grupo de recursos ou um único recurso. Uma função atribuída a um escopo pai também concede acesso toohello filhos contidos nele. Por exemplo, um usuário com o grupo de recursos do acesso tooa pode gerenciar todos os recursos de saudação contém, como sites, máquinas virtuais e sub-redes.

![Relação entre os elementos do Azure Active Directory - diagrama](./media/role-based-access-control-what-is/rbac_aad.png)

função RBAC Olá que você atribui determina quais recursos Olá usuário, grupo ou aplicativo pode gerenciar dentro desse escopo.

## <a name="built-in-roles"></a>Funções internas
RBAC do Azure tem três funções básicas que se aplicam a tipos de recurso de tooall:

* **Proprietário** tem acesso completo tooall recursos incluindo Olá toodelegate direito acesso tooothers.
* **Colaborador** pode criar e gerenciar todos os tipos de recursos do Azure, mas não é possível conceder acesso tooothers.
* **leitor** pode exibir os recursos existentes do Azure.

rest Olá das funções de RBAC hello Azure permitir o gerenciamento de recursos do Azure específicos. Por exemplo, hello função Colaborador da máquina Virtual permite Olá toocreate de usuário e gerenciar máquinas virtuais. Ele não oferece a eles acesso a rede virtual toohello ou sub-rede Olá Olá máquina virtual se conecta ao. 

[Funções internas de RBAC](role-based-access-built-in-roles.md) listas Olá funções disponíveis no Azure. Especifica operações hello e escopo de cada função interna concede toousers. Se você estiver procurando toodefine suas próprias funções para controlar ainda mais, consulte como toobuild [funções personalizadas no Azure RBAC](role-based-access-control-custom-roles.md).

## <a name="resource-hierarchy-and-access-inheritance"></a>Hierarquia de recursos e herança de acesso
* Cada **assinatura** no Azure pertence tooonly um diretório. (Porém, cada diretório pode ter mais de uma assinatura).
* Cada **grupo de recursos** pertence tooonly uma assinatura.
* Cada **recurso** pertence tooonly um grupo de recursos.

O acesso concedido em escopos pai é herdado em escopos filho. Por exemplo:

* Atribuir o grupo Olá leitor função tooan AD do Azure no escopo de assinatura de saudação. Olá membros desse grupo podem exibir cada grupo de recursos e recursos na assinatura de saudação.
* Atribuir o aplicativo tooan de função de Colaborador hello no escopo do grupo de recursos de saudação. Ele pode gerenciar recursos de todos os tipos nesse grupo de recursos, mas não de outros grupos de recursos na assinatura de saudação.

## <a name="azure-rbac-vs-classic-subscription-administrators"></a>RBAC do Azure versus administrador de assinatura clássico
Os administradores de assinatura clássico e coadministradores têm acesso completo toohello assinatura do Azure. Eles podem gerenciar recursos usando Olá [portal do Azure](https://portal.azure.com) com APIs do Gerenciador de recursos do Azure ou hello [portal clássico do Azure](https://manage.windowsazure.com) e o modelo de implantação clássico do Azure. No modelo RBAC hello, administradores clássicos atribuídos a função de proprietário de saudação no escopo de assinatura de saudação.

Somente Olá portal do Azure e Olá novo suporte a APIs do Gerenciador de recursos do Azure RBAC do Azure. Usuários e aplicativos que são atribuídos funções de RBAC não podem usar o portal de gerenciamento clássico hello e modelo de implantação clássico do Azure hello.

## <a name="authorization-for-management-vs-data-operations"></a>Autorização para o gerenciamento versus operações de dados
RBAC do Azure somente dá suporte a operações de gerenciamento de recursos do Azure de Olá Olá portal do Azure e APIs do Gerenciador de recursos do Azure. Ele não pode autorizar todas as operações no nível de dados para os recursos do Azure. Por exemplo, você pode autorizar alguém toomanage contas de armazenamento, mas não toohello blobs ou tabelas em uma conta de armazenamento. Da mesma forma, um banco de dados SQL pode ser gerenciado, mas não Olá tabelas dentro dele.

## <a name="next-steps"></a>Próximas etapas
* Introdução ao [controle de acesso baseado em função no portal do Azure de saudação](role-based-access-control-configure.md).
* Consulte Olá [funções internas de RBAC](role-based-access-built-in-roles.md)
* Defina suas próprias [Funções personalizadas no RBAC do Azure](role-based-access-control-custom-roles.md)
