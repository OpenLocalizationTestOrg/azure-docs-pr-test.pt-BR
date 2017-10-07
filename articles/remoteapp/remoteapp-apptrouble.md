---
title: "aaaAzure solução de problemas do RemoteApp - falhas de conexão e inicialização do aplicativo | Microsoft Docs"
description: Saiba como tootroubleshoot problemas com Iniciar e conectar-se tooapplications no Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e51d480c9d3fa1f2076f95b63c7a8cd2f6956a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a>Solucionar problemas do Azure RemoteApp - falhas de conexão e inicialização do aplicativo
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Aplicativos hospedados no Azure RemoteApp podem falhar toolaunch por alguns motivos diferentes. Este artigo descreve vários motivos e mensagens de erro, os usuários podem receber quando tentar toolaunch aplicativos. Ele também fala sobre falhas de conexão. (Mas este artigo descreve problemas ao entrar no cliente do Azure RemoteApp hello.)  

Continue lendo para obter informações sobre mensagens de erro comuns devido a falhas de inicialização e conexão tooapp.

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a>Estamos configurando para você... Tente novamente em 10 minutos.
Esse erro significa que o Azure RemoteApp está sendo reduzido a necessidade de capacidade de saudação toomeet dos usuários. Plano de fundo hello mais instâncias de VM do Azure RemoteApp estão sendo criadas necessidades de capacidade de saudação toohandle de seus usuários. Normalmente isso leva cerca de cinco minutos, mas pode levar até too10 minutos. Às vezes, isso não acontece rápido o suficiente e os recursos são necessários imediatamente. Por exemplo, um cenário 9: 00 onde muitos usuários precisarem toouse seu aplicativo no Azure RemoteAppn no hello simultaneamente. Se isso acontecer tooyou é possível habilitar **modo capacidade** em Olá back-end. toodo nesse abrir um tíquete de suporte do Azure. Ser determinada tooinclude sua ID de assinatura na solicitação de saudação.  

![Estamos configurando para você](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-tooyour-applications-please-re-launch-your-application"></a>Não foi possível autoreconectar tooyour aplicativos reinicie seu aplicativo
Essa mensagem de erro é geralmente Vista se estivesse usando o Azure RemoteApp e, em seguida, coloque o toosleep PC mais de 4 horas e, em seguida, ativou seu PC hello Azure RemoteApp cliente tentativa tooauto reconectar e tempo limite foi excedido.  Instrua os usuários toonavigate toohello back aplicativo e tente tooopen-la no cliente do Azure RemoteApp hello.

![Não foi possível autoreconectar tooyour aplicativos](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-hello-temp-profile"></a>Problemas com o perfil de tempo de saudação
Esse erro ocorre quando seu perfil de usuário (disco de perfil do usuário) falha toomount e usuário Olá recebeu um perfil temporário.  Os administradores devem navegar coleção toohello em Olá portal do Azure e acesse toohello **sessões** guia e tente muito**logoff** usuário hello. Isso força um log completo da sessão de usuário Olá - e tiver um aplicativo hello usuário tentativa toolaunch novamente. Se não funcionar, entre em contato com o suporte do Azure.

## <a name="azure-remoteapp-has-stopped-working"></a>O Azure RemoteApp parou de funcionar
Essa mensagem de erro significa o cliente do Azure RemoteApp hello está tendo um problema e precisa toobe reiniciado. Instrua os usuários tooclose: selecione **fechar programa** e inicie o cliente do Azure RemoteApp Olá novamente.  Se o problema de saudação continua aberto e o tíquete de suporte do Azure.

![O Azure RemoteApp parou de funcionar](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-hello-connection-or-contact-your-system-administrator"></a>Ocorreu um erro enquanto a Conexão de Área de Trabalho Remota estava acessando este recurso. Repita a conexão de saudação ou entre em contato com o administrador do sistema
Esta é uma mensagem de erro genérica — entre em contato com o suporte do Azure para que possamos investigar. 

![Mensagem genérica do Azure RemoteApp](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

