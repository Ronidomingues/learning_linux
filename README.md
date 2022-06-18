# Linux Debian 11

# Comandos Para Manipular Diretórios e Arquivos

1. **`mkdir` --> Permite criar novos diretórios.**

|Argumentos|Objetivos|
|--------|----|
|`-m`|(–mode=MODE): usada a fim de estabelecer regras e permissões ao diretório criado, de modo similar ao comando chmod.|
|`-p`|(–parents): a opção `-p` habilita a criação de diretórios parentes quando necessário.|
|`-v`|(–verbose): imprime em tela uma mensagem para cada diretório criado.|
|`-Z`|Ajusta o contexto de segurança SELinux de cada diretório criado para o seu tipo padrão.|
|`-help`|Apresenta as opções existentes.|
|`mkdir -m a=rwx '<file_name>'`|Começando pelo `a` (all), este é um parâmetro que estabelece a aplicação das permissões a todos os usuários da máquina. Já as letras `r`, `w` e `x` significam read, write e execute, respectivamente.|

2. **`rmdir` --> Permite remover diretórios.**
   - **OBS.: os diretrtórios a serem removidos devem estar vazios**
3. **`rm` --> Permite a remoção de arquivos.**

|Argumentos|Objetivos|
|--------|----|
|`-f`|(–force): ignora arquivos e argumentos inexistentes.|
|`-r`, `-R`|(–recursive): remove diretórios e respectivos conteúdos recursivamente.|
|`-d`,`–dir`|Remove diretórios vazios.|
|`-v`|(–verbose): explica as ações promovidas com o uso do comando rm.|
|`–preserve-root`|Não remove o diretório root.|
|`–one-file-system`|Ao remover uma hierarquia recursivamente, o comando pula qualquer diretório que se encontre em um sistema de arquivos diferente daquele argumentado.|

4. **`mv` --> __Permite__ mover e __Renomear__ arquivos.**
5. **`cp` --> Permite efetuar cópias de arqivos e diretórios.**
6. **`ln` --> Permite efetuar lincagens de arquivos, criando um novo arquivo com o nome escolhido e lincado com o arquivo original, toda modificação feita em um rflete no outro.**

|Argumentos|Objetivos|
|--------|----|
|`ln '<file>' '<link>'`| `'<file>'` é o arquivo original e `'<link>'` é o nome do arquivo link que será criadao idêntico ao original|
|`ln -f '<file>' '<link>'`|`-f` é para forçar, mesmo que exista na pasta um arquivo com o memo nome do link que se deseja criar|
|`ln -d '<file>' '<link>'`|`-d` cria uma ligação direta (hard link), é o padrão.|
|`ln -L '<file>' '<link>'` ou `ln -logical '<file>' '<link>'`|`-L` ou `-logical` cria uma ligação para um link simbólico.|
|`ln -s '<file>' '<link>'`|`-s` cria uma ligação simbólica (soft link).|
|`ln -v '<file>' '<link>'`|`-v` mostra o nome de cada arquivo antes de criar o link.|

---

# Adicionando um diretório, temporariamente, à variável de Ambiente `PATH`

1. Exibir o conteúdo da variável `PATH`.

```shell
echo $PATH
```

2. Adicionar um diretório ao `PATH`.

```shell
export PATH=$PATH:'<path_of_dir>'
```
|Código|Significado|
|------|-----------|
|`export`|Diz ao bash para disponibilizar a variável de ambiente para um processo filho.|
|`PATH`|Informa ao bash que você está configurando a variável `$PATH`.|
|`$PATH`|Coloca o valor atual da variável `PATH` na variável recém definida.|
|`:`|É um separador ou delimitador.|
|`'<path_of_dir>'`|É o caminho que você deseja colocar na varável.|

---

# Adicionando um repositório à lista de repositórios do Debian

1. Editando o arquivo que contém a lista de repositórios:

```shell
sudo gedit /etc/apt/sources.list
```

2. Ao abrir basta adicionar o link do novo repositório e em seguida salvar, fechar o arquivo e por fim atualizar os repositórios via Terminal:

```shell
sudo apt update && sudo apt upgrade
```
----

# Comando para dar permissão de Executável ao arquivo

```shell
chmod +x '<file_name>'
```
---

# Compactar arquivos pelo Terminal

- Apenas Juntar os arquivos (`.tar`)
   - Este é um dos métodos mais rápidos para juntar vários arquivos dentro de um único container, porém, sem compressão.
   - Lembre-se do seguinte, o `-c` significa “criate”, porque você está pegando uma pasta ou vários arquivos e jogando dentro de um único pacote. Quando você for separar tais arquivos ou pastas, irá utilizar `-x` (essa é a única diferença entre juntar e separar arquivos).

|Objetivo| Código|
|-----|-----|
|Juntar|`tar -cvf unico.tar pasta/`|
|Listar|`tar -tvf unico.tar`|
|Juntar Separadamente|`tar -cvf unico.tar arquivo1 arquivo2 arquivo3`|
|Separar por pasta|`tar -xvf unico.tar -C caminho/da/pasta/`|

