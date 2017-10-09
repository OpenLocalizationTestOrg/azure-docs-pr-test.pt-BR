---
title: aaaCopy atividade guia de desempenho e ajuste | Microsoft Docs
description: "Saiba mais sobre os principais fatores que afetam o desempenho de saudação da movimentação dos dados no Azure Data Factory quando você usa a atividade de cópia."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 4b9a6a4f-8cf5-4e0a-a06f-8133a2b7bc58
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jingwang
ms.openlocfilehash: b0fb5a76c34752d07e8ddfffbb799a05fb5d6be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-activity-performance-and-tuning-guide"></a>Guia Desempenho e ajuste da Atividade de Cópia
A Atividade de cópia do Azure Data Factory fornece uma solução de dados excelente, segura, confiável e de alto desempenho. Ele permite que você toocopy dezenas de terabytes de dados de cada dia em uma grande variedade de nuvem e repositórios de dados local. Desempenho de carregamento de dados de rápido são tooensure chave, você pode focalizar o problema de "big data" core Olá: Criando soluções de análise avançada e obter um aprofundamento de todos esses dados.

O Azure fornece um conjunto de nível empresarial soluções de depósito de dados e armazenamento de dados e atividade de cópia oferece um experiência que é fácil tooconfigure e configure de carregamento de dados altamente otimizados. Com apenas uma atividade de cópia única, você pode obter:

* Carregar dados no **SQL Data Warehouse do Azure** a **1,2 GBps**. Para ver um passo a passo com um caso de uso, veja [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carregar 1 TB no SQL Data Warehouse do Azure em menos de 15 minutos com o Azure Data Factory).
* O carregamento de dados no **Armazenamento de Blobs do Azure** a **1,0 GBps**
* O carregamento de dados no **Azure Data Lake Store** a **1,0 GBps**

Este artigo descreve:

