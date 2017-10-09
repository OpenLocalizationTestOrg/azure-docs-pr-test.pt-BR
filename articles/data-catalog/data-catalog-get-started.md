---
title: "aaaGet iniciado no catálogo de dados | Microsoft Docs"
description: "Tutorial de ponta a ponta apresentar cenários hello e recursos do catálogo de dados do Azure."
documentationcenter: 
services: data-catalog
author: steelanddata
manager: jhubbard
editor: 
tags: 
ms.assetid: 03332872-8d84-44a0-8a78-04fd30e14b18
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 7652918b5a8254f5cff9e32d77b1fd3e1bf59d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-catalog"></a>Introdução ao Catálogo de Dados do Azure
O Catálogo de Dados do Azure é um serviço de nuvem totalmente gerenciado que atua como um sistema de registro e sistema de descoberta em ativos de dados da empresa. Para obter uma visão detalhada, confira [O que é o Catálogo de Dados do Azure](data-catalog-what-is-data-catalog.md).

Este tutorial ajudará você a começar a usar o Catálogo de Dados do Azure. Execute o hello seguindo os procedimentos neste tutorial:

| Procedimento | Descrição |
|:--- |:--- |
| [Provisionar catálogo de dados](#provision-data-catalog) |Neste procedimento, você provisiona ou configura o Catálogo de Dados do Azure. Você executar esta etapa somente se o catálogo de saudação não foi configurado antes. Você só pode ter um catálogo de dados por organização (domínio do Microsoft Azure Active Directory), mesmo que haja várias assinaturas associadas à sua conta do Azure. |
| [Registrar ativos de dados](#register-data-assets) |Neste procedimento, você pode registrar ativos de dados do banco de dados do exemplo hello AdventureWorks2014 no catálogo de dados de saudação. Registro é o processo de saudação de extrair metadados estruturais chave como nomes, tipos e locais de fonte de dados de saudação e copiar esse catálogo de toohello de metadados. Olá fonte de dados e ativos de dados permanecem onde eles são, mas Olá metadados são usados pelo Olá catálogo toomake-las mais facilmente identificável e compreensível. |
| [Descobrir ativos de dados](#discover-data-assets) |Neste procedimento, você deve usar Olá Data Catalog do Azure portal toodiscover ativos de dados que foram registrados na etapa anterior hello. Depois de uma fonte de dados tiver sido registrada com o Data Catalog do Azure, seus metadados é indexado por serviço Olá para que os usuários podem pesquisar facilmente dados Olá necessários. |
| [Anotar ativos de dados](#annotate-data-assets) |Neste procedimento, você fornece anotações (informações como descrições, marcas, documentação ou os especialistas) para Olá ativos de dados. Essas informações complementam Olá metadados extraídos da fonte de dados de saudação e mais pessoas toomore compreensível da fonte de dados de saudação do toomake. |
| [Conecte-se ativos toodata](#connect-to-data-assets) |Neste procedimento, você abre os ativos de dados em ferramentas de cliente integradas, como Excel e ferramentas de dados do SQL Server, e em ferramentas não integradas (SQL Server Management Studio). |
| [Gerenciar ativos de dados](#manage-data-assets) |Neste procedimento, você define a segurança de seus ativos de dados. Catálogo de dados não dê aos usuários acesso toohello dados em si. proprietário Olá Olá da fonte de dados controla o acesso a dados. <br/><br/> Com o catálogo de dados, você pode descobrir fontes de dados e Olá exibição **metadados** relacionados fontes toohello registrados no catálogo de saudação. Pode haver situações, porém, onde as fontes de dados devem ser visível toospecific somente usuários ou toomembers de grupos específicos. Para esses cenários, você pode usar a propriedade do catálogo de dados tootake de ativos de dados registrados na visibilidade de Olá catálogo e controle de saudação de ativos de saudação que você possui. |
| [Remover ativos de dados](#remove-data-assets) |Neste procedimento, você aprenderá como ativos de dados tooremove de Olá catálogo de dados. |

## <a name="tutorial-prerequisites"></a>Pré-requisitos do tutorial
### <a name="azure-subscription"></a>Assinatura do Azure
tooset o catálogo de dados do Azure, você deve ser o proprietário de saudação ou coproprietário de uma assinatura do Azure.

As assinaturas do Azure ajudarão-lo a organizar os recursos de serviço acesso toocloud como Data Catalog do Azure. Eles também ajudam a controlar como o uso de recursos é reportado, cobrado e pago. Cada assinatura pode ter uma configuração diferente de cobrança e pagamento, assim você pode ter diferentes assinaturas e planos diferentes por departamento, projeto, escritório regional, etc. Cada serviço de nuvem pertence tooa assinatura, e você precisa toohave uma assinatura antes de configurar o catálogo de dados do Azure. mais, consulte toolearn [gerenciar contas, assinaturas e funções administrativas](../active-directory/active-directory-how-subscriptions-associated-directory.md).

Se você não tiver uma assinatura, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Confira [Avaliação Gratuita](https://azure.microsoft.com/pricing/free-trial/) para obter detalhes.

### <a name="azure-active-directory"></a>Azure Active Directory
tooset o catálogo de dados do Azure, você deve estar conectado com uma conta de usuário do Azure Active Directory (AD do Azure). Você deve ser o proprietário de saudação ou coproprietário de uma assinatura do Azure.  

O AD do Azure fornece uma maneira fácil para sua identidade de toomanage de negócios e acesso, tanto na nuvem hello e local. Você pode usar um único trabalho ou escola conta toosign na nuvem tooany ou aplicativo da web local. Catálogo de dados do Azure usa o AD do Azure tooauthenticate entrar. mais, consulte toolearn [o que é o Active Directory do Azure](../active-directory/active-directory-whatis.md).

### <a name="azure-active-directory-policy-configuration"></a>Configuração de política do Azure Active Directory
Você pode encontrar uma situação em que você pode entrar no portal do toohello Data Catalog do Azure, mas quando você tenta toosign na ferramenta de registro de fonte de dados toohello, encontrar uma mensagem de erro que impede que você entrar. Esse erro pode ocorrer quando você estiver usando a rede de empresa de saudação ou quando você está se conectando fora Olá rede da empresa.

ferramenta de registro de saudação usa *autenticação de formulários* toovalidate entradas do usuário no Active Directory do Azure. Para entrar com êxito, um administrador do Active Directory do Azure deve habilitar a autenticação de formulários em Olá *política de autenticação global*.

Com a política de autenticação global hello, você pode habilitar autenticação separadamente para conexões de intranet e extranet, conforme mostrado no Olá a imagem a seguir. Erros de entrada podem ocorrer se a autenticação de formulários não está habilitada para rede de saudação do qual você está se conectando.

 ![Política de Autenticação Global do AzureActive Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

Para saber mais, confira [Configurando políticas de autenticação](https://technet.microsoft.com/library/dn486781.aspx).

## <a name="provision-data-catalog"></a>Provisionar catálogo de dados
Você somente pode provisionar um catálogo de dados por organização (domínio do Azure Active Directory). Portanto, se o proprietário de saudação ou coproprietário de uma assinatura do Azure que pertence a toothis domínio do Active Directory do Azure já tiver criado um catálogo, não será capaz de toocreate um catálogo novamente mesmo se você tiver várias assinaturas do Azure. tootest se um catálogo de dados foi criado por um usuário em seu domínio do Active Directory do Azure, vá toohello [Data Catalog do Azure HomePage](http://azuredatacatalog.com) e verificar se você ver o catálogo de saudação. Se um catálogo já foi criado para você, ignore Olá seguindo o procedimento e ir toohello próxima seção.    

1. Vá toohello [página de serviço de catálogo de dados](https://azure.microsoft.com/services/data-catalog) e clique em **começar**.
   
    ![Catálogo de Dados do Azure – página inicial de marketing](media/data-catalog-get-started/data-catalog-marketing-landing-page.png)
2. Entrar com uma conta de usuário que é proprietário da saudação ou coproprietário de uma assinatura do Azure. Você verá Olá página a seguir depois de entrar.
   
    ![Catálogo de Dados do Azure – provisionar catálogo de dados](media/data-catalog-get-started/data-catalog-create-azure-data-catalog.png)
3. Especifique um **nome** para catálogo de dados de Olá Olá **assinatura** você deseja toouse e Olá **local** para o catálogo de saudação.
4. Expanda **Preço** e selecione uma **edição** (Gratuita ou Standard) do Catálogo de Dados do Azure.
    ![Catálogo de Dados do Azure – selecionar edição](media/data-catalog-get-started/data-catalog-create-catalog-select-edition.png)
5. Expanda **usuários catálogo** e clique em **adicionar** tooadd usuários do catálogo de dados de saudação. Você é adicionados automaticamente toothis grupo.
    ![Catálogo de Dados do Azure – usuários](media/data-catalog-get-started/data-catalog-add-catalog-user.png)
6. Expanda **catálogo administradores** e clique em **adicionar** tooadd outros administradores de catálogo de dados de saudação. Você é adicionados automaticamente toothis grupo.
    ![Catálogo de Dados do Azure – administradores](media/data-catalog-get-started/data-catalog-add-catalog-admins.png)
7. Clique em **criar catálogo** toocreate catálogo de dados Olá para sua organização. Consulte o hello home page do catálogo de dados Olá depois que ele é criado.
    ![Catálogo de Dados do Azure – criado](media/data-catalog-get-started/data-catalog-created.png)    

### <a name="find-a-data-catalog-in-hello-azure-portal"></a>Localizar um catálogo de dados em Olá portal do Azure
1. Em uma guia separada no navegador da web de saudação ou em uma janela de navegador da web separado, vá toohello [portal do Azure](https://portal.azure.com) e entrar no Olá a mesma conta que você toocreate usado Olá catálogo de dados na etapa anterior hello.
2. Selecione **Procurar** e clique em **Catálogo de Dados**.
   
    ![Catálogo de dados do Azure – procurar Azure](media/data-catalog-get-started/data-catalog-browse-azure-portal.png) ver dados saudação catálogo criado.
   
    ![Catálogo de Dados do Azure – exibir catálogo em lista](media/data-catalog-get-started/data-catalog-azure-portal-show-catalog.png)
3. Clique em catálogo Olá que você criou. Consulte Olá **catálogo de dados** folha no portal de saudação.
   
   ![Catálogo de Dados do Azure – folha no portal ](media/data-catalog-get-started/data-catalog-blade-azure-portal.png)
4. Você pode exibir as propriedades do catálogo de dados hello e atualizá-los. Por exemplo, clique em **preço** e alterar a edição de saudação.
   
    ![Catálogo de Dados do Azure – tipo de preço](media/data-catalog-get-started/data-catalog-change-pricing-tier.png)

### <a name="adventure-works-sample-database"></a>Banco de dados de exemplo do Adventure Works
Neste tutorial, você registrar ativos de dados (tabelas) do banco de dados de exemplo hello AdventureWorks2014 para Olá mecanismo de banco de dados do SQL Server, mas você pode usar qualquer fonte de dados com suporte, se você preferir toowork com dados que é familiar e relevantes tooyour função. Para obter uma lista das fontes de dados com suporte, confira [Fontes de dados com suporte](data-catalog-dsr.md).

### <a name="install-hello-adventure-works-2014-oltp-database"></a>Instalar o banco de dados do Adventure Works 2014 OLTP Olá
banco de dados do Adventure Works Olá oferece suporte a cenários de processamento de transações online padrão para um fabricante de bicicletas fictício (Adventure Works Cycles), que inclui os produtos, vendas e compras. Neste tutorial, você registra informações sobre produtos no Catálogo de Dados do Azure.

dados de exemplo da Adventure Works tooinstall hello:

1. Baixe [Adventure Works 2014 Full Database backup.zip](https://msftdbprodsamples.codeplex.com/downloads/get/880661) do CodePlex.
2. banco de dados do toorestore Olá em seu computador, siga as instruções de saudação em [restaurar um Backup de banco de dados usando o SQL Server Management Studio](http://msdn.microsoft.com/library/ms177429.aspx), ou seguindo estas etapas:
   1. Abra o SQL Server Management Studio e conecte-se toohello mecanismo de banco de dados do SQL Server.
   2. Clique com botão direito do mouse em **Bancos de Dados** e clique em **Restaurar Banco de Dados**.
   3. Em **restaurar banco de dados**, clique em Olá **dispositivo** opção **fonte** e clique em **procurar**.
   4. Em **Selecionar dispositivos de backup**, clique em **Adicionar**.
   5. Vá toohello pasta em que você tenha Olá **AdventureWorks2014.bak** arquivo, Olá Selecione arquivo e clique em **Okey** tooclose Olá **localizar arquivo de Backup** caixa de diálogo.
   6. Clique em **Okey** tooclose Olá **Selecione dispositivos de backup** caixa de diálogo.    
   7. Clique em **Okey** tooclose Olá **restaurar banco de dados** caixa de diálogo.

Agora você pode registrar os ativos de dados do banco de dados de exemplo Adventure Works hello usando o catálogo de dados do Azure.

## <a name="register-data-assets"></a>Registrar ativos de dados
Neste exercício, você pode usar ativos de dados Olá registro ferramenta tooregister do banco de dados do Adventure Works Olá com o catálogo de saudação. Registro é o processo de saudação de extrair metadados estruturais chave como nomes, tipos e locais Olá fonte de dados e ativos Olá contém e copiar esse catálogo de toohello de metadados. Olá fonte de dados e ativos de dados permanecem onde eles são, mas Olá metadados são usados pelo Olá catálogo toomake-las mais facilmente identificável e compreensível.

### <a name="register-a-data-source"></a>Registrar uma fonte de dados
1. Vá toohello [Data Catalog do Azure HomePage](http://azuredatacatalog.com) e clique em **publicar dados**.
   
   ![Catálogo de Dados do Azure – botão Publicar Dados](media/data-catalog-get-started/data-catalog-publish-data.png)
2. Clique em **Iniciar aplicativo** toodownload, a instalação e a ferramenta de registro de execução Olá em seu computador.
   
   ![Catálogo de Dados do Azure – botão Iniciar](media/data-catalog-get-started/data-catalog-launch-application.png)
3. Em Olá **bem-vindo** , clique em **entrar** e insira suas credenciais.     
   
    ![Catálogo de Dados do Azure – página inicial](media/data-catalog-get-started/data-catalog-welcome-dialog.png)
4. Em Olá **catálogo de dados do Microsoft Azure** , clique em **do SQL Server** e **próximo**.
   
    ![Catálogo de Dados do Azure – fontes de dados](media/data-catalog-get-started/data-catalog-data-sources.png)
5. Insira as propriedades de conexão do SQL Server Olá para **AdventureWorks2014** (consulte Olá exemplo a seguir) e clique em **conectar**.
   
   ![Catálogo de Dados do Azure – configurações de conexão do SQL Server](media/data-catalog-get-started/data-catalog-sql-server-connection.png)
6. Registre metadados de saudação do seu ativo de dados. Neste exemplo, você deve registrar **produção/produto** objetos do namespace de AdventureWorks produção de hello:
   
   1. Em Olá **hierarquia servidor** de árvore, expanda **AdventureWorks2014** e clique em **produção**.
   2. Selecione **Product**, **ProductCategory**, **ProductDescription** e **ProductPhoto** usando Ctrl+clique.
   3. Clique em Olá **mover seta selecionado** (**>**). Essa ação move todos os objetos selecionados para Olá **toobe objetos registrado** lista.
      
      ![Tutorial do Catálogo de Dados do Azure – procurar e selecionar objetos](media/data-catalog-get-started/data-catalog-server-hierarchy.png)
   4. Selecione **incluir uma visualização** tooinclude uma visualização de instantâneo de dados de saudação. instantâneo Olá inclui too20 registros de cada tabela, e ele é copiado para o catálogo de saudação.
   5. Selecione **incluir dados de perfil** tooinclude um instantâneo de estatísticas do objeto Olá para o perfil de dados hello (por exemplo: os valores mínimos, máximo e médios para uma coluna, o número de linhas).
   6. Em Olá **adicionar marcas** , digite **adventure funciona, ciclos**. Essa ação adiciona marcas de pesquisa para esses ativos de dados. Marcas são uma ótima maneira toohelp usuários encontram uma fonte de dados registrado.
   7. Especificar nome de saudação de um **especialista** esses dados (opcional).
      
      ![Tutorial de catálogo de dados do Azure – objetos toobe registrado](media/data-catalog-get-started/data-catalog-objects-register.png)
   8. Clique em **REGISTRAR**. O Catálogo de Dados do Azure registra os objetos selecionados. Neste exercício, objetos de saudação selecionado da Adventure Works são registrados. ferramenta de registro de saudação extrai metadados de ativo de dados hello e copia esses dados no serviço de catálogo de dados do Azure hello. Olá dados permanecem em que ela reside atualmente e permanece em controle de saudação de administradores de saudação e políticas do sistema atual hello.
      
      ![Catálogo de Dados do Azure – objetos registrados](media/data-catalog-get-started/data-catalog-registered-objects.png)
   9. toosee seus objetos de fonte de dados registrado, clique **exibição Portal**. No portal do catálogo de dados do Azure hello, confirme se todas as quatro tabelas e banco de dados de saudação na exibição de grade de saudação.
      
      ![Objetos no portal do catálogo de dados do Azure Olá ](media/data-catalog-get-started/data-catalog-view-portal.png)

Neste exercício, você registrou objetos do banco de dados de exemplo Adventure Works Olá para que eles podem ser facilmente descobertos por usuários da sua organização. Olá exercício, você aprenderá como toodiscover registrado ativos de dados.

## <a name="discover-data-assets"></a>Descobrir ativos de dados
A descoberta no Catálogo de Dados do Azure usa dois mecanismos principais: pesquisa e filtragem.

A pesquisa é projetado toobe intuitiva e eficiente. Por padrão, os termos de pesquisa são comparados com qualquer propriedade no catálogo hello, incluindo anotações fornecido pelo usuário.

A filtragem é projetada toocomplement pesquisa. Você pode selecionar as características específicas como especialistas, o tipo de fonte de dados, o tipo de objeto e marcas tooview correspondência ativos de dados e pesquisa tooconstrain resulta toomatching ativos.

Usando uma combinação de pesquisa e filtragem, você pode navegar rapidamente as fontes de dados de saudação que foram registradas com ativos de dados do Data Catalog do Azure toodiscover Olá que é necessário.

Neste exercício, é usar os ativos de dados do hello Data Catalog do Azure portal toodiscover registrado no exercício anterior Olá. Confira [Referência de sintaxe de pesquisa do catálogo de dados](https://msdn.microsoft.com/library/azure/mt267594.aspx) para obter detalhes sobre a sintaxe de pesquisa.

A seguir estão alguns exemplos para descobrir ativos de dados no catálogo de saudação.  

### <a name="discover-data-assets-with-basic-search"></a>Descobrir ativos de dados com a pesquisa básica
A pesquisa básica ajuda você a procurar um catálogo usando um ou mais termos de pesquisa. Os resultados são qualquer ativos que correspondem a qualquer propriedade com um ou mais termos Olá especificados.

1. Clique em **início** no portal do hello Data Catalog do Azure. Se você fechou o navegador da web de hello, vá toohello [Data Catalog do Azure HomePage](https://www.azuredatacatalog.com).
2. Na caixa de pesquisa hello, digite `cycles` e pressione **ENTER**.
   
    ![Catálogo de Dados do Azure – pesquisa de texto básica](media/data-catalog-get-started/data-catalog-basic-text-search.png)
3. Confirme se todas as quatro tabelas e do banco de dados do hello (AdventureWorks2014) nos resultados da saudação. Você pode alternar entre **exibição de grade** e **exibição de lista** clicando nos botões na barra de ferramentas Olá conforme Olá a imagem a seguir. Observe que essa palavra-chave de pesquisa Olá é realçado em resultados da pesquisa Olá porque Olá **realçar** opção é **ON**. Você também pode especificar o número de saudação do **resultados por página** nos resultados da pesquisa.
   
    ![Catálogo de Dados do Azure – resultados da pesquisa de texto básica](media/data-catalog-get-started/data-catalog-basic-text-search-results.png)
   
    Olá **pesquisas** painel está na saudação à esquerda e hello **propriedades** painel está na saudação à direita. Em Olá **pesquisas** painel, você pode alterar os critérios de pesquisa e filtrar resultados. Olá **propriedades** painel exibe as propriedades de um objeto selecionado na grade de saudação ou lista.
4. Clique em **produto** nos resultados da pesquisa hello. Clique em Olá **visualização**, **colunas**, **perfil de dados**, e **documentação** guias, ou clique em painel inferior do hello seta tooexpand hello.  
   
    ![Catálogo de Dados do Azure – painel inferior](media/data-catalog-get-started/data-catalog-data-asset-preview.png)
   
    Em Olá **visualização** guia, você verá uma visualização de dados Olá Olá **produto** tabela.  
5. Clique em Olá **colunas** guia toofind detalhes sobre as colunas (como **nome** e **tipo de dados**) no ativo de dados hello.
6. Clique em Olá **perfil de dados** guia toosee Olá criação de perfil de dados (por exemplo: número de linhas, o tamanho de dados ou o valor mínimo em uma coluna) no ativo de dados hello.
7. Filtrar resultados de saudação usando **filtros** Olá esquerda. Por exemplo, clique em **tabela** para **tipo de objeto**, e você ver apenas tabelas Olá quatro, Olá não o banco de dados.
   
    ![Catálogo de Dados do Azure – filtrar resultados da pesquisa](media/data-catalog-get-started/data-catalog-filter-search-results.png)

### <a name="discover-data-assets-with-property-scoping"></a>Descobrir ativos de dados com escopo de propriedade
Propriedade escopo ajuda a que descobrir ativos de dados onde o termo de pesquisa de saudação é correspondido com hello especificada propriedade.

1. Olá limpar **tabela** filtrar em **tipo de objeto** na **filtros**.  
2. Na caixa de pesquisa hello, digite `tags:cycles` e pressione **ENTER**. Consulte [referência de sintaxe de pesquisa de catálogo de dados](https://msdn.microsoft.com/library/azure/mt267594.aspx) para todos os Olá propriedades que você pode usar para pesquisar o catálogo de dados de saudação.
3. Confirme se todas as quatro tabelas e do banco de dados do hello (AdventureWorks2014) nos resultados da saudação.  
   
    ![Catálogo de Dados – resultados da pesquisa de escopo de propriedade](media/data-catalog-get-started/data-catalog-property-scoping-results.png)

### <a name="save-hello-search"></a>Salvar pesquisa Olá
1. Em Olá **pesquisas** painel Olá **pesquisa atual** seção, insira um nome para pesquisa de saudação e clique em **salvar**.
   
    ![Catálogo de dados do Azure – salvar pesquisa](media/data-catalog-get-started/data-catalog-save-search.png)
2. Confirme que a pesquisa salvada de saudação é mostrado em **pesquisas salvas**.
   
    ![Catálogo de Dados do Azure – pesquisas salvas](media/data-catalog-get-started/data-catalog-saved-search.png)
3. Selecione uma saudação ações na pesquisa de saudação salvada (**Renomear**, **excluir**, **Salvar como padrão** pesquisa).
   
    ![Catálogo de Dados do Azure – opções de pesquisa salvas](media/data-catalog-get-started/data-catalog-saved-search-options.png)

### <a name="boolean-operators"></a>Operadores boolianos
Você pode ampliar ou restringir sua pesquisa com operadores boolianos.

1. Na caixa de pesquisa hello, digite `tags:cycles AND objectType:table`e pressione **ENTER**.
2. Confirme que você vê somente tabelas (não banco de dados Olá) nos resultados de saudação.  
   
    ![Catálogo de Dados do Azure – operador booliano na pesquisa](media/data-catalog-get-started/data-catalog-search-boolean-operator.png)

### <a name="grouping-with-parentheses"></a>Agrupando com parênteses
Agrupando com parênteses, você pode agrupar partes de saudação consulta tooachieve isolamento lógico, especialmente com operadores boolianos.

1. Na caixa de pesquisa hello, digite `name:product AND (tags:cycles AND objectType:table)` e pressione **ENTER**.
2. Confirme que você vê apenas Olá **produto** tabela nos resultados da pesquisa hello.
   
    ![Catálogo de dados do Azure – agrupando pesquisa](media/data-catalog-get-started/data-catalog-grouping-search.png)   

### <a name="comparison-operators"></a>Operadores de comparação
Com operadores de comparação, você pode usar comparações que não sejam de igualdade para propriedades que tenham tipos de dados numéricos e de data.

1. Na caixa de pesquisa hello, digite `lastRegisteredTime:>"06/09/2016"`.
2. Olá limpar **tabela** filtrar em **tipo de objeto**.
3. Pressione **ENTER**.
4. Confirme que você vê Olá **produto**, **ProductCategory**, **ProductDescription**, e **ProductPhoto** tabelas e hello Banco de dados AdventureWorks2014 registrados nos resultados da pesquisa.
   
    ![Catálogo de Dados do Azure – resultados da pequisa de comparação](media/data-catalog-get-started/data-catalog-comparison-operator-results.png)

Consulte [como ativos de dados toodiscover](data-catalog-how-to-discover.md) para obter informações detalhadas sobre a descoberta de ativos de dados e [referência de sintaxe de pesquisa de catálogo de dados](https://msdn.microsoft.com/library/azure/mt267594.aspx) para obter a sintaxe de pesquisa.

## <a name="annotate-data-assets"></a>Anotar ativos de dados
Neste exercício, você usar Olá Data Catalog do Azure portal tooannotate (Adicionar informações como descrições, marcas ou especialistas) ativos de dados que você registrou anteriormente no catálogo de saudação. anotações de saudação complementam e aprimorar Olá metadados estruturais extraídos da fonte de dados Olá durante o registro e torna os ativos de dados Olá toodiscover muito mais fácil e entenderem.

Neste exercício, você anota um ativo de dados único (ProductPhoto). Você adiciona um nome amigável e o ativo de dados descrição toohello ProductPhoto.  

1. Vá toohello [Data Catalog do Azure HomePage](https://www.azuredatacatalog.com) e de pesquisa com `tags:cycles` ativos de dados Olá toofind você registrou.  
2. Clique em **ProductPhoto** nos resultados da pesquisa.  
3. Digite **imagens de produto** para **nome amigável** e **fotos de produtos para material de marketing** para Olá **descrição**.
   
    ![Catálogo de Dados do Azure – descrição de ProductPhoto](media/data-catalog-get-started/data-catalog-productphoto-description.png)
   
    Olá **descrição** outros ajuda a descobrir e entender por que e como toouse Olá selecionado ativo de dados. Você também pode adicionar mais marcas e exibir colunas. Agora você pode tentar ativos de dados de pesquisa e filtragem toodiscover usando metadados descritivos Olá adicionou toohello catálogo.

Você também pode fazer Olá nesta página a seguir:

* Adicione especialistas para ativos de dados hello. Clique em **adicionar** em Olá **especialistas** área.
* Adicione marcas no nível de conjunto de dados de saudação. Clique em **adicionar** em Olá **marcas** área. Uma marca pode ser uma marca de usuário ou de glossário. Olá edição Standard do catálogo de dados inclui um glossário de negócios que ajuda os administradores do catálogo definem uma taxonomia de central de negócios. Os usuários do catálogo podem anotar os ativos de dados com os termos do glossário. Para obter mais informações, consulte [como tooset backup Olá Glossário de negócios para marcação controlado](data-catalog-how-to-business-glossary.md)
* Adicione marcas no nível de coluna hello. Clique em **adicionar** em **marcas** coluna Olá deseja tooannotate.
* Adicione descrição no nível de coluna hello. Digite a **Descrição** para uma coluna. Você também pode exibir metadados de descrição Olá extraídos da fonte de dados de saudação.
* Adicionar **solicitar acesso** informações que mostra aos usuários como toorequest acessar toohello dados ativos.
  
    ![Catálogo de Dados do Azure – adicionar marcas, descrições](media/data-catalog-get-started/data-catalog-add-tags-experts-descriptions.png)
* Escolha Olá **documentação** guia e fornecer a documentação para o ativo de dados hello. Com a documentação do Data Catalog do Azure, você pode usar o catálogo de dados como um repositório de conteúdo de toocreate uma narrativa completa de seus ativos de dados.
  
    ![Catálogo de Dados do Azure – guia Documentação](media/data-catalog-get-started/data-catalog-documentation.png)

Você também pode adicionar os ativos de dados de toomultiple uma anotação. Por exemplo, você pode selecionar todos os ativos de dados Olá registrado e especifique um especialista para eles.

![Catálogo de Dados do Azure – anotar vários ativos de dados](media/data-catalog-get-started/data-catalog-multi-select-annotate.png)

Catálogo de dados do Azure oferece suporte a um tooannotations de abordagem de fornecimento do público. Qualquer usuário do catálogo de dados pode adicionar marcas (usuário ou Glossário), descrições e outros metadados, para que qualquer usuário com uma perspectiva de um ativo de dados e seu uso pode ter essa perspectiva capturados e usuários tooother disponíveis.

Consulte [como ativos de dados tooannotate](data-catalog-how-to-annotate.md) para obter informações detalhadas sobre como anotar os ativos de dados.

## <a name="connect-toodata-assets"></a>Conecte-se ativos toodata
Neste exercício, você abre os ativos de dados em uma ferramenta de cliente integrada (Excel) e em uma ferramenta não integrada (SQL Server Management Studio) usando informações de conexão.

> [!NOTE]
> É importante tooremember Data Catalog do Azure não fornece acesso a fonte de dados real toohello — simplesmente torna mais fácil para você toodiscover e compreendê-la. Quando você se conectar a fonte de dados tooa, Olá aplicativo cliente que você escolher usa credenciais de janelas ou solicita as credenciais conforme necessário. Se você não anteriormente recebeu fonte de dados do access toohello, será necessário toobe acesso antes de conectar.
> 
> 

### <a name="connect-tooa-data-asset-from-excel"></a>Conecte-se tooa ativo de dados do Excel
1. Selecione **Produto** nos resultados da pesquisa. Clique em **abrir em** na barra de ferramentas hello e clique em **Excel**.
   
    ![Catálogo de dados do Azure – conectar toodata ativo](media/data-catalog-get-started/data-catalog-connect1.png)
2. Clique em **abrir** na janela pop-up de download de saudação. Essa experiência pode variar dependendo do navegador de saudação.
   
    ![Catálogo de Dados do Azure – arquivo de conexão do Excel baixado](media/data-catalog-get-started/data-catalog-download-open.png)
3. Em Olá **aviso de segurança do Microsoft Excel** janela, clique em **habilitar**.
   
    ![Catálogo de Dados do Azure – pop-up de segurança do Excel](media/data-catalog-get-started/data-catalog-excel-security-popup.png)
4. Lembre-Olá Olá padrões **importar dados** caixa de diálogo e clique em **Okey**.
   
    ![Catálogo de Dados do Azure – importar dados do Excel](media/data-catalog-get-started/data-catalog-excel-import-data.png)
5. Exibir a fonte de dados do hello no Excel.
   
    ![Catálogo de Dados do Azure – tabela de produto no Excel](media/data-catalog-get-started/data-catalog-connect2.png)

Neste exercício, você conectado toodata ativos descobertos usando o catálogo de dados do Azure. Com o portal do catálogo de dados do Azure hello, você pode se conectar diretamente por meio de aplicativos de cliente Olá integrados Olá **aberto no** menu. Você também pode se conectar com qualquer aplicativo que desejar usando as informações de local de conexão Olá incluídas nos metadados de ativo de saudação. Por exemplo, você pode usar dados do SQL Server Management Studio tooconnect toohello AdventureWorks2014 banco de dados tooaccess saudação em ativos de dados Olá registrados neste tutorial.

1. Abra o **SQL Server Management Studio**.
2. Em Olá **conectar tooServer** caixa de diálogo, digite o nome do servidor de saudação do hello **propriedades** painel no portal do hello Data Catalog do Azure.
3. Use o ativo de dados credenciais tooaccess hello e autenticação apropriadas. Se você não tiver acesso, use informações Olá **solicitar acesso** campo tooget-lo.
   
    ![Catálogo de Dados do Azure – solicitar acesso](media/data-catalog-get-started/data-catalog-request-access.png)

Clique em **exibir cadeias de Conexão** tooview e cópia ADF.NET, ODBC e OLEDB conexão cadeias de caracteres toohello área de transferência para uso em seu aplicativo.

## <a name="manage-data-assets"></a>Gerenciar ativos de dados
Nesta etapa, você deve ver como tooset a segurança de seus ativos de dados. Catálogo de dados não dê aos usuários acesso toohello dados em si. proprietário Olá Olá da fonte de dados controla o acesso a dados.

Você pode usar o catálogo de dados toodiscover fontes de dados e metadados de saudação tooview relacionados fontes toohello registrados no catálogo de saudação. Pode haver situações, porém, em que fontes de dados só devem ser visível toospecific usuários ou toomembers de grupos específicos. Para esses cenários, você pode usar a propriedade de tootake do catálogo de dados de ativos de dados registrados no catálogo hello e toothen controlar a visibilidade de saudação de ativos de saudação que você possui.

> [!NOTE]
> recursos de gerenciamento de saudação descritos neste exercício estão disponíveis apenas em Olá Standard Edition do Data Catalog do Azure, não em Olá edição gratuita.
> No catálogo de dados do Azure, apropriar-se de ativos de dados, adicione os coproprietários toodata ativos e definir a visibilidade de saudação de ativos de dados.
> 
> 

### <a name="take-ownership-of-data-assets-and-restrict-visibility"></a>Apropriar-se dos ativos de dados e restringir a visibilidade
1. Vá toohello [Data Catalog do Azure HomePage](https://www.azuredatacatalog.com). Em Olá **pesquisa** texto, digite `tags:cycles` e pressione **ENTER**.
2. Clique em um item na lista de resultados de saudação e clique em **Take Ownership** na barra de ferramentas de saudação.
3. Em Olá **gerenciamento** seção Olá **propriedades** do painel, clique em **Take Ownership**.
   
    ![Catálogo de Dados do Azure – apropriar-se](media/data-catalog-get-started/data-catalog-take-ownership.png)
4. visibilidade de toorestrict, escolha **proprietários & esses usuários** em Olá **visibilidade** seção e clique em **adicionar**. Insira endereços de email do usuário na caixa de texto de saudação e pressione **ENTER**.
   
    ![Catálogo de Dados do Azure – restringir acesso](media/data-catalog-get-started/data-catalog-ownership.png)

## <a name="remove-data-assets"></a>Remover ativos de dados
Neste exercício, você use Olá dados de visualização do catálogo de dados do Azure portal tooremove ativos de dados registrado e excluir ativos de dados do catálogo de saudação.

No Catálogo de Dados do Azure, você pode eliminar um ativo individual ou excluir vários ativos.

1. Vá toohello [Data Catalog do Azure HomePage](https://www.azuredatacatalog.com).
2. Em Olá **pesquisa** texto, digite `tags:cycles` e clique em **ENTER**.
3. Selecione um item na lista de resultados de saudação e clique em **excluir** na barra de ferramentas Olá conforme Olá a imagem a seguir:
   
    ![Catálogo de Dados do Azure – excluir o item de grade](media/data-catalog-get-started/data-catalog-delete-grid-item.png)
   
    Se você estiver usando o modo de exibição de lista Olá, Olá caixa de seleção é toohello esquerda do item de saudação conforme Olá a imagem a seguir:
   
    ![Catálogo de Dados do Azure – excluir o item de lista](media/data-catalog-get-started/data-catalog-delete-list-item.png)
   
    Você também pode selecionar vários ativos de dados e excluí-los, conforme mostrado no Olá a imagem a seguir:
   
    ![Catálogo de Dados do Azure – excluir vários ativos de dados](media/data-catalog-get-started/data-catalog-delete-assets.png)

> [!NOTE]
> Olá o comportamento padrão do catálogo de saudação é tooallow tooregister qualquer usuário qualquer fonte de dados e tooallow toodelete qualquer usuário qualquer ativo de dados que foi registrado. recursos de gerenciamento de saudação incluídos no hello Standard Edition do Data Catalog do Azure fornecem opções adicionais para assumir a propriedade de ativos, restringir quem pode descobrir ativos e restringir quem pode excluir ativos.
> 
> 

## <a name="summary"></a>Resumo
Neste tutorial, você explorou recursos essenciais do Catálogo de Dados do Azure, incluindo o registro, a anotação, a descoberta e o gerenciamento de ativos de dados corporativos. Agora que você concluiu o tutorial Olá, é hora de tooget iniciado. Você pode começar hoje registrando você e sua equipe dependem de fontes de dados hello e convidar o catálogo de saudação toouse colegas.

## <a name="references"></a>Referências
* [Como os ativos de dados tooregister](data-catalog-how-to-register.md)
* [Como os ativos de dados toodiscover](data-catalog-how-to-discover.md)
* [Como os ativos de dados tooannotate](data-catalog-how-to-annotate.md)
* [Como os ativos de dados toodocument](data-catalog-how-to-documentation.md)
* [Como tooconnect toodata ativos](data-catalog-how-to-connect.md)
* [Como os ativos de dados toomanage](data-catalog-how-to-manage.md)

