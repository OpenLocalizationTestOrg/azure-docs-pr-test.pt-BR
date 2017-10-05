---
title: "Desenvolver UDOs (operadores definidos pelo usuário) do U-SQL | Microsoft Docs"
description: "Saiba como desenvolver operadores definidos pelo usuário para serem usados e reutilizados em trabalhos do Data Lake Analytics. "
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
ms.openlocfilehash: fdee02fb60b633c26704fc1774dfc3a7825b5e0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="60c3b-103">Desenvolver UDOs (operadores definidos pelo usuário) do U-SQL</span><span class="sxs-lookup"><span data-stu-id="60c3b-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="60c3b-104">Saiba como desenvolver operadores definidos pelo usuário para processar dados em um trabalho do U-SQL.</span><span class="sxs-lookup"><span data-stu-id="60c3b-104">Learn how to develop user-defined operators to process data in a U-SQL job.</span></span>

<span data-ttu-id="60c3b-105">Para obter instruções para desenvolver assemblies de uso geral para U-SQL, consulte [Desenvolver assemblies U-SQL para trabalhos do Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md)</span><span class="sxs-lookup"><span data-stu-id="60c3b-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="60c3b-106">Definir e usar o operador definido pelo usuário no U-SQL</span><span class="sxs-lookup"><span data-stu-id="60c3b-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="60c3b-107">**Para criar e enviar um trabalho do U-SQL**</span><span class="sxs-lookup"><span data-stu-id="60c3b-107">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="60c3b-108">No Visual Studio, selecione **Arquivo > Novo > Projeto > Projeto U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="60c3b-108">From the Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="60c3b-109">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="60c3b-109">Click **OK**.</span></span> <span data-ttu-id="60c3b-110">O Visual Studio cria uma solução com um arquivo Script.usql.</span><span class="sxs-lookup"><span data-stu-id="60c3b-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="60c3b-111">No **Gerenciador de Soluções**, expanda Script.usql e clique duas vezes em **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="60c3b-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="60c3b-112">Cole o seguinte código no arquivo:</span><span class="sxs-lookup"><span data-stu-id="60c3b-112">Paste the following code into the file:</span></span>

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
6. <span data-ttu-id="60c3b-113">Abra o **Script.usql** e cole o seguinte script U-SQL:</span><span class="sxs-lookup"><span data-stu-id="60c3b-113">Open **Script.usql**, and paste the following U-SQL script:</span></span>

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
            TO "/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. <span data-ttu-id="60c3b-114">Especifique a conta da Análise do Data Lake, o Banco de Dados e o Esquema.</span><span class="sxs-lookup"><span data-stu-id="60c3b-114">Specify the Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="60c3b-115">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Script.usql** e clique em **Criar Script**.</span><span class="sxs-lookup"><span data-stu-id="60c3b-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="60c3b-116">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Script.usql** e clique em **Enviar Script**.</span><span class="sxs-lookup"><span data-stu-id="60c3b-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="60c3b-117">Se você ainda não tiver se conectado à sua assinatura do Azure, será solicitado a inserir as credenciais de conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="60c3b-117">If you haven't connected to your Azure subscription, you will be prompted to enter your Azure account credentials.</span></span>
11. <span data-ttu-id="60c3b-118">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="60c3b-118">Click **Submit**.</span></span> <span data-ttu-id="60c3b-119">Os resultados do envio e o link do trabalho estarão disponíveis na janela Resultados quando o envio for concluído.</span><span class="sxs-lookup"><span data-stu-id="60c3b-119">Submission results and job link are available in the Results window when the submission is completed.</span></span>
12. <span data-ttu-id="60c3b-120">Clique no botão **Atualizar** para ver o status do trabalho mais recente e atualizar a tela.</span><span class="sxs-lookup"><span data-stu-id="60c3b-120">Click the **Refresh** button to see the latest job status and refresh the screen.</span></span>

<span data-ttu-id="60c3b-121">**Para ver a saída**</span><span class="sxs-lookup"><span data-stu-id="60c3b-121">**To see the output**</span></span>

1. <span data-ttu-id="60c3b-122">No **Gerenciador de Servidores**, expanda **Azure**, expanda **Data Lake Analytics**, expanda sua conta do Data Lake Analytics, expanda **Contas de Armazenamento**, clique com o botão direito do mouse no Armazenamento Padrão e clique em **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="60c3b-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="60c3b-123">Expanda Exemplos, expanda Saídas e clique duas vezes em **Drivers.csv**.</span><span class="sxs-lookup"><span data-stu-id="60c3b-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="60c3b-124">Confira também</span><span class="sxs-lookup"><span data-stu-id="60c3b-124">See also</span></span>
* [<span data-ttu-id="60c3b-125">Introdução à Análise Data Lake usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="60c3b-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="60c3b-126">Introdução à Análise Data Lake usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="60c3b-126">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="60c3b-127">Usar as Ferramentas do Data Lake para Visual Studio para desenvolver aplicativos do U-SQL</span><span class="sxs-lookup"><span data-stu-id="60c3b-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
