---
title: aaaGet iniciado com licenciamento no Active Directory do Azure | Microsoft Docs
description: "Como Active Directory do Azure funciona o licenciamento, como tooget iniciado com as práticas recomendadas"
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
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 268dab806b8b959790341d630a0355c6a43871d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="license-yourself-and-your-users-in-azure-active-directory"></a>Licenciar a si mesmo e seus usuários no Azure Active Directory

> [!div class="op_single_selector"]
> * [Instruções do Portal do Azure](active-directory-licensing-get-started-azure-portal.md)
> * [Informações sobre como obter o portal clássico do Azure](active-directory-licensing-what-is.md)
>
>

O Azure AD (Azure Active Directory) é uma solução e plataforma de identidade como um serviço (IDaaS) da Microsoft. O Azure AD é oferecido em edições de serviço diferentes:

* O Azure Active Directory Gratuito, que está disponível em qualquer serviço da Microsoft, como Office 365, Dynamics, Microsoft Intune ou Azure. O Azure AD não gera nenhum encargo de consumo nesse modo.

* Edições pagas do Azure AD, como:
  - Enterprise Mobility + Security 
  - Azure AD Premium (P1 e P2)
  - AD Basic do Azure
  - Autenticação Multifator do Azure

Como muitos serviços online da Microsoft, a maioria das versões pagas do AD do Azure é fornecida por meio de direitos de usuário, como é no Office 365, Microsoft Intune e AD do Azure. Nesses casos, compra do serviço de saudação é representada por uma ou mais assinaturas, e cada assinatura inclui algumas licenças prepurchased em seu locatário. Os direitos por usuário são obtidos ao:

* Atribuir uma licença. 
* Criar um vínculo entre o usuário hello e produto hello.
* Habilitar Olá componentes de serviço para usuário hello.
* Consumindo uma saudação pago licenças.

