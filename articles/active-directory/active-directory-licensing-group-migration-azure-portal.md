---
title: "toomigrate aaaHow tooa seus usuários licenciados individuais de grupo no Active Directory do Azure | Microsoft Docs"
description: "Como tooswitch de usuário individual licenças licenciamento baseado em toogroup usando o Active Directory do Azure"
services: active-directory
keywords: Licenciamento do AD do Azure
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 25e5c760b7e632ba71edde10d937fe580aa6ed35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-licensed-users-tooa-group-for-licensing-in-azure-active-directory"></a>Como tooadd licenciado grupo tooa de usuários para licenciamento no Azure Active Directory

Você pode ter toousers existente de licenças implantadas em organizações Olá via "atribuição direta"; ou seja, usando scripts do PowerShell ou outras licenças de usuário individual do tooassign de ferramentas. Se você quiser toostart usando licenças de toomanage licenciamento baseado em grupos em sua organização, você precisará de uma migração plano tooseamlessly substituir as soluções existentes com licenciamento baseado em grupo.

Olá tookeep de coisa mais importante em mente é que você deve evitar uma situação onde migrando licenciamento baseado em toogroup resultará em usuários temporariamente perder suas licenças atribuídas no momento. Qualquer processo que pode resultar na remoção das licenças deve ser evitado tooremove risco de saudação de perder o acesso tooservices e seus dados de usuários.

## <a name="recommended-migration-process"></a>Processo de migração recomendado

1. Você tem a automação existente (por exemplo, PowerShell) gerenciando a atribuição e a remoção de licenças para usuários. Deixe-o em execução como está.

2. Criar um novo grupo de licença (ou decidir quais existente grupos toouse) e certifique-se de que todos os necessários os usuários são adicionados como membros.

3. Atribuir licenças Olá necessário toothose grupos; sua meta deve ser tooreflect Olá mesmo estado de licenciamento sua automação existentes (por exemplo, o PowerShell) está aplicando toothose usuários.

4. Verifique se que as licenças foram aplicados tooall usuários nesses grupos. Isso pode ser feito verificando o estado de processamento de saudação em cada grupo e verificando os Logs de auditoria.

  - Você pode identificar usuários individuais ao examinar os detalhes de suas licenças. Você verá que elas têm Olá mesmo licenças atribuídas "diretamente" e "herdado" de grupos.

  - Você pode executar um script do PowerShell muito[verificar como as licenças são atribuídas toousers](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).

  - Quando hello mesmo produto licença será atribuída toohello usuário diretamente ou através de um grupo, apenas uma licença é consumida por usuário hello. Portanto, não há licenças adicionais são tooperform necessária migração.

5. Verifique se nenhuma atribuição de licença falhou ao verificar cada grupo de usuários em estado de erro. Para saber mais, veja [Identificar e resolver problemas de licença para um grupo](active-directory-licensing-group-problem-resolution-azure-portal.md).

6. Considere a remoção de atribuições de direta original Olá; Talvez você queira toodo gradativamente, em "ondas", toomonitor Olá resultado em um subconjunto de usuários primeiro.

  Pode deixar Olá atribuições diretas originais em usuários, mas quando os usuários de saudação deixar seus grupos licenciados, eles ainda manterão licença original hello, que é possivelmente não deseja que você deseja.

## <a name="an-example"></a>Um exemplo

Temos uma organização com 1.000 usuários. Todos os usuários exigem licenças EMS (Enterprise Mobility + Security). 200 usuários estão em Olá departamento financeiro e exigem licenças do Office 365 Enterprise E3. Temos um script do PowerShell em execução no local, adicionando e removendo licenças de usuários à medida que eles vêm e vão. Queremos que o script de saudação tooreplace com licenciamento baseado em grupo para que licenças são gerenciadas automaticamente pelo AD do Azure.

Aqui está o processo de migração Olá pôde como:

1. Usando Olá atribuir portal do Azure Olá EMS licença toohello **todos os usuários** grupo no AD do Azure. Atribuir Olá E3 licença toohello **departamento financeiro** grupo que contém todos os usuários de saudação necessário.

2. Para cada grupo, confirme que a atribuição de licença foi concluída para todos os usuários. Folha de toohello vá para cada grupo, selecione **licenças**e verificar o status de processamento de saudação na parte superior de saudação do hello **licenças** folha.

  - Pesquisar para "alterações de licença mais recentes foram aplicadas tooall usuários" tooconfirm o processamento foi concluído.

  - Procure uma notificação na parte superior sobre quaisquer usuários para os quais as licenças talvez não tenham sido atribuídas com êxito. Nós não temos mais licenças para alguns usuários? Alguns usuários têm SKUs com licenças conflitantes que os impedem de herdar as licenças de grupo?

3. Ponto de verificação tooverify alguns usuários que têm Olá direto e licenças de grupo aplicadas. Folha de toohello vá para um usuário, selecione **licenças**e examinar o estado de saudação de licenças.

  - Este é o estado do usuário Olá esperado durante a migração:

      ![estado do usuário esperado](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  Isso confirma que Olá possui licenças diretas e herdadas. Podemos ver que **EMS** e **E3** estão atribuídas.

  - Selecione os detalhes de tooshow cada licença sobre serviços Olá habilitado. Isso pode ser usado toocheck se hello direto e grupo licenças habilitar mesmo planos de serviço para usuário Olá Olá exatamente.

      ![planos do serviço de aplicativo](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. Depois de confirmar que as licenças direta e de grupo são equivalentes, você poderá começar a remover as licenças diretas dos usuários. Você pode testar isso, removendo-os para usuários individuais no portal de saudação e, em seguida, executar toohave de scripts de automação-los removidos em massa. Aqui está um exemplo de hello mesmo usuário com licenças direto Olá removido por meio do portal hello. Observe que o estado da licença Olá permanece inalterado, mas não vemos atribuições diretas.

  ![licenças diretas removidas](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre outros cenários de gerenciamento de licenças por meio de grupos, ler

* [Atribuir licenças tooa grupo no Active Directory do Azure](active-directory-licensing-group-assignment-azure-portal.md)
* [O que é o licenciamento baseado em grupo no Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Identificar e resolver problemas de licença para um grupo no Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Cenários adicionais de licenciamento baseado em grupo do Azure Active Directory](active-directory-licensing-group-advanced.md)
