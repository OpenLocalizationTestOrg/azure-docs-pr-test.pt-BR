---
title: "Migrar do Serviço de Controle de Acesso do Azure | Microsoft Docs"
description: "Opções para mover aplicativos e serviços do Serviço de Controle de Acesso do Azure"
services: active-directory
documentationcenter: dev-center-name
author: dstrockis
manager: mtillman
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/14/2017
ms.author: dastrock
ms.openlocfilehash: f3de9016fe29a51ab2c7fb9e93fcd33af0f0e871
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="migrate-from-the-azure-access-control-service"></a>Migrar do Serviço de Controle de Acesso do Azure

O Controle de Acesso do Azure, um serviço do Azure Active Directory (Azure AD), será desativado em novembro de 2018. Os aplicativos e serviços que atualmente utilizam o Controle de Acesso devem ser totalmente migrados para um mecanismo de autenticação diferente até esta data. Este artigo descreve recomendações para os clientes atuais, uma vez que você pretende substituir o uso do Controle de Acesso. Se você não estiver usando o Controle de Acesso, não precisa realizar nenhuma ação.


## <a name="overview"></a>Visão geral

O Controle de Acesso é um serviço de autenticação de nuvem que oferece uma maneira fácil de autenticar e autorizar usuários para acesso a seus aplicativos web e serviços. Ele permite que muitos recursos de autenticação e autorização sejam fatorados fora do seu código. O Controle de Acesso é usado principalmente por desenvolvedores e arquitetos de clientes .NET da Microsoft, aplicativos web ASP.NET e serviços web do Windows Communication Foundation (WCF).

Os casos de uso para o Controle de Acesso podem ser subdivididos em três categorias principais:

- Autenticação para certos serviços em nuvem da Microsoft, incluindo o Azure Service Bus e o Dynamics CRM. Os aplicativos clientes obtêm tokens do Controle de Acesso que podem ser usados para autenticar esses serviços para realizar várias ações.
- Adicionar autenticação a aplicativos web, predefinidos (como SharePoint) e personalizados. Usando a autenticação de "passiva" do Controle de Acesso, os aplicativos web podem suportar o logon com uma conta da Microsoft (anteriormente conhecida como Live ID) e contas do Google, Facebook, Yahoo, Azure AD e os Serviços de Federação do Active Directory (AD FS).
- Proteção de serviços web criados personalizados com tokens emitidos pelo Controle de Acesso. Usando a autenticação "ativa", os serviços web podem garantir que eles só permitem o acesso de clientes conhecidos que foram autenticadas com o Controle de Acesso.

Cada um desses casos de uso e as estratégias de migração recomendadas são discutidos nas seções a seguir. 

> [!WARNING]
> Na maioria dos casos, as alterações significativas do código são necessárias para migrar serviços e aplicativos existentes para tecnologias mais novas. Recomendamos que você comece imediatamente a planejar e executar a migração para evitar qualquer possibilidade de interrupções ou tempo de inatividade.

O Controle de Acesso tem os seguintes componentes:

- Um serviço de token de segurança (STS), que recebe solicitações de autenticação e emite tokens de segurança em troca.
- O portal clássico do Azure, onde você cria, exclui e habilita e desabilita namespaces do Controle de Acesso.
- Um portal de gerenciamento do Controle de Acesso separado, onde você pode personalizar e configurar os namespaces de Controle de Acesso.
- Um serviço de gerenciamento, que você pode usar para automatizar as funções dos portais.
- Um mecanismo de regra de transformação de token, que você pode usar para definir a lógica complexa para manipular o formato de saída de tokens emitidos pelo Controle de Acesso.

Para usar esses componentes, você deve criar um ou mais namespaces do Controle de Acesso. Um *namespace* é uma instância dedicada do Controle de Acesso com que seus aplicativos e serviços se comunicam. Um namespace é isolado de todos os outros clientes do Controle de Acesso. Os outros clientes de Controle de Acesso usam seus próprios namespaces. Um namespace do Controle de Acesso tem uma URL dedicada que tem esta aparência:

```HTTP
https://<mynamespace>.accesscontrol.windows.net
```

