---
title: classe aaaEnterprise WordPress no Azure | Microsoft Docs
description: "Saiba como toohost um corporativo WordPress site no serviço de aplicativo do Azure"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 22d68588-2511-4600-8527-c518fede8978
ms.service: app-service-web
ms.devlang: php
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 4347eddb31d622d1189dc5db4d81b0f3745d6e69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-class-wordpress-on-azure"></a>WordPress de classe empresarial no Azure
O Serviço de Aplicativo do Azure oferece um ambiente escalonável, seguro e fácil de usar para sites do [WordPress][wordpress] críticos e de grande escala. A própria Microsoft executa sites corporativos, como Olá [Office] [ officeblog] e [Bing] [ bingblog] blogs. Este artigo mostra como toouse Olá recurso de aplicativos Web do serviço de aplicativo do Microsoft Azure tooestablish e manter um corporativo, o site de WordPress baseado em nuvem que pode lidar com um grande volume de visitantes.

## <a name="architecture-and-planning"></a>Arquitetura e planejamento
Uma instalação básica do WordPress tem apenas dois requisitos:

* **Banco de dados MySQL**: esse requisito está disponível por meio de [ClearDB em hello Azure Marketplace][cdbnstore]. Como alternativa, é possível gerenciar sua própria instalação do MySQL nas Máquinas Virtuais do Azure usando o [Windows][mysqlwindows] ou o [Linux][mysqllinux].

  > [!NOTE]
  > O ClearDB fornece diversas configurações de MySQL. Cada configuração tem características de desempenho diferentes. Consulte Olá [Azure Store] [ cdbnstore] para obter informações sobre as ofertas que são fornecidos por meio de hello Azure Store ou diretamente como visto no hello [site ClearDB](http://www.cleardb.com/pricing.view).
  >
  >
* **PHP 5.2.4 ou posterior**: atualmente, o Serviço de Aplicativo do Azure fornece as [versões 5.4, 5.5 e 5.6 do PHP][phpwebsite].

  > [!NOTE]
  > É recomendável que você sempre execute Olá versão mais recente do PHP para que você tenha mais recentes correções de segurança hello.
  >
  >

### <a name="basic-deployment"></a>Implantação básica
Se você usar apenas os requisitos básicos de saudação, você pode criar uma solução básica de dentro de uma região do Azure.

![Um aplicativo Web do Azure e um Banco de Dados MySQL hospedados em uma única região do Azure][basic-diagram]

Embora isso permitiria que você criar várias instâncias de aplicativos Web do hello site tooscale seu aplicativo, tudo o que é hospedado em datacenters de saudação em uma região geográfica específica. Os visitantes desta região podem ver os tempos de resposta lentos ao usar o site de saudação. Se datacenters Olá nessa região, ficarem desativados, portanto não seu aplicativo.

### <a name="multi-region-deployment"></a>Implantação em várias regiões
Usando o Azure [Traffic Manager][trafficmanager], você pode dimensionar seu site de WordPress em várias regiões geográficas e fornecer hello a mesma URL para todos os visitantes. Todos os visitantes são fornecidos por meio do Gerenciador de tráfego e são roteadas tooa região com base no hello configuração de balanceamento de carga.

![Um aplicativo web do Azure, hospedado em várias regiões, usando CDBR alta disponibilidade roteador tooroute tooMySQL entre regiões][multi-region-diagram]

Dentro de cada região, o site de WordPress Olá ainda deve ser dimensionado em várias instâncias de aplicativos Web, mas esse escalonamento é região tooa específico. As regiões de tráfego alto podem ser dimensionadas de maneira diferente do que as de tráfego baixo.

tooreplicate e rotear tráfego toomultiple bancos de dados MySQL, você pode usar [ClearDB roteadores de alta disponibilidade (CDBRs)] [ cleardbscale] (mostrado à esquerda) ou [MySQL Cluster operadora classificação Edition (CGE)] [cge].

### <a name="multi-region-deployment-with-media-storage-and-caching"></a>Implantação em várias regiões com armazenamento e cache de mídia
Se o site Olá aceita carregamentos ou arquivos de mídia de hosts, use o armazenamento de BLOBs do Azure. Se você precisar de armazenamento em cache, considere [cache Redis][rediscache], [Memcache nuvem](http://azure.microsoft.com/gallery/store/garantiadata/memcached/), [MemCachier](http://azure.microsoft.com/gallery/store/memcachier/memcachier/), ou uma de Olá outras ofertas de cache em Olá [Repositório azure](http://azure.microsoft.com/gallery/store/).

![Um aplicativo Web do Azure, hospedado em várias regiões, usando o roteador de Alta Disponibilidade do CDBR para MySQL, com o Cache Gerenciado, Armazenamento de Blobs e Rede de Distribuição de Conteúdo][performance-diagram]

Armazenamento de blob é distribuído geograficamente entre regiões por padrão, para que você não tenha tooworry sobre a replicação de arquivos em todos os sites. Você também pode habilitar hello Azure [rede de fornecimento de conteúdo] [ cdn] para o armazenamento de Blob, que distribui nós de tooend de arquivos que são os visitantes de tooyour mais próximos.

### <a name="planning"></a>Planejamento
#### <a name="additional-requirements"></a>Requisitos adicionais
| toodo isso... | Use isto... |
| --- | --- |
| **Carregar ou armazenar arquivos grandes** |[Plug-in do WordPress para usar o Armazenamento de Blobs][storageplugin] |
| **Enviar email** |[SendGrid] [ storesendgrid] e hello [plug-in de WordPress para usar o SendGrid][sendgridplugin] |
| **Nomes de domínio personalizados** |[Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure][customdomain] |
| **HTTPS** |[Habilitar HTTPS para um aplicativo Web no Serviço de Aplicativo do Azure][httpscustomdomain] |
| **Validação de pré-produção** |[Configurar ambientes de preparo para aplicativos Web no Serviço de Aplicativo do Azure][staging] <p>Quando você move um aplicativo web de preparo tooproduction, você também mover configuração do WordPress hello. Certifique-se de que todas as configurações estão atualizados toohello requisitos para seu aplicativo de produção antes de mover tooproduction de aplicativo hello preparado.</p> |
| **Monitoramento e solução de problemas** |[Habilitar o log de diagnóstico para aplicativos Web no Serviço de Aplicativo do Azure][log] e [Monitorar aplicativos Web no Serviço de Aplicativo do Azure][monitor] |
| **Implantar o site** |[Implantar um aplicativo Web no Serviço de Aplicativo do Azure][deploy] |

#### <a name="availability-and-disaster-recovery"></a>Disponibilidade e recuperação de desastre
| toodo isso... | Use isto... |
| --- | --- |
| **Sites de balanceamento de carga** ou **sites distribuídos geograficamente** |[Encaminhar tráfego com o Gerenciador de Tráfego do Azure][trafficmanager] |
| **Backup e restauração** |[Fazer backup de um aplicativo Web no Serviço de Aplicativo do Azure][backup] e [Restaurar um aplicativo Web no Serviço de Aplicativo do Azure][restore] |

#### <a name="performance"></a>Desempenho
O desempenho na nuvem Olá é obtido principalmente por meio de cache e expansão. No entanto, Olá memória, largura de banda e outros atributos da hospedagem de aplicativos da Web devem ser considerados.

| toodo isso... | Use isto... |
| --- | --- |
| **Compreender recursos de instância do Site** |[Detalhes do preço, incluindo recursos de camadas do Serviço de Aplicativo][websitepricing] |
| **Recursos do cache** |[Cache redis][rediscache], [Memcache nuvem](/gallery/store/garantiadata/memcached/), [MemCachier](/gallery/store/memcachier/memcachier/), ou uma de Olá outras ofertas de cache em Olá [armazenamento do Azure](/gallery/store/) |
| **Dimensionar o aplicativo** |[Dimensionar um aplicativo Web no Serviço de Aplicativo do Azure][websitescale] e [Roteamento de alta disponibilidade do ClearDB][cleardbscale]. Se você escolher toohost e gerenciar sua própria instalação do MySQL, você deve considerar [MySQL Cluster CGE] [ cge] para expansão. |

#### <a name="migration"></a>Migração
Há dois toomigrate de métodos um tooAzure de site do WordPress existente do serviço de aplicativo:

* **[Exportar WordPress][export]**: esse método exporta o conteúdo de saudação do seu blog. Você pode importar Olá tooa conteúdo novo site de WordPress no serviço de aplicativo do Azure usando Olá [plug-in do WordPress importador][import].

  > [!NOTE]
  > Embora permita migrar o conteúdo, esse processo não migra qualquer plug-in, tema ou outra personalização. Instale novamente esses componentes de forma manual.
  >
  >
* **Migração manual**: [backup de seu site] [ wordpressbackup] e [banco de dados][wordpressdbbackup]e, em seguida, restaure-o manualmente tooa web aplicativo no Azure Serviço de aplicativo e banco de dados MySQL associado. Esse método é útil toomigrate altamente personalizada sites porque ela evita tédio Olá de instalar manualmente os plug-ins, temas e outras personalizações.

## <a name="step-by-step-instructions"></a>Instruções passo a passo
### <a name="create-a-wordpress-site"></a>Criar um site do WordPress
1. Saudação de uso [Azure Marketplace] [ cdbnstore] toocreate um banco de dados MySQL de tamanho de saudação identificado na Olá [planejamento e arquitetura](#planning) seção Olá região ou regiões onde você irá hospedar seu site.
2. Siga as etapas de saudação em [criar um aplicativo web do WordPress no serviço de aplicativo do Azure] [ createwordpress] toocreate um aplicativo da web de WordPress. Quando você cria um aplicativo da web de saudação, selecione **usar um banco de dados MySQL**e, em seguida, selecione o banco de dados de saudação que você criou na etapa 1.

Se você estiver migrando um site existente do WordPress, consulte [migrar um tooAzure de site existente do WordPress](#Migrate-an-existing-WordPress-site-to-Azure) depois de criar um novo aplicativo web.

### <a name="migrate-an-existing-wordpress-site-tooazure"></a>Migrar um tooAzure de site do WordPress existente
Conforme mencionado em Olá [planejamento e arquitetura](#planning) seção, há um site de WordPress em toomigrate de duas maneiras:

* **Usar exportação e importação** para sites que não tem muito personalização ou onde você quiser apenas conteúdo de saudação toomove.
* **Use backup e restauração** para sites que têm muitos de personalização onde você deseja toomove tudo.

Use uma saudação toomigrate seções a seguir seu site.

#### <a name="hello-export-and-import-method"></a>Olá exportar e importar o método
1. Use [WordPress exportar] [ export] tooexport existente do site.
2. Criar um aplicativo web usando as etapas de Olá Olá [criar um site de WordPress](#Create-a-new-WordPress-site) seção.
3. Entrar no site de WordPress tooyour Olá [portal do Azure][mgmtportal]e, em seguida, clique em **plug-ins** > **adicionar novo**. Procurar e instalar Olá **importador de WordPress** plug-in.
4. Depois de instalar o plug-in do WordPress importador de saudação, clique em **ferramentas** > **importação**e, em seguida, clique em **WordPress** toouse Olá plug-in do WordPress importador.
5. Em Olá **importação WordPress** , clique em **Escolher arquivo**. Localizar o arquivo WXR Olá que foi exportado do seu site de WordPress existente e, em seguida, clique em **importação e carregar arquivo**.
6. Clique em **Enviar**. Você será solicitado que Olá importação foi bem-sucedida.
7. Depois de concluir todas estas etapas, reinicie o site de sua **serviços de aplicativos** folha em Olá [portal do Azure][mgmtportal].

Depois de importar site hello, talvez seja necessário Olá tooperform configurações de tooenable de etapas que não estão no arquivo de importação de saudação a seguir.

| Se você estava usando isto... | Faça isso... |
| --- | --- |
| **Permalinks** |No painel de WordPress saudação do novo site de saudação, clique **configurações** > **links permanentes**e, em seguida, atualizar a estrutura de links permanentes Olá. |
| **links de imagem/mídia** |tooupdate links toohello novo local, use Olá [veludo azuis atualizar URLs plug-in][velvet], uma pesquisa e substituição ferramenta ou atualizar manualmente os links de saudação do banco de dados. |
| **Temas** |Vá muito**aparência** > **tema**e, em seguida, atualize o tema do site Olá conforme necessário. |
| **Menus** |Se seu tema dá suporte a menus, home page do links tooyour ainda poderá ter subdiretório do antigo Olá incorporado a eles. Vá muito**aparência** > **Menus**e, em seguida, atualizá-los. |

#### <a name="hello-backup-and-restore-method"></a>Olá backup e restauração do método
1. O WordPress existente de backup do site usando as informações de saudação em [WordPress backups][wordpressbackup].
2. Fazer backup de banco de dados existente usando as informações de saudação em [fazendo backup de seu banco de dados][wordpressdbbackup].
3. Criar um banco de dados e restaurar o backup de saudação.

   1. Comprar um novo banco de dados de saudação [Azure Marketplace][cdbnstore], ou configurar um banco de dados MySQL em um [Windows] [ mysqlwindows] ou [Linux ] [ mysqllinux] máquina virtual.
   2. Use um cliente MySQL como [MySQL Workbench] [ workbench] tooconnect toohello novo banco de dados e importar o banco de dados do WordPress.
   3. Olá banco de dados toochange Olá domínio entradas tooyour nova do serviço de aplicativo do Azure domínio de atualização, por exemplo, mywordpress.azurewebsites.net. Saudação de uso [pesquisar e substituir para Script de bancos de dados do WordPress] [ searchandreplace] toosafely altere todas as instâncias.
4. Criar um aplicativo web no portal do Azure de saudação e publicar o backup do WordPress hello.

   1. toocreate um aplicativo web que tem um banco de dados em Olá [portal do Azure][mgmtportal], clique em **novo** > **Web + móvel**  >  **Do azure Marketplace** > **aplicativos Web** > **Web app + SQL** (ou **Web app + MySQL**) > **Criar**. Configure todos os toocreate de configurações de saudação necessária um aplicativo web vazio.
   2. Em seu backup WordPress, localize Olá **config.php wp** de arquivo e abra-o em um editor. Substitua Olá entradas com informações de saudação para seu novo banco de dados MySQL a seguir:

      * **DB_NAME**: nome de usuário de saudação do banco de dados de saudação.
      * **DB_USER**: Olá usuário nome usado tooaccess Olá banco de dados.
      * **DB_PASSWORD**: senha de usuário de saudação.

        Depois de alterar essas entradas, salve e feche o hello **config.php wp** arquivo.
   3. Saudação de uso [implantar um aplicativo web no serviço de aplicativo do Azure] [ deploy] informações tooenable Olá método de implantação que você deseja toouse e, em seguida, implante seu aplicativo de web do WordPress tooyour backup no serviço de aplicativo do Azure.
5. Após a implantação do site de WordPress hello, deve ser novo site de tooaccess capaz de saudação (como um aplicativo do serviço de aplicativo web) usando hello *. azurewebsite.net URL para o site de saudação.

### <a name="configure-your-site"></a>Configurar o site
Site de WordPress Olá foi criado ou migrado, usar Olá desempenho tooimprove de informações a seguir ou habilitar funcionalidades adicionais.

| toodo isso... | Use isto... |
| --- | --- |
| **Definir o modo do plano de Serviço de Aplicativo e o tamanho e habilitar o dimensionamento** |[Dimensionar um aplicativo Web no Serviço de Aplicativo do Azure][websitescale]. |
| **Habilitar conexões de banco de dados persistentes** |Por padrão, o WordPress não usa conexões de banco de dados persistente, o que podem causar o toobecome de banco de dados de toohello conexão limitada após várias conexões. as conexões persistentes tooenable, instalar Olá [plug-in de adaptador de conexões persistentes](https://wordpress.org/plugins/persistent-database-connection-updater/installation/). |
| **Melhorar o desempenho** |<ul><li><p><a href="https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/">Desabilitar o cookie ARR Olá</a>, que pode melhorar o desempenho quando o WordPress é executado em várias instâncias de aplicativos Web.</p></li><li><p>Habilitar caching. Você pode usar <a href="http://msdn.microsoft.com/library/azure/dn690470.aspx">cache Redis</a> (visualização) com hello <a href="https://wordpress.org/plugins/redis-object-cache/">Redis plug-in de WordPress de cache objeto</a>, ou você pode usar uma saudação outras ofertas de cache de saudação <a href="/gallery/store/">Azure Store</a>.</p></li><li><p>[Tornar o WordPress mais rápido com Wincache](https://wordpress.org/plugins/w3-total-cache/). O Wincache está habilitado por padrão para aplicativos Web. Ao usar o WinCache e Cache dinâmico juntos, desativar o cache de arquivo do WinCache, mas deixar o usuário hello e cache de sessão habilitada. tooturn desativar o cache de arquivo, em um arquivo. ini do nível de sistema, definir Olá seguinte valor:<br/><code>wincache.fcenabled = 0</code></p></li><li><p>[Dimensione um aplicativo Web no Serviço de Aplicativo do Azure][websitescale] e use o <a href="http://www.cleardb.com/developers/cdbr/introduction">Roteamento de Alta Disponibilidade do ClearDB</a> ou o <a href="http://www.mysql.com/products/cluster/">CGE de Cluster do MySQL</a>.</p></li></ul> |
| **Usar blobs para armazenamento** |<ol><li><p>[Criar uma conta de Armazenamento do Azure](../storage/common/storage-create-storage-account.md).</p></li><li><p>Saiba como muito[Olá Use rede de distribuição de conteúdo](../cdn/cdn-create-new-endpoint.md) toogeo-distribuir dados armazenados em blobs.</p></li><li><p>Instalar e configurar Olá <a href="https://wordpress.org/plugins/windows-azure-storage/">armazenamento do Azure para o plug-in do WordPress</a>.</p><p>Para detalhadas de instalação e informações de configuração para o plug-in do hello, consulte Olá <a href="http://plugins.svn.wordpress.org/windows-azure-storage/trunk/UserGuide.docx">guia do usuário</a>.</p> </li></ol> |
| **Habilitar o email** |Habilitar <a href="https://azure.microsoft.com/en-us/marketplace/partners/sendgrid/sendgrid-azure/">SendGrid</a> usando hello Azure Store. Instalar Olá <a href="http://wordpress.org/plugins/sendgrid-email-delivery-simplified">SendGrid plug-in</a> para WordPress. |
| **Configurar um nome de domínio personalizado** |[Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure][customdomain]. |
| **Habilitar protocolo HTTPS para um nome de domínio personalizado** |[Habilitar HTTPS para um aplicativo Web no Serviço de Aplicativo do Azure][httpscustomdomain]. |
| **Fazer balanceamento de carga ou distribuir geograficamente o site** |[Encaminhar tráfego com o Gerenciador de Tráfego do Azure][trafficmanager]. Se você estiver usando um domínio personalizado, consulte [configurar um nome de domínio personalizado no serviço de aplicativo do Azure] [ customdomain] para obter informações sobre como toouse Gerenciador de tráfego com nomes de domínio personalizado. |
| **Habilitar backups automatizados** |[Fazer backup de um aplicativo Web no Serviço de Aplicativo do Azure][backup]. |
| **Habilitar registro em log de diagnóstico** |[Habilitar o registro em log de diagnóstico para aplicativos Web no Serviço de Aplicativo do Azure][log]. |

## <a name="next-steps"></a>Próximas etapas
* [Otimização do WordPress](http://codex.wordpress.org/WordPress_Optimization)
* [Converter WordPress toomultisite no serviço de aplicativo do Azure](web-sites-php-convert-wordpress-multisite.md)
* [Assistente de atualização do ClearDB para o Azure](http://www.cleardb.com/store/azure/upgrade)
* [Hospedando o WordPress em uma subpasta do seu aplicativo Web no Serviço de Aplicativo do Azure](http://blogs.msdn.com/b/webapps/archive/2013/02/13/hosting-wordpress-in-a-subfolder-of-your-windows-azure-web-site.aspx)
* [Passo a passo: criar um site do WordPress usando o Azure](http://blogs.technet.com/b/blainbar/archive/2013/08/07/article-create-a-wordpress-site-using-windows-azure-read-on.aspx)
* [Hospedar o blog do WordPress existente no Azure](http://blogs.msdn.com/b/msgulfcommunity/archive/2013/08/26/migrating-a-self-hosted-wordpress-blog-to-windows-azure.aspx)
* [Habilitando formatação de permalinks no WordPress](http://www.iis.net/learn/extensions/url-rewrite-module/enabling-pretty-permalinks-in-wordpress)
* [Como toomigrate e execute seu blog do WordPress no serviço de aplicativo do Azure](http://www.kefalidis.me/2012/06/how-to-migrate-and-run-your-wordpress-blog-on-windows-azure-websites/)
* [Como toorun WordPress no serviço de aplicativo do Azure para livre](http://architects.dzone.com/articles/how-run-wordpress-azure)
* [WordPress no Azure em dois minutos ou menos](http://www.sitepoint.com/wordpress-windows-azure-2-minutes-less/)
* [Movendo um tooAzure de blog do WordPress - parte 1: criar um blog do WordPress no Azure](http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1)
* [Movendo um tooAzure de blog do WordPress - parte 2: transferir o conteúdo](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content)
* [Movendo um tooAzure de blog do WordPress - parte 3: configurar seu domínio personalizado](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain)
* [Movendo um tooAzure de blog do WordPress - parte 4: muito links permanentes e regras de reescrita de URL](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules)
* [Movendo um tooAzure de blog do WordPress - parte 5: mover de uma raiz de toohello subpasta](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root)
* [Como tooset a um WordPress web aplicativo em sua conta do Azure](http://www.itexperience.net/2014/01/20/how-to-set-up-a-wordpress-website-in-your-windows-azure-account/)
* [Preparando o WordPress no Azure](http://www.johnpapa.net/wordpress-on-azure/)
* [Dicas para o WordPress no Azure](http://www.johnpapa.net/azurecleardbmysql/)

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de você se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido e não há compromissos.
>
>

## <a name="whats-changed"></a>O que mudou
Uma alteração de toohello do guia de sites tooApp serviço, consulte [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714).

<!-- URL List -->

[performance-diagram]: ./media/web-sites-php-enterprise-wordpress/performance-diagram.png
[basic-diagram]: ./media/web-sites-php-enterprise-wordpress/basic-diagram.png
[multi-region-diagram]: ./media/web-sites-php-enterprise-wordpress/multi-region-diagram.png
[wordpress]: http://www.microsoft.com/web/wordpress
[officeblog]: http://blogs.office.com/
[bingblog]: http://blogs.bing.com/
[cdbnstore]: http://www.cleardb.com/store/azure
[storageplugin]: https://wordpress.org/plugins/windows-azure-storage/
[sendgridplugin]: http://wordpress.org/plugins/sendgrid-email-delivery-simplified/
[phpwebsite]: web-sites-php-configure.md
[customdomain]: app-service-web-tutorial-custom-domain.md
[trafficmanager]: ../traffic-manager/traffic-manager-overview.md
[backup]: web-sites-backup.md
[restore]: web-sites-restore.md
[rediscache]: https://azure.microsoft.com/documentation/services/redis-cache/
[managedcache]: http://msdn.microsoft.com/library/azure/dn386122.aspx
[websitescale]: web-sites-scale.md
[managedcachescale]: http://msdn.microsoft.com/library/azure/dn386113.aspx
[cleardbscale]: http://www.cleardb.com/developers/cdbr/introduction
[staging]: web-sites-staged-publishing.md
[monitor]: web-sites-monitor.md
[log]: web-sites-enable-diagnostic-log.md
[httpscustomdomain]: app-service-web-tutorial-custom-ssl.md
[mysqlwindows]:../virtual-machines/windows/classic/mysql-2008r2.md
[mysqllinux]:../virtual-machines/linux/classic/mysql-on-opensuse.md
[cge]: http://www.mysql.com/products/cluster/
[websitepricing]: /pricing/details/app-service/
[export]: http://en.support.wordpress.com/export/
[import]: http://wordpress.org/plugins/wordpress-importer/
[wordpressbackup]: http://wordpress.org/plugins/wordpress-importer/
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[createwordpress]: web-sites-php-web-site-gallery.md
[velvet]: https://wordpress.org/plugins/velvet-blues-update-urls/
[mgmtportal]: https://portal.azure.com/
[wordpressbackup]: http://codex.wordpress.org/WordPress_Backups
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[workbench]: http://www.mysql.com/products/workbench/
[searchandreplace]: http://interconnectit.com/124/search-and-replace-for-wordpress-databases/
[deploy]: web-sites-deploy.md
[posh]: /powershell/azureps-cmdlets-docs
[Azure CLI]:../cli-install-nodejs.md
[storesendgrid]: https://azure.microsoft.com/marketplace/partners/sendgrid/sendgrid-azure/
[cdn]: ../cdn/cdn-overview.md
