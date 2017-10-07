---
title: "aaaWindows autenticação e o servidor Azure MFA | Microsoft Docs"
description: "Isso é a página de autenticação do Azure multi-factor Olá ajudará na implantação de autenticação do Windows e o servidor Azure multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>Autenticação do Windows e Servidor Azure Multi-Factor Authentication
Use a seção de autenticação do Windows hello de saudação servidor Azure multi-Factor Authentication tooenable e configurar a autenticação do Windows para aplicativos. Antes de configurar a autenticação do Windows, lembre-Olá lista em mente a seguir:

* Após a instalação, reinicialize hello Azure multi-Factor Authentication para efeito de tootake de serviços de Terminal.
* Se 'Correspondência de usuários exigir Azure multi-Factor Authentication' está marcada e você não estiver na lista de saudação do usuário, não será capaz de toolog na máquina de saudação após a reinicialização.
* IPs confiáveis que é depende se o aplicativo hello pode fornecer Olá IP do cliente com a autenticação de saudação. Atualmente, apenas os Serviços de Terminal têm suporte.  

> [!NOTE]
> Este recurso não está toosecure com suporte dos serviços de Terminal no Windows Server 2012 R2.

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a>toosecure um aplicativo com autenticação do Windows, use Olá procedimento a seguir.
1. No servidor Azure multi-Factor Authentication de saudação Clique ícone de autenticação do Windows hello.
   ![Autenticação do Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)
2. Verificar Olá **habilitar autenticação do Windows** caixa de seleção. Por padrão, essa caixa está desmarcada.
3. Guia de aplicativos Olá permite Olá administrador tooconfigure um ou mais aplicativos para autenticação do Windows.
4. Selecione um servidor ou aplicativo – especifique se o servidor/aplicativo hello está habilitado. Clique em **OK**.
5. Clique em **Adicionar...**
6. Guia do Hello IPs confiáveis permite que você tooskip Azure multi-Factor Authentication para sessões do Windows provenientes de IPs específicos. Por exemplo, se os funcionários usarem o aplicativo hello no office hello e em casa, você pode decidir que você não quer seus telefones liguem para o Azure multi-Factor Authentication e ao office hello. Para isso, você deve especificar a sub-rede de escritório hello como entrada de IPs confiáveis.
7. Clique em **Adicionar...**
8. Selecione **IP único** se você gostaria que tooskip um único endereço IP.
9. Selecione **intervalo IP** se você gostaria que tooskip todo um intervalo IP. Exemplo 10.63.193.1-10.63.193.100.
10. Selecione **sub-rede** se você gostaria que toospecify um intervalo de IPs usando a notação de sub-rede. Insira o IP inicial da sub-rede hello e escolha a máscara de rede apropriada da lista suspensa de Olá Olá.
11. Clique em **OK**.

## <a name="next-steps"></a>Próximas etapas

- [Configure os dispositivos de VPN de terceiros para servidor Azure MFA](multi-factor-authentication-advanced-vpn-configurations.md)

- [Aumentar sua infraestrutura de autenticação existente com hello extensão NPS para o Azure MFA](multi-factor-authentication-nps-extension.md)
