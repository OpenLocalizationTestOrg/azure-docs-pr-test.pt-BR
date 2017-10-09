---
title: aaaChoose entre o servidor ou de nuvem do Azure MFA | Microsoft Docs
description: "Escolha solução de segurança de autenticação multifator Olá que é ideal para você perguntando, qual am I tentar toosecure e onde estão meus usuários localizado.  Em seguida, escolha nuvem, Servidor MFA ou AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: ec2270ea-13d7-4ebc-8a00-fa75ce6c746d
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: bd9639e5f744f586d9143c6e90b105ed645eecb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-hello-azure-multi-factor-authentication-solution-for-you"></a>Escolha a solução do Azure multi-Factor Authentication Olá para você
Porque há vários tipos do Azure multi-Factor Authentication (MFA), podemos deve responder a algumas toofigure perguntas sobre qual versão é Olá toouse adequada de um.  Essas perguntas são:

* [O que eu estou tentando toosecure](#what-am-i-trying-to-secure)
* [Onde estão localizados os usuários Olá](#where-are-the-users-located)
* [De quais recursos preciso?](#what-featured-do-i-need)

Olá seções a seguir fornecem orientação sobre como determinar cada essas respostas.

## <a name="what-am-i-trying-toosecure"></a>O que eu estou tentando toosecure?
solução de verificação em duas etapas correto do hello toodetermine, primeiro vamos deve responder a pergunta Olá dos quais são toosecure tentar com um segundo método de autenticação.  É um aplicativo no Azure?  Ou um sistema de acesso remoto?  Determinando o que estamos tentando toosecure, pode responder a pergunta de saudação de onde o multi-Factor Authentication precisa toobe habilitado.  

| O que estão tentando toosecure | MFA na nuvem Olá | Servidor MFA |
| --- |:---:|:---:|
| Aplicativos primários da Microsoft |● |● |
| Aplicativos SaaS na Galeria de aplicativo hello |● |  |
| Aplicativos Web publicados por meio da Proxy de Aplicativo do Azure AD |● |  |
| Aplicativos IIS não publicados por meio da Proxy de aplicativo do Azure AD | |● |
| Acesso remoto, como VPN, RDG | ● | ● |

## <a name="where-are-hello-users-located"></a>Onde estão localizados os usuários Olá
Em seguida, observando onde se encontram nossos usuários ajuda toodetermine Olá solução correta toouse, se na nuvem de saudação ou no local usando Olá servidor MFA.

| Local do usuário | MFA na nuvem Olá | Servidor MFA |
| --- |:---:|:---:|
| Azure Active Directory |● | |
| Azure AD e AD local usando federação com AD FS |● |● |
| Azure AD e AD local usando o DirSync, o Azure AD Sync, o Azure AD Connect - sem sincronização de senha |● |● |
| Azure AD e AD local usando o DirSync, o Azure AD Sync, o Azure AD Connect - com sincronização de senha |● | |
| Active Directory local | |● |

## <a name="what-features-do-i-need"></a>De quais recursos preciso?
Hello tabela a seguir compara os recursos de saudação que estão disponíveis com o multi-Factor Authentication na nuvem hello e Olá servidor multi-Factor Authentication.

| Recurso | MFA na nuvem Olá | Servidor MFA |
| --- |:---:|:---:|
| Notificação de aplicativo móvel como um segundo fator | ● | ● |
| Código de verificação de aplicativo móvel como um segundo fator | ● | ● |
| Chamada telefônica como um segundo fator | ● | ● |
| SMS unidirecional como segundo fator | ● | ● |
| SMS bidirecional como segundo fator | | ● |
| Tokens de hardware como segundo fator | | ● |
| Senhas de aplicativos para clientes do Office 365 que não oferecem suporte a MFA | ● | |
| Controle do administrador sobre métodos de autenticação | ● | ● |
| Modo PIN | | ● |
| Alerta de fraude |● | ● |
| Relatórios de MFA |● | ● |
| Desvio único | | ● |
| Saudações personalizadas para chamadas telefônicas | ● | ● |
| ID do chamador personalizável para chamadas telefônicas | ● | ● |
| IPs confiáveis | ● | ● |
| Lembrar MFA para dispositivos confiáveis | ● | |
| Acesso condicional | ● | ● |
| Cache |  | ● |

## <a name="next-steps"></a>Próximas etapas

Agora que determinamos se toouse nuvem Olá servidor MFA local ou autenticação multifator, podemos começar configurando e usando o Azure multi-Factor Authentication. **Selecione o ícone de saudação que representa seu cenário**

<center>




[![Nuvem](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![Servidor](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center>
