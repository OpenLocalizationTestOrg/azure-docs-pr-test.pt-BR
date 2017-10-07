---
title: aaaAzure IoT Suite e do Active Directory do Azure | Microsoft Docs
description: "Descreve como o Azure IoT Suite usa permissões do Active Directory do Azure toomanage."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a>Permissões no site de azureiotsuite.com Olá

## <a name="what-happens-when-you-sign-in"></a>O que acontece quando você entra

Olá a primeira vez que você entrar no [azureiotsuite.com][lnk-azureiotsuite], site Olá determina os níveis de permissão Olá baseado em Olá atualmente selecionado locatário do Azure Active Directory (AAD) e o Azure assinatura.

1. Primeiro, toopopulate lista de saudação de locatários vistos próximo tooyour username, site Olá encontra do Azure que locatários do AAD você pertence. Atualmente, site Olá somente pode obter tokens de usuário para um locatário por vez. Portanto, quando você alternar locatários usando Olá suspensa no canto superior direito da saudação, site Olá efetua login tokens de saudação do toothat locatário tooobtain para esse locatário.

2. Em seguida, site Olá encontra do Azure quais assinaturas você associou à saudação selecionado locatário. Você verá assinaturas disponíveis hello quando você cria uma nova solução pré-configurada.

3. Finalmente, o site Olá recupera todos os recursos de saudação em assinaturas de saudação e grupos de recursos marcados como soluções pré-configuradas e preenche blocos Olá Olá home page.

Olá seções a seguir descreve funções hello que controlam o acesso toohello pré-configurado soluções.

## <a name="aad-roles"></a>Funções do AAD

funções AAD Olá Olá capacidade provisionar pré-configurado soluções de controle e gerenciar usuários em uma solução pré-configurada.

Saiba mais sobre funções de administrador no AAD em [Atribuir funções de administrador no Azure AD][lnk-aad-admin]. artigo atual Olá enfoca Olá **Administrador Global** e hello **usuário** soluções pré-configuradas de funções de diretório conforme é usado pelo hello.

### <a name="global-administrator"></a>Administrador global

Pode haver muitos administradores globais por locatário do AAD:

* Quando você cria um locatário do AAD, você está pelo administrador global do saudação padrão do locatário.
* administrador global Olá pode provisionar uma solução pré-configurada e é atribuído um **Admin** função para o aplicativo hello dentro de seu locatário do AAD.
* Se outro usuário Olá mesmo locatário do AAD cria um aplicativo, a função padrão de saudação é concedido de administrador global toohello **ReadOnly**.
* Um administrador global pode atribuir usuários tooroles para aplicativos que usam Olá [portal do Azure][lnk-portal].

### <a name="domain-user"></a>Usuário de domínio

Pode haver muitos usuários de domínio por locatário do AAD:

* Um usuário de domínio pode provisionar uma solução pré-configurada por meio de saudação [azureiotsuite.com] [ lnk-azureiotsuite] site. Por padrão, o usuário de domínio Olá é concedido Olá **Admin** função no hello provisionado o aplicativo.
* Um usuário de domínio pode criar um aplicativo usando o script de build.cmd Olá Olá [azure-iot-monitoramento remoto][lnk-rm-github-repo], [azure iot-previsão manutenção] [ lnk-pm-github-repo], ou [azure iot-conectado-fábrica] [ lnk-cf-github-repo] repositório. No entanto, a função padrão de saudação concedido toohello usuário de domínio é **ReadOnly**, porque um usuário de domínio não tem funções tooassign de permissão.
* Se outro usuário no locatário do AAD Olá cria um aplicativo, usuário de domínio Olá recebe Olá **ReadOnly** função por padrão para o aplicativo.
* O usuário de domínio não terá a capacidade de atribuir funções para aplicativos, portanto, não poderá adicionar usuários ou funções para usuários para um aplicativo, mesmo se o tiver provisionado.

### <a name="guest-user"></a>Usuário Convidado

Pode haver muitos usuários convidados por locatário do AAD. Usuários convidados têm um conjunto limitado de direitos no locatário do AAD hello. Como resultado, os usuários convidados não é possível provisionar uma solução pré-configurada no locatário do AAD hello.

Para obter mais informações sobre usuários e funções no AAD, consulte Olá recursos a seguir:

* [Criar usuários no Azure AD][lnk-create-edit-users]
* [Atribuir usuários tooapps][lnk-assign-app-roles]

## <a name="azure-subscription-administrator-roles"></a>Funções de administrador da assinatura do Azure

funções de administrador do Azure Olá controlam Olá capacidade toomap um locatário tooan AD de assinatura do Azure.

Saiba mais sobre as funções de administrador do Azure Olá artigo Olá [como tooadd ou alterar a conta de administrador, administrador de serviço e Coadministrador do Azure][lnk-admin-roles].

## <a name="application-roles"></a>Funções de aplicativo

funções de aplicativo Hello controlam acesso toodevices em sua solução pré-configurada.

Há duas funções definidas e uma função implícita definida em um aplicativo provisionado:

* **Administração:** tem controle total tooadd, remover dispositivos e modificar as configurações.
* **Somente Leitura:** pode exibir dispositivos, regras, ações, trabalhos e telemetria.

