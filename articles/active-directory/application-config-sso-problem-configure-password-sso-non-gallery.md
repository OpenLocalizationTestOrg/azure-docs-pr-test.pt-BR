---
title: "aaaProblem configurando senha single sign-on para um aplicativo da Galeria não | Microsoft Docs"
description: "Entender a face de pessoas problemas comuns Olá ao configurar logon único de senha para aplicativos não-Galeria personalizados que não estão listados em Olá Galeria de aplicativos do Azure AD"
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a>Como configurar o logon único com senha para um aplicativo que não seja da galeria

Este artigo ajuda face de pessoas de problemas comuns do toounderstand Olá ao configurar **senha SSO** com um aplicativo não Galeria.

## <a name="how-toocapture-sign-in-fields-for-an-application"></a>Como entrar toocapture os campos para um aplicativo

Captura de campo de entrada só tem suporte para páginas de entrada habilitadas por HTML e **não tem suporte para páginas de entrada não padrão**, como aquelas que usam Flash ou outras tecnologias de HTML não habilitado.

Há duas maneiras que você pode capturar campos de entrada para aplicativos personalizados:

-   Captura automática de campo de entrada

-   Captura manual de campo de entrada

**Captura de campo de entrada automática** funciona bem com a maioria dos habilitado HTML páginas de entrada, se eles usarem **IDs DIV conhecidos Olá nome de usuário e senha de entrada** campo. Isso funciona de maneira de saudação é por atrito Olá HTML na página de saudação toofind IDs DIV que correspondem a certos critérios e, em seguida, salvando metadados para esse aplicativo para que pode reproduzir senhas tooit mais tarde.

**Captura de campo de entrada manual** pode ser usado em caso de Olá Olá aplicativo **fornecedor não rotula** Olá entrada campos usados para entrar. Captura de campo de entrada manual também pode ser usada no caso de Olá quando hello **fornecedor renderiza vários campos** que não pode ser detectado automaticamente. AD do Azure pode armazenar dados para vários campos que estejam na Olá entrar na página, desde que você Conte-nos onde esses campos estão na página de saudação.

Em geral, **se a captura de campo de entrada automática não funcionar, sugerimos sempre tentar opção manual de saudação.**

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a>Como tooautomatically capturar campos de entrada para um aplicativo

tooconfigure **com base em senha de logon único** para um aplicativo usando **captura automática campo entrar**, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione aplicativo hello deseja tooconfigure-logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Modo de seleção Olá **com base em senha de logon.**

9.  Digite hello **URL de logon**. Isso é Olá URL onde os usuários digitarão seu nome de usuário e senha toosign em para. **Certifique-se de campos de entrada hello são visíveis na URL Olá você fornecer**.

10. Clique em Olá **salvar** botão.

11. Depois de você fazer isso, podemos será arranhar automaticamente essa URL para um nome de usuário e senha caixa de entrada e permitem que você toouse AD do Azure toosecurely transmitir aplicativos de toothat senhas usando a extensão de navegador do painel de acesso de saudação.

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a>Como toomanually capturar campos de entrada para um aplicativo

