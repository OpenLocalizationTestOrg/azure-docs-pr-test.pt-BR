---
title: "aaaLicense usuários no Active Directory do Azure | Microsoft Docs"
description: "Saiba como toolicense por conta própria e os usuários no Active Directory do Azure."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: ae0bc030fa02b79d1dd01ca961b4e96e6b9c470d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-license-users-in-azure-active-directory"></a>Início rápido: Licenciar usuários no Azure Active Directory
Os Serviços do Azure AD baseados em licença funcionam por meio da ativação da assinatura do Azure AD (Azure Active Directory) em seu locatário do Azure. Depois Olá assinatura estiver ativa, recursos de serviço são gerenciados por administradores do AD do Azure e usados por usuários licenciados. Quando você comprar o Enterprise Mobility + Security, Azure AD Premium ou Azure AD Basic, seu locatário será atualizado com assinatura hello, incluindo o período de validade e pago licenças. As informações de assinatura, incluindo o número de saudação de licenças atribuídas ou disponíveis, estão disponíveis por meio de saudação do Azure portal em **Active Directory do Azure** por abrindo Olá **licenças** lado a lado. Olá **licenças** folha também é Olá melhor toomanage de local de suas atribuições de licença.

Embora a obtenção de uma assinatura é que tudo o que você precisa tooconfigure paga recursos, você ainda deve atribuir licenças de usuário pago do AD do Azure recursos pagos. Qualquer usuário que deve ter acesso ou é gerenciado por meio de um recurso pago do Azure AD deve ter uma licença atribuída. Uma atribuição de licença é um mapeamento entre um usuário e um serviço comprado, como o Azure AD Premium, Básico ou o Enterprise Mobility + Security.

Você pode usar [atribuição de licença baseada em grupo](active-directory-licensing-whatis-azure-portal.md) tooset as regras, como a seguir hello:
* Todos os usuários em seu diretório obtêm automaticamente uma licença
* Todos com o título do trabalho apropriado Olá obtém uma licença
* Você pode delegar gerenciadores de tooother decisão Olá na organização da saudação (usando [grupos de autoatendimento](active-directory-accessmanagement-self-service-group-management.md))

