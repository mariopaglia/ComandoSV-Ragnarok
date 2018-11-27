#!/usr/bin/env bash
# Autor: Mário Augusto Paglia Júnior < https://pagliahost.com.br >
#
# Descrição: Comando "SV" para Ragnarok é um comando para ligar, desligar, compilar, baixar emuladores, realizar edições e muito mais!
#
# Versões:
#
# 1.0 - 2016 ou anterior - Criação do script pelo Rhúlio Victor, Carlos Lain e Alexandre Leigo
# 2.0 - 26/07/2017 - Reformulação completa do script realizado por Mário Augusto em 2017
# 2.1 - 01/08/2017 - Correção e Adição de Novas Funções
# 2.2 - 07/08/2017 - Adição do comando compilar-cmake para compilação via CMAKE
# 2.3 - 25/08/2017 - Adição do comando SV Status, verificando se o servidor está online nos processos
# 2.4 - 28/08/2017 - Adição dos comandos SV PREPARAR-RATHENA e SV COMPILAR-RATHENA especificos para preparação e compilação do emulador rAthena
# 2.5 - 26/09/2017 - Adição do comando SV COMPILAR-RATHENA2 onde é instalado o compilador GCC 5.3 para os emuladores rAthena atuais
# 2.6 - 30/09/2017 - Adição do comando SV COMPILAR-EAMOD, para compilar emuladores eAmod
# 2.7 - 26/10/2017 - Melhoria e correção da listagem e descrição dos comandos através do comando principal "sv comandos"
# 2.8 - 13/11/2017 - Melhoria do comando SV-STATUS, mostrando cores e a informação escrita se o emulador está ligado ou desligado
# 2.9 - 07/02/2018 - Adição da função de verificar se o emulador está ligado para evitar ligar 2x o mesmo processo
# 3.0 - 07/02/2018 - Adição da função de desligar forçadamente o emulador caso ele fique com processo preso, melhoria no visual do código
# 3.1 - 13/03/2018 - Melhoria na indentação do código
# 3.2 - 21/03/2018 - Alterado os comandos de backups para usar o comando ZIP ao invés do RAR (melhoria na compactação/descompactação)
# 3.3 - 05/04/2018 - Ajustado case "ligar" para fazer diversas verificações antes de tentar ligar o emulador e otimização da explicação dos comandos gerais no 'sv (*)'
# 3.4 - 10/04/2018 - Arrumado o BUG no comando "sv ligar" que fazia com que o MYSQL não reconhecesse as tabelas, retirado os fechamentos de saídas de erros
# 3.5 - 31/07/2018 - Adicionado função para importar automaticamente banco de dados de acordo com o emulador baixado no "sv baixar-emulador"
# 3.6 - 24/10/2018 - Adicionado função para instalar brAthena Old
# 3.7 - 29/10/2018 - Otimização e melhorias no código para melhor portabilidade, adição do comando "SV EDITAR" e implementação da primeira função de troca de IP

# Variáveis de Ambiente - Modificáveis

EMULADOR=/home/emulador           # Coloque aqui o diretório raiz do seu emulador
BANCO=/var/lib/phpMyAdmin/upload/ # Coloque aqui o diretório de upload do seu phpMyAdmin

# ATENÇÃO: À PARTIR DAQUI, NÃO MEXA EM NADA, À NÃO SER QUE SAIBA O QUE ESTEJA FAZENDO!

VERIFICA_PROCESSOS=$(ps aux | grep -E "map-server|login-server|char-server" | grep -v grep | wc -l)
export COMANDO=$1

