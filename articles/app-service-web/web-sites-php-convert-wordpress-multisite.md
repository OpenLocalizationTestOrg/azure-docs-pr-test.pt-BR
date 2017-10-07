---
title: "aaaConvert WordPress tooMultisite no serviço de aplicativo do Azure"
description: "Saiba como tootake um aplicativo web de WordPress existente criado por meio da Galeria de saudação do Azure e convertê-la tooWordPress multissite"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 1153f0a8043de875f081704cd0a124776758878c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-wordpress-toomultisite-in-azure-app-service"></a>Converter WordPress tooMultisite no serviço de aplicativo do Azure
## <a name="overview"></a>Visão geral
*Por [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*

Neste tutorial, você aprenderá como tootake um aplicativo web de WordPress existente criado por meio da Galeria de saudação do Azure e converter em um multissite WordPress instalar. Além disso, você aprenderá como tooassign tooeach um domínio personalizado da saudação subsites dentro de sua instalação.

Presume-se que você tem uma instalação existente do WordPress. Se você não fizer isso, siga orientação Olá fornecida [criar um site de WordPress da Galeria de saudação no Azure][website-from-gallery].

Convertendo um WordPress existente tooMultisite de instalação de site único geralmente é bastante simple e muitas das etapas iniciais Olá aqui são fornecidos diretamente da saudação [criar uma rede] [ wordpress-codex-create-a-network] página Olá [WordPress código](http://codex.wordpress.org).

Vamos começar.

## <a name="allow-multisite"></a>Permitir que o multissite
É necessário primeiro tooenable multissite por meio de saudação `wp-config.php` arquivo com hello **WP\_permitir\_MULTISSITE** constante. Há dois tooedit de métodos os arquivos de aplicativo da web: Olá primeiro é por meio de saudação segundo pelo Git e FTP. Se você estiver familiarizado com o toosetup qualquer um desses métodos, consulte toohello tutoriais a seguir:

* [Site do PHP com o MySQL e FTP][website-w-mysql-and-ftp-ftp-setup]
* [Site do PHP com o MySQL e Git][website-w-mysql-and-git-git-setup]

Olá abrir `wp-config.php` arquivo com o editor de saudação de sua escolha e adicione a seguinte Olá acima Olá `/* That's all, stop editing! Happy blogging. */` linha.

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

Arquivo de saudação toosave-se de que e carregue-o servidor toohello back!

## <a name="network-setup"></a>Configuração de rede
Faça logon no toohello *wp-admin* área de seu aplicativo web e você verá um novo item sob Olá **ferramentas** menu chamado **configuração de rede**. Clique em **configuração de rede** e preencha os detalhes de saudação da sua rede.

![Tela de configuração de rede][wordpress-network-setup]

Este tutorial usa Olá *subdiretórios* site esquema porque ele sempre deve funcionar e vão configurar domínios personalizados para cada subsite posteriormente no tutorial de saudação. No entanto, ele deve ser possível toosetup um subdomínio instalar se você mapear um domínio por meio de saudação [Portal do Azure](https://portal.azure.com) e instalação curinga DNS corretamente.

Para obter mais informações sobre o subdomínio vs subpasta configurações Consulte Olá [tipos de rede multissite] [ wordpress-codex-types-of-networks] artigo Olá WordPress código.

## <a name="enable-hello-network"></a>Habilitar Olá rede
rede Olá agora está configurado no banco de dados hello, mas não há um restantes etapa tooenable Olá funcionalidade de rede. Finalizar Olá `wp-config.php` configurações e certifique-se de `web.config` corretamente roteia cada site.

Depois de clicar em Olá **instalar** botão Olá *configuração de rede* página, WordPress tentará Olá tooupdate `wp-config.php` e `web.config` arquivos. No entanto, você sempre deve verificar Olá arquivos tooensure Olá atualizações foram bem-sucedidas. Caso contrário, esta tela apresentará as atualizações necessárias hello. Editar e salvar arquivos hello.

Depois de fazer essas atualizações, você precisará toolog-out e o log novamente no painel de administração de pt hello.

Agora deve haver um menu adicional na barra de admin Olá rotulada **Meus Sites**. Esse menu permite que você toocontrol sua nova rede por meio de saudação **administrador de rede** painel.

## <a name="adding-custom-domains"></a>Adicionando domínios personalizados
Olá [mapeamento de domínio do WordPress MU] [ wordpress-plugin-wordpress-mu-domain-mapping] plug-in transforma em um site de tooany muito fácil tooadd domínios personalizados na sua rede. Para Olá plug-in toooperate corretamente, é necessário toodo alguma configuração adicional no hello Portal e também em seu registrador de domínio.

## <a name="enable-domain-mapping-toohello-web-app"></a>Habilitar o aplicativo web do domínio mapeamento toohello
Olá **livre** [do serviço de aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714) plano de modo não oferece suporte para a adição de domínios personalizados tooWeb aplicativos. Você precisará tooswitch muito**compartilhado** ou **padrão** modo. toodo isso:

* Faça logon no Portal do Azure de toohello e localize seu aplicativo web. 
* Clique em Olá **expandir** guia **configurações**.
* Em **Geral**, selecione *COMPARTILHADO* ou *STANDARD*
* Clique em **Salvar**

Você pode receber uma mensagem solicitando que você alterar de saudação tooverify e confirmar seu aplicativo web agora pode incorrer em um custo, dependendo do uso e Olá outra configuração que você definir.

Levará alguns segundos tooprocess Olá novas configurações, agora é um bom momento toostart ao configurar seu domínio.

## <a name="verify-your-domain"></a>Verifique se seu domínio
Antes de aplicativos Web do Azure permitirá que você toomap um site de toohello do domínio, você primeiro precisa tooverify se você possui Olá autorização toomap Olá domínio. toodo, portanto, você deve adicionar uma nova entrada DNS de tooyour registro CNAME.

* Faça logon no Gerenciador de DNS do domínio tooyour
* Criar um novo CNAME *awverify*
* Ponto *awverify* muito*awverify. YOUR_DOMAIN.azurewebsites.NET*

Ele pode levar algum tempo para Olá DNS alterações toogo em vigor, portanto, se Olá etapas a seguir não funciona imediatamente, fazer uma xícara de café, em seguida, volte e tente novamente.

## <a name="add-hello-domain-toohello-web-app"></a>Adicionar o aplicativo web do hello domínio toohello
Aplicativo web de retorno tooyour por meio de saudação Portal do Azure, clique em **configurações**e, em seguida, clique em **domínios personalizados e SSL**.

Olá quando *configurações de SSL* são exibidos, você verá campos Olá onde você digitará todos os domínios de saudação que você deseja que o aplicativo de web tooyour tooassign. Se um domínio não estiver listado aqui, ele não estará disponível para o mapeamento de dentro do WordPress, independentemente de como o domínio Olá DNS está configurado.

![Caixa de diálogo domínios personalizados gerenciar][wordpress-manage-domains]

Depois de digitar seu domínio na caixa de texto de saudação, o Azure verificará Olá registro CNAME que você criou anteriormente. Se Olá DNS não foi totalmente propagada, um indicador vermelho será exibido. Se tiver êxito, você verá uma marca de seleção verde. 

Anote Olá que endereço IP listado na parte inferior da saudação da caixa de diálogo de saudação. Você precisará este Olá toosetup um registro para o seu domínio.

## <a name="setup-hello-domain-a-record"></a>Configurar o registro de um domínio Olá
Se hello a outras etapas foram bem-sucedidas, agora você pode atribuir a aplicativo da web do Azure tooyour Olá domínio por meio de um registro A do DNS. 

É importante toonote aqui aplicativos web do Azure aceitam CNAME e registros, porém você *deve* usar um mapeamento de domínio adequado tooenable registro A. Um CNAME não pode ser encaminhado tooanother CNAME, que é o Azure criado para você com YOUR_DOMAIN.azurewebsites.net.

Usando o endereço IP de saudação da etapa anterior hello, retorne tooyour Gerenciador de DNS e Olá instalação um IP de toothat toopoint registro.

## <a name="install-and-setup-hello-plugin"></a>Instalar e configurar o plug-in de saudação
WordPress multissite atualmente não tem um método interno toomap os domínios personalizados. No entanto, há um plug-in chamado [mapeamento de domínio do WordPress MU] [ wordpress-plugin-wordpress-mu-domain-mapping] que adiciona funcionalidade Olá para você. Fazer login toohello parte de administrador de rede do seu site e instalar Olá **mapeamento de domínio do WordPress MU** plug-in.

Depois de instalar e ativar o plug-in hello, visite **configurações** > **domínio mapeamento** tooconfigure Olá plugin. Na primeira caixa de texto de saudação, *endereço IP do servidor*, endereço IP usado toosetup de entrada hello Olá um registro para o domínio de saudação. Defina qualquer *opções de domínio* desejados (Olá padrões geralmente são permitidos) e clique em **salvar**.

## <a name="map-hello-domain"></a>Domínio de saudação do mapa
Visite Olá **painel** para o site de saudação desejar domínio Olá toomap. Clique em **ferramentas** > **domínio mapeamento** e tipo hello novo domínio na caixa de texto de saudação e clique em **adicionar**.

Por padrão, Olá novo será reconfigurado toohello gerado automaticamente site domínio. Se você quiser toohave todo o tráfego enviado toohello novo domínio, marque Olá *domínio primário para este blog* caixa antes de salvar. Você pode adicionar um número ilimitado de site de tooa de domínios, mas apenas um pode ser primário.

## <a name="do-it-again"></a>Fazê-lo novamente
Os aplicativos Web do Azure permitem que você tooadd um número ilimitado de aplicativo de web tooa domínios. tooadd outro domínio, você precisará Olá tooexecute **verificar seu domínio** e **configurar o registro de domínio A saudação** seções para cada domínio.    

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


