---
title: "aaaAuthentication cenários do AD do Azure | Microsoft Docs"
description: "Uma visão geral dos cenários mais comuns de autenticação do hello cinco para Azure Active Directory (AAD)"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 0c84e7d0-16aa-4897-82f2-f53c6c990fd9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: 5b391e3f096fcb52934c4a8aff08688352bfd3dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-scenarios-for-azure-ad"></a>Cenários de autenticação do AD do Azure
Azure Active Directory (AD do Azure) simplifica a autenticação para desenvolvedores, fornecendo identidade como um serviço, com suporte para protocolos de padrão da indústria, como OAuth 2.0 e OpenID Connect, bem como bibliotecas de código aberto para diferentes plataformas toohelp você Inicie a codificação rapidamente. Este documento ajudará você entender Olá suporte de vários cenários do AD do Azure e mostrará como tooget iniciada. Ele é dividido em Olá seções a seguir:

* [Noções básicas de autenticação no Azure AD.](#basics-of-authentication-in-azure-ad)
* [Declarações em tokens de segurança do Azure AD](#claims-in-azure-ad-security-tokens)
* [Noções básicas de registrar um aplicativo no Azure AD](#basics-of-registering-an-application-in-azure-ad)
* [Cenários e tipos de aplicativos](#application-types-and-scenarios)
  
  * [TooWeb de navegador da Web aplicativo](#web-browser-to-web-application)
  * [SPA (Aplicativo de Página Única)](#single-page-application-spa)
  * [TooWeb do aplicativo nativo API](#native-application-to-web-api)
  * [TooWeb de aplicativo da Web API](#web-application-to-web-api)
  * [TooWeb daemon ou aplicativo de servidor API](#daemon-or-server-application-to-web-api)

## <a name="basics-of-authentication-in-azure-ad"></a>Noções básicas de autenticação no Azure AD.
Se você não estiver familiarizado com os conceitos básicos de autenticação no Azure AD, leia esta seção. Caso contrário, talvez você queira tooskip para baixo demais[tipos de aplicativos e cenários](#application-types-and-scenarios).

Vamos considerar o cenário mais básico de saudação em que a identidade é necessária: tooauthenticate tooa aplicativo precisa de um usuário em um navegador da web. Este cenário é descrito mais detalhadamente nos Olá [tooWeb do navegador da Web aplicativo](#web-browser-to-web-application) seção, mas ele do útil iniciando tooillustrate ponto Olá recursos do AD do Azure e Conceituar como funciona o cenário de saudação. Considere Olá diagrama para este cenário a seguir:

![Visão geral do aplicativo de logon tooweb](./media/active-directory-authentication-scenarios/basics_of_auth_in_aad.png)

Com o diagrama de saudação acima em mente, aqui está o que você precisa tooknow sobre seus vários componentes:

* O AD do Azure é o provedor de identidade hello, responsável por verificar a identidade de saudação de usuários e aplicativos que existem no diretório da organização e, finalmente, emitir tokens de segurança após a autenticação bem-sucedida desses usuários e aplicativos.
* Um aplicativo que deseja toooutsource autenticação tooAzure AD deve ser registrado no AD do Azure, que registra e identifica exclusivamente o aplicativo hello no diretório de saudação.
* Os desenvolvedores podem usar Olá software livre do AD do Azure bibliotecas toomake autenticação fácil ao manipular detalhes de protocolo Olá para você. Consulte [Bibliotecas de autenticação do Azure Active Directory](active-directory-authentication-libraries.md) para obter mais informações.

• Uma vez um usuário foi autenticado, o aplicativo hello deve validar tooensure de token de segurança do usuário Olá que a autenticação tenha sido bem-sucedida para Olá se destina a partes. Os desenvolvedores podem usar Olá fornecido a validação de toohandle de bibliotecas de autenticação de qualquer token do AD do Azure, incluindo o JSON Web Tokens (JWT) ou SAML 2.0. Se você quiser tooperform validação manualmente, consulte Olá [manipulador de Token de JWT](https://msdn.microsoft.com/library/dn205065.aspx) documentação.

> [!IMPORTANT]
> O AD do Azure usa criptografia de chave pública toosign tokens e verificar se eles são válidos. Consulte [importantes informações sobre assinatura de substituição de chave no AD do Azure](active-directory-signing-key-rollover.md) para obter mais informações sobre a lógica necessária Olá que você deve ter em seu aplicativo tooensure ele esteja sempre atualizado com chaves de hello mais recentes.
> 
> 

• fluxo de saudação de solicitações e respostas Olá processo de autenticação é determinado pelo protocolo de autenticação de saudação que foi usado, como OAuth 2.0, OpenID Connect, WS-Federation ou SAML 2.0. Esses protocolos são discutidos detalhadamente no hello [protocolos de autenticação do Azure Active Directory](active-directory-authentication-protocols.md) tópico e nas seções de saudação abaixo.

> [!NOTE]
> AD do Azure suporta Olá OAuth 2.0 e OpenID Connect normas de amplo usam de tokens de portador, incluindo tokens de portador representados como JWTs. Um token de portador é o recurso protegido de um token de segurança leve que concede Olá tooa de acesso de "portador". Nesse sentido, Olá "portador" é qualquer parte que pode apresentar um token de saudação. Embora uma parte deve primeiro autenticar com o token de portador de saudação do AD do Azure tooreceive, se Olá necessárias não são as etapas seguidas token de saudação toosecure durante a transmissão e armazenamento, pode ser interceptado e usado por uma parte não pretendida. Embora alguns tokens de segurança tenham um mecanismo interno para impedir que partes não autorizadas os utilizem, tokens de portador não possuem esse mecanismo e devem ser transportados em um canal seguro, como segurança da camada de transporte (HTTPS). Se um token de portador for transmitido no hello criptografado, um ataque intermediária Olá man-in pode ser usado por um token de saudação do terceiro mal-intencionado tooacquire e usá-lo para um recurso de tooa protegido do acesso não autorizado. Olá mesmos princípios de segurança se aplicam ao armazenar ou armazenamento em cache os tokens de portador para uso posterior. Sempre certifique-se de que seu aplicativo transmita e armazene tokens de portador de maneira segura. Para obter mais considerações de segurança sobre tokens de portador, consulte [RFC 6750 seção 5](http://tools.ietf.org/html/rfc6750).
> 
> 

Agora que você tem uma visão geral dos conceitos básicos da saudação, leia as seções de saudação abaixo toounderstand como provisionamento funciona no AD do Azure e oferece suporte a cenários comuns de saudação do AD do Azure.

## <a name="claims-in-azure-ad-security-tokens"></a>Declarações em tokens de segurança do Azure AD
Tokens de segurança emitidos pelo AD do Azure contêm declarações ou asserções de informações sobre o assunto de saudação que foi autenticado. Essas declarações podem ser usadas pelo aplicativo hello para várias tarefas. Por exemplo, eles podem ser toovalidate usado Olá token, identificar o locatário de diretório da entidade Olá, exibir informações do usuário, determinar a autorização da entidade Olá e assim por diante. Olá declarações presentes em qualquer token de segurança variam de acordo com o tipo de saudação do token, o tipo de Olá da credencial usada tooauthenticate Olá usuário e a configuração do aplicativo hello. Uma breve descrição de cada tipo de declaração emitida pelo AD do Azure é fornecida na tabela de saudação abaixo. Para obter mais informações, consulte muito[tipos de declaração e Token com suporte](active-directory-token-and-claims.md).

| Declaração | Descrição |
| --- | --- |
| ID do aplicativo |Identifica o aplicativo hello que está usando o token de saudação. |
| Público-alvo |Identifica o recurso do destinatário Olá Olá token é destinado. |
| Referência de classe de contexto de autenticação de aplicativo |Indica como o cliente Olá foi autenticado (cliente público versus cliente confidencial). |
| Instante da autenticação |Registros Olá data e hora em que ocorreu a autenticação de saudação. |
| Método de autenticação |Indica como o assunto de saudação do token Olá foi autenticado (senha, certificado, etc.). |
| Nome |Fornece Olá nome de usuário de saudação conforme definido no AD do Azure. |
| Grupos |Contém Olá usuário é um membro de grupos de objetos de Ids do Azure AD. |
| Provedor de identidade |Registros Olá provedor de identidade que autenticou o assunto de saudação do token hello. |
| Emitido em |Tempo de saudação de registros em qual Olá token foi emitido, geralmente usado para atualização de token. |
| Emissor |Identifica Olá STS que emitiu o token hello, bem como o locatário do AD do Azure hello. |
| Sobrenome |Fornece o sobrenome de saudação do usuário Olá conforme definido no AD do Azure. |
| Nome |Fornece um valor legível que identifica a entidade de saudação do token de saudação. |
| ID do objeto |Contém um identificador exclusivo e imutável do assunto Olá no AD do Azure. |
| Funções |Contém os nomes amigáveis de funções de aplicativo do AD do Azure que o usuário Olá foi concedido. |
| Escopo |Indica o aplicativo hello cliente toohello, concedidas permissões. |
| Assunto |Indica a entidade Olá sobre quais Olá token dá informações. |
| ID do locatário |Contém um identificador exclusivo e imutável do locatário de diretório Olá que emitiu o token de saudação. |
| Tempo de vida do token |Define o intervalo de tempo de saudação no qual um token é válido. |
| Nome UPN |Contém o nome principal do usuário de saudação do assunto de saudação. |
| Versão |Contém o número de versão de saudação do token de saudação. |

## <a name="basics-of-registering-an-application-in-azure-ad"></a>Noções básicas de registrar um aplicativo no Azure AD
Qualquer aplicativo que terceirize a autenticação tooAzure que AD deve ser registrado em um diretório. Esta etapa envolve comunicar ao AD do Azure sobre seu aplicativo, incluindo URL Olá onde ele está localizado, Olá URL toosend respostas após a autenticação, Olá URI tooidentify seu aplicativo e muito mais. Essas informações são necessárias por alguns motivos:

* AD do Azure precisa de coordenadas toocommunicate com o aplicativo hello ao manipular tokens de logon ou de troca. Eles incluem o seguinte hello:
  
  * URI da ID do aplicativo: Olá identificador de um aplicativo. Esse valor é enviado tooAzure AD durante a autenticação tooindicate quais chamador de saudação do aplicativo deseja um token. Além disso, esse valor é incluído no token Olá para que o aplicativo hello Saiba que ele foi Olá se destina o destino.
  * Responder a URL e o URI de redirecionamento: no caso de saudação de uma API da web ou aplicativo web, Olá URL de resposta é Olá local toowhich AD do Azure enviará a resposta de autenticação hello, incluindo um token se a autenticação for bem-sucedida. No caso de saudação de um aplicativo nativo, Olá URI de redirecionamento é que um identificador exclusivo de toowhich AD do Azure redirecionará Olá agente do usuário em uma solicitação OAuth 2.0.
  * ID do aplicativo: hello ID para um aplicativo, que é gerado pelo AD do Azure, quando o aplicativo hello é registrado. Ao solicitar um código de autorização ou token, Olá ID do aplicativo e a chave são enviadas tooAzure AD durante a autenticação.
  * : Olá chave enviada juntamente com uma ID de aplicativo ao autenticar tooAzure AD toocall uma API da web.
* Necessidades de AD do Azure tooensure Olá aplicativo tem Olá permissões necessárias tooaccess os dados do diretório, outros aplicativos em sua organização e assim por diante

O provisionamento fica mais claro quando você entende que há duas categorias de aplicativos que podem ser desenvolvidos e integrados no Azure AD:

* Aplicativo de locatário único: um aplicativo de locatário único destina-se ao uso em uma organização. Eles normalmente são aplicativos de linha de negócios (LoB) escritos por um desenvolvedor empresarial. Um aplicativo de locatário único só precisa toobe acessado por usuários em um diretório e como resultado, ele só precisa toobe provisionado em um diretório. Esses aplicativos normalmente são registrados por um desenvolvedor na organização hello.
* Aplicativos multilocatários: um aplicativo multilocatário é destinado para uso em muitas organizações, não apenas em uma organização. Esses são normalmente aplicativos de software como serviço (SaaS) escritos por um fornecedor de software independente (ISV). Aplicativos de multilocação precisam toobe provisionado em cada diretório em que eles serão usados, o que exige tooregister de consentimento do usuário ou administrador-los. Esse processo de consentimento inicia quando um aplicativo tiver sido registrado no diretório hello e recebe acesso toohello Graph API ou talvez a outra API da web. Quando um usuário ou administrador de uma organização diferente se inscreve toouse aplicativo de hello, são apresentadas com uma caixa de diálogo que exibe permissões Olá Olá aplicativo requer. Olá usuário ou administrador pode consentimento toohello aplicativo, que fornece toohello de acesso do aplicativo hello mencionado dados, e finalmente registra Olá aplicativo em seu diretório. Para obter mais informações, consulte [visão geral da estrutura de consentimento do hello](active-directory-integrating-applications.md#overview-of-the-consent-framework).

Surgem algumas considerações adicionais ao desenvolver um aplicativo multilocatário em vez de um aplicativo de locatário único. Por exemplo, se você estiver fazendo o toousers disponíveis do aplicativo em vários diretórios, é necessário um mecanismo toodetermine qual locatário que estão contidos. Um aplicativo de locatário único só precisa toolook em seu próprio diretório para um usuário, enquanto um aplicativo multilocatário, precisa tooidentify um usuário específico em todos os diretórios de saudação no AD do Azure. tooaccomplish nesta tarefa, o AD do Azure fornece um ponto de extremidade de autenticação comum em que qualquer aplicativo multilocatário pode direcionar solicitações de entrada, em vez de um ponto de extremidade específico de locatário. Esse ponto de extremidade é https://login.microsoftonline.com/common para todos os diretórios no AD do Azure, enquanto que um ponto de extremidade específico de locatário pode ser https://login.microsoftonline.com/contoso.onmicrosoft.com. ponto de extremidade comum Olá é especialmente importante tooconsider ao desenvolver seu aplicativo, pois você precisará Olá lógica necessária toohandle vários locatários durante a entrada, saída e validação de token.

Se você está desenvolvendo um aplicativo de locatário único, mas deseja toomake-organizações toomany disponível, você pode facilmente fazer alterações toohello aplicativo e sua configuração no AD do Azure toomake-lo compatível com multilocatário. Além disso, o AD do Azure usa Olá mesma chave para todos os tokens em todos os diretórios de assinatura, se você estiver fornecendo autenticação em um locatário único ou um aplicativo multilocatário.

Cada cenário listado neste documento inclui uma subseção que descreve seus requisitos de provisionamento. Para obter informações mais detalhadas sobre o provisionamento de um aplicativo no AD do Azure e Olá diferenças entre aplicativos único e vários locatários, consulte [integrando aplicativos com o Active Directory do Azure](active-directory-integrating-applications.md) para obter mais informações. Continue a leitura toounderstand cenários comuns de aplicativo hello no AD do Azure.

## <a name="application-types-and-scenarios"></a>Cenários e tipos de aplicativos
Cada um dos cenários de saudação descritos neste documento pode ser desenvolvida usando diversas plataformas e linguagens. Eles são copiados por exemplos de código completo que estão disponíveis no nosso [guia de exemplos de código](active-directory-code-samples.md), ou diretamente da saudação correspondente [repositórios de exemplo do GitHub](https://github.com/Azure-Samples?utf8=%E2%9C%93&query=active-directory). Além disso, se seu aplicativo precisar de uma parte ou segmento específico de um cenário de ponta a ponta, na maioria dos casos, essa funcionalidade pode ser adicionada independentemente. Por exemplo, se você tiver um aplicativo nativo que chama uma API da web, você pode adicionar facilmente um aplicativo web que também chama Olá web API. Olá diagrama a seguir ilustra esses cenários e tipos de aplicativos, e como os diferentes componentes podem ser adicionados:

![Cenários e tipos de aplicativos](./media/active-directory-authentication-scenarios/application_types_and_scenarios.png)

Estes são Olá cinco aplicativos principais cenários suportados pelo AD do Azure:

* [Web navegador tooWeb aplicativo](#web-browser-to-web-application): um usuário precisa toosign no aplicativo web tooa que é protegido pelo AD do Azure.
* [Um único aplicativo de página (SPA)](#single-page-application-spa): um usuário precisa toosign no aplicativo de página única tooa que é protegido pelo AD do Azure.
* [TooWeb do aplicativo nativo API](#native-application-to-web-api): um aplicativo nativo que é executado em um telefone, tablet ou PC necessidades tooauthenticate tooget um usuário recursos de uma API da web que é protegido pelo AD do Azure.
* [Web Application tooWeb API](#web-application-to-web-api): um aplicativo web precisa tooget recursos de uma API da web protegida pelo AD do Azure.
* [TooWeb daemon ou aplicativo de servidor API](#daemon-or-server-application-to-web-api): um aplicativo daemon ou um aplicativo de servidor sem interface de usuário da web precisa tooget recursos de uma API da web protegida pelo AD do Azure.

### <a name="web-browser-tooweb-application"></a>TooWeb de navegador da Web aplicativo
Esta seção descreve um aplicativo que autentica um usuário em um aplicativo de web de tooa de navegador da web. Nesse cenário, o aplicativo de web de Olá direciona toosign do navegador do usuário Olá em tooAzure AD. AD do Azure retorna uma resposta de logon por meio do navegador do usuário hello, que contém declarações sobre o usuário Olá em um token de segurança. Este cenário dá suporte a logon usando protocolos WS-Federation, SAML 2.0 e OpenID Connect do hello.

#### <a name="diagram"></a>Diagrama
![Fluxo de autenticação do aplicativo do navegador tooweb](./media/active-directory-authentication-scenarios/web_browser_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Descrição do fluxo de protocolo
1. Quando um usuário visita o aplicativo hello e precisa toosign no, ele será redirecionado por meio de um ponto de extremidade de autenticação de toohello de solicitação de entrada no AD do Azure.
2. Olá usuário se inscreve página de entrada hello.
3. Se a autenticação for bem-sucedida, o AD do Azure cria um token de autenticação e retorna a URL de resposta do aplicativo de toohello uma resposta de logon que foi configurado no hello Portal do Azure. Para um aplicativo de produção, essa URL de resposta deve ser HTTPS. Olá retornada um token inclui declarações sobre o usuário hello e AD do Azure que são exigidas pelo token de Olá Olá aplicativo toovalidate.
4. aplicativo Hello valida o token hello usando uma chave pública de assinatura e as informações de emissor disponíveis no documento de metadados de federação de saudação do AD do Azure. Depois que o aplicativo hello valida o token hello, o AD do Azure inicia uma nova sessão com usuário hello. Essa sessão permite Olá usuário tooaccess aplicativo hello até expirar.

#### <a name="code-samples"></a>Exemplos de código
Consulte exemplos de código de saudação para cenários de aplicativo do navegador da Web tooWeb. E, volte a consultar frequentemente - adicionamos novos exemplos de todo o tempo de saudação. [Web navegador tooWeb aplicativo](active-directory-code-samples.md#web-browser-to-web-application).

#### <a name="registering"></a>Registro
* Único locatário: Se você estiver criando um aplicativo para a sua organização, ele deve ser registrado no diretório da empresa usando Olá Portal do Azure.
* Multilocatário: Se você estiver criando um aplicativo que pode ser usado por usuários fora da sua organização, ele deve ser registrado no diretório da sua empresa, mas também deve ser registrado no diretório de cada organização que usará o aplicativo hello. toomake seu aplicativo disponível em seu diretório, você pode incluir um processo de inscrição para os clientes que permite que eles tooconsent tooyour aplicativo. Ao se inscreverem para seu aplicativo, eles verá uma caixa de diálogo que mostra Olá permissões Olá exigidos e, em seguida, Olá tooconsent opção. Dependendo de permissões Olá necessárias, um administrador no hello outra organização pode ser necessário toogive consentimento. Quando Olá usuário ou administrador der consentimento, o aplicativo hello está registrado no seu diretório. Para saber mais, confira [Integrando aplicativos com o Active Directory do Azure](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Expiração do token
sessão de usuário de saudação expira quando o tempo de vida de saudação do hello token emitido pelo AD do Azure expire. Seu aplicativo pode encurtar esse período de tempo, se desejado, por exemplo, desconectando usuários com base em um período de inatividade. Quando a sessão de saudação expira, o usuário de Olá será toosign solicitada no novamente.

### <a name="single-page-application-spa"></a>SPA (Aplicativo de Página Única)
Esta seção descreve a autenticação de um único aplicativo de página, que usa o AD do Azure e autorização implícita do OAuth 2.0 hello conceder toosecure terminar de fazer sua API da web. Aplicativos de página única normalmente são estruturados como uma camada de apresentação de JavaScript (front-end) que é executado no navegador hello e um back-end de API da Web que é executado em um servidor e implementa Olá lógica de negócios do aplicativo. toolearn mais informações sobre concessão de autorização implícita hello e ajuda você a decidir se é adequado para seu cenário de aplicativo, consulte [Olá Noções básicas sobre implícita do OAuth2 conceder fluxo no Azure Active Directory](active-directory-dev-understanding-oauth2-implicit-grant.md).

Nesse cenário, quando o usuário Olá entrar, Olá JavaScript front end usa [Active Directory Authentication Library para JavaScript (ADAL. JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js/tree/dev) e autorização implícita Olá conceder tooobtain um token de ID (id_token) do AD do Azure. token Olá é armazenado em cache e cliente Olá anexa-toohello solicitação como token de portador Olá ao fazer chamadas tooits API da Web do back-end, que é protegida usando Olá OWIN middleware. 

#### <a name="diagram"></a>Diagrama
![Diagrama de Aplicativo de Página Única](./media/active-directory-authentication-scenarios/single_page_app.png)

#### <a name="description-of-protocol-flow"></a>Descrição do fluxo de protocolo
1. usuário Olá navega toohello aplicativo de web.
2. aplicativo Hello retorna navegador de toohello Olá JavaScript front-end (camada de apresentação).
3. usuário Olá inicia a entrada, por exemplo, clicando em uma link de entrada. navegador Olá envia um token de ID de toorequest de ponto de extremidade de autorização um GET toohello AD do Azure. Essa solicitação inclui a URL de resposta e a ID de aplicativo de Olá nos parâmetros de consulta de saudação.
4. AD do Azure valida Olá que URL de resposta em relação a saudação registrado URL de resposta que foi configurado no hello Portal do Azure.
5. Olá usuário se inscreve página de entrada hello.
6. Se a autenticação for bem-sucedida, o AD do Azure cria um token de ID e o retorna como URL de resposta do aplicativo um URL fragmento (#) toohello. Para um aplicativo de produção, essa URL de resposta deve ser HTTPS. Olá retornada um token inclui declarações sobre o usuário hello e AD do Azure que são exigidas pelo token de Olá Olá aplicativo toovalidate.
7. código do cliente Olá JavaScript em execução no navegador de saudação extrai o token de saudação do hello resposta toouse proteger chamadas de API de web do aplicativo toohello volta terminar.
8. Olá end da API web do aplicativo do navegador chamadas Olá novamente com o token de acesso de saudação no cabeçalho de autorização de saudação.

#### <a name="code-samples"></a>Exemplos de código
Consulte exemplos de código de saudação para cenários de aplicativo de página única (SPA). Ser toocheck-se novamente com frequência – adicionamos novos exemplos todo o tempo de saudação. [SPA (Aplicativo de Página Única)](active-directory-code-samples.md#single-page-application-spa).

#### <a name="registering"></a>Registro
* Único locatário: Se você estiver criando um aplicativo para a sua organização, ele deve ser registrado no diretório da empresa usando Olá Portal do Azure.
* Multilocatário: Se você estiver criando um aplicativo que pode ser usado por usuários fora da sua organização, ele deve ser registrado no diretório da sua empresa, mas também deve ser registrado no diretório de cada organização que usará o aplicativo hello. toomake seu aplicativo disponível em seu diretório, você pode incluir um processo de inscrição para os clientes que permite que eles tooconsent tooyour aplicativo. Ao se inscreverem para seu aplicativo, eles verá uma caixa de diálogo que mostra Olá permissões Olá exigidos e, em seguida, Olá tooconsent opção. Dependendo de permissões Olá necessárias, um administrador no hello outra organização pode ser necessário toogive consentimento. Quando Olá usuário ou administrador der consentimento, o aplicativo hello está registrado no seu diretório. Para saber mais, confira [Integrando aplicativos com o Active Directory do Azure](active-directory-integrating-applications.md).

Depois de registrar o aplicativo hello, ele deve ser configurado toouse protocolo de concessão implícita do OAuth 2.0. Por padrão, esse protocolo é desabilitado para aplicativos. Olá tooenable protocolo de concessão implícita do OAuth2 para seu aplicativo, edite o manifesto do aplicativo de saudação Portal do Azure e defina tootrue de valor de "oauth2AllowImplicitFlow" hello. Para obter instruções detalhadas, consulte [Habilitar a concessão implícita do OAuth 2.0 para aplicativos de página única](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Expiração do token
Quando você usa o ADAL.js toomanage autenticação com o AD do Azure, você se beneficiar de vários recursos que facilitam a atualização de um token expirado, bem como obter tokens para recursos da API da web adicionais que podem ser chamados por um aplicativo hello. Quando o usuário Olá autentica com êxito com o Azure AD, é estabelecida uma sessão protegida por um cookie para o usuário Olá entre navegador hello e Azure AD. É importante toonote que sessão Olá existe entre o usuário hello e AD do Azure e não entre o usuário hello e aplicativo web de saudação em execução no servidor de saudação. Quando um token expira, o ADAL.js usa essa sessão toosilently obter outro token. Ele faz isso usando um iFrame oculto toosend e receber a solicitação de saudação usando o protocolo de concessão implícita do OAuth hello. ADAL.js também pode usar o mesmo mecanismo toosilently obter tokens de acesso do AD do Azure para outra web API recursos que chamadas de aplicativo hello como esses recursos oferecem suporte a recursos de origens cruzadas compartilhando (CORS), são registradas no diretório saudação do usuário, e qualquer consentimento necessário foi fornecido pelo usuário Olá durante o logon.

### <a name="native-application-tooweb-api"></a>TooWeb do aplicativo nativo API
Esta seção descreve um aplicativo nativo que chama uma API da Web em nome de um usuário. Este cenário se baseia no tipo de concessão de código de autorização de saudação OAuth 2.0 com um cliente público, conforme descrito na seção 4.1 da saudação [especificação OAuth 2.0](http://tools.ietf.org/html/rfc6749). aplicativo nativo Hello obtém um token de acesso de usuário de saudação usando o protocolo de saudação OAuth 2.0. Esse token de acesso é enviado na Olá solicitação toohello API da web, que autoriza o usuário hello e retorna o recurso de saudação desejado.

#### <a name="diagram"></a>Diagrama
![TooWeb do aplicativo nativo diagrama de API](./media/active-directory-authentication-scenarios/native_app_to_web_api.png)

#### <a name="authentication-flow-for-native-application-tooapi"></a>Fluxo de autenticação do aplicativo nativo tooAPI
#### <a name="description-of-protocol-flow"></a>Descrição do fluxo de protocolo
Se você estiver usando bibliotecas de autenticação Olá AD, a maioria dos detalhes de protocolo hello descritas abaixo é tratada para você, como pop-up do navegador hello, cache de token e manipulação de tokens de atualização.

1. Usando um pop-up do navegador, o aplicativo nativo hello faz um ponto de extremidade de autorização de toohello de solicitação no AD do Azure. Essa solicitação inclui hello ID do aplicativo e redirecionamento de saudação URI do aplicativo nativo hello conforme mostrado no hello Portal do Azure e o aplicativo hello URI de ID para a API da web hello. Se o usuário Olá ainda não tiver entrado, que sejam solicitada toosign no novamente
2. Azure AD autentica o usuário hello. Se for um aplicativo multilocatário e consentimento for necessário toouse Olá aplicativo, o usuário de Olá será tooconsent necessária se eles ainda não tiver feito isso. Após dar consentimento e após a autenticação bem-sucedida, o Azure AD emite o URI de redirecionamento de uma autorização código resposta toohello voltar do aplicativo cliente.
3. Quando o AD do Azure envia de volta uma resposta de código de autorização toohello URI de redirecionamento, Olá paradas de navegador interação e extrai Olá autorização código do aplicativo cliente de resposta de saudação. Usando esse código de autorização, aplicativo de cliente de saudação envia uma solicitação de tooAzure do AD do ponto de extremidade que inclui o código de autorização de saudação, detalhes sobre Olá aplicativo cliente (ID do aplicativo e URI de redirecionamento) e Olá recurso desejado (ID do aplicativo URI para a API da web hello).
4. código de autorização Hello e obter informações sobre o aplicativo de cliente hello e a API da web são validados pelo AD do Azure. Após a validação bem-sucedida, o Azure AD retorna dois tokens: um token de acesso JWT e um token de atualização JWT. Além disso, o AD do Azure retorna informações básicas sobre o usuário hello, como seu ID de nome e de locatário de exibição
5. Via HTTPS, o aplicativo de cliente de saudação usa Olá retornado Olá tooadd token de acesso JWT cadeia de caracteres JWT com uma designação "Portador" no cabeçalho de autorização de saudação da API da web do toohello Olá solicitação. Olá web API, em seguida, valida o token JWT hello e se a validação for bem-sucedida, retorna Olá desejado de recursos.
6. Quando o token de acesso de saudação expira, aplicativo de cliente hello receberá um erro que indica que o usuário de saudação precisa tooauthenticate novamente. Se o aplicativo hello tem um token de atualização válido, pode ser usado tooacquire um novo token de acesso sem solicitar Olá toosign de usuário em novamente. Se o token de atualização de saudação expira, o aplicativo hello precisará toointeractively autenticar usuário Olá novamente.

> [!NOTE]
> o token de atualização Olá emitido pelo AD do Azure pode ser usado tooaccess vários recursos. Por exemplo, se você tiver um aplicativo cliente que tem APIs da web de toocall dois permissão, o token de atualização Olá pode ser usado tooget uma acesso toohello token outra API da web também.
> 
> 

#### <a name="code-samples"></a>Exemplos de código
Consulte exemplos de código de saudação para cenários de API do aplicativo nativo tooWeb. E, volte a consultar frequentemente - adicionamos novos exemplos de todo o tempo de saudação. [TooWeb do aplicativo nativo API](active-directory-code-samples.md#native-application-to-web-api).

#### <a name="registering"></a>Registro
* Único locatário: Ambos Olá aplicativo nativo e Olá web API deve ser registrada no hello mesmo diretório no AD do Azure. Olá web API pode ser configurado tooexpose um conjunto de permissões, que são usados toolimit Olá nativo acesso tooits recursos de aplicativo. aplicativo de cliente Hello, em seguida, seleciona permissões Olá desejado no menu Olá suspenso "Permissões tooOther aplicativos" hello Portal do Azure.
* Multilocatário: Primeiro, aplicativo nativo hello registrou-se apenas no diretório Olá desenvolvedor ou do publicador. Segundo, o aplicativo nativo hello é configurado tooindicate Olá permissões requer toobe funcional. Esta lista de permissões necessárias é mostrada em uma caixa de diálogo quando um usuário ou administrador no diretório de destino Olá dá consentimento toohello aplicativo, o que torna disponíveis tootheir organização. Alguns aplicativos exigem permissões de nível de usuário, que qualquer usuário na organização Olá pode consentir. Outros aplicativos exigem permissões de administrador, que um usuário de organização de saudação não pode consentir. Somente um administrador do diretório pode dar consentimento tooapplications que requerem esse nível de permissões. Quando Olá usuário ou administrador der consentimento, apenas Olá API da web está registrado no seu diretório. Para saber mais, confira [Integrando aplicativos com o Active Directory do Azure](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Expiração do token
Quando o aplicativo nativo hello usa seu código de autorização tooget um token de acesso JWT, ele também recebe um token de atualização JWT. Quando o token de acesso de saudação expira, token de atualização de saudação pode ser usado toore-autenticar o usuário Olá sem exigir que eles toosign em novamente. Esse token de atualização é usado tooauthenticate Olá usuário, que resulta em um novo acesso de token e de atualização de token.

### <a name="web-application-tooweb-api"></a>TooWeb de aplicativo da Web API
Esta seção descreve um aplicativo web que precisa de recursos de tooget de uma API da web. Nesse cenário, há dois tipos de identidade que Olá aplicativo web podem usar tooauthenticate e chamar a API da web do hello: uma identidade de aplicativo, ou uma identidade de usuário delegado.

*Identidade do aplicativo:* essa usa cenário as credenciais do cliente OAuth 2.0 conceder tooauthenticate como aplicativo hello e hello de acesso web API. Ao usar uma identidade de aplicativo, Olá web API só pode detectar que o aplicativo hello está chamando, como Olá API da web não recebe todas as informações sobre usuário hello. Se o aplicativo hello recebe informações sobre o usuário hello, ele será enviado por meio do protocolo de aplicativo hello e ele não está assinado pelo AD do Azure. API da web Hello confia que o aplicativo da web hello autenticado usuário hello. Por esse motivo, esse padrão é chamado de subsistema confiável.

*Identidade de usuário delegado:* o cenário pode ser realizado de duas maneiras, OpenID Connect e concessão de código de autorização OAuth 2.0 com um cliente confidencial. aplicativo da web Hello obtém um token de acesso de usuário hello, que prova toohello web API esse aplicativo de web toohello Olá usuário autenticado com êxito e que o aplicativo da web hello foi capaz de tooobtain um usuário delegado identidade toocall Olá API da web. Esse token de acesso é enviado em Olá solicitação toohello API da web, que autoriza o usuário hello e retorna o recurso de saudação desejado.

#### <a name="diagram"></a>Diagrama
![Diagrama de tooWeb API do aplicativo de Web](./media/active-directory-authentication-scenarios/web_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Descrição do fluxo de protocolo
Ambos Olá identidade de aplicativo e tipos de identidade de usuário delegado são discutidos no fluxo de saudação abaixo. Olá principal diferença entre eles é que Olá delegada a identidade do usuário deve primeiro adquirir um código de autorização antes de saudação usuário pode entrar e obter acesso toohello web API.

##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>Identidade do aplicativo com concessão de credenciais do cliente OAuth 2.0
1. Um usuário está conectado no tooAzure AD no aplicativo da web hello (consulte Olá [tooWeb do navegador da Web aplicativo](#web-browser-to-web-application) acima).
2. aplicativo da web Hello precisa tooacquire um token de acesso para que ele possa autenticar toohello web API e recuperar o recurso de saudação desejado. Faz uma tooAzure de solicitação do AD do ponto de extremidade token, fornecendo credenciais de hello, ID do aplicativo e URI de ID do aplicativo da API da web.
3. O AD do Azure autentica o aplicativo hello e retorna um token de acesso JWT que é usado toocall Olá web API.
4. Via HTTPS, o aplicativo da web hello usa Olá retornado Olá tooadd token de acesso JWT cadeia de caracteres JWT com uma designação "Portador" no cabeçalho de autorização de saudação da API da web do toohello Olá solicitação. Olá web API, em seguida, valida o token JWT hello e se a validação for bem-sucedida, retorna Olá desejado de recursos.

##### <a name="delegated-user-identity-with-openid-connect"></a>Identidade de usuário delegado com OpenID Connect
1. Um usuário está conectado no aplicativo web de tooa usando o AD do Azure (consulte Olá [tooWeb do navegador da Web aplicativo](#web-browser-to-web-application) seção acima). Se o usuário de saudação do aplicativo da web hello não consentiu ainda tooallowing Olá web aplicativo toocall Olá API da web em seu nome, o usuário Olá precisará tooconsent. aplicativo Hello exibirá permissões Olá requer e, se qualquer uma dessas permissões de administrador, um usuário normal no diretório de saudação não será capaz de tooconsent. Esse processo de consentimento só se aplica a aplicativos de locatário toomulti, aplicativos de locatário não único, como aplicativo hello já terão as permissões necessárias de saudação. Quando hello usuário conectado, o aplicativo hello recebeu um token de ID com informações sobre o usuário hello, bem como um código de autorização.
2. Usando o código de autorização Olá emitido pelo AD do Azure, aplicativo da web hello envia uma solicitação de tooAzure do AD do ponto de extremidade que inclui o código de autorização de saudação, detalhes sobre o aplicativo de cliente hello (ID do aplicativo e URI de redirecionamento) e hello desejado de recurso ( aplicativo do URI de ID para Olá web API).
3. código de autorização Hello e obter informações sobre o aplicativo da web hello e a API da web são validados pelo AD do Azure. Após a validação bem-sucedida, o Azure AD retorna dois tokens: um token de acesso JWT e um token de atualização JWT.
4. Via HTTPS, o aplicativo da web hello usa Olá retornado Olá tooadd token de acesso JWT cadeia de caracteres JWT com uma designação "Portador" no cabeçalho de autorização de saudação da API da web do toohello Olá solicitação. Olá web API, em seguida, valida o token JWT hello e se a validação for bem-sucedida, retorna Olá desejado de recursos.

##### <a name="delegated-user-identity-with-oauth-20-authorization-code-grant"></a>Identidade de usuário delegado com concessão de código de autorização do OAuth 2.0
1. Um usuário já está conectado no aplicativo da web tooa, cujo mecanismo de autenticação é independente do AD do Azure.
2. Olá aplicativo web requer uma autorização de código tooacquire um token de acesso, portanto, envia uma solicitação por meio do ponto de extremidade de autorização de Olá navegador tooAzure do AD, fornecendo Olá ID do aplicativo e URI de redirecionamento para o aplicativo da web hello após bem-sucedida autenticação. usuário Olá entra tooAzure AD.
3. Se o usuário de saudação do aplicativo da web hello não consentiu ainda tooallowing Olá web aplicativo toocall Olá API da web em seu nome, o usuário Olá precisará tooconsent. aplicativo Hello exibirá permissões Olá requer e, se qualquer uma dessas permissões de administrador, um usuário normal no diretório de saudação não será capaz de tooconsent. Esse consentimento aplica tooboth único e multilocatário o aplicativo.  No caso de locatário único hello, um administrador pode executar tooconsent de consentimento do administrador em nome dos seus usuários.  Isso pode ser feito usando Olá `Grant Permissions` botão Olá [Portal do Azure](https://portal.azure.com). 
4. Após Olá usuário consentiu, aplicativo da web hello recebe código de autorização de saudação que precisa tooacquire um token de acesso.
5. Usando o código de autorização Olá emitido pelo AD do Azure, aplicativo da web hello envia uma solicitação de tooAzure do AD do ponto de extremidade que inclui o código de autorização de saudação, detalhes sobre o aplicativo de cliente hello (ID do aplicativo e URI de redirecionamento) e hello desejado de recurso ( aplicativo do URI de ID para Olá web API).
6. código de autorização Hello e obter informações sobre o aplicativo da web hello e a API da web são validados pelo AD do Azure. Após a validação bem-sucedida, o Azure AD retorna dois tokens: um token de acesso JWT e um token de atualização JWT.
7. Via HTTPS, o aplicativo da web hello usa Olá retornado Olá tooadd token de acesso JWT cadeia de caracteres JWT com uma designação "Portador" no cabeçalho de autorização de saudação da API da web do toohello Olá solicitação. Olá web API, em seguida, valida o token JWT hello e se a validação for bem-sucedida, retorna Olá desejado de recursos.

#### <a name="code-samples"></a>Exemplos de código
Consulte exemplos de código de saudação para cenários de API de tooWeb do aplicativo Web. E, volte a consultar frequentemente - adicionamos novos exemplos de todo o tempo de saudação. Web [tooWeb aplicativo API](active-directory-code-samples.md#web-application-to-web-api).

#### <a name="registering"></a>Registro
* Único locatário: Identidade de aplicativo hello e casos de identidade de usuário delegado, Olá aplicativo web e Olá web API deve ser registrada no hello mesmo diretório no AD do Azure. Olá web API pode ser configurado tooexpose um conjunto de permissões, que são usados toolimit Olá web access tooits recursos de aplicativo. Se um tipo de identidade de usuário delegado estiver sendo usado, o aplicativo da web de Olá precisa tooselect permissões de saudação desejada no menu Olá suspenso "Permissões tooOther aplicativos" hello Portal do Azure. Essa etapa não será necessária se o tipo de identidade de aplicativo hello está sendo usado.
* Multilocatário: Primeiro, aplicativo da web hello é configurado tooindicate Olá permissões requer toobe funcional. Esta lista de permissões necessárias é mostrada em uma caixa de diálogo quando um usuário ou administrador no diretório de destino Olá dá consentimento toohello aplicativo, o que torna disponíveis tootheir organização. Alguns aplicativos exigem permissões de nível de usuário, que qualquer usuário na organização Olá pode consentir. Outros aplicativos exigem permissões de administrador, que um usuário de organização de saudação não pode consentir. Somente um administrador do diretório pode dar consentimento tooapplications que requerem esse nível de permissões. Quando consente usuário ou administrador, Olá Olá a API da web hello e de aplicativo da web estão registrados no seu diretório.

#### <a name="token-expiration"></a>Expiração do token
Quando o aplicativo da web hello usa seu código de autorização tooget um token de acesso JWT, ele também recebe um token de atualização JWT. Quando o token de acesso de saudação expira, token de atualização de saudação pode ser usado toore-autenticar o usuário Olá sem exigir que eles toosign em novamente. Esse token de atualização é usado tooauthenticate Olá usuário, que resulta em um novo acesso de token e de atualização de token.

### <a name="daemon-or-server-application-tooweb-api"></a>TooWeb daemon ou aplicativo de servidor API
Esta seção descreve um aplicativo daemon ou de servidor que precisa de recursos de tooget de uma API da web. Há dois cenários secundários que se aplicam a seção toothis: um daemon que precisa toocall uma API da web, baseada no tipo de concessão de credenciais de cliente OAuth 2.0; e uma API da web, de um aplicativo de servidor (como uma API da web) que precisa toocall criadas na especificação de rascunho do nome do OAuth 2.0.

Para o cenário de saudação quando um aplicativo daemon precisa toocall uma API da web, é importante toounderstand algumas coisas. Primeiro, a interação do usuário não é possível com um aplicativo daemon, que exige Olá aplicativo toohave sua própria identidade. Um exemplo de um aplicativo daemon é um trabalho em lotes ou um serviço de sistema operacional em execução no plano de fundo de saudação. Esse tipo de aplicativo solicita um token de acesso usando a identidade do aplicativo e apresentando seu ID de aplicativo, credencial (senha ou certificado) e URI de ID de aplicativo tooAzure AD. Após a autenticação bem-sucedida, o daemon Olá recebe um token de acesso do AD do Azure, que é então usado toocall Olá API da web.

Para o cenário de saudação quando precisa de um aplicativo de servidor toocall uma API da web, é útil toouse um exemplo. Imagine que um usuário autenticado em um aplicativo nativo e esse aplicativo precisa toocall uma API da web. O Azure AD emite um JWT acesso toocall token Olá API da web. Se precisar de API da web hello toocall outra API da web downstream, pode usar a identidade do usuário do hello em nome de fluxo toodelegate hello e autenticar a API da web de segunda camada toohello.

#### <a name="diagram"></a>Diagrama
![Diagrama de tooWeb API daemon ou aplicativo de servidor](./media/active-directory-authentication-scenarios/daemon_server_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Descrição do fluxo de protocolo
##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>Identidade do aplicativo com concessão de credenciais do cliente OAuth 2.0
1. Primeiro, o aplicativo de servidor hello precisa tooauthenticate com o Azure AD como ele mesmo, sem qualquer interação humana, como uma caixa de diálogo de logon interativa. Faz uma tooAzure de solicitação do AD do ponto de extremidade token, fornecendo credenciais de hello, ID do aplicativo e URI de ID do aplicativo.
2. O AD do Azure autentica o aplicativo hello e retorna um token de acesso JWT que é usado toocall Olá web API.
3. Via HTTPS, o aplicativo da web hello usa Olá retornado Olá tooadd token de acesso JWT cadeia de caracteres JWT com uma designação "Portador" no cabeçalho de autorização de saudação da API da web do toohello Olá solicitação. Olá web API, em seguida, valida o token JWT hello e se a validação for bem-sucedida, retorna Olá desejado de recursos.

##### <a name="delegated-user-identity-with-oauth-20-on-behalf-of-draft-specification"></a>Identidade de usuário delegado com a especificação de rascunho do OAuth 2.0 On-Behalf-Of
fluxo de saudação discutido a seguir supõe que um usuário foi autenticado em outro aplicativo (como um aplicativo nativo) e sua identidade de usuário tiver sido usado tooacquire uma API de web de primeira camada de toohello de token de acesso.

1. aplicativo nativo Hello envia Olá acesso toohello token primeira camada API da web.
2. API da web de primeira camada Olá envia um tooAzure de solicitação do AD do ponto de extremidade token, fornecendo sua ID de aplicativo e credenciais, bem como o token de acesso do usuário hello. Além disso, a solicitação de saudação é enviada com um on_behalf_of parâmetro que indica Olá web API está solicitando novos tokens toocall uma API da web downstream em nome de usuário original hello.
3. AD do Azure verifica que Olá primeira camada API da web tem permissões tooaccess Olá web de segunda camada API e valida a solicitação hello, retornando que um token de acesso JWT e um JWT toohello token da web de primeira camada API de atualização.
4. Via HTTPS, Olá web de primeira camada, em seguida, chama uma API Olá API da web de segunda camada, acrescentando a cadeia de caracteres token no cabeçalho de autorização de saudação na solicitação Olá Olá. API da web de primeira camada Olá pode continuar a API da web do segundo nível toocall hello como token de acesso de saudação e tokens de atualização são válidos.

#### <a name="code-samples"></a>Exemplos de código
Consulte exemplos de código de saudação para cenários de tooWeb API Daemon ou aplicativo de servidor. E, volte a consultar frequentemente - adicionamos novos exemplos de todo o tempo de saudação. [Servidor ou aplicativo Daemon tooWeb API](active-directory-code-samples.md#server-or-daemon-application-to-web-api)

#### <a name="registering"></a>Registro
* Único locatário: Identidade de aplicativo hello e casos de identidade de usuário delegado, Olá daemon ou aplicativo de servidor deve ser registrado no hello mesmo diretório no AD do Azure. Olá web API pode ser configurado tooexpose um conjunto de permissões, que são o daemon Olá toolimit usado ou recursos de tooits de acesso do servidor. Se um tipo de identidade de usuário delegado estiver sendo usado, aplicativo de servidor de saudação precisa de permissões de saudação desejada de tooselect do menu Olá suspenso "Permissões tooOther aplicativos" hello Portal do Azure. Essa etapa não será necessária se o tipo de identidade de aplicativo hello está sendo usado.
* Multilocatário: Primeiro, Olá daemon ou aplicativo de servidor é configurado tooindicate Olá permissões requer toobe funcional. Esta lista de permissões necessárias é mostrada em uma caixa de diálogo quando um usuário ou administrador no diretório de destino Olá dá consentimento toohello aplicativo, o que torna disponíveis tootheir organização. Alguns aplicativos exigem permissões de nível de usuário, que qualquer usuário na organização Olá pode consentir. Outros aplicativos exigem permissões de administrador, que um usuário de organização de saudação não pode consentir. Somente um administrador do diretório pode dar consentimento tooapplications que requerem esse nível de permissões. Quando Olá usuário ou administrador der consentimento, as APIs da web hello são registradas em seu diretório.

#### <a name="token-expiration"></a>Expiração do token
Quando o aplicativo primeiro hello usa seu código de autorização tooget um token de acesso JWT, ele também recebe um token de atualização JWT. Quando o token de acesso de saudação expira, token de atualização de saudação pode ser usado toore-autenticar o usuário Olá sem solicitar credenciais. Esse token de atualização é usado tooauthenticate Olá usuário, que resulta em um novo acesso de token e de atualização de token.

## <a name="see-also"></a>Consulte também
[Guia do desenvolvedor do Active Directory do Azure](active-directory-developers-guide.md)

[Exemplos de código do Azure Active Directory](active-directory-code-samples.md)

[Informações importantes sobre a substituição da chave de assinatura no Azure AD](active-directory-signing-key-rollover.md)

[OAuth 2.0 no Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx)

