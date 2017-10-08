---
title: "aaaManage conta de automação do Azure | Microsoft Docs"
description: "Este artigo descreve como toomanage Olá a configuração de sua conta de automação, como uma configuração incorreta, a exclusão e a renovação de certificados."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a>Como gerenciar uma conta de Automação do Azure
Em algum momento antes de sua conta de automação expira, você precisará toorenew Olá certificado. Se você acredita que Olá conta executar como foi comprometida, você pode excluir e recriá-la. Esta seção discute como tooperform essas operações.

## <a name="self-signed-certificate-renewal"></a>Renovação do certificado autoassinado
Olá o certificado autoassinado que você criou para a conta executar como de saudação expira um ano da data de saudação da criação. Você pode renová-lo a qualquer momento antes que ele expire. Quando você renová-la, o certificado de válido atual Olá é retido tooensure que todos os runbooks que são enfileiradas até ou ativamente em execução e que pode autenticar com hello conta executar como, não são afetados negativamente. certificado Olá permanece válido até a data de expiração.

> [!NOTE]
> Se você tiver configurado seu toouse de conta executar como automação um certificado emitido por sua autoridade de certificação corporativa e você usar essa opção, o certificado corporativo de saudação será substituído por um certificado autoassinado.

Olá toorenew do certificado, Olá a seguir:

1. No portal do Azure de Olá, abra conta de automação de saudação.

2. Em Olá **conta de automação** folha em Olá **propriedades de conta** painel, em **configurações de conta**, selecione **contas executar como**.

    ![Painel de propriedades da conta de Automação](media/automation-manage-account/automation-account-properties-pane.png)
3. Em Olá **contas executar como** folha de propriedades, selecione qualquer Olá executado como conta ou Olá clássico conta executar como que você deseja toorenew Olá certificado para.

4. Em Olá **propriedades** folha para Olá selecionada conta, clique em **Renovar certificado**.

    ![Renovar o certificado da conta Executar como](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. Enquanto o certificado hello está sendo renovado, você pode acompanhar o progresso de saudação em **notificações** menu hello.

## <a name="delete-a-run-as-or-classic-run-as-account"></a>Excluir uma conta Executar como ou Executar como Clássica
Esta seção descreve como toodelete e crie novamente uma conta executar como ou clássico executar como. Ao executar esta ação, Olá conta de automação é mantida. Depois de excluir uma conta executar como ou clássico executar como, você poderá recriá-la em Olá portal do Azure.

1. No portal do Azure de Olá, abra conta de automação de saudação.

2. Em Olá **conta de automação** folha, no painel de propriedades da conta hello, selecione **contas executar como**.

3. Em Olá **contas executar como** folha de propriedades, selecione qualquer Olá executado como conta ou clássico executar como da conta que você deseja toodelete. Em seguida, na Olá **propriedades** folha para Olá selecionada conta, clique em **excluir**.

 ![Excluir Conta Executar como](media/automation-manage-account/automation-account-delete-runas.png)

4. Enquanto a conta de hello está sendo excluída, você pode acompanhar o progresso de saudação em **notificações** menu hello.

5. Após a exclusão de conta hello, você pode criá-lo novamente no hello **contas executar como** opção de criação de folha de propriedades selecionando Olá **Azure conta executar como**.

 ![Recriar Olá automação executar como conta](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a>Configuração incorreta
Alguns itens de configuração necessárias para toofunction de conta executar como ou clássico executar como Olá corretamente podem foram excluídos ou incorretamente criados durante a instalação inicial. Olá itens incluem:

* Ativo de certificado
* Ativo de conexão
* Conta executar como foi removida da função de Colaborador Olá
* Entidade de serviço ou aplicativo no Azure AD

Olá anterior e outras instâncias de uma configuração incorreta, Olá conta de automação detecta Olá altera e exibe o status de *incompleta* em Olá **contas executar como** folha de propriedades para Olá conta.

![Status incompleto de configuração de conta Executar como](media/automation-manage-account/automation-account-runas-incomplete-config.png)

Quando você selecionar a conta executar como do hello, Olá conta **propriedades** painel exibe o saudação a seguinte mensagem de erro:

![Mensagem de aviso incompleto da configuração da conta Executar como](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png).

Rapidamente, você pode resolver esses problemas de conta executar como, excluindo e recriando conta hello.

## <a name="next-steps"></a>Próximas etapas
* Para obter mais informações sobre entidades de serviço, consulte muito[objetos Application e entidade de serviço](../active-directory/active-directory-application-objects.md).
* Para obter mais informações sobre o controle de acesso baseado em função na automação do Azure, consulte muito[controle de acesso baseado em função no Azure Automation](automation-role-based-access-control.md).
* Para obter mais informações sobre certificados e serviços do Azure, consulte muito[visão geral de certificados para serviços de nuvem do Azure](../cloud-services/cloud-services-certs-create.md).
