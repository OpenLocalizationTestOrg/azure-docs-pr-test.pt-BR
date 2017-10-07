---
title: aaaIntegrate uma conta de armazenamento do Azure com o Azure CDN | Microsoft Docs
description: "Saiba como o conteúdo de rede de fornecimento de conteúdo (CDN) do Azure toodeliver alta largura de banda de saudação toouse armazenando em cache blobs do armazenamento do Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a>Integrar uma conta de armazenamento do Azure com a CDN do Azure
CDN pode ser habilitado toocache conteúdo do armazenamento do Azure. Ele oferece aos desenvolvedores uma solução global para distribuir o conteúdo de alta largura de banda ao armazenar em cache o conteúdo estático de instâncias de computação em nós físicos nos Estados Unidos de hello, Europa, Ásia, Austrália e América do Sul e blobs.

## <a name="step-1-create-a-storage-account"></a>Etapa 1: Criar uma conta de armazenamento
Use Olá seguindo o procedimento toocreate uma nova conta de armazenamento para uma assinatura do Azure. A conta de armazenamento dá acesso aos serviços de armazenamento do Azure. conta de armazenamento de saudação representa o nível mais alto de Olá Olá namespace para acessar cada um dos componentes de serviço de armazenamento do Azure Olá: services, serviços de fila e tabela serviços de Blob. Para obter mais informações, consulte toohello [tooMicrosoft Introdução armazenamento do Azure](../storage/common/storage-introduction.md).

toocreate uma conta de armazenamento, você deve ser administrador de serviço hello ou um coadministrador para Olá associado assinatura.

> [!NOTE]
> Há vários métodos que você pode usar toocreate uma conta de armazenamento, inclusive Olá Portal do Azure e do Powershell.  Para este tutorial, usaremos Olá Portal do Azure.  
> 
> 

**toocreate uma conta de armazenamento para uma assinatura do Azure**

1. Entrar toohello [Portal do Azure](https://portal.azure.com).
2. No canto esquerdo superior do hello, selecione **novo**. Em Olá **novo** caixa de diálogo, selecione **dados + armazenamento**, em seguida, clique em **conta de armazenamento**.
    
    Olá **criar conta de armazenamento** folha é exibida.   

    ![Criar conta de armazenamento][create-new-storage-account]  

3. Em Olá **nome** , digite um nome de subdomínio. Essa entrada pode conter de 3 a 24 letras minúsculas e números.
   
    Esse valor se torna o nome do host Olá no hello URI que é usado para endereçar recursos de Blob, fila ou tabela para a assinatura de saudação. Para endereçar um recurso de contêiner no serviço Blob da saudação, você usaria um URI no hello seguinte formato, onde * &lt;StorageAccountLabel&gt; * refere-se o valor de toohello que você digitou na **insira uma URL**:
   
    http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*
   
    **Importante:** Olá subdomínio do URL rótulo formulários Olá Olá da conta de armazenamento URI e deve ser exclusivo entre todos os serviços hospedados no Azure.
   
    Esse valor também é usado como nome de saudação dessa conta de armazenamento no portal de hello, ou ao acessar essa conta por meio de programação.
4. Mantenha os padrões de saudação para **modelo de implantação**, **conta tipo**, **desempenho**, e **replicação**. 
5. Selecione Olá **assinatura** que a conta de armazenamento hello será usada com.
6. Selecione ou crie um **Grupo de Recursos**.  Para saber mais sobre Grupos de Recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Selecione um local para sua conta de armazenamento.
8. Clique em **Criar**. processo de saudação de criação de conta de armazenamento Olá pode levar várias toocomplete de minutos.

## <a name="step-2-enable-cdn-for-hello-storage-account"></a>Etapa 2: Habilitar a CDN Olá conta de armazenamento

Com a integração mais recente do hello, agora você pode habilitar CDN para sua conta de armazenamento sem sair de sua extensão de portal de armazenamento. 

1. Selecione a conta de armazenamento hello, pesquisar "CDN" ou role para baixo no menu de navegação à esquerda de saudação, clique em "CDN do Azure".
    
    Olá **Azure CDN** folha é exibida.

    ![navegação habilitada para cdn][cdn-enable-navigation]
    
2. Criar um novo ponto de extremidade inserindo informações de saudação necessária
    - **Perfil CDN**: você pode criar um novo perfil ou usar um existente.
    - **Camada de preços**: você só precisa tooselect um preço se você criar um novo perfil CDN.
    - **Nome do ponto de extremidade da CDN**: insira um nome de ponto de extremidade de sua escolha.

    > [!TIP]
    > Por padrão, o ponto de extremidade CDN Olá criado usa Olá hostname de sua conta de armazenamento como origem.

    ![cdn new endpoint creation][cdn-new-endpoint-creation]

3. Após a criação, novo ponto de extremidade de saudação aparecerão na lista de ponto de extremidade de saudação acima.

    ![novo ponto de extremidade do armazenamento da cdn][cdn-storage-new-endpoint]

> [!NOTE]
> Você também pode ir tooAzure CDN extensão tooenable CDN. [Tutorial](#Tutorial-cdn-create-profile).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a>Etapa 3: Habilitar recursos adicionais da CDN

Na folha de "Azure CDN" da conta de armazenamento, clique em ponto de extremidade CDN de saudação da folha de configuração Olá lista tooopen CDN. Você pode habilitar recursos adicionais da CDN para o fornecimento, como compactação, cadeia de caracteres de consulta e filtragem de área geográfica. Você também pode adicionar o ponto de extremidade CDN tooyour de mapeamento de domínio personalizado e habilitar HTTPS do domínio personalizado.
    
![configuração da cdn do armazenamento da CDN][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a>Etapa 4: acessar conteúdo da CDN
use Olá URL CDN tooaccess armazenado em cache o conteúdo em Olá CDN, fornecido no portal de saudação. endereço de saudação para um blob armazenado em cache será a seguir toohello semelhante:

http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\>

> [!NOTE]
> Depois de habilitar a conta de armazenamento de tooa de acesso à CDN, todos os objetos publicamente disponíveis são qualificados para o cache de borda da CDN. Se você modificar um objeto que está atualmente armazenada em cache Olá CDN, novo conteúdo de saudação não estará disponível por meio de saudação CDN até Olá CDN atualize seu conteúdo quando o período de tempo de vida conteúdo Olá armazenado em cache expira.
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a>Etapa 5: Remover conteúdo da saudação CDN
Se você não deseja mais toocache um objeto no hello Azure Content Delivery Network (CDN), você pode executar uma das Olá etapas a seguir:

* Você pode fazer Olá privado de contêiner, e não público. Consulte [gerenciar o acesso de leitura anônimo toocontainers e blobs](../storage/blobs/storage-manage-access-to-resources.md) para obter mais informações.
* Você pode desabilitar ou excluir o ponto de extremidade CDN hello usando Olá Portal de gerenciamento.
* Você pode modificar seu toorequests de responder mais tempo do serviço hospedado toono para objeto hello.

Um objeto já armazenado em cache no hello CDN permanecerá em cache até que Olá tempo de vida do objeto Olá expirar ou ponto de extremidade de saudação é apagado. Quando o período de tempo de vida de saudação expira, Olá CDN verificará toosee se o ponto de extremidade do hello CDN ainda é válido e o objeto de saudação permanece acessível anonimamente. Se não for, não será armazenada em objeto hello.

## <a name="additional-resources"></a>Recursos adicionais
* [Como tooMap conteúdo CDN tooa domínio personalizado](cdn-map-content-to-custom-domain.md)
* [Habilitar o HTTPS para seu domínio personalizado](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
