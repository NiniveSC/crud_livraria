    ##Pesquisa sobre Prepared Statements 

    *O que são Prepared Statements?
        São uma forma de fazer comandos SQL de uma maneira mais segura usando PHP e MySQL. Eles servem principalmente para evitar problemas de segurança, como o SQL Injection.
        Basicamente, ao invés de colocar diretamente uma informação que o usuário digitou dentro do comando SQL, usamos alguns espaços chamados de parâmetros, que geralmente aparecem como ?. Depois os valores são enviados separadamente para o banco de dados.

    *O que é SQL Injection?
        É um tipo de ataque que pode acontecer quando um sistema coloca diretamente informações que o usuário digitou dentro de um comando SQL.
        Isso pode ser um problema porque uma pessoa pode tentar colocar comandos SQL no lugar de uma informação normal, fazendo o banco de dados entender aquilo como um comando e não apenas como um texto.
        Dependendo da situação, isso pode permitir que uma pessoa consiga acessar, alterar ou até apagar informações do banco de dados.
        Por isso não é recomendado colocar diretamente os dados fornecidos pelo usuário dentro de uma consulta SQL.

    *Como os Prepared Statements ajudam a prevenir do SQL Injection?
        Eles separam o comando SQL dos dados que serão usados nele.
        Primeiro o banco recebe o modelo do comando, com os ? no lugar dos valores. Depois os valores são associados a esses espaços e a consulta é executada.
        Dessa forma, o banco entende que os valores enviados são apenas dados e não partes do comando SQL. Isso ajuda a impedir que um usuário consiga colocar um comando dentro de uma informação e fazer o banco executar aquilo.

    *Como funciona?
        O funcionamento de um Prepared Statement acontece basicamente em três partes: preparação, associação dos valores e execução.
        -Primeiro usamos o prepare() para preparar o comando SQL;
        -Depois usamos o bind_param() para colocar os valores nos lugares dos ?;
        -Por último usamos o execute() para executar o comando.

    *Prepared Statements no CRUD
        No nosso projeto da livraria temos um CRUD, que possui quatro operações principais. O cadastro usa o INSERT, a consulta usa o SELECT, a atualização usa o UPDATE e a exclusão usa o DELETE.
        Essas operações recebem informaçõe como o nome do livro, autor, e o ano de lançamento. Por isso é importante tomar cuidado com a forma que essas informações são enviadas para o banco.
        Um exemplo pratico é que o título e o autor são textos, por isso usamos s, e o ano é um número inteiro, por isso usamos i. Mas existe outros tipos: d = número decimal e b = dados binários, como imagens ou arquivos.


    ([Fonte 1](https://www.w3schools.com/php/php_mysql_prepared_statements.asp))
    ([Fonte 2](https://www.php.net/manual/en/mysqli.quickstart.prepared-statements.php))



    ##Fork

    *Problema encontrado:
        No cadastro, os dados enviados pelo formulário que são o título, autor e ano, são colocados diretamente dentro do comando SQL. Isso como vimos deixa o sistema vulnerável a SQL Injection.

            $sql = "INSERT INTO livros (titulo,autor,ano) VALUES ('$titulo','$autor','$ano')";
            mysqli_query($conexao, $sql);

        Essa parte do código mostra que os dados estão sendo diretamente inseridos na tabela do banco de dados no mysql, o que é o errado a se fazer.

    *Como solucionei:
        A solução que tive foi alterar o código para utilizar Prepared Statement, separando o comando SQL dos dados recebidos pelo usuário.

            $sql = "INSERT INTO livros (titulo,autor,ano) VALUES (?, ?, ?)";

            $stmt = $conexao->prepare($sql);
            $stmt->bind_param("ssi", $titulo, $autor, $ano);
            $stmt->execute();

        O $conexao faz a conexão com o banco de dados. Depois vem o prepare(), que prepara o comando SQL antes de enviar para o banco. O $stmt guarda esse comando preparado. Em seguida, o bind_param() liga os valores aos ? do comando e o "ssi" indica o tipo de cada valor, sendo s para texto e i para número inteiro. Por último, o execute() executa o comando no banco de dados.

    *Conclusão que tive:
        Com essa atividade consegui entender melhor o que são Prepared Statements e porque eles são importantes para a segurança do código. Antes eu não sabia que colocar os dados diretamente no SQL poderia causar problemas como o SQL Injection. Ao realizar a pesquisa e o Fork do CRUD da livraria, consegui encontrar esse problema no cadastro (e no final da atividade entendi que se aplica para atualizar, editar e excluir) e mudar o código para usar o Prepared Statements. Também descobri que essa mudança não aparece para o usuário, mas deixa a comunicação com o banco de dados mais segura. Com isso, entendi que os Prepared Statements são uma boa prática para evitar problemas e proteger melhor os dados de uma aplicação.