importarDB() {

	echo
	read -p "Deseja realizar a importação do banco de dados de forma automática? (S/N): " IMPORTAR

	if [ $IMPORTAR = "n" ] || [ $IMPORTAR = "N" ]; then
		exit 1
	else
		echo
		echo "Cancele à qualquer momento apertando CTRL + C"
	fi

	echo
	echo "Iniciando importação do banco de dados..."
	echo
	read -p "Digite o usuário do MYSQL (phpMyAdmin): " USUARIO_MYSQL
	read -p "Digite a senha do MYSQL (phpMyAdmin): " SENHA_MYSQL

	mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL -e "show databases" >/dev/null

	if [ $? = 0 ]; then # SE FOR IGUAL "0" É PORQUE SE CONECTOU AO BANCO DE DADOS

		echo
		echo "Conexão realizada com sucesso, vamos prosseguir..."

		echo
		read -p "Digite o nome do banco de dados (se não existir, será criado): " BANCO_MYSQL

		mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL -e "CREATE DATABASE $BANCO_MYSQL" >/dev/null

		if [ $? = 1 ]; then
			echo
			echo "O banco de dados '$BANCO_MYSQL' já existe, vamos prosseguir..."
		else
			echo
			echo "O banco de dados '$BANCO_MYSQL' foi criado com sucesso, vamos prosseguir..."
		fi

		echo
		read -p "Seu emulador é RENOVAÇÃO ou PRÉ-RENOVAÇÃO? Digite 1 para RENOVAÇÃO ou 2 para PRÉ-RENOVAÇÃO: " CLASSE

		if [ $CLASSE -eq 1 ]; then # RENOVAÇÃO

			case $COMANDO in
			'baixar-cronus')
				cd /home/emulador/sql-files

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <main.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <logs.sql

				cd /home/emulador/sql-files/item

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_db_re.sql

				cd /home/emulador/sql-files/mob

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_db_re.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_skill_db_re.sql

				echo
				echo "Importação realizada com sucesso, configure em seu 'inter-server.conf' o nome do banco de dados '$BANCO_MYSQL'"
				;;

			'baixar-brathena')
				cd /home/emulador/sql-files

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <main.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <logs.sql

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_db_re.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_db_re.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_skill_db_re.sql

				echo
				echo "Importação realizada com sucesso, configure em seu 'sql_connection.conf' o nome do banco de dados '$BANCO_MYSQL'"
				;;

			'baixar-brathena-old')
				cd /home/emulador/sql

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <principal.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <logs.sql

				cd /home/emulador/sql/pre-renovacao

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <pre-renovacao.sql

				echo
				echo "Importação realizada com sucesso, configure em seu 'sql_connection.conf' o nome do banco de dados '$BANCO_MYSQL'"
				;;

			'baixar-hercules')
				cd /home/emulador/sql-files

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <main.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <logs.sql

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_db_re.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_db_re.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_skill_db_re.sql

				echo
				echo "Importação realizada com sucesso, configure em seu 'sql_connection.conf' o nome do banco de dados '$BANCO_MYSQL'"
				;;

			'baixar-rathena')
				cd /home/emulador/sql-files

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <main.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <logs.sql

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_db_re.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_db2_re.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_db_re.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_db2_re.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_skill_db_re.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_skill_db2_re.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <roulette_default_data.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_cash_db.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_cash_db2.sql

				echo
				echo "Importação realizada com sucesso, configure em seu 'inter_athena.conf' o nome do banco de dados '$BANCO_MYSQL'"
				;;
			esac

		elif [ $CLASSE -eq 2 ]; then # PRÉ-RENOVAÇÃO

			case $COMANDO in
			'baixar-cronus')
				cd /home/emulador/sql-files

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <main.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <logs.sql

				cd /home/emulador/sql-files/item

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_db.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_db2.sql

				cd /home/emulador/sql-files/mob

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_db.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_db2.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_skill_db.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_skill_db2.sql

				echo
				echo "Importação realizada com sucesso, configure em seu 'inter-server.conf' o nome do banco de dados '$BANCO_MYSQL'"
				;;

			'baixar-brathena')
				cd /home/emulador/sql-files

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <main.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <logs.sql

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_db.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_db2.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_db.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_db2.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_skill_db.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_skill_db2.sql

				echo
				echo "Importação realizada com sucesso, configure em seu 'sql_connection.conf' o nome do banco de dados '$BANCO_MYSQL'"
				;;

			'baixar-brathena-old')
				cd /home/emulador/sql

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <principal.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <logs.sql

				cd /home/emulador/sql/renovacao

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <renovacao.sql

				echo
				echo "Importação realizada com sucesso, configure em seu 'sql_connection.conf' o nome do banco de dados '$BANCO_MYSQL'"
				;;

			'baixar-hercules')
				cd /home/emulador/sql-files

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <main.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <logs.sql

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_db.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_db2.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_db.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_db2.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_skill_db.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_skill_db2.sql

				echo
				echo "Importação realizada com sucesso, configure em seu 'sql_connection.conf' o nome do banco de dados '$BANCO_MYSQL'"
				;;

			'baixar-rathena')
				cd /home/emulador/sql-files

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <main.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <logs.sql

				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_db.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_db2.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_db.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_db2.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_skill_db.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <mob_skill_db2.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <roulette_default_data.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_cash_db.sql
				mysql -u $USUARIO_MYSQL -p$SENHA_MYSQL $BANCO_MYSQL <item_cash_db2.sql

				echo
				echo "Importação realizada com sucesso, configure em seu 'inter_athena.conf' o nome do banco de dados '$BANCO_MYSQL'"
				;;
			esac

		else
			echo
			echo "Número não reconhecido. Digite 1 ou 2, tente novamente, use o comando '"$0" importar-db'"
			echo
		fi

	else
		echo
		echo "Usuário ou Senha informados não existem, tente novamente, use o comando '"$0" importar-db'"
		echo

	fi # VERIFICA SE A CONEXÃO DO BANCO DE DADOS É REALIZADA

}

