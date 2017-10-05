---
title: "Validar XML – Aplicativo Lógico do Azure | Microsoft Docs"
description: "Validar XML com esquemas para o Aplicativo Lógico do Azure e cenários B2B usando o Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8558efffa354cc4bb93820c837077ee997924c95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="9164a-103">Validar XML para integração corporativa</span><span class="sxs-lookup"><span data-stu-id="9164a-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="9164a-104">Geralmente, em cenários B2B, os parceiros de um contrato devem garantir que as mensagens trocadas entre eles são válidas antes de iniciar o processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="9164a-104">Often in B2B scenarios, the partners in an agreement must make sure that the messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="9164a-105">É possível validar documentos com um esquema predefinido usando o conector de Validação de XML do Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="9164a-105">You can validate documents against a predefined schema by using the use the XML Validation connector in the Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-the-xml-validation-connector"></a><span data-ttu-id="9164a-106">Validar um documento com o conector de Validação de XML</span><span class="sxs-lookup"><span data-stu-id="9164a-106">Validate a document with the XML Validation connector</span></span>

1. <span data-ttu-id="9164a-107">Crie um aplicativo lógico e [vincule-o à sua conta de integração](../logic-apps/logic-apps-enterprise-integration-accounts.md "Saiba como vincular uma conta de integração a um Aplicativo lógico") que contém o esquema que você deseja usar para validar os dados XML.</span><span class="sxs-lookup"><span data-stu-id="9164a-107">Create a logic app, and [link the app to the integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that has the schema you want to use for validating XML data.</span></span>

2. <span data-ttu-id="9164a-108">Adicione um gatilho **Solicitação - quando uma solicitação HTTP é recebida** ao seu Aplicativo Lógico.</span><span class="sxs-lookup"><span data-stu-id="9164a-108">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="9164a-109">Para adicionar a ação de **Validação de XML**, escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="9164a-109">To add the **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="9164a-110">Para filtrar todas as ações para aquela que você deseja usar, insira *xml* na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9164a-110">To filter all the actions to the one that you want, enter *xml* in the search box.</span></span> <span data-ttu-id="9164a-111">Escolha **Validação de XML**.</span><span class="sxs-lookup"><span data-stu-id="9164a-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="9164a-112">Para especificar o conteúdo XML que você deseja validar, selecione **CONTEÚDO**.</span><span class="sxs-lookup"><span data-stu-id="9164a-112">To specify the XML content that you want to validate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="9164a-113">Selecione a marca body como o conteúdo que você deseja validar.</span><span class="sxs-lookup"><span data-stu-id="9164a-113">Select the body tag as the content that you want to validate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="9164a-114">Para especificar o esquema desejado a fim de validar a entrada de *conteúdo* anterior, escolha **NOME DO ESQUEMA**.</span><span class="sxs-lookup"><span data-stu-id="9164a-114">To specify the schema you want to use for validating the previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="9164a-115">Salve seu trabalho </span><span class="sxs-lookup"><span data-stu-id="9164a-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="9164a-116">Agora, a configuração do conector de validação foi concluída.</span><span class="sxs-lookup"><span data-stu-id="9164a-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="9164a-117">Em um aplicativo real, convém armazenar os dados validados em um aplicativo LOB (de linha de negócios), como o SalesForce.</span><span class="sxs-lookup"><span data-stu-id="9164a-117">In a real world application, you might want to store the validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="9164a-118">Para enviar a saída validada ao Salesforce, adicione uma ação.</span><span class="sxs-lookup"><span data-stu-id="9164a-118">To send the validated output to Salesforce, add an action.</span></span>

<span data-ttu-id="9164a-119">Para testar a ação de validação, faça uma solicitação ao ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="9164a-119">To test your validation action, make a request to the HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9164a-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9164a-120">Next steps</span></span>
[<span data-ttu-id="9164a-121">Saiba mais sobre o Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="9164a-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o Enterprise Integration Pack")   

