### <a name="install-via-composer"></a><span data-ttu-id="dd3d1-101">Instalar por meio do Composer</span><span class="sxs-lookup"><span data-stu-id="dd3d1-101">Install via Composer</span></span>
1. <span data-ttu-id="dd3d1-102">[Instale o Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="dd3d1-102">[Install Git][install-git].</span></span> <span data-ttu-id="dd3d1-103">Observe que no Windows, você também deverá adicionar variável de ambiente PATH do hello Git tooyour executável.</span><span class="sxs-lookup"><span data-stu-id="dd3d1-103">Note that on Windows, you must also add hello Git executable tooyour PATH environment variable.</span></span> 
2. <span data-ttu-id="dd3d1-104">Crie um arquivo chamado **composer.json** em Olá raiz do seu projeto e adicionar Olá tooit de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd3d1-104">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. <span data-ttu-id="dd3d1-105">Baixe **[composer.phar][composer-phar]** na raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="dd3d1-105">Download **[composer.phar][composer-phar]** in your project root.</span></span>
4. <span data-ttu-id="dd3d1-106">Abra um prompt de comando e execute Olá após o comando na raiz de seu projeto</span><span class="sxs-lookup"><span data-stu-id="dd3d1-106">Open a command prompt and execute hello following command in your project root</span></span>
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
