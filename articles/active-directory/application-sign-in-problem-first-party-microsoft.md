---
title: aaaProblems entrar tooa aplicativo Microsoft | Microsoft Docs
description: Solucionar problemas enfrentados ao entrar toofirst terceiros Microsoft Applications usando o Azure AD (como o Office 365)
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a>Problemas para entrar no tooa aplicativos Microsoft

Os aplicativos Microsoft (como o Office 365 Exchange, SharePoint, Yammer, etc.) são atribuídos e gerenciados de forma um pouco diferente dos aplicativos SaaS de terceiros ou outros aplicativos que você integra com o Azure AD para o logon único.

Há três maneiras principais que um usuário pode obter acesso tooa Microsoft publicou o aplicativo.

-   Para aplicativos em Olá Office 365 ou outros pacotes pagas, os usuários terão acesso por meio de **atribuição de licença** ou diretamente tootheir conta de usuário, ou por meio de um grupo usando nosso recurso de atribuição de licença baseada em grupo.

-   Para aplicativos que Microsoft ou uma terceira parte confiável publica livremente para qualquer pessoa toouse, os usuários podem receber acesso por meio de **consentimento do usuário**. This0 significa que eles entrar no aplicativo toohello com sua conta do Azure AD ou de estudante e permitir que ele toohave acesso toosome limitada de conjunto de dados em sua conta.

-   Para aplicativos que Microsoft ou uma parte do 3º publica livremente para qualquer pessoa toouse, os usuários também podem ser concedidos acesso por meio de **consentimento do administrador**. Isso significa que um administrador determinou aplicativo hello pode ser usado por todas as pessoas na organização hello, para que poderem entrar no aplicativo de toohello com uma conta de Administrador Global e conceder acesso tooeveryone na organização hello.

