---
title: "Configurar o serviço de Gerenciamento de API usando o Git - Azure | Microsoft Docs"
description: "Saiba como salvar e definir a configuração de seu serviço de Gerenciamento de API usando o Git"
services: api-management
documentationcenter: 
author: vladvino
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
ms.openlocfilehash: 0abf2635e08bfc3113e9dec1947b9bb162cd3952
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="how-to-save-and-configure-your-api-management-service-configuration-using-git"></a>Como salvar e definir a configuração de seu serviço de Gerenciamento de API usando o Git
> 
> 

Cada instância do serviço de Gerenciamento de API mantém um banco de dados de configuração que contém informações sobre a configuração e sobre os metadados da instância do serviço. É possível fazer alterações na instância do serviço alterando uma configuração no portal do editor, usando um cmdlet do PowerShell ou fazendo uma chamada à API REST. Além desses métodos, você também pode gerenciar a configuração da instância do serviço usando o Git, permitindo cenários de gerenciamento de serviço, como:

* Controle de versão da configuração - baixe e armazene versões diferentes da configuração do seu serviço
* Alterações de configuração em massa - faça alterações em várias partes da configuração de seu serviço no repositório local e integre essas alterações no servidor com uma única operação
* Cadeia de ferramentas e fluxo de trabalho conhecido do Git - use as ferramentas e fluxo de trabalho do Git com os quais você já está familiarizado

O diagrama a seguir mostra uma visão geral das diferentes maneiras de configurar sua instância de serviço do Gerenciamento de API.

![Configuração do Git][api-management-git-configure]

Quando você faz alterações em seu serviço usando o portal do editor, cmdlets do PowerShell ou a API REST, você está gerenciando o banco de dados de configuração de seu serviço usando o ponto de extremidade `https://{name}.management.azure-api.net` , como exibido no lado direito do diagrama. O lado esquerdo do diagrama ilustra como você pode gerenciar a configuração de seu serviço usando o Git e o repositório Git de seu serviço localizado em `https://{name}.scm.azure-api.net`.

As etapas a seguir fornecem uma visão geral do gerenciamento de sua instância de serviço de Gerenciamento de API usando o Git.

1. Acessar a configuração GIT em seu serviço
2. Salvar o banco de dados de configuração de seu serviço em seu repositório Git
3. Clonar o repositório Git em seu computador local
4. Obter o repositório mais recente em seu computador local, confirmar e enviar as alterações de volta ao seu repositório
5. Implantar as alterações de seu repositório para o banco de dados de configuração de seu serviço

Este artigo descreve como habilitar e usar o Git para gerenciar a configuração de seu serviço e fornece uma referência para os arquivos e pastas no repositório Git.

## <a name="access-git-configuration-in-your-service"></a>Acessar a configuração GIT em seu serviço
Você pode exibir rapidamente o status da configuração do Git exibindo o ícone do Git no canto superior direito do portal do editor. Neste exemplo, a mensagem de status indica que há alterações não salvas no repositório. Isso ocorre porque o banco de dados de configuração do serviço de Gerenciamento de API ainda não foi salvo no repositório.

![Status do Git][api-management-git-icon-enable]

Para exibir e definir as configurações do Git, clique no ícone do Git ou clique no menu **Segurança** e navegue até a guia **Repositório de configuração**.

![Habilitar o GIT][api-management-enable-git]

> [!IMPORTANT]
> Quaisquer segredos que não sejam definidos como propriedades serão armazenados no repositório e permanecerão em seu histórico até que você desabilite e habilite novamente o acesso ao Git. As propriedades fornecem um local seguro para o gerenciamento de valores constantes de cadeia de caracteres, incluindo segredos, em todas as configurações e políticas de API. Portanto, não é necessário armazená-los diretamente nas instruções de sua política. Para saber mais, confira [Como usar as propriedades nas políticas de Gerenciamento de API do Azure](api-management-howto-properties.md).
> 
> 

Para saber mais sobre como habilitar ou desabilitar o acesso ao Git usando a API REST, confira [Habilitar ou desabilitar o acesso ao Git usando a API REST](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).

