# Java - Instalação e Ambiente

## Ferramentas úteis

$ sudo apt install rar unrar p7zip-full p7zip-rar unzip wget git

## Instalando o Java 10 (ppa >>> Obsoleto - Oracle)

$ sudo add-apt-repository ppa:linuxuprising/java
$ sudo apt update
$ sudo apt-get install oracle-java10-installer

## Instalando o Java 11 LTS (Oracle)

Agora o nome do pacote é adicionado "-local": These are step-by-step instructions for installing Oracle Java 11 using the new "oracle-java11-installer-local" package (https://www.linuxuprising.com/2019/06/new-oracle-java-11-installer-for-ubuntu.html):

1. Create an Oracle account at https://profile.oracle.com/myprofile/account/create-account.jspx and sign in

2. Download (https://www.oracle.com/java/technologies/javase-downloads.html) Oracle JDK 11 .tar.gz archive. Make sure the Oracle JDK version you're downloading is the same as the oracle-java11-installer-local package version. E.g. the installer is currently version 11.0.6, so it can be used to install Oracle JDK 11.0.6.

3. Create a /var/cache/oracle-jdk11-installer-local/ folder, and copy the Oracle JDK 11 .tar.gz to this folder.

For example, create the /var/cache/oracle-jdk11-installer-local/ folder and copy jdk-11.0.3_linux-x64_bin.tar.gz to this folder (from the current directory) using:

$ cd Downloads
$ ls 
jdk-11.0.6_linux-x64_bin.tar.gz

$ sudo mkdir -p /var/cache/oracle-jdk11-installer-local/
$ sudo cp jdk-11.0.6_linux-x64_bin.tar.gz /var/cache/oracle-jdk11-installer-local/

4. Purge the old oracle-java11-installer package if you had it installed:

$ sudo apt purge oracle-java11-installer

5. Add the Linux Uprising Java PPA (it works on Ubuntu, Linux Mint, Pop!_OS, elementary OS, and any other Ubuntu based Linux distribution) and install the oracle-java11-installer-local package to set up Oracle Java 11:

$ sudo add-apt-repository ppa:linuxuprising/java
$ sudo apt update
$ sudo apt install oracle-java11-installer-local

No DEBIAN: On Debian, add the PPA and install the oracle-java11-installer-local package using:

$ su -
$ echo "deb http://ppa.launchpad.net/linuxuprising/java/ubuntu focal main" | tee /etc/apt/sources.list.d/linuxuprising-java.list
$ apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 73C3DB2A
$ apt-get update
$ apt-get install oracle-java11-installer-local
$ exit

6. This is optional. Use the command below to install oracle-java11-set-default-local, which makes Oracle JDK 11 default:

$ sudo apt install oracle-java11-set-default-local

On Ubuntu, this package is automatically installed when installing oracle-java11-installer-local, but that's not the case on Linux Mint.

If you don't want Oracle Java 11 to be the default JDK version on your system, remove the package that makes it default, like this:

$ sudo apt remove oracle-java11-set-default-local

7. Variáveis de ambiente:

Edit your ~/.bashrc file and add the paths as follows (.bashrc or /etc/profile file):
$ nano ~/.bashrc

insert following lines:

export JAVA_HOME="/usr/lib/jvm/java-11-oracle"
export PATH=$JAVA_HOME/bin:$PATH

check with:

$ echo $JAVA_HOME

8. Verifica a versão do java instalado:

$ java -version
$ java --version
$ javac -version

9. Mudar versão java

Lista as versões instaladas:
$ update-java-alternatives --list

Configura java:
$ sudo update-alternatives --config java

Configura javac:
$ sudo  update-alternatives --config javac

## Ferramentas de build (Maven e Gradle)

### Gradle
+ https://gradle.org/

- versão 7.1
- Ganhando popularidade (Android Studio)
- Usa linguagem de programação Groovy

$ mkdir /opt/gradle
$ cd ~/Downloads
$ unzip -d /opt/gradle gradle-X.X-bin.zip
$ ls /opt/gradle/gradle-X.X 
$ export PATH=$PATH:/opt/gradle/gradle-X.X/bin

- add Gradle to PATH environment variable:
$ echo "export PATH=$PATH:/opt/gradle/gradle-X.X/bin" >> ~/.bashrc

- this way is better, like i did for java :)
export GRADLE_HOME="/opt/gradle/gradle-X.X"
export PATH=$GRADLE_HOME/bin:$PATH

- execute ~/.bashrc file:
$ source ~/.bashrc

- check Gradle version:
$ gradle -v
$ echo $GRADLE_HOME

- pode instalar pelo apt tbm
$ sudo apt purge gradle //old versions

### Maven
+ https://maven.apache.org/

- versão 3.8.1
- Legados do ANT 
- Baseado no XML

$ mkdir /opt/maven
$ unzip -d /opt/maven apache-maven-X.X.X-bin.zip
$ ls /opt/maven/apache-maven-X.X.X 
$ export PATH=$PATH:/opt/maven/apache-maven-X.X.X/bin

- this way is better, like i did for java :)
export MAVEN_HOME="/opt/maven/apache-maven-3.8.1"
export PATH=$MAVEN_HOME/bin:$PATH

$ mvn -v
$ echo $MAVEN_HOME

### Wrappers
+ https://github.com/takari/maven-wrapper
+ https://docs.gradle.org/current/userguide/gradle_wrapper.html

- Gradle
$ mkdir project_folder && cd project_folder
$ touch settings.gradle
$ gradle wrapper
$ ./gradlew -v 

- Maven 
$ mvn -N io.takari:maven:wrapper
$ ./mvnw -v 

- Garante a mesma versão para todos os desenvolvedores
