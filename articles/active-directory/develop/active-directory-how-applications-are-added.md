---
title: "aplicativos de aaaHow são adicionados tooAzure do Active Directory."
description: "Este artigo descreve como os aplicativos são adicionados tooan instância do Active Directory do Azure."
services: active-directory
documentationcenter: 
author: shoatman
manager: kbrint
editor: 
ms.assetid: 3321d130-f2a8-4e38-b35e-0959693f3576
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/09/2016
ms.author: shoatman
ms.custom: aaddev
ms.openlocfilehash: 3ca710c58a403b52e8b728202ad9010f4873bcea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-and-why-applications-are-added-tooazure-ad"></a>Como e por que os aplicativos são adicionados tooAzure AD
Uma saudação inicialmente as coisas ao exibir uma lista de aplicativos em sua instância do Active Directory do Azure para entender onde veio aplicativos hello e por que elas existem.  Este artigo fornecem uma visão geral de alto nível de como os aplicativos são representados no diretório hello e fornecem contexto que irá ajudá-lo na compreensão de como um aplicativo fornecido toobe em seu diretório.

## <a name="what-services-does-azure-ad-provide-tooapplications"></a>Os serviços do Azure AD fornecem tooapplications?
Os aplicativos são adicionados tooAzure AD tooleverage um ou mais dos serviços de saudação fornece.  Esses serviços incluem:

* Autenticação e autorização de aplicativo
* Autenticação e autorização de usuário
* SSO (logon único) usando federação ou sua senha
* Provisionamento do usuário e sincronização
* Controle de acesso baseado em função; Use Olá diretório toodefine aplicativo tooperform funções com base em verificações de autorização em um aplicativo.
* Serviços de autorização do oAuth (usados pelo Office 365 e outros tooAPIs recursos acesso Microsoft aplicativos tooauthorize).
* Publicação de aplicativos & proxy; Publicar um aplicativo a partir de uma rede privada toohello internet

## <a name="how-are-applications-represented-in-hello-directory"></a>Como os aplicativos são representados no diretório Olá?
Aplicativos são representados no hello Azure AD usando 2 objetos: um objeto de aplicativo e um objeto de entidade de serviço.  Há um objeto de aplicativo, registrado em "casa" / diretório "proprietário" ou "publicação" e um ou mais objetos principais que representa o aplicativo hello em todas as pastas em que ele atue de serviço.  

Olá objeto application descreve Olá aplicativo tooAzure AD (serviço de multilocatário Olá) e pode incluir qualquer um dos seguintes Olá: (*Observação*: isso não é uma lista exaustiva.)

* Nome, logotipo e publicador
* Segredos (chaves simétricas e/ou assimétricas usaram tooauthenticate Olá app)
* Dependências de API (oAuth)
* APIs/recursos/escopos publicados (oAuth)
* Funções de aplicativo (RBAC)
* Metadados SSO e configuração (SSO)
* Configuração e metadados de provisionamento de usuário
* Configuração e metadados de proxy

entidade de serviço Olá é um registro de aplicativo hello em todas as pastas, onde o aplicativo hello atua como seu diretório base.  entidade de serviço Hello:

* Refere-se novamente tooan o objeto de aplicativo por meio da propriedade de id de aplicativo hello
* Registra atribuições de função de aplicativo de usuários e grupos locais
* Permissões locais de administrador e usuário registros concedidas toohello aplicativo
  * Por exemplo: permissão para Olá aplicativo tooaccess um email de usuários específicos
* Registra políticas locais, incluindo a política de acesso condicional
* Registra configurações alternativas locais para um aplicativo
  * Declara regras de transformação
  * Mapeamentos de atributos (provisionamento do usuário)
  * Funções de aplicativo específico de locatário (se o aplicativo hello dá suporte a funções personalizadas)
  * Nome/logotipo

### <a name="a-diagram-of-application-objects-and-service-principals-across-directories"></a>Um diagrama de objetos de aplicativo e entidades de serviço entre diretórios
![Um diagrama que ilustra como objetos de aplicativo e entidades de serviço coexistem com instâncias do AD do Azure.][apps_service_principals_directory]

Como você pode ver no diagrama de saudação acima.  A Microsoft mantém dois diretórios internamente (em Olá esquerda), ele usa toopublish aplicativos.

