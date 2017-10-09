### <a name="install-via-composer"></a>Instalar por meio do Composer
1. [Instale o Git][install-git]. Observe que no Windows, você também deverá adicionar variável de ambiente PATH do hello Git tooyour executável. 
2. Crie um arquivo chamado **composer.json** em Olá raiz do seu projeto e adicionar Olá tooit de código a seguir:
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. Baixe **[composer.phar][composer-phar]** na raiz do projeto.
4. Abra um prompt de comando e execute Olá após o comando na raiz de seu projeto
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
