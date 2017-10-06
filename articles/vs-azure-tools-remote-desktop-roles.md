---
title: "aaaUsing área de trabalho remota com funções do Azure | Microsoft Docs"
description: "Usando a Área de Trabalho Remota com as funções do Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a>Usando a Área de Trabalho Remota com as funções do Azure
Por meio de saudação do SDK do Azure e os serviços de área de trabalho remota, você pode acessar as funções do Azure e máquinas virtuais que são hospedadas pelo Azure. No Visual Studio, você pode configurar os Serviços de Área de Trabalho Remota por meio de um projeto de serviço de nuvem do Azure. tooenable de serviços de área de trabalho remota, você deve criar um projeto de trabalho que contém uma ou mais funções e, em seguida, publicá-lo tooAzure.

> [!IMPORTANT]
> Você deve acessar uma função do Azure apenas para desenvolvimento ou solução de problemas. Olá a finalidade de cada máquina virtual é toorun uma função específica em seu aplicativo do Azure, não toorun outros aplicativos cliente. Se você quiser toouse Azure toohost uma máquina virtual que você pode usar para qualquer finalidade, consulte Acessando máquinas virtuais do Azure do Gerenciador de servidores.
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a>tooenable e use a área de trabalho remota para uma função do Azure
1. No Gerenciador de soluções, abrir o menu de atalho de saudação para seu projeto de serviço de nuvem e, em seguida, escolha **publicar**.
   
    Olá **publicar aplicativo do Azure** assistente é exibido.
   
    ![Publicar o comando para um projeto de Serviço de Nuvem](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. Na parte inferior de saudação do **configurações de publicação do Microsoft Azure** página do Assistente de saudação, selecione Olá **habilitar área de trabalho remota** todas as funções caixa de seleção. 
   
    Olá **configuração da área de trabalho remota** caixa de diálogo é exibida.
3. Na parte inferior de saudação do hello **configuração da área de trabalho remota** caixa de diálogo caixa, escolha Olá **mais opções** botão. 
   
    Isso exibe uma caixa de listagem suspensa que permite que você crie ou escolha um certificado para que você possa criptografar informações de credenciais ao conectar-se via área de trabalho remota.
4. Na lista suspensa de saudação, escolha  **&lt;criar >**, ou escolha um existente na lista de saudação. 
   
    Se você escolher um certificado existente, ignore Olá etapas a seguir.
   
   > [!NOTE]
   > certificados de saudação que é necessário para uma conexão de área de trabalho remota são diferentes dos certificados de saudação que você usa para outras operações do Azure. certificado de acesso remoto Olá deve ter uma chave privada.
   > 
   > 
   
    Olá **Create Certificate** caixa de diálogo é exibida.
   
   1. Forneça um nome amigável para o novo certificado de saudação e escolha Olá **Okey** botão. novo certificado de saudação aparece na caixa de listagem suspensa hello.
   2. Em Olá **configuração da área de trabalho remota** caixa de diálogo caixa, forneça um nome de usuário e uma senha.
      
       Você não pode usar uma conta existente. Não especifique um administrador como nome de usuário de Olá para a nova conta de saudação.
      
      > [!NOTE]
      > Se a senha de saudação não atende aos requisitos de complexidade de saudação, um ícone vermelho aparece próxima caixa de texto de senha toohello. senha de saudação deve incluir letras maiusculas, letras minúsculas e números ou símbolos.
      > 
      > 
   3. Escolha uma data na qual conta Olá irá expirar e depois quais conexões de área de trabalho remotas serão bloqueados.
   4. Depois de ter fornecido todas as informações necessárias de hello, escolha Olá **Okey** botão.
      
       Várias configurações que permitem que os serviços de acesso remoto são adicionadas toohello. cscfg e. csdef arquivos.
5. Em Olá **configurações de publicação do Microsoft Azure** assistente, escolha Olá **Okey** botão quando estiver pronto toopublish seu serviço de nuvem.
   
    Se você não tiver toopublish pronto, escolha Olá **Cancelar** botão. Olá configurações são salvas, e você pode publicar seu serviço de nuvem mais tarde.

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a>Conecte-se tooan função do Azure usando a área de trabalho remota
Depois de publicar seu serviço de nuvem no Azure, você pode usar toolog do Gerenciador de servidores em máquinas virtuais Olá que hospeda do Azure. 

1. No Gerenciador de servidores, expanda Olá **Azure** nó e, em seguida, expanda o nó de saudação de um serviço de nuvem e uma das sua funções toodisplay uma lista de instâncias.
2. Abrir menu de atalho Olá para um nó da instância e, em seguida, escolha **se conectar usando área de trabalho remota**.
   
    ![Conectando-se via área de trabalho remota](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. Insira o nome de usuário de saudação e a senha que você criou anteriormente. Agora você está conectado na sessão remota.

