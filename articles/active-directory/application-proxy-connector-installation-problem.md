---
title: "Instalando aaaProblem Olá conector de agente de Proxy de aplicativo | Microsoft Docs"
description: "Como tootroubleshoot problemas que você pode Olá de face ao instalar o conector do agente de Proxy de aplicativo"
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
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a>Problema ao instalar o conector do agente de Proxy de aplicativo de saudação

Conector de Proxy de aplicativo Microsoft AAD é um componente de domínio interno que usa conectividade de saudação tooestablish conexões de saída do domínio interno do toohello Olá nuvem ponto de extremidade disponível.

## <a name="general-problem-areas-with-connector-installation"></a>Áreas de problemas gerais com a instalação do conector

Quando ocorre falha na instalação de saudação de um conector, causa Olá é normalmente uma saudação áreas a seguir:

1.  **Conectividade** – toocomplete uma instalação bem sucedida, Olá tooregister de necessidades novo conector e estabelecer as propriedades de confiança futuras. Isso é feito por meio da conexão toohello serviço de nuvem do Proxy de aplicativo do AAD.

2.  **Estabelecimento de confiança** – novo conector de saudação cria um certificado autoassinado e registra o serviço de nuvem toohello.

3.  **Autenticação de Olá administrador** – durante a instalação, a saudação usuário deve fornecer credenciais de administrador de instalação do conector toocomplete hello.

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a>Verifique se o serviço de Proxy de aplicativo de nuvem toohello conectividade e página de Login da Microsoft

**Objetivo:** verificar máquina Olá conector pode conectar-se o ponto de extremidade de registro de Proxy de aplicativo AAD toohello, bem como a página de logon do Microsoft.

1.  Abra uma página da web a seguir de toohello navegador e acesse: <https://aadap-portcheck.connectorporttest.msappproxy.net> , verifique se essa conectividade de saudação tooCentral dos EUA e data centers do Leste dos EUA com portas 9090 e 9091 está funcionando.

2.  Se qualquer uma dessas portas não for bem-sucedida (não tem uma marca de seleção verde), verifique se esse Olá Firewall ou proxy de back-end tem \*. msappproxy.net com portas 9090 e 9091 definidos corretamente.

3.  Abra um navegador (guia separada) e vá toohello página da web a seguir: <https://login.microsoftonline.com>, certifique-se de que você pode fazer logon toothat página.

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a>Verifique se os componentes do computador e de back-end oferecem suporte para certificados de confiança de Application Proxy

**Objetivo:** verificar se o computador do conector hello, proxy de back-end e firewall podem suportam certificado Olá criado pelo conector Olá para futuras de confiança.

>[!NOTE]
>conector de saudação tenta toocreate um certificado de SHA512 com suporte do TLS 1.2. Se a máquina hello ou firewall de back-end hello e proxy não oferece suporte a TLS 1.2, instalação de saudação falhar.
>
>

**problema de saudação tooresolve:**

1.  Verifique se a máquina Olá dá suporte a TLS 1.2 – as versões de todas as janelas após 2012 R2 devem oferecer suporte a TLS 1.2. Se o computador do conector é de uma versão do 2012 R2 ou anterior, certifique-se de que Olá seguintes KBs estão instalados na máquina de saudação: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2>

2.  Contate seu administrador de rede e tooverify que firewall e proxy de back-end de saudação não bloqueiam SHA512 para tráfego de saída.

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a>Verifique se administrador é usado tooinstall Olá conector

**Objetivo:** Verifique se esse usuário Olá que tenta conector de saudação tooinstall é um administrador com as credenciais corretas. No momento, o usuário de saudação deve ser um administrador global para Olá toosucceed de instalação.

**credenciais de saudação do tooverify estão corretas:**

Conecte-se muito<https://login.microsoftonline.com> e use Olá as mesmas credenciais. Certifique-se de saudação logon for bem-sucedido. Você pode verificar a função de usuário Olá indo muito**Active Directory do Azure**  - &gt; **usuários e grupos**  - &gt; **todos os usuários**. 

Selecione sua conta de usuário, em seguida, "função de diretório" no menu resultante hello. Verifique se a função hello selecionado é "Administrador Global". Se você não é possível tooaccess qualquer Olá páginas ao longo dessas etapas, você não for um administrador global.

## <a name="next-steps"></a>Próximas etapas
[Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD](application-proxy-understand-connectors.md)