## <a name="to-save-the-service-configuration-to-the-git-repository"></a>Para salvar a configuração do serviço no repositório Git
A primeira etapa antes de clonar o repositório é salvar o estado atual da configuração do serviço no repositório. Clique em **Salvar configuração no repositório**.

![Salvar configuração][api-management-save-configuration]

Faça as alterações desejadas na tela de confirmação e clique em **Ok** para salvar.

![Salvar configuração][api-management-save-configuration-confirm]

Após alguns instantes, a configuração será salva e o status da configuração do repositório será exibido, incluindo a data e a hora da última alteração de configuração e a última sincronização entre a configuração do serviço e o repositório.

![Status da configuração][api-management-configuration-status]

Quando a configuração for salva no repositório, ele poderá ser clonado.

Para saber mais sobre como executar essa operação usando a API REST, confira [Confirmar a configuração do instantâneo usando a API REST](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).

## <a name="to-clone-the-repository-to-your-local-machine"></a>Para clonar o repositório em seu computador local
Para clonar um repositório, você precisa da URL de seu repositório, um nome de usuário e uma senha. O nome de usuário e a URL são exibidos próximos à parte superior da guia **Repositório de configuração** .

![Clone do Git][api-management-configuration-git-clone]

A senha é gerada na parte inferior da guia **Repositório de configuração** .

![Gerar senha][api-management-generate-password]

Para gerar uma senha, primeiro verifique se **Vencimento** está definido como a data e a hora de vencimento desejadas e clique em **Gerar Token**.

![Senha][api-management-password]

> [!IMPORTANT]
> Anote essa senha. Depois que você sair desta página a senha não será exibida novamente.
> 
> 

