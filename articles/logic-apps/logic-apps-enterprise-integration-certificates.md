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
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a>Saiba mais sobre certificados e o Enterprise Integration Pack
## <a name="overview"></a>Visão geral
Integração da empresa usa comunicações de B2B toosecure certificados. Você pode usar dois tipos de certificados em seus aplicativos de integração corporativa:

* Certificados públicos, que devem ser adquiridos de uma autoridade de certificação (CA).
* Certificados privados, você pode emitir por conta própria. Esses certificados são às vezes chamado tooas os certificados autoassinados.

## <a name="what-are-certificates"></a>O que são certificados?
Os certificados são documentos digitais que verificar a identidade de saudação dos participantes Olá comunicações eletrônicas e que também proteger comunicações eletrônicas.

## <a name="why-use-certificates"></a>Por que usar certificados?
Às vezes, as comunicações B2B devem ser mantidas confidenciais. Integração da empresa usa certificados toosecure essas comunicações de duas maneiras:

* Criptografando o conteúdo de saudação de mensagens
* Assinando digitalmente as mensagens  

## <a name="upload-a-public-certificate"></a>Carregar um certificado público

toouse um *certificado público* em seus aplicativos de lógica com recursos de B2B, você primeiro precisa tooupload Olá certificado à sua conta de integração.  

Depois de carregar um certificado, é disponível toohelp proteger suas mensagens B2B quando você define suas propriedades no hello [contratos](logic-apps-enterprise-integration-agreements.md) que você criar.  

Aqui estão Olá etapas detalhadas para carregar os certificados públicos em sua conta de integração depois de entrar no portal do Azure de toohello:

1. Selecione **mais serviços** e digite **integração** na caixa de pesquisa do filtro de saudação. Selecione **contas de integração** Olá da lista de resultados     
![Selecionar Procurar](media/logic-apps-enterprise-integration-certificates/overview-1.png)  
2. Selecione Olá integração conta toowhich você deseja tooadd Olá certificado.  
![Selecione Olá integração conta toowhich você deseja tooadd Olá certificado](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. Selecione Olá **certificados** lado a lado.  
![Olá selecione certificados lado a lado](media/logic-apps-enterprise-integration-certificates/certificate-1.png)
4. Em Olá **certificados** folha que é aberta, selecione Olá **adicionar** botão.   
![Selecione o botão de adicionar Olá](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
5. Insira um **nome** de certificado e hello, em seguida, selecione o tipo de certificado como **pública** na lista suspensa de saudação.  
6. Ícone de pasta selecione Olá Olá direita da saudação **certificado** caixa de texto. Quando abre o selecionador de arquivo hello, localize e selecione o arquivo de certificado Olá que você deseja tooupload tooyour integração conta.
7. Selecionar certificado hello e, em seguida, selecione **Okey** no selecionador de arquivo hello. Isso valida e os carrega Olá certificado tooyour integração de conta.
8. Por fim, faça Olá **Adicionar certificado** folha, selecione Olá **Okey** botão.  
![Selecione o botão Okey Olá](media/logic-apps-enterprise-integration-certificates/certificate-3.png)  
9. Selecione Olá **certificados** lado a lado. Você deve ver Olá certificado adicionado recentemente.  
![Consulte o novo certificado de saudação](media/logic-apps-enterprise-integration-certificates/certificate-4.png)  

## <a name="upload-a-private-certificate"></a>Carregar um certificado privado

toouse um *certificado privado* em seus aplicativos de lógica com recursos de B2B, você pode carregar uma conta de integração do certificado privado tooyour Olá colocar as etapas a seguir

1. [Carregue seu tooKey chave privada cofre](../key-vault/key-vault-get-started.md "Saiba mais sobre o Cofre de chaves") e fornecer um **nome da chave** 
   
   > [!TIP]
   > É necessário autorizar as operações de tooperform aplicativos lógicos no cofre de chaves. Você pode conceder a entidade de serviço de aplicativos lógicos do acesso toohello usando Olá comando PowerShell a seguir:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`  
   > 
   > 

Depois de concluir a etapa anterior hello, adicione uma conta de toointegration de certificado particular.

A seguir são Olá etapas detalhadas para carregar os certificados privados em sua conta de integração depois que você entra no toohello portal do Azure:  
 
1. Selecione Olá integração conta toowhich deseja tooadd Olá certificado e selecione Olá **certificados** lado a lado.  
![Olá selecione certificados lado a lado](media/logic-apps-enterprise-integration-certificates/certificate-1.png)  
2. Em Olá **certificados** folha que é aberta, selecione Olá **adicionar** botão.   
![Selecione o botão de adicionar Olá](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
3. Insira um **nome** de certificado e Olá selecione o tipo de certificado como **privada** na lista suspensa de saudação.   
4. Selecione o ícone de pasta Olá Olá direita da saudação **certificado** caixa de texto. Quando abre o selecionador de arquivo hello, localize o certificado público correspondente Olá que você deseja tooupload tooyour integração conta.   
   
   > [!Note]
   > Ao adicionar um certificado privado é importante tooadd correspondente pública do certificado tooshow em [acordo AS2](logic-apps-enterprise-integration-as2.md) para receber e enviar as configurações para assinar e criptografar mensagens de saudação.
   > 
   >   

5. Selecione Olá **grupo de recursos**, **Cofre de chaves**, **nome da chave** e selecione hello **Okey** botão.  
![Adicionar certificado](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)  
6. Selecione Olá **certificados** lado a lado. Você deve ver Olá certificado adicionado recentemente.
![Consulte o novo certificado de saudação](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)  



* [Criar um contrato de B2B](logic-apps-enterprise-integration-agreements.md)  
* [Saiba mais sobre o Cofre de Chaves](../key-vault/key-vault-get-started.md "Saiba mais sobre o Cofre de Chaves")  

