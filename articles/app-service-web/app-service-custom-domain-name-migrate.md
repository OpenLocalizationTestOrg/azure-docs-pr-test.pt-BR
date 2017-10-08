---
title: "aaaMigrate um DNS active nome tooAzure do serviço de aplicativo | Microsoft Docs"
description: "Saiba como toomigrate um nome de domínio DNS personalizado que já está atribuído a tooa live tooAzure do serviço de aplicativo do site sem qualquer tempo de inatividade."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a>Migrar um ativo tooAzure de nome DNS do serviço de aplicativo

Este artigo mostra como toomigrate um DNS active nome muito[do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) sem qualquer tempo de inatividade.

Quando você migra um site em tempo real e seu tooApp de nome de domínio DNS serviço, o nome DNS já está servindo tráfego ao vivo. Você pode evitar o tempo de inatividade na resolução DNS durante a migração de saudação associando preventivamente Olá active DNS nome tooyour aplicativo de serviço de aplicativo.

Se você não estiver preocupado com tempo de inatividade na resolução de DNS, consulte [mapear um tooAzure de nome DNS de personalizada existente aplicativos Web](app-service-web-tutorial-custom-domain.md).

## <a name="prerequisites"></a>Pré-requisitos

toocomplete nesse instruções:

- [Verifique se o aplicativo Serviço de Aplicativo não está na camada GRATUITA](app-service-web-tutorial-custom-domain.md#checkpricing).

## <a name="bind-hello-domain-name-preemptively"></a>Associar o nome de domínio Olá preventivamente

Quando você associa um domínio personalizado preventivamente, realiza as seguinte Olá antes de fazer alterações nos registros DNS:

- Verificar a propriedade de domínio
- Habilitar o nome de domínio de saudação para seu aplicativo

Quando você migra, por fim, seu nome DNS personalizado Olá antigo toohello de site do aplicativo de serviço de aplicativo, haverá sem tempo de inatividade na resolução de DNS.

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a>Criar registro de verificação de domínio

propriedade do domínio tooverify, adicionar um TXT registrar. Olá registro TXT mapas de _awverify.&lt; subdomínio >_ too_&lt;appname >. azurewebsites.net_. 

Olá registro TXT é necessário depende Olá deseja toomigrate de registro DNS. Para obter exemplos, consulte Olá a tabela a seguir (`@` normalmente representa Olá domínio raiz):  

| Exemplo de registro DNS | Host TXT | Valor TXT |
| - | - | - |
| @ (raiz) | _awverify_ | _&lt;appname>.azurewebsites.net_ |
| www (sub) | _awverify.www_ | _&lt;appname>.azurewebsites.net_ |
| \* (curinga) | _awverify.\*_ | _&lt;appname>.azurewebsites.net_ |

Em sua página de registros DNS, observe o tipo de registro de saudação do hello nome DNS que você deseja toomigrate. O Serviço de Aplicativo dá suporte a mapeamentos de CNAME e registros A.

### <a name="enable-hello-domain-for-your-app"></a>Habilitar Olá domínio para seu aplicativo

Em Olá [portal do Azure](https://portal.azure.com), no hello navegação à esquerda da página de aplicativo hello, selecione **domínios personalizados**. 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Em Olá **domínios personalizados** página, selecione Olá  **+**  ícone Avançar muito**Adicionar nome de host**.

![Adicionar nome do host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Nome de domínio totalmente qualificado do tipo hello que você adicionou o registro TXT de saudação, como `www.contoso.com`. Para um domínio de curinga (como \*. contoso.com), você pode usar qualquer nome DNS que coincide com o domínio de curinga hello. 

Selecione **Validar**.

Olá **Adicionar nome de host** botão está ativado. 

Verifique se **tipo de registro de nome de host** é definir o tipo de registro de DNS do toohello deseja toomigrate.

Selecione **Adicionar nome do host**.

![Adicionar aplicativo de toohello de nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Pode levar algum tempo para Olá novo nome de host toobe refletida no aplicativo hello **domínios personalizados** página. Tente atualizar os dados de saudação do hello navegador tooupdate.

![Registro CNAME adicionado](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Agora, o nome DNS personalizado está habilitado no Azure App. 

## <a name="remap-hello-active-dns-name"></a>Remapear o nome do DNS do active Olá

Olá somente coisa toodo esquerdo é remapeamento seu ativo tooApp de toopoint de registro de DNS serviço. Direita agora, ele ainda aponta site antigo tooyour.

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a>Copie o endereço IP de saudação do aplicativo (somente um registro)

Se estiver fazendo o remapeamento de um registro CNAME, ignore esta seção. 

tooremap um um registro, é necessário que o endereço IP externo do aplicativo de serviço de aplicativo hello que é mostrado na Olá **domínios personalizados** página.

Olá fechar **Adicionar nome de host** página selecionando **X** no canto superior direito de saudação. 

Em Olá **domínios personalizados** página, copie o endereço IP de saudação do aplicativo.

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a>Atualizar o registro DNS Olá

Em página de registros DNS de saudação do seu provedor de domínio, selecione tooremap de registro de DNS hello.

Para Olá `contoso.com` raiz de domínio exemplo, remapear o registro A ou CNAME hello como exemplos Olá Olá a tabela a seguir: 

| Exemplo de FQDN | Tipo de registro | Host | Valor |
| - | - | - | - |
| contoso.com (raiz) | Uma | `@` | Endereço IP do [endereço IP do aplicativo da saudação de cópia](#info) |
| www.contoso.com (sub) | CNAME | `www` | _&lt;appname>.azurewebsites.net_ |
| \*.contoso.com (curinga) | CNAME | _\*_ | _&lt;appname>.azurewebsites.net_ |

Salve suas configurações.

Consultas DNS devem iniciar a resolução tooyour aplicativo de serviço de aplicativo imediatamente após a propagação DNS ocorre.

## <a name="next-steps"></a>Próximas etapas

Saiba como toobind um SSL personalizado tooApp serviço de certificado.

> [!div class="nextstepaction"]
> [Associar um tooAzure de certificado SSL de personalizada existente aplicativos Web](app-service-web-tutorial-custom-ssl.md)
