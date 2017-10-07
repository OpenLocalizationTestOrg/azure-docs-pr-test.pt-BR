---
title: "aaaSecurity práticas recomendadas para MFA | Microsoft Docs"
description: "Este documento fornece as práticas recomendadas sobre o uso do Azure MFA com contas do Azure"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3be7d968-96bb-4320-8701-869fd04a2595
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 7f18c2592764878b842d81783b321a05f29ee3d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-using-azure-multi-factor-authentication-with-azure-ad-accounts"></a>Práticas recomendadas de segurança para o uso do Azure Multi-Factor Authentication com contas do AD do Azure

Verificação em duas etapas é a opção de saudação preferida para a maioria das organizações que desejam tooenhance seu processo de autenticação. O MFA (Azure Multi-Factor Authentication) ajuda as empresas a atenderem aos seus requisitos de segurança e conformidade, ao mesmo tempo que fornece uma experiência de conexão simples para seus usuários. Este artigo aborda algumas dicas que você deve considerar ao planejar para a adoção de saudação do Azure MFA.

## <a name="deploy-azure-mfa-in-hello-cloud"></a>Implantar o Azure MFA na nuvem Olá

Há duas maneiras tooenable Azure MFA para todos os usuários.

* Comprar licenças para cada usuário (o MFA do Azure, Azure AD Premium, ou Enterprise Mobility + Security)
* Criar um provedor de autenticação multifator e pagamento por usuário ou por autenticação

### <a name="licenses"></a>Licenças
![EMS](./media/multi-factor-authentication-security-best-practices/ems.png)

Se você tiver o Azure AD Premium ou licenças do Enterprise Mobility + Segurança, você já tem o Azure MFA. Usuários do tooextend nada adicionais Olá em duas etapas verificação recurso tooall não precisa de sua organização. Você só precisa tooassign um usuário de tooa de licença e, em seguida, você pode ativar MFA.

Ao configurar a autenticação multifator, considere Olá dicas a seguir:

* Não crie um provedor de autenticação por autenticação multifator. Se você fizer isso, poderá acabar pagando solicitações de verificação de usuários que já têm licenças.
* Se você não possui licenças suficientes para todos os usuários, você pode criar uma pausa de saudação por usuário provedor de autenticação multifator toocover da sua organização. 
* O Azure AD Connect só será exigido se você estiver sincronizando o ambiente do Active Directory local com um diretório do Azure AD. Se você usar apenas um diretório do AD do Azure que não está sincronizado com uma instância local do Active Directory, você não precisará do Azure AD Connect.

### <a name="multi-factor-auth-provider"></a>Provedor de Multi-Factor Authentication
![Provedor de Multi-Factor Authentication](./media/multi-factor-authentication-security-best-practices/authprovider.png)

Se você não tiver licenças que incluem o MFA do Azure, poderá criar um Provedor de Autenticação do MFA. 

Ao criar hello provedor de autenticação, você precisa tooselect um diretório e considere Olá detalhes a seguir:

* Não é necessário um toocreate de diretório do AD do Azure um provedor de autenticação multifator, mas você obtém mais funcionalidade com um. Olá recursos a seguir é habilitado quando você associar Olá provedor de autenticação um diretório do AD do Azure:  
  * Estender tooall de verificação em duas etapas que os usuários  
  * Oferece recursos adicionais, como o portal de gerenciamento hello, saudações personalizadas e relatórios de seus administradores globais.
* Se você sincronizar o ambiente do Active Directory local com um diretório do Azure AD, precisará do DirSync ou do AAD Sync. Se você usa apenas um diretório do AD do Azure que não está sincronizado com uma instância local do Active Directory, não haverá necessidade do DirSync ou AAD Sync.
* Escolha o modelo de consumo de hello mais adequada aos seus negócios. Quando você seleciona o modelo de uso do hello, você não pode alterá-lo. Olá dois modelos são:
  * Por autenticação: cobra para cada verificação. Use esse modelo se desejar verificação em duas etapas para qualquer pessoa que acessa um determinado aplicativo, não para usuários específicos.
  * Por usuário habilitado: cobra para cada usuário que você habilita para o Azure MFA. Use esse modelo se você tiver alguns usuários com licenças de Enterprise Mobility Suite ou Azure AD Premium e outros sem licenças.

