---
title: "problemas de aaaResolve de licenças para um grupo no Active Directory do Azure | Microsoft Docs"
description: "Tooidentify e resolver licenciar problemas de atribuição quando você estiver usando o licenciamento baseado em grupo do Active Directory do Azure"
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
ms.openlocfilehash: ec9c74214a9e246f21fcf767b0bbd586ae702445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a>Identificar e resolver problemas de atribuição de licenças para um grupo no Azure Active Directory

Licenciamento baseado em grupo no Azure Active Directory (AD do Azure) apresenta o conceito de saudação de usuários em um estado de erro de licenciamento. Neste artigo, explicamos motivos Olá por que os usuários podem acabar nesse estado.

Quando você atribuir licenças diretamente tooindividual usuários, sem usar o licenciamento baseado em grupo, a operação de atribuição de saudação poderá falhar. Por exemplo, quando você executa o cmdlet do PowerShell Olá `Set-MsolUserLicense` em um usuário, Olá cmdlet pode falhar por vários motivos que estão relacionadas toobusiness lógica. Por exemplo, pode haver um número insuficiente de licenças ou um conflito entre dois planos de serviço que não pode ser atribuído a saudação mesmo tempo. Olá problema é imediatamente relatado fazer tooyou.

Quando você estiver usando o grupo com base em licenciamento, Olá mesmo erros podem ocorrer, mas eles ocorrem em plano de hello quando Olá serviço AD do Azure é atribuir licenças. Por esse motivo, os erros de saudação não podem ser comunicada tooyou imediatamente. Em vez disso, eles são registrados no objeto de usuário hello e, então, relatados por meio do portal administrativo hello. Observe que o usuário de Olá Olá original toolicense intenção nunca é perdido, mas é registrado em um estado de erro para investigação futura e resolução.

## <a name="how-toofind-license-assignment-errors"></a>Como o erro de atribuição de licença toofind

1. usuários de toofind em um estado de erro em um grupo específico, a folha de saudação aberta para o grupo de saudação. Em **Licenças**, uma notificação será exibida se houver usuários em um estado de erro.

