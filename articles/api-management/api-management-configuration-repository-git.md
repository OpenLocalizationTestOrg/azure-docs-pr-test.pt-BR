---
title: "aaaConfigure seu serviço de gerenciamento de API usando o Git - Azure | Microsoft Docs"
description: "Saiba como toosave e configurar a configuração do serviço de gerenciamento de API usando o Git."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a>Como toosave e configurar a configuração do serviço de gerenciamento de API usando o Git
> 
> 

Cada instância de serviço de gerenciamento de API mantém um banco de dados de configuração que contém informações sobre a configuração de saudação e metadados para a instância do serviço hello. Alterações a instância do serviço toohello alterar uma configuração no portal do publicador hello, usando um cmdlet do PowerShell ou fazer uma chamada à API REST. Além de métodos de toothese, você também pode gerenciar a configuração de instância do serviço usando o Git, permitindo cenários de gerenciamento de serviço, como:

* Controle de versão da configuração - baixe e armazene versões diferentes da configuração do seu serviço
* Em massa as alterações de configuração - faça alterações toomultiple partes da sua configuração de serviço no seu repositório local e integrar o servidor de back toohello de alterações de saudação com uma única operação
* Cadeia de ferramentas do Git e fluxo de trabalho - familiar usar ferramentas de Git hello e fluxos de trabalho que você já estiver familiarizado com

Olá diagrama a seguir mostra uma visão geral de tooconfigure de maneiras diferentes de saudação sua instância de serviço de gerenciamento de API.

![Configuração do Git][api-management-git-configure]

Quando você fizer alterações tooyour serviço usando o portal do publicador hello, cmdlets do PowerShell ou Olá API REST, você está gerenciando o banco de dados de configuração de serviço usando Olá `https://{name}.management.azure-api.net` ponto de extremidade, conforme mostrado no lado direito de saudação do diagrama de saudação. lado esquerdo de saudação do diagrama Olá ilustra como você pode gerenciar a configuração de serviço usando o Git e repositório Git para seu serviço localizado em `https://{name}.scm.azure-api.net`.

Olá, as etapas a seguir fornece uma visão geral do gerenciamento de sua instância de serviço de gerenciamento de API usando o Git.

1. Acessar a configuração GIT em seu serviço
2. Salvar o repositório do Git de tooyour do banco de dados de configuração de serviço
3. Clonar a máquina local de tooyour Olá de repositório Git
4. Pull hello mais recente máquina local tooyour e o repositório de backup tooyour alterações confirmação e enviar por push
5. Implantar alterações de saudação do seu repositório em seu banco de dados de configuração de serviço

Este artigo descreve como tooenable usar Git toomanage sua configuração de serviço e fornece uma referência para os arquivos de saudação e pastas no repositório do Git hello.

## <a name="access-git-configuration-in-your-service"></a>Acessar a configuração GIT em seu serviço
Você pode exibir rapidamente status de saudação da configuração do Git exibindo o ícone de Git Olá no canto superior direito de saudação do portal do publicador hello. Neste exemplo, a mensagem de saudação do status indica que há um repositório de toohello alterações não salvas. Isso ocorre porque o banco de dados do gerenciamento de API serviço configuração Olá ainda não foi salvo toohello repositório.

![Status do Git][api-management-git-icon-enable]

tooview e configurar as definições de configuração de Git, você pode clique ícone de Git hello, ou Olá **segurança** menu e navegue toohello **repositório de configuração** guia.

![Habilitar o GIT][api-management-enable-git]

> [!IMPORTANT]
> Nenhum segredo que não está definido como propriedades serão armazenadas no repositório de saudação e permanecerão no histórico de até que você desabilita e reabilitar o acesso de Git. Propriedades fornecem um local seguro toomanage valores de constante de cadeia de caracteres, inclusive segredos, em todas as políticas e configurações de API para não ter toostore-los diretamente em suas instruções de política. Para obter mais informações, consulte [como toouse propriedades nas políticas de gerenciamento do Azure API](api-management-howto-properties.md).
> 
> 