Os exemplos a seguir usam a ferramenta Git Bash do [Git para Windows](http://www.git-scm.com/downloads) , mas você pode usar qualquer ferramenta Git com a qual esteja familiarizado.

Abra sua ferramenta Git na pasta desejada e execute o comando a seguir para clonar o repositório git em seu computador local usando o comando fornecido pelo portal do editor.

```
git clone https://bugbashdev4.scm.azure-api.net/
```

Quando solicitado, forneça o nome de usuário e a senha.

Se ocorrer algum erro, tente modificar seu comando `git clone` para incluir o nome de usuário e a senha, conforme exibido no exemplo a seguir.

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

Se isso resultar em erro, tente codificar na URL a parte da senha do comando. Uma maneira rápida de fazer isso é abrir o Visual Studio e emitir o seguinte comando na **Janela Imediata**. Para abrir a **Janela Imediata**, abra qualquer solução ou projeto no Visual Studio (ou crie um novo aplicativo de console vazio) e escolha **Janelas**, **Imediata** no menu **Depuração**.

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

Use a senha codificada juntamente com seu nome de usuário e o local do repositório para construir o comando do git.

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

Assim que o repositório for clonado, você poderá exibi-lo e trabalhar com ele no sistema de arquivos local. Para obter mais informações, veja [Referência da estrutura de pastas e arquivos do repositório Git local](#file-and-folder-structure-reference-of-local-git-repository).

## <a name="to-update-your-local-repository-with-the-most-current-service-instance-configuration"></a>Para atualizar seu repositório local com a configuração mais recente da instância do serviço
Se você fizer alterações na instância de seu serviço de Gerenciamento de API no portal do editor, ou usando a API REST, será necessário salvar essas alterações no repositório antes de poder atualizar seu repositório local com as alterações mais recentes. Para fazer isso, clique em **Salvar configuração no repositório** na guia **Repositório de configuração** no portal do editor e emita o seguinte comando em seu repositório local.

```
git pull
```

Antes de executar o `git pull` , certifique-se de que você esteja na pasta de seu repositório local. Se você acabou de concluir o comando `git clone` , será necessário alterar o diretório de seu repositório executando um comando parecido com o seguinte.

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="to-push-changes-from-your-local-repo-to-the-server-repo"></a>Para enviar por push as alterações de seu repositório local para o repositório do servidor
Para enviar por push as alterações de seu repositório local para o repositório do servidor, você deve confirmar as alterações e, em seguida, enviá-las ao repositório do servidor. Para confirmar as alterações, abra sua ferramenta de comando do Git, alterne para o diretório de seu repositório local e execute os comandos a seguir.

```
git add --all
git commit -m "Description of your changes"
```

Para enviar por push todas as confirmações para o servidor, execute o comando a seguir.

```
git push
```

## <a name="to-deploy-any-service-configuration-changes-to-the-api-management-service-instance"></a>Para implantar quaisquer alterações da configuração do serviço na instância do serviço de Gerenciamento de API
Após a confirmação de suas alterações locais e o envio para o repositório do servidor, você pode implantá-las na instância de seu serviço de Gerenciamento de API.

![Implantar][api-management-configuration-deploy]

Para saber mais sobre como executar essa operação usando a API REST, confira [Implantar as alterações do Git no banco de dados de configuração usando a API REST](https://docs.microsoft.com/rest/api/apimanagement/tenantconfiguration).

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a>Referência da estrutura de pastas e arquivos do repositório Git local
Os arquivos e pastas no repositório git local contêm as informações de configuração sobre a instância do serviço.

| Item | Descrição |
| --- | --- |
| pasta api-management raiz |Contém a configuração de nível superior da instância do serviço |
| pasta apis |Contém a configuração das APIs na instância do serviço |
| pasta groups |Contém a configuração dos grupos na instância do serviço |
| pasta policies |Contém as políticas na instância do serviço |
| pasta portalStyles |Contém a configuração das personalizações do portal do desenvolvedor na instância do serviço |
| pasta products |Contém a configuração dos produtos na instância do serviço |
| pasta templates |Contém a configuração dos modelos de email na instância do serviço |

Cada pasta pode conter um ou mais arquivos e, em alguns casos, uma ou mais pastas, por exemplo, uma pasta para cada API, produto ou grupo. Os arquivos em cada pasta são específicos ao tipo de entidade descrito pelo nome da pasta.

| Tipo de arquivo | Finalidade |
| --- | --- |
| json |Informações de configuração sobre a respectiva entidade |
| html |Descrições sobre a entidade, geralmente exibidas no portal do desenvolvedor |
| xml |Declarações de políticas |
| css |Folhas de estilo para personalização do portal do desenvolvedor |

Esses arquivos podem ser criados, excluídos, editados e gerenciados em seu sistema de arquivos local, e as alterações podem ser implantadas de volta na instância de seu serviço de Gerenciamento de API.

> [!NOTE]
> As entidades a seguir não estão no repositório Git e não podem ser configuradas usando o Git.
> 
> * Usuários
> * Assinaturas
> * Propriedades
> * Outras entidades do portal do desenvolvedor além dos estilos
> 
> 

### <a name="root-api-management-folder"></a>Pasta api-management raiz
A pasta `api-management` raiz contém um arquivo `configuration.json` com informações de alto nível sobre a instância do serviço no seguinte formato.

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

As primeiras quatro configurações (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled` e `UserRegistrationTermsConsentRequired`) são mapeadas para as seguintes configurações na guia **Identidades** da seção **Segurança**.

| Configuração de identidade | É mapeada para |
| --- | --- |
| RegistrationEnabled |**Redirecionar usuários anônimos para a página de entrada**  |
| UserRegistrationTerms |**Termos de uso na inscrição do usuário**  |
| UserRegistrationTermsEnabled |**Mostrar os termos de uso na página de entrada**  |
| UserRegistrationTermsConsentRequired |**Exigir consentimento**  |

![Configurações de identidade][api-management-identity-settings]

As quatro configurações seguintes (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled` e `DelegationValidationKey`) são mapeadas para as seguintes configurações na guia **Delegação** da seção **Segurança**.

| Configuração de delegação | É mapeada para |
| --- | --- |
| DelegationEnabled |Caixa de seleção **Delegar entrada e inscrição** |
| DelegationUrl |**URL do ponto de extremidade da delegação**  |
| DelegatedSubscriptionEnabled |**Delegar assinatura do produto**  |
| DelegationValidationKey |**Delegar Chave de Validação**  |

![Configurações de delegação][api-management-delegation-settings]

A configuração final, `$ref-policy`, é mapeada para o arquivo de instruções de política global da instância do serviço.

### <a name="apis-folder"></a>pasta apis
A pasta `apis` contém uma pasta para cada API na instância do serviço que contém os itens a seguir.

* `apis\<api name>\configuration.json` - é a configuração da API e contém informações sobre a URL do serviço de back-end e as operações. Essas são as mesmas informações que retornariam se você chamasse [Obter uma API específica](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) com `export=true` no formato `application/json`.
* `apis\<api name>\api.description.html` - é a descrição da API e corresponde à propriedade `description` da [entidade da API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).
* `apis\<api name>\operations\` - esta pasta contém os arquivos `<operation name>.description.html` que são mapeados para as operações na API. Cada arquivo contém a descrição de uma única operação na API que mapeia para a propriedade `description` da [entidade de operação](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) na API REST.

### <a name="groups-folder"></a>pasta groups
A pasta `groups` contém uma pasta para cada grupo definido na instância do serviço.

* `groups\<group name>\configuration.json` - é a configuração do grupo. Essas são as mesmas informações que retornariam se você chamasse a operação [Obter um grupo específico](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) .
* `groups\<group name>\description.html` - é a descrição do grupo e corresponde à propriedade `description` da [entidade de grupo](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).

### <a name="policies-folder"></a>pasta policies
A pasta `policies` contém as instruções da política para a instância de seu serviço.

* `policies\global.xml` - contém políticas definidas no escopo global da instância de seu serviço.
* `policies\apis\<api name>\` - se houver alguma política definida no escopo da API, ela estará nessa pasta.
* Pasta `policies\apis\<api name>\<operation name>\` - se houver alguma política definida no escopo da operação, ela estará nessa pasta, nos arquivos `<operation name>.xml`, que são mapeados para as instruções da política de cada operação.
* `policies\products\` - se houver alguma política definida no escopo do produto, ela estará nessa pasta, que contém os arquivos `<product name>.xml`, que são mapeados para as instruções da política de cada produto.

### <a name="portalstyles-folder"></a>pasta portalStyles
A pasta `portalStyles` contém folhas de estilo e configuração para personalizações do portal do desenvolvedor da instância do serviço.

* `portalStyles\configuration.json` - contém os nomes das folhas de estilo usadas pelo portal do desenvolvedor
* `portalStyles\<style name>.css` - cada arquivo `<style name>.css` contém estilos para o portal do desenvolvedor (`Preview.css` e `Production.css` por padrão).

### <a name="products-folder"></a>pasta products
A pasta `products` contém uma pasta para cada produto definida na instância do serviço.

* `products\<product name>\configuration.json` - é a configuração do produto. Essas são as mesmas informações que retornariam se você chamasse a operação [Obter um produto específico](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) .
* `products\<product name>\product.description.html` - é a descrição do produto e corresponde à propriedade `description` da [entidade do produto](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) na API REST.

### <a name="templates"></a>modelos
A pasta `templates` contém a configuração dos [modelos de email](api-management-howto-configure-notifications.md) na instância do serviço.

* `<template name>\configuration.json` - é a configuração do modelo de email.
* `<template name>\body.html` - é o corpo do modelo de email.

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre outras maneiras de gerenciar sua instância de serviço, confira:

* Gerenciar a instância de seu serviço usando os seguintes cmdlets do PowerShell
  * [Referência de cmdlets do PowerShell para implantação de serviços](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [Referência de cmdlet do PowerShell para gerenciamento de serviços](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* Gerenciar a instância de seu serviço no portal do editor.
  * [Gerenciar sua primeira API](import-and-publish.md)
* Gerenciar a instância de seu serviço usando a API REST
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




