---
title: "Azure Active Directory Domain Services: introdução | Microsoft Docs"
description: "Habilitar o Azure Active Directory Domain Services usando Olá portal do Azure (visualização)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Habilitar o Azure Active Directory Domain Services usando Olá portal do Azure (visualização)
Este artigo mostra como tooenable do Azure Active Directory serviços de domínio (do Azure AD DS) usando Olá portal do Azure.


Olá toolaunch **serviços de domínio de AD do Azure permitem** Olá assistente, concluir as etapas a seguir:

1. Vá toohello [portal do Azure](https://portal.azure.com).
2. No painel esquerdo do hello, clique em **novo**.
3. Em Olá **novo** folha, digite **dos serviços de domínio** na barra de pesquisa de saudação.

    ![Pesquisa pelo Domain Services](./media/getting-started/search-domain-services.png)

4. Clique em tooselect **serviços de domínio do AD do Azure** de lista de saudação de sugestões de pesquisa. Em Olá **serviços de domínio do AD do Azure** folha, clique em Olá **criar** botão.

    ![Folha do Domain Services](./media/getting-started/domain-services-blade.png)

5. Olá **serviços de domínio de AD do Azure permitem** assistente é iniciado.


## <a name="task-1-configure-basic-settings"></a>Tarefa 1: definir as configurações básicas
Em Olá **Noções básicas sobre** página do Assistente para Olá, você pode especificar o nome de domínio DNS Olá para o domínio gerenciado hello. Você também pode escolher o grupo de recursos de saudação e domínio gerenciado de saudação do local do Azure toowhich deve ser implantado.

![Configurar os aspectos básicos](./media/getting-started/domain-services-blade-basics.png)

1. Escolha Olá **nome de domínio DNS** para seu domínio gerenciado.

   * nome de domínio saudação padrão do diretório de saudação (com um **. c o m** sufixo) é especificada por padrão.

   * Você também pode inserir um nome de domínio personalizado. Neste exemplo, é o nome de domínio personalizado Olá *contoso100.com*.

     > [!WARNING]
     > prefixo de saudação do seu nome de domínio especificado (por exemplo, *contoso100* em Olá *contoso100.com* nome de domínio) deve conter a 15 caracteres. Você não pode criar um domínio gerenciado com um prefixo de mais de 15 caracteres.
     >
     >

2. Verifique se esse nome de domínio DNS Olá escolhido para Olá gerenciado domínio ainda não existir na rede virtual hello. Especificamente, verifique se:

   * Você já tiver um domínio com hello mesmo nome de domínio DNS na rede virtual hello.

   * rede virtual Hello, onde você planeja tooenable Olá gerenciado domínio tem uma conexão VPN com a sua rede local. Nesse cenário, verifique se você não tiver um domínio com hello mesmo nome de domínio DNS na rede local.

   * Você tem um serviço de nuvem existente com esse nome na rede virtual hello.

3. Escolha Olá **tipo de rede virtual**. Por padrão, Olá **Gerenciador de recursos** tipo de rede virtual está selecionado. Recomendamos o uso desse tipo de rede virtual para todos os domínios gerenciados recém-criados.

4. Selecione hello Azure **assinatura** em que você gostaria que toocreate Olá gerenciado domínio.

5. Selecione Olá **grupo de recursos** toowhich Olá gerenciado domínio deve pertencer. Você pode escolher qualquer Olá **criar novo** ou **usar existente** grupo de recursos opções tooselect hello.

6. Escolha hello Azure **local** em qual Olá domínio gerenciado deve ser criado. Em Olá **rede** página do Assistente de saudação, você ver as redes virtuais só pertencem toohello local selecionado.

7. Quando terminar, clique em **Okey** toomove na toohello **rede** página do Assistente de saudação.


## <a name="next-step"></a>Próxima etapa
[Tarefa 2: definir as configurações de rede](active-directory-ds-getting-started-network.md)