Para obter informações sobre como habilitar ou desabilitar o acesso de Git usando Olá API REST, consulte [habilitar ou desabilitar o acesso de Git usando a API REST de saudação](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a>repositório do Git toosave Olá serviço configuração toohello
a primeira etapa Olá antes da clonagem do repositório de saudação é estado atual do toosave saudação do repositório de toohello de configuração de serviço hello. Clique em **Salvar configuração toorepository**.

![Salvar configuração][api-management-save-configuration]

Faça as alterações desejadas na tela de confirmação de saudação e clique em **Okey** toosave.

![Salvar configuração][api-management-save-configuration-confirm]

Após alguns instantes configuração Olá é salvo e status de configuração de saudação do repositório de saudação é exibida, incluindo date de hello e a hora da última alteração de configuração hello e a última sincronização Olá entre a configuração do serviço hello e hello repositório.

![Status da configuração][api-management-configuration-status]

Depois de salvo toohello repositório configuração hello, ele pode ser clonado.

Para obter informações sobre como executar essa operação usando Olá API REST, consulte [configuração de confirmação de instantâneo usando a API REST de saudação](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).

## <a name="tooclone-hello-repository-tooyour-local-machine"></a>máquina local do tooyour tooclone Olá repositório
tooclone um repositório, que é necessário que o repositório de tooyour URL hello, um nome de usuário e uma senha. Olá nome de usuário e URL são exibidos superior de saudação do hello **repositório de configuração** guia.

![Clone do Git][api-management-configuration-git-clone]

senha Olá é gerada na parte inferior de saudação do hello **repositório de configuração** guia.

![Gerar senha][api-management-generate-password]

toogenerate uma senha, primeiro certifique-se que Olá **expiração** está definida toohello desejado de data e hora e, em seguida, clique em **gerar Token**.

![Senha][api-management-password]

> [!IMPORTANT]
> Anote essa senha. Depois que você deixar essa senha de saudação de página não será exibida novamente.
> 
> 

Olá seguindo exemplos de uso Olá Git Bash ferramenta de [Git para Windows](http://www.git-scm.com/downloads) , mas você pode usar qualquer ferramenta de Git que você esteja familiarizado com.

Abra sua ferramenta de Git na pasta desejada hello e execute Olá comando tooclone Olá git repositório tooyour máquina local a seguir, usando o comando Olá fornecido pelo portal do publicador hello.

```
git clone https://bugbashdev4.scm.azure-api.net/
```

Fornece nome de usuário de saudação e a senha quando solicitado.

Se você receber erros, tente modificar sua `git clone` comando tooinclude Olá nome e uma senha, conforme mostrado no exemplo a seguir de saudação.

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

Se isso fornece um erro, tente parte de senha de saudação do comando de saudação de codificação de URL. Um toodo de maneira rápida isso é tooopen Visual Studio, e o comando a seguir de saudação problema em Olá **janela imediata**. Olá tooopen **janela imediata**, abra qualquer solução ou projeto no Visual Studio (ou crie um novo aplicativo de console vazio) e escolha **Windows**, **imediato** de Olá **depurar** menu.

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

Use senha Olá codificado junto com seu nome e o repositório local tooconstruct Olá git comando de usuário.

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

Depois que o repositório de saudação é clonado, você pode exibir e trabalhar com ele no sistema de arquivos local. Para obter mais informações, veja [Referência da estrutura de pastas e arquivos do repositório Git local](#file-and-folder-structure-reference-of-local-git-repository).

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a>tooupdate seu repositório local com a configuração mais atual da instância de serviço Olá
Se você fizer a instância de serviço de gerenciamento de API de tooyour alterações no portal do publicador hello ou Olá API REST, você deve salvar o repositório de toohello essas alterações antes de atualizar o seu repositório local com as alterações mais recentes de saudação. toodo, clique **Salvar configuração toorepository** em Olá **repositório de configuração** guia no portal do publicador hello e, em seguida, emitir Olá comando no seu repositório local a seguir.

```
git pull
```

Antes de executar `git pull` Certifique-se de que você está na pasta Olá para seu repositório local. Se você concluiu a saudação `git clone` de comando, em seguida, você deve alterar o repositório de tooyour directory Olá executando um comando como Olá a seguir.

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a>alterações de toopush do seu repositório de servidor toohello repositório local
toopush alterações do seu repositório de servidor toohello repositório local, você deve confirmar suas alterações e, em seguida, enviá-las toohello repositório de servidor. toocommit suas alterações, abra a ferramenta de comando Git, comutador toohello diretório de repositório local e Olá problema comandos a seguir.

```
git add --all
git commit -m "Description of your changes"
```

toopush todos Olá confirma que o servidor toohello, execute Olá seguinte comando.

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a>toodeploy qualquer instância de serviço do serviço configuração alterações toohello gerenciamento de API
Depois que as alterações locais são confirmadas e enviadas por push toohello repositório de servidor, você pode implantá-las tooyour instância de serviço de gerenciamento de API.

![Implantar][api-management-configuration-deploy]

Para obter informações sobre como executar essa operação usando Olá API REST, consulte [Git implantar alterações tooconfiguration banco de dados usando a API REST de saudação](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a>Referência da estrutura de pastas e arquivos do repositório Git local
Olá arquivos e pastas no repositório do git local Olá contêm Olá informações de configuração sobre a instância de serviço hello.

| Item | Descrição |
| --- | --- |
| pasta api-management raiz |Contém a configuração de nível superior para a instância do serviço Olá |
| pasta apis |Contém a configuração de Olá Olá APIs na instância de serviço Olá |
| pasta groups |Contém a configuração de saudação de grupos de saudação na instância do serviço de saudação |
| pasta policies |Contém políticas de saudação na instância de serviço Olá |
| pasta portalStyles |Contém a configuração de saudação de personalizações portal do desenvolvedor Olá na instância de serviço Olá |
| pasta products |Contém a configuração de saudação de produtos Olá na instância de serviço Olá |
| pasta templates |Contém a configuração de saudação para modelos de email de saudação na instância de serviço Olá |

Cada pasta pode conter um ou mais arquivos e, em alguns casos, uma ou mais pastas, por exemplo, uma pasta para cada API, produto ou grupo. arquivos Hello dentro de cada pasta são específicos para o tipo de entidade Olá descrito pelo nome da pasta hello.

| Tipo de arquivo | Finalidade |
| --- | --- |
| json |Informações de configuração sobre a entidade respectivos Olá |
| html |Descrições sobre entidade hello, geralmente é exibido no portal do desenvolvedor Olá |
| xml |Declarações de políticas |
| css |Folhas de estilo para personalização do portal do desenvolvedor |

Esses arquivos podem ser criados, excluídos, editados e gerenciados no sistema de arquivos local, e alterações de saudação implantadas toohello back sua instância de serviço de gerenciamento de API.

> [!NOTE]
> Olá entidades a seguir não estão contidas no repositório do Git hello e não podem ser configuradas usando o Git.
> 
> * Usuários
> * Assinaturas
> * Propriedades
> * Outras entidades do portal do desenvolvedor além dos estilos
> 
> 

### <a name="root-api-management-folder"></a>Pasta api-management raiz
raiz de saudação `api-management` pasta contém um `configuration.json` arquivo que contém informações de nível superior sobre a instância de serviço de saudação no hello formato a seguir.

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

Olá primeiro quatro configurações (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, e `UserRegistrationTermsConsentRequired`) mapear toohello configurações a seguir no hello **identidades** guia Olá **segurança** seção.

| Configuração de identidade | Mapeia muito|
| --- | --- |
| RegistrationEnabled |**Redirecionar usuários anônimos toosign na página** caixa de seleção |
| UserRegistrationTerms |**Termos de uso na inscrição do usuário**  |
| UserRegistrationTermsEnabled |**Mostrar os termos de uso na página de entrada**  |
| UserRegistrationTermsConsentRequired |**Exigir consentimento**  |

![Configurações de identidade][api-management-identity-settings]

Olá quatro configurações (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, e `DelegationValidationKey`) mapear toohello configurações a seguir no hello **delegação** guia Olá **segurança** seção.

| Configuração de delegação | Mapeia muito|
| --- | --- |
| DelegationEnabled |Caixa de seleção **Delegar entrada e inscrição** |
| DelegationUrl |**URL do ponto de extremidade da delegação**  |
| DelegatedSubscriptionEnabled |**Delegar assinatura do produto**  |
| DelegationValidationKey |**Delegar Chave de Validação**  |

![Configurações de delegação][api-management-delegation-settings]

Olá configuração final, `$ref-policy`, mapeia toohello política global instruções arquivo hello instância de serviço.

### <a name="apis-folder"></a>pasta apis
Olá `apis` pasta contém uma pasta para cada API na instância de serviço Olá que contém Olá itens a seguir.

* `apis\<api name>\configuration.json`-Esta é a configuração Olá Olá API e contém informações sobre a URL de serviço de back-end hello e operações de saudação. Isso é hello mesmas informações que seriam retornadas se você toocall [obter uma API específica](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) com `export=true` na `application/json` formato.
* `apis\<api name>\api.description.html`-Esta é a descrição de saudação do hello API e corresponde toohello `description` propriedade Olá [entidade API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).
* `apis\<api name>\operations\`-Esta pasta contém `<operation name>.description.html` arquivos que operações de mapa toohello no hello API. Cada arquivo contém a descrição de saudação de uma única operação no hello API que mapeia toohello `description` propriedade Olá [entidade de operação](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) em Olá API REST.

### <a name="groups-folder"></a>pasta groups
Olá `groups` pasta contém uma pasta para cada grupo definido na instância de serviço hello.

* `groups\<group name>\configuration.json`-Esta é a configuração Olá para o grupo de saudação. Isso é hello mesmas informações que seriam retornadas se você Olá toocall [obter um grupo específico](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operação.
* `groups\<group name>\description.html`-Esta é a descrição de saudação do grupo de saudação e corresponde toohello `description` propriedade Olá [grupo entidade](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).

### <a name="policies-folder"></a>pasta policies
Olá `policies` pasta contém declarações de política de saudação para sua instância de serviço.

* `policies\global.xml` - contém políticas definidas no escopo global da instância de seu serviço.
* `policies\apis\<api name>\` - se houver alguma política definida no escopo da API, ela estará nessa pasta.
* `policies\apis\<api name>\<operation name>\`pasta - se você tiver qualquer políticas definidas no escopo da operação, elas são contidas nessa pasta na `<operation name>.xml` arquivos mapeados toohello declarações de política para cada operação.
* `policies\products\`-Se você tiver qualquer políticas definidas no escopo do produto, elas são contidas nessa pasta, que contém `<product name>.xml` arquivos mapeados toohello declarações de política para cada produto.

### <a name="portalstyles-folder"></a>pasta portalStyles
Olá `portalStyles` pasta contém a configuração e folhas de estilo para personalizações portal do desenvolvedor Olá instância de serviço.

* `portalStyles\configuration.json`-contém os nomes de Olá Olá de folhas de estilo usadas pelo portal do desenvolvedor Olá
* `portalStyles\<style name>.css`-cada `<style name>.css` arquivo contém estilos para o portal do desenvolvedor hello (`Preview.css` e `Production.css` por padrão).

### <a name="products-folder"></a>pasta products
Olá `products` pasta contém uma pasta para cada produto definido na instância de serviço hello.

* `products\<product name>\configuration.json`-Esta é a configuração Olá para o produto de saudação. Isso é hello mesmas informações que seriam retornadas se você Olá toocall [obter um produto específico](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operação.
* `products\<product name>\product.description.html`-Esta é a descrição de saudação do produto de saudação e corresponde toohello `description` propriedade Olá [entidade product](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) em Olá API REST.

### <a name="templates"></a>modelos
Olá `templates` pasta contém a configuração de saudação [modelos de email](api-management-howto-configure-notifications.md) da instância de serviço hello.

* `<template name>\configuration.json`-Esta é a configuração Olá para o modelo de email hello.
* `<template name>\body.html`-Este é o corpo de saudação do modelo de email de saudação.

## <a name="next-steps"></a>Próximas etapas
Para obter informações sobre outra maneiras toomanage sua instância de serviço, consulte:

* Gerenciar a instância de serviço usando Olá seguintes cmdlets do PowerShell
  * [Referência de cmdlets do PowerShell para implantação de serviços](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [Referência de cmdlet do PowerShell para gerenciamento de serviços](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* Gerenciar a instância de serviço no portal do publicador Olá
  * [Gerenciar sua primeira API](api-management-get-started.md)
* Gerenciar a instância de serviço usando a API REST de saudação
  * [Referência de API REST do Gerenciamento de API](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a>Assista a uma visão geral em vídeo
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




