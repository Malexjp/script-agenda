#!/bin/bash
# script-agenda

nomes=( )
telefones=( )

saida1="nao"
until [ $saida1 = "sim" ]
do

clear
echo "Bem vindo a sua agenda"
echo "Escolha uma das opções abaixo:"
echo #Pular linha
echo "[1] Cadastrar contato"
echo "[2] Buscar contato"
echo "[3] Listar contato"
echo "[4] Sair"
read opcao


case $opcao in
	1)
	cadastro="nao"	
	until [ $cadastro = "sim" ]
	do	
		clear		
		echo "Cadastro de contatos"		
		echo		
		echo "[1] Cadastrar um contato"
		echo "[2] Sair"	
		read cadastrar
		
		if [ $cadastrar -eq 1 ]
		then
			saida="nao"
			while [ $saida = "nao" ]
			do
				echo "Digite o nome do contato: "
				read name
				echo "Digite o telefone do contato: "
				read phone
				if [ -z $name ] || [ -z $phone ]; #Verifica se as variaveis sao nulas
				then
					echo "Campos obrigatórios, digite novamente."
				else
					nomes+=( "$name" )
					telefones+=( "$phone" )
					saida="sim"
					echo "Cadastro realizado com sucesso."
				fi
			done
		elif [ $cadastrar -eq 2 ]
		then
			cadastro="sim"
		else
			clear			
			echo "Escolha uma das opções"
			echo
		fi
	done ;;

	2)
	busca="nao"
	until [ $busca = "sim" ]
	do	
		echo "Buscar contatos"
		echo
		echo "[1] Buscar por nome"
		echo "[2] Buscar por telefone"
		echo "[3] Sair"
		echo -n "Escolha uma das opções: "
		read opt1
	
		existenome="nada"
		existephone="nada"	
		if [ $opt1 -eq 1 ]; #Efetua busca por nome
		then
			echo -n "Digite o nome para busca: "		
			read nome_busca
			for (( count = 0; count <= ${#nomes[@]}; count++ ))
			do
				if [ "$nome_busca" = "${nomes[count]}" ]
				then
					existenome=${nomes[count]}
					existephone=${telefones[count]}
				fi
				
			done
			# Caso encontre o contato, exibe na tela
			if [ $existenome = "nada" ] && [ $existephone = "nada" ]
			then
				echo "Contado não encontrado "
				echo

			else
				echo "Contato encontrado"
				echo $existenome
				echo $existephone
				echo
			fi
	
		elif [ $opt1 -eq 2 ] #Efetua busca por telefone
		then
			echo -n "Digite o telefone para busca: "		
			read phone1
			for (( count = 0; count <= ${#telefones[@]}; count++  ))
			do
				
				if [ "$phone1" = "${telefones[count]}" ]
				then
					existenome=${nomes[count]}
					existephone=${telefones[count]}
				fi
			done
			# Caso encontre o contato, exibe na tela
			if [ $existenome = "nada" ] && [ $existephone = "nada" ]
			then
				echo "Contado não encontrado "
				echo
				
			else
				echo "Contato encontrado"
				echo $existenome
				echo $existephone
				echo
			fi
		
		elif [ $opt1 -eq 3 ] # Sai da opção escolhida
		then
			busca="sim"
		
		else #Repete caso a opção seja inválida
			echo "Opção inválida, escolha uma das opções abaixo"
			echo
		fi
	done ;;
	
	3)
	outlist3="nao"
	until [ $outlist3 = "sim" ]
	do
		echo "Listagem de contatos"
		echo
		echo "[1] Listar os contatos"
		echo "[2] Sair"
		read optlist3		
		
		if [ $optlist3 -eq 1 ]
		then
			count=0			
			for contato in ${nomes[*]};
			do
								
				echo				
				echo $contato
				echo ${telefones[count]}
				(( count+=1 ))
			done
			echo # Pula linha no final da listagem
		
		elif [ $optlist3 -eq 2 ]
		then
			outlist3="sim"

		else
			echo "Opção inválida. Digite uma das opções"
			echo
		fi
	done ;;
				



	4)
		saida1="sim";;
esac
done
