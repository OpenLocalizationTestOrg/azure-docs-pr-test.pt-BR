---
title: "aplicativos de toocloud aaaManage acesso restringindo locatários - Azure | Microsoft Docs"
description: "Como toouse locatário restrições toomanage quais usuários podem acessar aplicativos com base em seu locatário do AD do Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: kgremban
ms.openlocfilehash: 6470fa217738b29104353ae17a2f53216f825c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-tenant-restrictions-toomanage-access-toosaas-cloud-applications"></a>Use restrições de locatário toomanage acesso tooSaaS aplicativos em nuvem

Organizações de grandes porte que enfatizam segurança desejam toomove toocloud serviços como o Office 365, mas aprovada de tooknow necessário que os usuários só podem acessar recursos. Tradicionalmente, as empresas restringem endereços IP ou nomes de domínio quando desejarem toomanage acesso. Essa abordagem falha em um mundo em que os aplicativos de SaaS são hospedados em uma nuvem pública e são executados em nomes de domínio compartilhados como outlook.office.com e login.microsoftonline.com. Bloquear esses endereços manteria os usuários de acessar o Outlook Web hello totalmente, em vez de simplesmente restringindo-os recursos e as identidades de tooapproved.

Desafio de toothis de solução do Azure do Active Directory é um recurso chamado restrições de locatário. Locatário restrições permite que as organizações toocontrol acesso tooSaaS aplicativos, com base no uso de aplicativos de Olá Olá AD do Azure locatário para logon único em nuvem. Por exemplo, convém aplicativos do Office 365 tooallow acesso tooyour organização, evitando instâncias acesso tooother organizações esses mesmos aplicativos.  

Restrições de locatário fornece toospecify de capacidade de organizações Olá Olá a lista de locatários que seus usuários têm permissão tooaccess. AD do Azure, em seguida, concede acesso toothese permitido locatários.