Você pode encontrar permissões Olá designado como tooeach no hello [RolePermissions.cs] [ lnk-resource-cs] arquivo de origem.

### <a name="changing-application-roles-for-a-user"></a>Alterando as funções de aplicativo para um usuário

Você pode usar o hello seguindo o procedimento toomake um usuário no Active Directory do administrador de sua solução pré-configurada.

Você deve ter funções de toochange AAD administrador global para um usuário:

1. Vá toohello [portal do Azure][lnk-portal].
2. Selecione **Azure Active Directory**.
3. Verifique se que você está usando diretório Olá escolhido em azureiotsuite.com quando você provisionou sua solução. Se você tiver vários diretórios associados à sua assinatura, você pode alternar entre eles, se você clicar no nome da conta na saudação de superior direita do portal de saudação.
4. Clique em **Aplicativos empresariais** e, em seguida, **Todos os aplicativos**.
4. Mostrar **Todos os aplicativos** com **Qualquer** status. Então pesquise um aplicativo com o nome da sua solução pré-configurada.
5. Clique em nome de saudação do aplicativo hello que coincide com o nome de solução pré-configurada.
6. Clique em **Usuários e grupos**.
7. Selecione o usuário a saudação ser tooswitch funções.
8. Clique em **atribuir** e selecione Olá função (como **Admin**) você gostaria que tooassign toohello usuário, clique em marca de seleção de saudação.

## <a name="faq"></a>Perguntas frequentes

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a>Sou um administrador de serviço e gostaria de mapeamento de diretório Olá toochange entre minha assinatura e um locatário do AAD específico. Como posso concluir esta tarefa?

1. Vá toohello [portal clássico do Azure][lnk-classic-portal], clique em **configurações** na lista de saudação de serviços no lado esquerdo da saudação.
2. Selecione a assinatura de saudação você gostaria que o mapeamento de diretório toochange Olá para.
3. Clique em **Editar Diretório**.
4. Selecione Olá **diretório** você gostaria que toouse na lista suspensa de saudação. Clique em seta Avançar hello.
5. Confirmar o mapeamento de diretório hello e afetados administradores. Se você estiver movendo em outro diretório, todos os administradores saudação do diretório original hello serão removidos.

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a>Sou um usuário/membro do domínio no locatário do AAD hello e criei uma solução pré-configurada. Como recebo uma função para o meu aplicativo?

Peça toomake um administrador global é um administrador global no hello AAD locatário e, em seguida, atribuir funções toousers por conta própria. Como alternativa, peça a um administrador global tooassign é uma função diretamente. Se desejar que o locatário do AAD Olá toochange que sua solução pré-configurada tiver sido implantada, consulte a saudação próxima pergunta.

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a>Como alternar o locatário do AAD Olá a que minha solução pré-configurada de monitoramento remota e o aplicativo estão atribuídos?

É possível executar uma implantação de nuvem do <https://github.com/Azure/azure-iot-remote-monitoring> e reimplantar com um locatário do AAD recém-criado. Como são, por padrão, um administrador global quando você cria um locatário do AAD, você tem permissões tooadd os usuários e atribuir funções de usuários toothose.

1. Criar um diretório AAD no hello [portal do Azure][lnk-portal].
2. Vá muito<https://github.com/Azure/azure-iot-remote-monitoring>.
3. Execute `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (por exemplo, `build.cmd cloud debug myRMSolution`)
4. Quando solicitado, defina Olá **tenantid** toobe seu locatário recém-criada em vez de seu locatário anterior.

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a>Desejo toochange um administrador de serviço ou Coadministrador quando conectado com uma conta organizacionais

Consulte o artigo de suporte Olá [alterar administrador de serviço e co-administrador quando conectado com uma conta organizacionais][lnk-service-admins].

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a>Por que vejo este erro? "Sua conta não tem Olá permissões adequadas toocreate uma solução. Verifique com o administrador da conta ou tente com uma conta diferente."

Examine Olá diagrama para obter diretrizes a seguir:

![][img-flowchart]

> [!NOTE]
> Se você continuar erro de saudação toosee após a validação for um administrador global no locatário do AAD hello e um coadministrador de assinatura de hello, peça ao administrador de conta remover usuário hello e reatribuir permissões necessárias nessa ordem. Primeiro, adicione usuário hello como um administrador global e, em seguida, adicionar o usuário como um coadministrador no hello assinatura do Azure. Se o problema persistir, entre em contato com [Ajuda e Suporte][lnk-help-support].

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a>Por que estou vendo este erro se eu tenho uma assinatura do Azure? "Uma assinatura do Azure é necessário toocreate pré-configurado soluções. Você pode criar uma conta de avaliação gratuita em apenas alguns minutos.”

Se você tiver certeza de que você tem uma assinatura do Azure, validar o mapeamento para a sua assinatura de locatário de saudação e certifique-se de locatário de saudação correto está selecionado na lista suspensa de saudação. Se você tiver validado Olá desejado de locatário está correto, execute Olá precede o diagrama e validar o mapeamento de saudação de sua assinatura e este locatário do AAD.

## <a name="next-steps"></a>Próximas etapas
toocontinue aprendendo sobre IoT Suite, consulte como é possível [personalizar uma solução pré-configurada][lnk-customize].

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
