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
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="dee55-103">Desenvolver UDOs (operadores definidos pelo usuário) do U-SQL</span><span class="sxs-lookup"><span data-stu-id="dee55-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="dee55-104">Saiba como toodevelop definida pelo usuário dados de tooprocess operadores em um trabalho de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="dee55-104">Learn how toodevelop user-defined operators tooprocess data in a U-SQL job.</span></span>

<span data-ttu-id="dee55-105">Para obter instruções para desenvolver assemblies de uso geral para U-SQL, consulte [Desenvolver assemblies U-SQL para trabalhos do Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md)</span><span class="sxs-lookup"><span data-stu-id="dee55-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="dee55-106">Definir e usar o operador definido pelo usuário no U-SQL</span><span class="sxs-lookup"><span data-stu-id="dee55-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="dee55-107">**toocreate e enviar um trabalho de U-SQL**</span><span class="sxs-lookup"><span data-stu-id="dee55-107">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="dee55-108">Olá Visual Studio selecione **arquivo > Novo > projeto > projeto U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="dee55-108">From hello Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="dee55-109">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="dee55-109">Click **OK**.</span></span> <span data-ttu-id="dee55-110">O Visual Studio cria uma solução com um arquivo Script.usql.</span><span class="sxs-lookup"><span data-stu-id="dee55-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="dee55-111">No **Gerenciador de Soluções**, expanda Script.usql e clique duas vezes em **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="dee55-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="dee55-112">Cole Olá código a seguir no arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="dee55-112">Paste hello following code into hello file:</span></span>

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
6. <span data-ttu-id="dee55-113">Abra **Script.usql**, e colar Olá script U-SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="dee55-113">Open **Script.usql**, and paste hello following U-SQL script:</span></span>

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
7. <span data-ttu-id="dee55-114">Especifique a conta de análise Data Lake hello, banco de dados e esquema.</span><span class="sxs-lookup"><span data-stu-id="dee55-114">Specify hello Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="dee55-115">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Script.usql** e clique em **Criar Script**.</span><span class="sxs-lookup"><span data-stu-id="dee55-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="dee55-116">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Script.usql** e clique em **Enviar Script**.</span><span class="sxs-lookup"><span data-stu-id="dee55-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="dee55-117">Se você ainda não tiver conectado tooyour assinatura do Azure, você vai ser tooenter solicitada as credenciais de conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="dee55-117">If you haven't connected tooyour Azure subscription, you will be prompted tooenter your Azure account credentials.</span></span>
11. <span data-ttu-id="dee55-118">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="dee55-118">Click **Submit**.</span></span> <span data-ttu-id="dee55-119">Resultados de envio e o link de trabalho estão disponíveis na janela de resultados de saudação quando o envio de saudação é concluído.</span><span class="sxs-lookup"><span data-stu-id="dee55-119">Submission results and job link are available in hello Results window when hello submission is completed.</span></span>
12. <span data-ttu-id="dee55-120">Clique em Olá **atualização** botão toosee hello mais recente trabalho status e a atualização de tela hello.</span><span class="sxs-lookup"><span data-stu-id="dee55-120">Click hello **Refresh** button toosee hello latest job status and refresh hello screen.</span></span>

<span data-ttu-id="dee55-121">**saída de hello toosee**</span><span class="sxs-lookup"><span data-stu-id="dee55-121">**toosee hello output**</span></span>

1. <span data-ttu-id="dee55-122">De **Server Explorer**, expanda **Azure**, expanda **análise Data Lake**, expanda sua conta da análise Data Lake, expanda **ascontasdearmazenamento**, com o botão direito Olá armazenamento padrão e, em seguida, clique em **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="dee55-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="dee55-123">Expanda Exemplos, expanda Saídas e clique duas vezes em **Drivers.csv**.</span><span class="sxs-lookup"><span data-stu-id="dee55-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="dee55-124">Confira também</span><span class="sxs-lookup"><span data-stu-id="dee55-124">See also</span></span>
* [<span data-ttu-id="dee55-125">Introdução à Análise Data Lake usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="dee55-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="dee55-126">Introdução à análise Data Lake usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dee55-126">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="dee55-127">Usar as Ferramentas do Data Lake para Visual Studio para desenvolver aplicativos do U-SQL</span><span class="sxs-lookup"><span data-stu-id="dee55-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