case $1 in

'ligar')

	if [[ -d $EMULADOR ]]; then

		if [[ "$VERIFICA_PROCESSOS" -ge "1" ]]; then
			echo
			echo "PRIMEIRAMENTE DESLIGUE O SEU EMULADOR COM '"$0" desligar' ANTES DE LIGAR NOVAMENTE"
			echo
		else

			if [[ -x $EMULADOR/login-server || -x $EMULADOR/char-server || -x $EMULADOR/map-server || -x $EMULADOR/loginserv || -x $EMULADOR/charserv || -x $EMULADOR/mapserv || -x $EMULADOR/login-server_sql || -x $EMULADOR/char-server_sql || -x $EMULADOR/map-server_sql ]]; then

				cd $EMULADOR
				exec ./login-server &
				exec ./char-server &
				exec ./map-server &
				exec ./loginserv &
				exec ./charserv &
				exec ./mapserv &
				exec ./login-server_sql &
				exec ./char-server_sql &
				exec ./map-server_sql &
			else
				echo
				echo "OS ARQUIVOS DO SEU EMULADOR DENTRO DE $EMULADOR NÃO EXISTEM OU NECESSITAM DE PERMISSÕES, USE '"$0" preparar' E DEPOIS COMPILE SEU EMULADOR"
				echo
			fi
		fi
	else
		echo
		echo "O DIRETÓRIO $EMULADOR AINDA NÃO EXISTE"
		echo
	fi
	;;

'desligar')
	ps ax | grep -E "login-server|char-server|map-server" | awk '{print $1}' | xargs kill
	sleep 1
	echo
	echo "AGUARDE 2 SEGUNDOS..."
	sleep 1
	echo "AGUARDE 1 SEGUNDO..."
	sleep 1

	VERIFICA_PROCESSOS2=$(ps aux | grep -E "map-server|login-server|char-server" | grep -v grep | wc -l)

	if [ "$VERIFICA_PROCESSOS2" -eq "0" ]; then
		echo
	else
		ps ax | grep -E "login-server|char-server|map-server" | awk '{print $1}' | xargs kill -9
	fi
	echo
	echo "O SEU EMULADOR FOI DESLIGADO COM SUCESSO!"
	echo
	;;

'compilar' | 'compilar-autoconf')
	cd /home/emulador
	make clean
	make sql
	;;

'compilar-cmake')
	cd /home/emulador
	cmake .
	make
	;;

'screen')
	screen -S ragnarok
	;;

'retornar')
	screen -r ragnarok
	;;

'status')
	ps aux | grep -E "map-server|login-server|char-server" | grep -v grep

	STATUS=$(ps aux | grep -E "map-server|login-server|char-server" | grep -v grep | wc -l)

	if [ "$STATUS" = "3" ]; then
		echo
		echo -e "O SEU EMULADOR ESTÁ \e[00;32mLIGADO\e[00m NO MOMENTO!"
		echo
	elif [ "$STATUS" = "2" ] || [ "$STATUS" = "1" ]; then
		echo
		echo -e "O SEU EMULADOR ESTÁ \e[00;32mLIGADO\e[00m NO MOMENTO, PORÉM COM UM DOS PROCESSOS DESLIGADOS, NECESSÁRIO SUA ATENÇÃO!"
		echo
	else
		echo
		echo -e "O SEU EMULADOR ESTÁ \e[00;31mDESLIGADO\e[00m NO MOMENTO!"
		echo
	fi
	;;

