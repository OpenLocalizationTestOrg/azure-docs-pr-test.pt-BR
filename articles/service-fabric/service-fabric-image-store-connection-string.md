---
title: "aaaAzure cadeia de conexão de repositório de imagens do Service Fabric | Microsoft Docs"
description: "Entender a cadeia de conexão de repositório de imagens de saudação"
services: service-fabric
documentationcenter: .net
author: alexwun
manager: timlt
editor: 
ms.assetid: 00f8059d-9d53-4cb8-b44a-b25149de3030
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: alexwun
ms.openlocfilehash: 83f5ad75b5df07726997da3173722028255b8cae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-imagestoreconnectionstring-setting"></a>Entender a configuração de ImageStoreConnectionString de saudação

Em alguns nossa documentação, vamos mencionar brevemente existência de saudação de um parâmetro de "ImageStoreConnectionString" sem que descreve o que realmente significa. E depois passando por um artigo como [implantar e remover aplicativos usando o PowerShell][10], parece que tudo é o valor de saudação de copiar/colar como ele aparece no manifesto do cluster de saudação do destino Olá cluster. Para configuração de saudação sejam configurável por cluster, mas quando você cria um cluster por meio de saudação [portal do Azure][11], não há nenhuma opção tooconfigure essa configuração e é sempre "fabric: ImageStore". Qual é a finalidade de saudação dessa configuração?

![Manifesto do cluster][img_cm]

Service Fabric foi iniciada como uma plataforma para consumo interno do Microsoft por muitas equipes diferentes, para alguns aspectos são altamente personalizáveis - Olá "Image Store" é um aspecto tal. Essencialmente, Olá Image Store é um repositório conectável para armazenar os pacotes de aplicativos. Quando seu aplicativo é implantado tooa nó no cluster Olá, o nó baixa conteúdo de saudação do seu pacote de aplicativo de saudação Image Store. Olá ImageStoreConnectionString é uma configuração que inclui todas as informações necessárias de saudação para clientes e nós toofind Olá imagem repositório correto para um determinado cluster.

Existem três tipos possíveis de provedores de armazenamento de imagens e suas cadeias de conexão correspondentes são os seguintes:

1. Serviço de Armazenamento de Imagens: "fabric:ImageStore"

2. Sistema de Arquivos: "file:[caminho do sistema de arquivos]"

3. Armazenamento do Azure: "xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"

tipo de provedor de saudação usado na produção é Olá serviço de repositório de imagem, que é um serviço de sistema persistente com monitoração de estado que você pode ver no Gerenciador do Service Fabric. 

![Serviço de armazenamento de imagens][img_is]

Hospedagem hello Image Store em um serviço de sistema dentro do próprio cluster Olá elimina dependências externas para o repositório de pacotes de saudação e nos dá mais controle sobre a localidade de saudação do armazenamento. As melhorias futuras no hello repositório de imagens é provavelmente tootarget provedor de repositório de imagens de Olá primeiro, se não exclusivamente. cadeia de caracteres de conexão de saudação para o provedor de serviço de repositório de imagem Olá não tem nenhuma informação exclusiva desde que o cliente Olá já está conectado toohello cluster de destino. cliente Olá só precisa tooknow que protocolos direcionando o serviço do sistema Olá devem ser usados.

Olá sistema de arquivos provedor é usado em vez da saudação serviço de repositório de imagens para clusters de uma caixa locais durante o cluster de saudação do desenvolvimento toobootstrap ligeiramente mais rápido. diferença de saudação seja normalmente pequena, mas é uma otimização útil para a maioria das pessoas durante o desenvolvimento. É possível toodeploy uma caixa local de um cluster com hello outros tipos de provedor de armazenamento, mas geralmente não há nenhum motivo toodo assim como fluxo de trabalho de desenvolvimento/teste Olá permanece Olá mesmo, independentemente do provedor. Diferentes esse uso, provedores de sistema de arquivos e armazenamento do Azure Olá só existem para dar suporte.

Portanto enquanto Olá ImageStoreConnectionString é configurável, você geralmente apenas use Olá configuração padrão. Ao publicar tooAzure por meio de [Visual Studio][12], parâmetro hello será definido automaticamente para você adequadamente. Para tooclusters implantação programática hospedado no Azure, a cadeia de caracteres de conexão de saudação é sempre "fabric: ImageStore". Embora em caso de dúvida, seu valor pode ser verificado sempre recuperando Olá manifesto do cluster por [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), ou [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest). Locais de teste e clusters de produção devem sempre ser o provedor de serviço de repositório de imagens de saudação toouse configurado também.

### <a name="next-steps"></a>Próximas etapas
[Implantar e remover aplicativos usando o PowerShell][10]

<!--Image references-->
[img_is]: ./media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: ./media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md
