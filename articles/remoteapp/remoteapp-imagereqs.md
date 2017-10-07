---
title: requisitos de imagem do RemoteApp aaaAzure | Microsoft Docs
description: "Saiba mais sobre os requisitos de saudação para a criação de imagens toobe usado com o Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a>Requisitos para as imagens do Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

O Azure RemoteApp usa um toohost de imagem do Windows Server 2012 R2 todos os programas de saudação que você deseja tooshare com seus usuários. toocreate uma imagem personalizada, você pode iniciar com uma imagem existente ou [criar um novo](remoteapp-create-custom-image.md).

> [!TIP]
> Você sabia que o oferece de assinatura do Azure RemoteApp que acesso imagem do Windows Server 2012 R2 tooa no hello Galeria de VMs do Azure que você pode usar toocreate sua própria imagem de modelo? [Confira](remoteapp-image-on-azurevm.md).  
> 
> 

requisitos de saudação de imagem Olá que podem ser carregados para uso com o Azure RemoteApp são:

* Aplicativos personalizados não armazenam dados localmente na imagem de saudação. Essas imagens são sem monitoração de estado e devem conter apenas aplicativos.
* Olá imagem não contém dados que podem ser perdidos.
* tamanho da imagem Olá deve ser um múltiplo de MBs. Se você tentar tooupload uma imagem que não é um múltiplo exato, carregamento Olá falhará.
* tamanho da imagem Olá deve ser 127 GB ou menores.
* Deve estar em um arquivo VHD (arquivos VHDX atualmente não têm suporte).
* Olá VHD não deve ser uma máquina virtual de geração 2.
* Olá VHD pode ser um tamanho fixo ou expansão dinâmica. Um VHD de expansão dinâmica é recomendado porque ela usa menos tooAzure tooupload de tempo que um arquivo VHD de tamanho fixo.
* disco Olá deve ser inicializado usando o estilo de particionamento Olá registro mestre de inicialização (MBR). Não há suporte para a saudação estilo de partição GUID partição GPT (tabela).
* Olá VHD deve conter uma única instalação do Windows Server 2012 R2. Ele deve conter vários volumes, mas apenas um que contenha uma instalação do Windows.
* função de Host de sessão de área de trabalho remota (RDSH) Hello e o recurso Experiência Desktop de saudação devem ser instalados.
* função de agente de Conexão de área de trabalho remota Olá deve *não* ser instalado.
* Olá Encrypting File System (EFS) deve ser desabilitada.
* Olá imagem deve ser submetida a Sysprep usando parâmetros de saudação **/oobe /generalize /shutdown** (não use Olá **/Mode: VM** parâmetro).
* Não há suporte para carregar o VHD de uma cadeia de instantâneo.

Consulte [Criar uma imagem do RemoteApp do Azure](remoteapp-imageoptions.md) para obter mais informações sobre a criação de imagens para o RemoteApp do Azure.