'preparar')
	cd $EMULADOR
	chmod 777 configure
	./configure
	echo "As permissões foram preparadas com sucesso!"
	;;

'preparar-rathena')
	wget http://people.centos.org/tru/devtools-2/devtools-2.repo -O /etc/yum.repos.d/devtools-2.repo && yum -y install devtoolset-2-gcc devtoolset-2-binutils devtoolset-2-gcc-c++ devtoolset-2-gcc-gfortran

	source scl_source enable devtoolset-2

	if [ "$?" = "0" ]; then
		source /opt/rh/devtoolset-2/enable
		sv preparar-rathena2
	else
		echo
		echo "COMANDO DE PREPARAÇÃO NÃO CONSEGUIU SER CONCLUÍDO COM SUCESSO!"
		echo
	fi
	;;

'preparar-rathena2')
	cd /etc/yum.repos.d/ && wget https://copr.fedorainfracloud.org/coprs/mlampe/devtoolset-4.1/repo/epel-6/mlampe-devtoolset-4.1-epel-6.repo && yum -y install devtoolset-4-toolchain

	USUARIO=$(cat /usr/bin/usuario)

	echo "source scl_source enable devtoolset-4" >>/home/$USUARIO/.bashrc
	chown -R $USUARIO /var/lib/phpMyAdmin/upload/

	echo
	echo "A SUA VPS ESTÁ PREPARADA COM SUCESSO PARA RECEBER O RATHENA!"
	echo
	;;

'compilar-rathena')
	cd /home/emulador
	./configure --disable-64bit
	make clean
	make server
	;;

'compilar-rathena2')
	cd /home/emulador
	./configure
	make clean
	make server
	;;

'compilar-eamod')
	cd /home/emulador
	make clean
	make sql
	make sql
	;;

'backup')
	cd /home
	zip -r backup_$(date +%d_%m_%y_%H_%M).zip emulador
	mkdir backup
	mv backup_$(date +%d_%m_%y_%H_%M).zip /home/backup
	;;

'antigo')
	cd /home
	zip -r emulador_antigo_$(date +%d_%m_%y).zip emulador
	mkdir backup
	mv emulador_antigo_$(date +%d_%m_%y).zip /home/backup
	;;

'baixar-emulador')
	echo "Para baixar um emulador, use um dos seguintes comandos: sv baixar-cronus | sv baixar-brathena | sv baixar-hercules | sv baixar-rathena"
	;;

'baixar-cronus')
	cd /home
	sv antigo
	rm -rf emulador
	mkdir emulador
	svn co https://github.com/Cronus-Emulator/Cronus/trunk emulador
	echo "O seu emulador foi baixado com sucesso e se encontra dentro de /home/emulador"
	rm -rf $BANCO*
	cd /home/emulador/sql-files
	cp main.sql logs.sql $BANCO
	cd /home/emulador/sql-files/item
	cp item_db.sql item_db2.sql item_db_re.sql $BANCO
	cd /home/emulador/sql-files/mob
	cp mob_db.sql mob_db2.sql mob_db_re.sql mob_skill_db.sql mob_skill_db2.sql mob_skill_db_re.sql $BANCO
	sv preparar
	importarDB
	;;

'baixar-brathena')
	cd /home
	sv antigo
	rm -rf emulador
	mkdir emulador
	svn co https://github.com/brAthena/brAthena/trunk emulador
	echo "O seu emulador foi baixado com sucesso e se encontra dentro de /home/emulador"
	rm -rf $BANCO*
	cd /home/emulador/sql-files/
	cp *.sql $BANCO
	sv preparar
	importarDB
	;;

'baixar-brathena-old')
	cd /home
	sv antigo
	rm -rf emulador
	mkdir emulador
	svn co https://github.com/brAthena/brAthena20180924/trunk emulador
	echo "O seu emulador foi baixado com sucesso e se encontra dentro de /home/emulador"
	rm -rf $BANCO*
	cd /home/emulador/sql-files/
	cp *.sql $BANCO
	sv preparar
	importarDB
	;;

