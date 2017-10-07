---
title: "aaaData Assistente de cópia de fábrica do Azure | Microsoft Docs"
description: "Saiba mais sobre como toouse Olá dados do Assistente para cópia do Data Factory do Azure toocopy de toosinks de fontes de dados com suporte."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 0974eb40-db98-4149-a50d-48db46817076
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 188b3ae15f937b84a58aec1b979347ac8090abf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory-copy-wizard"></a>Assistente de Cópia do Azure Data Factory
Olá Assistente para cópia de fábrica de dados do Azure facilita o processo de saudação de ingestão de dados, o que geralmente é uma primeira etapa em um cenário de integração de dados de ponta a ponta. Ao passar por Olá Assistente para cópia de fábrica de dados do Azure, não é necessário toounderstand quaisquer definições de JSON para serviços vinculados, conjuntos de dados e pipelines. Assistente de saudação cria automaticamente um toocopy de dados do pipeline de destino selecionado de toohello Olá de fonte dados selecionados. Além disso, Olá Assistente para cópia de ajuda dados de saudação toovalidate sendo incluídos no tempo de saudação de criação. Isso economiza tempo, especialmente quando você estiver ingestão de dados para Olá primeira vez Olá da fonte de dados. Olá toostart Assistente para cópia, clique em Olá **copiar dados** bloco Olá home page de sua fábrica de dados.

