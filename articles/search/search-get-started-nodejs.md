---
title: aaaGet iniciar a pesquisa do Azure no Node. js | Microsoft Docs
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
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a>Introdução ao Azure Search no Node.js
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Saiba como o aplicativo que usa a pesquisa do Azure para sua experiência de pesquisa de pesquisa toobuild um Node. js personalizado. Este tutorial usa Olá [API de REST do serviço de pesquisa do Azure](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct Olá objetos e operações usadas neste exercício.

Usamos [Node.js](https://Nodejs.org) e NPM, [Sublime 3 de texto](http://www.sublimetext.com/3)e o Windows PowerShell no Windows 8.1 toodevelop e testar esse código.

toorun neste exemplo, você deve ter um serviço de pesquisa do Azure, que pode inscrever-se em Olá [portal do Azure](https://portal.azure.com). Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter instruções passo a passo.

## <a name="about-hello-data"></a>Sobre dados saudação
Este aplicativo de exemplo usa dados da saudação [dos Estados Unidos geológica serviços (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtrado no tamanho do conjunto de dados do hello estado de Rhode Island tooreduce hello. Vamos usar essa toobuild dados um aplicativo de pesquisa que retorna as construções de pontos de referência, como escolas e hospitais, bem como recursos geológica como fluxos, Lagos e Cúpulas.

Neste aplicativo, Olá **DataIndexer** programa cria e carrega Olá índice usando um [indexador](https://msdn.microsoft.com/library/azure/dn798918.aspx) construção, recuperando Olá filtrados USGS conjunto de dados de um banco de dados do SQL Azure público. Conexão e credenciais de fonte de dados online toohello informações é fornecido no código do programa hello. Nenhuma configuração adicional é necessária.

> [!NOTE]
> Aplicamos um filtro em toostay este conjunto de dados abaixo do limite de documento 10.000 Olá de saudação livre de camada de preços. Se você usar a camada padrão hello, esse limite não se aplica. Para obter detalhes sobre a capacidade de cada tipo de preço, consulte [Limites de serviço da Pesquisa](search-limits-quotas-capacity.md).
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Localizar o nome do serviço hello e chave de api do serviço de pesquisa do Azure
Depois de criar serviço hello, retorne toohello tooget portal Olá URL ou `api-key`. Conexões tooyour serviço de pesquisa requer que você tenha ambas as URLs de saudação e um `api-key` tooauthenticate chamada de saudação.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Na barra de salto hello, clique em **serviço de pesquisa** toolist todos os serviços de pesquisa do Azure provisionados para sua assinatura.
3. Selecione serviço Olá toouse desejado.
4. No painel de serviço hello, você deverá ver blocos de informações essenciais, como o ícone de chave Olá para acessar as chaves de administração de saudação.
5. Copie a URL do serviço hello, uma chave de administração e uma chave de consulta. Você precisa todos os três posteriormente quando você adicioná-las toohello config.js arquivo.

## <a name="download-hello-sample-files"></a>Baixar arquivos de exemplo hello
Use um dos Olá exemplo de hello toodownload abordagens a seguir.

1. Vá muito[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).
2. Clique em **baixar ZIP**, salve o arquivo. zip de saudação e, em seguida, extraia todos os arquivos de saudação nele.

Todas as modificações de arquivos posteriores e instruções de execução serão feitas nos arquivos nessa pasta.

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a>Atualize config.js hello. com a URL e a chave de api do serviço Pesquisa
Usando Olá URL e a chave de api que você copiou anteriormente, especifique a URL de hello, chave de administração e a chave de consulta no arquivo de configuração.

As chaves de administrador oferecem controle total sobre as operações do serviço, incluindo a criação ou exclusão de um índice e carregamento de documentos. Em contraste, as chaves de consulta são para operações somente leitura, normalmente usadas por aplicativos cliente que se conectam tooAzure pesquisa.

Neste exemplo, nós incluímos consulta Olá toohelp chave reforçar a prática recomendada de saudação do uso de chave de consulta Olá em aplicativos cliente.

Olá captura de tela mostra a seguir **config.js** aberto em um editor de texto com hello entradas relevantes delimitadas para que você possa ver onde o arquivo hello tooupdate Olá valores que são válidas para o serviço de pesquisa.

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a>Host de um ambiente de tempo de execução para o exemplo hello
exemplo Hello requer um servidor HTTP, que pode ser instalado usando globalmente npm.

Use uma janela do PowerShell para Olá comandos a seguir.

1. Navegue toohello pasta que contém a saudação **Package. JSON** arquivo.
2. Digite `npm install`.
3. Digite `npm install -g http-server`.

## <a name="build-hello-index-and-run-hello-application"></a>Criar índice hello e executar o aplicativo hello
1. Digite `npm run indexDocuments`.
2. Digite `npm run build`.
3. Digite `npm run start_server`.
4. Direcione seu navegador para `http://localhost:8080/index.html`

## <a name="search-on-usgs-data"></a>Pesquisar dados do USGS
conjunto de dados USGS Olá inclui registros que são relevante toohello estado de Rhode Island. Se você clicar em **pesquisa** em uma caixa de pesquisa vazia, você obter entradas de 50 principais hello, que é o padrão de saudação.

Inserindo um termo de pesquisa fornece o mecanismo de pesquisa Olá algo toogo em. Tente inserir um nome regional. "Roger Williams" era o administrador primeiro Olá de Rhode Island. Vários parques, edifícios e escolas receberam seus nomes em homenagem a ele.

![][9]

Você também pode tentar qualquer um destes termos:

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>Próximas etapas
Este é o hello primeiro tutorial de pesquisa do Azure com base em Node. js e hello USGS dataset. Ao longo do tempo, estenderemos esse tutorial toodemonstrate recursos adicionais de pesquisa convém toouse em suas soluções personalizadas.

Se você já tiver alguma experiência com a Pesquisa do Azure, use este exemplo como um trampolim para experimentar sugestões (consultas de preenchimento automático ou de digitação antecipada), filtros e navegação facetada. Você também pode melhorar após a página de resultados da pesquisa de saudação adicionando contagens e envio em lote documentos para que os usuários podem percorrer resultados hello.

TooAzure nova pesquisa? É recomendável tentar toodevelop outros tutoriais um entendimento de como você pode criar. Visite nosso [página de documentação](https://azure.microsoft.com/documentation/services/search/) toofind mais recursos. Você também pode exibir links Olá em nosso [vídeo e Tutorial lista](search-video-demo-tutorial-list.md) tooaccess obter mais informações.

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
