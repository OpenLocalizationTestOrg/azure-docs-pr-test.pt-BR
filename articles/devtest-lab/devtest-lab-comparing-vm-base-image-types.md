---
title: "aaaComparing imagens personalizadas e as fórmulas em DevTest Labs | Microsoft Docs"
description: "Saiba mais sobre as diferenças de saudação entre imagens personalizadas e as fórmulas como bases de VM para que você possa decidir qual mais adequada para seu ambiente."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a>Comparando imagens personalizadas e fórmulas em Laboratórios de Desenvolvimento/Teste
É possível usar tanto as [imagens personalizadas](devtest-lab-create-template.md) quanto as [fórmulas](devtest-lab-manage-formulas.md) como bases para as [novas VMs criadas](devtest-lab-add-vm-with-artifacts.md). No entanto, a principal diferença Olá entre imagens personalizadas e as fórmulas é uma imagem personalizada é simplesmente uma imagem com base em um VHD, enquanto uma fórmula é uma imagem com base em um VHD *além* pré-configurado configurações - como tamanho da VM, uma rede virtual, subrede e artefatos. Essas configurações predefinidas são configuradas com valores padrão que podem ser substituídos no tempo de saudação da criação de VM. Este artigo explica algumas das vantagens de saudação (profissionais) e desvantagens imagens personalizadas do toousing (contras) versus usando fórmulas.

## <a name="custom-image-pros-and-cons"></a>Prós e contras das imagens personalizadas
Imagens personalizadas fornecem um modo estático, imutável toocreate VMs de um ambiente desejado. 

**Prós**

* Provisionamento de uma imagem personalizada da VM é rápida como nada muda após Olá que passe VM da imagem de saudação. Em outras palavras, não há nenhum tooapply configurações como imagem personalizada Olá é apenas uma imagem sem configurações. 
* VMs criadas por meio de uma única imagem personalizada são idênticas.

**Contras**

* Se você precisar tooupdate algum aspecto da imagem personalizada do hello, imagem Olá deve ser recriada.  

## <a name="formula-pros-and-cons"></a>Prós e contras da fórmula
Fórmulas fornecem uma maneira dinâmica toocreate VMs do hello desejado configurações.

**Prós**

* Alterações no ambiente de saudação podem ser capturadas em Olá instantaneamente por meio de artefatos. Por exemplo, se você desejar uma VM instalada com o bits mais recentes de saudação do seu pipeline de versão ou inscrever-se código mais recente de saudação do seu repositório, você simplesmente especificar um artefato que implanta os bits mais recentes hello ou inscreve código mais recente de saudação na fórmula Olá junto com um imagem de base de destino. Sempre que essa fórmula é usada toocreate VMs, Olá bits/código mais recente são implantados/inscrito toohello VM. 
* As fórmulas podem definir as configurações padrão que as imagens personalizadas não podem fornecer, como configurações de rede virtual e tamanhos de VM. 
* configurações de saudação salvos em uma fórmula são mostradas como valores padrão, mas podem ser modificadas quando Olá VM é criada. 

**Contras**

* Criar uma VM por meio de uma fórmula pode levar mais tempo do que criar uma VM por meio de uma imagem personalizada.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Postagens de blogs relacionadas
* [Imagens personalizadas ou fórmulas?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Próximas etapas
- [Perguntas frequentes do DevTest Labs](devtest-lab-faq.md)