tootroubleshoot seu problema, começam com hello [áreas de problemas gerais com acesso de aplicativo tooconsider](#general-problem-areas-with-application-access-to-consider) e, em seguida, ler Olá [passo a passo: etapas tootroubleshoot access do Microsoft Application](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget detalhes hello.

## <a name="general-problem-areas-with-application-access-tooconsider"></a>Áreas de problemas gerais com tooconsider de acesso do aplicativo

Abaixo está uma lista de saudação áreas de problema geral que você pode analisar se você tiver uma ideia de onde toostart, mas é recomendável que você leia Olá passo a passo tooget ir rapidamente: [passo a passo: etapas tootroubleshoot access do Microsoft Application](#walkthrough-steps-to-troubleshoot-microsoft-application-access).

-   [Problemas com a conta do usuário Olá](#problems-with-the-users-account)

-   [Problemas com grupos](#problems-with-groups)

-   [Problemas com políticas de acesso condicional](#problems-with-conditional-access-policies)

-   [Problemas com consentimento do aplicativo](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a>Etapas tootroubleshoot access do Microsoft Application

Abaixo estão algumas pessoas problemas comuns encontrar quando os usuários não podem entrar no tooa aplicativos Microsoft.

-   Geral emite toocheck primeiro

  * Verifique se o usuário hello está entrando toohello **corrigir URL** e não é uma URL de aplicativo local.

  * Certifique-se de conta de usuário Olá **não bloqueada.**

  * Verifique se Olá **conta de usuário existe** no Active Directory do Azure. [Verificar se existe uma conta de usuário no Azure Active Directory](#problems-with-the-users-account)

  * Certifique-se de conta de usuário Olá **habilitado** para entradas. [Verificar o status da conta do usuário](#problems-with-the-users-account)

  * Tornar-se de que usuário Olá **senha não está expirada ou esquecida.** [Redefinir uma senha do usuário](#reset-a-users-password) ou [Habilitar a redefinição de senha por autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)

   * Certifique-se de que a **Autenticação Multifator** não está bloqueando o acesso do usuário. [Verificar o status de autenticação multifator do usuário](#check-a-users-multi-factor-authentication-status) ou [Verificar informações de contato de autenticação do usuário](#check-a-users-authentication-contact-info)

   * Certifique-se de que uma **Política de Acesso Condicional** ou política de **Proteção de Identidade** não está bloqueando o acesso do usuário. [Verificar uma política específica de acesso condicional ](#problems-with-conditional-access-policies) ou [Verificar uma política específica de acesso condicional do aplicativo](#check-a-specific-applications-conditional-access-policy) ou [Desabilitar uma política específica de acesso condicional ](#disable-a-specific-conditional-access-policy)

   * Certifique-se de que um usuário **informações de contato de autenticação** está ativo toodate tooallow autenticação multifator ou o acesso condicional políticas toobe imposta. [Verificar o status de autenticação multifator do usuário](#check-a-users-multi-factor-authentication-status) ou [Verificar informações de contato de autenticação do usuário](#check-a-users-authentication-contact-info)

-   Para **Microsoft** **aplicativos que exigem uma licença** (como o Office365), aqui estão alguns problemas específicos toocheck depois de verificar problemas gerais de saudação acima:

   * Verifique se o usuário hello ou tem um **licença atribuída.** [Verificar as licenças atribuídas de um usuário](#check-a-users-assigned-licenses) ou [Verificar licenças atribuídas de um grupo](#check-a-groups-assigned-licenses)

   * Se a licença de saudação é **atribuído tooa** **grupo estático**, certifique-se de que Olá **usuário é um membro** desse grupo. [Verificar as associações de grupo de um usuário](#check-a-users-group-memberships)

   * Se a licença de saudação é **atribuído tooa** **grupo dinâmico**, certifique-se de que Olá **regra dinâmica de grupo está definida corretamente**. [Verificar os critérios de associação do grupo dinâmico](#check-a-dynamic-groups-membership-criteria)

   * Se a licença de saudação é **atribuído tooa** **grupo dinâmico**, certifique-se de que esse grupo dinâmico Olá tem **concluir o processamento** sua associação e que hello **usuário é um membro** (Isso pode levar algum tempo). [Verificar as associações de grupo de um usuário](#check-a-users-group-memberships)

   *  Depois que você certifique-se de saudação licença será atribuída, certifique-se de licença Olá é **não expirado**.

   *  Certifique-se de licença Olá é **para o aplicativo hello** estão acessando.

-   Para **Microsoft** **aplicativos que não requerem uma licença**, aqui estão algumas outra coisas toocheck:

   * Se o aplicativo hello está solicitando **permissões em nível de usuário** (por exemplo "acesso a caixa de correio do usuário"), certifique-se de que o usuário Olá entrou no aplicativo toohello e executou um **operação consentimento de nível de usuário**  toolet Olá aplicativo acessar seus dados.

   * Se o aplicativo hello está solicitando **permissões de administrador** (por exemplo "acesso a caixas de correio de todos os usuários"), certifique-se de que um Administrador Global executou um **operação consentimento de nível de administrador nome de todos os usuários** na organização hello.

## <a name="problems-with-hello-users-account"></a>Problemas com a conta do usuário Olá

Acesso de aplicativo pode ser bloqueado devido a problema tooa com um usuário que é atribuído o aplicativo toohello. Veja abaixo algumas maneiras de solucionar problemas dos usuários e suas configurações de conta:

-   [Verificar se existe uma conta de usuário no Azure Active Directory](#check-if-a-user-account-exists-in-azure-active-directory)

-   [Verificar o status da conta do usuário](#check-a-users-account-status)

-   [Redefinir a senha de um usuário](#reset-a-users-password)

-   [Habilitar a redefinição de senha por autoatendimento](#enable-self-service-password-reset)

-   [Verificar o status da Autenticação Multifator de um usuário](#check-a-users-multi-factor-authentication-status)

-   [Verificar as informações de contato de autenticação de um usuário](#check-a-users-authentication-contact-info)

-   [Verificar as associações de grupo de um usuário](#check-a-users-group-memberships)

-   [Verificar as licenças atribuídas de um usuário](#check-a-users-assigned-licenses)

-   [Atribuir uma licença a um usuário](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a>Verificar se existe uma conta de usuário no Azure Active Directory

toocheck se uma conta de usuário estiver presente, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Verifique as propriedades de saudação do hello usuário objeto toobe-se de que elas são conforme o esperado e nenhum dado está ausente.

### <a name="check-a-users-account-status"></a>Verificar o status da conta do usuário

toocheck um usuário status da conta, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **Perfil**.

8.  Em **configurações** Certifique-se de que **bloco entrar** está definido muito**não**.

### <a name="reset-a-users-password"></a>Redefinir a senha de um usuário

tooreset a senha do usuário, siga Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em Olá **Redefinir senha** botão na parte superior de saudação da folha de usuário hello.

8.  Clique em hello **Redefinir senha** botão Olá **Redefinir senha** folha que aparece.

9.  Saudação de cópia **senha temporária** ou **insira uma nova senha** para usuário hello.

10. Se comunicar esse novo usuário toohello senha, eles toochange necessária essa senha durante o próximo entrar tooAzure do Active Directory.

### <a name="enable-self-service-password-reset"></a>Habilitar a redefinição de senha por autoatendimento

senha de autoatendimento tooenable redefinir, execute as etapas de implantação de saudação abaixo:

-   [Habilitar os usuários tooreset suas senhas do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [Habilitar os usuários tooreset ou alterar suas senhas do Active Directory local](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>Verificar o status da Autenticação Multifator de um usuário

toocheck um usuário do multi-factor status de autenticação seguem Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  Clique em Olá **multi-Factor Authentication** botão na parte superior de saudação da folha de saudação.

7.  Uma vez Olá **Portal de administração do multi-Factor Authentication** cargas, certifique-se você estiver usando Olá **usuários** guia.

8.  Localize usuário Olá Olá lista de usuários por pesquisa, filtragem ou classificação.

9.  Usuário Olá selecione da lista de saudação de usuários e **habilitar**, **desabilitar**, ou **impor** autenticação multifator conforme desejado.

  * **Observação**: se um usuário estiver em um **imposto** de estado, você pode defini-las muito**desabilitado** temporariamente toolet-los de volta para sua conta. Quando eles forem novamente, você pode alterar seu estado muito**habilitado** novamente toorequire-los entre suas informações de contato durante o próximo registro de toore. Como alternativa, você pode seguir etapas Olá Olá [Verifique informações de contato de autenticação do usuário](#check-a-users-authentication-contact-info) tooverify ou defina esses dados para eles.

### <a name="check-a-users-authentication-contact-info"></a>Verificar as informações de contato de autenticação de um usuário

toocheck autenticação do usuário entre em contato com informações usadas para autenticação multifator, acesso condicional, proteção de identidade e de redefinição de senha, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **Perfil**.

8.  Role para baixo demais**informações de contato de autenticação**.

9.  **Revisão** dados saudação registrado para o usuário hello e atualização conforme necessário.

### <a name="check-a-users-group-memberships"></a>Verificar as associações de grupo de um usuário

toocheck um usuário as associações de grupo, execute as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **grupos** toosee que agrupa usuário Olá é membro.

### <a name="check-a-users-assigned-licenses"></a>Verificar as licenças atribuídas de um usuário

toocheck um usuário atribuído licenças, siga Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **licenças** toosee quais licenças Olá atualmente atribuída ao usuário.

### <a name="assign-a-user-a-license"></a>Atribuir uma licença a um usuário 

tooassign um usuário de tooa de licença, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **licenças** toosee quais licenças Olá atualmente atribuída ao usuário.

8.  Clique em Olá **atribuir** botão.

9.  Selecione **um ou mais produtos** da lista de saudação de produtos disponíveis.

10. **Opcional** clique Olá **opções atribuição** item toogranularly atribuir produtos. Clique em **OK** quando isso for concluído.

11. Clique em Olá **atribuir** botão tooassign usuário de toothis essas licenças.

## <a name="problems-with-groups"></a>Problemas com grupos

Acesso de aplicativo pode ser bloqueado devido a problema tooa com um grupo que é atribuído o aplicativo toohello. Abaixo são apresentadas algumas maneiras para solucionar problemas com grupos e associações de grupo:

-   [Verificar associações de um grupo](#check-a-groups-membership)

-   [Verificar os critérios de associação do grupo dinâmico](#check-a-dynamic-groups-membership-criteria)

-   [Verificar as licenças atribuídas de um usuário](#check-a-groups-assigned-licenses)

-   [Reprocessar licenças do um grupo](#reprocess-a-groups-licenses)

-   [Atribuir uma licença a um grupo](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a>Verificar associações de um grupo

toocheck a associação do grupo, siga Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  clique em **Todos os grupos**.

6.  **Pesquisa** para grupo de saudação que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **membros** tooreview lista de saudação de usuários atribuídos toothis grupo.

### <a name="check-a-dynamic-groups-membership-criteria"></a>Verificar os critérios de associação do grupo dinâmico 

toocheck critérios de associação do grupo dinâmico, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  clique em **Todos os grupos**.

6.  **Pesquisa** para grupo de saudação que lhe interessam e **clique linha hello** tooselect.

7.  clique em **Regras de associação dinâmica.**

8.  Saudação de revisão **simples** ou **avançados** definida para esse grupo de regras e certifique-se de que esse usuário Olá deseja toobe um membro desse grupo atenda a esses critérios.

### <a name="check-a-groups-assigned-licenses"></a>Verificar as licenças atribuídas de um usuário

toocheck um grupo atribuído licenças, siga Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  clique em **Todos os grupos**.

6.  **Pesquisa** para grupo de saudação que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **licenças** toosee qual grupo de licenças Olá atualmente tem atribuída.

### <a name="reprocess-a-groups-licenses"></a>Reprocessar licenças do um grupo

tooreprocess um grupo atribuído licenças, siga Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  clique em **Todos os grupos**.

6.  **Pesquisa** para grupo de saudação que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **licenças** toosee qual grupo de licenças Olá atualmente tem atribuída.

8.  Clique em Olá **reprocessar** tooensure botão que Olá membros do grupo de toothis licenças atribuídas estão atualizados. Isso pode levar algum tempo, dependendo do tamanho de saudação e a complexidade do grupo de saudação.

   >[!NOTE]
   >toodo isso mais rapidamente, considere temporariamente atribuir uma licença toohello usuário diretamente. [Atribua uma licença a um usuário](#problems-with-application-consent).
   >
   >

### <a name="assign-a-group-a-license"></a>Atribuir uma licença a um grupo

tooassign um grupo de tooa de licença, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  clique em **Todos os grupos**.

6.  **Pesquisa** para grupo de saudação que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **licenças** toosee qual grupo de licenças Olá atualmente tem atribuída.

8.  Clique em Olá **atribuir** botão.

9.  Selecione **um ou mais produtos** da lista de saudação de produtos disponíveis.

10. **Opcional** clique Olá **opções atribuição** item toogranularly atribuir produtos. Clique em **OK** quando isso for concluído.

11. Clique em Olá **atribuir** botão tooassign grupo de toothis essas licenças. Isso pode levar algum tempo, dependendo do tamanho de saudação e a complexidade do grupo de saudação.

   >[!NOTE]
   >toodo isso mais rapidamente, considere temporariamente atribuir uma licença toohello usuário diretamente. [Atribua uma licença a um usuário](#problems-with-application-consent).
   > 
   >

## <a name="problems-with-conditional-access-policies"></a>Problemas com políticas de acesso condicional

### <a name="check-a-specific-conditional-access-policy"></a>Verificar uma política específica de acesso condicional

toocheck ou validar uma política de acesso condicional:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação hello.

5.  Clique em Olá **acesso condicional** item de navegação.

6.  Clique em diretiva de saudação que lhe interessam inspecionar.

7.  Analise se não há condições, atribuições ou outras configurações específicas que podem estar bloqueando o acesso do usuário.

   >[!NOTE]
   >Você poderá desabilitar tootemporarily este tooensure de política está afetando sinal ins toodo não hello, conjunto **habilitar política** alternar muito**não** e clique em Olá **salvar** botão .
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a>Verificar uma política específica de acesso condicional do aplicativo

toocheck ou validar a política de acesso condicional configurada atualmente de um único aplicativo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação hello.

5.  clique em **Todos os aplicativos**.

6.  Pesquisa para o aplicativo hello está interessado, ou Olá usuário está tentando toosign no aplicativo tooby exibir a id de aplicativo ou nome.

     >[!NOTE]
     >Se você não vir o aplicativo hello que você está procurando, clique em Olá **filtro** botão e expandir o escopo de saudação da lista de saudação muito**todos os aplicativos**. Se você quiser toosee mais colunas, clique em Olá **colunas** botão detalhes adicionais de tooadd para seus aplicativos.
     >
     >

7.  Clique em Olá **acesso condicional** item de navegação.

8.  Clique em diretiva de saudação que lhe interessam inspecionar.

9.  Analise se não há condições, atribuições ou outras configurações específicas que podem estar bloqueando o acesso do usuário.

     >[!NOTE]
     >Você poderá desabilitar tootemporarily este tooensure de política está afetando sinal ins toodo não hello, conjunto **habilitar política** alternar muito**não** e clique em Olá **salvar** botão .
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a>Desabilitar uma política específica de acesso condicional

toocheck ou validar uma política de acesso condicional:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação hello.

5.  Clique em Olá **acesso condicional** item de navegação.

6.  Clique em diretiva de saudação que lhe interessam inspecionar.

7.  Desabilitar política Olá por configuração Olá **habilitar política** alternar muito**não** e clique em Olá **salvar** botão.

## <a name="problems-with-application-consent"></a>Problemas com consentimento do aplicativo

Acesso de aplicativo pode ser bloqueado porque não houve Olá permissões adequadas consentimento operação. Abaixo, são apresentadas algumas maneiras de solucionar problemas e resolver questões relacionados ao consentimento do aplicativo:

-   [Executar uma operação de consentimento de nível de usuário](#perform-a-user-level-consent-operation)

-   [Executar operação de consentimento de nível de administrador para qualquer aplicativo](#perform-administrator-level-consent-operation-for-any-application)

-   [Executar consentimento de nível de administrador para um aplicativo de locatário único](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [Executar consentimento de nível de administrador para um aplicativo multilocatário](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a>Executar uma operação de consentimento de nível de usuário

-   Para qualquer aplicativo habilitado para abrir conexão de ID que solicita permissões, navegar a tela de entrada do aplicativo toohello executa um aplicativo de toohello de nível de consentimento do usuário para o usuário conectado hello.

-   Se você desejar toodo isso programaticamente, consulte [solicita o consentimento do usuário individual](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).

### <a name="perform-administrator-level-consent-operation-for-any-application"></a>Executar operação de consentimento de nível de administrador para qualquer aplicativo

-   Para **somente os aplicativos desenvolvidos usando o modelo de aplicativo hello V1**, você pode forçar essa toooccur de nível de consentimento do administrador adicionando "**? prompt = admin\_consentimento**" toohello final de um entrada do aplicativo na URL.

-   Para **qualquer aplicativo desenvolvido usando o modelo de aplicativo hello V2**, você pode impor esse toooccur consentimento de nível de administrador, seguindo as instruções de saudação em Olá **solicitar permissões de saudação de um diretório administrador** seção [usando o ponto de extremidade de autorização do Olá administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a>Executar consentimento de nível de administrador para um aplicativo de locatário único

-   Para **único locatário aplicativos** que solicitar permissões (como aqueles que você está desenvolvendo ou possuir em sua organização), você pode executar uma **consentimento de nível administrativo** operação em nome de todos os os usuários fazer logon como um Administrador Global e clicando em Olá **conceder permissões** botão na parte superior de saudação do hello **registro de aplicativos -&gt; todos os aplicativos -&gt; selecionar um aplicativo - &gt; Permissões necessárias** folha.

-   Para **qualquer aplicativo desenvolvido usando Olá V1 ou V2 modelo de aplicativo**, você pode impor esse toooccur consentimento de nível de administrador, seguindo as instruções de saudação em Olá **solicitar permissões de saudação de um administrador de diretório** seção [usando o ponto de extremidade de autorização do Olá administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a>Executar consentimento de nível de administrador para um aplicativo multilocatário

-   Para **Aplicativos de multilocatário** que solicitar permissões (como um aplicativo de terceiros ou desenvolvido pela Microsoft), você pode executar uma operação de **consentimento de nível administrativo**. Entrar como um Administrador Global e clicando em Olá **conceder permissões** botão sob Olá **aplicativos corporativos -&gt; todos os aplicativos -&gt; selecionar um aplicativo -&gt; Permissões** folha (disponível em breve).

-   Você também pode impor esse toooccur consentimento de nível de administrador seguindo as instruções de saudação em hello **solicitar permissões de saudação de um administrador de diretório** seção [usando o ponto de extremidade de autorização do Olá administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

## <a name="next-steps"></a>Próximas etapas
[Usando o ponto de extremidade de autorização do Olá administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