* Um para Microsoft Apps (diretório de serviços da Microsoft)
* Um para aplicativos de terceiros pré-integrados (diretório de galeria de aplicativos)

Editores/fornecedores de aplicativos que integram com o AD do Azure são necessário toohave um diretório de publicação.  (algum diretório SAAS).

Os aplicativos que você adiciona por conta própria incluem:

* Aplicativos desenvolvidos por você (integrados ao AAD)
* Aplicativos conectados por você para logon único
* Aplicativos que você publicou usando Olá proxy de aplicativo do AD do Azure.

### <a name="a-couple-of-notes-and-exceptions"></a>Algumas observações e exceções
* Nem todas as entidades de serviço do ponto tooapplication back objetos.  Hein? Quando o AD do Azure foi criado originalmente serviços Olá fornecido tooapplications foram muito mais limitado e entidade de serviço Olá foi suficiente para estabelecer uma identidade de aplicativo.  entidade de serviço original Olá era mais próximo na forma toohello conta de serviço do Windows Server Active Directory.  Por esse motivo, é possível toocreate entidades de serviço usando Olá PowerShell do Azure AD sem primeiro criar um objeto de aplicativo.  Olá Graph API requer um objeto de aplicativo antes de criar um serviço principal.
* Não todas as informações de saudação descritas acima no momento é exposto por meio de programação.  a seguir Olá só está disponível em Olá da interface do usuário:
  * Declara regras de transformação
  * Mapeamentos de atributos (provisionamento do usuário)
