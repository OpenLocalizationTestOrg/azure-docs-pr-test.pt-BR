---
title: "configurações de aaaCustom para ambientes de serviço de aplicativo"
description: "Definições de configuração personalizadas para Ambientes de Serviço de Aplicativo"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a>Definições de configuração personalizadas para Ambientes de Serviço de Aplicativo
## <a name="overview"></a>Visão geral
Como os ambientes de serviço de aplicativo isolado tooa único cliente, há determinadas definições de configuração que podem ser aplicadas tooApp exclusivamente os ambientes de serviço. Este artigo documenta Olá várias personalizações específicas que estão disponíveis para ambientes de serviço de aplicativo.

Se você não tiver um ambiente de serviço de aplicativo, consulte [como tooCreate um ambiente de serviço de aplicativo](app-service-web-how-to-create-an-app-service-environment.md).

Você pode armazenar as personalizações do ambiente de serviço de aplicativo usando uma matriz em Olá novo **clusterSettings** atributo. Esse atributo é encontrado no dicionário "Propriedades" Olá Olá *hostingEnvironments* entidade do Gerenciador de recursos do Azure.

seguinte trecho de modelo do Gerenciador de recursos abreviado Hello mostra Olá **clusterSettings** atributo:

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

Olá **clusterSettings** atributo pode ser incluído em uma saudação de tooupdate de modelo do Gerenciador de recursos o ambiente de serviço de aplicativo.

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a>Use o Gerenciador de recursos do Azure tooupdate um ambiente de serviço de aplicativo
Como alternativa, você pode atualizar Olá ambiente de serviço de aplicativo usando [Gerenciador de recursos do Azure](https://resources.azure.com).  

1. No Gerenciador de recursos, vá para o nó de toohello para Olá ambiente de serviço de aplicativo (**assinaturas** > **resourceGroups** > **provedores**  >  **Microsoft** > **hostingEnvironments**). Clique Olá ambiente de serviço de aplicativo específico que você deseja tooupdate.
2. No painel direito da saudação, clique em **leitura/gravação** no tooallow de barra de ferramentas superior Olá interativo de edição no Gerenciador de recursos.  
3. Clique em Olá azul **editar** modelo Olá de Gerenciador de recursos do toomake botão editável.
4. Rolagem toohello parte inferior do painel direito da saudação. Olá **clusterSettings** atributo é Olá parte mais inferior, onde você pode inserir ou atualizar o seu valor.
5. Matriz de saudação tipo (ou copiar e colar) de valores de configuração que você deseja no hello **clusterSettings** atributo.  
6. Clique em Olá verde **colocar** botão que foi localizado na parte superior de saudação do hello painel direito toocommit Olá alteração toohello ambiente de serviço de aplicativo.

No entanto, enviar alterações hello, que leva aproximadamente 30 minutos, multiplicados pelo número de saudação do front-ends no hello ambiente de serviço de aplicativo para Olá alterar tootake efeito.
Por exemplo, se um ambiente de serviço de aplicativo tem quatro front-ends, levará aproximadamente duas horas para Olá toofinish de atualização de configuração. Embora a alteração de configuração hello está sendo revertida, outras operações de dimensionamento ou operações de alteração de configuração podem ocorrer em Olá ambiente de serviço de aplicativo.

## <a name="disable-tls-10"></a>Desabilitar o TLS 1.0
Uma pergunta recorrente de clientes, especialmente os clientes estejam lidando com conformidade PCI auditorias, é como tooexplicitly desabilitar o TLS 1.0 para seus aplicativos.

TLS 1.0 pode ser desabilitado por meio do seguinte Olá **clusterSettings** entrada:

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a>Mudar a ordem do pacote de criptografia TLS
Outra pergunta de clientes é se eles podem modificar a lista Olá codificações negociado por seu servidor e isso pode ser feito por meio de modificação Olá **clusterSettings** conforme mostrado abaixo. lista de saudação de conjuntos de codificação disponíveis pode ser recuperada de [este artigo do MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> Se forem definidos valores incorretos para o conjunto de codificação de saudação SChannel não é possível entender, todos os servidores de tooyour de comunicação TLS podem parar de funcionar. Nesse caso, você precisará Olá tooremove *FrontEndSSLCipherSuiteOrder* entrada do **clusterSettings** e enviar Olá atualizado codificação padrão do Gerenciador de recursos modelo toorevert toohello back configurações de pacote.  Use esta funcionalidade com cuidado.
> 
> 

## <a name="get-started"></a>Introdução
site de modelo do Gerenciador de recursos de início rápido do Azure Olá inclui um modelo com a definição base Olá para [criando um ambiente de serviço de aplicativo](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).

<!-- LINKS -->

<!-- IMAGES -->