* [Números de referência de desempenho](#performance-reference) para toohelp de repositórios de dados com suporte de origem e do coletor planejar seu projeto.
* Recursos que podem aumentar Olá taxa de transferência de cópia em diferentes cenários, incluindo [unidades de movimentação de dados em nuvem](#cloud-data-movement-units), [paralelo cópia](#parallel-copy), e [preparados cópia](#staged-copy);
* [Orientação de ajuste de desempenho](#performance-tuning-steps) em como tootune Olá Olá e desempenho fatores principais que podem afetar o desempenho de cópia.

> [!NOTE]
> Se você não estiver familiarizado com a Atividade de Cópia em geral, consulte [Mover dados usando a Atividade de Cópia](data-factory-data-movement-activities.md) antes de ler este artigo.
>

## <a name="performance-reference"></a>Referência de desempenho

Como uma referência de tabela abaixo mostra o número de taxa de transferência de cópia Olá em MBps para Olá fornecido com base em testes internos de pares de origem e do coletor. Para comparação, ela também demonstra como as diferentes configurações das [unidades de movimentação de dados na nuvem](#cloud-data-movement-units) ou da [escalabilidade do Gateway de Gerenciamento de Dados](data-factory-data-management-gateway-high-availability-scalability.md) (vários nós de gateway) podem ajudar no desempenho da cópia.

![Matriz de desempenho](./media/data-factory-copy-activity-performance/CopyPerfRef.png)


**Toonote pontos:**
* Taxa de transferência é calculada usando Olá seguinte fórmula: [tamanho dos dados lidos na origem] / [atividade de cópia duração da execução].
* Olá números de referência de desempenho na tabela de saudação foram medidos usando [TPC-H](http://www.tpc.org/tpch/) conjunto de dados em uma atividade de cópia única execução.
* Em repositórios de dados do Azure, Olá origem e do coletor estão em Olá mesma região do Azure.
* Para a cópia híbrida entre local e nuvem armazenamentos de dados, cada nó do gateway foi executado em uma máquina que foi separada do armazenamento de dados de local Olá com abaixo especificação. Quando uma única atividade foi executada no gateway, operação de cópia Olá consumido apenas uma pequena parte da CPU, memória ou largura de banda de rede da máquina de teste hello. Saiba mais em [Considerações do Gateway de Gerenciamento de Dados](#considerations-for-data-management-gateway).
    <table>
    <tr>
        <td>CPU</td>
        <td>32 núcleos, Intel Xeon E5-2660 v2 de 2.20 GHz</td>
    </tr>
    <tr>
        <td>Memória</td>
        <td>128 GB</td>
    </tr>
    <tr>
        <td>Rede</td>
        <td>Interface da Internet: 10 Gbps; Interface da intranet: 40 Gbps</td>
    </tr>
    </table>


> [!TIP]
> Você pode obter maior taxa de transferência utilizando mais unidades de movimentação de dados (DMUs) que saudação padrão DMUs máximo, que é 32 para executar uma atividade de cópia de nuvem para a nuvem. Por exemplo, com 100 DMUs, é possível copiar dados do Blob do Azure para o Azure Data Lake Store a **1 GBps**. Consulte Olá [unidades de movimentação de dados em nuvem](#cloud-data-movement-units) seção para obter detalhes sobre esse recurso e a saudação de cenário com suporte. Entre em contato com [suporte do Azure](https://azure.microsoft.com/support/) toorequest DMUs mais.

## <a name="parallel-copy"></a>Cópia paralela
Você pode ler a fonte de dados de saudação ou gravar o destino de toohello dados **em paralelo dentro de uma atividade de cópia executar**. Esse recurso melhora a taxa de transferência de saudação de uma operação de cópia e reduz o tempo de saudação demora toomove dados.

Essa configuração é diferente da saudação **simultaneidade** propriedade na definição de atividade de saudação. Olá **simultaneidade** propriedade determina o número de saudação do **executa atividades simultâneas de cópia** tooprocess dados do windows diferente de atividade (1 too2 de AM AM, estou too3 de AM 2, 3 too4 de AM, e assim por diante). Esse recurso é útil quando você executa um carregamento histórico. capacidade de cópia paralela Olá aplica tooa **única de execução da atividade**.

Vejamos um cenário de exemplo. Olá exemplo a seguir, várias fatias de saudação últimos necessário toobe processado. O Data Factory executa uma instância da Atividade de Cópia (uma execução da atividade) para cada fatia:

* a fatia de dados Olá da primeira janela de atividade hello (estou too2 de AM 1) = = > atividade executada 1
* a fatia de dados Olá da segunda janela de atividade hello (estou too3 de AM 2) = = > atividade executada 2
* a fatia de dados Olá da segunda janela de atividade hello (estou 3 too4 de AM) = = > atividade executada 3

E assim por diante.

Neste exemplo, quando hello **simultaneidade** valor é definido como too2, **atividade executada 1** e **atividade executada 2** copiar dados de duas janelas de atividade **simultaneamente**  tooimprove desempenho de movimento de dados. No entanto, se vários arquivos estão associados com 1 de execução da atividade, o serviço de movimentação de dados Olá copia arquivos de Olá fonte toohello destino um arquivo por vez.

### <a name="cloud-data-movement-units"></a>Unidades de movimentação de dados de nuvem
Um **unidade de movimentação de dados de nuvem (DMU —)** é uma medida que representa a potência de saudação (uma combinação de CPU, memória e alocação de recursos de rede) de uma única unidade na fábrica de dados. Uma DMU pode ser usada em uma operação de cópia de nuvem para nuvem, mas não em uma cópia híbrida.

Por padrão, a fábrica de dados usa tooperform de DMU — uma única nuvem uma única atividade de cópia executados. toooverride esse padrão, especifique um valor para Olá **cloudDataMovementUnits** propriedade da seguinte maneira. Para obter informações sobre nível de saudação de ganho de desempenho que você pode obter ao configurar unidades de mais de uma origem de cópia específica e do coletor, consulte Olá [referência desempenho](#performance-reference).

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "cloudDataMovementUnits": 32
        }
    }
]
```
Olá **valores permitidos** para Olá **cloudDataMovementUnits** propriedade são 1 (padrão), 2, 4, 8, 16, 32. Olá **número real de nuvem DMUs** que a operação de cópia Olá usa em tempo de execução é igual tooor menor do que valor de saudação configurada, dependendo de seu padrão de dados.

> [!NOTE]
> Se precisar de mais DMUs de nuvem para uma taxa de transferência maior, entre em contato com o [suporte do Azure](https://azure.microsoft.com/support/). Configuração de 8 e superior atualmente só funcionam quando você **copiar vários arquivos de Blob repositório Data Lake/armazenamento/Amazon S3/nuvem FTP/nuvem SFTP tooBlob armazenamento repositório Data Lake/do Azure/banco de dados SQL**.
>

### <a name="parallelcopies"></a>parallelCopies
Você pode usar o hello **parallelCopies** paralelismo de saudação tooindicate de propriedade que você deseja toouse de atividade de cópia. Você pode pensar essa propriedade como o número máximo de saudação de threads na atividade de cópia que pode ler sua fonte ou gravar armazenamentos de dados do coletor tooyour em paralelo.

Para cada atividade de cópia executados, a fábrica de dados determina Olá número de paralelo cópias toouse toocopy dados do repositório de dados de origem hello e repositório de dados de destino toohello. número padrão de saudação do cópias paralelas que ele usa depende do tipo hello de origem e do coletor que você está usando.  

| Fonte e coletor | Contagem de cópia paralela padrão determinada pelo serviço |
| --- | --- |
| Copiar dados entre os armazenamentos baseados em arquivo (armazenamento de Blobs; Data Lake Store; Amazon S3; sistema de arquivos local; HDFS (Sistema de Arquivos Distribuído Hadoop) local) |Entre 1 e 32. Depende do tamanho de saudação dos arquivos de saudação e número de saudação de unidades de movimentação de dados de nuvem (DMUs) toocopy usados dados entre dois armazenamentos de dados de nuvem ou Olá de configuração física de saudação do computador do Gateway usado para uma cópia híbrida (toocopy dados tooor de um repositório de dados local ). |
| Copiar dados de **tooAzure o armazenamento de tabela de armazenamento de qualquer fonte de dados** |4 |
| Todos os outros pares de origem e coletor |1 |

Geralmente, comportamento padrão de saudação deve fornecer melhor taxa de transferência de saudação. No entanto, Olá toocontrol de carga em computadores que hospedam seus armazenamentos de dados ou de desempenho de cópia tootune, você pode escolher o valor de padrão de saudação toooverride e especifique um valor para hello **parallelCopies** propriedade. Olá valor deve ser entre 1 e 32 (ambos incluídos). Em tempo de execução para um melhor desempenho hello, atividade de cópia usa um valor que seja menor ou igual valor toohello definido.

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "parallelCopies": 8
        }
    }
]
```
Toonote pontos:

* Quando você copiar dados entre armazenamentos baseada em arquivo, Olá **parallelCopies** determinar paralelismo Olá no nível de arquivo hello. saudação de agrupamento em um único arquivo aconteceria sob automática e transparente e foi projetada toouse Olá melhor adequado tamanho da parte de um repositório de dados de origem digite dados tooload em paralelo e ortogonal tooparallelCopies. número real de saudação de cópias paralelas Olá movimentação de dados serviço usa para a operação de cópia de saudação em tempo de execução é não mais do que o número de saudação de arquivos que você tem. Se o comportamento de cópia de saudação é **mergeFile**, atividade de cópia não pode tirar proveito de paralelismo de nível de arquivo.
* Quando você especificar um valor para Olá **parallelCopies** propriedade, considere a possibilidade de aumento de carga Olá seus repositórios de dados de origem e do coletor e toogateway se ela é uma cópia híbrida. Isso acontece especialmente quando você tem várias atividades ou execuções simultâneas do hello mesmo atividades executadas em Olá mesmo repositório de dados. Se você notar que o repositório de dados hello ou Gateway é sobrecarregado com carga hello, diminuir Olá **parallelCopies** carga de saudação do valor toorelieve.
* Quando você copia dados de armazenamentos que não são toostores baseados em arquivo que são baseados em arquivo, o serviço de movimentação de dados de saudação ignora Olá **parallelCopies** propriedade. Mesmo se o paralelismo for especificado, ele não será aplicado neste caso.

> [!NOTE]
> Você deve usar saudação de toouse 1.11 ou mais recente do Gateway de gerenciamento de dados versão **parallelCopies** recurso quando você faz uma cópia híbrida.
>
>

toobetter usar essas duas propriedades e tooenhance a taxa de transferência de movimentação de dados, consulte Olá [casos de uso de exemplo](#case-study-use-parallel-copy). Você não precisa tooconfigure **parallelCopies** tootake vantagem do comportamento padrão de saudação. Se você configurar e **parallelCopies** for muito pequeno, várias DMUs de nuvem poderão não ser totalmente utilizadas.  

### <a name="billing-impact"></a>Impacto de cobrança
Ele tem **importante** tooremember que você é cobrado com base no tempo total de saudação da operação de cópia de saudação. Se um trabalho de cópia usado tootake uma hora com a unidade de uma nuvem e agora ele entra em 15 minutos com quatro unidades de nuvem, hello permanece geral de cobrança quase Olá mesmo. Por exemplo, você usa quatro unidades de nuvem. primeira unidade de nuvem Olá gasta 10 minutos, hello um segundo, 10 minutos, Olá um terceiro, 5 minutos e Olá uma quarta, 5 minutos, tudo em uma atividade de cópia executados. Você é cobrado para Olá cópia total (movimentação de dados) tempo, o que é 10 + 10 + 5 + 5 = 30 minutos. Usar **parallelCopies** não afeta a cobrança.

## <a name="staged-copy"></a>Cópia em etapas
Quando você copiar dados de um repositório de dados do coletor do repositório tooa do fonte dados, você pode escolher toouse armazenamento de Blob como um armazenamento de preparo intermediários. Preparação é especialmente útil em Olá casos a seguir:

1. **Você deseja tooingest dados de várias fontes de dados no SQL Data Warehouse por meio de PolyBase**. SQL Data Warehouse usa PolyBase como tooload um mecanismo de alta taxa de transferência uma grande quantidade de dados no SQL Data Warehouse. No entanto, os dados de origem Olá devem estar no armazenamento de Blob, e ela deve atender aos critérios adicionais. Quando você carrega dados de um armazenamento de dados diferente do armazenamento de Blobs, pode ativar a cópia dos dados por meio do armazenamento de Blobs de preparo intermediário. Nesse caso, a fábrica de dados executa Olá necessário tooensure de transformações de dados se ele atende aos requisitos de saudação do PolyBase. Em seguida, ele usa dados tooload no SQL Data Warehouse. Para obter mais detalhes, consulte [Use tooload dados no Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse). Para ver um passo a passo com um caso de uso, veja [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carregar 1 TB no SQL Data Warehouse do Azure em menos de 15 minutos com o Azure Data Factory).
2. **Às vezes, leva algum tempo tooperform uma movimentação de dados híbrido (ou seja, toocopy entre um repositório de dados local e um repositório de dados de nuvem) em uma conexão de rede lenta**. tooimprove desempenho, é possível compactar Olá dados no local para que ele leva menos tempo do repositório de dados de preparo do toomove dados toohello na nuvem de saudação. Em seguida, poderá descompactar dados Olá Olá repositório de preparo antes de carregá-lo no armazenamento de dados de destino hello.
3. **Você não quiser tooopen portas que a porta 80 e a porta 443 em seu firewall, devido a políticas de TI corporativas**. Por exemplo, quando você copiar dados de um coletor de banco de dados SQL local dados repositório tooan ou um coletor do Azure SQL Data Warehouse, você precisa tooactivate comunicação de saída TCP na porta 1433 para o firewall do Windows hello e do firewall corporativo. Nesse cenário, aproveita Olá gateway toofirst cópia tooa Blob storage preparo instância dados via HTTP ou HTTPS na porta 443. Em seguida, carrega dados saudação no banco de dados SQL ou SQL Data Warehouse de preparo do armazenamento de Blob. Nesse fluxo, você não precisa tooenable porta 1433.

### <a name="how-staged-copy-works"></a>Como funciona a cópia em etapas
Quando você ativa o hello recurso de preparo, primeiro dados de saudação são copiados do hello fonte dados repositório toohello repositório de dados de preparo (traga seu próprio). Em seguida, os dados de saudação são copiados do hello armazenar toohello coletor dados armazenamento de dados de preparo. Fábrica de dados gerencia automaticamente o fluxo de dois estágios Olá para você. Fábrica de dados também limpa os dados temporários de saudação preparo armazenamento após a conclusão da movimentação de dados de saudação.

No cenário de cópia de nuvem hello (origem e o coletor de dados repositórios estão na nuvem Olá), o gateway não é usado. Olá serviço da fábrica de dados executa operações de cópia de saudação.

![Cópia em etapas: cenário de nuvem](media/data-factory-copy-activity-performance/staged-copy-cloud-scenario.png)

No cenário de cópia híbrida hello (origem no local e coletor está na nuvem Olá), gateway Olá move tooa repositório de dados de preparo do repositório de dados dos dados de origem de saudação. Serviço de fábrica de dados move toohello repositório de coletor de dados do repositório de dados de saudação dados de teste. Copiando dados de um tooan de repositório de dados de nuvem local do repositório de dados por meio de preparo também é suportado com fluxo Olá revertida.

![Cópia em etapas: cenário híbrido](media/data-factory-copy-activity-performance/staged-copy-hybrid-scenario.png)

Quando você ativa a movimentação de dados por meio de um repositório de preparo, você pode especificar se deseja Olá dados toobe compactado antes de mover dados de origem de saudação dados armazenam tooan provisória ou armazenamento de dados de preparo e, em seguida, descompactado antes de mover dados de um provisório ou repositório de dados do coletor toohello do repositório de dados de preparo.

Atualmente, não é possível copiar dados entre dois armazenamentos de dados locais usando um armazenamento de preparo. Esperamos que este toobe opção disponível em breve.

### <a name="configuration"></a>Configuração
Configurar Olá **enableStaging** configuração na atividade de cópia toospecify se desejar Olá dados toobe testado no armazenamento de Blob antes de carregá-los em um repositório de dados de destino. Quando você define **enableStaging** tooTRUE, especificar propriedades adicionais de saudação listadas na tabela seguinte hello. Se você não tiver um, você também precisa toocreate um armazenamento do Azure ou serviço vinculado a assinatura de acesso para a preparação do armazenamento compartilhado.

| Propriedade | Descrição | Valor padrão | Obrigatório |
| --- | --- | --- | --- |
| **enableStaging** |Especifique se deseja toocopy dados por meio de um provisório repositório de preparo. |Falso |Não |
| **linkedServiceName** |Especificar nome de saudação de um [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [o AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) serviço, que se refere a instância de toohello de armazenamento que você pode usar como um repositório de preparo provisório vinculado. <br/><br/> Você não pode usar o armazenamento com um dado de tooload de assinatura de acesso compartilhado no SQL Data Warehouse por meio do PolyBase. Pode usar em todos os outros cenários. |N/D |Sim, quando **enableStaging** é definido tooTRUE |
| **path** |Especifique o caminho de armazenamento de Blob Olá que deseja que os dados de preparação de saudação toocontain. Se você não fornecer um caminho, o serviço de saudação cria um contêiner toostore os dados temporários. <br/><br/> Especifique um caminho apenas se você usar o armazenamento com uma assinatura de acesso compartilhado ou exigir toobe dados temporários em um local específico. |N/D |Não |
| **enableCompression** |Especifica se os dados devem ser compactados antes de ser copiado toohello destino. Essa configuração reduz o volume de saudação de dados sendo transferidos. |Falso |Não |

Aqui está um exemplo de definição de atividade de cópia com propriedades Olá descritas Olá anterior da tabela:

```json
"activities":[  
{
    "name": "Sample copy activity",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDBOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlSink"
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob",
            "path": "stagingcontainer/path",
            "enableCompression": true
        }
    }
}
]
```

### <a name="billing-impact"></a>Impacto de cobrança
Você é cobrado com base em duas etapas: duração da cópia e tipo de cópia.

* Ao usar o preparo durante uma cópia de nuvem (copiar dados de um repositório de dados de nuvem nuvem dados repositório tooanother), você é cobrado Olá [soma da duração de cópia de etapas 1 e 2] x [preço de unidade de cópia de nuvem].
* Ao usar o preparo durante uma cópia híbrida (copiar dados de um repositório de dados local dados repositório tooa nuvem), você será cobrado por [duração da cópia híbrida] x [híbrida cópia unitário] + [duração de cópia de nuvem] x [preço de unidade de cópia de nuvem].

## <a name="performance-tuning-steps"></a>Etapas de ajuste do desempenho
Sugerimos que você siga essas etapas tootune desempenho de saudação do seu serviço de fábrica de dados com a atividade de cópia:

1. **Estabelecer uma linha de base**. Durante a fase de desenvolvimento hello, teste seu pipeline usando a atividade de cópia em uma amostra representativa de dados. Você pode usar o hello fábrica de dados [divisão modelo](data-factory-scheduling-and-execution.md) toolimit quantidade de saudação de dados que você trabalha com.

   Coletar o tempo de execução e as características de desempenho usando Olá **monitoramento e gerenciamento de aplicativo**. Escolha **Monitorar e Gerenciar** na página inicial do Data Factory. Na exibição de árvore de saudação, escolha Olá **conjunto de dados de saída**. Em Olá **atividade Windows** , escolha a saudação de execução da atividade de cópia. **Atividade Windows** lista duração da atividade de cópia hello e tamanho de saudação dos dados de saudação que são copiados. taxa de transferência de saudação é listada em **Pesquisador de objetos de janela de atividade**. toolearn mais sobre o aplicativo hello, consulte [monitorar e gerenciar os pipelines de fábrica de dados do Azure usando Olá monitoramento e gerenciamento de aplicativo](data-factory-monitor-manage-app.md).

   ![Detalhes da execução da atividade](./media/data-factory-copy-activity-performance/mmapp-activity-run-details.png)

   Artigo hello, você pode comparar o desempenho de saudação e a configuração do seu cenário tooCopy atividade [referência desempenho](#performance-reference) de nossos testes.
2. **Diagnosticar e otimizar o desempenho**. Se você observar de desempenho de saudação não atende às suas expectativas, será necessário tooidentify afunilamentos de desempenho. Em seguida, otimizar o desempenho tooremove ou reduzir o efeito de saudação de afunilamentos. Uma descrição completa de diagnóstico de desempenho está além do escopo deste artigo hello, mas aqui estão algumas considerações comuns:

   * Recursos de desempenho:
     * [Cópia paralela](#parallel-copy)
     * [Unidades de movimentação de dados de nuvem](#cloud-data-movement-units)
     * [Cópia em etapas](#staged-copy)
     * [Escalabilidade do Gateway de Gerenciamento de Dados](data-factory-data-management-gateway-high-availability-scalability.md)
   * [Gateway de gerenciamento de dados](#considerations-for-data-management-gateway)
   * [Fonte](#considerations-for-the-source)
   * [Coletor](#considerations-for-the-sink)
   * [Serialização e desserialização](#considerations-for-serialization-and-deserialization)
   * [Compactação](#considerations-for-compression)
   * [Mapeamento de coluna](#considerations-for-column-mapping)
   * [Outras considerações](#other-considerations)
3. **Expanda o conjunto de dados inteiro do hello configuração tooyour**. Quando estiver satisfeito com o desempenho e os resultados da execução de hello, você pode expandir a definição de saudação e pipeline toocover período ativo de todo o conjunto de dados.

## <a name="considerations-for-data-management-gateway"></a>Considerações do Gateway de Gerenciamento de Dados
**Instalação do gateway**: Recomendamos que você use um toohost máquina dedicada Gateway de gerenciamento de dados. Confira [Considerações para o uso do Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md#considerations-for-using-gateway).  

**Monitoramento de gateway e backup/expansão**: um único gateway lógico com um ou mais nós de gateway pode atender vários atividade de cópia é executado no Olá a mesma hora simultaneamente. Você pode exibir um instantâneo de quase em tempo real de utilização de recursos (CPU, memória, network(in/out), etc.) em uma máquina de gateway, assim como o número de saudação de trabalhos simultâneos em execução em vez de limite em Olá portal do Azure, consulte [gateway Monitor no portal de saudação](data-factory-data-management-gateway.md#monitor-gateway-in-the-portal). Se você precisar pesada na movimentação de dados híbrido com grande número de execuções de atividade de cópia simultânea ou com grande volume de dados toocopy, considere muito[aumentar ou expandir gateway](data-factory-data-management-gateway-high-availability-scalability.md#scale-considerations) assim como toobetter utilizam o recurso ou Copiar do tooprovision mais tooempower de recursos. 

## <a name="considerations-for-hello-source"></a>Considerações sobre a origem de saudação
### <a name="general"></a>Geral
Certifique-se de que Olá subjacente de repositório de dados não está sobrecarregado com outras cargas de trabalho que estão executando em ou em relação a ela.

Para repositórios de dados da Microsoft, consulte [monitoramento e ajuste tópicos](#performance-reference) que são específicos toodata repositórios e ajudam você a compreender dados armazenam características de desempenho, minimizar tempos de resposta e maximizar a taxa de transferência.

Se você copiar dados de armazenamento de Blob tooSQL Data Warehouse, considere o uso de **PolyBase** tooboost desempenho. Consulte [Use tooload dados no Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) para obter detalhes. Para ver um passo a passo com um caso de uso, veja [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carregar 1 TB no SQL Data Warehouse do Azure em menos de 15 minutos com o Azure Data Factory).

### <a name="file-based-data-stores"></a>Armazenamentos de dados baseado em arquivo
*(Inclui o armazenamento de Blobs, Data Lake Store, Amazon S3, sistemas de arquivos locais e HDFS local)*

* **Média de tamanho do arquivo e contagem de arquivos**: a Atividade de Cópia transfere os dados um arquivo por vez. Com hello movida da mesma quantidade de dados toobe, hello produtividade geral é menor se dados saudação consistem em vários pequenos arquivos em vez de alguns arquivos grandes devido a fase de inicialização toohello para cada arquivo. Portanto, se possível, combine pequenos arquivos em maior arquivos toogain maior taxa de transferência.
* **Compactação e o formato de arquivo**: de maneiras tooimprove desempenho, consulte Olá [considerações para serialização e desserialização](#considerations-for-serialization-and-deserialization) e [considerações para compactação](#considerations-for-compression) seções.
* Para Olá **sistema de arquivos local** cenário no qual **Data Management Gateway** é obrigatório, consulte Olá [considerações para o Gateway de gerenciamento de dados](#considerations-for-data-management-gateway) seção.

### <a name="relational-data-stores"></a>Armazenamentos de dados relacionais
*(Inclui o Banco de Dados SQL, SQL Data Warehouse, Amazon Redshift, bancos de dados do SQL Server e bancos de dados Oracle, MySQL, DB2, Teradata, Sybase e PostgreSQL, etc.)*

* **Padrão de dados**: o esquema da tabela afeta a taxa de transferência de cópia. Um tamanho de linha grande oferece um desempenho melhor do que o tamanho da linha pequeno, toocopy Olá a mesma quantidade de dados. motivo de saudação é que banco de dados Olá pode recuperar com mais eficiência menos lotes de dados que contêm menos linhas.
* **Consulta ou procedimento armazenado**: otimizar a lógica de saudação de consulta de saudação ou procedimento armazenado que você especificar hello atividade de cópia dados de origem toofetch com mais eficiência.
* Para **bancos de dados relacionais locais**, como o SQL Server e Oracle, o que exige o uso de saudação do **Data Management Gateway**, consulte Olá [considerações para o Gateway de gerenciamento de dados](#considerations-on-data-management-gateway) seção.

## <a name="considerations-for-hello-sink"></a>Considerações para o coletor de saudação
### <a name="general"></a>Geral
Certifique-se de que Olá subjacente de repositório de dados não está sobrecarregado com outras cargas de trabalho que estão executando em ou em relação a ela.

Para repositórios de dados da Microsoft, consulte muito[monitoramento e ajuste tópicos](#performance-reference) que são lojas de toodata específico. Esses tópicos podem ajudá-lo a entender as características de desempenho do armazenamento de dados e como os tempos de resposta de toominimize e maximizar a taxa de transferência.

Se você estiver copiando dados de **armazenamento de Blob** muito**SQL Data Warehouse**, considere o uso de **PolyBase** tooboost desempenho. Consulte [Use tooload dados no Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) para obter detalhes. Para ver um passo a passo com um caso de uso, veja [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carregar 1 TB no SQL Data Warehouse do Azure em menos de 15 minutos com o Azure Data Factory).

### <a name="file-based-data-stores"></a>Armazenamentos de dados baseado em arquivo
*(Inclui o armazenamento de Blobs, Data Lake Store, Amazon S3, sistemas de arquivos locais e HDFS local)*

* **Copie o comportamento**: se você copiar dados de um repositório de dados diferentes com base em arquivo, atividade de cópia tem três opções via Olá **copyBehavior** propriedade. Preserva a hierarquia, nivela a hierarquia ou mescla os arquivos. Preservando tanto a simplificação de hierarquia tem pouca ou nenhuma sobrecarga de desempenho, mas mesclar arquivos causa tooincrease de sobrecarga de desempenho.
* **Compactação e o formato de arquivo**: consulte Olá [considerações para serialização e desserialização](#considerations-for-serialization-and-deserialization) e [considerações para compactação](#considerations-for-compression) seções de desempenho tooimprove maneiras .
* **Armazenamento de Blobs**: atualmente, o armazenamento de Blobs apenas suporta os blobs de blocos da transferência de dados otimizada e da taxa de transferência.
* Para **sistemas de arquivos local** cenários que exigem o uso de saudação do **Data Management Gateway**, consulte Olá [considerações para o Gateway de gerenciamento de dados](#considerations-for-data-management-gateway) seção.

### <a name="relational-data-stores"></a>Armazenamentos de dados relacionais
*(Inclui o Banco de Dados SQL, SQL Data Warehouse, bancos de dados do SQL Server e bancos de dados Oracle)*

* **Copie o comportamento**: dependendo definidas para as propriedades Olá **sqlSink**, atividade de cópia grava o banco de dados de destino de toohello dados de maneiras diferentes.
  * Por padrão, Olá dados movimentação serviço usa dados de tooinsert Olá API de cópia em massa em Acrescentar modo, que fornece Olá melhor desempenho.
  * Se você configurar um procedimento armazenado no coletor hello, o banco de dados de saudação aplica-se uma linha de dados de saudação em um horário em vez de um carregamento em massa. O desempenho cai significativamente. Se seu conjunto de dados for grande, quando aplicável, considere a possibilidade de saudação toousing **sqlWriterCleanupScript** propriedade.
  * Se você configurar Olá **sqlWriterCleanupScript** executar de propriedade para cada atividade de cópia, disparadores do serviço de Olá Olá script e, em seguida, você usar dados de saudação do hello API de cópia em massa tooinsert. Por exemplo, toooverwrite Olá toda a tabela com dados mais recentes do hello, você pode especificar um script toofirst excluir todos os registros antes de novos dados de saudação de carregamento em massa da fonte de hello.
* **Padrão de dados e tamanho do lote**:
  * O esquema da tabela afeta a taxa de transferência da cópia. toocopy Olá a mesma quantidade de dados, um tamanho de linha grande fornece desempenho melhor do que um tamanho de linha pequeno porque o banco de dados de saudação pode ser confirmada menos lotes de dados com mais eficiência.
  * A Atividade de Cópia insere dados em uma série de lotes. Você pode definir o número de saudação de linhas em um lote usando Olá **writeBatchSize** propriedade. Se os dados tiverem linhas pequenas, você pode definir Olá **writeBatchSize** propriedade com um toobenefit de valor mais alto de sobrecarga de lote menor e maior taxa de transferência. Se o tamanho de linha de saudação dos dados for grande, tenha cuidado ao aumentar **writeBatchSize**. Um valor alto pode causar falha de cópia tooa devida à sobrecarga de banco de dados de saudação.
* Para **bancos de dados relacionais locais** como o SQL Server e Oracle, o que exige o uso de saudação do **Data Management Gateway**, consulte Olá [considerações para o Gateway de gerenciamento de dados](#considerations-for-data-management-gateway) seção.

### <a name="nosql-stores"></a>Repositórios NoSQL
*(Inclui o Armazenamento de tabelas e o Azure Cosmos DB)*

* Para o **Armazenamento de Tabelas**:
  * **Partição**: gravar as partições de dados toointerleaved drasticamente degrada o desempenho. Classifique os dados de origem por chave de partição, de forma que dados saudação são inseridos com eficiência em uma partição após o outro, ou ajuste Olá lógica toowrite Olá tooa única partição de dados.
* Para o **Azure Cosmos DB**:
  * **Tamanho do lote**: Olá **writeBatchSize** propriedade define o número de saudação de solicitações em paralelo toohello documentos de toocreate do serviço de banco de dados do Azure Cosmos. Você pode esperar um desempenho melhor quando você aumenta **writeBatchSize** como mais solicitações paralelas são enviadas tooAzure Cosmos DB. No entanto, observe limitação quando você escreve tooAzure Cosmos DB (mensagem de saudação do erro é "Solicitar a taxa é grande"). Vários fatores podem causar limitação, incluindo o tamanho do documento, número de saudação de termos em documentos Olá e Olá política de indexação da coleção de destino. tooachieve maior throughput de cópia, considere o uso de uma coleção melhor, por exemplo, S3.

## <a name="considerations-for-serialization-and-deserialization"></a>Considerações da serialização e desserialização
A serialização e desserialização podem acontecer quando o conjunto de dados de entrada ou saída é um arquivo. Consulte [Formatos de arquivo e compactação com suporte](data-factory-supported-file-and-compression-formats.md) para obter detalhes sobre os formatos de arquivo com suporte na Atividade de Cópia.

**Comportamento da cópia**:

* Copiar arquivos entre os armazenamentos de dados baseados em arquivos:
  * Quando os conjuntos de dados de entrada e saídos têm Olá mesmo ou não as configurações de formato de arquivo, o serviço de movimentação de dados Olá executa uma cópia do binária sem serialização ou desserialização. Você verá um cenário de toohello comparado de taxa de transferência maior, na qual Olá configurações de formato de arquivo de origem e o coletor são diferentes uns dos outros.
  * Quando a entrada e saída conjuntos de dados os dois são no formato de texto e a codificação de saudação somente tipo é diferente, o serviço de movimentação de dados Olá só faz a conversão de codificação. Ela não faz qualquer serialização e desserialização, o que faz com que alguns sobrecarga de desempenho em comparação com cópia de tooa binário.
  * Quando a entrada e saídos conjuntos de dados ambos têm diferentes formatos de arquivos ou configurações diferentes, como delimitadores, Olá serviço de movimentação de dados desserializa toostream de dados de origem, transformação e, em seguida, serializá-lo no formato de saída de hello indicado. Essa operação resulta em uma sobrecarga muito mais significativos de desempenho em comparação com tooother cenários.
* Quando você copia arquivos para/de um repositório de dados que não seja baseado em arquivo (por exemplo, de um armazenamento baseado em arquivo tooa repositório relacional), a etapa de serialização ou desserialização de saudação é necessária. Essa etapa resulta em uma sobrecarga significativa do desempenho.

**Formato de arquivo**: formato de arquivo hello escolhido pode afetar o desempenho de cópia. Por exemplo, Avro é um formato binário compacto que armazena metadados com dados. Ele tem suporte amplo ecossistema de Hadoop Olá para processamento e consulta. No entanto, Avro é mais caro para serialização e desserialização, o que resulta em menor taxa de transferência de cópia em comparação com o formato de tootext. Verifique o formato de arquivo durante a saudação todo o fluxo de processamento de sua escolha. Começar com os dados de saudação do formulário são armazenados no, repositórios de dados ou toobe extraídos dos sistemas externos; de origem melhor formato Olá para armazenamento, processamento analítico e consulta; e, em que formato dados saudação devem ser exportados em armazéns de dados para as ferramentas de relatório e visualização. Às vezes, de um formato de arquivo que está abaixo do ideal para leitura e gravação de desempenho pode ser uma boa opção quando você considera Olá geral analíticos processo.

## <a name="considerations-for-compression"></a>Considerações da compactação
Quando o conjunto de dados de entrada ou saído é um arquivo, você pode definir atividade de cópia tooperform compactação ou descompactação conforme ele grava o destino de toohello de dados. Quando você escolher a compactação, faça uma compensação entre a entrada/saída (E/S) e a CPU. A compactação de dados Olá custos extras em recursos de computação. Mas, por sua vez, reduz a E/S da rede e o armazenamento. Dependendo de seus dados, você poderá ver um aumento na taxa de transferência geral da cópia.

**Codec**: a atividade de cópia suporta gzip, bzip2 e os tipos de compactação Deflate. O Azure HDInsight pode consumir todos os três tipos de processamento. Cada codec de compactação tem suas vantagens. Por exemplo, bzip2 tem a taxa de transferência de cópia de menor hello, mas obter Olá melhor Hive desempenho de consulta com bzip2 porque você pode dividi-lo para processamento. Gzip é a opção de hello mais balanceada e ele é usado com mais frequência hello. Escolha o codec hello mais adequada para seu cenário de ponta a ponta.

**Nível**: você pode escolher entre duas opções para cada codec de compactação: compactado mais rápido e compactado ideal. Hello mais rápida compactada opção compacta dados saudação assim que possível, mesmo se o arquivo resultante Olá ideal não é compactado. Hello opção ideal compactada gasta mais tempo na compactação e produz uma quantidade mínima de dados. Você pode testar toosee ambas as opções que fornece melhor desempenho no seu caso.

**Uma consideração**: toocopy uma grande quantidade de dados entre um repositório local e nuvem hello, considere o uso de armazenamento de blob provisório com a compactação. Usando o armazenamento provisório é útil quando a largura de banda de saudação de sua rede corporativa e os serviços do Azure é o fator limitante Olá e desejar que o conjunto de dados de entrada hello e ambas as toobe do conjunto de dados de saída em formato descompactado. Mais especificamente, é possível dividir uma atividade de cópia única em duas atividades de cópia. Olá primeiro copiar atividade copia da provisória do hello fonte tooan ou preparo blob em formato compactado. atividade de cópia segundo Olá copia dados compactado de saudação do preparo e descompacta enquanto grava toohello coletor.

## <a name="considerations-for-column-mapping"></a>Considerações do mapeamento de coluna
Você pode definir Olá **columnMappings** propriedade na atividade de cópia toomap todos ou um subconjunto de saudação colunas de saída toohello colunas de entrada. Depois que o serviço de movimentação de dados Olá lê dados de saudação de fonte de hello, ele precisa tooperform mapeamento de coluna nos dados de saudação antes de gravar Olá dados toohello coletor. Esse processamento extra reduz a taxa de transferência de cópia.

Se o repositório de dados de origem é passível de consulta, por exemplo, se é um repositório relacional, como banco de dados SQL ou SQL Server, ou se é um repositório NoSQL, como o armazenamento de tabela ou banco de dados do Azure Cosmos, considerar enviar por push Olá filtragem de coluna e reordenação lógica toohello **consulta**  propriedade em vez de usar o mapeamento de coluna. Dessa forma, a projeção de saudação ocorre enquanto o serviço de movimentação de dados Olá lê dos dados de origem de saudação do repositório de dados, onde ele é muito mais eficiente.

## <a name="other-considerations"></a>Outras considerações
Se hello tamanho dos dados que você deseja toocopy é grande, você pode ajustar sua toofurther partição Olá dados de lógica comercial usando Olá dividindo o mecanismo de fábrica de dados. Em seguida, agende atividade de cópia toorun com mais frequência do tamanho dos dados tooreduce Olá para cada atividade de cópia é executado.

Seja cuidadoso ao número de saudação de conjuntos de dados e atividades de cópia que exigem a fábrica de dados tooconnector toohello mesmo repositório de dados em Olá mesmo tempo. Número de trabalhos de cópia simultânea pode limitar um repositório de dados e levar toodegraded desempenho, copie as repetições internas do trabalho e, em alguns casos, falhas de execução.

## <a name="sample-scenario-copy-from-an-on-premises-sql-server-tooblob-storage"></a>Exemplo de cenário: cópia de um armazenamento de tooBlob do SQL Server local
**Cenário**: um pipeline é criado toocopy dados de um armazenamento de tooBlob do SQL Server local no formato CSV. toomake Olá o trabalho de cópia mais rapidamente, os arquivos CSV Olá devem ser compactados no formato bzip2.

**Teste e análise**: taxa de transferência de saudação de atividade de cópia é menor que 2 MBps, que é muito mais lento do que o parâmetro de comparação de desempenho de saudação.

**Análise de desempenho e ajuste**: tootroubleshoot Olá problema de desempenho, vamos dar uma olhada em como os dados de saudação forem processados e movidos.

1. **Ler dados**: Gateway abre uma conexão tooSQL servidor e envia Olá consulta. SQL Server responde enviando Olá tooGateway de fluxo de dados via intranet hello.
2. **Serializar e compactar dados**: Gateway serializa o formato de tooCSV de fluxo de dados hello e compacta Olá bzip2 de tooa TDS.
3. **Gravar dados**: Gateway carrega o armazenamento de tooBlob de fluxo Olá bzip2 via Olá da Internet.

Como você pode ver, dados de saudação estão sendo processados e movidos de maneira sequencial streaming: SQL Server > LAN > Gateway > WAN > armazenamento de Blob. **Olá desempenho geral é retido por taxa de transferência mínima Olá em pipeline Olá**.

![Fluxo de dados](./media/data-factory-copy-activity-performance/case-study-pic-1.png)

Um ou mais dos Olá fatores a seguir podem causar o afunilamento de desempenho hello:

* **Origem:**o próprio SQL Server tem uma baixa taxa de transferência devido às cargas pesadas.
* **Gateway de Gerenciamento de Dados**:
  * **LAN**: Gateway está localizado distantes de máquina do SQL Server hello e tem uma conexão de baixa largura de banda.
  * **Gateway**: Gateway atingiu seu Olá de tooperform carga limitações seguintes operações:
    * **Serialização**: Olá tooCSV de fluxo de dados de serialização formato tem taxa de transferência lenta.
    * **Compactação**: você escolheu um codec de compactação lenta (por exemplo, bzip2, que é 2.8 MBps com Core i7).
  * **WAN**: largura de banda de saudação entre a rede corporativa hello e os serviços do Azure é baixa (por exemplo, T1 = 1,544 kbps; T2 = 6,312 kbps).
* **Coletor**: o armazenamento de Blobs tem baixa taxa de transferência. (Esse cenário é improvável porque seu SLA garante um mínimo de 60 MBps.)

Nesse caso, bzip2 compactação de dados pode ser lento pipeline toda hello. Alternância de codec de compactação gzip tooa pode facilitar esse afunilamento.

## <a name="sample-scenarios-use-parallel-copy"></a>Cenários de exemplo: usar cópia paralela
**Cenário i:** copiar 1.000 arquivos de 1 MB de armazenamento tooBlob de sistema de arquivos do Olá local.

**Análise e ajuste de desempenho**: por exemplo, se você tiver instalado o gateway em um computador quad-core, fábrica de dados usa 16 cópias paralelas toomove arquivos de armazenamento de tooBlob do sistema de arquivo hello simultaneamente. Essa execução paralela deve resultar em alta taxa de transferência. Você também pode especificar explicitamente Olá contagem de cópias paralelas. Ao copiar muitos arquivos pequenos, as cópias paralelas ajudam muito a taxa de transferência usando os recursos com mais eficiência.

![Cenário 1](./media/data-factory-copy-activity-performance/scenario-1.png)

**Cenário II**: copiar 20 blobs de 500 MB de armazenamento de Blob tooData Lake análise de armazenamento e, em seguida, ajustar o desempenho.

**Análise e ajuste de desempenho**: nesse cenário, fábrica de dados copia dados de saudação do repositório do Blob storage tooData Lake usando cópia única (**parallelCopies** definir too1) e unidades de movimentação de dados de nuvem único. Olá taxa de transferência você observar vai ser fechar toothat descrito em hello [seção de referência de desempenho](#performance-reference).   

![Cenário 2](./media/data-factory-copy-activity-performance/scenario-2.png)

**Cenário III**: o tamanho de arquivo Individual é maior que dezenas de MBs e o volume total é grande.

**Análise e ajuste de desempenho**: aumentando **parallelCopies** não resulta em um melhor desempenho de cópia devido a limitações de recursos de saudação do DMU de — única nuvem. Em vez disso, você deve especificar mais nuvem DMUs tooget mais recursos tooperform Olá a movimentação de dados. Não especifique um valor para Olá **parallelCopies** propriedade. Fábrica de dados controla o paralelismo Olá para você. Nesse caso, se você definir **cloudDataMovementUnits** too4, uma taxa de transferência sobre quatro vezes ocorre.

![Cenário 3](./media/data-factory-copy-activity-performance/scenario-3.png)

## <a name="reference"></a>Referência
Aqui estão monitoramento de desempenho e ajuste as referências para alguns armazenamentos de dados de saudação com suporte:

* Armazenamento do Azure (incluindo o armazenamento de Blobs e o armazenamento de Tabelas): [metas de escalabilidade do Armazenamento do Azure](../storage/common/storage-scalability-targets.md) e [Lista de verificação de escalabilidade e desempenho do Armazenamento do Azure](../storage/common/storage-performance-checklist.md)
* Banco de dados SQL do Azure: Você pode [monitorar o desempenho de saudação](../sql-database/sql-database-single-database-monitor.md) e verifica a porcentagem DTU (unidade) de transação de banco de dados de saudação
* SQL Data Warehouse do Azure: Sua capacidade é medida em unidades de data warehouse (DWUs); consulte [Gerenciar poder de computação no SQL Data Warehouse do Azure (Visão Geral)](../sql-data-warehouse/sql-data-warehouse-manage-compute-overview.md)
* Azure Cosmos DB: [níveis de desempenho no Azure Cosmos DB](../documentdb/documentdb-performance-levels.md)
* SQL Server local: [monitoramento e ajuste do desempenho](https://msdn.microsoft.com/library/ms189081.aspx)
* Servidor de arquivos local: [ajuste de desempenho para servidores de arquivos](https://msdn.microsoft.com/library/dn567661.aspx)