'baixar-hercules')
	cd /home
	sv antigo
	rm -rf emulador
	svn co https://github.com/HerculesWS/Hercules/trunk emulador
	echo "O seu emulador foi baixado com sucesso e se encontra dentro de /home/emulador"
	rm -rf $BANCO*
	cd /home/emulador/sql-files/
	cp *.sql $BANCO
	sv preparar
	importarDB
	;;

'baixar-rathena')
	cd /home
	sv antigo
	rm -rf emulador
	mkdir emulador
	svn co https://github.com/rathena/rathena/trunk emulador
	echo "O seu emulador foi baixado com sucesso e se encontra dentro de /home/emulador"
	rm -rf $BANCO*
	cd /home/emulador/sql-files
	cp item_cash_db.sql item_cash_db2.sql item_db.sql item_db2.sql item_db2_re.sql item_db_re.sql logs.sql main.sql mob_db.sql mob_db2.sql mob_db2_re.sql mob_db_re.sql mob_skill_db.sql mob_skill_db2.sql mob_skill_db2_re.sql mob_skill_db_re.sql roulette_default_data.sql $BANCO
	sv preparar
	importarDB
	;;

'importar-db')
	importarDB
	;;

'editar')

	# Verifica o nome do emulador utilizado no momento, se é Hércules ou rAthena
	NOME_EMULADOR=$(ls -l $EMULADOR | awk '{print $9}' | cut -d "-" -f1 | cut -d "." -f1 | uniq | grep -E "Hercules|rAthena" | head -n 1)

	PS3="Selecione o que deseja editar em seu emulador: "
	select menu_editar in "IP" "Nome" "Rates" "Level" "Drops" "Configuração Renovação" "Configuração Pré-Renovação" "Sair/Encerrar"; do
		case "$menu_editar" in

		'IP')

			if [[ "$NOME_EMULADOR" == "Hercules" ]] || [[ "$NOME_EMULADOR" == "brAthena" ]]; then

				# Descobrir o IP atual do Hércules
				IP_ATUAL=$(cat $EMULADOR/conf/char/char-server.conf | grep "login_ip:" | cut -d "\"" -f2)

				echo
				read -p "O IP configurado atualmente é '$IP_ATUAL', deseja alterar? (S/N) " DESEJA_ALTERAR

				if [[ "$DESEJA_ALTERAR" == "S" ]] || [[ "$DESEJA_ALTERAR" == "s" ]]; then
					echo
					read -p "Informe número do novo IP: " NOVO_IP
					echo

					sed -i 's/"'$IP_ATUAL'"/"'$NOVO_IP'"/' $EMULADOR/conf/char/char-server.conf
					sed -i 's/"'$IP_ATUAL'"/"'$NOVO_IP'"/' $EMULADOR/conf/map/map-server.conf

					if [[ "$?" == 0 ]]; then
						echo
						echo "IP alterado com sucesso!"
						echo
					else
						echo
						echo "Falha na troca do IP!"
						echo
					fi

					# Verifica se "login_ip", "char_ip" e "map_ip" estão com comentário //, se estiver, remove

					if [ "cat $EMULADOR/conf/char/char-server.conf | grep '//login_ip:' > /dev/null" ]; then
						sed -i 's/\/\/login_ip:/login_ip:/' $EMULADOR/conf/char/char-server.conf
					fi

					if [ "cat $EMULADOR/conf/char/char-server.conf | grep '//char_ip:' > /dev/null" ]; then
						sed -i 's/\/\/char_ip:/char_ip:/' $EMULADOR/conf/char/char-server.conf
						sed -i 's/\/\/char_ip:/char_ip:/' $EMULADOR/conf/map/map-server.conf
					fi

					if [ "cat $EMULADOR/conf/char/map-server.conf | grep '//map_ip:' > /dev/null" ]; then
						sed -i 's/\/\/map_ip:/map_ip:/' $EMULADOR/conf/map/map-server.conf
					fi
				else
					exit 0
				fi # Fim do segundo IF

			elif [[ "$NOME_EMULADOR" == "rAthena" ]]; then

				# Descobrir o IP atual do rAthena

				IP_ATUAL=$(cat $EMULADOR/conf/char_athena.conf | grep "login_ip:" | cut -d " " -f2)

				echo
				read -p "O IP configurado atualmente é '$IP_ATUAL', deseja alterar? (S/N) " DESEJA_ALTERAR

				if [[ "$DESEJA_ALTERAR" == "S" ]] || [[ "$DESEJA_ALTERAR" == "s" ]]; then
					echo
					read -p "Informe número do novo IP: " NOVO_IP
					echo

					sed -i 's/'$IP_ATUAL'/'$NOVO_IP'/' $EMULADOR/conf/char_athena.conf
					sed -i 's/'$IP_ATUAL'/'$NOVO_IP'/' $EMULADOR/conf/map_athena.conf

					if [[ "$?" == 0 ]]; then
						echo
						echo "IP alterado com sucesso!"
						echo
					else
						echo
						echo "Falha na troca do IP!"
						echo
					fi

					# Verifica se "login_ip", "char_ip" e "map_ip" estão com comentário //, se estiver, remove

					if [ "cat $EMULADOR/conf/char_athena.conf | grep '//login_ip:' > /dev/null" ]; then
						sed -i 's/\/\/login_ip:/login_ip:/' $EMULADOR/conf/char_athena.conf
					fi

					if [ "cat $EMULADOR/conf/char_athena.conf | grep '//char_ip:' > /dev/null" ]; then
						sed -i 's/\/\/char_ip:/char_ip:/' $EMULADOR/conf/char_athena.conf
						sed -i 's/\/\/char_ip:/char_ip:/' $EMULADOR/conf/map_athena.conf
					fi

					if [ "cat $EMULADOR/conf/map_athena.conf | grep '//map_ip:' > /dev/null" ]; then
						sed -i 's/\/\/map_ip:/map_ip:/' $EMULADOR/conf/map_athena.conf
					fi
				else
					exit 0
				fi # Fim do IF "Deseja continuar" do emulador rAthena

			else
				echo "Não é o Hércules, ajuste!"
			fi # Fim do primeiro IF

			;;

		'Nome')
			echo "Função '"$menu_editar"' em construção!"
			;;

		'Rates')
			echo "Função '"$menu_editar"' em construção!"
			;;

		'Level')
			echo "Função '"$menu_editar"' em construção!"
			;;

		'Drops')
			echo "Função '"$menu_editar"' em construção!"
			;;

		'Configuração Renovação')
			echo "Função '"$menu_editar"' em construção!"
			;;

		'Configuração Pré-Renovação')
			echo "Função '"$menu_editar"' em construção!"
			;;

		'Sair/Encerrar')
			exit 0
			;;
		esac
	done
	;;

