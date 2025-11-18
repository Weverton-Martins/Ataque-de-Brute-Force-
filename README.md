# Ataque-de-Brute-Force-

Este documento técnico detalha a implementação e a execução de múltiplos cenários de ataque de Força Bruta (Brute Force) de credenciais utilizando a ferramenta Medusa, nativa do Kali Linux. O objetivo é demonstrar a vulnerabilidade de serviços de rede e formulários web contra tentativas automatizadas de quebra de senhas, fornecendo subsídios para a correta documentação e recomendação de mitigação.

Os testes foram realizados em um ambiente laboratorial controlado, composto por máquinas virtuais propositalmente vulneráveis (Metasploitable 2 e DVWA - Damn Vulnerable Web Application).

Kali Linux	Máquina Atacante	[192.168.56.102]
Metasploitable 2	Alvo (FTP, SMB, DVWA)	[192.168.56.101]

Objetivo: Obter as credenciais de login para o serviço FTP (Porta 21) do Metasploitable 2.
Wordlists Utilizadas:

Usuários (user.txt): Lista simples contendo nomes de usuários comuns (ex: msfadmin, admin, user, root).
Senhas (pass.txt): Lista de senhas comuns/padrão (ex: msfadmin, password, 123456, qwerty).

Comando utilizados: medusa -H [192.168.56.101] -u msfadmin -P /home/vverto/pass.txt -M ftp -t 5
medusa -H [192.168.56.101] -u admin -P /home/vverto/pass.txt -M http -m DIR:/dvwa/login.php -T "user=^USER^&password=^PASS^&Login=Login" -e "Failed"
medusa -H [192.168.56.101] -U /home/vverto/smb_users.txt -p password -M smb
smbclient -L //[192.168.56.101]/ -U [USUARIO_DESCOBERTO]%password
