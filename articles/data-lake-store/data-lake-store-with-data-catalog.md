---
title: "dados de aaaRegister do repositório Data Lake no catálogo de dados do Azure | Microsoft Docs"
description: "Registrar dados do Repositório Data Lake no Catálogo de Dados do Azure"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3294d91e-a723-41b5-9eca-ace0ee408a4b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3e895b42cab4ba39d288950763312a243883cbdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-from-data-lake-store-in-azure-data-catalog"></a>Registrar dados do Repositório Data Lake no Catálogo de Dados do Azure
Neste artigo, você aprenderá como toointegrate do Azure Data Lake armazenar com Data Catalog do Azure toomake dados detectáveis dentro de uma organização pela integração com o catálogo de dados. Para obter mais informações sobre a catalogação de dados, consulte [Catálogo de Dados do Azure](../data-catalog/data-catalog-what-is-data-catalog.md). toounderstand cenários em que você pode usar o catálogo de dados, consulte [cenários comuns do Data Catalog do Azure](../data-catalog/data-catalog-common-scenarios.md).

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Habilite sua assinatura do Azure** para a Public Preview do Data Lake Store. Veja [instruções](data-lake-store-get-started-portal.md).
* **Conta do Repositório Azure Data Lake**. Siga as instruções de saudação em [Introdução ao repositório Azure Data Lake usando hello Azure Portal](data-lake-store-get-started-portal.md). Para este tutorial, vamos criar uma conta do Repositório Data Lake chamada **datacatalogstore**.

    Depois de criar conta hello, carregue um tooit de conjunto de dados de exemplo. Para este tutorial, vamos carregar todos os arquivos. csv de saudação em hello **AmbulanceData** pasta Olá [repositório Git do Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/). Você pode usar vários clientes, como [Azure Storage Explorer](http://storageexplorer.com/), contêiner de blob de tooa tooupload dados.
* **Catálogo de Dados do Azure**. Sua organização já deve ter um Catálogo de Dados do Azure criados para sua organização. É permitido somente um catálogo para cada organização.

## <a name="register-data-lake-store-as-a-source-for-data-catalog"></a>Registre o Repositório Data Lake como uma fonte do Catálogo de Dados

> [!VIDEO https://channel9.msdn.com/Series/AzureDataLake/ADCwithADL/player]

1. Vá muito`https://azure.microsoft.com/services/data-catalog`e clique em **começar**.
2. Faça logon no portal do catálogo de dados do Azure hello e, em seguida, clique em **publicar dados**.

    ![Registrar uma fonte de dados](./media/data-lake-store-with-data-catalog/register-data-source.png "Registrar uma fonte de dados")
3. Na próxima página do hello, clique em **Iniciar aplicativo**. Isso baixará o arquivo de manifesto de aplicativo hello em seu computador. Clique duas vezes no aplicativo de saudação de toostart hello arquivo de manifesto.
4. Na página de boas-vindas hello, clique em **entrar**e insira suas credenciais.

    ![Tela de boas-vindas](./media/data-lake-store-with-data-catalog/welcome.screen.png "Tela de boas-vindas")
5. Em Olá selecionar uma página de fonte de dados, selecione **Azure Data Lake**e, em seguida, clique em **próximo**.

    ![Selecionar fonte de dados](./media/data-lake-store-with-data-catalog/select-source.png "Selecionar fonte de dados")
6. Na página seguinte do hello, fornece Olá nome de conta do repositório Data Lake que você deseja tooregister no catálogo de dados. Deixe Olá outras opções como padrão e, em seguida, clique em **conectar**.

    ![Conectar toodata fonte](./media/data-lake-store-with-data-catalog/connect-to-source.png "conectar toodata fonte")
7. próxima página de saudação pode ser dividida em Olá segmentos a seguir.

    a. Olá **Server hierarquia** caixa representa a estrutura de pastas de conta de repositório Data Lake hello. **$Root** representa Olá raiz de conta do repositório Data Lake, e **AmbulanceData** representa Olá pasta criada na raiz de saudação da saudação conta do repositório Data Lake.

    b. Olá **objetos disponíveis** caixa de lista arquivos hello e pastas em Olá **AmbulanceData** pasta.

    c. **Objetos toobe registrado caixa** listas Olá arquivos e pastas que você deseja tooregister no catálogo de dados do Azure.

    ![Exibir a estrutura de dados](./media/data-lake-store-with-data-catalog/view-data-structure.png "Exibir a estrutura de dados")
8. Para este tutorial, você deve registrar todos os arquivos de saudação no diretório de saudação. Para fazer isso, clique em hello (![mover objetos](./media/data-lake-store-with-data-catalog/move-objects.png "mover objetos")) toomove botão Olá a todos os demais arquivos**toobe objetos registrado** caixa.

    Como dados saudação serão registrados em um catálogo de dados em toda a organização, é um recomendados abordagem tooadd alguns metadados que você pode usar mais tarde tooquickly localizar dados saudação. Por exemplo, você pode adicionar um endereço de email para o proprietário dos dados hello (por exemplo, um que está carregando dados saudação) ou adicionar uma marca tooidentify Olá de dados. captura de tela de saudação abaixo mostra uma marca que adicionamos toohello dados.

    ![Exibir a estrutura de dados](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "Exibir a estrutura de dados")

    Clique em **Registrar**.
9. Olá captura de tela a seguir indica que dados saudação são registrados com êxito no hello catálogo de dados.

    ![Registro concluído](./media/data-lake-store-with-data-catalog/registration-complete.png "Exibir a estrutura de dados")
10. Clique em **exibição Portal** toogo fazer toohello portal do catálogo de dados e verifique se que você pode agora Olá acesso registrados dados do portal de saudação. dados de saudação toosearch, você pode usar marca Olá usado durante o registro de dados de saudação.

     ![Pesquisar dados no catálogo](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "Pesquisar dados no catálogo")
11. Agora você pode executar operações como a adição de anotações e dados de toohello documentação. Para obter mais informações, consulte Olá links a seguir.

    * [Anotar fontes de dados no Catálogo de Dados](../data-catalog/data-catalog-how-to-annotate.md)
    * [Documentar fontes de dados no Catálogo de Dados](../data-catalog/data-catalog-how-to-documentation.md)

## <a name="see-also"></a>Confira também
* [Anotar fontes de dados no Catálogo de Dados](../data-catalog/data-catalog-how-to-annotate.md)
* [Documentar fontes de dados no Catálogo de Dados](../data-catalog/data-catalog-how-to-documentation.md)
* [Integrar o Repositório Data Lake a outros serviços do Azure](data-lake-store-integrate-with-other-services.md)
