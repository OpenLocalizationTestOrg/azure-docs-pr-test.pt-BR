---
title: "Introdução ao Azure Search no Node.js | Microsoft Docs"
description: "Percorra a criação de um aplicativo de pesquisa em um serviço de pesquisa hospedado na nuvem no Azure usando Node.js como linguagem de programação."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: 32865ed986f5eea961ef2c3813dcc6531498c90a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a>Introdução ao Azure Search no Node.js
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Aprenda a criar um aplicativo de pesquisa Node.js personalizado que usa o Azure Search para a sua experiência de pesquisa. O tutorial usa a [API REST do Serviço de Pesquisa do Azure](https://msdn.microsoft.com/library/dn798935.aspx) para construir os objetos e as operações usados neste exercício.

Usamos o [Node.js](https://Nodejs.org) e o NPM, o [Sublime Text 3](http://www.sublimetext.com/3) e o Windows PowerShell no Windows 8.1 para desenvolver e testar esse código.

Para executar este exemplo, você deve ter um serviço do Azure Search, no qual pode se inscrever no [portal do Azure](https://portal.azure.com). Consulte [Criar um serviço de Pesquisa do Azure no portal](search-create-service-portal.md) para encontrar instruções passo a passo.

## <a name="about-the-data"></a>Sobre os dados
Este exemplo de aplicativo usa dados do [Serviço Geológico dos Estados Unidos (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtrados no estado de Rhode Island, para reduzir o tamanho do conjunto de dados. Vamos usar esses dados para criar um aplicativo de pesquisa que retorna prédios de referência, por exemplo, hospitais e escolas, e características geológicas, como rios, lagos e picos.

Neste aplicativo, o programa **DataIndexer** cria e carrega o índice usando um constructo [Indexador](https://msdn.microsoft.com/library/azure/dn798918.aspx) , recuperando o conjunto de dados filtrado do USGS de um Banco de Dados SQL do Azure público. As informações de credenciais e de conexão para a fonte de dados online são fornecidas no código do programa. Nenhuma configuração adicional é necessária.

> [!NOTE]
> Aplicamos um filtro a esse conjunto de dados para permanecer abaixo do limite de 10.000 documentos da camada de preços gratuita. Se você usar a camada padrão, esse limite não se aplicará. Para obter detalhes sobre a capacidade de cada tipo de preço, consulte [Limites de serviço da Pesquisa](search-limits-quotas-capacity.md).
> 
> 

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a>Localizar o nome do serviço e a chave de api do serviço de Pesquisa do Azure
Depois de criar o serviço, retorne ao portal para obter a URL ou `api-key`. Conexões com seu serviço de Pesquisa requerem que você tenha tanto uma URL quanto um `api-key` para autenticar a chamada.

1. Entre no [Portal do Azure](https://portal.azure.com).
2. Na barra de atalhos, clique em **Serviço de Pesquisa** para listar todos os serviços do Azure Search provisionados para a sua assinatura.
3. Selecione o serviço que você deseja usar.
4. No painel de serviço, você deverá ver blocos com as informações essenciais, como o ícone de chave para acessar as chaves de administrador.
5. Copie a URL do serviço, uma chave de administrador e uma chave de consulta. Você precisa de todos os três mais tarde, ao adicioná-los ao arquivo config.js.

## <a name="download-the-sample-files"></a>Baixe os arquivos do exemplo.
Use qualquer um dos procedimentos a seguir para baixar o exemplo.

1. Acesse [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).
2. Clique em **Baixar ZIP**, salve o arquivo .zip e, em seguida, extraia todos os arquivos que ele contém.

Todas as modificações de arquivos posteriores e instruções de execução serão feitas nos arquivos nessa pasta.

## <a name="update-the-configjs-with-your-search-service-url-and-api-key"></a>Atualize o config.js. com a URL e a chave de api do serviço Pesquisa
Usando a URL e a chave de api que você copiou anteriormente, especifique a URL, a chave de administrador e a chave de consulta no arquivo de configuração.

As chaves de administrador oferecem controle total sobre as operações do serviço, incluindo a criação ou exclusão de um índice e carregamento de documentos. Em contraste, as chaves de consulta servem para operações somente leitura, normalmente usadas por aplicativos cliente que se conectam à Pesquisa do Azure.

Neste exemplo, incluímos a chave de consulta para ajudar a reforçar a prática recomendada de usar a chave de consulta em aplicativos cliente.

A captura de tela a seguir mostra **config.js** aberto em um editor de texto, com as entradas relevantes demarcadas para que você possa ver onde deve atualizá-lo com os valores válidos para o serviço de pesquisa.

![][5]

## <a name="host-a-runtime-environment-for-the-sample"></a>Hospedar um ambiente de tempo de execução para o exemplo
O exemplo exige um servidor HTTP, que pode ser instalado globalmente usando npm.

Use uma janela do PowerShell para os comandos a seguir.

1. Navegue até a pasta que contém o arquivo **package.json** .
2. Digite `npm install`.
3. Digite `npm install -g http-server`.

## <a name="build-the-index-and-run-the-application"></a>Crie o índice e executar o aplicativo.
1. Digite `npm run indexDocuments`.
2. Digite `npm run build`.
3. Digite `npm run start_server`.
4. Direcione seu navegador para `http://localhost:8080/index.html`

## <a name="search-on-usgs-data"></a>Pesquisar dados do USGS
O conjunto de dados do USGS inclui registros relevantes para o estado de Rhode Island. Se você clicar em **Pesquisar** em uma caixa de pesquisa vazia, obterá as 50 entradas principais, que é o valor padrão.

A inserção de um termo de pesquisa fornece ao mecanismo de pesquisa algo para seguir. Tente inserir um nome regional. "Roger Williams" foi o primeiro governador de Rhode Island. Vários parques, edifícios e escolas receberam seus nomes em homenagem a ele.

![][9]

Você também pode tentar qualquer um destes termos:

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>Próximas etapas
Este é o primeiro tutorial do Azure Search com base no Node.js e no conjunto de dados do USGS. Ao longo do tempo, ampliaremos este tutorial para demonstrar outros recursos de pesquisa que talvez você queira usar em suas soluções personalizadas.

Se você já tiver alguma experiência com a Pesquisa do Azure, use este exemplo como um trampolim para experimentar sugestões (consultas de preenchimento automático ou de digitação antecipada), filtros e navegação facetada. Você também pode melhorar a página de resultados da pesquisa adicionando contagens e documentos em lote para que os usuários possam percorrer os resultados.

Ainda não conhece a Pesquisa do Azure? Recomendamos os outros tutoriais para que você compreenda o que pode criar. Visite nossa [página de documentação](https://azure.microsoft.com/documentation/services/search/) para encontrar mais recursos. Você também pode exibir os links em nossa [Lista de vídeos e Tutorial](search-video-demo-tutorial-list.md) para acessar mais informações.

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
