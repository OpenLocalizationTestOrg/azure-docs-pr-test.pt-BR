---
title: aaaIntegrate DNS do Azure com os recursos do Azure | Microsoft Docs
description: Saiba como toouse DNS do Azure ao longo de tooprovide DNS para os recursos do Azure.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: b9b6f829513f0ad9da510190c75bc60dc7431545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-dns-tooprovide-custom-domain-settings-for-an-azure-service"></a>Use as configurações do DNS do Azure tooprovide domínio personalizado para um serviço do Azure

O DNS do Azure fornece o DNS para um domínio personalizado para qualquer um dos recursos do Azure que dão suporte a domínios personalizados ou que têm um FQDN (nome de domínio totalmente qualificado). Um exemplo é ter um aplicativo web do Azure e deseja que seus usuários tooaccess-lo pelo usando contoso.com ou www.contoso.com como um FQDN. Este artigo o orienta na configuração do serviço do Azure com o DNS do Azure para usar domínios personalizados.

## <a name="prerequisites"></a>Pré-requisitos

Em ordem toouse DNS do Azure para seu domínio personalizado, primeiro você deve delegar tooAzure seu domínio DNS. Visite [delegar tooAzure um domínio DNS](./dns-delegate-domain-azure-dns.md) para obter instruções sobre como tooconfigure seus servidores de nome para delegação. Após seu domínio delegado tooyour zona de DNS do Azure, você está tooconfigure capaz de registros de DNS de saudação necessários.

