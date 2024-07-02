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

project é a tag de nível superior de nosso arquivo pom.xml, que encapsula todas as informações relacionadas ao nosso projeto Maven.

modelVersion representa qual versão do POM você está usando. O modelVersion para Maven 3 é sempre 4.0. Isso nunca mudará, a menos que você esteja usando outra versão principal do Maven.

### Adicionando Dependências ao nosso projeto

Adicionando o JUnit em nosso projeto.
Nota-se que a versão ficou destacada em vermelho, isso porque, precisamos depois de editar o arquivo POM.xml, fazer com o que o Maven adicione efetivamente essas dependencias ao nosso projeto.
Essa atualização pode ser feita, clicanco sobre o ícone azul a direita da imagem, ou também através da aba Maven, a direita do IntelliJ

![image](https://github.com/lschlestein/maven/assets/103784532/99c95877-d6a9-4ed5-a073-80479e7ff935)


![image](https://github.com/lschlestein/maven/assets/103784532/d1ea62ff-acd3-4785-b912-9d81703ea491)







