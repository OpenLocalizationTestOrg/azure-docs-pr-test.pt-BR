## <a name="install-wordpress"></a>Instalar o WordPress

Se você quiser tootry sua pilha, instale um aplicativo de exemplo. Por exemplo, Olá etapas instala código-fonte aberto Olá [WordPress](https://wordpress.org/) plataforma toocreate sites e blogs. Incluir outra cargas de trabalho tootry [Drupal](http://www.drupal.org) e [o Moodle](https://moodle.org/). 

Esta instalação do WordPress destina-se à prova de conceito. Para obter mais informações e configurações para instalação de produção, consulte Olá [WordPress documentação](https://codex.wordpress.org/Main_Page). 



### <a name="install-hello-wordpress-package"></a>Instalar o pacote de WordPress Olá

Execute Olá comando a seguir:

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a>Configurar WordPress

Configure o WordPress toouse MySQL e PHP. Executar Olá tooopen de comando a seguir em um editor de texto de sua escolha e criar o arquivo hello `/etc/wordpress/config-localhost.php`:

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
Saudação de copiar arquivos de toohello linhas a seguir, substituindo sua senha de banco de dados para *yourPassword* (deixe outros valores inalterados). Salve arquivo hello.

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

Em um diretório de trabalho, crie um arquivo de texto `wordpress.sql` banco de dados do tooconfigure Olá WordPress: 

```bash
sudo sensible-editor wordpress.sql
```

Adicionar Olá comandos a seguir, substituindo sua senha de banco de dados para *yourPassword* (deixe outros valores inalterados). Salve arquivo hello.

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


Execute Olá banco de dados do comando toocreate Olá a seguir:

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

Após a conclusão do comando hello, exclua o arquivo de saudação `wordpress.sql`.

Mova a raiz do documento hello WordPress instalação toohello web server:

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

Agora você pode concluir a instalação do WordPress hello e publicar na plataforma de saudação. Abra um navegador e vá muito`http://yourPublicIPAddress/wordpress`. Substitua o endereço IP público de saudação da VM. Ela deve ser a imagem toothis semelhante.

![Página de instalação do WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)