- Juntar Compactando os arquivos (`.tar.gz`)
   - Este é o método de compactação gzip (`.gz`), não consome tanto processamento e tem um fator de compressão muito bom.
   - Apenas adicione um `-z` no comando e a extensão `.gz`, já estará comprimindo os arquivos.

|Objetivo| Código|
|-----|-----|
|Compactar|`tar -zcvf compactada.tar.gz pasta/`|
|Listar|`tar -ztvf compactada.tar.gz`|
|Compactar Separadamente|`tar -zcvf compactada.tar.gz pasta/arquivos-{1,2}.txt outra-coisa/`|

- Juntar Compactando os arquivos (`.tar.bz2`)
   - Este é o `bzip2`, apesar de utilizar mais recursos do computador, tem um fato de compressão excelente

|Objetivo| Código|
|-----|-----|
|Compactar|`tar -jcvf compactada.tar.bz2 pasta/`|
|Listar|`tar -jtvf compactada.tar.bz2`|
|Compactar Separadamente|`tar -jcvf compactada.tar.bz2 pasta/arquivo-{1,2}.txt`|

- Compactar e Descompactar Arquivos (`.zip`)
   - ZIP é um formato bastante conhecido por usuários Windows, tanto que você pode compactar e descompactar pastas no sistema da Microsoft sem instalar nada caso tal arquivo esteja no formato `.zip`.
   - Muitas versões do Linux já trazem o `zip` e `unzip` instalados, mas caso precise instalar manualmente, utilize o gerenciador de pacotes da seguinte maneira:

```shell
sudo apt install zip unzip
```

   - Para compactar e descompactar arquivos `.zip`, siga as instruções abaixo:

|Objetivo| Código|
|-----|-----|
|Compactar|`zip -r compactada.zip pasta/`|
|Descompactar|`unzip compactada.zip`|
|Listar|`unzip -l compactada.zip`|
|Compactar Separadamente|`zip compactada.zip pasta/arquivo-{1,2,3}.txt`|
|Descompactar para pasta|`unzip compactada.zip -d caminho/`|
|Compactar com Senha|`zip -P senha -r compactada.zip pasta/`|

- Compactar e descompactar arquivos (`.rar`)
   - Se você estiver lidando com o formato `RAR`, é praticamente certeza de que este pacote veio de um Windows. De qualquer maneira, existe a possibilidade de utilizar `rar` e `unrar` no Linux também. Mas será necessário instalar esses pacotes.
   - Pra realizar a instalação:

```shell
sudo apt install rar unrar
```

   - Para utilizar rar e unrar, siga os passos abaixo:

|Objetivo| Código|
|-----|-----|
|Compactar|`rar a compactada.rar pasta/`|
|Descompactar|`unrar x compactada.rar`|
|Listar|`unrar l compactada.rar`|
|Compactar Separadamente|`rar a compactada.rar pasta/arquivo-{1,2,3}.txt`|
|Descompactar para Pasta|`unrar x compactada.rar caminho/`
|Compactar com Senha|`rar a compactada.rar pasta/ -p`|

---

# Configurações Avançadas do Linux.

1. Editar a lista que contém os links dos repositórios do Sistema Operacional:

```shell
sudo gedit /etc/apt/source.list
```

2. Sincronizar a lista de repositórios com os dados do Sistema Operacional:

```shell
sudo apt update
```

3. Atualisar pacotes:

```shell
sudo apt upgrade
```

4. Atualisar elementos da distribuição do Sistema Operacional:

```shell
sudo apt dist-upgrade
```

4. Remover pacotes quebrados ou pacotes que não estão mais em uso:

```shell
sudo apt autoremove
```

---

# Como descompactar os tipos de arquivos: .zip, .rar, tar.gz, bz2, tar.bz2. pelo Terminal

- `.zip`

```shell
unzip '<name_file.zip>'
```
---

- `.rar`

```shell
unrar x '<name_file.rar>'
```
---

- `.tar`

```shell
tar -xvf '<name_file.tar>'
```
---

- `.tar.gz`

```shell
tar -vzxf '<name_file.tar.gz>'
```
---

- `.bz2`

```shell
bunzip '<name_file.bz2>'
```
---

- `.tar.bz2`

```shell
tar -jxvf '<name_file.tar.bz2>'
```
---

# Montar unidades removíveis através do Terminal

1. Abra um Terminal:

> `Ctrl + Alt + T`

2. Entre no modo `root` no Terminal:

```shell
su
```

3. Navegue ate a pasta em que deseja criar a raiz da unidade:

```shell
cd /media/ronivaldo
```

4. Crie dentro dela uma pasta onde será a raiz da unidade montada:

```shell
mkdir ronivaldo.DESKTOP
```

5. Agora com o `fdisk` iremos localizar a unidade a ser montada:

```shell
sudo fdisk -l
```

6. Após achar a unidade desejada e saber seu `Device` (caminho virtual), podemos montar ela no ambiente físico:

```shell
mount /dev/sda5 ronivaldo.DESKTOP
```
# Para desmontar a unidade que acabamos de montar

1. Ainda no mesmo lugar que estávamos para montar, fazemos:

```shell
umount /dev/sda5
```

---
