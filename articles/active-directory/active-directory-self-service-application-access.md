---
title: "acesso de aplicativo de serviço aaaSelf e gerenciamento delegado com o Active Directory do Azure | Microsoft Docs"
description: Este artigo descreve como acessar o aplicativo de autoatendimento tooenable e gerenciamento de delegado com o Active Directory do Azure.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 448a7fe8-a162-475e-9ba2-2e3ab59302bc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: asmalser
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 90bec3bd71796f22a782929b028db0d18c3aa1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-application-access-and-delegated-management-with-azure-active-directory"></a>Acesso a aplicativos de autoatendimento e gerenciamento delegado com o Active Directory do Azure
A habilitação de recursos de autoatendimento para usuários finais é um cenário comum para TI empresarial. Muitos usuários, muitos aplicativos e Olá pessoa acesso de toomake best-informed concedem decisões não podem ser o administrador do diretório hello. Geralmente Olá melhor pessoa toodecide quem pode acessar um aplicativo é um líder ou outro administrador delegado. No entanto, é Olá usuário usa o aplicativo hello e Olá sabe o que precisam toodo capaz de toobe seu trabalho.

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo. 

O acesso ao aplicativo de autoatendimento é um recurso de licenciamento P1 e P2 do [Azure Active Directory Premium](https://azure.microsoft.com/trial/get-started-active-directory/) que permite aos administradores do diretório:

* Habilitar o acesso do usuários toorequest tooapplications usando um "obter mais aplicativos" lado a lado no hello [painel de acesso do AD do Azure](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)
* Definir para quais aplicativos os usuários podem solicitar acesso
* Definir se uma aprovação é necessária para os usuários toobe poderá tooself-atribuir acesso tooan aplicativo
* Conjunto de quem deve aprovar solicitações de saudação e gerenciar o acesso para cada aplicativo

Atualmente esse recurso tem suporte para todos os aplicativos pré-integrados e personalizados que oferecem suporte a federados ou com base em senha de logon único no hello [Galeria de aplicativos do Active Directory do Azure](https://azure.microsoft.com/marketplace/active-directory/all/), incluindo aplicativos como o Salesforce, Dropbox, Google Apps e muito mais.
Este artigo descreve como:

* Configurar acesso de aplicativo de autoatendimento para usuários finais, incluindo a configuração de um fluxo de trabalho de aprovação opcional 
* Delegar o gerenciamento de acesso para as pessoas mais apropriados de toohello aplicativos específicos na sua organização e habilitá-las em solicitações de acesso tooapprove do painel de acesso de Olá AD do Azure toouse, atribuir acesso diretamente tooselected usuários ou definir (opcionalmente) credenciais para acesso a aplicativos quando é configurado com base em senha de logon único

## <a name="configuring-self-service-application-access"></a>Configurando acesso ao aplicativo de autoatendimento
acesso de aplicativo de autoatendimento tooenable e configurado os aplicativos que podem ser adicionados ou solicitados pelos usuários finais, siga estas instruções.

1. O logon no hello [portal clássico do Azure](https://manage.windowsazure.com/).

2.   Em Olá **do Active Directory** seção, selecione seu diretório, em seguida Olá **aplicativos** guia. 

3. Selecione Olá **adicionar** botão, usar Olá Galeria opção tooselect e adicionar um aplicativo.

4. Depois que seu aplicativo tiver sido adicionado, você obterá a página de início rápido de aplicativo hello. Clique em **configurar logon único**, selecione Olá desejado único modo de logon e salvar a configuração de saudação. 

5. Em seguida, selecione Olá **configurar** guia tooenable usuários toorequest acesso toothis aplicativo de painel de acesso de saudação do AD do Azure, defina **permitir o acesso do aplicativo de autoatendimento** muito**Sim**.
  
  ![][1]

6. toooptionally configurar um fluxo de trabalho de aprovação para solicitações de acesso, definir **exigir aprovação antes de conceder acesso** muito**Sim**. E um ou mais aprovadores podem ser selecionados Olá **aprovadores** botão.

  Um aprovador pode ser qualquer usuário na organização Olá com uma conta do AD do Azure e pode ser responsável pela conta de provisionamento, licenciamento, ou qualquer outro processo de negócios exige que sua organização antes de conceder acesso tooan aplicativo. aprovador Olá pode até mesmo ser proprietário do grupo de saudação de um ou mais grupos conta compartilhados e pode atribuir Olá usuários tooone desses toogive grupos a eles acesso por meio de uma conta compartilhada. 

  Se nenhuma aprovação for necessária, o usuários obtém instantaneamente painel de acesso do hello aplicativo tootheir adicionado do AD do Azure. Se o aplicativo hello configurado para [provisionamento de usuário automático](active-directory-saas-app-provisioning.md), ou foi configurado [modo SSO de senha "gerenciada pelo usuário"](active-directory-appssoaccess-whatis.md#password-based-single-sign-on), usuário Olá já deve ter um usuário de conta e saber a senha de saudação.

7. Se o aplicativo hello tiver sido configurado toouse com base em senha de logon único, em seguida, uma opção para permitir o aprovador Olá credenciais de SSO Olá tooset em nome de cada usuário também está disponível. Para obter mais informações, consulte a seção Olá em [gerenciamento de acesso delegado](#delegated-application-access-management).

8. Por fim, Olá **grupo para usuários Self-Assigned** mostra Olá nome do grupo de saudação que é usado toostore Olá que os usuários tenham sido concedidos ou acesso toohello aplicativo atribuídos. aprovador de acesso de saudação se torna o proprietário de saudação desse grupo. Se o nome do grupo de saudação mostrado não existir, ele será criado automaticamente. Opcionalmente o nome do grupo de saudação pode ser definido toohello nome de um grupo existente.

9. configuração de saudação toosave, clique em **salvar** na parte inferior da saudação da tela hello. Agora os usuários podem toorequest acesso toothis aplicativo de painel de acesso de saudação.

10. experiência do usuário final tootry Olá, entrar no painel de acesso do AD do Azure da sua organização no https://myapps.microsoft.com, preferencialmente usando uma conta diferente que não seja um aprovador de aplicativo. 

11. Em Olá **aplicativos** , clique em Olá **obter mais aplicativos** lado a lado. Este bloco exibe uma galeria de todos os aplicativos de saudação que foram habilitados para acesso ao aplicativo de autoatendimento no diretório hello, com hello capacidade toosearch e filtrar por categoria de aplicativo hello esquerda. 

12. Clicar em um aplicativo inicia o processo de solicitação de saudação. Se nenhum processo de aprovação é necessário, o aplicativo hello será adicionado imediatamente em Olá **aplicativos** guia após um curto confirmação. Se for necessária uma aprovação, você verá uma caixa de diálogo indicando isso e aprovadores toohello é enviado um email. Você deve entrar em Olá o painel de acesso como um aprovador não toosee esse processo de solicitação.

13. email Olá direciona Olá aprovador toosign no painel de acesso do AD do Azure hello e aprovar a solicitação de saudação. Depois de saudação solicitação for aprovada (e quaisquer processos especiais que você definir foram executados pelo aprovador Olá), o hello usuário vê aplicativo hello aparecem em seus **aplicativos** guia em que ele podem entrar.

## <a name="delegated-application-access-management"></a>Gerenciamento de acesso delegado ao aplicativo
Um aprovador de acesso do aplicativo pode ser qualquer usuário em sua organização que é hello mais apropriado pessoa tooapprove ou negar acesso toohello aplicativo em questão. Este usuário pode ser responsável pela conta de provisionamento, licenciamento, ou qualquer outro processo de negócios exige que sua organização antes de conceder acesso tooan aplicativo.

Ao configurar o acesso do aplicativo de autoatendimento descrito acima, qualquer aplicativo atribuído aprovadores consulte adicional **gerenciar aplicativos** lado a lado no painel de acesso de saudação do AD do Azure, que mostra quais são os aplicativos administrador de acesso Olá para. Clicar em um aplicativo mostra uma tela com várias opções.

![][2]

### <a name="approve-requests"></a>Aprovar solicitações
Olá **aprovar solicitações** lado a lado permite que os aprovadores toosee pendentes aprovações toothat específico aplicativo e guia de aprovações toohello redirecionamentos onde Olá solicita podem ser confirmado ou negado. aprovador Olá também receberá emails automatizados sempre que uma solicitação é criada que instrui o toodo.

### <a name="add-users"></a>Adicionar Usuários
Olá **adicionar usuários** lado a lado permite que os aprovadores toodirectly grant selecionado aos usuários acesso toohello aplicativo. Ao clicar nesse bloco, o aprovador Olá vê uma caixa de diálogo permite que eles tooview e pesquisa por usuários em seu diretório. Adicionando um usuário resulta no aplicativo hello sendo mostrado em painéis de acesso desses usuários do AD do Azure ou Office 365. Se qualquer processo de provisionamento manual do usuário é necessária no aplicativo hello antes que o usuário de saudação é capaz de toosign em, aprovador Olá deve executar esse processo antes de atribuir acesso.  

### <a name="manage-users"></a>Gerenciar Usuários
Olá **gerenciar usuários** lado a lado permite aprovadores toodirectly atualizar ou remover os usuários que têm acesso toohello aplicativo. 

### <a name="configure-password-sso-credentials-if-applicable"></a>Configurar credenciais de SSO de senha (se aplicável)
Olá **configurar** lado a lado é mostrada apenas se configurado pelo Olá IT administrador toouse baseada em senha logon único no aplicativo hello e administrador Olá concedidas aprovador Olá credenciais de SSO de senha do hello capacidade tooset conforme descrito anteriormente. Quando selecionado, Olá aprovador é apresentado com várias opções para como credenciais de saudação são propagadas tooassigned usuários:

![][3]

* **Usuários entrar com suas próprias senhas** – nesse modo, os usuários de saudação atribuído sabem o que seus nomes de usuário e senhas são para o aplicativo hello e são solicitada tooentê-los em seu primeiro aplicativo de entrada toohello. Olá cenário corresponde caso SSO de senha toohello onde hello [usuários gerenciam credenciais](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Os usuários sejam desconectados automaticamente usando contas separadas que gerenciar** – neste modo, os usuários de Olá atribuído não são necessária tooenter ou conhecer suas credenciais específicas do aplicativo ao entrar no aplicativo hello. Em vez disso, o aprovador Olá define credenciais Olá para cada usuário depois de atribuir acesso usando Olá **adicionar usuário** lado a lado. Quando o usuário Olá clica no aplicativo hello no seu painel de acesso ou o Office 365, que sejam desconectados automaticamente usando as credenciais de saudação definidas pelo aprovador hello. Olá cenário corresponde caso SSO de senha toohello onde hello [administradores gerenciam as credenciais](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Os usuários sejam desconectados automaticamente usando uma única conta que gerenciar** -um caso especial, nesse caso é toouse apropriada quando todos os usuários atribuídos precisarem toobe acesso usando uma única conta compartilhada. caso de uso mais comum Olá para esse recurso é com aplicativos de mídia social, onde uma organização tem uma conta única "company" e vários usuários precisam toomake atualizações toothat conta. Olá cenário também corresponde caso SSO de senha toohello onde hello [administradores gerenciam as credenciais](active-directory-appssoaccess-whatis.md#password-based-single-sign-on). No entanto, depois de selecionar essa opção, aprovador Olá será solicitada tooenter Olá usuário e a senha conta compartilhada única de saudação. Depois de concluído, todos os usuários atribuídos são conectados usando essa conta ao clicar em um aplicativo hello em seus painéis de acesso do AD do Azure ou Office 365.

## <a name="additional-resources"></a>Recursos adicionais
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)

<!--Image references-->
[1]: ./media/active-directory-self-service-application-access/ssaa_admin.PNG
[2]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app.PNG
[3]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app_config.PNG
