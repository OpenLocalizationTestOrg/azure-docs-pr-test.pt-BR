---
title: aaaProblem usando o acesso do aplicativo de autoatendimento | Microsoft Docs
description: "Solucionar problemas de acesso do aplicativo de serviço tooself relacionada de problemas"
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
ms.reviewer: japere
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a>Problema ao usar o acesso de aplicativo de autoatendimento

Acesso de aplicativo de autoatendimento é tooself de usuários de tooallow uma ótima maneira-descobrir aplicativos, se desejar permitir Olá business grupo tooapprove acesso toothose aplicativos. Você pode permitir credenciais de Olá Olá business grupo toomanage atribuído toothose usuários para a direita da senha de logon único em aplicativos de seus painéis de acesso.

Antes dos usuários podem descobrir automaticamente aplicativos do seu painel de acesso, é necessário tooenable **acesso de aplicativo de autoatendimento** tooany aplicativos que você deseja tooallow usuários tooself-descobrir e solicitar acesso a.

## <a name="general-issues-toocheck-first"></a>Geral emite toocheck primeiro

-   Verifique se o acesso do aplicativo de autoatendimento está configurado corretamente. Consulte "Como acessar o aplicativo de autoatendimento tooconfigure".

-   Certifique-se de saudação usuário ou grupo tiver sido habilitado toorequest acesso ao aplicativo de autoatendimento.

-   Verifique se o usuário hello está visitando o local correto de saudação para acesso ao aplicativo de autoatendimento. os usuários podem navegar tootheir [painel de acesso do aplicativo](https://myapps.microsoft.com/) e clique em Olá **+ adicionar** botão toofind Olá aplicativos toowhich você habilitou o acesso de autoatendimento.

-   Se o acesso de aplicativo de autoatendimento foi configurado recentemente, tente toosign e sair novamente no painel de acesso do usuário Olá após toosee de alguns minutos se as alterações de acesso de autoatendimento Olá apareceu.

## <a name="how-tooconfigure-self-service-application-access"></a>Como acessar o aplicativo de autoatendimento tooconfigure

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
 > Não há suporte para grupos.
 >
 >

13. **Opcional:** **para aplicativos que expõem as funções**, se desejar tooa função tooassign autoatendimento usuários aprovados clique Olá seletor próximo toohello **função toowhich devem ser atribuídos aos usuários nesta aplicativo?**  tooselect Olá função toowhich esses usuários devem ser atribuídos.

14. Clique em Olá **salvar** botão na parte superior de saudação do hello toofinish de folha.

Depois de concluir a configuração do aplicativo de autoatendimento, os usuários podem navegar tootheir [painel de acesso do aplicativo](https://myapps.microsoft.com/) e clique em Olá **+ adicionar** botão toofind Olá aplicativos toowhich você habilitou Acesso de autoatendimento. Aprovadores de negócios também recebem uma notificação em seu [Painel de Acesso do Aplicativo](https://myapps.microsoft.com/). Você pode habilitar um email notificando-os quando um usuário solicitou o aplicativo de tooan de acesso que requer sua aprovação. 

Suportam a essas aprovações única aprovação fluxos de trabalho, que significa que, se você especificar vários aprovadores, qualquer aprovador único pode aprovar acesso toohello aplicativo.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Se essas etapas de solução de problemas não resolver o problema de saudação 

Abra um tíquete de suporte com hello informações a seguir se disponíveis:

-   ID de erro de correlação

-   UPN (endereço de email de usuário)

-   TenantID

-   Tipo de navegador

-   Fuso horário e hora/cronograma durante o erro

-   Rastreamentos do Fiddler

## <a name="next-steps"></a>Próximas etapas
[Configuração do Azure Active Directory para gerenciamento de grupo de autoatendimento](active-directory-accessmanagement-self-service-group-management.md)
