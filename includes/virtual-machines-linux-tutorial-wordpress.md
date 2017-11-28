## <a name="install-wordpress"></a><span data-ttu-id="d3ad4-101">Instalar o WordPress</span><span class="sxs-lookup"><span data-stu-id="d3ad4-101">Install WordPress</span></span>

<span data-ttu-id="d3ad4-102">Se você quiser experimentar sua pilha, instale um aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d3ad4-102">If you want to try your stack, install a sample app.</span></span> <span data-ttu-id="d3ad4-103">Por exemplo, as etapas a seguir instalam a plataforma [WordPress](https://wordpress.org/) de código-fonte aberto para criar sites e blogs.</span><span class="sxs-lookup"><span data-stu-id="d3ad4-103">As an example, the following steps install the open source [WordPress](https://wordpress.org/) platform to create websites and blogs.</span></span> <span data-ttu-id="d3ad4-104">Outras cargas de trabalho tentam incluir [Drupal](http://www.drupal.org) e [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="d3ad4-104">Other workloads to try include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="d3ad4-105">Esta instalação do WordPress destina-se à prova de conceito.</span><span class="sxs-lookup"><span data-stu-id="d3ad4-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="d3ad4-106">Para saber mais e conhecer as configurações de instalação em produção, consulte a [documentação do WordPress](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="d3ad4-106">For more information and settings for production installation, see the [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-the-wordpress-package"></a><span data-ttu-id="d3ad4-107">Instalar o pacote de WordPress</span><span class="sxs-lookup"><span data-stu-id="d3ad4-107">Install the WordPress package</span></span>

<span data-ttu-id="d3ad4-108">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3ad4-108">Run the following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="d3ad4-109">Configurar WordPress</span><span class="sxs-lookup"><span data-stu-id="d3ad4-109">Configure WordPress</span></span>

<span data-ttu-id="d3ad4-110">Configure o WordPress para usar PHP e MySQL.</span><span class="sxs-lookup"><span data-stu-id="d3ad4-110">Configure WordPress to use MySQL and PHP.</span></span> <span data-ttu-id="d3ad4-111">Execute o seguinte comando para abrir um editor de texto de sua preferência e criar o arquivo `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="d3ad4-111">Run the following command to open a text editor of your choice and create the file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="d3ad4-112">Copie as linhas a seguir no arquivo, substituindo *yourPassword* por sua senha de banco de dados (não altere outros valores).</span><span class="sxs-lookup"><span data-stu-id="d3ad4-112">Copy the following lines to the file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="d3ad4-113">Em seguida, salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="d3ad4-113">Then save the file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="d3ad4-114">Em um diretório de trabalho, crie um arquivo de texto `wordpress.sql` para configurar o banco de dados do WordPress:</span><span class="sxs-lookup"><span data-stu-id="d3ad4-114">In a working directory, create a text file `wordpress.sql` to configure the WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="d3ad4-115">Adicione os comandos a seguir, substituindo *yourPassword* por sua senha de banco de dados (não altere outros valores).</span><span class="sxs-lookup"><span data-stu-id="d3ad4-115">Add the following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="d3ad4-116">Em seguida, salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="d3ad4-116">Then save the file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
TO wordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="d3ad4-117">Execute o comando a seguir para criar o banco de dados:</span><span class="sxs-lookup"><span data-stu-id="d3ad4-117">Run the following command to create the database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="d3ad4-118">Após a conclusão do comando, exclua o arquivo `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="d3ad4-118">After the command completes, delete the file `wordpress.sql`.</span></span>

<span data-ttu-id="d3ad4-119">Mova a instalação do WordPress para a raiz do documento do servidor Web:</span><span class="sxs-lookup"><span data-stu-id="d3ad4-119">Move the WordPress installation to the web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="d3ad4-120">Agora você pode concluir a instalação do WordPress e publicar na plataforma.</span><span class="sxs-lookup"><span data-stu-id="d3ad4-120">Now you can complete the WordPress setup and publish on the platform.</span></span> <span data-ttu-id="d3ad4-121">Abra um navegador e acesse `http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="d3ad4-121">Open a browser and go to `http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="d3ad4-122">Substitua o endereço IP público de sua VM.</span><span class="sxs-lookup"><span data-stu-id="d3ad4-122">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="d3ad4-123">A página deve ser semelhante a esta imagem.</span><span class="sxs-lookup"><span data-stu-id="d3ad4-123">It should look similar to this image.</span></span>

![Página de instalação do WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)