---
title: "aaaWhat é o acesso ao aplicativo e o logon único com o Active Directory do Azure? | Microsoft Docs"
description: "Use o Active Directory do Azure tooenable único logon tooall de saudação SaaS e os aplicativos web que você precisa para os negócios."
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 75d1a3fd-b3c5-4495-a5c8-c4c24145ff00
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curyand
ms.openlocfilehash: 429522cbd570ab27359c4630c5a6d7b25b692ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-access-and-single-sign-on-with-azure-active-directory"></a>O que é o acesso a aplicativos e logon único com o Azure Active Directory?
Logon único significa que está sendo tooaccess capaz de todos os aplicativos de saudação e recursos que você precisa toodo business, inscrevendo-se apenas uma vez usando uma conta de usuário único. Depois de conectado, você pode acessar todos os aplicativos de saudação sem sendo tooauthenticate necessário (por exemplo, digite uma senha) uma segunda vez.

Muitas organizações contam com o software como um aplicativo de serviço (SaaS) como o Office 365, Box e Salesforce para produtividade do usuário final. Historicamente, a equipe de TI precisa tooindividually criar e atualizar contas de usuário em cada aplicativo SaaS, e os usuários têm tooremember uma senha para cada aplicativo SaaS.

Active Directory do Azure se estende do Active Directory local para nuvem hello, permitindo que os usuários toouse seu primário toonot somente logon da conta organizacional tootheir domínio dispositivos e recursos da empresa, mas também todos os Olá web e aplicativos SaaS necessário para seu trabalho.

Portanto não apenas os usuários não possuem toomanage vários conjuntos de nomes de usuário e senhas, seus aplicativos de acesso pode ser provisionado ou eliminação provisionado automaticamente com base em seus membros de grupo da organização, além de seu status como um funcionários. Apresenta a segurança do Azure Active Directory e controles de controle de acesso que permitem que você toocentrally gerenciam o acesso dos usuários nos aplicativos SaaS.

AD do Azure permite toomany fácil integração de aplicativos SaaS populares de hoje; Ele fornece gerenciamento de identidade e acesso e permite que os usuários toosingle logon tooapplications diretamente, ou descobre e iniciá-los a partir de um portal como o Office 365 ou hello painel de acesso do AD do Azure.

arquitetura de saudação de integração Olá consiste em Olá quatro principais blocos de construção a seguir:

* Logon único permite que os usuários tooaccess seus aplicativos SaaS com base em sua conta organizacional no AD do Azure. O logon único é o que permite que o aplicativo de tooan tooauthenticate de usuários usando sua conta organizacional único.
* O provisionamento do usuário permite que o usuário de provisionamento e desprovisionamento no SaaS com base nas alterações feitas no Active Directory do Windows Server e/ou Azure AD de destino. Uma conta provisionada é o que permite um toouse toobe autorizada do usuário um aplicativo após terem autenticado por meio de logon único.
* Gerenciamento de acesso de aplicativo centralizado no Portal de gerenciamento de saudação permite acesso de aplicativo de ponto único de SaaS e o gerenciamento, com hello capacidade toodelegate aplicativo acesso decisão tomada e aprovações tooanyone na organização Olá
* Relatório unificado e monitoramento de atividade de usuário no AD do Azure

## <a name="how-does-single-sign-on-with-azure-active-directory-work"></a>Como funciona o logon único com o Active Directory do Azure?
Quando um aplicativo de tooan usuário "entrar", eles passarem por um processo de autenticação quando forem necessário tooprove que eles sejam que eles dizem que são. Sem logon único, isso geralmente é feito inserindo uma senha que é armazenada no aplicativo hello e usuário Olá é necessário tooknow essa senha.

AD do Azure suporta tooapplications toosign de três maneiras diferentes:

