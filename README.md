### Versão em inglês / English version: [Clique aqui / Click here](https://github.com/agenciah1code/ComandoSV-Ragnarok/blob/master/README-EN.md)

# História do Projeto

O comando "SV" para Ragnarok foi criado em 2016 ou anteriormente por **Rhúlio Victor**, **Carlos Lain** e **Alexandre Leigo** em sua  [Versão 1.0](https://github.com/agenciah1code/ComandoSV-Ragnarok/tree/v1.0), em 2017 foi reformulado por **Mário Augusto Paglia** em sua [Versão 2.0](https://github.com/agenciah1code/ComandoSV-Ragnarok/tree/v2.0) e em Outubro/2018 retornado como Open Source.

## Informações Técnicas

* **Versão atual:** [3.6](https://github.com/agenciah1code/ComandoSV-Ragnarok/tree/master)
* **Sistemas Operacional:** Linux 
* **Distribuições:** Testado e criado em CentOS 6.  

[![GitHub issues](https://img.shields.io/github/issues/agenciah1code/ComandoSV-Ragnarok.svg)](https://github.com/agenciah1code/ComandoSV-Ragnarok/issues)
[![GitHub forks](https://img.shields.io/github/forks/agenciah1code/ComandoSV-Ragnarok.svg)](https://github.com/agenciah1code/ComandoSV-Ragnarok/network)
[![GitHub stars](https://img.shields.io/github/stars/agenciah1code/ComandoSV-Ragnarok.svg)](https://github.com/agenciah1code/ComandoSV-Ragnarok/stargazers)
[![GitHub license](https://img.shields.io/github/license/agenciah1code/ComandoSV-Ragnarok.svg)](https://github.com/agenciah1code/ComandoSV-Ragnarok/blob/master/LICENSE)

## Funções Disponíveis

Até a presente versão, estão disponíveis as seguintes funções:

* **sv ligar** - Liga o emulador (brAthena/Cronus/Hércules/rAthena/eAmods)
* **sv desligar** - Desliga o emulador (brAthena/Cronus/Hércules/rAthena/eAmods)
* **sv compilar** - Compila o emulador (brAthena/Cronus/Hércules)
* **sv compilar-cmake** - Compilar emulador com CMAKE (emuladores específicos)
* **sv compilar-rathena** - Comando especialmente criado para compilar emuladores rAthena (GCC-C++ versão 5.X)
* **sv status** - Verifica se o emulador está com seus processos ligados ou desligados
* **sv screen** - Roda o emulador em segundo plano com o Screen **(POSSIVELMENTE SERÁ DESCONTINUADA)**
* **sv retornar** - Retorna à tela do Screen nos demais acessos ao SSH **(POSSIVELMENTE SERÁ DESCONTINUADA)**
* **sv preparar** - Dá as permissões iniciais ao emulador (chmod 777 configure e ./configure)
* **sv backup** - Cria um backup e um arquivo .zip da pasta /home/emulador em /home/backup
* **sv baixar-emulador** - Baixar emuladores diretamente dos repositórios oficiais do GitHub (brAthena/Cronus/Hércules/rAthena)
* * **sv baixar-brathena** - Baixa o emulador brAthena no [repositório oficial](https://github.com/brAthena/brAthena)
* * **sv baixar-brathena-old** - Baixa o emulador brAthena (Versão 24/09/2018) no [repositório oficial](https://github.com/brAthena/brAthena20180924)
* * **sv baixar-cronus** - Baixa o emulador Cronus no [repositório oficial](https://github.com/Cronus-Emulator/Cronus)
* * **sv baixar-hercules** - Baixa o emulador Hércules no [repositório oficial](https://github.com/HerculesWS/Hercules/)
* * **sv baixar-rathena** - Baixa o emulador rAthena no [repositório oficial](https://github.com/rathena/rathena)
* **sv compilar-eamod** - Comando especialmente criado para compilar emuladores eAmod

## O que será implementado no futuro?

Além de correções constantes nas funções atuais, pretendemos também que o comando "SV" tenha a função de editar completamente o emulador através da linha de comando (terminal), pretendemos unificar o projeto paralelo [RagEditor - Linux](https://github.com/agenciah1code/rageditor-linux) a este projeto, fazendo com que haja uma função chamada **"sv editar"**, na qual será passado parâmetros adicionais como, por exemplo:

* **sv editar --ip** - Configurar o IP do map-server, char-server  e login-server
* **sv editar --nome** - Configurar nome do servidor no emulador 
* **sv editar --rates** - Configurar rates do emulador
* **sv editar --level** - Configurar level máximo do emulador
* **sv editar --drops** - Configurar drops do emulador
* **sv editar --re** - Configurar o emulador para Renovação
* **sv editar --pre-re** - Configurar o emulador para Pré-Renovação
* Tem sugestões? [Deixe aqui!](https://github.com/agenciah1code/ComandoSV-Ragnarok/issues)

# Como instalar?

1. [Baixe o comando SV](https://github.com/agenciah1code/ComandoSV-Ragnarok/archive/master.zip)
2. Extraia o arquivo `sv` para dentro da pasta `bin` do seu sistema Linux
3. Execute o comando `chmod +x /bin/sv`
4. Teste o funcionando digital `sv ` em seu terminal

# Agradecimentos

Pessoas que contribuíram para este projeto tornar-se possível:

* Rhúlio Victor
* Carlos Lain
* Alexandre Leigo
* Mário Augusto Paglia

## Como contribuir com o projeto?

### É programador?

1. Realize um Fork do projeto
2. Faça testes, alterações, implementações ou correções
3. Envie um Pull Request

### Não é programador?

Se você não é programador, não tem problemas, você também poderá contribuir com o projeto através [deste link.](https://github.com/agenciah1code/ComandoSV-Ragnarok/issues)