Este artigo se concentra em restrições de locatário para o Office 365, mas o recurso Olá deve funcionar com qualquer aplicativo de nuvem SaaS que usa protocolos de autenticação moderna com o Azure AD para logon único. Se você usar SaaS aplicativos com um AD Azure diferentes de locatário de locatário Olá usado pelo Office 365, certifique-se de que todos os necessários locatários são permitidos. Para obter mais informações sobre aplicativos de nuvem de SaaS, consulte Olá [Marketplace do Active Directory](https://azure.microsoft.com/en-us/marketplace/active-directory/).

## <a name="how-it-works"></a>Como ele funciona

Olá geral solução inclui Olá componentes a seguir: 

1. **O AD do Azure** – se hello `Restrict-Access-To-Tenants: <permitted tenant list>` está presente, o Azure AD somente tokens de segurança de problemas para Olá permitido locatários. 

2. **Infraestrutura de servidor proxy local** – um dispositivo de proxy capaz de inspeção SSL, o cabeçalho de saudação configurado tooinsert que contém a lista de saudação do permitido locatários para o tráfego destinado para o AD do Azure. 

3. **Software cliente** – toosupport restrições de locatário, o software cliente deve solicitar tokens de diretamente do AD do Azure, para que o tráfego pode ser interceptado por infraestrutura do proxy de saudação. As Restrições de Locatário atualmente têm suporte pelos aplicativos do Office 365 baseados no navegador e pelos clientes do Office quando a autenticação moderna (como OAuth 2.0) é usada. 

4. **Autenticação moderna** – serviços de nuvem devem usar a autenticação moderna toouse restrições de locatário e bloquear o acesso a tooall não permitido locatários. Serviços do Office 365 nuvem devem ser protocolos de autenticação moderna toouse configurado por padrão. Para obter informações mais recentes sobre o suporte do Office 365 para autenticação moderna hello, ler [autenticação moderna atualizado do Office 365](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/).

Olá diagrama a seguir ilustra o fluxo de tráfego de alto nível de saudação. Inspeção SSL é necessário apenas no tráfego tooAzure AD, não toohello Office 365 serviços em nuvem. Essa distinção é importante porque o volume de tráfego de saudação para autenticação tooAzure AD é geralmente muito menor do que o tráfego volume tooSaaS aplicativos, como o Exchange Online e o SharePoint Online.

![Fluxo de tráfego de Restrições de Locatário – diagrama](./media/active-directory-tenant-restrictions/traffic-flow.png)

## <a name="set-up-tenant-restrictions"></a>Configurar as Restrições de Locatário

Há dois tooget etapas iniciado com restrições de locatário. Olá primeira etapa é toomake-se de que os clientes podem se conectar a endereços direito toohello. Olá segundo é tooconfigure sua infraestrutura do proxy.

### <a name="urls-and-ip-addresses"></a>URLs e endereços IP

toouse restrições de locatário, seus clientes devem ser capaz de tooconnect toohello tooauthenticate do AD do Azure URLs a seguir: login.microsoftonline.com, login.microsoft.com e login.windows.net. Além disso, tooaccess Office 365, os clientes também devem ser capaz de tooconnect toohello FQDNs/URLs e endereços IP definido no [intervalos de endereços IP e URLs do Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2). 

### <a name="proxy-configuration-and-requirements"></a>Requisitos e configuração de proxy

Olá configuração a seguir é necessário tooenable restrições de locatário por meio de sua infraestrutura do proxy. Essa orientação é genérica, você deverá consultar a documentação do fornecedor de proxy tooyour para etapas de implementação específica.

#### <a name="prerequisites"></a>Pré-requisitos

- proxy de saudação deve ser capaz de tooperform interceptação de SSL, inserção do cabeçalho HTTP e destinos de filtro usando FQDNs/URLs. 

- Os clientes devem confiar cadeia de certificados Olá apresentada pelo proxy Olá para comunicações SSL. Por exemplo, se forem usados certificados de uma PKI interna, Olá interno emissora certificado certificado de autoridade raiz deve ser confiável.

- Esse recurso está incluído nas assinaturas do Office 365, mas se desejar que os aplicativos de SaaS toouse locatário restrições toocontrol acesso tooother, em seguida, licenças do Azure AD Premium 1 são necessárias.

#### <a name="configuration"></a>Configuração

Para cada toologin.microsoftonline.com de solicitação de entrada, login.microsoft.com e login.windows.net, inserir dois cabeçalhos HTTP: *acesso restrito de locatários* e *contexto de acesso restrito*.

cabeçalhos de saudação devem incluir Olá elementos a seguir: 
- Para *acesso restrito de locatários*, um valor de \<permitido lista locatário\>, que é uma lista separada por vírgulas de locatários, você deseja tooallow tooaccess de usuários. Qualquer domínio que está registrado com um locatário pode ser locatário de saudação tooidentify usado nesta lista. Por exemplo, toopermit acessar tooboth inquilinos da Contoso e Fabrikam, Olá parece do par nome/valor que:`Restrict-Access-To-Tenants: contoso.onmicrosoft.com,fabrikam.onmicrosoft.com` 
- Para *contexto de acesso restrito*, um valor de uma ID de diretório único, declarando que locatário é definir restrições de locatário de saudação. Por exemplo, toodeclare Contoso como locatário Olá que defina Olá diretiva restrições de locatário, par de nome/valor Olá aparência:`Restrict-Access-Context: 456ff232-35l2-5h23-b3b3-3236w0826f3d`  

> [!TIP]
> Você pode encontrar sua ID de diretório no hello [portal do Azure](https://portal.azure.com). Entre como administrador, selecione **Azure Active Directory** e selecione **Propriedades**.

tooprevent usuários de inserir seu próprio cabeçalho HTTP com locatários não aprovado, proxy Olá precisa de cabeçalho de acesso restrito de locatários Olá tooreplace se ele já está presente na solicitação de entrada hello. 

Os clientes devem ser forçado toouse Olá proxy para todas as solicitações toologin.microsoftonline.com, login.microsoft.com e login.windows.net. Por exemplo, se arquivos PAC são usadas toodirect clientes toouse Olá proxy, os usuários finais não deve ser capaz de tooedit ou desabilitar arquivos Olá PAC.

## <a name="hello-user-experience"></a>experiência do usuário Olá

Esta seção mostra a experiência de saudação para usuários finais e administradores.

### <a name="end-user-experience"></a>Experiência do usuário final

Um usuário de exemplo é na rede de Contoso hello, mas está tentando tooaccess Olá Fabrikam instância de um compartilhado SaaS aplicativo como o Outlook online. Se Contoso é um locatário não permitido para essa instância, o usuário Olá vê Olá página a seguir:

![Página de acesso negado para usuários em locatários não permitido](./media/active-directory-tenant-restrictions/end-user-denied.png)

### <a name="admin-experience"></a>Experiência de admin

Enquanto a configuração de restrições de locatário é feita na infraestrutura do proxy corporativo Olá, administradores podem acessar relatórios locatário restrições Olá Olá portal do Azure diretamente. Olá tooview relatórios, acesse a página de visão geral do Azure Active Directory toohello e procure 'Outras funcionalidades'.

Olá administrador locatário Olá especificado como locatário Olá contexto de acesso restrito pode usar este toosee relatório todas as entradas bloqueada devido a saudação diretiva de restrições de locatário, incluindo identidade de saudação usada e ID de diretório de destino de saudação.

![Use hello Azure tooview portal restringido nas tentativas de entrar](./media/active-directory-tenant-restrictions/portal-report.png)

Como outros relatórios no hello portal do Azure, você pode usar filtros toospecify Olá escopo do relatório. Você pode filtrar um usuário, aplicativo, cliente ou intervalo de tempo específico.

## <a name="office-365-support"></a>Suporte ao Office 365

Aplicativos do Office 365 devem atender aos suporte de toofully dois critérios restrições de locatário:

1. cliente Olá usado dá suporte a autenticação moderna
2. Autenticação moderna está habilitada como protocolo de autenticação padrão Olá Olá serviço de nuvem.

Consulte também[autenticação moderna atualizado do Office 365](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/) para obter informações mais recentes de saudação em qual Office clientes atualmente suportam a autenticação moderna. Essa página também inclui links tooinstructions para habilitar a autenticação moderna em específicas do Exchange Online e Skype para locatários Business Online. A autenticação moderna já está habilitada por padrão no SharePoint Online.

Restrições de locatário é suportado atualmente por aplicativos do Office 365 com base em navegador (Olá do SharePoint do Portal do Office, Yammer, sites, Outlook em Olá Web, etc.). Para clientes espessos (Outlook, Skype for Business, Word, Excel, PowerPoint etc.) As Restrições de Locatário podem ser aplicadas somente quando a autenticação moderna é usada.  

Outlook e o Skype para clientes de negócios que suportam a autenticação moderna são protocolos herdados de toouse ainda poderá contra locatários onde a autenticação moderna não está habilitada, efetivamente ignorar restrições de locatário. Para o Outlook no Windows, os clientes podem escolher restrições tooimplement impedindo que os usuários finais adicionando perfis de tootheir de contas de email não aprovado. Por exemplo, consulte Olá [evitar a adição de contas do Exchange não padrão](http://gpsearch.azurewebsites.net/default.aspx?ref=1) configuração de política de grupo. No momento, não há suporte completo para Restrições de Locatário para o Outlook em plataformas não Windows e para Skype for Business em nenhuma plataforma.

## <a name="testing"></a>Testando

Se você quiser tootry out locatário restrições antes de implementá-lo para toda a organização, há duas opções: uma abordagem baseada em host usando uma ferramenta como o Fiddler ou uma distribuição pré-configurada de configurações de proxy.

### <a name="fiddler-for-a-host-based-approach"></a>Fiddler para uma abordagem baseada em host

O Fiddler é uma web gratuita proxy que pode ser usado toocapture e modificam o tráfego HTTP/HTTPS, inclusive Inserir cabeçalhos HTTP de depuração. tooconfigure Fiddler tootest restrições de locatário, execute Olá etapas a seguir:

1.  [Baixe e instale o Fiddler](http://www.telerik.com/fiddler).
2.  Configurar o tráfego HTTPS do Fiddler toodecrypt, por [a documentação de Ajuda do Fiddler](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS).
3.  Configurar saudação do Fiddler tooinsert *acesso restrito de locatários* e *contexto de acesso restrito* cabeçalhos usando regras personalizadas:
  1. Na ferramenta do Fiddler Web Debugger hello, selecione Olá **regras** menu e selecione **personalizar regras...** arquivo de CustomRules de saudação tooopen.
  2. Adicionar Olá linhas no início de saudação do hello seguintes *OnBeforeRequest* função. Substitua \<tenant domain\> por um domínio registrado com seu locatário, por exemplo, contoso.onmicrosoft.com. Substitua \<directory ID\> pelo identificador de GUID do Azure AD do locatário.

  ```
  if (oSession.HostnameIs("login.microsoftonline.com") || oSession.HostnameIs("login.microsoft.com") || oSession.HostnameIs("login.windows.net")){      oSession.oRequest["Restrict-Access-To-Tenants"] = "<tenant domain>";      oSession.oRequest["Restrict-Access-Context"] = "<directory ID>";}
  ```

  Se você precisar tooallow vários locatários, use nomes de locatário uma vírgula tooseparate hello. Por exemplo:

  ```
  oSession.oRequest["Restrict-Access-To-Tenants"] = "contoso.onmicrosoft.com,fabrikam.onmicrosoft.com";
  ```

4. Salve e feche o arquivo de CustomRules hello.

Depois de configurar o Fiddler, você pode capturar o tráfego por vai toohello **arquivo** menu e selecionando **capturar tráfego**.

### <a name="staged-rollout-of-proxy-settings"></a>Distribuição em etapas as configurações de proxy

Dependendo de recursos de saudação da sua infraestrutura do proxy, você pode ser toostage capaz de distribuição de saudação de configurações que os usuários tooyour. Aqui estão algumas opções de alto nível para consideração:

1.  Use PAC arquivos toopoint teste usuários tooa teste infraestrutura do proxy, enquanto os usuários normais continuam a infraestrutura de proxy de produção de hello toouse.
2.  Alguns servidores proxy podem dar suporte a configurações diferentes usando grupos.

Consulte a documentação do servidor proxy tooyour para obter detalhes específicos.

## <a name="next-steps"></a>Próximas etapas

- Leia sobre a [Updated Office 365 modern authentication](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/) (Autenticação moderna do Office 365 atualizada)

- Saudação de revisão [intervalos de endereços IP e URLs do Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
