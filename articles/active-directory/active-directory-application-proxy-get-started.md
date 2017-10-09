---
title: aplicativos de locais tooon aaaHow tooprovide acesso remoto seguro
description: Aborda como toouse tooyour de acesso remoto seguro de tooprovide de Proxy de aplicativo do Azure AD local aplicativos.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d5450da1-9e06-4d08-8146-011c84922ab5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 289e970ed0596fcd06ccf6b2ad92203366fbb494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprovide-secure-remote-access-tooon-premises-applications"></a>Como tooprovide proteger o acesso remoto aplicativos tooon locais

Os funcionários hoje devem toobe produtivos em qualquer lugar, a qualquer momento e de qualquer dispositivo. Eles querem toowork em seus próprios dispositivos, independentemente de estarem tablets, celulares ou laptops. E eles esperam tooaccess capaz de toobe todos os seus aplicativos, aplicativos SaaS em nuvem hello e aplicativos corporativos no local. Fornecer acesso a aplicativos locais tooon tradicionalmente tem envolvidos redes virtuais privadas (VPNs) ou zonas desmilitarizada (DMZs). Não só são esses toomake complexos e difíceis de soluções seguras, mas eles são cara tooset backup e gerenciar.

Há uma opção melhor!

Uma força de trabalho moderna no primeiro mobile Olá, mundo de nuvem, primeiro precisa de uma solução modernos de acesso remoto. O Proxy de Aplicativo do Azure AD é um recurso do Azure Active Directory que oferece acesso remoto como um serviço. Isso significa que é fácil toodeploy, usar e gerenciar.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="what-is-azure-active-directory-application-proxy"></a>O que é o Proxy de Aplicativo do Active Directory do Azure?
O Proxy de Aplicativo Azure AD fornece SSO (logon único) e acesso remoto seguro para aplicativos da Web hospedados no local. Alguns aplicativos que você esperaria toopublish incluem sites do SharePoint, Outlook Web Access ou qualquer outro aplicativo de web LOB que você tem. Essas web local aplicativos estão integrados ao AD do Azure, Olá a mesma identidade e controle de plataforma que é usada pelo O365. Os usuários finais podem acessar a saudação de aplicativos local mesma maneira que acessam o O365 e outros aplicativos SaaS integrada ao AD do Azure. Você não precisará de infraestrutura de rede Olá toochange ou exigem VPN tooprovide esta solução para seus usuários.

## <a name="why-is-application-proxy-a-better-solution"></a>Por que o Proxy de Aplicativo é uma solução melhor?
Proxy de aplicativo do Azure AD fornece um tooall de solução de acesso remoto seguro, simples e econômica seus aplicativos locais.

O Proxy de Aplicativo do Azure AD é:

* **Simples**
   * Você não precisa toochange ou atualizar toowork seus aplicativos com Proxy de aplicativo. 
   * Os usuários obtêm uma experiência de autenticação consistente. Eles podem usar aplicativos de SaaS tooboth Olá MyApps tooget portal SSO em seus aplicativos locais e de nuvem de saudação. 
* **Proteger**
   * Quando você publicar seus aplicativos usando o Proxy de aplicativo do Azure AD, você pode tirar proveito de controles de rich autorização hello e análise de segurança no Azure. Você obtém segurança de escala de nuvem e recursos de segurança do Azure como verificação em duas etapas e acesso condicional.
   * Você não tem tooopen conexões de entrada por meio de seu firewall toogive seus usuários de acesso remoto. 
* **Econômico**
   * Proxy de aplicativo funciona em nuvem hello, portanto você pode economizar tempo e dinheiro. Soluções locais geralmente exigem tooset backup e mantém DMZs, servidores de borda ou outras infra-estruturas complexas.  

## <a name="what-kind-of-applications-work-with-application-proxy"></a>Quais tipos de aplicativos funcionam com o Proxy de Aplicativo?
Com o Proxy de Aplicativo Azure AD, você pode acessar diferentes tipos de aplicativos internos:

* Aplicativos Web que usam a [Autenticação Integrada do Windows](active-directory-application-proxy-sso-using-kcd.md) para autenticação  
* Aplicativos Web que usam o acesso baseado em formulário ou [baseado em cabeçalho](application-proxy-ping-access.md)  
* APIs que você deseja tooexpose toorich aplicativos em dispositivos diferentes da Web  
* Aplicativos hospedados por trás de um [Gateway de Área de Trabalho Remota](application-proxy-publish-remote-desktop.md)  
* Aplicativos cliente avançados que são integrados com hello biblioteca de autenticação do Active Directory (ADAL)

