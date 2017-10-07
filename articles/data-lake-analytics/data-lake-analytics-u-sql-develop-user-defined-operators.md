---
title: "operadores de aaaDevelop U-SQL definida pelo usuário (UDOs) | Microsoft Docs"
description: "Saiba como toodevelop operadores definidos pelo usuário toobe usado e reutilizado em análise Data Lake trabalhos. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: e5189e4e-9438-46d1-8686-ed4836bf3356
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 6b86618efd3751cd9a5e91875879d7dd6d6a7b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a>Desenvolver UDOs (operadores definidos pelo usuário) do U-SQL
Saiba como toodevelop definida pelo usuário dados de tooprocess operadores em um trabalho de U-SQL.

Para obter instruções para desenvolver assemblies de uso geral para U-SQL, consulte [Desenvolver assemblies U-SQL para trabalhos do Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md)

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a>Definir e usar o operador definido pelo usuário no U-SQL
**toocreate e enviar um trabalho de U-SQL**

1. Olá Visual Studio selecione **arquivo > Novo > projeto > projeto U-SQL**.
2. Clique em **OK**. O Visual Studio cria uma solução com um arquivo Script.usql.
3. No **Gerenciador de Soluções**, expanda Script.usql e clique duas vezes em **Script.usql.cs**.
4. Cole Olá código a seguir no arquivo hello:

        using Microsoft.Analytics.Interfaces;
        using System.Collections.Generic;

        namespace USQL_UDO
        {
            public class CountryName : IProcessor
            {
                private static IDictionary<string, string> CountryTranslation = new Dictionary<string, string>
                {
                    {
                        "Deutschland", "Germany"
                    },
                    {
                        "Suisse", "Switzerland"
                    },
                    {
                        "UK", "United Kingdom"
                    },
                    {
                        "USA", "United States of America"
                    },
                    {
                        "中国", "PR China"
                    }
                };

                public override IRow Process(IRow input, IUpdatableRow output)
                {

                    string UserID = input.Get<string>("UserID");
                    string Name = input.Get<string>("Name");
                    string Address = input.Get<string>("Address");
                    string City = input.Get<string>("City");
                    string State = input.Get<string>("State");
                    string PostalCode = input.Get<string>("PostalCode");
                    string Country = input.Get<string>("Country");
                    string Phone = input.Get<string>("Phone");

                    if (CountryTranslation.Keys.Contains(Country))
                    {
                        Country = CountryTranslation[Country];
                    }
                    output.Set<string>(0, UserID);
                    output.Set<string>(1, Name);
                    output.Set<string>(2, Address);
                    output.Set<string>(3, City);
                    output.Set<string>(4, State);
                    output.Set<string>(5, PostalCode);
                    output.Set<string>(6, Country);
                    output.Set<string>(7, Phone);

                    return output.AsReadOnly();
                }
            }
        }
6. Abra **Script.usql**, e colar Olá script U-SQL a seguir:

        @drivers =
            EXTRACT UserID      string,
                    Name        string,
                    Address     string,
                    City        string,
                    State       string,
                    PostalCode  string,
                    Country     string,
                    Phone       string
            FROM "/Samples/Data/AmbulanceData/Drivers.txt"
            USING Extractors.Tsv(Encoding.Unicode);

        @drivers_CountryName =
            PROCESS @drivers
            PRODUCE UserID string,
                    Name string,
                    Address string,
                    City string,
                    State string,
                    PostalCode string,
                    Country string,
                    Phone string
            USING new USQL_UDO.CountryName();    

        OUTPUT @drivers_CountryName
            too"/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. Especifique a conta de análise Data Lake hello, banco de dados e esquema.
8. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Script.usql** e clique em **Criar Script**.
9. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Script.usql** e clique em **Enviar Script**.
10. Se você ainda não tiver conectado tooyour assinatura do Azure, você vai ser tooenter solicitada as credenciais de conta do Azure.
11. Clique em **Enviar**. Resultados de envio e o link de trabalho estão disponíveis na janela de resultados de saudação quando o envio de saudação é concluído.
12. Clique em Olá **atualização** botão toosee hello mais recente trabalho status e a atualização de tela hello.

**saída de hello toosee**

1. De **Server Explorer**, expanda **Azure**, expanda **análise Data Lake**, expanda sua conta da análise Data Lake, expanda **ascontasdearmazenamento**, com o botão direito Olá armazenamento padrão e, em seguida, clique em **Explorer**.
2. Expanda Exemplos, expanda Saídas e clique duas vezes em **Drivers.csv**.

## <a name="see-also"></a>Confira também
* [Introdução à Análise Data Lake usando o PowerShell](data-lake-analytics-get-started-powershell.md)
* [Introdução à análise Data Lake usando Olá portal do Azure](data-lake-analytics-get-started-portal.md)
* [Usar as Ferramentas do Data Lake para Visual Studio para desenvolver aplicativos do U-SQL](data-lake-analytics-data-lake-tools-get-started.md)