[Experimente o Azure AD Premium agora.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

Para obter uma visão geral ampla dos recursos de serviço do Azure AD, confira [O que é o Azure AD?](active-directory-whatis.md). Para obter mais informações, veja nossa [página de Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/).

> [!NOTE]
> Assinatura paga pelo uso do Azure permite a criação de recursos do Azure e mapeá-los tooyour de pagamento. Não há nenhum contagens de licença associadas à assinatura hello. Quando você concede que uma toooperate de permissão de usuário nos recursos do Azure mapeada toohello assinatura, eles estão associados a assinatura de saudação e podem gerenciar os recursos de assinatura.

## <a name="how-does-azure-active-directory-licensing-work"></a>Como funciona a licença do Azure Active Directory?

Os serviços do Azure AD baseados em licença funcionam ao ativar uma assinatura no locatário de serviço do Azure AD. Após Olá assinatura estiver ativa, recursos de serviço de saudação são gerenciados por administradores do AD do Azure e usados por usuários licenciados.

### <a name="manage-subscription-information"></a>Gerenciamento de informações da assinatura

Quando você comprar o Enterprise Mobility + Security, Azure AD Premium ou Azure AD Basic, seu locatário será atualizado com assinatura hello, incluindo o período de validade e pago licenças. As informações de assinatura, incluindo o número de saudação de licenças atribuídas ou disponíveis, estão disponíveis por meio do portal do Azure de saudação: em **Active Directory do Azure**, abra Olá **licenças** bloco Olá diretório específico. Olá **licenças** folha também é Olá melhor toomanage de local de suas atribuições de licença.

Cada assinatura consiste em um ou mais planos de serviço, como o Azure AD, Autenticação Multifator, Intune, Exchange Online ou SharePoint Online.  O gerenciamento de licença do Azure AD *não* requer gerenciamento de nível de plano de serviço. O Office 365 é diferente porque ele se baseia nos serviços de tooincluded configuração avançada modo toomanage acesso. AD do Azure se baseia em recursos de tooenable de configuração em funcionamento e gerenciar permissões individuais.

> [!IMPORTANT]
> O Azure AD Premium, Azure AD Basic e mobilidade corporativa + assinaturas de segurança são tootheir confinado provisionado/locatário do diretório. As assinaturas não podem ser divididas entre diretórios ou usuários tooentitle usada em outros diretórios. É possível mover uma assinatura entre diretórios, mas requer o envio de um tíquete de suporte ou cancelamento e nova compra para compras diretas.
>
> Quando o AD do Azure ou Enterprise Mobility + Security adquiridas por meio de uma assinatura de licenciamento por Volume, e quando o contrato de saudação inclui outros serviços Online da Microsoft (por exemplo, Office 365), a ativação ocorre automaticamente. 

### <a name="assign-licenses"></a>Atribuir licenças

Embora a obtenção de uma assinatura é que tudo o que você precisa tooconfigure paga recursos, você deve distribuir ainda licenças do AD do Azure paga toousers de recursos. Qualquer usuário que deve ter tooor de acesso que é gerenciado por meio do AD do Azure paga o recurso deve ser atribuído uma licença. Uma atribuição de licença é um mapeamento entre um usuário e um serviço comprado, como o Azure AD Premium, Básico ou o Enterprise Mobility + Security.


O gerenciamento de usuários, em seu diretório, que devem ter uma licença pode ser obtido ao: 

* Atribuir licenças toogroups em Olá [portal do Azure](active-directory-licensing-whatis-azure-portal.md).
* Atribuir licenças diretamente toousers por meio do portal de hello, PowerShell ou APIs. 

Durante a atribuição de grupo de tooa de licenças, todos os membros do grupo são atribuídos a uma licença. Se os usuários são adicionados ou removidos do grupo Olá, licença adequada Olá é atribuída ou removida. Atribuição de grupo pode utilizar qualquer tooyou disponíveis de gerenciamento de grupo e é consistente com a atribuição baseada em grupo tooapplications.

Você pode usar [atribuição de licença baseada em grupo](active-directory-licensing-whatis-azure-portal.md) tooset as regras, como a seguir hello:
* Todos os usuários em seu diretório obtêm automaticamente uma licença
* Todos com o título do trabalho apropriado Olá obtém uma licença
* Você pode delegar gerenciadores de tooother decisão Olá na organização da saudação (usando [grupos de autoatendimento](active-directory-accessmanagement-self-service-group-management.md))

Para obter uma discussão detalhada da toogroups de atribuição de licença, incluindo avançados de cenários e Office 365 licenciamento cenários, consulte [atribuir licenças toousers pela associação de grupo no Active Directory do Azure](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="get-started-with-azure-ad-licensing"></a>Introdução ao licenciamento do Azure AD

É fácil começar a usar o Azure AD. Você sempre pode criar seu diretório como parte de uma inscrição para uma [avaliação gratuita do Azure](https://azure.microsoft.com/offers/ms-azr-0044p/).

Olá práticas recomendadas a seguir podem ajudar a garantir que seu locatário está alinhado com outros serviços da Microsoft que você talvez esteja consumindo e suas metas de serviço hello:

- Se você já estiver usando qualquer um dos serviços de saudação organizacionais da Microsoft, você já tem um locatário do AD do Azure. É útil toouse Olá que mesmo locatário para outros serviços para que o gerenciamento de identidade de núcleo, incluindo o provisionamento e híbrida-logon único (SSO), pode ser usado em serviços de saudação. Com o logon único, os usuários se beneficiar de recursos avançados de saudação em serviços de saudação. Portanto, se você decidir toobuy um serviço pago do AD do Azure para sua força de trabalho, é recomendável que você use Olá mesmo locatário novamente.

- É recomendável que você use um novo locatário no portal do Azure de saudação se você estiver planejando:
  - Usar o Azure AD para um conjunto diferente de usuários (como parceiros ou clientes).
  - Avaliar os serviços do Azure AD isoladamente de seu serviço de produção.
  - Configurar um ambiente de área restrita para seus serviços.

  Olá novo diretório é criado com sua conta como um usuário externo com permissões de administrador global. Quando você entrar no toohello portal do Azure com essa conta, você pode ver este locatário e acessar todas as tarefas de administração.

> [!NOTE]
> O Azure AD dá suporte a "usuários convidados", que são contas de usuário em um locatário do Azure AD criadas usando uma conta da Microsoft ou uma identidade do Azure AD de outro locatário. portal de administração do Office 365 de saudação atualmente não dá suporte para esses usuários. Usuários convidados com contas da Microsoft não estão tooaccess capaz de portal de administração de saudação Office 365, enquanto usuários convidados de outros locatários do AD do Azure são ignorados. No último caso de Olá, Olá apenas a conta local do usuário no AD do Azure de saudação ou Locatário do Office 365 em que o usuário Olá foi criado originalmente, está acessível.

### <a name="select-one-or-more-license-trials"></a>Selecione uma ou mais avaliações de licença

É possível ativar uma assinatura de avaliação do Azure AD Premium ou do Enterprise Mobility + Security no **Azure Active Directory** &gt; **Início rápido**.

![Selecione uma versão de avaliação de licença](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

Licenças de avaliação estão disponíveis em Olá **licenças** folha.

### <a name="assign-licenses-toousers-and-groups"></a>Atribuir grupos e toousers de licenças

Após Olá assinatura estiver ativa, você deve atribuir uma licença tooyourself. Em seguida, atualize Olá tooensure de navegador que você está vendo todos os recursos de saudação. Olá próxima etapa é tooassign usuários de toohello de licenças que precisam de recursos do access toopaid AD do Azure. Conforme descrito em [atribuir licenças](#assign-licenses), uma maneira fácil de licenças tooassign é tooidentify Olá representando Olá desejado público e atribuir Olá tooit de licença. Dessa forma, os usuários que são adicionados ou removidos do grupo de saudação durante seu ciclo de vida são atribuídos ou removidos da licença hello, respectivamente.

> [!NOTE]
> Alguns serviços da Microsoft não estão disponíveis em todos os locais. Usuário tooa possa ser atribuídos uma licença, o administrador de saudação deve especificar Olá **local de uso** propriedade para o usuário hello. Você pode definir essa propriedade em **usuário** &gt; **perfil** &gt; **configurações** no hello portal do Azure. Ao usar a atribuição de grupo de licenças, qualquer usuário cujo uso local não for especificado herda local de saudação do diretório de saudação.

tooassign uma licença, em **Active Directory do Azure** &gt; **licenças** &gt; **todos os produtos**, selecione um ou mais produtos e, em seguida, selecione **Atribuir** na barra de comandos de saudação.

![Selecione um tooassign de licença](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

Você pode usar o hello **usuários e grupos** toochoose folha planos de vários usuários ou grupos ou serviço toodisable produto hello. Use caixa de pesquisa Olá toosearch superior para nomes de usuário e grupo.

![Selecione um usuário ou grupo para atribuição de licença](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

Quando você estiver atribuindo um grupo de licenças tooa, pode levar algum tempo até que todos os usuários herdam licença hello, dependendo do número de saudação de usuários no grupo de saudação. Você pode verificar o status de processamento Olá Olá **grupo** folha sob Olá **licenças** lado a lado.

![Status de atribuição de licença](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

Erros de atribuição podem ocorrer durante a atribuição de licença do Azure AD, mas são relativamente raros ao gerenciar os produtos do Azure AD e do Enterprise Mobility + Security. Os possíveis erros de atribuição estão limitados a:
- Conflito de atribuição: quando um usuário foi anteriormente atribuído uma licença que é incompatível com a licença atual hello. Nesse caso, a atribuição de licença nova Olá requer a remoção de saudação atual.
- Excedido licenças disponíveis: quando o número de saudação de usuários em grupos atribuídos excede licenças disponíveis Olá, status de atribuição do usuário reflete tooassign uma falha devido toomissing licenças.

#### <a name="azure-ad-b2b-collaboration-licensing"></a>Licenciamento da colaboração B2B do Azure AD

Colaboração B2B permite tooinvite convidados em seus serviços de tooAzure AD de acesso do AD do Azure locatário tooprovide e todos os recursos do Azure você disponibilizar.  

Não há nenhuma taxa para convidar usuários B2B e atribuindo-lhes tooan aplicativo no AD do Azure. Backup too10 aplicativos por convidado 3 relatórios básicos e o usuário também são gratuitos para usuários de colaboração B2B. Se o usuário convidado tem as licenças apropriadas atribuídas no locatário do AD do Azure do parceiro Olá, eles serão ser licenciados também nas suas.

Não é obrigatório, mas se você deseja que os recursos do tooprovide acesso toopaid AD do Azure, os usuários de convidado B2B devem ser licenciados com adequado licenças do AD do Azure. Um locatário convidar com paga a licença do AD do Azure pode atribuir direitos de usuário de colaboração B2B tooan adicionais cinco usuários de convidado convidados toohello locatário. Para obter informações e cenários, consulte [Diretrizes de licenciamento de colaboração B2B](active-directory-b2b-licensing.md).

### <a name="view-assigned-licenses"></a>Exibir licenças atribuídas

É mostrada uma exibição resumida de licenças disponíveis e atribuídas no **Azure Active Directory** &gt; **Licenças** &gt; **Todos os produtos**.

![Exibir resumo da licença](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

Uma lista detalhada de usuários e grupos atribuídos está disponível ao selecionar um produto específico. Olá **usuários licenciados** lista mostra todos os usuários atualmente consumindo uma licença e se o hello licença foi atribuída diretamente toohello usuário ou se ela é herdada de um grupo.

![Exibir detalhes da licença](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

Da mesma forma, Olá **licenciado grupos** lista mostra todos os grupos de licenças toowhich foram atribuídas. Selecione uma saudação de usuário ou grupo tooopen **licenças** folha, que mostra todas as licenças atribuídas toothat objeto.

### <a name="remove-a-license"></a>Remover uma licença

tooremove uma licença, vá toohello usuário ou grupo e abra Olá **licenças** lado a lado. Selecione Olá licença e, em seguida, clique em **remover**.

![Remover uma licença](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

Herdado por usuário Olá de um grupo de licenças não podem ser removidas diretamente. Em vez disso, remova usuário de saudação do grupo de saudação do qual eles são herdadas licença hello.

### <a name="extend-trials"></a>Estender avaliações

Extensões de avaliação para clientes que estão disponíveis como autoatendimento inscrição por meio do portal Olá Office 365. Um administrador do cliente pode acessar o portal do Office toohello (acesso depende das permissões para o portal do Office Olá) e selecione a avaliação do Azure AD Premium Olá. Olá clicando em **Estender avaliação** link inicia o processo de extensão de saudação. Um cartão de crédito é necessário, mas ele não é cobrado.

![Estender a avaliação de saudação portal do Azure](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre toolearn avançado cenários para o gerenciamento de licenças por meio de grupos, leia o artigo de saudação [grupo de tooa atribuindo licenças](active-directory-licensing-group-assignment-azure-portal.md).

Aqui está a obter informações sobre como tooconfigure e usar outros recursos pagos do AD do Azure:

* [Redefinição de senha de autoatendimento](active-directory-manage-passwords.md)
* [Gerenciamento de grupo de autoatendimento](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Autenticação Multifator do Azure](../multi-factor-authentication/multi-factor-authentication.md)
* [Compra direta de licenças do AD Premium do Azure](http://aka.ms/buyaadp)
