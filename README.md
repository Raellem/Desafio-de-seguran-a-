# Desafio-de-seguran-a-
Apenas uma demonstração, já que não estou usando nenhum computador e estou contando com o suporte da IA.
# =======================================================================
# SIMULAÇÃO DE ATAQUE DE DICIONÁRIO CONTRA LOGIN WEB (CONCEITUAL)
# OBJETIVO: Demonstrar a lógica do ataque de Força Bruta / Dicionário.
# =======================================================================

# 1. Variáveis de Configuração (O que seria configurado por um atacante)
# -----------------------------------------------------------------------
WORDLIST_FILE = "wordlist.txt"     # Nome do arquivo de senhas
TARGET_URL = "http://alvo-ficticio.com/login" # URL da página de login (conceitual)
TARGET_USER = "admin"              # Usuário alvo (geralmente conhecido)
SUCCESS_KEYWORD = "Bem-vindo"      # Palavra-chave que indica login bem-sucedido
FAILURE_KEYWORD = "inválida"       # Palavra-chave que indica falha no login (conceitual)


# 2. Função Principal de Simulação
# -----------------------------------------------------------------------
def brute_force_simulation():
    """
    Simula o processo de leitura da wordlist e tentativa de login
    usando um loop de requisições web.
    """
    # Bloco try-except para lidar com o caso do arquivo não ser encontrado
    try:
        # Abertura do arquivo de wordlist no modo de leitura ('r')
        with open(WORDLIST_FILE, 'r') as file:
            print("-" * 50)
            print(f"[*] ALVO: {TARGET_URL}")
            print(f"[*] USUÁRIO ALVO: {TARGET_USER}")
            print(f"[*] CARREGANDO: {WORDLIST_FILE}")
            print("-" * 50)
            
            # Itera sobre cada linha (senha) do arquivo
            for line in file:
                # Limpa a senha: remove quebras de linha (\n) e espaços em branco
                password = line.strip()
                
                # Garante que não está tentando senhas vazias
                if not password:
                    continue
                
                # Os dados que seriam enviados na requisição POST do formulário de login
                payload = {
                    'username': TARGET_USER,
                    'password': password
                }
                
                # ====================================================================
                # LÓGICA DE REQUISIÇÃO (MANTIDA COMO COMENTÁRIO para fins conceituais)
                # ====================================================================
                
                # # 1. Enviar a requisição POST para a URL de login
                # #    (Isto exigiria a biblioteca 'requests', não disponível no ambiente simulado)
                # print(f"[TENTANDO] Senha: {password}")
                # # response = requests.post(TARGET_URL, data=payload, timeout=5)
                # # response_text = response.text.lower()
                
                # # 2. Simulação de resposta (Para fins de documentação)
                print(f"[TENTANDO] Usuário: {TARGET_USER} | Senha: {password}")
                
                # 3. Lógica de Verificação (Conceitual)
                # O ataque verifica se a palavra de sucesso (ex: "Bem-vindo") está na resposta
                # ou se a palavra de falha ("inválida") NÃO está na resposta.
                
                # Simulação de Sucesso (Exemplo: Encontrou a senha "admin")
                if password == "admin": 
                    print("\n" + "="*50)
                    print(f"[!!! SUCESSO !!!] Credencial encontrada: {TARGET_USER}:{password}")
                    print("="*50 + "\n")
                    return # Encerra a função após encontrar a senha
                    
                # Simulação de Falha
                # elif FAILURE_KEYWORD in response_text: (Com código real)
                else:
                    print("[FALHA] Resposta não indica sucesso.")
                    
        # Se o loop terminar sem encontrar a senha
        print("-" * 50)
        print("[*] Fim da wordlist. Nenhuma senha encontrada na lista.")

    except FileNotFoundError:
        print("\n" + "="*50)
        print(f"[ERRO CRÍTICO] Arquivo '{WORDLIST_FILE}' não encontrado.")
        print("Certifique-se de que 'wordlist.txt' está no mesmo diretório do script.")
        print("="*50 + "\n")
    except Exception as e:
        print(f"[ERRO GERAL] Ocorreu um erro: {e}")

# Inicia a simulação quando o script é executado
if __name__ == "__main__":
    brute_force_simulation()