toomanually captura campos de entrada, primeiro você deve ter extensão de navegador do painel de acesso Olá instalado e **não esteja em execução em modo privado, inPrivate ou incognito.** extensão de navegador tooinstall hello, siga etapas Olá Olá [como tooinstall Olá extensão de navegador do painel de acesso](#i-cannot-manually-detect-sign-in-fields-for-my-application) seção.

tooconfigure **com base em senha de logon único** para um aplicativo usando **captura do campo de entrada manual**, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

   * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione aplicativo hello deseja tooconfigure-logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Modo de seleção Olá **com base em senha de logon.**

9.  Digite hello **URL de logon**. Isso é Olá URL onde os usuários digitarão seu nome de usuário e senha toosign em para. **Certifique-se de campos de entrada hello são visíveis na URL Olá você fornecer**.

10. Clique em Olá **salvar** botão.

11. Depois de você fazer isso, podemos será arranhar automaticamente essa URL para um nome de usuário e senha caixa de entrada e permitem que você toouse AD do Azure toosecurely transmitir aplicativos de toothat senhas usando a extensão de navegador do painel de acesso de saudação. No caso de Olá que isso falhar, você pode **Olá entrar no modo toouse campo de entrada manual captura de alteração** continuando toostep 12.

12. clique em **Configurar &lt;appname&gt; configurações de logon único com senha**.

13. Selecione Olá **detectar manualmente os campos de entrada** opção de configuração.

14. Clique em **OK**.

15. Clique em **Salvar**.

16. Execute Olá na tela instruções toouse Olá painel de acesso.

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a>Vejo o erro "Não foi possível encontrar os campos de entrada nessa URL"

Você vê este erro quando a detecção automática de campos de entrada falha. tooresolve esse problema, tente detecção de campo de entrada manual por Olá seguindo as etapas em Olá [como toomanually capturar campos de entrada para um aplicativo](#how-to-manually-capture-sign-in-fields-for-an-application) seção.

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a>Consulte o erro "não é possível toosave Single Sign-on configuração"

Em alguns casos raros, a configuração de logon único Olá a atualização pode falhar. tooresolve esse tente salvar Olá única configuração de logon novamente.

Se isso continuar toofail consistentemente, abrir um caso de suporte e fornecer informações de saudação coletadas Olá [como detalhes de saudação toosee de uma notificação de portal](#i-cannot-manually-detect-sign-in-fields-for-my-application) e [como tooget ajuda enviando tooa de detalhes de notificação engenheiro de suporte](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) seções.

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a>Não posso manualmente detectar os campos de entrada para meu aplicativo

Alguns dos comportamentos de saudação que podem ocorrer ao detecção manual não está funcionando:

-   processo de captura manual Olá apareceu toowork, mas campos Olá capturados não estavam corretos

-   Olá direita campos não destacados ao executar o processo de captura Olá

-   o processo de captura Olá leva-me a página de logon do aplicativo toohello conforme o esperado, mas nada acontece

-   Captura manual aparece toowork, mas SSO não acontece quando os usuários navegam toohello aplicativo hello painel de acesso.

Se você encontrar qualquer um desses problemas, verifique o seguinte de saudação:

-   Verifique se você tem a versão mais recente de saudação da extensão de navegador do painel de acesso Olá **instalado** e **habilitado** , seguindo as etapas de Olá Olá [como tooinstall Olá navegador do painel de acesso extensão](#how-to-install-the-access-panel-browser-extension) seção.

-   Certifique-se de que você está tentando não o processo de captura Olá ao seu navegador **modo privado, inPrivate ou incognito**. Não há suporte para a extensão do painel de acesso Olá nesses modos.

-   Certifique-se de que os usuários não estão tentando toosign no aplicativo toohello do painel de acesso Olá ao mesmo tempo em **modo privado, inPrivate ou incognito**. Não há suporte para a extensão do painel de acesso Olá nesses modos.

-   Repita o processo de captura manual hello, garantindo marcadores Olá vermelho sobre campos corretos de saudação.

-   Se o processo de captura manual Olá parece toohang, ou na página de entrada hello não faz nada (caso 3 acima), tente Olá captura manual processo novamente. Mas, desta vez depois de concluir o processo hello, pressione Olá **F12** botão tooopen console do desenvolvedor do navegador. Uma vez aberto, Olá **console** e tipo **window.location= "&lt;digite Olá logon na url que você especificou ao configurar o aplicativo hello&gt;"** e, em seguida, pressione  **Digite**. Essa força uma página redirecionar que terminar o processo de captura hello e armazenar os campos de saudação que foram capturados.

Se nenhuma dessas abordagens funcionar para você, podemos ajudar. Abrir um caso de suporte com detalhes de saudação do que você tentou, bem como informações de saudação coletadas Olá [como detalhes de saudação toosee de uma notificação de portal](#i-cannot-manually-detect-sign-in-fields-for-my-application) e [como tooget ajuda enviando detalhes de notificação tooa suporte engenheiro](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) seções (se aplicável).

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Como tooinstall Olá extensão de navegador do painel de acesso

Olá tooinstall extensão de navegador do painel de acesso, execute as etapas de saudação abaixo:

1.  Olá abrir [painel de acesso](https://myapps.microsoft.com) em um dos navegadores Olá com suporte e entre como um **usuário** no AD do Azure.

2.  Clique em uma **aplicativo SSO de senha** no painel de acesso de saudação.

3.  Olá prompt perguntando tooinstall Olá software, selecione **instalar agora**.

4.  Com base em seu navegador é direcionado toohello link para download. **Adicionar** navegador de tooyour Olá extensão.

5.  Se seu navegador solicita, selecione tooeither **habilitar** ou **permitir** Olá extensão.

6.  Quando estiver instalado, **reinicie** a sessão do navegador.

7.  Entrar painel de acesso de saudação e veja se é possível **iniciar** seus aplicativos de SSO de senha.

Você também pode baixar a extensão Olá para Chrome e Firefox de links diretos da saudação abaixo:

-   [Extensão do Painel de Acesso do Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extensão do Painel de Acesso do Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a>Como detalhes de saudação toosee de uma notificação de portal

Você pode ver os detalhes de saudação de qualquer notificação de portal, seguindo as etapas de saudação abaixo:

1.  Clique em Olá **notificações** ícone (bell Olá) no canto superior direito de saudação do hello Portal do Azure

2.  Selecione qualquer notificação em um **erro** estado (aquelas com um toothem de Avançar vermelho (!)).

  >!NOTA] Não é possível clicar em notificações com estado de **Êxito** ou **Em Andamento**.
  >
  >

3.  Este Olá abrir **detalhes da notificação** folha.

4.  Use essas informações por conta própria toounderstand mais detalhes sobre o problema de saudação.

5.  Se você ainda precisar de Ajuda, você também pode compartilhar essas informações com um suporte engenheiro ou hello grupo tooget Ajuda do produto com o problema.

6.  Clique em Olá **cópia** **ícone** toohello direito da saudação **copiar erro** textbox toocopy todos os Olá tooshare de detalhes de notificação com um engenheiro de suporte ou produto de grupo.

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a>Como ajudar a tooget enviando o engenheiro de suporte de tooa de detalhes de notificação

É muito importante que você compartilhe **todos os detalhes abaixo de Olá** com um engenheiro de suporte se você precisar de Ajuda, para que eles podem ajudá-lo rapidamente. Você pode fazer isso facilmente por **tirar uma captura de tela,** ou clicando Olá **ícone de erro de cópia**, encontrado toohello direito da saudação **copiar erro** caixa de texto.

## <a name="notification-details-explained"></a>Detalhes da notificação explicados

Olá abaixo explica mais que cada um dos itens de notificação Olá significa e fornece exemplos de cada um deles.

### <a name="essential-notification-items"></a>Itens de notificação essenciais

-   **Título** – Olá título descritivo da notificação de saudação

    -   Exemplo – **Configurações do proxy do aplicativo**

-   **Descrição** – Olá descrição do que ocorreu como resultado da operação de saudação

    -   Exemplo – **A URL interna inserida já está sendo usada por outro aplicativo**

-   **Id de notificação** – a id exclusiva Olá da notificação de saudação

    -   Exemplo – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **Id de solicitação do cliente** – id de solicitação específica de saudação feita pelo seu navegador

    -   Exemplo – **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Hora UTC de carimbo de data /** – Olá timestamp durante o qual ocorreu notificação hello, em UTC

    -   Exemplo – **2017-03-23T19:50:43.7583681Z**

-   **Id de transação interna** – Olá ID interna, podemos usar erro de saudação toolook em nossos sistemas

    -   Exemplo – **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **UPN** – usuário Olá que realizou a operação de saudação

    -   Exemplo – **tperkins@f128.info**

-   **Id do locatário** – ID exclusiva de saudação do locatário Olá Olá usuário que realizou a operação de saudação era um membro de

    -   Exemplo – **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **Id do objeto de usuário** – Olá ID exclusiva do usuário Olá que realizou a operação de saudação

    -   Exemplo – **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Itens de notificação detalhados

-   **Nome de exibição** – **(pode estar vazia)** um nome para exibição mais detalhado para o erro Olá

    -   Exemplo *– **Configurações do proxy do aplicativo**

-   **Status** – Olá status específicos de notificação de saudação

    -   Exemplo – **Falha**

-   **Id de objeto** – **(pode estar vazia)** Olá ID de objeto em relação a quais Olá a operação foi executada

    -   Exemplo – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Detalhes** – Olá descrição detalhada do que ocorreu como resultado da operação de saudação

    -   Exemplo – **A URL interna 'http://bing.com/' é inválida, uma vez que está sendo utilizada**

-   **Erro de cópia** – clique Olá **ícone para copiar** toohello direito da saudação **copiar erro** textbox toocopy todos os Olá tooshare de detalhes de notificação com um engenheiro de suporte ou produto de grupo

    -   Exemplo – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Próximas etapas
[Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo](active-directory-application-proxy-sso-using-kcd.md)