![Assistente de Cópia](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="designed-for-big-data"></a>Projetado para Big Data
Este assistente permite que você tooeasily mover dados de uma ampla variedade de fontes toodestinations em minutos. Depois que você percorrer o assistente hello, um pipeline com uma atividade de cópia é criado automaticamente para você, juntamente com entidades dependentes da fábrica de dados (serviços vinculados e conjuntos de dados). Nenhuma etapa adicional é necessário toocreate pipeline de saudação.   

![Selecione uma fonte de dados](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Para obter instruções passo a passo toocreate dados toocopy de pipeline de exemplo de uma tabela de banco de dados SQL do tooan de BLOBs do Azure, consulte Olá [tutorial do Assistente para copiar](data-factory-copy-data-wizard-tutorial.md).
>
>

Assistente de saudação foi projetado com dados grandes em mente a partir do início do hello, com suporte para vários tipos de dados e objeto. Você pode criar pipelines do Data Factory que movem centenas de pastas, arquivos ou tabelas. Assistente de saudação dá suporte à visualização de dados automática, captura de esquema e o mapeamento e a filtragem de dados.

## <a name="automatic-data-preview"></a>Visualização automática de dados
Você pode visualizar a parte dos dados de saudação da fonte de dados selecionada Olá em ordem toovalidate se dados saudação são que você deseja toocopy. Além disso, se os dados de origem Olá estiverem em um arquivo de texto, Assistente para cópia de saudação analisa delimitadores de coluna e linha de saudação toolearn do arquivo de texto hello e o esquema automaticamente.

![Configurações de formato de arquivo](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Captura e mapeamento do esquema
esquema de saudação de dados de entrada pode corresponde Olá esquema dos dados de saída em alguns casos. Nesse cenário, você precisa toomap colunas Olá toocolumns de esquema de origem do esquema de destino de saudação.

> [!TIP]
> Quando copiar dados do SQL Server ou banco de dados SQL Azure no Azure SQL Data Warehouse, se a tabela de saudação não existe no repositório de destino hello, fábrica de dados oferecem suporte a criação de tabela automática usando o esquema da fonte. Saiba mais no [mover tooand de dados de uso do Azure Data Factory do Azure SQL Data Warehouse](./data-factory-azure-sql-data-warehouse-connector.md).
>

Use uma lista suspensa de tooselect uma coluna da coluna de tooa Olá origem esquema toomap no esquema de destino hello. Assistente para cópia de saudação tenta toounderstand seu padrão para mapeamento de coluna. Ele se aplica Olá rest mesmo toohello de padrão de colunas hello, para que você não precisa tooselect colunas Olá individualmente mapeamento de esquema toocomplete hello. Se preferir, você pode substituir esses mapeamentos usando Olá listas suspensas toomap Olá colunas uma a uma. padrão de saudação se torna mais precisa, conforme você mapear as colunas mais. Olá Assistente para cópia atualiza constantemente padrão hello e finalmente atingir Olá direito padrão para a coluna Olá mapeamento que você deseja tooachieve.     

![Mapeamento de esquema](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Filtrando dados
Você pode filtrar dados tooselect somente Olá dados de origem que precisa de armazenamento de dados do coletor de toohello de toobe copiado. Filtragem reduz o volume de saudação do hello toobe toohello copiado coletor de dados de repositório de dados e, portanto, melhora a taxa de transferência de saudação da operação de cópia de saudação. Ele fornece dados de toofilter uma maneira flexível em um banco de dados relacional usando a linguagem de consulta SQL hello ou arquivos em uma pasta de BLOBs do Azure usando [variáveis e funções da fábrica de dados](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Filtragem de dados em um banco de dados
Olá, seguinte captura de tela mostra uma consulta SQL usando Olá `Text.Format` função e `WindowStart` variável.

![Validar expressões](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Filtragem de dados em uma pasta de blobs do Azure
Você pode usar variáveis em dados toocopy de caminho de pasta saudação de uma pasta que é determinado em tempo de execução com base em [variáveis de sistema](data-factory-functions-variables.md#data-factory-system-variables). variáveis de saudação com suporte são: **{year}**, **{month}**, **{day}**, **{hora}**, **{minuto}**, e **{personalizado}**. Por exemplo: pastadeentrada/{ano}/{mês}/{dia}.

Suponha que ter entrada pastas no hello formato a seguir:

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Clique em Olá **procurar** botão para **arquivo ou pasta**, procurar tooone dessas pastas (por exemplo, 2016 -> 03 -> 01 -> 02) e clique em **escolha**. Você deve ver `2016/03/01/02` na caixa de texto de saudação. Agora, substitua **2016** com **{year}**, **03** com **{month}**, **01** com **{day}** , e **02** com **{hora}**e pressione hello **guia** chave. Você deve ver o formato de saudação tooselect listas suspensas para esse quatro variáveis:

![Usando variáveis de sistema](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Conforme mostrado na Olá captura de tela a seguir, você também pode usar um **personalizado** variável e qualquer [suporte para cadeias de caracteres de formato](https://msdn.microsoft.com/library/8kb3ddd4.aspx). tooselect uma pasta com a estrutura, use Olá **procurar** botão primeiro. Em seguida, substituir um valor com **{personalizado}**e pressione hello **guia** toosee chave caixa de texto de saudação onde você pode digitar a cadeia de caracteres de formato de saudação.     

![Usando variáveis personalizadas](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="scheduling-options"></a>Opções de agendamento
Você pode executar operação de cópia Olá uma vez ou em uma agenda (por hora, diariamente, e assim por diante). Ambas as opções podem ser usadas para profundo Olá conectores Olá em ambientes, inclusive local, a nuvem e a cópia local de área de trabalho.

Uma operação de cópia única permite a movimentação de dados de uma origem tooa destino apenas uma vez. Ele se aplica a toodata de qualquer tamanho e em qualquer formato com suporte. Olá agendado copy permite toocopy dados em uma recorrência prescrita. Você pode usar configurações avançadas (como alertas, tempo limite e repetição) tooconfigure Olá agendado cópia.

![Propriedades de agendamento](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Próximas etapas
Para uma rápida explicação passo a passo do usando o Assistente para cópia de fábrica de dados de saudação toocreate um pipeline com atividade de cópia, consulte [Tutorial: criar um pipeline usando o Assistente para cópia de saudação](data-factory-copy-data-wizard-tutorial.md).
