---
title: aaaExporting um tooPowerApps API hospedado do Azure e Microsoft Flow | Microsoft Docs
description: "Visão geral de como tooexpose uma API hospedados no serviço de aplicativo tooPowerApps e Microsoft Flow"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/20/2017
ms.author: mahender
ms.openlocfilehash: 285b6efa3af5b0feac1ee2f617c0dc56dc3fd198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-an-azure-hosted-api-toopowerapps-and-microsoft-flow"></a>Exportando um tooPowerApps API hospedado do Azure e Microsoft Flow

## <a name="creating-custom-connectors-for-powerapps-and-microsoft-flow"></a>Criando conectores personalizados para o PowerApps e o Microsoft Flow

[PowerApps](https://powerapps.com) é um serviço para a criação e uso de aplicativos de negócios personalizada que se conectam a dados tooyour e funcionam entre plataformas. [Microsoft Flow](https://flow.microsoft.com) torna fácil tooautomate fluxos de trabalho e processos de negócios entre seus aplicativos favoritos e serviços. PowerApps e Microsoft Flow vem com uma variedade de fontes de toodata de conectores internos, como o Office 365, Dynamics 365, a equipe de vendas e muito mais. No entanto, os usuários também precisam toobe tooleverage capaz de fontes de dados e APIs que estão sendo criados por sua organização.

Da mesma forma, os desenvolvedores que desejam tooexpose suas APIs mais amplamente em Olá organização pode achar toomake seus tooPowerApps disponíveis APIs e Microsoft Flow usuários. Este tópico mostra como tooexpose uma API criada com tooPowerApps do serviço de aplicativo do Azure ou funções do Azure e Microsoft Flow. [Serviço de aplicativo do Azure](https://azure.microsoft.com/services/app-service/) é uma oferta de plataforma como um serviço que permite que desenvolvedores tooquickly e facilmente da web de nível empresarial de compilação, móveis e aplicativos de API. [As funções do Azure](https://azure.microsoft.com/services/functions/) é uma solução de computação sem servidor baseado em evento que permite que você tooquickly autor do código que possa reagir tooother partes do seu sistema e a escala com base na demanda.

toolearn mais sobre esses serviços, consulte:
- [Aprendizado Guiado do PowerApps](https://powerapps.microsoft.com/guided-learning/learning-introducing-powerapps/) 
- [Aprendizado Guiado do Microsoft Flow](https://flow.microsoft.com/guided-learning/learning-introducing-flow/)
- [O que é o Serviço de Aplicativo](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- [O que é o Azure Functions?](https://docs.microsoft.com/azure/azure-functions/functions-overview)

## <a name="sharing-an-api-definition"></a>Compartilhando uma definição de API

APIs geralmente são descritas usando um [OpenAPI documento](https://www.openapis.org/) (às vezes chamado de tooas um documento "Swagger"). Contém todas as informações de saudação sobre as operações que estão disponíveis e como os dados de saudação devem ser estruturados. O PowerApps e o Microsoft Flow podem criar conectores personalizados para qualquer documento API aberta 2.0. Depois de criar um conector personalizado, ele pode ser usado em exatamente Olá mesma maneira que um dos Olá conectores internos e rapidamente pode ser integrado a um aplicativo.

O Serviço de Aplicativo do Azure e o Azure Functions têm [suporte integrado](https://docs.microsoft.com/azure/app-service-api/app-service-api-metadata) para criação, hospedagem e gerenciamento um documento de API aberta. Em ordem toocreate um conector personalizado para web, móvel, API ou função de aplicativo, PowerApps e fluxo necessário toobe recebe uma cópia da definição de saudação.

> [!NOTE]
> Como uma cópia da definição de API do hello está sendo usada, PowerApps e Microsoft Flow não imediatamente saberá sobre atualizações ou aplicativo de toohello alterações recentes. Se uma nova versão da API de saudação for disponibilizada, essas etapas devem ser repetidas para a nova versão de hello. 

tooprovide PowerApps e Microsoft Flow com hello hospedado de definição de API para seu aplicativo, siga estas etapas:

1. Olá abrir [Portal do Azure](https://portal.azure.com) e navegue tooyour aplicativo de serviço de aplicativo ou funções do Azure.

    Se usar o serviço de aplicativo do Azure, selecione **de definição de API** na lista de configurações de saudação. 
    
    Se utilizar Azure Function, selecione seu aplicativo de funções, escolha **Recursos de plataforma** e, em seguida, **Definição de API**. Você também pode escolher Olá tooopen **de definição de API (visualização)** guia em vez disso.

2. Se uma definição de API foi fornecida, você verá um **exportar tooPowerApps + Microsoft Flow** botão. Clique neste processo de exportação do botão toobegin hello.

3. Selecione Olá **modo de exportação**. Isso determina etapas Olá precisará toofollow toocreate um conector. O Serviço de Aplicativo oferece duas opções para fornecer PowerApps e Microsoft Flow com sua definição de API:

    **Express** permite que você crie conector personalizado Olá de dentro de Olá portal do Azure. Isso requer que Olá atual usuário conectado tem conectores de toocreate de permissão no ambiente de destino hello. Isso é hello abordagem recomendada se esse requisito pode ser atendido. Se usar esse modo, siga Olá [Express exportação](#express) instruções a seguir.

    **Manual** permite que você exporte uma cópia da definição de API de saudação que pode ser importada usando Olá PowerApps ou portais Microsoft Flow. Isso é hello abordagem recomendada se hello usuário do Azure e Olá com conectores de toocreate de permissão são pessoas diferentes ou se o conector de saudação precisa toobe criado em outro locatário. Se usar esse modo, siga Olá [importação e exportação Manual](#manual) instruções a seguir.

<a name="express"></a>
## <a name="express-export"></a>Exportação de expresso

Nesta seção, você criará um novo conector personalizado de dentro de saudação portal do Azure. Você deve estar conectado em Olá locatário toowhich desejar tooexport, e você deve ter permissão toocreate um conector personalizado no ambiente de destino de saudação.

1. Selecione Olá ambiente em que você gostaria que o conector de saudação toocreate. Em seguida, forneça um nome para o conector personalizado.

2. Se a sua definição de API incluir quaisquer definições de segurança, elas serão chamadas na etapa n° 2. Se necessário, fornece segurança Olá detalhes de configuração necessário toogrant usuários acessar tooyour API. Para obter mais informações, consulte [Autenticação](#auth) abaixo. 

3. Clique em **Okey** toocreate seu conector personalizado.


<a name="manual"></a>
## <a name="manual-export-and-import"></a>Exportação e importação manual

Em ordem toocreate um conector personalizado para web, móvel, API ou função de aplicativo, serão necessário duas etapas:

1. [Recuperando a definição de API de saudação do serviço de aplicativo ou de funções do Azure](#export)
2. [Importar definição de API Olá para PowerApps e Microsoft Flow](#import)

É possível que essas duas etapas precisará toobe realizada por indivíduos separados dentro de uma organização, como um usuário não pode ter permissão tooperform ambas as ações. Nesse caso, um desenvolvedor que tenha acesso de Colaborador toohello aplicativo de serviço de aplicativo ou funções do Azure precisará de definição de saudação API tooobtain (um arquivo JSON único) ou tooit um link. Em seguida, deverá tooprovide proprietário definição tooa PowerApps ou Microsoft Flow. Esse proprietário pode usar o conector personalizado do Olá Olá metadados toocreate.

<a name="export"></a>
### <a name="retrieving-hello-api-definition-from-app-service-or-azure-functions"></a>Recuperando a definição de API de saudação do serviço de aplicativo ou de funções do Azure

Nesta seção, você exportará a definição de API Olá para a API do serviço de aplicativo, toobe usado posteriormente no portal de PowerApps ou Microsoft Flow hello.

1. Você pode escolher tooeither **baixar definição Olá API** ou **obter um link**. O que você escolher, o resultado hello será fornecido na próxima seção, Olá. Selecione uma destas opções e siga as instruções de saudação.
 
2. Se a sua definição de API incluir quaisquer definições de segurança, elas serão chamadas na etapa n° 2. Durante a importação, o PowerApps e o Microsoft Flow irão detectá-las e solicitar informações de segurança. Colete Olá credenciais relacionadas tooeach definição para uso na próxima seção, Olá. Para obter mais informações, consulte [Autenticação](#auth) abaixo. 

<a name="import"></a>
### <a name="importing-hello-api-definition-into-powerapps-and-microsoft-flow"></a>Importar definição de API Olá para PowerApps e Microsoft Flow

Nesta seção, você irá criar um conector personalizado no PowerApps e Microsoft Flow usando definição de saudação API obtida anteriormente. Conectores personalizados são compartilhados entre Olá dois serviços, para que você só precisa de definição de saudação tooimport uma vez. Para obter mais informações sobre conectores personalizados, consulte [registrar e usar conectores personalizados em PowerApps] e [registrar e usar conectores personalizados no Microsoft Flow].

1. Olá abrir [portal da web de Powerapps](https://web.powerapps.com) ou hello [portal da web do Microsoft Flow](https://flow.microsoft.com/)e entre. 

2. Clique em Olá **configurações** botão (ícone de engrenagem Olá) no canto superior direito de saudação da página hello e selecione **conectores personalizado**. 

3. Clique em **Criar conector personalizado**.

4. Em Olá **geral** guia, forneça um nome para a sua API e, em seguida, carregar a definição de OpenAPI hello ou cole a URL de metadados de saudação. Clique em **Continuar**.

4. Em Olá **segurança** guia, se você for solicitado tooprovide detalhes de autenticação, digite os valores hello obtidos na seção anterior hello. Se não, continuar toohello próxima etapa.

5. Em Olá **definições** guia, todas as operações de saudação definidas no seu arquivo OpenAPI são preenchidas automaticamente. Se todas as suas operações necessárias são definidas, você pode ir toohello próxima etapa. Caso contrário, você pode adicionar e modificar as operações aqui.

6. Clique em **Criar conector**. Se você desejar tootest chamadas de API, vá toohello próxima etapa.

7. Em Olá **teste** guia, criar uma conexão, selecione uma operação tootest e insira os dados necessários pela operação de saudação.

8. Clique em **Testar operação**.


<a name="auth"></a>
## <a name="authentication"></a>Autenticação

PowerApps e Microsoft Flow nativamente oferecem suporte a uma coleção de provedores de identidade que pode ser usado toolog os usuários do seu conector personalizado. Se sua API exige autenticação, certifique-se de que ela seja capturada como uma _definição de segurança_ no documento OpenAPI. Durante a exportação, você precisará tooprovide valores de configuração que permitem a uma ação de logon do Microsoft Flow tooperform PowerApps.

Esta seção aborda os tipos de autenticação de saudação que são suportados pelo fluxo express Olá: chave de API, Active Directory do Azure e genérico OAuth 2.0. Para obter uma lista completa de provedores e credenciais de saudação requer que cada um, consulte [registrar e usar conectores personalizados em PowerApps] e [registrar e usar conectores personalizados no Microsoft Flow].

### <a name="api-key"></a>Chave de API
Quando o esquema de segurança é usado, os usuários de saudação do seu conector será chave de saudação tooprovide solicitados quando eles criarem uma conexão. Você pode fornecer um toohelp do nome da chave de API sobre qual chave é necessária. Para funções do Azure, isso geralmente será uma das chaves de host hello, que abrangem várias funções dentro do aplicativo de função hello.

### <a name="azure-active-directory"></a>Azure Active Directory
Ao configurar um conector personalizado que requer o logon do AAD, dois registros do aplicativo AAD são necessários: uma API de back-end Olá toomodel e um conector de saudação toomodel no fluxo e PowerApps.

Sua API deve ser configurado toowork com o primeiro registro de saudação e isso será já ser resolvido se você usou Olá [aplicativo de serviço de autenticação/autorização](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication) recurso.

Você terá toomanually criar registro de saudação segundo conector Olá Olá etapas abordadas em [adicionar um aplicativo AAD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application). Olá registro precisa toohave recebido acesso tooyour API e uma URL de resposta de `https://msmanaged-na.consent.azure-apim.net/redirect`. Consulte [Este exemplo](
https://powerapps.microsoft.com/tutorials/customapi-azure-resource-manager-tutorial/) para obter mais detalhes, substituindo sua API para hello Azure Resource Manager.

Olá valores de configuração a seguir é necessária:
- **ID do cliente** -Olá ID do cliente do seu conector de registro do AAD
- **Segredo do cliente** -segredo do cliente de saudação do seu conector de registro do AAD
- **URL de logon** - Olá URL base para AAD. No Azure público, isso geralmente será `https://login.windows.net`.
- **ID do locatário** -Olá ID da saudação toobe de locatário usado para logon de saudação. Isso deve ser "comum" ou Olá ID de locatário Olá no qual Olá conector está sendo criado.
- **URL de recurso** -Olá URL de recurso de seu registro AAD de back-end de API

> [!IMPORTANT]
> Se outra pessoa estiver importando definição Olá API em PowerApps e Microsoft Flow como parte do fluxo de saudação manual, você precisará tooprovide-los com o segredo de cliente e a ID do cliente Olá **de registro do conector Olá**, bem como como a URL de recurso de saudação da sua API. Certifique-se de que esses segredos sejam gerenciados com segurança. **Não compartilhe credenciais de segurança de saudação de saudação própria API.**

### <a name="generic-oauth-20"></a>OAuth 2.0 genérico
suporte de OAuth 2.0 genérico Olá permite toointegrate com qualquer provedor OAuth 2.0. Isso permite que você toobring em qualquer provedor personalizado que não tem suporte nativo.

Olá valores de configuração a seguir é necessária:
- **ID do cliente** -Olá ID do cliente OAuth 2.0
- **Segredo do cliente** -segredo do cliente Olá OAuth 2.0
- **URL de autorização** -Olá URL de autorização do OAuth 2.0
- **URL de token** -Olá URL de token OAuth 2.0
- **URL de atualização** -Olá URL de atualização OAuth 2.0



[registrar e usar conectores personalizados em PowerApps]: https://powerapps.microsoft.com/tutorials/register-custom-api/
[registrar e usar conectores personalizados no Microsoft Flow]: https://flow.microsoft.com/documentation/register-custom-api/
