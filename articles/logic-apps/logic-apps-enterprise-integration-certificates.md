---
title: "aaaUsing certificados com o pacote de integração Enterprise | Microsoft Docs"
description: "Saiba como toouse certificados com hello Enterprise Integration Pack | Aplicativos lógicos do Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="33044-103">Saiba mais sobre certificados e o Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="33044-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="33044-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="33044-104">Overview</span></span>
<span data-ttu-id="33044-105">Integração da empresa usa comunicações de B2B toosecure certificados.</span><span class="sxs-lookup"><span data-stu-id="33044-105">Enterprise integration uses certificates toosecure B2B communications.</span></span> <span data-ttu-id="33044-106">Você pode usar dois tipos de certificados em seus aplicativos de integração corporativa:</span><span class="sxs-lookup"><span data-stu-id="33044-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="33044-107">Certificados públicos, que devem ser adquiridos de uma autoridade de certificação (CA).</span><span class="sxs-lookup"><span data-stu-id="33044-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="33044-108">Certificados privados, você pode emitir por conta própria.</span><span class="sxs-lookup"><span data-stu-id="33044-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="33044-109">Esses certificados são às vezes chamado tooas os certificados autoassinados.</span><span class="sxs-lookup"><span data-stu-id="33044-109">These certificates are sometimes referred tooas self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="33044-110">O que são certificados?</span><span class="sxs-lookup"><span data-stu-id="33044-110">What are certificates?</span></span>
<span data-ttu-id="33044-111">Os certificados são documentos digitais que verificar a identidade de saudação dos participantes Olá comunicações eletrônicas e que também proteger comunicações eletrônicas.</span><span class="sxs-lookup"><span data-stu-id="33044-111">Certificates are digital documents that verify hello identity of hello participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="33044-112">Por que usar certificados?</span><span class="sxs-lookup"><span data-stu-id="33044-112">Why use certificates?</span></span>
<span data-ttu-id="33044-113">Às vezes, as comunicações B2B devem ser mantidas confidenciais.</span><span class="sxs-lookup"><span data-stu-id="33044-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="33044-114">Integração da empresa usa certificados toosecure essas comunicações de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="33044-114">Enterprise integration uses certificates toosecure these communications in two ways:</span></span>

* <span data-ttu-id="33044-115">Criptografando o conteúdo de saudação de mensagens</span><span class="sxs-lookup"><span data-stu-id="33044-115">By encrypting hello contents of messages</span></span>
* <span data-ttu-id="33044-116">Assinando digitalmente as mensagens</span><span class="sxs-lookup"><span data-stu-id="33044-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="33044-117">Carregar um certificado público</span><span class="sxs-lookup"><span data-stu-id="33044-117">Upload a public certificate</span></span>

<span data-ttu-id="33044-118">toouse um *certificado público* em seus aplicativos de lógica com recursos de B2B, você primeiro precisa tooupload Olá certificado à sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="33044-118">toouse a *public certificate* in your logic apps with B2B capabilities, you first need tooupload hello certificate into your integration account.</span></span>  

<span data-ttu-id="33044-119">Depois de carregar um certificado, é disponível toohelp proteger suas mensagens B2B quando você define suas propriedades no hello [contratos](logic-apps-enterprise-integration-agreements.md) que você criar.</span><span class="sxs-lookup"><span data-stu-id="33044-119">After you upload a certificate, it's available toohelp you secure your B2B messages when you define their properties in hello [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="33044-120">Aqui estão Olá etapas detalhadas para carregar os certificados públicos em sua conta de integração depois de entrar no portal do Azure de toohello:</span><span class="sxs-lookup"><span data-stu-id="33044-120">Here are hello detailed steps for uploading your public certificates into your integration account after you sign in toohello Azure portal:</span></span>