![Grupo, notificação de erro](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. Clique em Olá notificação tooopen uma lista de todos os usuários afetados. Você pode clicar em cada usuário individualmente toosee mais detalhes.

![Grupo, lista de usuários em estado de erro](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. toofind todos os grupos que contêm pelo menos um erro em Olá **Active Directory do Azure** selecione folha **licenças** e **visão geral**. Uma caixa de informações é exibida quando alguns grupos exigem sua atenção.

![Visão geral, informações sobre grupos em estado de erro](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. Clique em Olá caixa toosee uma lista de todos os grupos com erros. Você pode clicar em cada grupo para obter mais detalhes.

![Visão geral, lista de grupos com erros](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


Abaixo está uma descrição de cada tooresolve de maneira hello e problema potencial-lo.

## <a name="not-enough-licenses"></a>Não há licenças suficientes

**Problema:** licenças suficientes disponíveis para um dos produtos de saudação que é especificado no grupo de saudação não existem. Você precisa tooeither comprar mais licenças de produto hello, ou liberar as licenças não usadas de outros usuários ou grupos.

toosee quantas licenças estão disponíveis, visite muito**Active Directory do Azure** > **licenças** > **todos os produtos**.

toosee quais usuários e grupos que está consumindo licenças, clique em um produto. Em **Usuários licenciados**, você verá todos os usuários que tiveram licenças atribuídas diretamente ou por meio de um ou mais grupos. Em **Grupos licenciados**, você verá todos os grupos que têm esse produto atribuído.

**PowerShell:** os cmdlets do PowerShell reportam esse erro como _CountViolation_.

## <a name="conflicting-service-plans"></a>Planos de serviço conflitante

**Problema:** um dos produtos de saudação que é especificado no grupo de saudação contém um plano de serviço que está em conflito com outro plano de serviço que já está atribuído toohello usuário por meio de um produto diferente. Alguns planos de serviço são configurados de forma que eles não podem ser atribuídos toohello mesmo usuário conforme outro plano de serviço relacionado.

Considere Olá exemplo a seguir. Um usuário tem uma licença para o Office 365 Enterprise **E1** atribuído diretamente, com todos os planos de saudação habilitados. Olá usuário foi adicionado tooa grupo que tem Olá Office 365 Enterprise **E3** tooit produto atribuído. Este produto contém planos de serviço que não podem se sobrepor com planos de saudação incluídos em E1, para que atribuição de licença do grupo Olá falhará com hello erro "Conflitante planos de serviço". Neste exemplo, planos de serviço Olá conflitantes são:

-   SharePoint Online (plano 2) está em conflito com o SharePoint Online (plano 1).
-   O Exchange Online (plano 2) está em conflito com o Exchange Online (plano 1).

toosolve este conflito, você precisa toodisable esses dois planos em Olá E1 de licença que usuário de toohello atribuído diretamente. Ou, você precisa de atribuição de licença toomodify Olá todo o grupo e desabilitar planos Olá na licença de E3 hello. Como alternativa, você pode decidir licença de E1 tooremove saudação do usuário Olá se ela é redundante no contexto de saudação da licença do hello E3.

decisão de saudação sobre como tooresolve conflitantes licenças de produtos sempre pertence toohello administrador. O Azure AD não resolve conflitos de licença automaticamente.

**PowerShell:** os cmdlets do PowerShell reportam esse erro como _MutuallyExclusiveViolation_.

## <a name="other-products-depend-on-this-license"></a>Outros produtos dependem desta licença

**Problema:** um dos produtos de saudação que é especificado no grupo de saudação contém um plano de serviço deve ser habilitado para outro plano de serviço, em outro produto, a função. Esse erro ocorre quando o AD do Azure tenta plano do serviço tooremove Olá subjacente. Por exemplo, isso pode acontecer como resultado de usuário hello está sendo removido do grupo de saudação.

toosolve esse problema, você precisará toomake-se de que esse plano necessário Olá ainda estiver atribuído toousers por meio de algum outro método, ou que os serviços dependentes Olá estão desabilitados para esses usuários. Depois de fazer isso, você pode remover corretamente licença de grupo Olá desses usuários.

**PowerShell:** os cmdlets do PowerShell reportam esse erro como _DependencyViolation_.

## <a name="usage-location-isnt-allowed"></a>O local de uso não é permitido

**Problema:** alguns serviços da Microsoft não estão disponíveis em todos os locais devido a leis e regulamentações locais. Antes de atribuir um usuário de tooa de licença, você tem toospecify hello "Local de uso" propriedade usuário hello. Você pode fazer isso em Olá **usuário** > **perfil** > **configurações** seção Olá portal do Azure.

Quando o AD do Azure tenta tooassign um grupo licença tooa usuário cujo local de uso não é suportado, ele falhará e registre esse erro no usuário hello.

toosolve esse problema, remover usuários locais sem suporte do grupo Olá licenciado. Como alternativa, se valores de local de uso atuais Olá não representam o local do usuário real hello, você pode modificá-las para que licenças Olá corretamente são atribuídas a próxima vez (se há suporte para o novo local de saudação).

**PowerShell:** os cmdlets do PowerShell reportam esse erro como _ProhibitedInUsageLocationViolation_.

> [!NOTE]
> Quando o Azure AD atribui licenças de grupo, todos os usuários sem um local de uso especificado herdam local de saudação do diretório de saudação. É recomendável que os administradores defina uso correto da saudação valores do local em usuários antes de usar toocomply licenciamento baseado em grupos com as leis e regulamentos locais.

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a>O que acontece quando há mais de uma licença de produto em um grupo?

Você pode atribuir mais de um grupo de tooa de licença de produto. Por exemplo, você pode atribuir o Office 365 Enterprise E3 e mobilidade corporativa + segurança tooa grupo tooeasily habilitar incluídos todos os serviços para os usuários.

O AD do Azure tenta tooassign todas as licenças que são especificadas em Olá grupo tooeach usuário. Se o AD do Azure não é possível atribuir um dos produtos Olá devido a problemas de lógica de negócios (por exemplo, se não há licenças suficientes para todos ou se houver conflitos com outros serviços que estão habilitados no usuário Olá), Olá não atribuir outras licenças no grupo de saudação a.

Você será Olá toosee capaz de falha de usuários que falha tooget atribuído e verificar quais produtos foram afetados por isso.

## <a name="license-assignment-fails-silently-for-a-user-due-tooduplicate-proxy-addresses-in-exchange-online"></a>Atribuição de licença silenciosamente falha por um usuário devido a endereços de proxy tooduplicate no Exchange Online

Se você estiver usando o Exchange Online, alguns usuários em seu locatário podem estar configurados incorretamente com hello mesmo valor de endereço de proxy. Quando o licenciamento baseado em grupo tenta tooassign toosuch uma licença um usuário, ele falhará e não registrará um erro (ao contrário de Olá outros casos de erro descritos acima) - Esta é uma limitação na versão de visualização Olá desse recurso e vamos tooaddress antes  *Disponibilidade geral*.

> [!TIP]
> Se você notar que alguns usuários não receberam uma licença e não há nenhum erro gravado nesses usuários, verifique primeiro se eles têm o endereço de proxy duplicado.
> Isso pode ser feito por meio da execução Olá seguinte cmdlet do PowerShell no Exchange Online:
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> [Este artigo](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) contém mais detalhes sobre esse problema, incluindo informações sobre [como tooExchange tooconnect Online usando o PowerShell remoto](https://technet.microsoft.com/library/jj984289.aspx).

Depois de solucionar problemas de proxy foram resolvidos para usuários Olá afetado, verifique se licença tooforce processamento Olá grupo toomake-se de licenças agora podem ser aplicadas novamente.

## <a name="how-do-you-force-license-processing-in-a-group-tooresolve-errors"></a>Como forçar o processamento em erros de tooresolve um grupo de licença?

Dependendo de quais etapas você já tomou tooresolve erros, talvez seja necessário toomanually processamento de gatilho de estado de usuário do grupo tooupdate hello.

Por exemplo, se você liberou algumas licenças Removendo atribuições de licença direto de usuários, será necessário tootrigger processamento de grupos que previamente falhou na licença toofully todos os membros de usuário. toodo que encontrar a folha de grupo hello, abra **licenças**e selecione hello **reprocessar** botão na barra de ferramentas de saudação.

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre outros cenários de gerenciamento de licenças por meio de grupos, consulte o seguinte hello:

* [Atribuir licenças tooa grupo no Active Directory do Azure](active-directory-licensing-group-assignment-azure-portal.md)
* [O que é o licenciamento baseado em grupo no Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Como indivíduo toomigrate licenciado usuários licenciamento no Azure Active Directory com base em toogroup](active-directory-licensing-group-migration-azure-portal.md)
* [Cenários adicionais de licenciamento baseado em grupo do Azure Active Directory](active-directory-licensing-group-advanced.md)