Você pode configurar um domínio intuitivo ou personalizado para [Aplicativos de Funções do Azure](#azure-function-app), [IoT do Azure](#azure-iot), [Endereços IP públicos](#public-ip-address), [Serviço de Aplicativo (Aplicativos Web)](#app-service-web-apps), [Armazenamento de Blobs](#blob-storage) e [Azure CDN](#azure-cdn).

## <a name="azure-function-app"></a>Aplicativo de Funções do Azure

tooconfigure um domínio personalizado para aplicativos de função do Azure, é criado um registro CNAME, bem como a configuração no próprio aplicativo de função hello.
 
Navegue muito**outros** > **aplicativo função** e selecione seu aplicativo de função. Clique em **Recursos de plataforma** e, em **REDE**, clique **Domínios personalizados**.

![folha de aplicativo de funções](./media/dns-custom-domain/functionapp.png)

Anote a url atual Olá em Olá **domínios personalizados** folha, esse endereço é usada como alias Olá para registro DNS Olá criado.

![folha de domínio personalizado](./media/dns-custom-domain/functionshostname.png)

Navegue tooyour zona de DNS e clique em **+ registrar conjunto**. Preencha Olá seguintes informações sobre Olá **Adicionar conjunto de registros** folha e clique em **Okey** toocreate-lo.

|Propriedade  |Valor  |Descrição  |
|---------|---------|---------|
|Nome     | myfunctionapp        | Esse valor junto com o rótulo de nome de domínio Olá é hello FQDN para o nome de domínio personalizado de saudação.        |
|Tipo     | CNAME        | Use um registro CNAME que esteja usando um alias.        |
|TTL     | 1        | 1 é usado por 1 hora        |
|Unidade de TTL     | Horas        | Horas são usadas como medida de tempo de saudação         |
|Alias     | adatumfunction.azurewebsites.net        | nome DNS Olá você está criando o alias Olá, neste exemplo é Olá adatumfunction.azurewebsites.net DNS nome fornecido pelo aplicativo de função toohello padrão.        |

Navegue tooyour back função aplicativo, clique em **recursos da plataforma**e, em **rede** clique em **domínios personalizados**, em seguida em **osnomesdehost**clique **+ Adicionar nome de host**.

Em Olá **Adicionar nome de host** folha, insira o registro CNAME Olá no hello **hostname** campo de texto e clique em **validar**. Se o registro de saudação toobe capaz de encontrar, Olá **Adicionar nome de host** botão é exibido. Clique em **Adicionar nome de host** tooadd alias de saudação.

![aplicativos de função adicionam a folha de nome do host](./media/dns-custom-domain/functionaddhostname.png)

## <a name="azure-iot"></a>IoT do Azure

IoT do Azure não tem todas as personalizações que são necessários no próprio serviço hello. toouse um domínio personalizado com um IoT Hub somente um registro CNAME apontada recursos toohello é necessária.

Navegue muito**Internet das coisas** > **IoT Hub** e selecione seu hub IoT. Em Olá **visão geral** folha, Olá Observação FQDN do hub IoT de saudação.

![Folha Hub IoT](./media/dns-custom-domain/iot.png)

Em seguida, navegue tooyour zona de DNS e clique em **+ registrar conjunto**. Preencha Olá seguintes informações sobre Olá **Adicionar conjunto de registros** folha e clique em **Okey** toocreate-lo.


|Propriedade  |Valor  |Descrição  |
|---------|---------|---------|
|Nome     | myiothub        | Esse valor junto com o rótulo de nome de domínio Olá é hello FQDN para o hub IoT de saudação.        |
|Tipo     | CNAME        | Use um registro CNAME que esteja usando um alias.
|TTL     | 1        | 1 é usado por 1 hora        |
|Unidade de TTL     | Horas        | Horas são usadas como medida de tempo de saudação         |
|Alias     | adatumIOT.azure-devices.net        | nome DNS Olá você está criando o alias Olá, neste exemplo é nome do host adatumIOT.azure devices.net Olá fornecido pelo hub IoT de saudação.

Depois de criar o registro hello, testar a resolução de nomes com o registro CNAME hello usando`nslookup`

## <a name="public-ip-address"></a>Endereço IP público

tooconfigure um domínio personalizado para serviços que usam um IP público endereço recurso como Application Gateway, o balanceador de carga, o serviço de nuvem, máquinas virtuais do Gerenciador de recursos, e, VMs clássico, um registro CNAME é usado.

Navegue muito**rede** > **endereço IP público**, selecione o recurso de IP público hello e clique em **configuração**. Notificar o endereço IP hello mostrado.

![folha de ip público](./media/dns-custom-domain/publicip.png)

Navegue tooyour zona de DNS e clique em **+ registrar conjunto**. Preencha Olá seguintes informações sobre Olá **Adicionar conjunto de registros** folha e clique em **Okey** toocreate-lo.


|Propriedade  |Valor  |Descrição  |
|---------|---------|---------|
|Nome     | mywebserver        | Esse valor junto com o rótulo de nome de domínio Olá é hello FQDN para o nome de domínio personalizado de saudação.        |
|Tipo     | Uma        | Use um registro como recursos de saudação é um endereço IP.        |
|TTL     | 1        | 1 é usado por 1 hora        |
|Unidade de TTL     | Horas        | Horas são usadas como medida de tempo de saudação         |
|Endereço IP     | <your ip address>       | endereço IP público de saudação.|

![criar um registro A](./media/dns-custom-domain/arecord.png)

Depois de saudação um registro é criado, execute `nslookup` toovalidate Olá registro converte.

![pesquisa de dns do ip público](./media/dns-custom-domain/publicipnslookup.png)

## <a name="app-service-web-apps"></a>Serviço de Aplicativo (Aplicativos Web)

Olá seguinte levá-lo a configurar um domínio personalizado para um aplicativo de serviço de aplicativo web.

Navegue muito**Web e móveis** > **do serviço de aplicativo** e selecione o recurso de saudação você estiver configurando um nome de domínio personalizado e clique em **domínios personalizados**.

Anote a url atual Olá em Olá **domínios personalizados** folha, esse endereço é usada como alias Olá para registro DNS Olá criado.

![folha de domínios personalizados](./media/dns-custom-domain/url.png)

Navegue tooyour zona de DNS e clique em **+ registrar conjunto**. Preencha Olá seguintes informações sobre Olá **Adicionar conjunto de registros** folha e clique em **Okey** toocreate-lo.


|Propriedade  |Valor  |Descrição  |
|---------|---------|---------|
|Nome     | mywebserver        | Esse valor junto com o rótulo de nome de domínio Olá é hello FQDN para o nome de domínio personalizado de saudação.        |
|Tipo     | CNAME        | Use um registro CNAME que esteja usando um alias. Se o recurso de saudação usado um endereço IP, um registro seria usado.        |
|TTL     | 1        | 1 é usado por 1 hora        |
|Unidade de TTL     | Horas        | Horas são usadas como medida de tempo de saudação         |
|Alias     | webserver.azurewebsites.net        | nome DNS Olá você está criando o alias Olá, neste exemplo é Olá webserver.azurewebsites.net DNS nome fornecido pelo aplicativo de web toohello padrão.        |


![criar um registro CNAME](./media/dns-custom-domain/createcnamerecord.png)

Navegue toohello voltar do serviço de aplicativo que está configurado para o nome de domínio personalizado de saudação. Clique em **Domínios personalizados**, em seguida, clique em **Nomes de host**. registro CNAME Olá tooadd que você criou, clique em **+ Adicionar nome de host**.

![figura 1](./media/dns-custom-domain/figure1.png)

Após a conclusão do processo hello, execute **nslookup** toovalidate a resolução de nomes está funcionando.

![figura 1](./media/dns-custom-domain/finalnslookup.png)

toolearn mais sobre como mapear um domínio personalizado de tooApp serviço, visite [mapear um tooAzure de nome DNS de personalizada existente aplicativos Web](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json).

Se você precisar toopurchase um domínio personalizado, visite [comprar um nome de domínio personalizado para aplicativos Web do Azure](../app-service-web/custom-dns-web-site-buydomains-web-app.md) toolearn mais informações sobre domínios de serviço de aplicativo.

## <a name="blob-storage"></a>Armazenamento de blob

Olá seguinte levá-lo a configurar um registro CNAME para uma conta de armazenamento de blob usando o método de asverify hello. Esse método garante que não haja tempo de inatividade.

Navegue muito**armazenamento** > **contas de armazenamento**, selecione sua conta de armazenamento e clique em **domínio personalizado**. Notificar Olá FQDN na etapa 2, esse valor é usado registro CNAME toocreate Olá primeiro

![domínio personalizado de armazenamento de blobs](./media/dns-custom-domain/blobcustomdomain.png)

Navegue tooyour zona de DNS e clique em **+ registrar conjunto**. Preencha Olá seguintes informações sobre Olá **Adicionar conjunto de registros** folha e clique em **Okey** toocreate-lo.


|Propriedade  |Valor  |Descrição  |
|---------|---------|---------|
|Nome     | asverify.mystorageaccount        | Esse valor junto com o rótulo de nome de domínio Olá é hello FQDN para o nome de domínio personalizado de saudação.        |
|Tipo     | CNAME        | Use um registro CNAME que esteja usando um alias.        |
|TTL     | 1        | 1 é usado por 1 hora        |
|Unidade de TTL     | Horas        | Horas são usadas como medida de tempo de saudação         |
|Alias     | asverify.adatumfunctiona9ed.blob.core.windows.net        | nome DNS de saudação você está criando o alias hello, neste exemplo é Olá asverify.adatumfunctiona9ed.blob.core.windows.net DNS nome fornecido pela conta de armazenamento toohello padrão.        |

Navegue de conta de armazenamento back tooyour clicando **armazenamento** > **contas de armazenamento**, selecione sua conta de armazenamento e clique em **domínio personalizado**. Tipo no hello alias é criado sem prefixo de asverify Olá na caixa de texto de saudação, seleção * * Use validação indireta de CNAME e, em seguida, clique em **salvar**. Depois que essa etapa for concluída, retorne tooyour zona DNS e crie um registro CNAME sem prefixo de asverify hello.  Depois disso, você está registro CNAME Olá toodelete seguro com o prefixo do hello cdnverify.

![domínio personalizado de armazenamento de blobs](./media/dns-custom-domain/indirectvalidate.png)

Valide a resolução de DNS, executando `nslookup`

toolearn mais sobre o mapeamento de um ponto de extremidade de armazenamento de blob de tooa de domínio personalizado, visite [configurar um nome de domínio personalizado para seu ponto de extremidade de armazenamento de Blob](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)

## <a name="azure-cdn"></a>CDN do Azure

Olá seguinte levá-lo a configurar um registro CNAME para um ponto de extremidade CDN usando o método de cdnverify hello. Esse método garante que não haja tempo de inatividade.

Navegue muito**rede** > **CDN perfis**, selecione o seu perfil CDN e clique em **pontos de extremidade** em **geral**.

Selecionar ponto de extremidade Olá você está trabalhando e clique em **+ domínio personalizado**. Saudação de Observação **nome de host do ponto de extremidade** como esse valor é o registro de saudação esse registro CNAME Olá aponta para.

![Domínio personalizado CDN](./media/dns-custom-domain/endpointcustomdomain.png)

Navegue tooyour zona de DNS e clique em **+ registrar conjunto**. Preencha Olá seguintes informações sobre Olá **Adicionar conjunto de registros** folha e clique em **Okey** toocreate-lo.

|Propriedade  |Valor  |Descrição  |
|---------|---------|---------|
|Nome     | cdnverify.mycdnendpoint        | Esse valor junto com o rótulo de nome de domínio Olá é hello FQDN para o nome de domínio personalizado de saudação.        |
|Tipo     | CNAME        | Use um registro CNAME que esteja usando um alias.        |
|TTL     | 1        | 1 é usado por 1 hora        |
|Unidade de TTL     | Horas        | Horas são usadas como medida de tempo de saudação         |
|Alias     | cdnverify.adatumcdnendpoint.azureedge.net        | nome DNS de saudação você está criando o alias hello, neste exemplo é Olá cdnverify.adatumcdnendpoint.azureedge.net DNS nome fornecido pela conta de armazenamento toohello padrão.        |

Navegue de ponto de extremidade CDN tooyour back clicando **rede** > **CDN perfis**e selecione o seu perfil CDN. Clique em **+ domínio personalizado** e insira o alias de registro CNAME sem prefixo de cdnverify hello e clique em **adicionar**.

Após essa etapa for concluída, retorne tooyour zona DNS e crie um registro CNAME sem prefixo do hello cdnverify.  Depois disso, você está registro CNAME Olá toodelete seguro com o prefixo do hello cdnverify. Para obter mais informações sobre a CDN e como tooconfigure um domínio personalizado sem a etapa de registro intermediário Olá visite [domínio personalizado do mapa do Azure CDN tooa conteúdo](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json).

## <a name="next-steps"></a>Próximas etapas

Saiba como muito[configurar DNS reverso para serviços hospedados no Azure](dns-reverse-dns-for-azure-services.md).
