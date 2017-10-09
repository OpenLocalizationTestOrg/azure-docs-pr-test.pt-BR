---
title: aplicativo web de aaaPython com Django em uma VM do Linux do Azure | Microsoft Docs
description: Saiba como toohost um baseado em Django web aplicativo no Azure usando uma VM do Linux.
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 520c47e19e8ffb4bb866f70772d506ddf76e242c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a>Aplicativo Web Django Olá, Mundo em uma VM do Linux
> [!div class="op_single_selector"]
> * [Windows](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [Mac/Linux](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

Este tutorial mostra como toohost um site baseado em Django no Linux em máquinas virtuais do Azure. Tutorial de Olá, vamos supor sem experiência anterior com o Azure. Quando você concluir o tutorial Olá, você pode ter um aplicativo baseado em Django para cima e em execução na nuvem hello.

Saiba como:

* Configure uma máquina virtual do Azure de toohost Django. Embora este tutorial explica como toodo para **Linux**, você pode fazer hello mesmo para uma VM do Windows Server hospedado no Azure. 
* Crie um novo aplicativo Django do Linux.

tutorial de saudação mostra como toobuild um Hello World básicas de aplicativo web. aplicativo Hello é hospedado em uma máquina virtual do Azure.

Olá captura de tela a seguir mostra um aplicativo hello concluída:

![Uma janela do navegador exibe a página do Olá Olá, mundo no Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Criar e configurar uma máquina virtual do Azure de toohost Django

1. toocreate uma máquina virtual do Azure com hello distribuição Ubuntu Server 14.04 LTS, consulte [criar uma máquina virtual Linux no portal do Azure de saudação](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Você também pode escolher a autenticação de senha em vez de usar uma chave pública SSH.
2. tooedit Olá rede segurança grupo tooallow entrada HTTP tráfego tooport 80, consulte [criar grupos de segurança de rede no portal do Azure de saudação](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).
3. (Opcional) Por padrão, a nova máquina virtual não tem um FQDN (nome de domínio totalmente qualificado).  toocreate uma VM com um FQDN, consulte [criar um FQDN no hello portal do Azure para uma VM do Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Esta etapa não é necessária para concluir este tutorial.

## <a id="setup"></a>Configurar o ambiente de desenvolvimento Olá
> [!NOTE]
> Se você precisa tooinstall Python ou bibliotecas de cliente toouse Olá, consulte Olá [guia de instalação do Python](../../python-how-to-install.md).

Olá Ubuntu Linux VM tem Python 2.7 pré-instalado, mas ela não vem com o Apache ou Django. Completar Olá seguindo as etapas tooconnect tooyour VM e instalar o Apache e Django:

1. Abra uma nova janela de terminal.
2. tooconnect toohello VM do Azure, digite Olá comando a seguir. Se você não criar um FQDN, você pode se conectar usando o endereço IP público Olá que é exibido na máquina virtual de saudação resumida Olá portal do Azure.
   
       $ ssh yourusername@yourVmUrl
3. tooinstall Django, digite Olá comandos a seguir:
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. tooinstall Apache com mod-wsgi, digite Olá comando a seguir:
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a>Criar um novo aplicativo Django
1. toouse tooaccess SSH sua VM, a janela do Terminal Olá abrir usado na saudação anterior de seção.
2. toocreate um novo projeto de Django, digite Olá comandos a seguir:
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   Olá `django-admin.py` script gera uma estrutura básica para sites baseados em Django:
   
   * `helloworld/manage.py` ajuda a iniciar a hospedagem e parar a hospedagem do seu site da web baseado em Django.
   * `helloworld/helloworld/settings.py` tem configurações do Django para seu aplicativo.
   * `helloworld/helloworld/urls.py`tiver um código de mapeamento de saudação entre cada URL e sua exibição.
3. No diretório de /var/www/helloworld/helloworld hello, crie um novo arquivo denominado views.py. Este arquivo tem o modo de exibição de saudação que renderiza a página de "hello world" hello. Em seu editor de código, digite Olá comandos a seguir:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Substitua o conteúdo de saudação do arquivo de urls.py de saudação com hello comandos a seguir:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a>Configurar o Apache
1. Na pasta de /etc/apache2/sites-available/helloworld.conf hello, crie um arquivo de configuração de host virtual Apache. Definir Olá conteúdo toohello valores a seguir. Substituir *Nomedasuavm* com nome real de saudação do máquina Olá que você está usando (por exemplo, *pyubuntu*).
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. site de saudação tooactivate, use Olá comando a seguir:
   
       $ sudo a2ensite helloworld
3. toorestart Apache, use Olá comando a seguir:
   
       $ sudo service apache2 reload
4. Carregar Olá página da Web no navegador:
   
   ![Uma janela do navegador exibirá a página do hello hello world no Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a>Desligar a máquina virtual do Azure
Quando você concluir este tutorial, é recomendável desligar ou remover Olá VM do Azure que você criou para o tutorial hello. Isso libera os recursos para outros tutoriais e você pode evitar incorrer em encargos de uso do Azure.

