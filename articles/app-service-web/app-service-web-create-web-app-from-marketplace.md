---
title: aaaCreate um aplicativo web do hello Azure Marketplace | Microsoft Docs
description: "Saiba como toocreate um novo aplicativo web WordPress do hello Azure Marketplace usando Olá Portal do Azure."
services: app-service\web
documentationcenter: 
author: sunbuild
manager: erikre
editor: 
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sunbuild
ms.custom: mvc
ms.openlocfilehash: 5ad1ca2f3f7831d857c3e9b02738b6b34acf3649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-from-hello-azure-marketplace"></a>Criar um aplicativo web do hello Azure Marketplace
<!-- Note: This article replaces web-sites-php-web-site-gallery.md -->

[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Olá Marketplace do Azure fornece uma ampla gama de aplicativos web populares desenvolvido pela comunidades de software de código-fonte aberto, por exemplo, WordPress e Umbraco CMS. Neste tutorial, você aprenderá como toocreate WordPress aplicativo do Azure marketplace.
que cria um Aplicativo Web do Azure e um banco de dados MySQL. 

![Exemplo de painel de aplicativo Web WordPress](./media/app-service-web-create-web-app-from-marketplace/wpdashboard2.png)

## <a name="before-you-begin"></a>Antes de começar 

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

## <a name="deploy-from-azure-marketplace"></a>Implantar do Azure Marketplace
Siga as próximas etapas, Olá toodeploy WordPress do Azure Marketplace.

### <a name="sign-in-tooazure"></a>Entrar tooAzure
Faça logon no toohello [portal do Azure](https://portal.azure.com).

### <a name="deploy-wordpress-template"></a>Implantar modelo do WordPress
Hello Azure Marketplace fornece modelos para configurar recursos, Olá instalação [WordPress](https://portal.azure.com/#create/WordPress.WordPress) tooget modelo iniciado.
   
Digite o seguinte Olá informações toodeploy Olá WordPress aplicativo e seus recursos.

  ![Criar fluxo do WordPress](./media/app-service-web-create-web-app-from-marketplace/wordpress-portal-create.png)


| Campo         | Valor sugerido           | Descrição  |
| ------------- |-------------------------|-------------|
| Nome do aplicativo      | mywordpressapp          | Insira um nome de aplicativo exclusivo em **Nome do aplicativo Web**. Esse nome é usado como parte do nome DNS saudação padrão para seu aplicativo `<app_name>.azurewebsites.net`, portanto, ele precisa toobe exclusivo entre todos os aplicativos no Azure. Mais tarde pode mapear um aplicativo de tooyour de nome de domínio personalizado antes que você expuser tooyour usuários |
| Assinatura  | Pré-paga             | Selecione uma **Assinatura**. Se você tiver várias assinaturas, escolha a assinatura apropriada hello. |
| Grupo de recursos| mywordpressappgroup                 |    Insira um **grupo de recursos**. Um grupo de recursos é um contêiner lógico no qual recursos do Azure, como aplicativos Web e bancos de dados, são implantados e gerenciados. Você pode criar um novo grupo de recursos ou usar um grupo existente |
| Plano do Serviço de Aplicativo | myappplan          | Planos de serviço de aplicativo representam a coleção de saudação de recursos físicos usados toohost seus aplicativos. Selecione Olá **local** e hello **preço**. Para obter mais informações sobre preços, consulte [Tipo de preço do Serviço de Aplicativo](https://azure.microsoft.com/pricing/details/app-service/) |
| Banco de dados      | mywordpressapp          | Selecione o provedor de banco de dados apropriado de saudação para MySQL. Os Aplicativos Web dão suporte a **ClearDB**, **Banco de Dados do Azure para MySQL** e **MySQL no aplicativo**. Para obter mais detalhes, consulte a seção [Configuração do banco de dados](#database-config). |
| Application Insights | ATIVAR ou DESATIVAR          | Isso é opcional. O [Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) fornece serviços de monitoramento para seu aplicativo Web clicando em **ATIVAR**.|

<a name="database-config"></a>

### <a name="database-configuration"></a>Configuração do banco de dados
Siga as etapas de saudação abaixo com base em sua opção de provedor de banco de dados MySQL.  É recomendável que banco de dados do aplicativo Web e o MySQL ser Olá mesmo local.

#### <a name="cleardb"></a>ClearDB 
O [ClearDB](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview) é uma solução de terceiros para um serviço MySQL totalmente integrado no Azure. Em ordem toouse ClearDB bancos de dados, você precisará tooassociate tooyour um cartão de crédito [conta do Azure](http://account.windowsazure.com/subscriptions). Se você selecionou o provedor de banco de dados ClearDB, você pode exibir uma lista de toochoose de bancos de dados existente do ou clique em **criar novo** botão toocreate um banco de dados.

![Criar ClearDB](./media/app-service-web-create-web-app-from-marketplace/mysqldbcreate.png)

#### <a name="azure-database-for-mysql-preview"></a>Banco de Dados do Azure para MySQL (versão prévia)
[Banco de dados do Azure para MySQL](https://azure.microsoft.com/en-us/services/mysql) fornece um serviço de banco de dados gerenciados para o desenvolvimento de aplicativos e implantação que permite que você toostand um banco de dados MySQL em minutos e escala de saudação surgir na nuvem hello mais confiáveis. Com inclusivos modelos de preços, você obtém todos os recursos de saudação desejado como alta disponibilidade, segurança e recuperação – interna, sem nenhum custo extra. Clique em **preço** toochoose outro [preço](https://azure.microsoft.com/pricing/details/mysql). toouse existentes do banco de dados ou existente do MySQL server, use um grupo de recursos existente no qual Olá servidor reside. 

![Definir as configurações de banco de dados de saudação do aplicativo web de saudação](./media/app-service-web-create-web-app-from-marketplace/wordpress-azure-database.PNG)

> [!NOTE]
>  O Banco de Dados do Azure para MySQL (versão prévia) e Aplicativo Web no Linux (versão prévia) não estão disponíveis em todas as regiões. toolearn mais sobre [banco de dados do Azure para MySQL (visualização)](https://docs.microsoft.com/en-us/azure/mysql) e [Web App no Linux](./app-service-linux-intro.md) limitações. 

#### <a name="mysql-in-app"></a>MySQL no aplicativo
[MySQL no aplicativo](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app) é um recurso do serviço de aplicativo que permite executar MySql nativamente na plataforma de saudação. funcionalidade de núcleo Olá compatível com a versão de saudação do recurso de saudação:

- Servidor MySQL em execução no hello mesmo instância lado a lado com o seu servidor web que hospeda o site de saudação. Isso aumenta o desempenho do seu aplicativo.
- O armazenamento é compartilhado entre o MySQL e os arquivos do aplicativo Web. Observação com planos gratuito e compartilhado, você pode atingir os limites de cota quando usando Olá site baseado em ações de saudação que você executar. Veja as [limitações de cota](https://azure.microsoft.com/en-us/pricing/details/app-service/plans/) para os planos Gratuito e Compartilhado.
- Você pode ativar o Log de consultas lentas e o log geral para MySQL. Observe que isso pode afetar o desempenho do site hello e deve não estar sempre ativado. o recurso de log Olá ajuda a investigar problemas de aplicativo. 

Para obter mais detalhes, consulte este [artigo](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/announcing-mysql-in-app-preview-for-web-apps/ )

![Gerenciamento do MySQL no aplicativo](./media/app-service-web-create-web-app-from-marketplace/mysqlinappmanage.PNG)

Você pode assistir progresso Olá Olá ícone de sino na parte superior de saudação da página do portal Olá durante a saudação WordPress aplicativo está sendo implantado.    
![Indicador de progresso](./media/app-service-web-create-web-app-from-marketplace/deploy-success.png)

## <a name="manage-your-new-azure-web-app"></a>Gerenciar seu novo aplicativo Web do Azure

Vá toohello tootake portal do Azure examinar Olá web aplicativo recém-criado.

toodo isso, entrar muito[https://portal.azure.com](https://portal.azure.com).

No menu à esquerda do hello, clique em **serviços de aplicativos**, clique em nome de saudação do seu aplicativo web do Azure.

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-list.png)


Você foi para a _folha_ de seu aplicativo Web (uma página do portal que abre horizontalmente).

Por padrão, a folha do seu aplicativo web mostra Olá **visão geral** página. Esta página fornece uma visão de como está seu aplicativo. Aqui, você também pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir. guias de Olá no lado esquerdo de saudação da folha de saudação mostra páginas de configuração diferentes de hello, você pode abrir.

![Folha Serviço de Aplicativo no portal do Azure](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-detail.png)

Essas guias na folha de saudação mostram Olá vários recursos excelentes, você pode adicionar o aplicativo da web de tooyour. Olá lista a seguir fornece apenas algumas possibilidades de saudação:

* mapear um nome DNS personalizado
* associar um certificado SSL personalizado
* configurar uma implantação contínua
* Escalar vertical e horizontalmente
* adicionar a autenticação do usuário

Conclua Olá 5 minutos WordPress Assistente toohave WordPress aplicativo de instalação em funcionamento. Check-out [Wordpress documentação](https://codex.WordPress.org/) toodevelop seu aplicativo web.

![Assistente de instalação do WordPress](./media/app-service-web-create-web-app-from-marketplace/wplanguage.png)

## <a name="configuring-your-app"></a>Configurando seu aplicativo 
Existem várias etapas envolvidas no gerenciamento de seu aplicativo do WordPress antes que ele esteja pronto para uso em produção. Siga essas etapas tooconfigure e gerencie o aplicativo de WordPress:

| toodo isso... | Use isto... |
| --- | --- |
| **Carregar ou armazenar arquivos grandes** |[Plug-in do WordPress para usar o Armazenamento de Blobs](https://wordpress.org/plugins/windows-azure-storage/)|
| **Enviar email** |Compra [SendGrid](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SendGrid.SendGrid?tab=Overview) serviço de email e usar o hello [plug-in de WordPress para usar o SendGrid](https://wordpress.org/plugins/sendgrid-email-delivery-simplified/) tooconfigure-lo|
| **Nomes de domínio personalizados** |[Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure](app-service-web-tutorial-custom-domain.md) |
| **HTTPS** |[Habilitar HTTPS para um aplicativo Web no Serviço de Aplicativo do Azure](app-service-web-tutorial-custom-ssl.md) |
| **Validação de pré-produção** |[Configurar ambientes de preparo e desenvolvimento para aplicativos Web no Serviço de Aplicativo do Azure](web-sites-staged-publishing.md)|
| **Monitoramento e solução de problemas** |[Habilitar o log de diagnóstico para aplicativos Web no Serviço de Aplicativo do Azure](web-sites-enable-diagnostic-log.md) e [Monitorar aplicativos Web no Serviço de Aplicativo do Azure](app-service-web-tutorial-monitoring.md) |
| **Implantar o site** |[Implantar um aplicativo Web no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md) |


## <a name="secure-your-app"></a>Proteja seu aplicativo 
Existem várias etapas envolvidas no gerenciamento de seu aplicativo do WordPress antes que ele esteja pronto para uso em produção. Siga essas etapas tooconfigure e gerencie o aplicativo de WordPress:

| toodo isso... | Use isto... |
| --- | --- |
| **Nome de usuário e senha forte**|  Altere a senha com frequência. Não use nomes de usuário comuns, como *admin* ou *wordpress* etc. Força todos os WordPress usuários toouse exclusivo nome de usuário e senhas fortes. |
| **Mantenha-se atualizado** | Mantenha seus principais do WordPress, temas, plug-ins backup toodate. Use Olá último tempo de execução PHP disponível no serviço de aplicativo do Azure |
| **Atualizar as chaves de segurança do WordPress** | Atualização [chave de segurança do WordPress](https://codex.wordpress.org/Editing_wp-config.php#Security_Keys) tooimprove criptografia armazenada em cookies|

## <a name="improve-performance"></a>Melhorar o desempenho
O desempenho na nuvem Olá é obtido principalmente por meio de cache e expansão. No entanto, Olá memória, largura de banda e outros atributos da hospedagem de aplicativos da Web devem ser considerados.

| toodo isso... | Use isto... |
| --- | --- |
| **Compreender recursos de instância do Site** |[Detalhes do preço, incluindo recursos de camadas do Serviço de Aplicativo](https://azure.microsoft.com/en-us/pricing/details/app-service/)|
| **Recursos do cache** |Use [cache Redis do Azure](https://azure.microsoft.com/en-us/services/cache/), ou uma de Olá outras ofertas de cache em Olá [armazenamento do Azure](https://azuremarketplace.microsoft.com) |
| **Dimensionar o aplicativo** |Você precisa tooscale [Olá web app no serviço de aplicativo do Azure](web-sites-scale.md) e/ou banco de dados MySQL. O MySQL no aplicativo não tem suporte para expansão, sendo assim, escolha o ClearDB ou o Banco de Dados do Azure para MySQL (versão prévia). [Dimensionar o banco de dados do Azure (visualização) do MySQL](https://azure.microsoft.com/en-us/pricing/details/mysql/) ou se usar [ClearDB alta disponibilidade roteamento](http://w2.cleardb.net/faqs/) tooscale banco de dados do |

## <a name="availability-and-disaster-recovery"></a>Disponibilidade e recuperação de desastre
Alta disponibilidade inclui o aspecto de saudação de continuidade de negócios de toomaintain de recuperação de desastres. Planejamento para falhas e desastres na nuvem Olá requer falhas de saudação toorecognize rapidamente. Essas soluções ajudam a implementar uma estratégia de alta disponibilidade.

| toodo isso... | Use isto... |
| --- | --- |
| **Sites de balanceamento de carga** ou **sites distribuídos geograficamente** |[Encaminhar tráfego com o Gerenciador de Tráfego do Azure](https://azure.microsoft.com/en-us/services/traffic-manager/) |
| **Backup e restauração** |[Fazer backup de um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-backup.md) e [Restaurar um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-restore.md) |

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre os vários recursos do [toodevelop do serviço de aplicativo e a escala](/app-service-web/).
