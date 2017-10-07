---
title: "Aplicativos de API de serviço - o que é alterado de aaaApp | Microsoft Docs"
description: "Saiba quais são as novidades dos Aplicativos de API no Serviço de Aplicativo do Azure."
services: app-service\api
documentationcenter: .net
author: mohitsriv
manager: erikre
editor: tdykstra
ms.assetid: a9b58066-e8fd-48b8-a651-4613b1736433
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: rachelap
ms.openlocfilehash: 79df54f1dae91d7c5d3b66d208d0d1c1d7d55ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps---whats-changed"></a>Aplicativos de API do Serviço de Aplicativo: o que mudou
No evento de conexão () do hello em novembro de 2015, inúmeras melhorias tooAzure do serviço de aplicativo foram [anunciada](https://azure.microsoft.com/blog/azure-app-service-updates-november-2015/). Esses aprimoramentos incluem alterações subjacentes tooAPI aplicativos toobetter alinhar móveis e aplicativos Web, reduzir a contagem de conceito e melhorar o desempenho de implantação e o tempo de execução. Iniciando novos aplicativos de API em 30 de novembro de 2015, você cria usando o portal de gerenciamento do Azure Olá ou ferramentas mais recentes Olá refletirão essas alterações. Este artigo descreve essas alterações, bem como tooredeploy existente aplicativos tootake aproveitar recursos de saudação.

## <a name="feature-changes"></a>Alterações de recurso
Olá os principais recursos de aplicativos de API – autenticação, CORS e a API de metadados – tenha movido diretamente para o serviço de aplicativo. Com essa alteração, recursos de saudação estão disponíveis na Web, móveis e aplicativos de API. Na verdade, todos os compartilhamento três Olá mesmo **Microsoft.Web/sites** o tipo de recurso no Gerenciador de recursos. gateway de aplicativos de API de saudação não é necessário ou oferecido com aplicativos de API. Isso também torna mais fácil toouse gerenciamento de API do Azure já que haverá apenas Olá única API gateway de gerenciamento.

![Visão geral de Aplicativos de API](./media/app-service-api-whats-changed/api-apps-overview.png)

Um princípio de design principais com hello atualizar aplicativos de API é tooenable toobring sua API como está, na linguagem de sua escolha.  Se sua API já estiver implantada como um aplicativo Web ou aplicativo móvel, você não tem tooredeploy seu aplicativo tootake aproveitar Olá novos recursos. Se você estiver atualmente na visualização dos Aplicativos de API, confira a orientação de migração detalhada abaixo.

### <a name="authentication"></a>Autenticação
Olá existente completas aplicativos de API, os serviços/aplicativos móveis e aplicativos Web autenticação recursos tiveram sido unificados e estão disponíveis em uma única folha de autenticação do serviço de aplicativo do Azure no portal de gerenciamento de saudação. Para uma introdução tooauthentication de serviços no serviço de aplicativo, consulte [autenticação do serviço de aplicativo de expansão / autorização](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/).

Para cenários de API, há diversos recursos novos relevantes:

* **Suporte para usar o Active Directory do Azure diretamente**, sem o código de cliente com o token do AAD Olá tooexchange para um token de sessão: O cliente pode apenas incluir tokens AAD Olá no cabeçalho de autorização hello, de acordo com o token de portador toohello especificação. Isso também significa que nenhum SDK App específico do serviço é necessário no lado do cliente ou servidor hello. 
* **Acesso de serviços ou "Interno"**: se você tiver um processo de daemon ou outro cliente que precisam de acesso tooAPIs sem uma interface, você pode solicitar um token usando uma entidade de serviço do AAD e passá-lo tooApp serviço para autenticação com o aplicativo.
* **Adiado autorização**: muitos aplicativos têm restrições de acesso diferentes para diferentes partes do aplicativo hello. Talvez você queira alguns toobe APIs publicamente disponível, enquanto outros exigem a entrada. o recurso de autenticação/autorização original Olá foi tudo ou nada, com todo o site Olá necessidade de logon. Essa opção ainda existe, mas você pode também permitir que o código do aplicativo toorender decisões de acesso depois que o serviço de aplicativo autenticou o usuário hello.

Para obter mais informações sobre os novos recursos de autenticação hello, consulte [autenticação e autorização para aplicativos de API no serviço de aplicativo do Azure](app-service-api-authentication.md). Para obter informações sobre como toomigrate aplicativos de API existentes de aplicativos de API anteriores Olá modelo consulte de um novo toohello [Migrando aplicativos de API existentes](#migrating-existing-api-apps) posteriormente neste artigo.

### <a name="cors"></a>CORS
Em vez de um delimitada por vírgulas **MS_CrossDomainOrigins** aplicativo definindo, agora há uma folha no portal de gerenciamento do Azure Olá para configurar o CORS. Como alternativa, é possível configurá-lo usando as ferramentas do Gerenciador de Recursos, como o Azure PowerShell, a CLI ou o [Gerenciador de Recursos](https://resources.azure.com/). Saudação de conjunto **cors** propriedade Olá **Microsoft.Web/sites/config** tipo de recurso para o  **&lt;nome do site&gt;/da web** recursos. Por exemplo:

    {
        "cors": {
            "allowedOrigins": [
                "https://localhost:44300"
            ]
        }
    } 

### <a name="api-metadata"></a>Metadados da API
folha de definição de API Olá agora está disponível na Web, móveis e aplicativos de API. No portal de gerenciamento hello, você pode especificar uma url relativa ou uma url absoluta apontando o ponto de extremidade tooan essa representação hosts Swagger 2.0 da sua API. Como alternativa, ela pode ser configurada usando as ferramentas do Gerenciador de Recursos. Saudação de conjunto **apiDefinition** propriedade Olá **Microsoft.Web/sites/config** tipo de recurso para o  **&lt;nome do site&gt;/da web** recursos. Por exemplo:

    {
        "apiDefinition":
        {
            "url": "https://myStorageAccount.blob.core.windows.net/swagger/apiDefinition.json"
        }
    }

Neste momento, ponto de extremidade de metadados Olá precisa toobe publicamente acessível sem autenticação para tooconsume de muitos clientes downstream (geração de cliente, por exemplo, o Visual Studio API REST e fluxo de "Adicionar API" PowerApps)-lo. Isso significa que se você estiver usando a autenticação do serviço de aplicativo e deseja tooexpose de definição de API de saudação de dentro de seu próprio aplicativo, você precisará de opção de autenticação adiada Olá toouse descrita anteriormente para que os metadados do Swagger tooyour Olá rota são público.

## <a name="management-portal"></a>Portal de Gerenciamento
Selecionando **Novo > Web + móvel > API App** Olá portal criará aplicativos de API que refletem os novos recursos de saudação descritos no artigo hello. **Procurar > Aplicativos de API** mostrará apenas esses novos aplicativos de API. Quando você navega em um aplicativo de API, compartilhamentos de folha Olá Olá mesmo layout e os recursos dos aplicativos Web e móveis. Olá únicas diferenças são o conteúdo do guia de início rápido e a ordenação de configurações.

Aplicativos de API existentes (ou aplicativos de API do Marketplace criados a partir de aplicativos lógicos) com hello recursos de visualização anteriores ainda estarão visíveis no designer de aplicativos lógicos hello e ao procurar todos os recursos em um grupo de recursos.

## <a name="visual-studio"></a>Visual Studio
A maioria dos aplicativos Web ferramentas funcionará com novos aplicativos de API, já que eles compartilham Olá subjacente mesmo **Microsoft.Web/sites** tipo de recurso. ferramentas do Hello Azure Visual Studio, no entanto, devem ser atualizado tooversion 2.8.1 ou posterior, porque ela expõe um número de tooAPIs de recursos específicos. Baixar Olá SDK da saudação [página de downloads do Azure](https://azure.microsoft.com/downloads/).

Com racionalização de saudação do hello tipos de serviço de aplicativo publicar também é unificada em **publicar > serviço de aplicativo do Microsoft Azure**:

![Publicação de Aplicativos de API](./media/app-service-api-whats-changed/api-apps-publish.png)

toolearn mais sobre o SDK 2.8.1, anúncio Olá leitura [postagem de blog](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).

Como alternativa, você pode importar manualmente Olá publicar perfil do tooenable portal de gerenciamento Olá publicar. No entanto, o Gerenciador de Nuvem, a geração de código e aseleção/criação de aplicativos de API exigirão o SDK 2.8.1 ou superior.

## <a name="migrating-existing-api-apps"></a>Migração de aplicativos de API existentes
Se a sua API personalizada é a versão de visualização anterior toohello implantado de aplicativos de API, solicitamos que você migre toohello novo modelo para aplicativos de API por dia 31 de dezembro de 2015. Como tanto o modelo de saudação antiga e nova é baseado em APIs da Web hospedado no serviço de aplicativo, a maioria de saudação do código existente pode ser reutilizada.

### <a name="hosting-and-redeployment"></a>Hospedagem e reimplantação
etapas de saudação para reimplantar são Olá igual ao implantar qualquer tooApp de API da Web serviço existente. Etapas:

1. Criar um aplicativo de API vazio. Isso pode ser feito no portal de saudação com New > App API, no Visual Studio de publicação ou de ferramentas do Gerenciador de recursos. Se estiver usando modelos ou ferramentas do Gerenciador de recursos, defina Olá **tipo** valor muito**api** em hello **Microsoft.Web/sites** início rápido do hello toohave de tipo de recurso e as configurações no portal de gerenciamento Olá orientado para cenários de API.
2. Conecte-se e implante seu projeto toohello vazio aplicativo de API usando qualquer um dos mecanismos de implantação Olá suportados pelo serviço de aplicativo. Leitura [documentação de implantação do serviço de aplicativo do Azure](../app-service-web/web-sites-deploy.md) toolearn mais. 

### <a name="authentication"></a>Autenticação
Olá, suporte de serviços de autenticação do serviço de aplicativo hello mesmos recursos que estavam disponíveis com o modelo de aplicativos de API anterior hello. Se você estiver usando tokens de sessão e exige SDKs, use Olá SDKs de cliente e o servidor a seguir:

* Cliente: [SDK de cliente móvel do Azure](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
* Servidor: [Extensão de autenticação .NET de aplicativo móvel do Microsoft Azure](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/) 

Se estivesse usando Olá alpha do serviço de aplicativo SDKs em vez disso, eles agora são preteridos:

* Cliente: [SDK do Serviço de Aplicativo do Microsoft Azure](http://www.nuget.org/packages/Microsoft.Azure.AppService)
* Servidor: [Microsoft.Azure.AppService.ApiApps.Service](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service)

Em particular com o Active Directory do Azure, no entanto, nenhum serviço App específico é necessário se você estiver usando o token do AAD Olá diretamente.

### <a name="internal-access"></a>Acesso interno
modelo de aplicativos de API anterior Olá incluído um nível de acesso interno internos. Isso exigia o uso de saudação SDK para assinar solicitações. Conforme descrito anteriormente, com o novo modelo de aplicativos de API hello, entidades de serviço AAD podem ser usadas como uma alternativa para autenticação de serviços sem a necessidade de um App-específico do serviço SDK. Saiba mais em [Autenticação de entidade de serviço para Aplicativos de API no Serviço de Aplicativo do Azure](app-service-api-dotnet-service-principal-auth.md).

### <a name="discovery"></a>Descoberta
Olá anterior aplicativos de API de modelo tinha APIs para a descoberta de outros aplicativos de API em tempo de execução no mesmo grupo de recursos por trás de hello Olá mesmo gateway. Isso é especialmente útil em arquiteturas que implementam padrões de microsserviço. Embora isso não tenha suporte direto, há várias opções disponíveis:

1. Saudação de uso da API do Gerenciador de recursos do Azure para descoberta.
2. Coloque o Gerenciamento de API do Azure a frente de suas APIs hospedadas no Serviço de Aplicativo. O Gerenciamento de API do Azure serve como uma fachada e pode fornecer uma URL externa estável, mesmo se a topologia interna mudar.
3. Criar seu próprio aplicativo de API de descoberta e têm outros aplicativos de API de registro com o aplicativo de descoberta de saudação na inicialização.
4. No momento da implantação, popule configurações do aplicativo hello de todos os Olá API aplicativos (e clientes) com pontos de extremidade Olá Olá outros aplicativos de API. Isso é viável em implantações de modelo e como aplicativos de API agora oferecem a você controle da url de saudação.

## <a name="using-api-apps-with-logic-apps"></a>Usando aplicativos de API com aplicativos lógicos
novo modelo de aplicativos de API Olá funciona bem com [aplicativos lógicos versão 2015-08-01 do esquema](../logic-apps/logic-apps-schema-2015-08-01.md).

## <a name="next-steps"></a>Próximas etapas
toolearn mais, leia os artigos de saudação em Olá [seção da documentação da API aplicativos](https://azure.microsoft.com/documentation/services/app-service/api/). Eles foram atualizados tooreflect Olá novo modelo para aplicativos de API. Além disso, chegar nos fóruns Olá para obter detalhes adicionais ou orientação na migração:

* [Fórum do MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)
* [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-api-apps)

