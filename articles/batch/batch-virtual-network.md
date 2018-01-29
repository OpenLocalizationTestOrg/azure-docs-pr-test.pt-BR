---
title: Provisionar o pool do Lote do Azure em uma rede virtual | Microsoft Docs
description: "Você pode criar um pool do Lote em uma rede virtual para que os nós de computação possam se comunicar com segurança com outras VMs na rede, como, por exemplo, um servidor de arquivos."
services: batch
author: v-dotren
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 10/16/2017
ms.author: v-dotren
ms.openlocfilehash: f34647afc600b72704859952d0a40edad4a3b40f
ms.sourcegitcommit: f8437edf5de144b40aed00af5c52a20e35d10ba1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2017
---
# <a name="create-an-azure-batch-pool-in-a-virtual-network"></a>Criar um pool do Lote do Azure em uma rede virtual


Quando você cria um pool do Lote do Azure, você pode provisionar o pool em uma sub-rede de uma [rede virtual do Azure](../virtual-network/virtual-networks-overview.md) (VNet) que você especificar. Este artigo explica como configurar um pool do Lote em uma rede virtual. 



## <a name="why-use-a-vnet"></a>Por que usar uma rede virtual?


Um pool do Lote do Azure tem configurações que permitem que os nós de computação se comuniquem entre si - por exemplo, para executar tarefas de várias instâncias. Essas configurações não exigem uma rede virtual separada. No entanto, por padrão, os nós não podem se comunicar com máquinas virtuais que não fazem parte do pool do Lote, como um servidor de licença ou um servidor de arquivos. Para permitir que nós de computação do pool se comuniquem de forma segura com outras máquinas virtuais, ou com uma rede local, você pode provisionar o pool em uma sub-rede de uma rede virtual do Azure. 



## <a name="prerequisites"></a>Pré-requisitos

* **Autenticação**. Para usar uma rede virtual do Azure, a API do cliente do Lote deverá usar a autenticação do Azure Active Directory (AD). O suporte ao Lote do Azure para o Azure AD está documentado em [Autenticar soluções do serviço Lote com o Active Directory](batch-aad-auth.md). 

* **Uma rede virtual do Azure**. Para preparar uma rede virtual com uma ou mais sub-redes com antecedência, você pode usar o portal do Azure, o Azure PowerShell, a interface de linha de comando (CLI) do Azure ou outros métodos. Para criar uma rede virtual baseada no Azure Resource Manager, consulte [Criar uma rede virtual com várias sub-redes](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Para criar uma rede virtual clássica, consulte [Criar uma rede virtual (clássica) com várias sub-redes](../virtual-network/create-virtual-network-classic.md).

### <a name="vnet-requirements"></a>Requisitos de rede virtual
[!INCLUDE [batch-virtual-network-ports](../../includes/batch-virtual-network-ports.md)]
    
## <a name="create-a-pool-with-a-vnet-in-the-portal"></a>Criar um pool com uma rede virtual no portal

Depois de criar sua rede virtual e ter atribuído uma sub-rede a ele, você pode criar um pool do Lote com essa rede virtual. Siga estas etapas para criar um pool no portal do Azure: 



1. Navegue até sua conta do Lote no portal do Azure. Esta conta deve estar na mesma assinatura e na mesma região que o grupo de recursos que contém a imagem que você deseja usar. 
2. Na janela **Configurações** à esquerda, selecione o item de menu **Pools**.
3. Na janela **Pools**, selecione o comando **Adicionar**.
4. Na janela **Adicionar pool**, selecione a opção que você deseja usar na lista suspensa **Tipo de imagem**. 
5. Selecione o **Editor/Oferta/SKU** correto para sua imagem personalizada.
6. Especifique o restante das configurações necessárias, incluindo o **Tamanho do nó**, os **Nós dedicados de destino** e os **Nós de baixa prioridade**, bem como qualquer configuração opcional desejada.
7. Em **Rede virtual**, selecione a rede virtual e a sub-rede que você deseja usar.
  
  ![Adicionar pool com a rede virtual](./media/batch-virtual-network/add-vnet-pool.png)

## <a name="user-defined-routes-for-forced-tunneling"></a>Rotas definidas pelo usuário para o túnel forçado

Você pode ter requisitos em sua organização para redirecionar (forçar) o tráfego associado à Internet da sub-rede de volta para a sua localização para inspeção e registro em log. Talvez você tenha habilitado o túnel forçado para as sub-redes na sua rede virtual. 

Para garantir que seus nós de computação do pool do Lote do Azure funcionam em uma rede virtual com túnel forçado habilitado, você deve adicionar as seguintes [rotas definidas pelo usuário](../virtual-network/virtual-networks-udr-overview.md) para essa sub-rede:

* O serviço do Lote precisa se comunicar com os nós de computação do pool para o agendamento de tarefas. Para habilitar essa comunicação, adicione uma rota definida pelo usuário para cada endereço IP usado pelo serviço do Lote na região onde existe sua conta do Lote. Para obter a lista de endereços IP do serviço do Lote, entre em contato com o Suporte do Azure.

* Certifique-se de que o tráfego de saída no Armazenamento do Azure (especificamente, as URLs da forma `<account>.table.core.windows.net`, `<account>.queue.core.windows.net` e `<account>.blob.core.windows.net`) não está bloqueado por meio de seu dispositivo de rede local.

Quando você adicionar uma rota definida pelo usuário, defina a rota para cada prefixo de endereço IP de lote relacionado e defina **Próximo tipo de salto** como **Internet**. Veja os exemplos a seguir:

![Rota definida pelo usuário](./media/batch-virtual-network/user-defined-route.png)

## <a name="next-steps"></a>Próximas etapas

- Para uma visão geral detalhada do Lote, confira [Desenvolver soluções de computação paralela em grande escala com o Lote](batch-api-basics.md).
- Para saber mais sobre como criar uma rota definida pelo usuário, consulte [Create a user-defined route – Azure portal](../virtual-network/create-user-defined-route-portal.md) (Criar uma rota definida pelo usuário – Portal do Azure).