* **O logon único federado** permite que aplicativos tooredirect tooAzure AD para autenticação de usuário em vez de solicitar sua própria senha. Isso tem suporte para aplicativos que suporte protocolos como SAML 2.0, WS-Federation ou OpenID Connect e é o modo mais rico de saudação do logon único.
* **Logon único baseado em senha** permite proteger o armazenamento de senhas de aplicativo e repetir usando uma extensão de navegador da web ou aplicativo móvel. Isso utiliza Olá existente processo de entrada fornecido pelo aplicativo hello, mas permite que senhas de saudação de toomanage um administrador e não requer Olá tooknow Olá senha.
* **Logon único existente** permite que o AD do Azure tooleverage qualquer existente logon único foi configurado para o aplicativo hello, mas permite que esses aplicativos toobe vinculado toohello Office 365 ou portais de painel de acesso do AD do Azure e também permite que relatórios no AD do Azure, quando os aplicativos de saudação são iniciados existe adicionais.

Depois que um usuário autenticado com um aplicativo, eles também precisam toohave um registro de conta provisionado no aplicativo hello que informa ao aplicativo hello onde há permissões e o nível de acesso estão dentro do aplicativo hello. Olá provisionamento deste registro de conta ou pode ocorrer automaticamente, ou pode ocorrer manualmente por um administrador antes que o usuário Olá é fornecido acesso de logon único.

 Mais detalhes sobre esses modos de logon único e provisionamento abaixo.

### <a name="federated-single-sign-on"></a>Logon único federado
Logon único federado permite que os usuários de saudação do habilita logon no seu toobe organização automaticamente conectado no aplicativo de SaaS de terceiros tooa pelo AD do Azure usando informações de conta de usuário de saudação do AD do Azure.

Nesse cenário, quando você já entrou no AD do Azure e você desejar que recursos tooaccess que são controlados por um aplicativo SaaS de terceiros, Federação elimina a necessidade de saudação de um toobe de usuário autenticado novamente.

AD do Azure pode dar suporte a federado SSO com aplicativos que oferecem suporte a saudação SAML 2.0, WS-Federation ou OpenID connect protocolos.

Consulte também: [Gerenciar certificados para federados Single Sign-On](active-directory-sso-certs.md)

### <a name="password-based-single-sign-on"></a>Logon único baseado em senha
Configuração baseada em senha de logon único permite aos usuários de saudação em seu toobe organização automaticamente conectado no aplicativo de SaaS de terceiros tooa pelo AD do Azure usando informações de conta de usuário de saudação do aplicativo de SaaS de terceiros hello. Quando você habilita esse recurso, o AD do Azure coleta e armazena com segurança informações de conta de usuário de saudação e a senha relacionada hello.

O AD do Azure pode dar suporte a logon único baseado em senha em qualquer aplicativo baseado em nuvem que tem uma página de entrada baseada em HTML. Usando um plug-in de navegador personalizado, o AAD automatiza o processo recuperando com segurança as credenciais do aplicativo como saudação de nome de usuário e senha de saudação do diretório de saudação de entrada do usuário hello e insere essas credenciais na página de entrada do aplicativo hello nome de usuário de saudação. Há dois casos de uso:

1. **Administrador gerencia credenciais** – os administradores podem criar e gerenciar credenciais de aplicativo e atribuir essas credenciais toousers ou grupos que precisam acessar o aplicativo de toohello. Nesses casos, Olá final usuário não precisa de credenciais de saudação tooknow, mas ainda obtém o aplicativo do acesso de logon único toohello simplesmente clicando no respectivo painel de acesso ou por meio de um link fornecido. Isso permite que ambos, gerenciamento de ciclo de vida de credenciais Olá Olá administrador, bem como sua conveniência para os usuários finais por meio do qual eles não precisam tooremember ou gerenciar senhas específicas de aplicativo. credenciais de saudação são ofuscadas do usuário final de saudação durante a saudação automatizada processo de entrada; No entanto, eles são tecnicamente detectáveis pelo usuário Olá usar depuração da web e ferramentas de usuários e administradores devem seguir Olá mesmas políticas de segurança, como se hello credenciais foram apresentadas diretamente pelo usuário hello. As credenciais fornecidas pelo administrador são muito úteis ao fornecer acesso de conta que é compartilhado entre vários usuários, como mídia social ou aplicativos de compartilhamento de documentos.
2. **Usuário gerencia credenciais** – os administradores podem atribuir aplicativos tooend usuários ou grupos e permitir Olá final usuários tooenter suas próprias credenciais diretamente ao acessar o aplicativo hello para Olá a primeira vez no respectivo painel de acesso. Isso cria uma conveniência para os usuários finais por meio do qual eles não precisam de toocontinually insira senhas específicas de aplicativo de saudação sempre que acessarem o aplicativo hello. Esse caso de uso também pode ser usado como uma revisão pedra tooadministrative de gerenciamento de credenciais hello, no qual Olá administrador pode definir novas credenciais para o aplicativo hello no futuro sem alterar a experiência de acesso do aplicativo de saudação do usuário final de saudação.

Em ambos os casos, as credenciais são armazenadas em um estado criptografado no diretório hello e são passadas via HTTPS somente durante o processo de entrada hello automatizada. Usando o logon único baseado em senha, o AD do Azure oferece uma solução de gerenciamento de acesso conveniente de identidade para aplicativos que não é capaz de oferecer suporte a protocolos de Federação.

SSO baseado em senha se baseia em um navegador extensão toosecurely recuperar Olá aplicativo e usuário informações específicas do AD do Azure e aplicá-lo toohello serviço. A maioria dos aplicativos SaaS de terceiros que são suportados pelo AD do Azure oferecem suporte a esse recurso.

Para SSO baseado em senha, navegadores de saudação do usuário podem ser:

* Internet Explorer 8, 9, 10 e 11 – no Windows 7 ou posterior (Consulte também [guia de implantação de extensão do IE](active-directory-saas-ie-group-policy.md))
* Chrome – No Windows 7 ou posterior e no MacOS X ou posterior
* Firefox 26.0 ou posterior, no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior

**Observação:** extensão SSO baseada em senha hello serão disponibilizadas para Edge no Windows 10 quando as extensões de navegador se tornam tem suporte para a borda.

### <a name="existing-single-sign-on"></a>Logon único existente
Ao configurar o logon único para um aplicativo, o portal de gerenciamento do Azure Olá fornece uma terceira opção de "existente Single Sign-On". Essa opção simplesmente permite Olá administrador toocreate um aplicativo de tooan link e colocá-lo no painel de acesso Olá para os usuários selecionados.

Por exemplo, se houver um aplicativo que é configurado tooauthenticate usuários usando o Active Directory Federation Services 2.0, um administrador pode usar o hello "existente Single Sign-On" opção toocreate tooit um link no painel de acesso de saudação. Quando os usuários acessam o link hello, eles são autenticados usando o Active Directory Federation Services 2.0 ou qualquer que seja único logon solução existente é fornecida pelo aplicativo hello.

### <a name="user-provisioning"></a>Provisionamento do usuário
Para selecionar aplicativos, o AD do Azure permite provisionamento automatizado de usuários e cancelamento de provisionamento de contas em aplicativos SaaS de terceiros de dentro de saudação Portal de gerenciamento do Azure, usando suas informações de identidade do Windows Server Active Directory ou AD do Azure. Quando um usuário recebe permissões no AD do Azure para um desses aplicativos, uma conta pode ser automaticamente criada (provisionada) no aplicativo SaaS de destino hello.

Quando um usuário é excluído ou suas informações mudam no AD do Azure, essas alterações também são refletidas em Olá aplicativo SaaS. Isso significa que, configurando o gerenciamento de ciclo de vida de identidade automatizado permite que os administradores toocontrol e fornecer o provisionamento automatizado e cancelamento de provisionamento de aplicativos SaaS. No AD do Azure, essa automação do ciclo de vida do gerenciamento de identidades é habilitada pelo provisionamento do usuário.

