- RESUMO PROVA 26/11

- CONTEUDO
  - Conexão JDBC com MySQL
    - Prepared Statement
  - Connection Factory
  - Centralizando o que é manipulação de dados
    - Padrão DAO - Data Access Object
  - Padrão MVC - Model View Controller

#Conexão JDBC com MySQL

- O que é JDBC?

  Pode-se dizer que é uma API que reúne conjuntos de classes e interfaces escritas na linguagem Java na qual possibilita se conectar através de um driver específico do banco de dados desejado. Com esse driver pode-se executar instruções SQL de qualquer tipo de banco de dados relacional.
  Para fazer a comunicação entre a aplicação e o SGBDs é necessário possuir um driver para a conexão desejada.
  
- O que é um Driver?
  
  Além de atuar como uma interface entre os SGBDs e as aplicações, também pode ser considerado como um tradutor que ajuda na definição das mensagens binárias trocadas com um protocolo de um SGBD.

- A classe DriverManager
  
  Cada driver que se deseja a usar precisa ser registrado nessa classe, pois oferece métodos estáticos para gerenciar um driver JDBC, é tambem responsável por se comunicar com todos os drivers que você deixou disponível.

- A interface Connection

  Representa uma conexão ao banco de dados. Nessa interface são apresentados os métodos mais utilizados.

- Metodo PreparedStatement
  
  Os Prepared Statements são declarações preparadas – literalmente como uma tradução do inglês para o português – é usado para criar um objeto que representa a instrução SQL que será executada, sem variação sintática, sendo que é invocado através do objeto Connetion.


-Exemplo de conexão
  public class JDBCExemplo {
      public static void main(String[] args){
          class.forName("com.jdbc.mysql.Driver");
          Connection conexao = DriverManager.getConnection("jdbc:mysql://localhost:3306/db_name", "root", "");
      }
  }
  
  class.forName(); - Carregamento do Driver JDBC
  
  - Diferença entre statement e prepared statement
  
    Quando executamos um statement, seja ele prepared ou não, na primeira vez ele é compilado no banco de dados.
    A diferença básica é que, o prepared statement, permite a passagem de parametro para o SQL e quando for chamado pela segunda vez, já estará compilada e preparado (como o nome diz) para ser executada, então, ganhamos algum tempo tornando as coisas um pouco mais ágeis.

Já o statement, sempre será compilado! 

# Connection Factory
  
  Em padrões de desenvolvimento, o "conceito de fábrica" nada mais é do que uma classe onde encapsulamos métodos muito utilizados, além da mesma ser capaz de retornar uma referência a um novo objeto.
  Resumindo, no caso da conexão a um Banco de Dados, criamos uma "ConnectionFactory" para nos conectarmos ao banco de dados, nos retornando uma instancia do objeto de conexão com o banco de dados, de maneira a evitar codificação repetida em diversos locais do código. 
  A classe ConnectionFactory deve possuir (ao menos) um método getConnection() que retorne um objeto Connection, contendo a conexão propriamente dita. Dentro do metodo getConnection() é onde toda as configurações de conexões devem ser realizadas, e onde é criado o objeto Connection.
  Uma fábrica de conexões pode nos permitir nao apenas a criar uma conexão com um UNICO banco de dados. Podemos implementar "N" métodos que retornem conexões, tendo cada metodo programado especificamente para bancos diferentes.
  EX:
  getConnectionMysql;
  getConnectionOracle;
  etc...

- Exemplo ConnectionFactory

  public class ConnectionFactory{
      public Connection getConnection(){
          class.forName("com.jdbc.mysql.Driver");
          Connection conexao = DriverManager.getConnection("jdbc:mysql://localhost:3306/db_name", "root", "");
          return con;
      }
  }
  
  Connection c = new ConnectionFactory().getConnection();
  
  #Padrão DAO- DATA ACCESS OBJECT








