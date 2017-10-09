---
title: gateway de dados local aaaInstall | Microsoft Docs
description: Saiba como tooinstall e configure um gateway de dados local.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a>Instalar e configurar um gateway de dados local
Um gateway de dados local é necessário quando um ou mais servidores de serviços de análise do Azure no hello mesmo região se conectar a fontes de dados locais tooon. toolearn mais sobre o gateway hello, consulte [gateway de dados no local](analysis-services-gateway.md).

## <a name="prerequisites"></a>Pré-requisitos
**Requisitos mínimos:**

* .NET 4.5 Framework
* Versão de 64 bits do Windows 7/Windows Server 2008 R2 (ou posterior)

**Recomendados:**

* CPU de 8 núcleos
* Memória de 8 GB
* Versão de 64 bits do Windows 2012 R2 (ou posterior)

**Considerações importantes:**

* Durante a instalação, ao registrar o gateway com o Azure, a região de padrão de saudação para sua assinatura está selecionada. Você pode escolher uma região diferente. Se tiver servidores em mais de uma região, você precisará instalar um gateway para cada região. 
* gateway de saudação não pode ser instalado em um controlador de domínio.
* Apenas um gateway pode ser instalado em um computador.
* Instale o gateway de saudação em um computador que permanece no e não vai toosleep.
* Não instale o gateway de saudação em uma rede sem fio conectada tooyour de computador. O desempenho pode ser prejudicado.


## <a name="download"></a>Baixar
 [Baixar o gateway Olá](https://aka.ms/azureasgateway)

## <a name="install"></a>Instalar

1. Execute a instalação.

2. Selecione um local, aceite os termos de saudação e, em seguida, clique em **instalar**.

   ![Instale os termos de licença e de local](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. Selecione **Gateway de dados local (recomendado)**. O Azure Analysis Services não dá suporte ao modo pessoal.

   ![Escolha o tipo de gateway](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. Insira uma conta toosign em tooAzure. Olá conta deve ser no Azure Active Directory do seu locatário. Essa conta é usada para o administrador do gateway hello. 

   ![Insira uma conta toosign em tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > Se você entrar com uma conta de domínio, ele será mapeado conta organizacional tooyour no AD do Azure. Sua conta organizacional será usada como o administrador do gateway Olá Olá.

## <a name="register"></a>Registrar
Ordem toocreate um recurso de gateway no Azure, você deve registrar instância local do hello instalado com hello serviço de nuvem do Gateway. 

1.  Selecione **Registrar um novo gateway neste computador**.

    ![Registrar](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. Digite um nome e uma chave de recuperação para o gateway. Por padrão, o gateway Olá usa região padrão de sua assinatura. Se você precisar tooselect uma região diferente, selecione **alteração região**.

   ![Registrar](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <a name="create-resource"></a>Criar um recurso de gateway do Azure
Depois de instalado e registrado seu gateway, você precisa toocreate um recurso de gateway na sua assinatura do Azure. Entrar tooAzure com hello mesma conta usada ao registrar o gateway de saudação.

1. No portal do Azure, clique em **Criar um novo serviço** > **Enterprise Integration** > **Gateway de dados local** > **Criar**.

   ![Criar um recurso de gateway](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. Em **Criar gateway de conexão**, insira estas configurações:

    * **Nome**: insira um nome para o recurso do gateway. 

    * **Assinatura**: selecione Olá tooassociate de assinatura do Azure com o recurso de gateway. 
    Essa assinatura deve ser Olá a mesma assinatura que seus servidores estão em.
   
      assinatura do saudação padrão baseia-se em Olá conta do Azure que você usou toosign no.

    * **Grupo de recursos**: Crie um novo grupo de recursos ou escolha um grupo de recursos existente.

    * **Local**: região Olá selecione registrado o gateway.

    * **Nome da instalação**: se a instalação do gateway não estiver selecionada, o gateway de saudação selecione registrado. 

    Quando tiver concluído, clique em **Criar**.

## <a name="connect-servers"></a>Conecte-se a recursos de servidores de gateway toohello

1. Na visão geral de seu servidor do Azure Analysis Services, clique em **Gateway de Dados Local**.

   ![Conecte-se o servidor toogateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. Em **escolher um Gateway de dados local tooconnect**, selecione o recurso de gateway e, em seguida, clique em **gateway selecionado conectar**.

   ![Conecte-se o recurso do servidor toogateway](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > Se o gateway não aparecer na lista de saudação, seu servidor provavelmente não está em Olá mesma região que a região Olá você especificou ao registrar o gateway de saudação. 

É isso. Se você precisa tooopen portas ou fazer qualquer solução de problemas, ser toocheck se out [gateway de dados no local](analysis-services-gateway.md).

## <a name="next-steps"></a>Próximas etapas
* [Gerenciar o Analysis Services](analysis-services-manage.md)   
* [Obter dados do Azure Analysis Services](analysis-services-connect.md)
