    ## Pesquisa sobre Prepared Statements 

    * O que são Prepared Statements?
        Prepared Statements são uma forma de fazer comandos SQL de uma maneira mais segura usando PHP e MySQL. Eles servem principalmente para evitar problemas de segurança, como o SQL Injection.
        Basicamente, ao invés de colocar diretamente uma informação que o usuário digitou dentro do comando SQL, usamos alguns espaços chamados de parâmetros, que geralmente aparecem como ?. Depois os valores são enviados separadamente para o banco de dados.

    * O que é SQL Injection?
        SQL Injection é um tipo de ataque que pode acontecer quando um sistema coloca diretamente informações que o usuário digitou dentro de um comando SQL.
        Isso pode ser um problema porque uma pessoa pode tentar colocar comandos SQL no lugar de uma informação normal, fazendo o banco de dados entender aquilo como um comando e não apenas como um texto.
        Dependendo da situação, isso pode permitir que uma pessoa consiga acessar, alterar ou até apagar informações do banco de dados.
        Por isso não é recomendado colocar diretamente os dados fornecidos pelo usuário dentro de uma consulta SQL.



    ( [Fonte 1] (https://www.w3schools.com/php/php_mysql_prepared_statements.asp) )
    ( [Fonte 2] (https://www.php.net/manual/en/mysqli.quickstart.prepared-statements.php) )


    ## Fork
    *