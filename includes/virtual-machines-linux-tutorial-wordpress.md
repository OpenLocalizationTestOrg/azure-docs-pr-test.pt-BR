## <a name="install-wordpress"></a><span data-ttu-id="7375b-101">Instalar o WordPress</span><span class="sxs-lookup"><span data-stu-id="7375b-101">Install WordPress</span></span>

<span data-ttu-id="7375b-102">Se você quiser tootry sua pilha, instale um aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7375b-102">If you want tootry your stack, install a sample app.</span></span> <span data-ttu-id="7375b-103">Por exemplo, Olá etapas instala código-fonte aberto Olá [WordPress](https://wordpress.org/) plataforma toocreate sites e blogs.</span><span class="sxs-lookup"><span data-stu-id="7375b-103">As an example, hello following steps install hello open source [WordPress](https://wordpress.org/) platform toocreate websites and blogs.</span></span> <span data-ttu-id="7375b-104">Incluir outra cargas de trabalho tootry [Drupal](http://www.drupal.org) e [o Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="7375b-104">Other workloads tootry include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="7375b-105">Esta instalação do WordPress destina-se à prova de conceito.</span><span class="sxs-lookup"><span data-stu-id="7375b-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="7375b-106">Para obter mais informações e configurações para instalação de produção, consulte Olá [WordPress documentação](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="7375b-106">For more information and settings for production installation, see hello [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-hello-wordpress-package"></a><span data-ttu-id="7375b-107">Instalar o pacote de WordPress Olá</span><span class="sxs-lookup"><span data-stu-id="7375b-107">Install hello WordPress package</span></span>

<span data-ttu-id="7375b-108">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7375b-108">Run hello following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="7375b-109">Configurar WordPress</span><span class="sxs-lookup"><span data-stu-id="7375b-109">Configure WordPress</span></span>

<span data-ttu-id="7375b-110">Configure o WordPress toouse MySQL e PHP.</span><span class="sxs-lookup"><span data-stu-id="7375b-110">Configure WordPress toouse MySQL and PHP.</span></span> <span data-ttu-id="7375b-111">Executar Olá tooopen de comando a seguir em um editor de texto de sua escolha e criar o arquivo hello `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="7375b-111">Run hello following command tooopen a text editor of your choice and create hello file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="7375b-112">Saudação de copiar arquivos de toohello linhas a seguir, substituindo sua senha de banco de dados para *yourPassword* (deixe outros valores inalterados).</span><span class="sxs-lookup"><span data-stu-id="7375b-112">Copy hello following lines toohello file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="7375b-113">Salve arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="7375b-113">Then save hello file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="7375b-114">Em um diretório de trabalho, crie um arquivo de texto `wordpress.sql` banco de dados do tooconfigure Olá WordPress:</span><span class="sxs-lookup"><span data-stu-id="7375b-114">In a working directory, create a text file `wordpress.sql` tooconfigure hello WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="7375b-115">Adicionar Olá comandos a seguir, substituindo sua senha de banco de dados para *yourPassword* (deixe outros valores inalterados).</span><span class="sxs-lookup"><span data-stu-id="7375b-115">Add hello following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="7375b-116">Salve arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="7375b-116">Then save hello file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="7375b-117">Execute Olá banco de dados do comando toocreate Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="7375b-117">Run hello following command toocreate hello database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="7375b-118">Após a conclusão do comando hello, exclua o arquivo de saudação `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="7375b-118">After hello command completes, delete hello file `wordpress.sql`.</span></span>

<span data-ttu-id="7375b-119">Mova a raiz do documento hello WordPress instalação toohello web server:</span><span class="sxs-lookup"><span data-stu-id="7375b-119">Move hello WordPress installation toohello web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="7375b-120">Agora você pode concluir a instalação do WordPress hello e publicar na plataforma de saudação.</span><span class="sxs-lookup"><span data-stu-id="7375b-120">Now you can complete hello WordPress setup and publish on hello platform.</span></span> <span data-ttu-id="7375b-121">Abra um navegador e vá muito`http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="7375b-121">Open a browser and go too`http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="7375b-122">Substitua o endereço IP público de saudação da VM.</span><span class="sxs-lookup"><span data-stu-id="7375b-122">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="7375b-123">Ela deve ser a imagem toothis semelhante.</span><span class="sxs-lookup"><span data-stu-id="7375b-123">It should look similar toothis image.</span></span>

![Página de instalação do WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)