## <a name="how-does-application-proxy-work"></a>Como o Proxy de Aplicativo funciona?
Há dois componentes que você precisa tooconfigure toomake trabalho de Proxy de aplicativo: um conector e um ponto de extremidade externo. 

conector de saudação é um agente leve que se encontra em um servidor Windows dentro de sua rede. conector de Olá facilita o fluxo de tráfego de saudação do hello serviço de Proxy de aplicativo hello nuvem tooyour aplicativo localmente. Ele usa apenas conexões de saída, para que você não tem tooopen portas de entrada ou coloque tudo na rede de Perímetro hello. conectores de saudação são sem monitoração de estado e obtém informações de nuvem Olá conforme necessário. Para obter mais informações sobre conectores, como eles fazem o balanceamento de carga e a autenticação, consulte [Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD](application-proxy-understand-connectors.md). 

ponto de extremidade externo Olá é como aos usuários acessar seus aplicativos enquanto fora da sua rede. Eles poderão ou acessar diretamente tooan URL externa que você determinar ou acessar aplicativo hello por meio do portal MyApps hello. Quando os usuários vão tooone desses pontos de extremidade, eles autenticar no AD do Azure e, em seguida, são roteados através de aplicativo do hello conector toohello local.

 ![Diagrama do Proxy de Aplicativo do Azure](./media/active-directory-application-proxy-get-started/azureappproxxy.png)

1. usuário Olá acessa o aplicativo hello por meio de saudação serviço Proxy de aplicativo e é tooauthenticate de página de entrada do AD do Azure toohello direcionado.
2. Após um bem-sucedido logon, um token é gerado e enviado toohello dispositivo de cliente.
3. cliente Olá envia Olá token toohello serviço de Proxy de aplicativo, que recupera o nome principal de usuário de saudação (UPN) e nome principal de segurança (SPN) do token Olá, em seguida, direciona o conector de Proxy de aplicativo hello solicitação toohello.
4. Se você tiver configurado o logon único, o conector de saudação realiza nenhuma autenticação adicional necessária em nome de usuário de saudação.
5. conector de saudação envia aplicativo local do hello solicitação toohello.  
6. Olá resposta será enviada pelo usuário de toohello de serviço e o conector de Proxy de aplicativo.

### <a name="single-sign-on"></a>Logon único
Proxy de aplicativo do AD do Azure fornece logon único (SSO) tooapplications que usam Windows IWA (autenticação integrada) ou aplicativos com reconhecimento de declarações. Se seu aplicativo usa a IWA, o Proxy de aplicativo representa usuário hello usando a delegação restrita de Kerberos tooprovide SSO. Se você tiver um aplicativo com reconhecimento de declaração de confiança do Active Directory do Azure, o SSO funciona porque o usuário Olá já foi autenticado pelo AD do Azure.

Para obter mais informações sobre o Kerberos, consulte [tudo o que você deseja tooknow sobre delegação de restrita de Kerberos (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

### <a name="managing-apps"></a>Gerenciando aplicativos
Um aplicativo é publicado com o Proxy de aplicativo, você pode gerenciá-lo como qualquer outro aplicativo de enterprise Olá portal do Azure. Você pode usar recursos de segurança do Active Directory do Azure como verificação de duas etapas e de acesso condicional, controlar permissões de usuário e personalizar identidade visual Olá para seu aplicativo. 

## <a name="get-started"></a>Introdução

Antes de configurar o Proxy de Aplicativo, verifique se você tem uma [edição do Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/) com suporte e um diretório do Azure AD do qual você é um administrador global.

Introdução ao Proxy de Aplicativo em duas etapas:

1. [Habilitar Proxy de aplicativo e configurar o conector Olá](active-directory-application-proxy-enable.md).    
2. [Publicar aplicativos](active-directory-application-proxy-publish.md) -use Olá seus aplicativos locais publicados e acessíveis de assistente rápida e fácil tooget remotamente.

## <a name="whats-next"></a>O que vem a seguir?
Depois de publicar seu primeiro aplicativo, há muito mais você pode fazer com o Proxy de Aplicativo:

* [Habilitar o logon único](active-directory-application-proxy-sso-using-kcd.md)
* [Publicar aplicativos usando seu próprio nome de domínio](active-directory-application-proxy-custom-domains.md)
* [Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD](application-proxy-understand-connectors.md)
* [Trabalhar com servidores proxy locais existentes](application-proxy-working-with-proxy-servers.md) 
* [Definir uma home page personalizada](application-proxy-office365-app-launcher.md)

Para Olá últimas notícias e atualizações, confira Olá [blog de Proxy de aplicativo](http://blogs.technet.com/b/applicationproxyblog/)