Toda a comunicação com o STS e as operações de gerenciamento são feitas nesta URL. Você pode usar diferentes caminhos para finalidades diferentes. Para determinar se os aplicativos ou serviços usam o Controle de Acesso, monitore todo o tráfego para https://\<namespace\>. accesscontrol.windows.net. Qualquer tráfego para essa URL é gerenciado pelo Controle de Acesso e precisa ser interrompido. 

A exceção é qualquer tráfego para https://accounts.accesscontrol.windows.net. O tráfego para esta URL já é gerenciado por um serviço diferente e não é afetado pela substituição do Controle de Acesso. 

Você também deve fazer logon no portal clássico do Azure e verificar todos os namespaces do Controle de Acesso nas assinaturas que você possui. Os namespaces do Controle de Acesso estão listados na guia **Namespaces do Controle de Acesso**, no serviço do **Active Directory**.

Para mais informações sobre o Controle de Acesso, consulte [Serviço de Controle de Acesso 2.0 (arquivado)](https://msdn.microsoft.com/library/hh147631.aspx).

## <a name="retirement-schedule"></a>Cronograma de desativação

A partir de novembro de 2017, todos os componentes do Controle de Acesso são totalmente suportados e operacionais. A única restrição é que você [não pode criar novos namespaces de Controle de Acesso por meio do portal clássico do Azure](https://azure.microsoft.com/blog/acs-access-control-service-namespace-creation-restriction/).

Aqui está a agenda para a substituição de componentes de Controle de Acesso:

- **Novembro de 2017**: a experiência de administração do Azure AD no portal clássico do Azure [é desativada](https://blogs.technet.microsoft.com/enterprisemobility/2017/09/18/marching-into-the-future-of-the-azure-ad-admin-experience-retiring-the-azure-classic-portal/). Neste ponto, o gerenciamento de namespace para o Controle de Acesso está disponível em uma nova URL dedicada: http://manage.windowsazure.com?restoreClassic=true. Use esta URL para exibir seus namespaces existentes, habilitar e desabilitar namespaces e excluir namespaces, se você desejar.
- **Abril de 2018**: o gerenciamento de namespace do Controle de Acesso não está mais disponível na URL dedicada http://manage.windowsazure.com?restoreClassic=true. Neste ponto, você não pode desabilitar ou habilitar, excluir ou enumerar seus namespaces de Controle de Acesso. No entanto, o portal de gerenciamento de Controle de Acesso será totalmente funcional e está localizado no https://\<namespace\>. accesscontrol.windows.net. Todos os outros componentes do Controle de Acesso continuam operando normalmente.
- **Novembro de 2018**: todos os componentes do Controle de Acesso são encerrados permanentemente. Isso inclui o portal de gerenciamento do Controle de Acesso, o serviço de gerenciamento, STS e o mecanismo de regras de transformação de token. Neste ponto, quaisquer solicitações enviadas para o Controle de Acesso (localizado em \<namespace\>.accesscontrol.windows.net) falham. Você deve ter migrado todos os aplicativos e serviços existentes para outras tecnologias bem antes disso.


## <a name="migration-strategies"></a>Estratégias de migração

As seções a seguir descrevem as recomendações de alto nível para a migração do Controle de Acesso para outras tecnologias da Microsoft.

### <a name="clients-of-microsoft-cloud-services"></a>Clientes de serviços em nuvem da Microsoft

Cada um dos serviços em nuvem da Microsoft que aceitam tokens emitidos pelo Controle de Acesso agora suportam pelo menos uma forma alternativa de autenticação. O mecanismo de autenticação correto varia para cada serviço. É recomendável que você consulte a documentação específica para cada serviço para obter orientação oficial. Para sua conveniência, cada conjunto de documentação é fornecido aqui:

| O Barramento de | Diretrizes |
| ------- | -------- |
| Barramento de Serviço do Azure | [Migrar para Assinaturas de Acesso Compartilhado](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas) |
| Retransmissão do Barramento de Serviço do Azure | [Migrar para Assinaturas de Acesso Compartilhado](https://docs.microsoft.com/azure/service-bus-relay/relay-migrate-acs-sas) |
| Cache Gerenciado do Azure | [Migrar para o Cache Redis do Azure](https://docs.microsoft.com/azure/redis-cache/cache-faq#which-azure-cache-offering-is-right-for-me) |
| DataMarket do Azure | [Migrar para as APIs de Serviços Cognitivos](https://docs.microsoft.com/azure/machine-learning/studio/datamarket-deprecation) |
| Serviços do BizTalk | [Migrar para o recurso de Aplicativos Lógicos do Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/machine-learning/studio/datamarket-deprecation) |
| Serviços de Mídia do Azure | [Migrar para a Autenticação do Azure AD](https://azure.microsoft.com/blog/azure-media-service-aad-auth-and-acs-deprecation/) |
| Serviço de Backup do Azure | [Atualizar o Agente de Backup do Azure](https://docs.microsoft.com/azure/backup/backup-azure-file-folder-backup-faq) |

<!-- Dynamics CRM: Migrate to new SDK, Dynamics team handling privately -->
<!-- Azure RemoteApp deprecated in favor of Citrix: http://www.zdnet.com/article/microsoft-to-drop-azure-remoteapp-in-favor-of-citrix-remoting-technologies/ -->
<!-- Exchange push notifications are moving, customers don't need to move -->
<!-- Retail federation services are moving, customers don't need to move -->
<!-- Azure StorSimple: TODO -->
<!-- Azure SiteRecovery: TODO -->


### <a name="web-applications-that-use-passive-authentication"></a>Aplicativos Web que usam autenticação passiva

Para aplicativos web que usam o Controle de Acesso para autenticação de usuário, o Controle de Acesso fornece os seguintes recursos e capacidades para arquitetos e desenvolvedores de aplicativos web:

- Integração profunda com o Windows Identity Foundation (WIF).
- Federação com contas do Google, Facebook, Yahoo, Azure Active Directory, AD FS e contas da Microsoft.
- Suporte para os seguintes protocolos de autenticação: OAuth 2.0 Draft 13, WS-Trust e Web Services Federation (WS-Federation).
- Suporte para os seguintes formatos de token: Token Web JSON (JWT), SAML 1.1, SAML 2.0 e Token Web Simples (SWT).
- Uma experiência de descoberta de realm inicial integrada ao WIF, que permite aos usuários escolher o tipo de conta que eles usam para entrar. Esta experiência é hospedada pelo aplicativo web e é totalmente personalizável.
- Transformação de token que permite uma personalização avançada das declarações recebidas pelo aplicativo web do Controle de Acesso, incluindo:
    - Declarações de passagem de provedores de identidade.
    - Adicionar declarações personalizadas extras.
    - Lógica se-então simples para emitir declarações em certas condições.

Infelizmente, não há um serviço que forneça todos esses recursos equivalentes. Você deve avaliar de quais recursos do Controle de Acesso precisa e, em seguida, escolher entre usar o [Azure Active Directory](https://azure.microsoft.com/develop/identity/signin/), [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) (Azure AD B2C) ou outro serviço de autenticação na nuvem.

#### <a name="migrate-to-azure-active-directory"></a>Migrar para o Azure Active Directory

Um caminho a ser levado em consideração é integrar seus aplicativos e serviços diretamente com o Azure AD. O Azure AD é o provedor de identidade baseados em nuvem para contas corporativas ou de estudante da Microsoft. O Azure AD é o provedor de identidade para o Office 365, Azure e muito mais. Ele fornece recursos de autenticação federados similares ao Controle de Acesso, mas não oferece suporte a todos os recursos do Controle de Acesso. 

O principal exemplo é a federação com provedores de identidade de redes sociais, como o Facebook, Google e Yahoo. Se seus usuários entram com esses tipos de credenciais, o Azure AD não é a solução para você. 

O Azure AD também não suporta necessariamente os mesmos protocolos de autenticação como Controle de Acesso. Por exemplo, embora o Controle de Acesso e o Azure AD suportem OAuth, há diferenças sutis entre cada implementação. Implementações diferentes exigem que você modifique o código como parte de uma migração.

No entanto, o Azure AD oferece várias possíveis vantagens para clientes do Controle de Acesso. Ele oferece suporte de forma nativa a contas corporativas e de estudante da Microsoft hospedadas na nuvem, que são normalmente usadas por clientes do Controle de Acesso. 

Um locatário do Azure AD também pode ser federado para uma ou mais instâncias do Active Directory local por meio do AD FS. Dessa forma, seu aplicativo pode autenticar usuários baseados em nuvem e os usuários que estão hospedados no local. Ele também oferece suporte ao protocolo WS-Federation, o que o torna relativamente fácil para integrar um aplicativo web usando o WIF.

A tabela a seguir compara os recursos do Controle de Acesso que são relevantes para aplicativos web aos recursos que estão disponíveis no Azure AD. 

Em um alto nível, o *Azure Active Directory provavelmente é a melhor opção para a sua migração se você permitir que os usuários entrem somente com suas contas corporativas ou de estudante da Microsoft*.

| Recurso | Suporte do Controle de Acesso | Suporte do Azure AD |
| ---------- | ----------- | ---------------- |
| **Tipos de contas** | | |
| Contas corporativas ou de estudante da Microsoft | Suportado | Suportado |
| Contas do Windows Server Active Directory e AD FS |- Com suporte por meio de federação com um locatário do Azure AD <br />- Com suporte via federação direta com AD FS | Com suporte apenas por meio de federação com um locatário do Azure AD | 
| Contas de outros sistemas de gerenciamento de identidade corporativa |- Possível por meio de federação com um locatário do Azure AD <br />- Com suporte via federação direta | Possível por meio de federação com um locatário do Azure AD |
| Contas da Microsoft para uso pessoal | Suportado | Com suporte por meio do protocolo do OAuth v2.0 do Azure AD, mas não sobre nenhum outro protocolo | 
| Contas do Facebook, Google, Yahoo | Suportado | Sem nenhum suporte |
| **Protocolos e compatibilidade do SDK** | | |
| WIF | Suportado | Com suporte, mas instruções limitadas estão disponíveis |
| O certificado do provedor de identidade do Web Services Federation | Suportado | Suportado |
| OAuth 2.0 | Suporte para Draft 13 | Suporte para RFC 6749, a especificação mais moderna |
| WS-Trust | Suportado | Sem suporte |
| **Formatos de Token** | | |
| JWT | Com suporte em versão beta | Suportado |
| SAML 1.1 | Suportado | Visualização |
| SAML 2.0 | Suportado | Suportado |
| SWT | Suportado | Sem suporte |
| **Personalizações** | | |
| Interface de usuário de seleção de conta/descoberta de realm de início personalizável | Código disponível para download que pode ser incorporado a aplicativos | Sem suporte |
| Carregar certificados de autenticação de tokens personalizados | Suportado | Suportado |
| Personalizar declarações em gráficos |- Declarações de entrada de passagem de provedores de identidade<br />- Obter token de acesso do provedor de identidade como uma declaração<br />- Emitir declarações de saída com base nos valores de declarações de entrada<br />- Emitir declarações de saída com valores constantes |- Não é possível passar declarações de provedores de identidade federados<br />- Não pode obter um token de acesso do provedor de identidade como uma declaração<br />- Não pode emitir declarações de saída com base nos valores de declarações de entrada<br />- Pode emitir declarações de saída com valores constantes<br />- Pode emitir declarações de saída com base nas propriedades de usuários sincronizadas ao Azure AD |
| **Automação** | | |
| Automatizar tarefas de gerenciamento e configuração | Suporte por meio do Serviço de Gerenciamento do Controle de Acesso | Com suporte via Microsoft Graph e Graph API do Azure AD |

Se você decidir que o Azure AD é o melhor caminho de migração para seus aplicativos e serviços, lembre-se de duas maneiras de integrar seu aplicativo com o Azure AD.

Para usar o WS-Federation ou WIF para integrar com o Azure AD, é recomendável seguir a abordagem descrita em [Configurar SSO federado para um aplicativo sem galeria](https://docs.microsoft.com/azure/active-directory/application-config-sso-how-to-configure-federated-sso-non-gallery). O artigo refere-se à configuração do Azure AD para logon único baseado em SAML, mas serve também para a configuração do WS-Federation. Seguir essa abordagem requer uma licença do Azure AD Premium. Essa abordagem tem duas vantagens:

- Você obtém toda a flexibilidade da personalização do token do Azure AD. Você pode personalizar as declarações que são emitidas pelo Azure AD para corresponder as declarações que são emitidas pelo Controle de Acesso. Especialmente, isso inclui a declaração do identificador de nome e ID de usuário. Para continuar a receber identificadores de usuário consistente para seus usuários depois que você alterar tecnologias, certifique-se de que as IDs de usuário emitidas pelo Azure AD correspondem com aquelas emitidas pelo Controle de Acesso.
- Você pode configurar um certificado de autenticação de token que é específico para seu aplicativo, e com um tempo de vida que você controla.

<!--

Possible nameIdentifiers from Access Control (via AAD or AD FS):
- AD FS - Whatever AD FS is configured to send (email, UPN, employeeID, what have you)
- Default from AAD using App Registrations, or Custom Apps before ClaimsIssuance policy: subject/persistent ID
- Default from AAD using Custom apps nowadays: UPN
- Kusto can't tell us distribution, it's redacted

-->

> [!NOTE]
> Esta abordagem requer uma licença do Azure AD Premium. Se você for um cliente de Controle de Acesso e precisa de uma licença premium para a configuração de logon único para um aplicativo, entre em contato conosco. Proporcionaremos licenças de desenvolvedores para você usar.

Uma abordagem alternativa é seguir [este código de exemplo](https://github.com/Azure-Samples/active-directory-dotnet-webapp-wsfederation), que fornece instruções um pouco diferentes para configurar o WS-Federation. Este exemplo de código não usa o WIF, mas, em vez disso, o middleware ASP.NET 4.5 OWIN. No entanto, as instruções de registro do aplicativo são válidas para aplicativos que usam o WIF e não exigem uma licença do Azure AD Premium. 

Se você escolher essa abordagem, é preciso entender a [sobreposição de chave de assinatura no Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-signing-key-rollover). Esta abordagem usa a chave de assinatura global do Azure AD para emitir tokens. Por padrão, o WIF não atualiza automaticamente as chaves de assinatura. Quando o Azure AD girar suas chaves de assinatura globais, sua implementação do WIF precisará estar preparada para aceitar as alterações.

Se você pode integrar-se ao Azure AD por meio dos protocolos do OAuth ou OpenID Connect, recomendamos que o faça. Disponibilizamos uma ampla documentação e orientações sobre como integrar o Azure AD ao seu aplicativo Web em nosso [Guia de desenvolvedor do Azure AD](http://aka.ms/aaddev).

<!-- TODO: If customers ask about authZ, let's put a blurb on role claims here -->

#### <a name="migrate-to-azure-active-directory-b2c"></a>Migrar para o Azure Active Directory B2C

O outro caminho de migração a considerar é o Azure AD B2C. O Azure AD B2C é um serviço de autenticação na nuvem, como o Controle de Acesso, que permite que os desenvolvedores terceirizem a sua lógica de gerenciamento de identidade e autenticação para um serviço na nuvem. É um serviço pago (com camadas gratuitas e premium) projetado para clientes com aplicativos que podem ter até milhões de usuários ativos.

Como o Controle de Acesso, um dos recursos mais atrativos do Azure AD B2C é que oferece suporte a muitos tipos diferentes de contas. Com o Azure AD B2C, você pode fazer logon de usuários usando sua conta da Microsoft, ou contas do Facebook, Google, LinkedIn, GitHub ou Yahoo e muito mais. O Azure AD B2C também oferece suporte a "contas locais" ou nome de usuário e senhas que os usuários criam especificamente para seu aplicativo. O Azure AD B2C também oferece uma extensibilidade avançada que você pode usar para personalizar seus fluxos de logon. 

No entanto, o Azure AD B2C não oferece suporte para a variedade de protocolos de autenticação e formatos de token que os clientes do Controle de Acesso podem exigir. Você também não pode usar o Azure AD B2C para obter tokens e consultar informações adicionais sobre o usuário do provedor de identidade, Microsoft ou outro.

A tabela a seguir compara os recursos do Controle de Acesso que são relevantes para aplicativos web aos que estão disponíveis no Azure AD B2C. Em um nível elevado, o *Azure AD B2C é provavelmente a escolha certa para a sua migração se seu aplicativo for voltado a clientes, ou se ele oferecer suporte a muitos tipos de contas.*

| Recurso | Suporte do Controle de Acesso | Suporte do Azure AD B2C |
| ---------- | ----------- | ---------------- |
| **Tipos de contas** | | |
| Contas corporativas ou de estudante da Microsoft | Suportado | Com suporte via políticas personalizadas  |
| Contas do Windows Server Active Directory e AD FS | Com suporte via federação direta com AD FS | Com suporte via federação SAML usando políticas personalizadas |
| Contas de outros sistemas de gerenciamento de identidade corporativa | Com suporte via federação direta via WS-Federation | Com suporte via federação SAML usando políticas personalizadas |
| Contas da Microsoft para uso pessoal | Suportado | Suportado | 
| Contas do Facebook, Google, Yahoo | Suportado | Suporte nativo ao Facebook e Google, suporte para Yahoo por meio da federação do OpenID Connect usando políticas personalizadas |
| **Protocolos e compatibilidade do SDK** | | |
| Windows Identity Foundation (WIF) | Suportado | Sem suporte |
| O certificado do provedor de identidade do Web Services Federation | Suportado | Sem suporte |
| OAuth 2.0 | Suporte para Draft 13 | Suporte para RFC 6749, a especificação mais moderna |
| WS-Trust | Suportado | Sem suporte |
| **Formatos de Token** | | |
| JWT | Com suporte em versão beta | Suportado |
| SAML 1.1 | Suportado | Sem suporte |
| SAML 2.0 | Suportado | Sem suporte |
| SWT | Suportado | Sem suporte |
| **Personalizações** | | |
| Interface de usuário de seleção de conta/descoberta de realm de início personalizável | Código disponível para download que pode ser incorporado a aplicativos | Interface do usuário totalmente personalizável via CSS personalizado |
| Carregar certificados de autenticação de tokens personalizados | Suportado | Chaves de autenticação personalizadas, não certificados, com suporte via políticas personalizadas |
| Personalizar declarações em gráficos |- Declarações de entrada de passagem de provedores de identidade<br />- Obter token de acesso do provedor de identidade como uma declaração<br />- Emitir declarações de saída com base nos valores de declarações de entrada<br />- Emitir declarações de saída com valores constantes |- Pode passar por declarações de provedores de identidade; políticas personalizadas necessárias para algumas declarações<br />- Não pode obter um token de acesso do provedor de identidade como uma declaração<br />- Pode emitir declarações de saída com base nos valores de declarações de entrada via políticas personalizadas<br />- Pode emitir declarações de saída com valores constantes via políticas personalizadas |
| **Automação** | | |
| Automatizar tarefas de gerenciamento e configuração | Suporte por meio do Serviço de Gerenciamento do Controle de Acesso |- Criação de usuários permitidos por meio da API do Graph do Azure AD<br />- Não pode criar políticas, aplicativos ou locatários B2C programaticamente |

Se você decidir que o Azure AD B2C é o melhor caminho para seus aplicativos e serviços, comece com os seguintes recursos:

- [Documentação do Azure AD B2C](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview)
- [Políticas personalizadas do Azure AD B2C](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview-custom)
- [Preços do Azure AD B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/)


#### <a name="migrate-to-ping-identity-or-auth0"></a>Migrar a identidade de Ping ou Auth0

Em alguns casos, você pode notar que o Azure AD e o Azure AD B2C não são suficientes para substituir o Controle de Acesso nos aplicativos web sem fazer alterações de código principais. Alguns exemplos comuns podem incluir:

- Aplicativos web que usam o WIF ou WS-Federation para entrar com provedores de identidade social, como Google ou Facebook.
- Aplicativos web que executam a federação direta para um provedor de identidade corporativa por meio do protocolo WS-Federation.
- Aplicativos web que exigem o token de acesso emitido por um provedor de identidade social (como Google ou Facebook) como uma declaração nos tokens emitidos pelo Controle de Acesso.
- Aplicativos web com as regras de transformação de token complexas que o Azure AD ou Azure AD B2C não pode reproduzir.
- Aplicativos web multilocatário que usam o ACS para gerenciar centralmente a federação para muitos provedores de identidade diferentes

Nesses casos, convém migrar seu aplicativo web para outro serviço de autenticação de nuvem. Recomendamos que você explorar as opções a seguir. Cada uma das opções a seguir oferecem recursos semelhantes ao Controle de Acesso:



|     |     | 
| --- | --- |
| ![Auth0](./media/active-directory-acs-migration/rsz_auth0.png) | [Auth0](https://auth0.com/acs) é um serviço de identidade de nuvem flexível que criou [orientação de migração de alto nível para os clientes de Controle de Acesso](https://auth0.com/acs)e oferece suporte a quase todos os recursos oferecidos pelo ACS. |
| ![Ping](./media/active-directory-acs-migration/rsz_ping.png) | [Identidade de ping](https://www.pingidentity.com) oferece duas soluções semelhantes ao ACS. PingOne é um serviço de identidade de nuvem que oferece suporte a muitos dos mesmos recursos que o ACS e o PingFederate é um produto de identidade local semelhante que oferece mais flexibilidade. Consulte [Orientação de desativação do Ping ACS](https://www.pingidentity.com/company/blog/2017/11/20/migrating_from_microsoft_acs_to_ping_identity.html) para obter mais detalhes sobre como usar esses produtos.  |

Nosso objetivo ao trabalhar com a identidade de Ping e Auth0 é garantir que todos os clientes de Controle de Acesso tem um caminho de migração para seus aplicativos e serviços que minimiza a quantidade de trabalho necessária para mover de Controle de Acesso.

<!--

## Sharepoint 2010, 2013, 2016

TODO: Azure AD only, use Azure AD SAML 1.1 tokens, when we bring it back online.
Other IDPs: use Auth0? https://auth0.com/docs/integrations/sharepoint.

-->

### <a name="web-services-that-use-active-authentication"></a>Serviços Web que usam a autenticação ativa

Para serviços web que são protegidos com tokens emitidos pelo Controle de Acesso, o Controle de Acesso oferece os seguintes recursos e capacidades:

- A capacidade de registrar uma ou mais *identidades de serviço* no seu namespace do Controle de Acesso. As identidades de serviço podem ser usadas para solicitar tokens.
- Suporte para os protocolos OAuth WRAP e OAuth 2.0 Draft 13 para solicitar tokens, usando os seguintes tipos de credenciais:
    - Uma senha simples que é criada para a identidade do serviço
    - Um SWT usando uma chave simétrica ou certificado X509
    - Um token SAML emitido por um provedor de identidades confiável (geralmente uma instância do AD FS)
- Suporte para os seguintes formatos de token: JWT, SAML 1.1, SAML 2.0 e SWT.
- Regras simples de transformação do token.

As identidades de serviço no Controle de Acesso são geralmente usadas para implementar uma autenticação de servidor para servidor.  

#### <a name="migrate-to-azure-active-directory"></a>Migrar para o Azure Active Directory

Nossa recomendação para este tipo de fluxo de autenticação é migrar para o [Azure Active Directory](https://azure.microsoft.com/develop/identity/signin/). O Azure AD é o provedor de identidade baseados em nuvem para contas corporativas ou de estudante da Microsoft. O Azure AD é o provedor de identidade para o Office 365, Azure e muito mais. 

Você também usar o Azure AB para a autenticação de servidor para servidor usando a implementação do Azure AD da concessão de credenciais de cliente do OAuth. A tabela a seguir compara os recursos do Controle de Acesso na autenticação de servidor para servidor com aquelas que estão disponíveis no Azure AD.

| Recurso | Suporte do Controle de Acesso | Suporte do Azure AD |
| ---------- | ----------- | ---------------- |
| Como registrar um serviço Web | Crie uma terceira parte confiável no portal de gerenciamento do Controle de Acesso | Crie um aplicativo web do Azure AD no portal do Azure |
| Como registrar um cliente | Crie uma terceira parte confiável no portal de gerenciamento do Controle de Acesso | Crie outro aplicativo web do Azure AD no portal do Azure |
| Protocolo usado |- Protocolo OAuth WRAP<br />- Concessão de credenciais do cliente do OAuth 2.0 Draft 13 | Concessão de credenciais de cliente do OAuth 2.0 |
| Métodos de autenticação do cliente |- Senha simples<br />- SWT assinado<br />- Token SAML de um provedor de identidade federado |- Senha simples<br />- JWT assinado |
| Formatos de Token |- JWT<br />- SAML 1.1<br />- SAML 2.0<br />- SWT<br /> | Somente JWT |
| Transformação de token |- Adicionar declarações personalizadas<br />- Lógica de emissão se-então simples | Adicionar declarações personalizadas | 
| Automatizar tarefas de gerenciamento e configuração | Suporte por meio do Serviço de Gerenciamento do Controle de Acesso | Com suporte via Microsoft Graph e API do Graph do Azure AD |

Para obter diretrizes sobre a implementação de cenários de servidor para servidor, consulte os seguintes recursos:

- Seção de Serviço para Serviço do [guia de desenvolvedor do Azure AD](https://aka.ms/aaddev)
- [Exemplo de código do Daemon usando as credenciais do cliente de senha simples](https://github.com/Azure-Samples/active-directory-dotnet-daemon)
- [Exemplo de código do Daemon usando as credenciais do cliente de certificado](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential)

#### <a name="migrate-to-ping-identity-or-auth0"></a>Migrar a identidade de Ping ou Auth0

Em alguns casos, você pode achar que as credenciais de cliente do Azure AD e a implementação de concessão OAuth não são suficientes para substituir o Controle de Acesso em sua arquitetura sem alterações de código principais. Alguns exemplos comuns podem incluir:

- Autenticação de servidor para servidor usando formatos de token que não seja JWTs.
- Autenticação de servidor para servidor usando um token de entrada fornecido por um provedor de identidade externa.
- Autenticação de servidor para servidor com as regras de transformação de token do Azure AD não pode reproduzir.

Nesses casos, convém migrar seu aplicativo web para outro serviço de autenticação de nuvem. Recomendamos que você explorar as opções a seguir. Cada uma das opções a seguir oferecem recursos semelhantes ao Controle de Acesso:

|     |     | 
| --- | --- |
| ![Auth0](./media/active-directory-acs-migration/rsz_auth0.png) | [Auth0](https://auth0.com/acs) é um serviço de identidade de nuvem flexível que criou [orientação de migração de alto nível para os clientes de Controle de Acesso](https://auth0.com/acs)e oferece suporte a quase todos os recursos oferecidos pelo ACS. |
| ![Ping](./media/active-directory-acs-migration/rsz_ping.png) | [Identidade de ping](https://www.pingidentity.com) oferece duas soluções semelhantes ao ACS. PingOne é um serviço de identidade de nuvem que oferece suporte a muitos dos mesmos recursos que o ACS e o PingFederate é um produto de identidade local semelhante que oferece mais flexibilidade. Consulte [Orientação de desativação do Ping ACS](https://www.pingidentity.com/company/blog/2017/11/20/migrating_from_microsoft_acs_to_ping_identity.html) para obter mais detalhes sobre como usar esses produtos.  |

Nosso objetivo ao trabalhar com a identidade de Ping e Auth0 é garantir que todos os clientes de Controle de Acesso tem um caminho de migração para seus aplicativos e serviços que minimiza a quantidade de trabalho necessária para mover de Controle de Acesso.

## <a name="questions-concerns-and-feedback"></a>Perguntas, preocupações e comentários

Sabemos que muitos clientes de Controle de Acesso não encontrarão um caminho de migração claro depois de ler este artigo. Talvez seja necessário alguns assistência ou orientação para determinar o plano à direita. Caso queira discutir suas dúvidas e cenários de migração, por favor deixe um comentário nesta página.
