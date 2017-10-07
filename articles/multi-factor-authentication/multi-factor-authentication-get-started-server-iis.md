---
title: "aaaIIS autenticação e o servidor Azure MFA | Microsoft Docs"
description: "Isso é a página de autenticação do Azure multi-factor Olá ajudará na implantação de autenticação do IIS e o servidor Azure multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d1bf1c8a-2c10-4ae6-9f4b-75f0c3df43eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017,it-pro
ms.openlocfilehash: 74bd39c2644e2bca0880baea3824cad4c9215111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-iis-web-apps"></a>Configurar o Servidor de Autenticação Multifator do Azure para aplicativos Web do IIS

Use a seção autenticação IIS Olá Olá servidor Azure multi-Factor Authentication (MFA) tooenable e configurar a autenticação IIS para integração com aplicativos web Microsoft IIS. Olá servidor Azure MFA instala um plug-in que pode filtrar solicitações que estão sendo feitas toohello IIS web server tooadd Azure multi-Factor Authentication. Olá plug-in do IIS fornece suporte para autenticação baseada em formulário e autenticação HTTP integrada do Windows. Confiável que IPS também pode ser configurado tooexempt os endereços IP internos de autenticação de dois fatores.

![Autenticação IIS](./media/multi-factor-authentication-get-started-server-iis/iis.png)

## <a name="using-form-based-iis-authentication-with-azure-multi-factor-authentication-server"></a>Usando a autenticação ISS baseada em formulário com o servidor Azure Multi-Factor Authentication
toosecure um IIS aplicativo que usa a autenticação baseada em formulário da web, instale o hello servidor Azure multi-Factor Authentication no servidor de web IIS hello e configurar Olá servidor por Olá procedimento a seguir:

1. No hello servidor Azure multi-Factor Authentication, clique em ícone de autenticação do IIS Olá no menu esquerdo hello.
2. Clique em Olá **baseado em formulário** guia.
3. Clique em **Adicionar**.
4. variáveis de nome de usuário, senha e domínio toodetect automaticamente, digite Olá URL de logon (como https://localhost/contoso/auth/login.aspx) dentro da caixa de diálogo Configurar automaticamente site hello e clique em **Okey**.
5. Verificar Olá **correspondência do usuário exigir multi-Factor Authentication** caixa se todos os usuários foram ou serão importados para hello servidor e autenticação de fator de toomulti da entidade. Se um número significativo de usuários ainda não foi importado no servidor de saudação e/ou estará isento da autenticação multifator, deixe caixa Olá desmarcada.
6. Se as variáveis de página de saudação não podem ser detectadas automaticamente, clique em **especificar manualmente** na caixa de diálogo Configurar automaticamente site hello.
7. Na caixa de diálogo Adicionar site Olá, insira a página de logon do hello URL toohello no campo de URL de envio de saudação e insira um nome de aplicativo (opcional). nome do aplicativo Hello aparece em relatórios do Azure multi-Factor Authentication e pode ser exibido em mensagens de autenticação SMS ou do aplicativo móvel.
8. Selecione o formato correto de solicitação hello. Isso é definido muito**POST ou GET** para a maioria dos aplicativos web.
9. Digite hello variável de nome de usuário, a variável de senha e domínio (se ele aparece na página de logon de saudação). nomes de saudação toofind de saudação caixas de entrada, navegar toohello a página de logon em um navegador da web, com o botão direito na página de saudação e selecione **Exibir código-fonte**.
10. Verificar Olá **correspondência de usuários exigir Azure multi-Factor Authentication** caixa se todos os usuários foram ou serão importados para hello servidor e autenticação de fator de toomulti da entidade. Se um número significativo de usuários ainda não foi importado no servidor de saudação e/ou estará isento da autenticação multifator, deixe caixa Olá desmarcada.
11. Clique em **avançado** tooreview as configurações avançada, incluindo:

  - Selecionar um arquivo de página de negação personalizado
  - Site de toohello de autenticações bem-sucedidas de cache por um período de tempo usando cookies
  - Selecione se tooauthenticate Olá primário credenciais em um domínio do Windows, diretório LDAP. ou servidor RADIUS.

12. Clique em **Okey** caixa de diálogo de Adicionar site tooreturn toohello.
13. Clique em **OK**.
14. Uma vez Olá URL e variáveis de página forem detectadas ou inseridas e dados do site de saudação é exibido no hello painel baseado em formulário.

## <a name="using-integrated-windows-authentication-with-azure-multi-factor-authentication-server"></a>Usando a autenticação integrada do Windows com o servidor Azure Multi-Factor Authentication
toosecure um IIS web um aplicativo que usa a autenticação HTTP integrada do Windows, instale o hello servidor Azure MFA no servidor de web IIS hello e configure Olá Server com hello etapas a seguir:

1. No hello servidor Azure multi-Factor Authentication, clique em ícone de autenticação do IIS Olá no menu esquerdo hello.
2. Clique em Olá **HTTP** guia.
3. Clique em **Adicionar**.
4. Na caixa de diálogo Adicionar URL Base Olá, insira a URL de saudação do site Olá onde a autenticação HTTP é executada (como http://localhost/owa) e forneça um nome de aplicativo (opcional). nome do aplicativo Hello aparece em relatórios do Azure multi-Factor Authentication e pode ser exibido em mensagens de autenticação SMS ou do aplicativo móvel.
5. Ajuste máximo e tempo limite de ociosidade Olá horas de sessão se saudação padrão não é suficiente.
6. Verificar Olá **correspondência do usuário exigir multi-Factor Authentication** caixa se todos os usuários foram ou serão importados para hello servidor e autenticação de fator de toomulti da entidade. Se um número significativo de usuários ainda não foi importado no servidor de saudação e/ou estará isento da autenticação multifator, deixe caixa Olá desmarcada.
7. Verificar Olá **cache de Cookie** caixa se desejar.
8. Clique em **OK**.

## <a name="enable-iis-plug-ins-for-azure-multi-factor-authentication-server"></a>Habilitar Plug-ins IIS para servidor Azure Multi-Factor Authentication
Depois de configurar Olá baseado em formulário ou URLs de autenticação HTTP e configurações, selecione Olá locais onde Olá plug-ins do IIS do Azure multi-Factor Authentication deve ser carregado e habilitada no IIS. Use Olá procedimento a seguir:

1. Se executado no IIS 6, clique em Olá **ISAPI** guia. Site selecione Olá Olá aplicativo web está em execução em (por exemplo, Site padrão) tooenable hello Azure multi-Factor Authentication filtro ISAPI plug-in para o site.
2. Se em execução no IIS 7 ou superior, clique em Olá **módulo nativo** guia. Selecione o servidor de saudação, sites ou aplicativos tooenable Olá plug-in IIS nos níveis de saudação desejado.
3. Clique em Olá **autenticação IIS habilitar** caixa na parte superior de saudação da tela hello. Autenticação multifator do Azure agora está protegendo o aplicativo do IIS Olá selecionado. Certifique-se de que os usuários foram importados no servidor de saudação.

## <a name="trusted-ips"></a>IPs confiáveis
Olá IPs confiáveis permite que os usuários toobypass Azure multi-Factor Authentication para solicitações de sites provenientes de específico de endereços IP ou sub-redes. Por exemplo, convém tooexempt usuários do Azure multi-Factor Authentication durante o logon do office de hello. Para isso, você deve especificar a sub-rede de escritório hello como uma entrada de IPs confiáveis. tooconfigure IPs confiáveis, use Olá procedimento a seguir:

1. Na seção autenticação IIS do hello, clique em Olá **IPs confiáveis** guia.
2. Clique em **Adicionar**.
3. Quando for exibida a caixa de diálogo Adicionar IPs confiáveis hello, selecione Olá **IP único**, **intervalo IP**, ou **sub-rede** botão de opção.
4. Insira o endereço IP hello, intervalo de endereços IP ou sub-rede que deve estar na lista de permissões. Se inserir uma sub-rede, selecione Olá apropriado a máscara de rede e clique em **Okey**. lista branca de saudação foi adicionada.
