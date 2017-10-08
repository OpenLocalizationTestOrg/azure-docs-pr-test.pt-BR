---
title: aaaMap um DNS personalizado existente nome tooAzure Web Apps | Microsoft Docs
description: "Saiba como tooadd um domínio DNS personalizado existente nome de aplicativo de web (domínio banido) tooa, back-end do aplicativo móvel ou aplicativo de API no serviço de aplicativo do Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a>Mapear um tooAzure de nome DNS de personalizada existente aplicativos Web

Os [aplicativos Web do Azure](app-service-web-overview.md) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches. Este tutorial mostra como toomap um DNS personalizado existente nome tooAzure os aplicativos Web.

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Mapear um subdomínio (por exemplo, `www.contoso.com`) usando um registro CNAME
> * Mapear um domínio raiz (por exemplo, `contoso.com`) usando um registro A
> * Mapear um domínio curinga (por exemplo, `*.contoso.com`) usando um registro CNAME
> * Automatizar o mapeamento de domínio com scripts

Você pode usar um **registro CNAME** ou um **um registro** tooApp serviço de nome de toomap um DNS personalizado. 

> [!NOTE]
> É recomendável que você use um CNAME para todos os nomes DNS personalizados, exceto um domínio raiz (por exemplo, `contoso.com`).

toomigrate um site em tempo real e seu tooApp de nome de domínio DNS serviço, consulte [migrar um ativo tooAzure de nome DNS do serviço de aplicativo](app-service-custom-domain-name-migrate.md).

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este tutorial:

* [Crie um aplicativo do Serviço de Aplicativo](/azure/app-service/) ou use um aplicativo que você criou para outro tutorial.
* Comprar um nome de domínio e verifique se você acessar toohello o registro DNS para o seu provedor de domínio (como GoDaddy).

  Por exemplo, as entradas DNS tooadd para `contoso.com` e `www.contoso.com`, você deve ser capaz de tooconfigure Olá configurações de DNS Olá `contoso.com` domínio raiz.

  > [!NOTE]
  > Se você não tiver um domínio existente de nome, considere [comprar um domínio usando Olá portal do Azure](custom-dns-web-site-buydomains-web-app.md). 

## <a name="prepare-hello-app"></a>Preparar o aplicativo hello

