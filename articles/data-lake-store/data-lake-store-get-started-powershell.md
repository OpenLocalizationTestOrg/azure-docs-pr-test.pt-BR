---
title: "aaaUse PowerShell tooget Introdução ao repositório Azure Data Lake | Microsoft Docs"
description: "Usar o Azure PowerShell toocreate uma conta do repositório Data Lake e executar operações básicas"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a>Introdução ao Repositório Azure Data Lake usando o Azure PowerShell
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

Saiba como toouse do Azure PowerShell toocreate uma Data Lake do Azure armazenam conta e executar operações básicas, como criar pastas, carregar e baixar arquivos de dados, excluir sua conta, etc. Para saber mais sobre o Data Lake Store, veja [Visão geral do Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 ou superior**. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

## <a name="authentication"></a>Autenticação
Este artigo usa uma abordagem mais simples de autenticação com repositório Data Lake onde você está tooenter solicitada as credenciais de conta do Azure. Olá acesso nível tooData Lake repositório conta de sistema de arquivos e, em seguida, é controlado pelo nível de acesso de saudação do hello usuário conectado no. No entanto, há outras abordagens como tooauthenticate bem com repositório Data Lake, que são **autenticação do usuário final** ou **autenticação de serviço a serviço**. Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-an-azure-data-lake-store-account"></a>Criar uma conta do Repositório Azure Data Lake
1. Da área de trabalho, abrir uma nova janela do Windows PowerShell, digite Olá seguinte trecho toolog em tooyour conta do Azure, definir Olá assinatura e registrar provedor de repositório Data Lake hello. Quando solicitada toolog, certifique-se de você fazer logon como uma saudação admininistrators/proprietário da assinatura:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. Uma conta do Repositório Azure Data Lake está associada a um Grupo de Recursos do Azure. Comece criando um Grupo de Recursos do Azure.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    ![Criar um Grupo de Recursos do Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Criar um Grupo de Recursos do Azure")
3. Crie uma conta do Repositório Azure Data Lake. nome de saudação especificado deve conter apenas letras minúsculas e números.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    ![Criar uma conta do Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Criar uma conta do Azure Data Lake Store")
4. Verifique se a conta de saudação é criada com êxito.

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    saudação de saída para isso deve ser **True**.

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a>Criar estruturas de diretório no Repositório Azure Data Lake
Você pode criar diretórios sob o toomanage de conta do repositório Azure Data Lake e armazenar dados.

1. Especifique um diretório raiz.

        $myrootdir = "/"
2. Criar um novo diretório chamado **mynewdirectory** na raiz de saudação especificado.

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. Verifique se o que diretório Olá novo é criado com êxito.

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    Ele deverá mostrar uma saída semelhante Olá seguinte:

    ![Verificar o Diretório](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verificar o Diretório")

## <a name="upload-data-tooyour-azure-data-lake-store"></a>Carregar o repositório de dados tooyour Azure Data Lake
Você pode carregar seu repositório data tooData Lake diretamente no hello nível ou tooa diretório raiz que você criou na conta de saudação. trechos de saudação a seguir demonstram como tooupload alguns diretório de toohello de dados de exemplo (**mynewdirectory**) criado na seção anterior hello.

Se você estiver procurando por alguns tooupload de dados de exemplo, você pode obter Olá **ambulância dados** pasta Olá [repositório Git do Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Baixe o arquivo hello e armazená-lo em um diretório local no seu computador, como C:\sampledata\.

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a>Renomear, baixar e excluir dados do Repositório Data Lake
toorename um arquivo, use Olá comando a seguir:

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

toodownload um arquivo, use Olá comando a seguir:

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

toodelete um arquivo, use Olá comando a seguir:

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

Quando solicitado, insira **Y** toodelete item de saudação. Se você tiver mais de um toodelete de arquivo, você pode fornecer todos os caminhos de saudação separados por vírgula.

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a>Excluir sua conta do Repositório Azure Data Lake
Use sua conta de repositório Data Lake de saudação toodelete de comando a seguir.

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

Quando solicitado, insira **Y** toodelete conta de saudação.

## <a name="performance-guidance-while-using-powershell"></a>Diretrizes de desempenho durante o uso do PowerShell

Abaixo está as configurações mais importantes que podem ser ajustadas tooget Olá melhor desempenho ao usar o PowerShell toowork com repositório Data Lake hello:

| Propriedade            | Padrão | Descrição |
|---------------------|---------|-------------|
| PerFileThreadCount  | 10      | Esse parâmetro permite que você toochoose número de saudação de threads paralelos para carregamento ou download de cada arquivo. Esse número representa Olá máximo de threads que pode ser alocado por arquivo, mas você pode receber menos threads dependendo do cenário (por exemplo, se você estiver carregando um arquivo de 1 KB, você obterá um thread mesmo se você pedir 20 segmentos).  |
| ConcurrentFileCount | 10      | Esse parâmetro é especificamente para carregar ou baixar pastas. Esse parâmetro determina o número de saudação de arquivos simultâneos que podem ser carregadas ou baixadas. Esse número representa o número máximo de saudação de arquivos simultâneos que podem ser carregadas ou baixadas ao mesmo tempo, mas você pode receber menos simultaneidade dependendo do cenário (por exemplo, se você estiver carregando dois arquivos, você obterá duas carregamentos de arquivo simultâneas mesmo se você pedir 15). |

**Exemplo**

Esse comando baixa os arquivos da unidade de local do usuário do repositório Azure Data Lake toohello usando 20 threads por arquivo e 100 arquivos simultâneos.

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a>Como determinar o hello tooset de valor para esses parâmetros?

Aqui estão algumas diretrizes que podem ser usadas.

* **Etapa 1: Determinar a contagem total de threads de saudação** -deve começar com calcular toouse de contagem total de threads de saudação. Como diretriz geral, você deve usar 6 threads para cada núcleo físico.

        Total thread count = total physical cores * 6

    **Exemplo**

    Supondo que você estiver executando Olá PowerShell comandos de uma VM D14 que tem 16 núcleos

        Total thread count = 16 cores * 6 = 96 threads


* **Etapa 2: Calcular PerFileThreadCount** -calculamos nosso PerFileThreadCount com base no tamanho de saudação de arquivos de saudação. Para arquivos menores do que 2,5 GB, há toochange sem necessidade esse parâmetro porque saudação padrão de 10 é suficiente. Para arquivos maiores do que 2,5 GB, você deve usar 10 threads como base Olá Olá primeiro 2,5 GB e adicionar 1 thread de cada aumento de 256 MB adicionais no tamanho do arquivo. Se você estiver copiando uma pasta com uma grande variedade de tamanhos de arquivo, considere agrupá-los em tamanhos de arquivo semelhantes. Ter tamanhos de arquivo diferentes pode fazer com que o desempenho não seja o ideal. Se isso não for possível toogroup semelhante tamanhos de arquivos, você deve definir PerFileThreadCount com base no maior tamanho de arquivo hello.

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    **Exemplo**

    Supondo que você tiver 100 arquivos que variam de 1GB too10GB, usamos Olá 10GB como Olá maior tamanho da equação, que lê como Olá seguinte do arquivo.

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* **Etapa 3: Calcular ConcurrentFilecount** -contagem de uso total de threads de saudação e PerFileThreadCount toocalculate ConcurrentFileCount com base em Olá equação a seguir.

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    **Exemplo**

    Com base nos valores de exemplo hello que utilizamos

        96 = 40 * ConcurrentFileCount

    Portanto, **ConcurrentFileCount** é **2.4**, que podemos pode arredondar muito**2**.

### <a name="further-tuning"></a>Ajuste adicional

Você pode precisar de mais ajuste porque há uma variedade de toowork de tamanhos de arquivo com. Olá acima cálculo funcionará bem se todos ou a maioria dos arquivos de saudação é toohello maiores e mais próximo intervalo de 10GB. Se em vez disso houver vários tamanhos de arquivos diferentes com muitos arquivos sendo menores, você poderá reduzir PerFileThreadCount. Reduzindo Olá PerFileThreadCount, podemos aumentar ConcurrentFileCount. Portanto, se vamos supor que a maioria dos arquivos menor no intervalo de 5GB hello, podemos novamente fazer nosso cálculo:

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

Portanto, **ConcurrentFileCount** será agora 96/20, que é 4.8, arredondado muito**4**.

Você pode continuar tootune essas configurações alterando Olá **PerFileThreadCount** para cima e para baixo dependendo da distribuição Olá seus tamanhos de arquivos de.

### <a name="limitation"></a>Limitações

* **Número de arquivos é menor do que ConcurrentFileCount**: se o número de saudação de arquivos que você está carregando seja menor que Olá **ConcurrentFileCount** calculado e, depois, você deve reduzir  **ConcurrentFileCount** toobe toohello igual número de arquivos. Você pode usar qualquer tooincrease segmentos restantes **PerFileThreadCount**.

* **Muitos threads**: se você aumentar o thread contagem muito sem aumentar o tamanho do cluster, você corre o risco de saudação de degradação do desempenho. Pode haver problemas de contenção quando a alternância de contexto em Olá da CPU.

* **Simultaneidade insuficiente**: se simultaneidade Olá não é suficiente, o cluster pode ser muito pequeno. Você pode aumentar o número de saudação de nós no cluster que lhe dará mais simultaneidade.

* **Erros de limitação**: você pode ver erros de limitação se a simultaneidade for muito alta. Se você estiver vendo erros de limitação, reduzir a simultaneidade de saudação ou entre em contato conosco.

## <a name="next-steps"></a>Próximas etapas
* [Proteger dados no Repositório Data Lake](data-lake-store-secure-data.md)
* [Usar a Análise Data Lake do Azure com o Repositório Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usar o Azure HDInsight com o Repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)