toolearn mais, consulte [tooSaaS automatizada de provisionamento de usuário e desprovisionamento aplicativos](active-directory-saas-app-provisioning.md)

## <a name="get-started-with-hello-azure-ad-application-gallery"></a>Introdução à Galeria de aplicativos do AD do Azure Olá
Pronto tooget iniciado? toodeploy logon único entre o AD do Azure e os aplicativos SaaS que sua organização usa, siga estas diretrizes.

### <a name="using-hello-azure-ad-application-gallery"></a>Usando a Galeria de aplicativos do AD do Azure Olá
Olá [Galeria de aplicativos do Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/) fornece uma lista de aplicativos que são conhecidos toosupport um formulário de logon único com o Active Directory do Azure.

![][1]

Aqui estão algumas dicas para localizar aplicativos segundo os recursos com os quais eles são compatíveis:

* O AD do Azure dá suporte ao provisionamento automático e cancelamento de provisionamento para todos os aplicativos de "Em destaque" hello [Galeria de aplicativos do Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/).
* Uma lista de aplicativos federados que dão suporte especificamente a logon único federado usando um protocolo como SAML, WS-Federation ou OpenID Connect pode ser encontrada [aqui](http://social.technet.microsoft.com/wiki/contents/articles/20235.azure-active-directory-application-gallery-federated-saas-apps.aspx).

Depois de localizar seu aplicativo, você pode começar a usar instruções passo a passo do hello siga apresentadas na Galeria de aplicativo hello e em tooenable portal de gerenciamento do Azure Olá logon único.

### <a name="application-not-in-hello-gallery"></a>Aplicativo não na Galeria de Olá?
Se seu aplicativo não for encontrado na Galeria de aplicativo do Azure AD hello, você terá estas opções:

* **Adicionar um aplicativo não listado que você está usando** -categoria do uso Olá personalizada na Galeria de aplicativo hello em tooconnect portal de gerenciamento do Azure de saudação um aplicativo não listado que sua organização está usando. Você pode adicionar qualquer aplicativo que ofereça suporte ao SAML 2.0 como um aplicativo federado ou qualquer aplicativo que tenha uma página de entrada baseada em HTML como um aplicativo do SSO de senha. Para obter mais detalhes, veja este artigo sobre [como adicionar seu próprio aplicativo](active-directory-saas-custom-apps.md).
* **Adicionar seu próprio aplicativo que está desenvolvendo** - se que você desenvolveu um aplicativo hello por conta própria, siga as diretrizes Olá Olá AD do Azure developer documentação tooimplement federado SSO ou usando o provisionamento Olá API do graph do Azure AD. Para obter mais informações, consulte estes recursos:
  
  * [Cenários de autenticação do Azure AD](active-directory-authentication-scenarios.md)
  * [https://GitHub.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-dotnet](https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet)
  * [https://GitHub.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-dotnet](https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet)
  * [https://GitHub.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore)
* **Solicitar uma integração de aplicativo** -solicitar suporte para o aplicativo hello necessária usando Olá [Fórum de comentários do AD do Azure](https://feedback.azure.com/forums/169401-azure-active-directory/).

### <a name="using-hello-azure-management-portal"></a>Usando o portal de gerenciamento do Azure Olá
Você pode usar o hello extensão do Active Directory em Olá Portal de gerenciamento tooconfigure Olá aplicativo logon único. Como uma primeira etapa, você precisa tooselect um diretório de saudação seção Active Directory no portal de saudação:

![][2]

toomanage seus aplicativos SaaS de terceiros, você pode alternar no guia de aplicativos de saudação do diretório selecionado hello. Essa exibição permite aos administradores:

* Adicionar novos aplicativos de galeria do Azure AD hello, bem como os aplicativos que você está desenvolvendo
* Excluir aplicativos integrados
* Gerenciar aplicativos de saudação que eles já integraram

Tarefas administrativas típicas para um aplicativo de SaaS de terceiros são:

* Habilitar logon único com o AD do Azure, usando SSO de senha ou, se disponível, para SaaS de destino Olá SSO federado
* Opcionalmente, habilitar o provisionamento de usuário para provisionamento e desprovisionamento de usuário (gerenciamento do ciclo de vida de identidade)
* Para aplicativos em que o provisionamento do usuário está habilitado, selecionando quais usuários têm acesso toothat aplicativo

Para aplicativos da Galeria que dão suporte a logon único federado, configuração normalmente requer que você tooprovide configurações adicionais, como certificados e metadados toocreate uma confiança federada entre o aplicativo de terceiros hello e o Azure AD. Assistente de configuração de saudação orienta detalhes hello e fornece acesso fácil toohello dados específicos de aplicativos SaaS e instruções.

Para aplicativos da Galeria que dão suporte ao provisionamento automático de usuário, isso requer você toogive AD do Azure permissões toomanage suas contas no aplicativo de SaaS hello. No mínimo, você precisa tooprovide credenciais do AD do Azure deve usar quando autenticar no aplicativo de destino toohello. Se as definições de configuração adicionais precisam toobe fornecido depende Olá requisitos do aplicativo hello.

## <a name="deploying-azure-ad-integrated-applications-toousers"></a>Implantar o AD do Azure integradas toousers de aplicativos
O AD do Azure fornece várias maneiras de personalizáveis toodeploy aplicativos tooend-os usuários em sua organização:

* Painel de acesso do AD do Azure
* Iniciador de aplicativos do Office 365
* Aplicativos de toofederated de logon direto
* Links profundos toofederated, com base em senha, ou aplicativos existentes

Qual método você escolher toodeploy em sua organização é seu critério.

### <a name="azure-ad-access-panel"></a>Painel de acesso do AD do Azure
Olá painel de acesso em https://myapps.microsoft.com é um portal baseado na web que permite que um usuário final com uma conta organizacional no Active Directory do Azure tooview e inicie aplicativos baseados em nuvem toowhich terem sido concedido acesso pelo Olá AD do Azure administrador. Se você for um usuário final com [Azure Active Directory Premium](https://azure.microsoft.com/pricing/details/active-directory/), também poderá utilizar os recursos de gerenciamento de grupo de autoatendimento por meio do painel de acesso de saudação.

![][3]

Olá painel de acesso é separado do Portal de gerenciamento de saudação e não requer usuários toohave uma assinatura do Azure ou a assinatura do Office 365.

Para obter mais informações sobre o painel de acesso de saudação do AD do Azure, consulte Olá [painel de acesso Introdução toohello](active-directory-saas-access-panel-introduction.md).

### <a name="office-365-application-launcher"></a>Iniciador de aplicativos do Office 365
Para organizações que implantaram o Office 365, aplicativos atribuídos toousers por meio do AD do Azure também aparecerá no portal do Office 365 de saudação em https://portal.office.com/myapps. Isso torna fácil e conveniente para os usuários em uma organização toolaunch seus aplicativos sem a necessidade de toouse um portal de segundo e é recomendada de saudação aplicativo Iniciar a solução para organizações que usam o Office 365.

![][4]

Para obter mais informações sobre o iniciador do aplicativo hello Office 365, consulte [que seu aplicativo seja exibido na iniciador do aplicativo hello Office 365](https://msdn.microsoft.com/office/office365/howto/connect-your-app-to-o365-app-launcher).

### <a name="direct-sign-on-toofederated-apps"></a>Aplicativos de toofederated de logon direto
Mais aplicativos federados que oferecem suporte a OpenID, WS-Federation ou SAML 2.0 também conectar suporte Olá capacidade para os usuários toostart no aplicativo hello e, em seguida, obtenham conectados por meio do AD do Azure pelo redirecionamento automático ou clicando no toosign link no. Isso é conhecido como provedor de serviços-iniciada pelo logon e mais aplicativos federados na Galeria de aplicativos de saudação do AD do Azure oferecem suporte a isso (consulte a documentação de saudação vinculada a partir do Assistente de configuração de logon único de saudação do aplicativo no portal de gerenciamento do Azure Olá para detalhes).

![][5]

### <a name="direct-sign-on-links-for-federated-password-based-or-existing-apps"></a>Links diretos logon para aplicativos federados, baseados em senha ou existentes
AD do Azure também oferece suporte a aplicativos de tooindividual único logon links diretos que oferecem suporte baseado em senha de logon único, logon único existente e nenhuma forma de logon único federado.

Esses links são URLs especialmente criados que enviam a um usuário por meio de saudação do Azure AD entrar no processo para um aplicativo específico sem exigir que o usuário Olá iniciá-los do painel de acesso de saudação do AD do Azure ou Office 365. As URLs de logon único pode ser encontradas na guia do painel de saudação de qualquer aplicativo pré-integrados Olá seção Active Directory do portal de gerenciamento do Azure hello, conforme mostrado na captura de tela de saudação abaixo.

![][6]

Esses links podem ser copiados e colados em qualquer lugar que você deseja tooprovide uma entrada link toohello selecionado aplicativo. Essa entrada poderia ser em um email ou em qualquer portal personalizado baseado na Web que você configurou o aplicativo para acesso de usuário. Aqui está um exemplo de uma URL de logon único direto do AD do Azure para o Twitter:

`https://myapps.microsoft.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

URLs tooorganization específico semelhantes para o painel de acesso hello, você pode personalizar ainda mais essa URL, adicionando um dos domínios de ativo ou verificado de saudação do seu diretório após o domínio de myapps.microsoft.com hello. Isso garante que qualquer identidade visual organizacional é carregada imediatamente na página de entrada hello sem precisar primeiro tooenter sua ID de usuário do usuário hello:

`https://myapps.microsoft.com/contosobuild.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Quando um usuário autorizado clica em um desses links específicos do aplicativo, eles primeiro ver sua página de entrada organizacional (supondo que eles não ainda tiver entrados) e depois de entrar são redirecionadas tootheir aplicativo sem parar primeiro no painel de acesso de saudação. Se usuário Olá tem pré-requisitos tooaccess Olá aplicativo, como a extensão de navegador de logon único baseado em senha hello, link Olá solicitará extensão ausente do Olá Olá usuário tooinstall. URL do link Olá também permanece constante se Olá configuração de logon único para o aplicativo hello mudar.

Esses links usam Olá mesmos mecanismos de controle de acesso como Olá acessar o painel e o Office 365, e apenas esses usuários ou grupos que foram atribuídos a toohello aplicativo no portal de gerenciamento do Azure Olá poderão autenticar toosuccessfully. No entanto, qualquer usuário que não está autorizado será exibida uma mensagem explicando o que eles não recebeu o acesso e que recebem um link tooload Olá acesso painel tooview aplicativos disponíveis para os quais têm acesso.

## <a name="related-articles"></a>Artigos relacionados
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [Encontrando aplicativos em nuvem não autorizados com o Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md)
* [Introdução tooManaging tooApps de acesso](active-directory-managing-access-to-apps.md)
* [Comparando recursos de gerenciamento de identidades externas no AD do Azure](active-directory-b2b-compare-external-identities.md)

<!--Image references-->
[1]: ./media/active-directory-appssoaccess-whatis/onlineappgallery.png
[2]: ./media/active-directory-appssoaccess-whatis/azuremgmtportal.png
[3]: ./media/active-directory-appssoaccess-whatis/accesspanel.png
[4]: ./media/active-directory-appssoaccess-whatis/officeapphub.png
[5]: ./media/active-directory-appssoaccess-whatis/workdaymobile.png
[6]: ./media/active-directory-appssoaccess-whatis/deeplink.png
