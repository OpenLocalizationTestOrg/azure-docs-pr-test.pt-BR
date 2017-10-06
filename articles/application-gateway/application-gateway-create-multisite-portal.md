---
title: "aaaHost vários sites com o Gateway de aplicativo do Azure | Microsoft Docs"
description: "Esta página fornece instruções tooconfigure um gateway existente do aplicativo do Azure para hospedar vários aplicativos web em Olá mesmo gateway com hello portal do Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a>Configurar um gateway de aplicativo existente para hospedar vários aplicativos Web

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-create-multisite-portal.md)
> * [PowerShell do Azure Resource Manager](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

Várias opções de hospedagem de site permite que você toodeploy mais de um aplicativo web em Olá mesmo gateway de aplicativo. Ele depende da presença do cabeçalho de host na solicitação HTTP entrada hello, toodetermine o ouvinte deve receber tráfego. ouvinte de Hello, em seguida, direciona o pool de back-end do tráfego tooappropriate conforme configurado na definição de regras de saudação do gateway de saudação. Em aplicativos da web SSL habilitado, o gateway de aplicativo depende Olá indicação de nome de servidor (SNI) extensão toochoose Olá correto ouvinte para o tráfego da web hello. Um uso comum para várias opções de hospedagem de site é equilibrar solicitações de tooload para pools de servidor back-end da web diferentes domínios toodifferent. Da mesma forma diversos subdomínios de saudação mesmo domínio raiz também pode ser hospedado em Olá mesmo gateway de aplicativo.

## <a name="scenario"></a>Cenário

Em Olá exemplo a seguir, o gateway de aplicativo está servindo tráfego para contoso.com e fabrikam.com com dois grupos de servidor back-end: contoso pool de servidores e pool de servidores da fabrikam. Configuração semelhante pode ser usado toohost subdomínios como app.contoso.com e blog.contoso.com.

![cenário multissite][multisite]

## <a name="before-you-begin"></a>Antes de começar

Esse cenário adiciona o gateway de aplicativo existente do suporte de vários locais tooan. toocomplete neste cenário, um gateway existente do aplicativo precisa tooconfigure disponível toobe. Visite [criar um gateway de aplicativo usando o portal de saudação](application-gateway-create-gateway-portal.md) toolearn como toocreate um application gateway básico no portal de saudação.

Olá seguem etapas Olá necessário gateway de aplicativo hello tooupdate:

1. Crie pools de back-end toouse para cada site.
2. Crie um ouvinte para cada site a que o gateway de aplicativo dará suporte.
3. Crie regras toomap cada ouvinte com hello apropriado back-end.

## <a name="requirements"></a>Requisitos

* **Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação. endereços IP Hello listado ou devem pertencer a sub-rede da rede virtual toohello ou devem ser um IP público/VIP. O FQDN também pode ser usado.
* **Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie. Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.
* **Porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello. Tráfego atinge essa porta e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação.
* **Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, esses valores diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento). Para Application Gateways habilitados para vários sites, os indicadores de SNI e nome do host também são adicionados.
* **Regra:** regra Olá associa ouvinte hello, pool de servidores de back-end hello e define o tráfego de saudação do pool de servidor back-end deve ser direcionado toowhen que ele atinja um ouvinte específico. As regras são processadas na ordem Olá que estão listados e o tráfego será direcionado por meio de saudação primeira regra correspondente, independentemente de especificidade. Por exemplo, se você tiver uma regra usando um ouvinte básico e uma regra usando um ouvinte de multissite ambos em Olá mesma regra de porta, Olá com ouvinte de multissite Olá deverá ser listada antes regra Olá com o ouvinte de saudação básica em ordem para Olá multissite regra toofunction como esperado. 
* **Certificados:** cada ouvinte exige um certificado exclusivo; neste exemplo, dois ouvintes são criados para multissite. Dois certificados. pfx e senhas Olá para que eles precisam toobe criado.