* Para obter mais informações detalhadas sobre a entidade de serviço hello e objetos de aplicativo, consulte a documentação de referência toohello API REST do Azure AD Graph.  *Dica*: Olá documentação da API do Azure AD Graph é a referência do hello mais próxima coisa tooa esquema do AD do Azure que está disponível no momento.  
  * [Aplicativo](https://msdn.microsoft.com/library/azure/dn151677.aspx)
  * [Entidade de serviço](https://msdn.microsoft.com/library/azure/dn194452.aspx)

## <a name="how-are-apps-added-toomy-azure-ad-instance"></a>Como os aplicativos são adicionados toomy instância do AD do Azure?
Há muitas maneiras que um aplicativo pode ser adicionado tooAzure AD:

* Adicionar um aplicativo de saudação [Galeria de aplicativos do Azure Active Directory](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)
* Inscreva-se em um Aplicativo de Terceiros integrado ao Azure Active Directory (por exemplo: [Smartsheet](https://app.smartsheet.com/b/home) ou [DocuSign](https://www.docusign.net/member/MemberLogin.aspx))
  * Durante a inscrição para cima/usuários são frequentes toogive permissão toohello aplicativo tooaccess seu perfil e outras permissões.  Olá primeira pessoa toogive consentimento faz com que uma entidade de serviço que representa Olá aplicativo toobe toohello adicionado diretório.
* Inscrever-se/entrar nos serviços online da Microsoft, como o [Office 365](http://products.office.com/)
  * Quando você assina tooOffice 365 ou iniciar uma avaliação ou mais entidades de serviço são criadas no diretório de saudação representando Olá vários serviços que são usado toodeliver toda a funcionalidade de saudação associadas com o Office 365.
  * Alguns serviços do Office 365 como o SharePoint criar entidades de serviço em uma base contínua tooallow uma comunicação segura entre componentes, incluindo fluxos de trabalho.
* Adicionar um aplicativo que você está desenvolvendo em hello, consulte o Portal de gerenciamento: https://msdn.microsoft.com/library/azure/dn132599.aspx
* Adicione um aplicativo que você está desenvolvendo com o Visual Studio, consulte:
  * [Métodos de autenticação do ASP.Net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)
  * [Serviços conectados](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)
* Adicionar uma saudação do aplicativo toouse toouse [Proxy de aplicativo do Azure AD](https://msdn.microsoft.com/library/azure/dn768219.aspx)
* Conectar a um aplicativo para logon único usando SAML ou SSO de senha
* Muitas outras, incluindo várias experiências de desenvolvedor no Azure e/ou experiências no Gerenciador de APIs entre centros de desenvolvedores

## <a name="who-has-permission-tooadd-applications-toomy-azure-ad-instance"></a>Quem tem a instância do AD do Azure do permissão tooadd aplicativos toomy?
Somente os administradores globais podem:

* Adicionar aplicativos da Galeria de aplicativos de saudação do AD do Azure (pré-integrados 3ª parte aplicativos)
* Publicar um aplicativo usando Olá Proxy de aplicativo do Azure AD

Todos os usuários em seu diretório têm aplicativos de tooadd de direitos que estão desenvolvendo e critério sobre quais aplicativos eles compartilhamento/dar acesso tootheir organizacional dados.  *Lembre-se de entrada do usuário up/tooan aplicativo e conceder permissões podem resultar em um serviço principal que está sendo criado.*

Este pode inicialmente som relacionadas, mas Olá mantenha em mente a seguir:

* Aplicativos foram tooleverage capaz de Windows Server Active Directory para autenticação por muitos anos, sem a necessidade de saudação aplicativo toobe registrado/registrado no diretório de saudação do usuário.  Agora a organização hello serão melhoraram visibilidade tooexactly quantos aplicativos estão usando diretório hello e quais for.
* Não é necessário que o processo de publicação/registro do aplicativo seja realizado pelo administrador.  Com os serviços de Federação do Active Directory é provável que um administrador teve tooadd um aplicativo como uma terceira parte confiável em nome de desenvolvedores.  Agora, os desenvolvedores podem usar o autoatendimento.
* Os usuários de assinatura/backup tooapps usando suas contas da organização para fins de negócios é bom.  Se subsequentemente saírem da organização Olá perderão o acesso tootheir conta no aplicativo hello que eles estavam usando.
* Ter um registro de quais dados foram compartilhados com qual o aplicativo é algo bom.  Os dados estão mais transportáveis do que nunca e é útil ter um registro claro de quem compartilhou quais dados com quais aplicativos.
* Aplicativos que usam o AD do Azure para o oAuth decidir exatamente quais permissões que os usuários são capazes de toogrant tooapplications e as permissões que exigem um tooagree admin para.  Ele deve ficar sem dizendo que somente os administradores podem consentimento toolarger escopos e as permissões mais significativas.
* Os usuários adicionando e permitindo que aplicativos tooaccess que seus dados são os eventos auditados, portanto você pode exibir relatórios de auditoria de saudação em hello Azure Management portal toodetermine como um aplicativo foi adicionado toohello directory.

**Observação:** *Microsoft em si tenha estado operacional usando a configuração de padrão de saudação para muitos meses agora.*

Com tudo isso diz é tooprevent possíveis usuários em seu diretório de adição de aplicativos e de exercer critério sobre quais informações os compartilham com aplicativos, modificando a configuração de diretório no portal de gerenciamento do Azure hello.  Olá configuração a seguir pode ser acessada no portal de gerenciamento do Azure Olá na guia "Configurar" do diretório.

![Uma captura de tela de saudação da interface do usuário para definir as configurações do aplicativo integrado][app_settings]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre como tooadd tooAzure aplicativos AD e como os serviços de tooconfigure para aplicativos.

* Desenvolvedores: [Saiba como toointegrate um aplicativo com o AAD](https://msdn.microsoft.com/library/azure/dn151122.aspx)
* Desenvolvedores: [Examinar o código de exemplo para aplicativos integrados ao Azure Active Directory no GitHub](https://github.com/AzureADSamples)
* Os desenvolvedores e profissionais de TI: [revisar a documentação da API de REST Olá Olá API do Graph do Azure Active Directory](https://msdn.microsoft.com/library/azure/hh974478.aspx)
* Os profissionais de TI: [Saiba como toouse Active Directory do Azure previamente integrado aplicativos Olá Galeria de aplicativos](https://msdn.microsoft.com/library/azure/dn308590.aspx)
* Profissionais de TI: [Localize tutoriais para a configuração de determinados aplicativos pré-integrados](https://msdn.microsoft.com/library/azure/dn893637.aspx)
* Os profissionais de TI: [Saiba como toopublish usando um aplicativo hello Proxy de aplicativo do Azure Active Directory](https://msdn.microsoft.com/library/azure/dn768219.aspx)

## <a name="see-also"></a>Consulte também
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](../active-directory-apps-index.md)

<!--Image references-->
[apps_service_principals_directory]:../media/active-directory-how-applications-are-added/HowAppsAreAddedToAAD.jpg
[app_settings]:../media/active-directory-how-applications-are-added/IntegratedAppSettings.jpg
