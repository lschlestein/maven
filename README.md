# Maven

### O que é Maven
O Apache Maven é uma ferramenta de gerenciamento de projetos usada para gerenciar projetos que são desenvolvidos usando principalmente linguagens JVM como Java.
Ele é baseado no conceito de Project Object Model (POM).

As principais tarefas e praticidades dessa ferramenta de gerenciamento de projetos incluem:
- Construir o Código Fonte
- Testar de código-fonte
- Empacotar o código-fonte em um artefato (ZIP, JAR, WAR ou EAR)
- Lidar com o controle de versão e releases dos artefatos
- Gerar JavaDocs a partir do código-fonte
- Gerenciar Dependências do Projeto

Maven também é chamado de ferramenta de construção ou ferramenta de gerenciamento de dependências.

Exemplo de um projeto Maven
![image](https://github.com/lschlestein/maven/assets/103784532/a25d1642-aaa4-425c-bb73-b485c1fca44b)

### Estrutura de um projeto Maven

![image](https://github.com/lschlestein/maven/assets/103784532/4323f47e-363a-470d-82de-1f4bb6973a14)
* A pasta src é a raiz do código-fonte e dos testes de nosso aplicativo. Então, temos as seguintes subpastas:
  * A pasta src/main/java contém o código-fonte java, do aplicativo
  * No src/main/resources estão os arquivos utilizados no projeto (ex.: Arquivos de propriedade, demais XML, CSV etc.). Caso se trate de um aplicativo, recursos estáticos também estarão nesta pasta.
  * Na pasta src/test/java ficam as classes de teste do projeto.
* External Libraries implementa as API´s Java no projeto.
* A pasta target armazena os arquivos de classe java compilados.
* Arquivo pom.xml que contém os metadados das dependências do projeto.

## Conceitos Básico do Maven
Explorando o arquivo POM.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.maven.exemaple</groupId>
    <artifactId>maven-example</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

</project>
```
project: é a tag de nível superior de nosso arquivo pom.xml, que encapsula todas as informações relacionadas ao nosso projeto Maven.
modelVersion: representa qual versão do POM você está usando. O modelVersion para Maven 3 é sempre 4.0. Isso nunca mudará, a menos que você esteja usando outra versão principal do Maven.

- groupId: Identificador único do projeto Maven
- artifactId: Nome do artefato em desenvolvimento (.jar)
- version: Versão que está sendo denvolvida (SNAPSHOT para versão em desenvolvimento).
  
Esse conjunto de informações também é conhecido como Maven coordinates

- maven.compiler.source: indica ao compilador que será utilizada a versão 17 do JDK nesse projeto
- maven.compiler.target: indica ao compilador que será utilizada a versão 17 do JDK para montar nosso .jar

### Adicionando Dependências ao nosso projeto

Adicionando o JUnit em nosso projeto.
Nota-se que a versão ficou destacada em vermelho, isso porque, precisamos depois de editar o arquivo POM.xml, fazer com o que o Maven adicione efetivamente essas dependencias ao nosso projeto.
Essa atualização pode ser feita, clicando sobre o ícone azul a direita da imagem, ou também através da aba Maven, a direita do IntelliJ.
Vale ressaltar que tags groupId, artifactId e principalmente version, são as referências para que o Maven possa baixar automaticamente essas dependências para o nosso projeto.

Também para exemplo adicionaremos a biblioteca Apache Commons Text. No final desse arquivo estão disponíveis as bibliotecas utilizadas.

![image](https://github.com/lschlestein/maven/assets/103784532/99c95877-d6a9-4ed5-a073-80479e7ff935)


Aba do Maven no IntelliJ

![image](https://github.com/lschlestein/maven/assets/103784532/9d717552-5018-4426-a7ea-3dde1afdf6a1)

Versões
Um projeto pode ser categorizada de duas maneiras:
- SNAPSHOT
- RELEASE
Quando o projeto está em desenvolvimento geralmente usamos as dependências SNAPSHOT. O Maven detecta que essa ainda é uma versão em desenvolvimento, e por essa tag ele poderá buscar por novas versões das dependências em nosso projeto, enquanto ele ainda esteja em desenvolvimento.
Quando o software está pronto para o lançamento, geralmente criamos uma versão RELEASE .
Ex.:

```xml
    <groupId>com.maven.exemaple</groupId>
    <artifactId>maven-example</artifactId>
    <version>1.0-SNAPSHOT</version>
```

### Escopos de Dependências

Cada dependência Maven pode ser categorizada em 6 escopos diferentes.
- *compile:* este é o escopo padrão se nenhum for especificado. As dependências de tempo de compilação estão disponíveis no classpath do projeto em todos os escopos.
- *provided:* Semelhante ao escopo compile, mas indica que o JDK ou o contêiner subjacente fornecerá a dependência no tempo de execução. A dependência estará disponível no momento da compilação, mas não será empacotada no artefato.
- *runtime:* as dependências definidas com este escopo estarão disponíveis apenas em tempo de execução (runtime), mas não em tempo de compilação. Um exemplo de uso: Imagine se você estiver usando o driver MySQL dentro do seu projeto, você pode adicionar a dependência com escopo como tempo de execução, para garantir que a abstração da API JDBC seja usada em vez da API do driver MySQL durante a implementação. Se o código-fonte incluir qualquer classe que faça parte da API JDBC do MySQL, o código não será compilado, pois a dependência não está disponível no momento da compilação.
- *test:* as dependências estão disponíveis apenas no momento da execução dos testes, exemplos típicos incluem JUnit.
- *system:* é semelhante ao escopo provided, mas a única diferença é que precisamos mencionar explicitamente onde a dependência pode ser encontrada no sistema, usando a tag systemPath:

```xml
<systemPath>${basedir}/lib/some-dependency.jar</systemPath>
```
### Repositórios

As dependências são armazenadas em um diretório especial chamado Repositório. Existem basicamente 2 tipos de repositórios:
Local Repository: Um Repositório local é um diretório na máquina onde o Maven está sendo executado.
O local padrão para o Repositório Local é ~/.m2 ou C:\Users<user-name>.m2\repository.
É importante ressaltar, que sempre o framework fará a busca pela dependência localmente, e caso não a encontronte, ele buscará a mesma do repositório central.

Remote Repository: Um Repositório remoto é um site onde podemos baixar dependências Maven. 
Quando uma dependência é definida dentro do arquivo pom.xml, o Maven primeiro verifica se a dependência já está presente no Repositório Local ou não.
Se não estiver, ele tenta se conectar ao Repositório Remoto, (Ex: https://repo.maven.org) e tenta baixar as dependências e armazená-las dentro do Repositório Local. 

```xml
<repositories>
 <repository>
  <id>my-internal-site</id>
  <url>http://myserver/repo</url>
  <snapshots>
      <enabled>true</enabled>
      <updatePolicy>always</updatePolicy>
  </snapshots>
 </repository>
</repositories>
```

A tag updatePolicy, pode ser:
- always: o frameworks sempre fará a verificação se há alguma versão mais recente.
- daily: essa é a configuração padrão, assim as versões serão atualizadas diariamente, na primeira execução do dia.
- interval:MMM: verifica a cada MMM minutos
- never: nunca verifica por atualizações
  
### Ciclo de Vida Da Versão Maven
Este ciclo de vida é dividido em 3 partes:

 - default
 - clean
 - site

Cada ciclo de vida é independente um do outro e podem ser executados juntos.

O ciclo de vida padrão é dividido em diferentes fases, como a seguir:

- *validate:* verifica se o arquivo pom.xml é válido ou não
- *compile:* compila o código-fonte dentro do projeto
- *test:* executa testes de unidade dentro do projeto
- *package:* empacota o código-fonte em um artefato (ZIP, JAR, WAR ou EAR)
- *integration-test:* executa testes marcados como testes de integração
- *verify:* verifica se o pacote criado é válido ou não.
- *install:* instala o pacote criado em nosso Repositório Local
- *site:* gera a documentação do projeto
- *deploy:* implanta o pacote criado no Repositório Remoto

O ciclo de vida clean é principalmente responsável por limpar o .class e metadados gerados pelas fases de compilação.
A fase do ciclo de vida do site é responsável por gerar a documentação Java.
Os 3 ciclos, quando executados, são quase sempre auxiliados por outros ciclos. Para maiores detalhes verifique a documentação do Maven.

### Plugins
Compilação

Para poder executar essas fases do ciclo de vida, o Maven nos fornece plugins para realizar cada tarefa.
Cada plugin está associado a um objetivo específico.

Plugin de Compilação Maven (Default)

O plug-in de compilação Maven é responsável por compilar os arquivos Java nos arquivos .class. É equivalente a executar javac.
Este plugin habilita a fase de compilação do ciclo de vida padrão.

Você pode adicionar o plugin de compilação conforme segue:
```xml
<project>
  ...
  <build>
    <pluginManagement>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.13.0</version>
          <configuration>
            <!-- put your configurations here -->
          </configuration>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
  ...
</project>
```
Por padrão, esse plugin executará todos os testes, se necessário, alguns poderão ser excluídos nessa fase:

Para maiores informações: [Apache Maven Plugins](https://maven.apache.org/plugins/maven-compiler-plugin/)

Apache Maven Assembly Plugin
Plugin utilizado para fazer o empacotamento de nossa aplicação em .jar. Com esse plugin configurado, nosso jar será empacotado com todos as dependências (jar) adicionadas em nosso projeto, em um único jar.

```xml
<build>
        <plugins>
            <plugin>
                <artifactId>maven-assembly-plugin</artifactId>
                <version>3.7.1</version>
                <configuration>
                    <descriptorRefs>
                        <descriptorRef>jar-with-dependencies</descriptorRef>
                    </descriptorRefs>
                    <archive>
                        <manifest>
                            <mainClass>com.maven.example.App</mainClass>
                        </manifest>
                    </archive>
                </configuration>
                <executions>
                    <execution>
                        <id>make-assembly</id> <!-- this is used for inheritance merges -->
                        <phase>package</phase> <!-- bind to the packaging phase -->
                        <goals>
                            <goal>single</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
```
Com esse plugin, quando gerarmos nosso .jar, (clean, install), serão gerados dois arquivos. Um jar é somente nosso programa, sem as dependências agrupadas junto a ele, e o outro, se a configuração do plugin for mantida como no exemplo, e o outro jar, que pode ser encontrada dentro da pasta /target dentro de nosso projeto, terá o sufixo jar-with-dependencies.jar. Esse jar contém todas a dependências empocatadas juntamente a nossa aplicação.

[Maven Assembly Plugin](https://maven.apache.org/plugins/maven-assembly-plugin/usage.html)

Instalação (Install)

Ele é usado para empacotar o código-fonte em um artefato de nossa escolha como um JAR e instalá-lo no Repositório local que é a pasta /.m2/repository.

A fase de instalação inclui também as fases anteriores do ciclo de vida:

valida pom.xml (validate)
compila código fonte (compile)
executa testes (test)
empacota código-fonte em JAR (package)
instala o JAR no repositório local (install)

Maven Clean

Ao executar as fases do ciclo de vida acima, os arquivos gerados são armazenados em uma pasta chamada destino.
Ao construir nosso código-fonte, precisamos começar do zero para que não haja inconsistências nos arquivos de classe ou JAR gerados.
Por esta razão, temos a fase de limpeza, em que todo o conteúdo da pasta de destino será removido. 

Existem uma diversidade de plugins que podem ser utilizados em um projeto com o Maven, os quais podem ser encontrados aqui:
[Plugins](maven.apache.org/plugins/index.html)

Criação de um projeto Maven no IntelliJ

![image](https://github.com/lschlestein/maven/assets/103784532/ab19b221-2c54-40cf-9f41-bd0699e10988)

![image](https://github.com/lschlestein/maven/assets/103784532/048e56ed-3b3b-4d55-bad2-f098f9d3e939)

Após, rode o maven com os ciclos clean e install:

```terminal
"C:\Program Files\Java\jdk-17\bin\java.exe" -Dmaven.multiModuleProjectDirectory=C:\Users\Lucas\eclipse-workspace\maven-example -Djansi.passthrough=true "-Dmaven.home=C:\Program Files\JetBrains\IntelliJ IDEA 2024.1.1\plugins\maven\lib\maven3" "-Dclassworlds.conf=C:\Program Files\JetBrains\IntelliJ IDEA 2024.1.1\plugins\maven\lib\maven3\bin\m2.conf" "-Dmaven.ext.class.path=C:\Program Files\JetBrains\IntelliJ IDEA 2024.1.1\plugins\maven\lib\maven-event-listener.jar" "-javaagent:C:\Program Files\JetBrains\IntelliJ IDEA 2024.1.1\lib\idea_rt.jar=50760:C:\Program Files\JetBrains\IntelliJ IDEA 2024.1.1\bin" -Dfile.encoding=UTF-8 -classpath "C:\Program Files\JetBrains\IntelliJ IDEA 2024.1.1\plugins\maven\lib\maven3\boot\plexus-classworlds-2.7.0.jar;C:\Program Files\JetBrains\IntelliJ IDEA 2024.1.1\plugins\maven\lib\maven3\boot\plexus-classworlds.license" org.codehaus.classworlds.Launcher -Didea.version=2024.1.2 clean install
[INFO] Scanning for projects...
[INFO] 
[INFO] ------------------< com.maven.exemaple:maven-example >------------------
[INFO] Building maven-example 1.0-SNAPSHOT
[INFO]   from pom.xml
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- clean:3.2.0:clean (default-clean) @ maven-example ---
[INFO] Deleting C:\Users\Lucas\eclipse-workspace\maven-example\target
[INFO] 
[INFO] --- resources:3.3.1:resources (default-resources) @ maven-example ---
[INFO] Copying 0 resource from src\main\resources to target\classes
[INFO] 
[INFO] --- compiler:3.11.0:compile (default-compile) @ maven-example ---
[INFO] Changes detected - recompiling the module! :source
[INFO] Compiling 1 source file with javac [debug target 17] to target\classes
[INFO] 
[INFO] --- resources:3.3.1:testResources (default-testResources) @ maven-example ---
[INFO] skip non existing resourceDirectory C:\Users\Lucas\eclipse-workspace\maven-example\src\test\resources
[INFO] 
[INFO] --- compiler:3.11.0:testCompile (default-testCompile) @ maven-example ---
[INFO] Changes detected - recompiling the module! :dependency
[INFO] 
[INFO] --- surefire:3.2.2:test (default-test) @ maven-example ---
[INFO] 
[INFO] --- jar:3.3.0:jar (default-jar) @ maven-example ---
[INFO] Building jar: C:\Users\Lucas\eclipse-workspace\maven-example\target\maven-example-1.0-SNAPSHOT.jar
[INFO] 
[INFO] --- install:3.1.1:install (default-install) @ maven-example ---
[INFO] Installing C:\Users\Lucas\eclipse-workspace\maven-example\pom.xml to C:\Users\Lucas\.m2\repository\com\maven\exemaple\maven-example\1.0-SNAPSHOT\maven-example-1.0-SNAPSHOT.pom
[INFO] Installing C:\Users\Lucas\eclipse-workspace\maven-example\target\maven-example-1.0-SNAPSHOT.jar to C:\Users\Lucas\.m2\repository\com\maven\exemaple\maven-example\1.0-SNAPSHOT\maven-example-1.0-SNAPSHOT.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  2.340 s
[INFO] Finished at: 2024-07-03T08:07:52-03:00
[INFO] ------------------------------------------------------------------------

Process finished with exit code 0
```
Nota-se que primeiramente o Maven limpará todo o conteúdo da pasta target e em seguida executa as seguintes ações:
default-resources:
default-compile:
default-testResources:
default-testCompile:
default-test:
default-jar:
default-install

### Dependências utilizadas neste exemplo:
```xml
<dependencies>
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-text</artifactId>
            <version>1.12.0</version>
            <scope>compile</scope>
        </dependency>

       <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-lang3</artifactId>
            <version>3.14.0</version>
            <scope>compile</scope>
        </dependency>

     <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <version>5.10.3</version>
            <scope>test</scope>
        </dependency>
</dependencies>
```
### Rodando um jar
Para rodar nosso projeto Maven recém compilado bastar executar a seguinte linha de comando:
```cmd
java -jar nome_do_arquivo_jar.jar

PS C:\users\maven-example\target> java -jar .\maven-example-1.0-SNAPSHOT-jar-with-dependencies.jar
```
Para que nossa aplicação funcione com essa linha de comando, precisamos tornar nosso jar executável, configurando o Maven Assembly Plugin como segue:
```xml
<project>
  [...]
  <build>
    [...]
    <plugins>
      <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <version>3.7.1</version>
        <configuration>
          [...]
          <archive>
            <manifest>
              <mainClass>org.sample.App</mainClass>
            </manifest>
          </archive>
        </configuration>
        [...]
      </plugin>
      [...]
</project>
```
Com a configuração acima, precisamos definir o class path, na linha de comando ao executar o .jar.

Outra forma de rodar o jar
Para essa segunda opção, devemos utilizar a configuração do Maven Assembly Plugin como segue:
```xml
<project>
 [...]
    <build>
        <plugins>
            <plugin>
                <artifactId>maven-assembly-plugin</artifactId>
                <version>3.7.1</version>
                <configuration>
                    <descriptorRefs>
                        <descriptorRef>jar-with-dependencies</descriptorRef>
                    </descriptorRefs>
                    <archive>
                        <manifest>
                            <mainClass>com.maven.example.App</mainClass>
                        </manifest>
                    </archive>
                </configuration>
                <executions>
                    <execution>
                        <id>make-assembly</id> <!-- this is used for inheritance merges -->
                        <phase>package</phase> <!-- bind to the packaging phase -->
                        <goals>
                            <goal>single</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
    [...]
</project>
```

Como executar uma aplicação maven Via terminal:

java -cp .\target\maven-example_-1.0-SNAPSHOT.jar com.maven.example.App

- java:
Invoca a Máquina Virtual Java (JVM) para executar nosso programa Java.

- -cp:
Esse é o argumento que especifica o "classpath". O classpath é uma lista de locais onde a JVM deve procurar classes e pacotes quando um programa é executado. Pode incluir diretórios, arquivos JAR e até URLs.

- .\target\maven-example-1.0-SNAPSHOT.jar:
Este é o caminho para o arquivo JAR que contém as classes compiladasde nosso projeto. Onde:

.\target: Especifica o diretório target no diretório atual (.\), que é o diretório onde o Maven coloca os arquivos compilados e os artefatos de build.
maven-example-1.0-SNAPSHOT.jar: Esse é o nome do arquivo JAR gerado pelo Maven. Nota-se que a versão que especificamos no arquivo pom.xml, é a que está nomeando nosso jar.

- com.maven.example.App:
Este é o nome completo da classe principal que desejamos executar. É composto pelo pacote (com.maven.example) e pelo nome da classe (App). O caminho completo para a classe App onde fica o método main de nossa aplicação.

Referências:

[Maven Complete Tutorial for Beginners](https://dev.to/saiupadhyayula/maven-complete-tutorial-for-beginners-1jek)

[Maven Assembly Plugin](https://maven.apache.org/plugins/maven-assembly-plugin/usage.html)

[Maven Repository](https://mvnrepository.com/)

[Apache Commons Word Utils](https://commons.apache.org/proper/commons-lang/apidocs/org/apache/commons/lang3/text/WordUtils.html)

[JUnit](https://junit.org/junit5/)





