---
title: aaaUpload uma imagem personalizada do Azure RemoteApp | Microsoft Docs
description: Saiba como tooupload um personalizado da imagem do Azure RemoteApp
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a>Carregar uma imagem personalizada para o RemoteApp do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Agora que você criou sua imagem de modelo personalizado ou atualizá-lo com as alterações, é necessário tooupload essa biblioteca de imagens do Azure RemoteApp imagem tooyour. Siga estas etapas.

## <a name="before-you-start"></a>Antes de começar
1. Verifique se atende a sua imagem personalizada Olá [requisitos da imagem](remoteapp-imagereqs.md) e [requisitos do aplicativo](remoteapp-appreqs.md).
2. Instalar Olá [módulo Azure PowerShell](/powershell/azure/overview).

## <a name="step-by-step-on-how-tooupload-custom-image"></a>Passo a passo sobre como imagem personalizada tooupload
1. Abra o Portal de gerenciamento e navegue toohello RemoteApp página.
2. Em Olá **imagens de modelo** , clique em **carregar** final Olá Olá página.
3. Insira um nome amigável para a imagem e especifique o local de conta de armazenamento hello. Certifique-se de local de saudação é hello mesmo local que sua coleção do RemoteApp ou em um local onde você deseja toocreate um.
4. Quando solicitado, faça o download do hello script tooyour PC local.
5. Copie parâmetros de comando Olá na área de transferência tooyour caixa de texto de saudação.
6. Abra uma janela elevada do Windows PowerShell.
7. De saudação elevados janela Windows PowerShell, navegar toohello mesmo diretório onde você baixou o script hello.
8. Saudação de colar copiados comando e pressione **Enter**.
   
   processo de carregamento de saudação será iniciado e duração pode depender de vários fatores, inclusive sua velocidade de rede e o tamanho da imagem de saudação
9. Se o carregamento não for bem-sucedida devido a interrupções de rede ou coisas como essa, você sempre pode retomar o processo de carregamento de saudação que você começou. Olá tooresume um upload, execute o script hello novamente usando a mesma linha de comando.

> [!WARNING]
> Nunca modifique o script de carregamento de saudação. Verificações de tem sido implementado tooensure que Olá Olá imagem atende aos requisitos de imagem e requisitos de aplicativo.
> 
> 

## <a name="common-problems"></a>Problemas comuns
* Certifique-se de usar o Windows PowerShell, não o PowerShell do Azure. Você precisa módulo de PowerShell do Azure Olá tooinstall porque determinados módulos são necessários durante o processo de carregamento de saudação.
* Nunca alterar script Olá, validações existem para sua conveniência.
* Se o arquivo de vhd Olá fica bloqueado durante o carregamento, copie o arquivo hello ou movê-la tooa novo local e tente carregar novamente. Pode haver algum processo do Windows impedindo o carregamento.  