toomap um personalizado DNS nome tooa do aplicativo web, aplicativo web de saudação [plano de serviço de aplicativo](https://azure.microsoft.com/pricing/details/app-service/) deve ser uma camada paga (**compartilhado**, **básica**, **padrão**, ou  **Premium**). Nesta etapa, você verifique se esse aplicativo está em saudação do serviço de aplicativo hello suporte para a camada de preços.

### <a name="sign-in-tooazure"></a>Entrar tooAzure

Olá abrir [portal do Azure](https://portal.azure.com) e entre com sua conta do Azure.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Navegue toohello aplicativo hello portal do Azure

No menu à esquerda do hello, selecione **serviços de aplicativos**e, em seguida, selecione o nome de saudação do aplicativo hello.

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/select-app.png)

Página de gerenciamento Olá de saudação do aplicativo de serviço de aplicativo é exibida.  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a>Saudação de verificação de preço

No hello barra de navegação de página de aplicativo hello esquerda, role toohello **configurações** seção e selecione **escalar verticalmente (plano de serviço de aplicativo)**.

![Menu Escalar verticalmente](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

camada atual do aplicativo Hello é realçada por uma borda azul. Verificar toomake se esse aplicativo hello não está em Olá **livre** camada. DNS personalizado não é suportada no hello **livre** camada. 

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Se hello plano de serviço de aplicativo não é **livre**, feche Olá **Escolher tipo de preços** página e ir muito[mapear um registro CNAME](#cname).

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a>Dimensionar o hello plano de serviço de aplicativo

Selecione qualquer uma das camadas não estão livres de saudação (**compartilhado**, **básica**, **padrão**, ou **Premium**). 

Clique em **Selecionar**.

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Quando você vir Olá notificação a seguir, a operação de escala de saudação foi concluída.

![Confirmação da operação de escala](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a>Criar um registro CNAME

Exemplo de tutorial hello, você adiciona um registro CNAME para Olá `www` subdomínio (por exemplo, `www.contoso.com`).

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Criar registro CNAME Olá

Adicionar nome do host padrão do aplicativo de toohello um subdomínio de um toomap de registro de CNAME (`<app_name>.azurewebsites.net`).

Para Olá `www.contoso.com` exemplo de domínio, adicione um registro CNAME que mapeia o nome hello `www` muito`<app_name>.azurewebsites.net`.

Depois de adicionar Olá CNAME, página de registros DNS Olá aparência Olá exemplo a seguir:

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a>Habilitar o mapeamento de registro CNAME Olá no Azure

No hello deixado navegação de página de aplicativo hello no hello portal do Azure, selecione **domínios personalizados**. 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Em Olá **domínios personalizados** página do aplicativo hello, adicione Olá totalmente qualificado nome DNS personalizado (`www.contoso.com`) toohello lista.

Selecione Olá  **+**  ícone Avançar muito**Adicionar nome de host**.

![Adicionar nome do host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Nome de domínio totalmente qualificado do tipo hello que você adicionou um registro CNAME para, como `www.contoso.com`. 

Selecione **Validar**.

Olá **Adicionar nome de host** botão está ativado. 

Verifique se **tipo de registro de nome de host** está definido muito**CNAME (www.example.com ou qualquer subdomínio)**.

Selecione **Adicionar nome do host**.

![Adicionar aplicativo de toohello de nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Pode levar algum tempo para Olá novo nome de host toobe refletida no aplicativo hello **domínios personalizados** página. Tente atualizar os dados de saudação do hello navegador tooupdate.

![Registro CNAME adicionado](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Se você perdeu uma etapa ou digitação em algum lugar anteriormente, você verá um erro de verificação final Olá Olá página.

![Erro de verificação](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a>Mapear um registro A

Exemplo de tutorial hello, você adiciona um registro a para o domínio raiz da saudação (por exemplo, `contoso.com`). 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a>Copie o endereço IP de saudação do aplicativo

toomap um um registro, é necessário o endereço IP externo de saudação do aplicativo. Você pode encontrar esse endereço IP do aplicativo hello **domínios personalizados** página Olá portal do Azure.

No hello deixado navegação de página de aplicativo hello no hello portal do Azure, selecione **domínios personalizados**. 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Em Olá **domínios personalizados** página, copie o endereço IP de saudação do aplicativo.

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a>Crie um registro a saudação

requer o serviço de aplicativo toomap um um aplicativo de registro tooan, **duas** registros de DNS:

- Um **um** registrar o endereço IP do toomap toohello aplicativo.
- Um **TXT** registre o nome do host do aplicativo do toomap toohello padrão `<app_name>.azurewebsites.net`. Serviço de aplicativo usa esse registro somente em tempo de configuração, tooverify que você possui o domínio personalizado hello. Depois que o domínio personalizado for validado e configurado no Serviço de Aplicativo, você poderá excluir esse registro TXT. 

Para Olá `contoso.com` exemplo de domínio, criar registros e TXT Olá toohello a tabela a seguir de acordo com (`@` normalmente representa Olá domínio raiz). 

| Tipo de registro | Host | Valor |
| - | - | - |
| Uma | `@` | Endereço IP do [endereço IP do aplicativo da saudação de cópia](#info) |
| TXT | `@` | `<app_name>.azurewebsites.net` |

Quando Olá registros são adicionados, Olá página de registros DNS aparência Olá exemplo a seguir:

![Página de Registros DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a>Habilitar Olá um mapeamento de registro no aplicativo hello

No aplicativo hello **domínios personalizados** página Olá portal do Azure, adicione o nome personalizado do DNS totalmente qualificado do Olá (por exemplo, `contoso.com`) toohello lista.

Selecione Olá  **+**  ícone Avançar muito**Adicionar nome de host**.

![Adicionar nome do host](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

Nome de domínio totalmente qualificado do tipo hello configuradas Olá um registro, como `contoso.com`.

Selecione **Validar**.

Olá **Adicionar nome de host** botão está ativado. 

Verifique se **tipo de registro de nome de host** está definido muito**um registro (example.com)**.

Selecione **Adicionar nome do host**.

![Adicionar aplicativo de toohello de nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

Pode levar algum tempo para Olá novo nome de host toobe refletida no aplicativo hello **domínios personalizados** página. Tente atualizar os dados de saudação do hello navegador tooupdate.

![Registro A adicionado](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

Se você perdeu uma etapa ou digitação em algum lugar anteriormente, você verá um erro de verificação final Olá Olá página.

![Erro de verificação](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a>Mapear um domínio curinga

No exemplo de tutorial hello, você mapeia uma [nome DNS de curinga](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (por exemplo, `*.contoso.com`) toohello aplicativo de serviço de aplicativo adicionando um registro CNAME. 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Criar registro CNAME Olá

Adicionar nome do host do aplicativo um curinga nome toohello padrão de um toomap de registro de CNAME (`<app_name>.azurewebsites.net`).

Para Olá `*.contoso.com` domínio exemplo hello registro CNAME mapeará nome hello `*` muito`<app_name>.azurewebsites.net`.

Quando Olá CNAME é adicionado, Olá página de registros DNS aparência Olá exemplo a seguir:

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a>Habilitar o mapeamento de registro CNAME Olá no aplicativo hello

Agora você pode adicionar qualquer subdomínio que corresponde a saudação curinga nome toohello aplicativo (por exemplo, `sub1.contoso.com` e `sub2.contoso.com` corresponder `*.contoso.com`). 

No hello deixado navegação de página de aplicativo hello no hello portal do Azure, selecione **domínios personalizados**. 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Selecione Olá  **+**  ícone Avançar muito**Adicionar nome de host**.

![Adicionar nome do host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Digite um nome de domínio totalmente qualificado que corresponda Olá curinga domínio (por exemplo, `sub1.contoso.com`) e, em seguida, selecione **validar**.

Olá **Adicionar nome de host** botão está ativado. 

Verifique se **tipo de registro de nome de host** está definido muito**registro CNAME (www.example.com ou qualquer subdomínio)**.

Selecione **Adicionar nome do host**.

![Adicionar aplicativo de toohello de nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

Pode levar algum tempo para Olá novo nome de host toobe refletida no aplicativo hello **domínios personalizados** página. Tente atualizar os dados de saudação do hello navegador tooupdate.

Selecione Olá  **+**  ícone novamente tooadd outro nome de host que corresponda Olá curinga domínio. Por exemplo, adicione `sub2.contoso.com`.

![Registro CNAME adicionado](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a>Testar no navegador

Procurar toohello nomes DNS que você configurou anteriormente (por exemplo, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, e `sub2.contoso.com`).

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a>Automatizar com scripts

Você pode automatizar o gerenciamento de domínios personalizados com scripts, usando Olá [CLI do Azure](/cli/azure/install-azure-cli) ou [Azure PowerShell](/powershell/azure/overview). 

### <a name="azure-cli"></a>CLI do Azure 

saudação de comando a seguir adiciona uma tooan de nome DNS de personalizado configurado o aplicativo de serviço de aplicativo. 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

Para obter mais informações, consulte [mapear um aplicativo web do domínio personalizado tooa](scripts/app-service-cli-configure-custom-domain.md). 

### <a name="azure-powershell"></a>Azure PowerShell 

saudação de comando a seguir adiciona uma tooan de nome DNS de personalizado configurado o aplicativo de serviço de aplicativo. 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

Para obter mais informações, consulte [atribuir um aplicativo web do domínio personalizado tooa](scripts/app-service-powershell-configure-custom-domain.md).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:

> [!div class="checklist"]
> * Mapear um subdomínio usando um registro CNAME
> * Mapear um domínio raiz usando um registro A
> * Mapear um domínio curinga usando um registro CNAME
> * Automatizar o mapeamento de domínio com scripts

Avançar toolearn tutorial do próximo toohello como toobind um SSL personalizado de certificado tooa web app.

> [!div class="nextstepaction"]
> [Associar um tooAzure de certificado SSL de personalizada existente aplicativos Web](app-service-web-tutorial-custom-ssl.md)