*)
	cat <<EOF

Os comandos válidos são:

sv ligar - Liga o emulador (brAthena/Cronus/Hércules/rAthena/eAmods)
sv desligar - Desliga o emulador (brAthena/Cronus/Hércules/rAthena/eAmods)
sv compilar - Compila o emulador (brAthena/Cronus/Hércules)
sv compilar-rathena - Comando especialmente criado para compilar emuladores rAthena (GCC-C++ versão 5.X)
sv compilar-eamod - Comando especialmente criado para compilar emuladores eAmod
sv editar - Realiza edição dos emuladores Hércules e rAthena como "nome, rates, drops, level, etc
sv status - Verifica se o emulador está com seus processos ligados ou desligados
sv compilar-cmake - Compilar emulador com CMAKE (emuladores específicos)
sv screen - Roda o emulador em segundo plano com o Screen
sv retornar - Retorna à tela do Screen nos demais acessos ao SSH
sv preparar - Dá as permissões iniciais ao emulador (chmod 777 configure e ./configure)
sv backup - Cria um backup e um arquivo .zip da pasta /home/emulador em /home/backup
sv baixar-emulador - Baixar emuladores diretamente dos repositórios oficiais do GitHub (brAthena/Cronus/Hércules/rAthena)
sv importar-db - Importa automaticamente o banco de dados (necessário ter feito o sv baixar-emulador)

Para utilizar os comandos, basta digitar em qualquer tela do seu SSH.

Lembre-se de que seu emulador precisa ser instalado dentro de $EMULADOR para o correto funcionamento dos comandos.

EOF
	;;
esac
