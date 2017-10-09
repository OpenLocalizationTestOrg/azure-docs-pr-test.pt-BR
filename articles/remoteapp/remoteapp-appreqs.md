---
title: requisitos de aaaApp do Azure RemoteApp | Microsoft Docs
description: "Saiba mais sobre requisitos de saudação para aplicativos que você deseja toouse no Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a>Requisitos de aplicativo
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

O RemoteApp do Azure dá suporte a streaming de aplicativos baseados em Windows 32 bits ou 64 bits de uma imagem do Windows Server 2012 R2. A maioria dos aplicativos baseados em Windows de 32 bits ou 64 bits é executada "como está" no ambiente RemoteApp do Azure (Serviços de Área de Trabalho Remota, anteriormente conhecido como Serviços de Terminal). No entanto, há uma diferença entre executar e executar bem – alguns aplicativos funcionam corretamente e executam bem, enquanto outros, não. Olá informações a seguir fornece orientação para desenvolvimento de aplicativos em um ambiente de serviços de área de trabalho remota e teste de compatibilidade de tooensure.

Dica: estamos trabalhando na criação de alguns exemplos práticos dos aplicativos para você. Você verá os novos tópicos que abordam o uso do Microsoft Access, do QuickBooks e do App-V no RemoteApp.

## <a name="requirements"></a>Requisitos
Esses três requisitos, se seguidos, ajudam o aplicativo a ser executado corretamente no RemoteApp:

1. Aplicativos que atendem a todos os [requisitos de certificação de aplicativos de área de trabalho do Windows](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) e aderir muito[diretrizes de programação dos serviços de área de trabalho remota](https://msdn.microsoft.com/library/aa383490.aspx) terá compatibilidade total com o RemoteApp.
2. Aplicativos nunca devem armazenar dados localmente em imagem hello ou instâncias de RemoteApp que podem ser perdidas.  Depois de criar uma coleção do RemoteApp, instâncias de saudação são clonadas e são sem monitoração de estado e devem conter apenas os aplicativos. Armazenar dados em uma fonte externa ou no perfil do usuário hello.
3. Imagens personalizadas nunca devem conter dados que possam ser perdidos.  

## <a name="testing-your-apps"></a>Testando seus aplicativos
Use aplicativos de tootesting essas etapas:

1. Instale o Windows Server 2012 R2 e o seu aplicativo
2. Habilite a Área de Trabalho Remota
3. Crie duas contas de usuário, UserA e UserB, adição de ambos os grupo de segurança do usuário contas toohello área de trabalho remota.
4. Verificar a compatibilidade de várias sessões, estabelecendo dois simultâneas RDS sessões toohello PC ao iniciar o aplicativo hello.
5. Validar o comportamento do aplicativo

## <a name="application-development-guidelines"></a>Diretrizes para desenvolvimento de aplicativos
Use Olá cumprimento das diretrizes para desenvolvimento de aplicativos para o RemoteApp.

### <a name="multiple-users"></a>Vários usuários
* Instalar um [aplicativo para um único usuário ](https://msdn.microsoft.com/library/aa380661.aspx)pode criar problemas em um ambiente multiusuário.
* Aplicativos devem [armazenar informações específicas do usuário](https://msdn.microsoft.com/library/aa383452.aspx) em locais específicos do usuário, separadamente de informações globais que se aplica tooall usuários.
* O RemoteApp usa vários [namespaces para objetos kernel](https://msdn.microsoft.com/library/aa382954.aspx); um namespace global é usado principalmente por serviços de aplicativos cliente/servidor.
* Não é seguro tooassume que Olá o nome do computador ou hello [endereço IP](https://msdn.microsoft.com/library/aa382942.aspx) toohello atribuído computador estão associados um único usuário porque vários usuários podem ser conectados simultaneamente tooa Host de sessão de área de trabalho remota (sessão de área de trabalho remota Servidor de host).

### <a name="performance"></a>Desempenho
* Desabilitar [efeitos gráficos](https://msdn.microsoft.com/library/aa380822.aspx) antes de adicionar tooRemoteApp seu aplicativo.
* disponibilidade de toomaximize da CPU para todos os usuários, desabilitar [tarefas em segundo plano ](https://msdn.microsoft.com/library/aa380665.aspx) ou criar tarefas de plano de fundo eficiente que não fazem uso intensivo de recursos.
* Você deve ajustar e balancear o [uso de thread](https://msdn.microsoft.com/library/aa383520.aspx) do aplicativo para um ambiente multiusuário com vários processadores.
* toooptimize desempenho, é uma boa prática para aplicativos muito[detectar](https://msdn.microsoft.com/library/aa380798.aspx) se estiverem sendo executados em uma sessão de cliente.

