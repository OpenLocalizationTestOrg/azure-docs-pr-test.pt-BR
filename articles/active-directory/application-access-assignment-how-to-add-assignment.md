---
title: "aplicativo de tooan aaaHow tooassign usuários e grupos | Microsoft Docs"
description: "Atribuir usuários toohello aplicativo toogrant acesso"
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
ms.openlocfilehash: e039a26e4b8f88ad747354859f1071b8f74b6789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-and-groups-tooan-application"></a>Como aplicativos de tooan de usuários e grupos tooassign

Antes dos usuários podem fazer qualquer Olá abaixo de um aplicativo específico, você precisa toofirst **atribuí-los toohello aplicativo** toogrant a eles acesso:

-   Acessar um aplicativo por **navegar diretamente o URL do aplicativo toohello** (também conhecido como iniciado por SP logon).

-   Acessar um aplicativo usando Olá **URL de acesso do usuário** em um aplicativo **propriedades** página (também conhecido como iniciado pelo IDP logon).

-   Ver um aplicativo em seu [Painel de Acesso do Aplicativo](https://myapps.microsoft.com/) ou aplicativo móvel.

-   Ver um aplicativo em seu [Inicializador de Aplicativos do Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).

## <a name="methods-tooassign-applications-with-azure-active-directory"></a>Aplicativos de tooassign de métodos com o Active Directory do Azure 

Há três formas de atribuir aplicativos com o Azure Active Directory:

-   [Atribuir um usuário diretamente tooan aplicativo como um administrador](#assign-a-user-directly-as-an-administrator)

-   [Atribua um grupo diretamente tooan aplicativo como um administrador](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [Habilitar o aplicativo de autoatendimento acesso tooallow usuários toofind seus próprios aplicativos](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a>Atribuir um usuário diretamente como administrador

tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.

7.  Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.

8.  Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.

9.  Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.

10. Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.

11. Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**. Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.

12. **Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.

13. Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.

14. **Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.

15. Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.

Após um curto período de tempo, usuários de saudação selecionado ser capaz de toolaunch esses aplicativos usando Olá métodos descritos na seção de descrição de solução de saudação.

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a>Atribua um grupo diretamente tooan aplicativo como um administrador

tooassign um ou mais grupos de aplicativo tooan diretamente, siga Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.

7.  Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.

8.  Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.

9.  Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.

10. Tipo de saudação **nome completo do grupo** do grupo de saudação que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.

11. Passe o mouse sobre Olá **grupo** em Olá lista tooreveal um **caixa de seleção**. Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello grupo seu usuário toohello **selecionados** lista.

12. **Opcional:** se você gostaria que muito**adicionar mais de um grupo**, tipo em outro **nome completo do grupo** em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa e clique em tooadd de caixa de seleção Olá esse grupo toohello **selecionados** lista.

13. Quando você terminar de selecionar os grupos, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.

14. **Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect toohello de tooassign uma função grupos selecionados.

15. Clique em Olá **atribuir** grupos selecionados do botão tooassign Olá aplicativo toohello.

Após um curto período de tempo, usuários hello dentro de grupos de saudação selecionado ser capaz de toolaunch esses aplicativos usando Olá métodos descritos na seção de descrição de solução de saudação. Se esses grupos forem dinâmicos, pode haver algum atraso de processamento adicional nessas atribuições que aparecem para os usuários nesses grupos atribuídos.

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a>Habilitar o aplicativo de autoatendimento acesso tooallow usuários toofind seus próprios aplicativos

Acesso de aplicativo de autoatendimento é tooself de usuários de tooallow uma ótima maneira-descobrir aplicativos, se desejar permitir Olá business grupo tooapprove acesso toothose aplicativos. Você pode permitir credenciais de Olá Olá business grupo toomanage atribuído toothose usuários para a direita da senha de logon único em aplicativos de seus painéis de acesso.

tooenable autoatendimento acesso tooan aplicativo, siga Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

   * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello tooenable acesso de autoatendimento toofrom Olá lista.

7.  Depois que o aplicativo hello carrega, clique em **autoatendimento** no menu de navegação à esquerda do aplicativo hello.

8.  tooenable acesso de aplicativo de autoatendimento para este aplicativo, ativar Olá **permitir que os usuários aplicativos de toothis acesso toorequest?** alternar muito**Sim.**

9.  Em seguida, tooselect Olá toowhich os usuários do grupo que solicitam acesso toothis aplicativo deve ser adicionado, clique em rótulo Olá seletor de Avançar toohello **toowhich grupo devem ser atribuídas usuários adicionados?** e selecione um grupo.

10. **Opcional:** se desejar toorequire uma aprovação de negócios antes que os usuários têm permissão de acesso, definir Olá **exigir aprovação antes de conceder acesso toothis aplicativo?** alternar muito**Sim**.

11. **Opcional: para aplicativos usando a senha de logon único no somente** se desejar tooallow esses negócios aprovadores toospecify Olá as senhas que são enviadas toothis aplicativo para usuários aprovados, defina Olá **permitir que os aprovadores tooset senhas do usuário para este aplicativo?**  alternar muito**Sim**.

12. **Opcional:** toospecify Olá business aprovadores são permitidos tooapprove aplicativos de toothis de acesso, clique em rótulo Olá seletor de Avançar toohello **quem tem permissão de aplicativo de toothis tooapprove access?** tooselect backup too10 aprovadores de negócio individuais.

  >[!NOTE]
  >Não há suporte para grupos.
  >
  >

13. **Opcional:** **para aplicativos que expõem as funções**, se desejar tooa função tooassign autoatendimento usuários aprovados clique Olá seletor próximo toohello **função toowhich devem ser atribuídos aos usuários nesta aplicativo?**  tooselect Olá função toowhich esses usuários devem ser atribuídos.

14. Clique em Olá **salvar** botão na parte superior de saudação do hello toofinish de folha.

Depois de concluir a configuração do aplicativo de autoatendimento, os usuários podem navegar tootheir [painel de acesso do aplicativo](https://myapps.microsoft.com/) e clique em Olá **+ adicionar** botão toofind Olá aplicativos toowhich você habilitou Acesso de autoatendimento. Aprovadores de negócios também recebem uma notificação em seu [Painel de Acesso do Aplicativo](https://myapps.microsoft.com/). Você pode habilitar um email notificando-os quando um usuário solicitou o aplicativo de tooan de acesso que requer sua aprovação. 

Essas aprovações oferecem suporte a fluxos de trabalho de aprovação único apenas, indicando que se você especificar vários aprovadores, qualquer aprovador único aplicativo de toohello aprovador access.

## <a name="next-steps"></a>Próximas etapas
[Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo](active-directory-application-proxy-sso-using-kcd.md)