### <a name="supportability"></a>Capacidade de suporte
Como a maioria dos usuários estão acostumados toousing senhas somente tooauthenticate, é importante que sua empresa agrega reconhecimento tooall usuários sobre esse processo. Esse reconhecimento pode reduzir a probabilidade de saudação que os usuários chamar o suporte técnico para tooMFA de pequenos problemas relacionados. No entanto, existem alguns cenários em que é necessário desabilitar temporariamente o MFA. Saudação de uso a seguir como diretrizes toounderstand toohandle esses cenários:

* Treine seus cenários de toohandle da equipe de suporte técnico onde os usuário Olá não pode entrar porque o aplicativo móvel hello ou telefone não está recebendo uma chamada telefônica ou uma notificação. O suporte técnico pode [permitir um desvio único](multi-factor-authentication-whats-next.md#one-time-bypass) tooallow tooauthenticate um usuário uma vez por "Ignorar" verificação em duas etapas. Olá bypass é temporário e expira após um número especificado de segundos.
* Considere Olá [IPs confiáveis recurso](multi-factor-authentication-whats-next.md#trusted-ips) no Azure MFA como uma verificação de duas etapas toominimize maneira. Com esse recurso, os administradores de um locatário gerenciado ou federado podem ignorar a verificação em duas etapas para usuários que estão entrando pela intranet local da empresa hello. Olá estão disponíveis para locatários do AD do Azure que têm licenças do Azure AD Premium, o Enterprise Mobility Suite ou do Azure multi-Factor Authentication.

## <a name="best-practices-for-an-on-premises-deployment"></a>Práticas recomendadas para a implantação no local
Se sua empresa decidiu tooleverage tooenable sua própria infraestrutura MFA, você precisa toodeploy um servidor Azure multi-Factor Authentication local. componentes de servidor MFA de saudação são mostrados em Olá diagrama a seguir:

![Componentes padrão do Servidor MFA: console, mecanismo de sincronização, portal de gerenciamento, serviço de nuvem](./media/multi-factor-authentication-security-best-practices/server.png) \*Não instalado por padrão \**Instalado, mas não habilitado por padrão

O Servidor de Autenticação Multifator do Azure pode proteger os recursos da nuvem e locais usando a federação. Você deve ter o AD FS e torná-lo federado com seu locatário do Azure AD.
Ao configurar o servidor multi-Factor Authentication, considere Olá detalhes a seguir:

* Se estiver protegendo recursos AD Azure usando os serviços de Federação do Active Directory (AD FS), a primeira etapa de verificação Olá será executada no local usando o AD FS. Olá segunda etapa é realizado no local, cumprindo a declaração de saudação.
* Você não tem tooinstall hello Azure multi-Factor Authentication Server seu servidor de Federação do AD FS. No entanto, a saudação adaptador do multi-Factor Authentication para o AD FS deve ser instalada em um Windows Server 2012 R2 em execução do AD FS. Você pode instalar o servidor de saudação em um computador diferente, como é uma versão com suporte e instalar o adaptador do hello AD FS separadamente no servidor de Federação do AD FS. 
* Assistente de instalação do adaptador do multi-Factor Authentication AD FS Olá cria um grupo de segurança chamado PhoneFactor Admins no Active Directory e, em seguida, adiciona seu grupo de toothis de conta de serviço do AD FS. Verifique se Olá grupo PhoneFactor Admins foi criado no controlador de domínio, conta de serviço Olá AD FS é um membro desse grupo. Se necessário, adicione manualmente toohello de conta de serviço de saudação do AD FS grupo PhoneFactor Admins no controlador de domínio.

### <a name="user-portal"></a>Portal do Usuário
portal do usuário Olá permite recursos de autoatendimento e fornece um conjunto completo de recursos de administração de usuário. Ele é executado em um site do IIS (Internet Information Server). Use este componente de Olá tooconfigure diretrizes a seguir:

* Use o IIS 6 ou superior
* Instalar e registrar o ASP.NET v2.0.507207
* Garanta que esse servidor possa ser implantado em uma rede de perímetro

### <a name="app-passwords"></a>Senhas de aplicativo
Se sua organização for federada para o SSO com o Azure AD e vai toobe usando o Azure MFA, em seguida, esteja atento Olá detalhes a seguir:

* senha de aplicativo Hello é verificada pelo AD do Azure e, portanto, ignora federação. A federação é usada apenas durante a configuração de senhas de aplicativo.
* Para os usuários federados (SSO), as senhas são armazenadas na id organizacional hello. Se o usuário Olá deixa a empresa hello, essas informações tem tooflow tooorganizational id usando o DirSync. Desabilitar/excluir a conta pode levar até toothree horas toosync, o que atrasa a desabilitação/exclusão de senhas de aplicativo no AD do Azure.
* As configurações do Controle de Acesso do Cliente local não são consideradas pela senha de aplicativo.
* Nenhum recurso de registro/auditoria de autenticação local está disponível para senhas de aplicativo.
* Alguns projetos arquitetônicos avançados podem exigir o uso de uma combinação de nome de usuário e senhas da organização e senhas de aplicativo ao usar a verificação em duas etapas com os clientes, dependendo de onde eles se autenticam. Para clientes que fazem a autenticação em uma infraestrutura local, você usaria um nome de usuário e senha organizacional. Para clientes que autenticam no Azure AD, você usaria a senha de aplicativo hello.
* Por padrão, os usuários não podem criar senhas de aplicativo. Se você precisar de senhas de aplicativo tooallow usuários toocreate, selecione Olá **permitem que os usuários toocreate aplicativo senhas toosign em aplicativos sem navegador** opção.

## <a name="additional-considerations"></a>Considerações adicionais
Use esta lista para obter outras considerações e diretrizes para cada componente implantado localmente:

- Configure a Autenticação Multifator do Azure com o [Serviço de Federação do Active Directory](multi-factor-authentication-get-started-adfs.md).
- Instalar e configurar o hello servidor Azure MFA com [autenticação RADIUS](multi-factor-authentication-get-started-server-radius.md).
- Instalar e configurar o hello servidor Azure MFA com [autenticação IIS](multi-factor-authentication-get-started-server-iis.md).
- Instalar e configurar o hello servidor Azure MFA com [autenticação do Windows](multi-factor-authentication-get-started-server-windows.md).
- Instalar e configurar o hello servidor Azure MFA com [autenticação LDAP](multi-factor-authentication-get-started-server-ldap.md).
- Instalar e configurar o hello servidor Azure MFA com [Gateway de área de trabalho remota e servidor Azure multi-Factor Authentication usando RADIUS](multi-factor-authentication-get-started-server-rdg.md).
- Instalar e configurar a sincronização entre hello servidor Azure MFA e [do Active Directory do Windows Server](multi-factor-authentication-get-started-server-dirint.md).
- [Implantar Olá aplicativo Web serviço do Azure multi-Factor Authentication Server Mobile](multi-factor-authentication-get-started-server-webservice.md).
- [Configuração de VPN com autenticação multifator do Azure avançada](multi-factor-authentication-advanced-vpn-configurations.md) para dispositivos Cisco ASA Netscaler da Citrix e Juniper/Pulse Secure VPN usando o LDAP ou RADIUS.

## <a name="next-steps"></a>Próximas etapas
Embora este artigo destaque algumas práticas recomendadas para o Azure MFA, há outros recursos que você também pode usar ao planejar sua implantação do MFA. lista de saudação abaixo tem alguns artigos principais que podem ajudá-lo durante esse processo:

* [Relatórios no Azure Multi-Factor Authentication](multi-factor-authentication-manage-reports.md)
* [experiência de registro de verificação de duas etapas Olá](multi-factor-authentication-end-user-first-time.md)
* [Perguntas frequentes sobre o Azure Multi-Factor Authentication](multi-factor-authentication-faq.md)