## <a name="create-back-end-pools-for-each-site"></a>Criar pools de back-end para cada site

É necessário um pool de back-end para cada site ao qual esse gateway de aplicativo dá suporte. Neste caso, serão criados dois: um para contoso11.com e outro para fabrikam11.com.

### <a name="step-1"></a>Etapa 1

Navegue tooan existente application gateway em hello (https://portal.azure.com) do portal do Azure. Selecione **Pools de back-end** e clique em **Adicionar**

![adicionar pools do back-end][7]

### <a name="step-2"></a>Etapa 2

Preencha as informações de saudação para pool de back-end Olá **pool1**, adição de endereços ip de saudação ou FQDNs para servidores de back-end hello e clique em **Okey**

![configurações do pool de back-end pool1][8]

### <a name="step-3"></a>Etapa 3

Na folha de pools de back-end Olá clique **adicionar** tooadd um pool de back-end adicional **pool2**, adição de endereços ip de saudação ou FQDNS para servidores de back-end hello e clique em **Okey**

![configurações do pool de back-end pool2][9]

## <a name="create-listeners-for-each-back-end"></a>Criar ouvintes para cada back-end

Application Gateway depende do HTTP 1.1 Olá de toohost de cabeçalhos de host com mais de um site da Web no mesmo endereço IP público e a porta. ouvinte de básica Olá criada no portal de saudação não contém essa propriedade.

### <a name="step-1"></a>Etapa 1

Clique em **ouvintes** Olá gateway de aplicativo existente e clique em **multissite** primeiro ouvinte de saudação tooadd.

![folha de visão geral de ouvintes][1]

### <a name="step-2"></a>Etapa 2

Preencha as informações de saudação para ouvinte hello. Neste exemplo, a terminação SSL está configurada; crie uma nova porta de front-end. Carregar toobe de certificado. pfx Olá usado para a terminação SSL. a única diferença Olá nesta folha de ouvinte básica padrão toohello folha em comparação comparada é o nome do host hello.

![folha de propriedades do ouvinte][2]

### <a name="step-3"></a>Etapa 3

Clique em **multissite** e criar outro ouvinte conforme descrito na etapa anterior de saudação para site segundo hello. Verifique toouse-se de que um certificado diferente para o ouvinte segundo hello. a única diferença Olá nesta folha de ouvinte básica padrão toohello folha em comparação comparada é o nome do host hello. Preencha as informações de ouvinte Olá Olá e clique em **Okey**.

![folha de propriedades do ouvinte][3]

> [!NOTE]
> A criação de ouvintes no hello portal do Azure para o application gateway é uma tarefa demorada, pode levar alguns Olá toocreate de tempo dois ouvintes nesse cenário. Quando ouvintes Olá completa exibido no portal de saudação visto Olá a imagem a seguir:

![visão geral do ouvinte][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a>Criar regras de pools de toobackend toomap ouvintes

### <a name="step-1"></a>Etapa 1

Navegue tooan existente application gateway em hello (https://portal.azure.com) do portal do Azure. Selecione **regras** e escolha a regra padrão existente de saudação **rule1** e clique em **editar**.

### <a name="step-2"></a>Etapa 2

Preencha a folha de regras de saudação visto Olá a imagem a seguir. Escolhendo o primeiro ouvinte de saudação e primeiro pool e clicando em **salvar** quando concluir.

![editar regra existente][6]

### <a name="step-3"></a>Etapa 3

Clique em **regra básica** segunda regra do toocreate hello. Preencha o formulário de saudação com hello segundo ouvinte e o segundo pool back-end e clique em **Okey** toosave.

![adicionar folha de regra básica][10]

Este cenário conclui Configurando um gateway existente do aplicativo com suporte a vários site por meio de saudação portal do Azure.

## <a name="next-steps"></a>Próximas etapas

Saiba como tooprotect seus sites com [Application Gateway - Firewall do aplicativo Web](application-gateway-webapplicationfirewall-overview.md)

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
