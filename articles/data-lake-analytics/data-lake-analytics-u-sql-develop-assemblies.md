---
title: "assemblies aaaDevelop U-SQL para trabalhos de análise do Azure Data Lake | Microsoft Docs"
description: "Saiba como toodevelop assemblies toobe usado e reutilizado em análise Data Lake trabalhos. "
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: 86dd17b25e0967306ed36bb5b7f3178d9409d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a>Desenvolver assemblies do U-SQL para trabalhos do Azure Data Lake Analytics
Saiba como tooturn por trás do código em assemblies toobe usado e reutilizado em trabalhos da análise Data Lake. 

U-SQL torna fácil tooadd próprios e personalizados de código em linguagens .net, como c#, VB.Net ou F #. Você ainda pode implantar sua própria toosupport de tempo de execução outras linguagens.

Olá mais fácil maneira toouse código personalizado é toouse Olá Data Lake Tools para recursos de por trás do código do Visual Studio. Para obter mais informações, consulte o [Tutorial: desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). Há algumas desvantagens em usar code-behind:

- código-fonte Olá é carregado para o envio de cada script.
- O code-behind não pode ser compartilhado com outros trabalhos.

tooaddress essas desvantagens, você pode transformar por trás do código em assemblies e registrar o catálogo do hello assemblies toohello análise Data Lake.

## <a name="prerequisites"></a>Pré-requisitos
* Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 atualização 4 ou Visual Studio 2012 com Visual C++ instalado
* SDK do Microsoft Azure para .NET versão 2.5 ou posterior.  Instale-o usando o instalador de plataforma da Web hello ou o instalador do Visual Studio
* Uma conta da Análise Data Lake.  Confira [Introdução ao Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-get-started-portal.md).
* Passar Olá [Introdução ao Azure Data Lake análise U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.
* Conecte-se tooAzure.
* Carregar dados de origem hello, consulte [Introdução ao Azure Data Lake análise U-SQL Studio](data-lake-analytics-u-sql-get-started.md). 

## <a name="develop-assemblies-for-u-sql"></a>Desenvolver assemblies para U-SQL

**toocreate e enviar um trabalho de U-SQL**

1. De saudação **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.
2. Expanda **instalado**, **modelos**, **Azure Data Lake**, **U-SQL(ADLA)**, selecione Olá **biblioteca de classes (para U-SQL Aplicativo)** modelo e depois clique em **Okey**.
3. Escreva seu código em Class1.cs.  a seguir Olá é um exemplo de código.

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. Clique em Olá **criar** menu e clique **compilar solução** toocreate Olá dll.

## <a name="register-assemblies"></a>Registrar assemblies

Veja [Usar o catálogo do Data Lake Analytics (U-SQL)](data-lake-analytics-use-u-sql-catalog.md).


## <a name="use-hello-assemblies"></a>Usar assemblies Olá

Consulte [usar hello Azure Data Lake Tools para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).

## <a name="see-also"></a>Consulte também
* [Introdução à Análise Data Lake usando o PowerShell](data-lake-analytics-get-started-powershell.md)
* [Introdução à análise Data Lake usando Olá portal do Azure](data-lake-analytics-get-started-portal.md)
* [Usar as Ferramentas do Data Lake para Visual Studio para desenvolver aplicativos do U-SQL](data-lake-analytics-data-lake-tools-get-started.md)
* [Usar o catálogo do Data Lake Analytics (U-SQL)](data-lake-analytics-use-u-sql-catalog.md)
* [Use hello Azure Data Lake Tools para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)
