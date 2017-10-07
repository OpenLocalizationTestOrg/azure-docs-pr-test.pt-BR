---
title: aaaGet iniciar a pesquisa do Azure em Java | Microsoft Docs
description: "Como a pesquisa de toobuild uma nuvem hospedada aplicativo no Azure usando o Java como sua linguagem de programação."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a>Introdução à Pesquisa do Azure em Java
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Saiba como o aplicativo que usa a pesquisa do Azure para sua experiência de pesquisa de pesquisa toobuild um Java personalizados. Este tutorial usa Olá [API de REST do serviço de pesquisa do Azure](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct Olá objetos e operações usadas neste exercício.

toorun neste exemplo, você deve ter um serviço de pesquisa do Azure, que pode inscrever-se em Olá [Portal do Azure](https://portal.azure.com). Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter instruções passo a passo.

Podemos usado Olá toobuild de software a seguir e testar este exemplo:

* [Eclipse IDE para desenvolvedores de Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar). Ter certeza de que toodownload Olá EE versão. Uma das etapas de verificação de saudação exige um recurso que se encontra apenas nesta edição.
* [JDK 8u40](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Apache Tomcat 8.0](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a>Sobre dados saudação
Este aplicativo de exemplo usa dados da saudação [dos Estados Unidos geológica serviços (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtrado no tamanho do conjunto de dados do hello estado de Rhode Island tooreduce hello. Vamos usar essa toobuild dados um aplicativo de pesquisa que retorna as construções de pontos de referência, como escolas e hospitais, bem como recursos geológica como fluxos, Lagos e Cúpulas.

Neste aplicativo, Olá **SearchServlet.java** programa cria e carrega Olá índice usando um [indexador](https://msdn.microsoft.com/library/azure/dn798918.aspx) construção, recuperando Olá filtrados USGS conjunto de dados de um banco de dados do SQL Azure público. Credenciais predefinidas e fonte de dados online de toohello de informações de conexão são fornecidas no código do programa hello. Em termos de acesso a dados, nenhuma configuração adicional é necessária.

> [!NOTE]
> Aplicamos um filtro em toostay este conjunto de dados abaixo do limite de documento 10.000 Olá de saudação livre de camada de preços. Se você usar a camada padrão Olá, não se aplicam a esse limite, e você pode modificar este código toouse um conjunto de dados maior. Para obter detalhes sobre a capacidade de cada camada de preços, consulte [Limites e restrições](search-limits-quotas-capacity.md).
> 
> 

## <a name="about-hello-program-files"></a>Sobre arquivos de programa Olá
Olá lista a seguir descreve os arquivos de saudação que são relevantes toothis exemplo.

* Search.jsp: Fornece a interface do usuário Olá
* SearchServlet.java: Fornece métodos (semelhante tooa controlador MVC)
* SearchServiceClient.java: lida com solicitações HTTP
* SearchServiceHelper.java: uma classe auxiliar que fornece métodos estáticos
* Document.Java: Fornece o modelo de dados de saudação
* config: define a URL do serviço de pesquisa de saudação e chave de api
* Pom.xml: uma dependência do Maven

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Localizar o nome do serviço hello e chave de api do serviço de pesquisa do Azure
Todas as chamadas de API REST na pesquisa do Azure exigem que você forneça a URL do serviço hello e uma chave de api. 

1. Entrar toohello [Portal do Azure](https://portal.azure.com).
2. Na barra de salto hello, clique em **serviço de pesquisa** toolist todos os serviços de pesquisa do Azure Olá provisionados para sua assinatura.
3. Selecione serviço Olá toouse desejado.
4. No painel de serviço hello, você verá blocos para obter informações essenciais, bem como o ícone de chave Olá para acessar as chaves de administração de saudação.
   
      ![][3]
5. Copiar URL do serviço hello e uma chave de administração. Você precisará deles mais tarde, quando você adiciona toohello **config** arquivo.

## <a name="download-hello-sample-files"></a>Baixar arquivos de exemplo hello
1. Vá muito[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) no GitHub.
2. Clique em **baixar ZIP**, salvar toodisk de arquivo. zip hello e, em seguida, extraia todos os arquivos de saudação nele. Considere a possibilidade de extrair Olá arquivos em seu toomake de espaço de trabalho do Java-projeto mais fácil de saudação toofind mais tarde.
3. arquivos de exemplo Hello são somente leitura. Clique em Propriedades de pasta e atributo somente leitura de saudação limpar.

Todas as modificações de arquivos subsequentes e instruções de execução serão feitas nos arquivos nessa pasta.  

## <a name="import-project"></a>Projeto de importação
1. No Eclipse, escolha **Arquivo** > **Importar** > **Geral** > **Projetos Existentes no Espaço de Trabalho**.
   
    ![][4]
2. Em **diretório raiz selecione**, procurar pasta toohello que contém os arquivos de exemplo. Selecione a pasta de saudação que contém a pasta do hello. Project. projeto Olá deve aparecer em Olá **projetos** lista como um item selecionado.
   
    ![][12]
3. Clique em **Concluir**.
4. Use **Explorador de projeto** tooview e editar arquivos de saudação. Se ainda não estiver aberto, clique em **janela** > **exibição** > **Explorador de projeto** ou use Olá atalho tooopen-lo.

## <a name="configure-hello-service-url-and-api-key"></a>Configurar URL do serviço hello e chave de api
1. Em **Explorador de projeto**, clique duas vezes em **config** tooedit Olá configurações que contém o nome do servidor de saudação e a chave de api.
2. Consulte toohello etapas neste artigo, onde você encontrado Olá URL do serviço e a chave de api no hello [Portal do Azure](https://portal.azure.com), valores de saudação tooget agora será informado no **config**.
3. Em **config**, substitua "Chave de Api" hello-chave de api para o serviço. Em seguida, o nome do serviço (hello primeiro componente Olá URL http://servicename.search.windows.net) substitui o "nome do serviço" no hello mesmo arquivo.
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a>Configurar ambientes de projeto, compilação e tempo de execução de saudação
1. No Eclipse, no Explorador de projeto, clique com botão direito hello > **propriedades** > **facetas de projeto**.
2. Selecione **Módulo da Web dinâmico**, **Java** e **JavaScript**.
   
    ![][6]
3. Clique em **Aplicar**.
4. Selecione **Janela** > **Preferências** > **Servidor** > **Ambientes de tempo de execução** > **Adicionar..**.
5. Expanda o Apache e selecione a versão de saudação do servidor do Apache Tomcat Olá instalado anteriormente. Em nosso sistema, instalamos a versão 8.
   
    ![][7]
6. Na página seguinte do hello, especifique o diretório de instalação do Tomcat de saudação. Em um computador Windows, isso provavelmente será C:\Arquivos de Programas\Apache Software Foundation\Tomcat *versão*.
7. Clique em **Concluir**.
8. Selecione **Janela** > **Preferências** > **Java** > **JREs Instalados** > **Adicionar**.
9. Em **Adicionar JRE**, selecione **VM padrão**.
10. Clique em **Avançar**.
11. Na Definição do JRE, na página inicial do JRE, clique em **Diretório**.
12. Navegue muito**arquivos de programa** > **Java** e selecione Olá JDK instalado anteriormente. É importante tooselect Olá JDK como Olá JRE.
13. No JREs instalado, escolha Olá **JDK**. As configurações devem ter aparência semelhante toohello captura de tela a seguir.
    
    ![][9]
14. Opcionalmente, selecione **janela** > **navegador da Web** > **Internet Explorer** aplicativo hello de tooopen em uma janela de navegador externo. Usar um navegador externo oferece uma melhor experiência de aplicativo Web.
    
    ![][8]

Agora você concluiu as tarefas de configuração de saudação. Em seguida, compilar e executar o projeto de saudação.

## <a name="build-hello-project"></a>Compilar o projeto de saudação
1. No Explorador de projeto, clique o nome do projeto hello e escolha **executar como** > **build Maven...**  tooconfigure projeto de saudação.
   
    ![][10]
2. Em Editar configurações, em Metas, digite "instalação limpa" e, em seguida, clique em **Executar**.

Mensagens de status são a janela do console de toohello de saída. Você deve ver o projeto de saudação indicando êxito na compilação compilado sem erros.

## <a name="run-hello-app"></a>Executar o aplicativo hello
Nesta última etapa, você executará o aplicativo hello em um ambiente de tempo de execução do servidor local.

Se você ainda não especificou um ambiente de tempo de execução do servidor no Eclipse, você precisará toodo isso primeiro.

1. No Gerenciador de Projetos, expanda **WebContent**.
2. Clique com o botão direito do mouse em **Search.jsp** > **Executar como** > **Executar no Servidor**. Selecione o servidor do Apache Tomcat hello e, em seguida, clique em **executar**.

> [!TIP]
> Se você tiver usado um espaço de trabalho não padrão toostore seu projeto, você precisará toomodify **configuração executar** toopoint toohello projeto local tooavoid um erro de inicialização do servidor. No Gerenciador de Projetos, clique com o botão direito do mouse em **Search.jsp** > **Executar como** > **Configurações de Execução**. Selecione o servidor do Apache Tomcat Olá. Clique em **Argumentos**. Clique em **espaço de trabalho** ou **sistema de arquivos** tooset pasta de saudação que contém o projeto de saudação.
> 
> 

Quando você executa o aplicativo hello, você verá uma janela do navegador, fornecendo uma caixa de pesquisa para a inserção de termos.

Aguarde cerca de um minuto antes de clicar em **pesquisa** toogive Olá serviço tempo toocreate e carga Olá índice. Se você receber um erro HTTP 404, basta toowait mais um pouco antes de tentar novamente.

## <a name="search-on-usgs-data"></a>Pesquisar dados do USGS
conjunto de dados USGS Olá inclui registros que são relevante toohello estado de Rhode Island. Se você clicar em **pesquisa** em uma caixa de pesquisa vazia, você obterá as entradas de 50 principais hello, que é o padrão de saudação.

Inserindo um termo de pesquisa fornecerá o mecanismo de pesquisa Olá algo toogo sobre. Tente inserir um nome regional. "Roger Williams" era o administrador primeiro Olá de Rhode Island. Vários parques, edifícios e escolas receberam seus nomes em homenagem a ele.

![][11]

Você também pode tentar qualquer um destes termos:

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>Próximas etapas
Este é o hello primeiro tutorial de pesquisa do Azure com base em Java e hello USGS dataset. Ao longo do tempo, estenderemos esse tutorial toodemonstrate recursos adicionais de pesquisa convém toouse em suas soluções personalizadas.

Se você já tiver alguns em segundo plano na pesquisa do Azure, você pode usar este exemplo como um springboard experimentação adicional, aumentando talvez Olá [página Pesquisa](search-pagination-page-layout.md), ou a implementação de [navegação facetada](search-faceted-navigation.md). Você também pode melhorar após a página de resultados da pesquisa de saudação adicionando contagens e envio em lote documentos para que os usuários podem percorrer resultados hello.

TooAzure nova pesquisa? É recomendável tentar toodevelop outros tutoriais um entendimento de como você pode criar. Visite nosso [página de documentação](https://azure.microsoft.com/documentation/services/search/) toofind mais recursos. Você também pode exibir links Olá em nosso [vídeo e Tutorial lista](search-video-demo-tutorial-list.md) tooaccess obter mais informações.

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
