---
title: aaaUpload um certificado de API de gerenciamento do Azure | Microsoft Docs
description: "Saiba como tooupload athe API de gerenciamento de certificado para Olá Portal clássico do Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a>Carregar um Certificado de Gerenciamento de API do Gerenciamento do Azure
Permitir certificados de gerenciamento que você tooauthenticate com o modelo de implantação clássico Olá fornecida pelo Azure. Muitos programas e ferramentas (como o Visual Studio ou saudação do SDK do Azure) usam esses configuração tooautomate de certificados e a implantação de vários serviços do Azure. 

> [!WARNING]
> Portanto, tenha cuidado! Esses tipos de certificados que qualquer pessoa que se autentica com eles toomanage assinatura de saudação que estão associados.
>
>

Se você quiser obter mais informações sobre certificados do Azure (incluindo a criação de um certificado autoassinado), veja [Visão geral de certificados para Serviços de Nuvem do Azure](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

Você também pode usar [Active Directory do Azure](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate-código do cliente para fins de automação.

## <a name="upload-a-management-certificate"></a>Carregar um certificado de gerenciamento
Depois que você tiver um certificado de gerenciamento criado, (arquivo. cer com a chave pública só Olá) você pode carregá-lo no portal de saudação. Quando o certificado hello está disponível no portal de Olá, qualquer pessoa com um certificado correspondente (chave privada) pode se conectar por meio de recursos de saudação API de gerenciamento e acesso de saudação para assinatura Olá associado.

1. Faça logon no toohello [portal do Azure](http://portal.azure.com).
2. Clique em **mais serviços** na lista de serviço do Azure do hello inferior, em seguida, selecione **assinaturas** em Olá _geral_ grupo do serviço.

    ![Menu de assinatura](./media/azure-api-management-certs/subscriptions_menu.png)

3. Certifique-se de tooselect Olá assinatura correta que você deseja tooassociate com certificado hello.     
4. Depois que você selecionou a assinatura correta hello, pressione **certificados de gerenciamento** em Olá _configurações_ grupo.

    ![Configurações](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. Olá pressione **carregar** botão.

    ![Carregar na página de certificados](./media/azure-api-management-certs/certificates_page.png)
6. Preencha as informações da caixa de diálogo de saudação e pressione **carregar**.

    ![Configurações](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a>Próximas etapas
Agora que você tem um certificado de gerenciamento associado a uma assinatura, você pode (depois de ter instalado o hello correspondência certificado localmente) programaticamente conectar toohello [API REST do modelo de implantação clássico](https://msdn.microsoft.com/library/azure/mt420159.aspx) e automatizar Olá vários recursos do Azure que também estão associados essa assinatura.
