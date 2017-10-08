---
title: "Introdução de aaaUse tooget portal do Azure ao repositório Data Lake | Microsoft Docs"
description: "Use Olá toocreate portal do Azure uma conta do repositório Data Lake e executar operações básicas em Olá repositório Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: fea324d0-ad1a-4150-81f0-8682ddb4591c
ms.service: data-lake-store
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/06/2017
ms.author: nitinme
ms.openlocfilehash: 6bb3413f00bfa4393f08aed18bc1d5f8a2f28fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-hello-azure-portal"></a>Introdução ao repositório Azure Data Lake usando Olá portal do Azure
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [SDK .NET](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [CLI 2.0 do Azure](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Saiba como toouse Olá toocreate portal do Azure uma conta do repositório Azure Data Lake e executar operações básicas de como criar pastas, carregar e baixar arquivos de dados, exclua sua conta, etc. Para obter mais informações, consulte [Visão geral do Azure Data Lake Store](data-lake-store-overview.md).

Olá dois vídeos a seguir contêm Olá as mesmas informações conforme descrito neste artigo:

* [Criar uma conta do Repositório Data Lake](https://mix.office.com/watch/1k1cycy4l4gen)
* [Gerenciar dados no repositório Data Lake usando Olá Explorador de dados](https://mix.office.com/watch/icletrxrh6pc)

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deve ter Olá itens a seguir:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-an-azure-data-lake-store-account"></a>Criar uma conta do Repositório Azure Data Lake

1. Logon toohello novo [portal do Azure](https://portal.azure.com).
2. Clique em **NOVO**, clique em **Dados + Armazenamento** e clique em **Azure Data Lake Store**. Ler informações de Olá Olá **repositório Azure Data Lake** folha e depois clique em **criar** na Olá inferior esquerda da folha de saudação.
3. Em Olá **novo repositório do Data Lake** folha, forneça os valores hello, conforme mostrado na Olá captura de tela a seguir:
   
    ![Criar uma nova conta do Azure Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.New.Account.png "Criar uma nova conta do Azure Data Lake Store")
   
   * **Nome**. Insira um nome exclusivo para Olá conta do repositório Data Lake.
   * **Assinatura**. Selecione a assinatura Olá sob a qual você deseja toocreate uma nova conta do repositório Data Lake.
   * **Grupo de Recursos**. Selecione um grupo de recursos existente ou selecione Olá **criar novo** toocreate opção um. Um grupo de recursos é um contêiner que mantém os recursos relacionados para um aplicativo. Para saber mais, consulte [Grupos de Recursos no Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).
   * **Local**: selecione um local onde deseja que a conta de repositório Data Lake toocreate hello.
   * **Configurações de Criptografia**. Há três opções:
     
     * **Não habilite a criptografia**.
     * **Use chaves gerenciadas pelo Azure Data Lake**.  Se você quiser repositório Azure Data Lake toomanage suas chaves de criptografia.
     * **Escolha as chaves no Azure Key Vault**. Você pode selecionar um Azure Key Vault existente ou criar um novo Key Vault. chaves de saudação toouse de um cofre de chave, você deve atribuir permissões para Olá conta do repositório Azure Data Lake tooaccess hello Azure Key Vault. Para obter instruções hello, consulte [atribuir permissões tooAzure Cofre de chaves](#assign-permissions-to-azure-key-vault).
       
        ![Criptografia do Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-2.png "Criptografia do Data Lake Store")
       
        Clique em **Okey** em Olá **configurações de criptografia** folha.

        Para obter mais informações, consulte [Criptografia dos dados no Azure Data Lake Store](./data-lake-store-encryption.md).

4. Clique em **Criar**. Se você escolher o painel da toohello toopin Olá conta, é exibida novamente o painel de toohello e você pode ver o progresso de saudação do seu provisionamento de conta do repositório Data Lake. Uma vez Olá conta do repositório Data Lake é provisionado, folha de conta Olá aparece.

Você também pode criar uma conta do Data Lake Store usando modelos do Azure Resource Manager. Esses modelos são acessíveis nos [Modelos de Início Rápido do Azure](https://azure.microsoft.com/resources/templates/?term=data+lake+store):

- Sem criptografia de dados: [Implantar conta do Azure Data Lake Store sem criptografia de dados](https://azure.microsoft.com/en-us/resources/templates/101-data-lake-store-no-encryption/).
- Com criptografia de dados usando o Data Lake Store: [Implantar conta do Data Lake Store com criptografia (Data Lake)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-adls/).
- Com criptografia de dados usando o Azure Key Vault: [Implantar conta do Data Lake Store com criptografia (Key Vault)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-key-vault/).

### <a name="assign-permissions-to-azure-key-vault"></a>Atribuir permissões tooAzure Cofre de chaves
Se você usou as chaves de criptografia de tooconfigure um cofre de chaves do Azure na conta do repositório Data Lake do hello, configure o acesso entre contas de repositório Data Lake hello e hello Azure Key Vault. Execute Olá toodo as etapas a seguir assim.

1. Se você usou as chaves da saudação Cofre de chaves do Azure, folha Olá para Olá conta do repositório Data Lake exibirá um aviso na parte superior da saudação. Clique em Olá Olá de tooopen aviso **configurar permissões de Cofre de chave** folha.
   
    ![Criptografia do Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-3.png "Criptografia do Data Lake Store")
2. folha de saudação mostra duas opções tooconfigure acesso.
   
   * Opção de primeira hello, clique em **conceder permissão** tooconfigure acesso. opção primeira Olá é habilitada somente quando o usuário Olá que criou a conta do repositório Data Lake Olá também é um administrador de saudação Cofre de chaves do Azure.
   * Olá, outra opção é cmdlet do PowerShell Olá toorun exibida na folha de saudação. Você precisa toobe proprietário Olá Olá Cofre de chaves do Azure ou ter permissões de toogrant de capacidade de Olá Olá Cofre de chaves do Azure. Depois de executar o cmdlet hello, volte a folha de toohello e clique em **habilitar** tooconfigure acesso.

## <a name="createfolder"></a>Criar pastas na conta do Repositório Azure Data Lake
Você pode criar pastas em seu toomanage de conta do repositório Data Lake e armazenar dados.

1. Abrir conta de repositório Data Lake Olá que você criou. No painel esquerdo do hello, clique em **procurar**, clique em **repositório Data Lake**e clique em nome da conta Olá sob a qual você deseja toocreate pastas da folha de repositório Data Lake hello,. Se você fixou Olá quadro inicial toohello de conta, clique em bloco essa conta.
2. Na folha de sua conta do Repositório Data Lake, clique em **Gerenciador de Dados**.
   
    ![Criar pastas na conta do Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.Folder.png "Criar pastas na conta do Data Lake Store")
3. Na folha de conta seu repositório Data Lake, clique em **nova pasta**, insira um nome para a nova pasta de saudação e, em seguida, clique em **Okey**.
   
    ![Criar pastas na conta do Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Folder.Name.png "Criar pastas na conta do Data Lake Store")
   
    pasta Olá recém-criado está listada no hello **Data Explorer** folha. Você pode criar pastas aninhadas em qualquer nível.
   
    ![Criar pastas na conta do Data Lake](./media/data-lake-store-get-started-portal/ADL.New.Directory.png "Criar pastas na conta do Data Lake")

## <a name="uploaddata"></a>Carregar conta de repositório Data Lake tooAzure dados
Você pode carregar seu tooan dados conta do repositório Azure Data Lake diretamente no hello nível ou tooa pasta raiz que você criou na conta de saudação. Olá seguinte captura de tela, siga tooupload de etapas de saudação uma subpasta de tooa do arquivo de saudação **Data Explorer** folha. Nesta captura de tela, o arquivo de saudação é carregado tooa subpasta mostrada na trilha de saudação (marcada por uma caixa vermelha).

Se você estiver procurando por alguns tooupload de dados de exemplo, você pode obter Olá **ambulância dados** pasta Olá [repositório Git do Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

![Carregar dados](./media/data-lake-store-get-started-portal/ADL.New.Upload.File.png "Carregar dados")

## <a name="properties"></a>Propriedades e ações disponíveis no hello dados armazenados
Clique em Olá Olá de tooopen de arquivo recém adicionada **propriedades** folha. Propriedades de saudação associadas ao arquivo hello e ações de saudação, que você pode executar no arquivo hello estão disponíveis nessa folha. Você também pode copiar Olá caminho completo toofile em sua conta do repositório Azure Data Lake, realçada na caixa Olá vermelho no hello captura de tela a seguir:

![Propriedades de dados saudação](./media/data-lake-store-get-started-portal/ADL.File.Properties.png "propriedades nos dados Olá")

* Clique em **visualização** toosee uma visualização de arquivo hello, diretamente do navegador de saudação. Você pode especificar o formato de saudação de visualização de saudação também. Clique em **visualização**, clique em **formato** em Olá **a visualização de arquivo** folha e em Olá **formato de arquivo de visualização** folha especificar Olá opções tais como como o número de linhas toodisplay, codificação toouse toouse delimitador, etc.
  
  ![Formato de arquivo de visualização](./media/data-lake-store-get-started-portal/ADL.File.Preview.png "Formato de arquivo de visualização")
* Clique em **baixar** computador de tooyour toodownload Olá arquivo.
* Clique em **renomear arquivo** toorename arquivo de saudação.
* Clique em **excluir arquivo** toodelete arquivo de saudação.

## <a name="secure-your-data"></a>Proteja seus dados
Você pode proteger dados Olá armazenados na conta do repositório Azure Data Lake usando o Active Directory do Azure e controle de acesso (ACLs). Para obter instruções sobre como toodo que, consulte [proteção de dados no repositório Azure Data Lake](data-lake-store-secure-data.md).

## <a name="delete-azure-data-lake-store-account"></a>Excluir a conta do Repositório Azure Data Lake
toodelete uma conta do repositório Azure Data Lake, na folha seu repositório Data Lake, clique **excluir**. ação de saudação tooconfirm, será nome de saudação do tooenter solicitadas da conta de Olá que desejar toodelete. Insira nome de saudação da conta de saudação e, em seguida, clique em **excluir**.

![Excluir conta do Data Lake](./media/data-lake-store-get-started-portal/ADL.Delete.Account.png "Excluir conta do Data Lake")

## <a name="next-steps"></a>Próximas etapas
* [Proteger dados no Repositório Data Lake](data-lake-store-secure-data.md)
* [Usar a Análise Data Lake do Azure com o Repositório Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usar o Azure HDInsight com o Repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Acessar os logs de diagnóstico do Azure Data Lake Store](data-lake-store-diagnostic-logs.md)

