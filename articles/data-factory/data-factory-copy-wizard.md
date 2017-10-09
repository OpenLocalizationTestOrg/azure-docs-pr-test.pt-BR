---
title: "dados de aaaCopy facilmente com o Assistente para cópia - Azure | Microsoft Docs"
description: "Saiba mais sobre como toouse Olá dados do Assistente para cópia de fábrica de dados toocopy de toosinks de fontes de dados com suporte."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f904972f-cd33-48db-9755-2b3196ae4168
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 99437ec16facf3b94c8be18487ec89e9f13acc9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-or-move-data-easily-with-azure-data-factory-copy-wizard"></a>Copiar ou mover dados facilmente com o Assistente de Cópia do Azure Data Factory
Olá Assistente para cópia de fábrica de dados do Azure é o processo de saudação de tooease de ingestão de dados, o que geralmente é uma primeira etapa em um cenário de integração de dados de ponta a ponta. Ao passar por Olá Assistente para cópia de fábrica de dados do Azure, não é necessário toounderstand quaisquer definições de JSON para pipelines, conjuntos de dados e serviços vinculados. No entanto, depois de concluir todas as etapas de saudação no assistente Olá, o Assistente de saudação cria automaticamente um toocopy de dados do pipeline do destino selecionado de toohello Olá de fonte dados selecionados. Além disso, Olá cópia assistente ajuda você a dados de saudação do toovalidate que estão sendo incluídos no tempo de saudação de criação, que salva muito tempo, especialmente quando você estiver ingestão de dados para Olá primeira vez Olá da fonte de dados. Olá toostart Assistente para cópia, clique em Olá **copiar dados** bloco Olá home page de sua fábrica de dados.

![Assistente de Cópia](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="an-intuitive-wizard-for-copying-data"></a>Um assistente intuitivo para copiar dados
Este assistente permite que você tooeasily mover dados de uma ampla variedade de fontes toodestinations em minutos. Depois de concluir o Assistente de saudação, um pipeline com uma atividade de cópia é criado automaticamente para você junto com entidades dependentes da fábrica de dados (serviços vinculados e conjuntos de dados). Nenhuma etapa adicional é necessário toocreate pipeline de saudação.   

![Selecione uma fonte de dados](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Consulte [tutorial do Assistente para cópia](data-factory-copy-data-wizard-tutorial.md) do artigo para obter instruções passo a passo toocreate dados toocopy de pipeline de exemplo de uma tabela de banco de dados SQL do tooan de BLOBs do Azure. 
> 
> 

Assistente de saudação foi projetado com dados grandes em mente a partir do início da saudação. É simples e eficiente tooauthor pipelines de fábrica de dados que se movem centenas de pastas, arquivos ou tabelas usando o Assistente para copiar dados de saudação. Olá assistente dá suporte a saudação três recursos a seguir: visualização de dados automática, captura de esquema e o mapeamento e filtragem de dados. 

## <a name="automatic-data-preview"></a>Visualização automática de dados
Assistente para cópia de saudação permite que você tooreview parte de dados Olá Olá fonte de dados selecionada para você toovalidate se os dados Olá Olá direita dados que você deseja toocopy. Além disso, se os dados de origem Olá estiverem em um arquivo de texto, o Assistente para cópia de saudação analisa esquema e delimitadores de coluna e linha de toolearn do arquivo de texto de saudação automaticamente. 

![Configurações de formato de arquivo](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Captura e mapeamento do esquema
esquema de saudação de dados de entrada pode corresponde Olá esquema dos dados de saída em alguns casos. Nesse cenário, você precisa toomap colunas Olá toocolumns de esquema de origem do esquema de destino de saudação. 

Assistente para cópia de saudação mapeia automaticamente colunas em Olá toocolumns de esquema de origem no esquema de destino hello. Você pode substituir mapeamentos hello usando listas suspensas de saudação (ou) especificar se uma coluna precisa toobe ignorado ao copiar dados de saudação.   

![Mapeamento de esquema](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Filtrando dados
Assistente de saudação permite toofilter dados tooselect somente Olá dados de origem que precisa de armazenamento de dados de destino/coletor de toohello toobe copiado. Filtragem reduz o volume de saudação do hello toobe toohello copiado coletor de dados de repositório de dados e, portanto, melhora a taxa de transferência de saudação da operação de cópia de saudação. Fornece dados de toofilter uma maneira flexível em um banco de dados relacional usando SQL query language (ou) arquivos em uma pasta de BLOBs do Azure usando [variáveis e funções da fábrica de dados](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Filtragem de dados em um banco de dados
No exemplo hello, consulta SQL Olá usa Olá `Text.Format` função e `WindowStart` variável. 

![Validar expressões](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Filtragem de dados em uma pasta de blobs do Azure
Você pode usar variáveis em dados toocopy de caminho de pasta saudação de uma pasta que é determinado em tempo de execução com base em [variáveis de sistema](data-factory-functions-variables.md#data-factory-system-variables). variáveis de saudação com suporte são: **{year}**, **{month}**, **{day}**, **{hora}**, **{minuto}**, e **{personalizado}**. Exemplo: pastadeentrada/{ano}/{mês}/{dia}.

Suponha que ter entrada pastas no hello formato a seguir:

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Clique em Olá **procurar** botão para **arquivo ou pasta**, procurar tooone dessas pastas (por exemplo, 2016 -> 03 -> 01 -> 02) e clique em **escolha**. Você deve ver `2016/03/01/02` na caixa de texto de saudação. Agora, substitua **2016** por **{ano}**, **03** por **{mês}**, **01** por **{dia}**, **02** por **{hora}** e pressione Tab. Você deve ver o formato de saudação tooselect listas suspensas para esse quatro variáveis:

![Usando variáveis de sistema](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Conforme mostrado na Olá captura de tela a seguir, você também pode usar um **personalizado** variável e qualquer [suporte para cadeias de caracteres de formato](https://msdn.microsoft.com/library/8kb3ddd4.aspx). tooselect uma pasta com a estrutura, use Olá **procurar** botão primeiro. Em seguida, substituir um valor com **{personalizado}**e pressione a caixa de texto do guia toosee Olá onde você pode digitar a cadeia de caracteres de formato de saudação.     

![Usando variáveis personalizadas](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="support-for-diverse-data-and-object-types"></a>Suporte para tipos de dados e objetos diversificados
Usando Olá Assistente para cópia, você pode mover com eficiência centenas de pastas, arquivos ou tabelas.

![Selecionar tabelas de quais dados toocopy](./media/data-factory-copy-wizard/select-tables-to-copy-data.png)

## <a name="scheduling-options"></a>Opções de agendamento
Você pode executar operação de cópia Olá uma vez ou em uma agenda (por hora, diariamente, e assim por diante). Ambas as opções podem ser usadas para amplitude Olá conectores Olá entre locais, a nuvem e a cópia local de área de trabalho.

Uma operação de cópia única permite a movimentação de dados de uma origem tooa destino apenas uma vez. Ele se aplica a toodata de qualquer tamanho e em qualquer formato com suporte. Olá agendado copy permite toocopy dados em uma recorrência prescrita. Você pode usar configurações avançadas (como alertas, tempo limite e repetição) tooconfigure Olá agendado cópia.

![Propriedades de agendamento](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Próximas etapas
Para uma rápida explicação passo a passo do usando o Assistente para cópia de fábrica de dados de saudação toocreate um pipeline com atividade de cópia, consulte [Tutorial: criar um pipeline usando o Assistente para cópia de saudação](data-factory-copy-data-wizard-tutorial.md).