1. <span data-ttu-id="33044-121">Selecione **mais serviços** e digite **integração** na caixa de pesquisa do filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="33044-121">Select **More services** and enter **integration** in hello filter search box.</span></span> <span data-ttu-id="33044-122">Selecione **contas de integração** Olá da lista de resultados</span><span class="sxs-lookup"><span data-stu-id="33044-122">Select **Integration Accounts** from hello results list</span></span>     
<span data-ttu-id="33044-123">![Selecionar Procurar](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="33044-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="33044-124">Selecione Olá integração conta toowhich você deseja tooadd Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="33044-124">Select hello integration account toowhich you want tooadd hello certificate.</span></span>  
![Selecione Olá integração conta toowhich você deseja tooadd Olá certificado](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="33044-126">Selecione Olá **certificados** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="33044-126">Select hello **Certificates** tile.</span></span>  
<span data-ttu-id="33044-127">![Olá selecione certificados lado a lado](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="33044-127">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="33044-128">Em Olá **certificados** folha que é aberta, selecione Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="33044-128">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="33044-129">![Selecione o botão de adicionar Olá](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="33044-129">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="33044-130">Insira um **nome** de certificado e hello, em seguida, selecione o tipo de certificado como **pública** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="33044-130">Enter a **Name** for your certificate, and then select hello certificate type as **public** from hello dropdown.</span></span>  
6. <span data-ttu-id="33044-131">Ícone de pasta selecione Olá Olá direita da saudação **certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="33044-131">Select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="33044-132">Quando abre o selecionador de arquivo hello, localize e selecione o arquivo de certificado Olá que você deseja tooupload tooyour integração conta.</span><span class="sxs-lookup"><span data-stu-id="33044-132">When hello file picker opens, find and select hello certificate file that you want tooupload tooyour integration account.</span></span>
7. <span data-ttu-id="33044-133">Selecionar certificado hello e, em seguida, selecione **Okey** no selecionador de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="33044-133">Select hello certificate, and then select **OK** in hello file picker.</span></span> <span data-ttu-id="33044-134">Isso valida e os carrega Olá certificado tooyour integração de conta.</span><span class="sxs-lookup"><span data-stu-id="33044-134">This validates and uploads hello certificate tooyour integration account.</span></span>
8. <span data-ttu-id="33044-135">Por fim, faça Olá **Adicionar certificado** folha, selecione Olá **Okey** botão.</span><span class="sxs-lookup"><span data-stu-id="33044-135">Finally, back on hello **Add certificate** blade, select hello **OK** button.</span></span>  
<span data-ttu-id="33044-136">![Selecione o botão Okey Olá](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="33044-136">![Select hello OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="33044-137">Selecione Olá **certificados** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="33044-137">Select hello **Certificates** tile.</span></span> <span data-ttu-id="33044-138">Você deve ver Olá certificado adicionado recentemente.</span><span class="sxs-lookup"><span data-stu-id="33044-138">You should see hello newly added certificate.</span></span>  
<span data-ttu-id="33044-139">![Consulte o novo certificado de saudação](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="33044-139">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="33044-140">Carregar um certificado privado</span><span class="sxs-lookup"><span data-stu-id="33044-140">Upload a private certificate</span></span>

<span data-ttu-id="33044-141">toouse um *certificado privado* em seus aplicativos de lógica com recursos de B2B, você pode carregar uma conta de integração do certificado privado tooyour Olá colocar as etapas a seguir</span><span class="sxs-lookup"><span data-stu-id="33044-141">toouse a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate tooyour integration account by taking hello following steps</span></span>

1. <span data-ttu-id="33044-142">[Carregue seu tooKey chave privada cofre](../key-vault/key-vault-get-started.md "Saiba mais sobre o Cofre de chaves") e fornecer um **nome da chave**</span><span class="sxs-lookup"><span data-stu-id="33044-142">[Upload your private key tooKey Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="33044-143">É necessário autorizar as operações de tooperform aplicativos lógicos no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="33044-143">You must authorize Logic Apps tooperform operations on Key Vault.</span></span> <span data-ttu-id="33044-144">Você pode conceder a entidade de serviço de aplicativos lógicos do acesso toohello usando Olá comando PowerShell a seguir:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="33044-144">You can grant access toohello Logic Apps service principal by using hello following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="33044-145">Depois de concluir a etapa anterior hello, adicione uma conta de toointegration de certificado particular.</span><span class="sxs-lookup"><span data-stu-id="33044-145">After you've taken hello previous step, add a private certificate toointegration account.</span></span>

<span data-ttu-id="33044-146">A seguir são Olá etapas detalhadas para carregar os certificados privados em sua conta de integração depois que você entra no toohello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="33044-146">Following are hello detailed steps for uploading your private certificates into your integration account after you sign in toohello Azure portal:</span></span>  
 
1. <span data-ttu-id="33044-147">Selecione Olá integração conta toowhich deseja tooadd Olá certificado e selecione Olá **certificados** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="33044-147">Select hello integration account toowhich you want tooadd hello certificate and select hello **Certificates** tile.</span></span>  
<span data-ttu-id="33044-148">![Olá selecione certificados lado a lado](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="33044-148">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="33044-149">Em Olá **certificados** folha que é aberta, selecione Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="33044-149">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="33044-150">![Selecione o botão de adicionar Olá](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="33044-150">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="33044-151">Insira um **nome** de certificado e Olá selecione o tipo de certificado como **privada** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="33044-151">Enter a **Name** for your certificate, and select hello certificate type as **private** from hello dropdown.</span></span>   
4. <span data-ttu-id="33044-152">Selecione o ícone de pasta Olá Olá direita da saudação **certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="33044-152">select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="33044-153">Quando abre o selecionador de arquivo hello, localize o certificado público correspondente Olá que você deseja tooupload tooyour integração conta.</span><span class="sxs-lookup"><span data-stu-id="33044-153">When hello file picker opens, find hello corresponding public certificate that you want tooupload tooyour integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="33044-154">Ao adicionar um certificado privado é importante tooadd correspondente pública do certificado tooshow em [acordo AS2](logic-apps-enterprise-integration-as2.md) para receber e enviar as configurações para assinar e criptografar mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="33044-154">While adding a private certificate it is important tooadd corresponding public certificate tooshow in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting hello messages.</span></span>
   > 
   >   

5. <span data-ttu-id="33044-155">Selecione Olá **grupo de recursos**, **Cofre de chaves**, **nome da chave** e selecione hello **Okey** botão.</span><span class="sxs-lookup"><span data-stu-id="33044-155">Select hello **Resource Group**, **Key Vault**, **Key Name** and select hello **OK** button.</span></span>  
<span data-ttu-id="33044-156">![Adicionar certificado](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="33044-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="33044-157">Selecione Olá **certificados** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="33044-157">Select hello **Certificates** tile.</span></span> <span data-ttu-id="33044-158">Você deve ver Olá certificado adicionado recentemente.</span><span class="sxs-lookup"><span data-stu-id="33044-158">You should see hello newly added certificate.</span></span>
<span data-ttu-id="33044-159">![Consulte o novo certificado de saudação](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="33044-159">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="33044-160">Criar um contrato de B2B</span><span class="sxs-lookup"><span data-stu-id="33044-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="33044-161">Saiba mais sobre o Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="33044-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "Saiba mais sobre o Cofre de Chaves")  

