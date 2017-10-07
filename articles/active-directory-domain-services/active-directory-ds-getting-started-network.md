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
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Habilitar o Azure Active Directory Domain Services usando Olá portal do Azure (visualização)


## <a name="before-you-begin"></a>Antes de começar
Consulte também[considerações de rede para o Azure Active Directory Domain Services](active-directory-ds-networking.md).


## <a name="task-2-configure-network-settings"></a>Tarefa 2: definir as configurações de rede
a próxima tarefa de configuração Olá é toocreate uma rede virtual do Azure e uma sub-rede dedicada dentro dele. Você pode habilitar o Azure Active Directory Domain Services nessa sub-rede dentro de sua rede virtual. Você também pode escolher uma rede virtual existente e criar hello dedicado sub-rede dentro dele.

1. Clique em **rede Virtual** tooselect uma rede virtual.
2. Em Olá **rede virtual escolha** folha, você vê todas as redes virtuais existentes. Consulte somente Olá redes virtuais que pertencem toohello grupo de recursos e local do Azure que você selecionou na Olá **Noções básicas sobre** página do assistente.

3. Escolha Olá rede virtual no qual os serviços de domínio do AD do Azure devem ser habilitados. Clique em **criar novo**, se você preferir toocreate uma nova rede virtual. É altamente recomendável usar uma sub-rede dedicada para o Azure AD Domain Services. Se você escolher uma rede virtual existente, [criar uma sub-rede dedicada usando a extensão de redes virtuais Olá](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) e, em seguida, selecione nessa sub-rede. 

    ![Escolher rede virtual](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. Clique em **sub-rede** toopick Olá sub-rede dedicada nessa rede virtual, no qual tooenable o domínio gerenciado seu novo. Em Olá **criar sub-rede** folha, especifique um nome para a sub-rede hello e clique em **Okey** quando terminar. Por exemplo, crie uma sub-rede com o nome de saudação 'DomainServices', tornando mais fácil para outros administradores toounderstand o que é implantado na sub-rede hello.

    ![Selecione a sub-rede na rede virtual Olá](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > **Diretrizes para selecionar uma sub-rede**
  > 1. Use uma sub-rede dedicada para o Azure AD Domain Services. Não implante nenhuma outra sub-rede toothis de máquinas virtuais. Essa configuração permite que você tooconfigure grupos de segurança de rede (NSGs) para as máquinas virtuais/cargas de trabalho sem interromper seu domínio gerenciado. Para obter detalhes, consulte as [Considerações de rede do Azure Active Directory Domain Services](active-directory-ds-networking.md).
  2. Não selecione a sub-rede de Gateway Olá para implantar serviços de domínio do AD do Azure, porque ele não é uma configuração com suporte.
  3. Certifique-se de sub-rede Olá selecionado tem espaço de endereço disponível suficiente - pelo menos 3 a 5 endereços IP.
  >

5. Quando terminar, clique em **Okey** toomove na toohello **grupo administrador** página do Assistente de saudação.


## <a name="next-step"></a>Próxima etapa
[Tarefa 3: configurar o grupo administrativo e habilitar o Azure AD Domain Services](active-directory-ds-getting-started-admingroup.md)
