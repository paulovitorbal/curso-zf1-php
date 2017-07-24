# O que são os PSRs

`PHP Stardart Recomendation`, ou em bom português, recomendações de padrões PHP. São recomendações feitas pelo PHP-FIG (framework interop group) que tentam padronizar certos aspectos para garantir a interoperabilidade entre diferentes fontes. Mais informações no site do [PHP-FIG](http://www.php-fig.org).

Em julho de 2017 haviam 18 proposições, sendo 9 aceitas, 1 rejeitada, 8 em rascunho.

## PSR 0 - Padrão para carregamento automático

Apesar de estar em desuso e ter sido substituída pela PSR-4, a PSR-0 é utilizada pelo zend framework 1 que é objeto deste curso.

São requisitos obrigatórios para o código seja considerado aderente a PSR-0:
*  Um namespace completamente qualificado e a classe com a seguinte estrutura \<nome do fornecedor>\(<namespace>)*<Nome da classe);
*  Cada namespace deve ter seu nível mais alto "nome do fornecedor";
*  Cada namespace deve ter quaisquer quantidade de subníveis;
*  Cada separador de namespace é convertido para um separador de diretórios (constante: DIRECTORY_SEPARATOR) quando do carregamento do arquivo do sistema de arquivos;
*  Cada caractere "_" no nome da classe é convertido para um separador de diretórios. O caracter "_" não possui nenhum significado especial no nome do namespace;
*  O namespace completamente qualificado é terminado com .php quando do carregamento do arquivo do sistema de arquivos;
*  Nomes de fornecedor, namespaces e nome de classes podem conter caracteres alfabéticos e qualquer combinação de letras em caixa alta ou baixa.

|Namespaces completamente qualificado|Arquivo|
|----|----|
|`\Doctrine\Common\IsolatedClassLoader`|`/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`|
|`\Symfony\Core\Request`|`/path/to/project/lib/vendor/Symfony/Core/Request.php`|
|`\Zend\Acl`|`/path/to/project/lib/vendor/Zend/Acl.php`|
|`\namespace\package_name\Class_Name`|`/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`|