> [!TIP]
> Para obter uma discussão detalhada da toogroups de atribuição de licença, incluindo avançados de cenários e Office 365 licenciamento cenários, consulte [atribuir licenças toousers pela associação de grupo no Active Directory do Azure](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="assign-licenses-toousers-and-groups"></a>Atribuir grupos e toousers de licenças
Usando uma assinatura ativa, primeiro você deve atribuir uma licença tooyourself e atualize seu tooensure de navegador que você vê todos os recursos de saudação esperado incluídos com a sua assinatura. Olá próxima etapa é tooassign usuários de toohello de licenças que precisam de recursos do access toopaid AD do Azure. Licenças de tooassign uma maneira fácil é tooassign toogroups de licenças de usuários em vez de tooindividuals. Quando você atribui licenças tooa grupo, todos os membros do grupo recebem uma licença. Se os usuários são adicionados ou removidos do grupo Olá, licença adequada Olá é automaticamente atribuída ou removida. 

> [!NOTE]
> Alguns serviços da Microsoft não estão disponíveis em todos os locais. Usuário tooa possa ser atribuídos uma licença, o administrador de saudação deve especificar Olá **local de uso** propriedade para o usuário hello. Você pode definir essa propriedade em **usuário** &gt; **perfil** &gt; **configurações** no hello portal do Azure. Ao usar a atribuição de grupo de licenças, qualquer usuário cujo uso local não for especificado herda local de saudação do diretório de saudação.

tooassign uma licença, em **Active Directory do Azure** &gt; **licenças** &gt; **todos os produtos**, selecione um ou mais produtos e, em seguida, selecione **Atribuir** na barra de comandos de saudação.

![Selecione um tooassign de licença](media/license-users-groups/select-license-to-assign.png)

Você pode usar o hello **usuários e grupos** toochoose folha planos de vários usuários ou grupos ou serviço toodisable produto hello. Use caixa de pesquisa Olá toosearch superior para nomes de usuário e grupo.

![Selecione um usuário ou grupo para atribuição de licença](media/license-users-groups/select-user-for-license-assignment.png)

Quando você atribui licenças tooa grupo, pode levar algum tempo até que todos os usuários herdam licença Olá dependendo do tamanho de saudação do grupo de saudação. Você pode verificar o status de processamento Olá Olá **grupo** folha sob Olá **licenças** lado a lado.

![Status de atribuição de licença](media/license-users-groups/license-assignment-status.png)

Erros de atribuição podem ocorrer durante a atribuição de licença do Azure AD, mas são relativamente raros ao gerenciar os produtos do Azure AD e do Enterprise Mobility + Security. Os possíveis erros de atribuição estão limitados a:
- Conflito de atribuição: quando um usuário foi anteriormente atribuído uma licença que é incompatível com a licença atual hello. Nesse caso, a atribuição de licença nova Olá requer a remoção de saudação atual.
- Excedido licenças disponíveis: quando o número de saudação de usuários em grupos atribuídos excede licenças disponíveis Olá, status de atribuição do usuário reflete tooassign uma falha devido toomissing licenças.

### <a name="azure-ad-b2b-collaboration-licensing"></a>Licenciamento da colaboração B2B do Azure AD

Colaboração B2B permite tooinvite convidados em seus serviços de tooAzure AD de acesso do AD do Azure locatário tooprovide e todos os recursos do Azure você disponibilizar.  

Não há nenhuma taxa para convidar usuários B2B e atribuindo-lhes tooan aplicativo no AD do Azure. Backup too10 aplicativos por convidado 3 relatórios básicos e o usuário também são gratuitos para usuários de colaboração B2B. Se o usuário convidado tem as licenças apropriadas atribuídas no locatário do AD do Azure do parceiro Olá, eles serão ser licenciados também nas suas.

Não é obrigatório, mas se você deseja que os recursos do tooprovide acesso toopaid AD do Azure, os usuários de convidado B2B devem ser licenciados com adequado licenças do AD do Azure. Um locatário convidar com paga a licença do AD do Azure pode atribuir direitos de usuário de colaboração B2B tooan adicionais cinco usuários de convidado convidados toohello locatário. Para obter informações e cenários, consulte [Diretrizes de licenciamento de colaboração B2B](active-directory-b2b-licensing.md).

## <a name="view-assigned-licenses"></a>Exibir licenças atribuídas

É mostrada uma exibição resumida de licenças disponíveis e atribuídas no **Azure Active Directory** &gt; **Licenças** &gt; **Todos os produtos**.

![Exibir resumo da licença](media/license-users-groups/view-license-summary.png)

Uma lista detalhada de usuários e grupos atribuídos está disponível ao selecionar um produto específico. Olá **usuários licenciados** lista mostra todos os usuários atualmente consumindo uma licença e se o hello licença foi atribuída diretamente toohello usuário ou se ela é herdada de um grupo.

![Exibir detalhes da licença](media/license-users-groups/view-license-detail.png)

Da mesma forma, Olá **licenciado grupos** lista mostra todos os grupos de licenças toowhich foram atribuídas. Selecione uma saudação de usuário ou grupo tooopen **licenças** folha, que mostra todas as licenças atribuídas toothat objeto.

## <a name="remove-a-license"></a>Remover uma licença

tooremove uma licença, vá toohello usuário ou grupo e abra Olá **licenças** lado a lado. Selecione Olá licença e, em seguida, clique em **remover**.

![Remover uma licença](media/license-users-groups/remove-license.png)

Herdado por usuário Olá de um grupo de licenças não podem ser removidas diretamente. Em vez disso, remova usuário de saudação do grupo de saudação do qual eles são herdadas licença hello.


## <a name="next-steps"></a>Próximas etapas
Este guia de início rápido, você aprendeu como tooassign licenças toousers e grupos no diretório do AD do Azure. 

Você pode usar o hello seguindo as atribuições de licença de assinatura do link tooconfigure no AD do Azure da saudação portal do Azure.

> [!div class="nextstepaction"]
> [Atribuir licenças do Azure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Overview) 