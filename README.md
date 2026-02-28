import random

def jogar_show_do_milhao():
    # Estrutura de Perguntas (Nível: Fácil, Médio, Difícil)
    perguntas = {
        "facil": [
            {"pergunta": "Quem construiu a arca?", "opcoes": ["A) Moisés", "B) Noé", "C) Davi", "D) Sansão"], "correta": "B"},
            {"pergunta": "Qual o primeiro livro da Bíblia?", "opcoes": ["A) Êxodo", "B) Salmos", "C) Gênesis", "D) Mateus"], "correta": "C"},
        ],
        "medio": [
            {"pergunta": "Qual o nome do mar que Moisés abriu?", "opcoes": ["A) Mar Morto", "B) Mar da Galileia", "C) Mar Vermelho", "D) Mar Mediterrâneo"], "correta": "C"},
        ],
        "dificil": [
            {"pergunta": "Qual era a profissão de Amós?", "opcoes": ["A) Pescador", "B) Cultivador de sicômoros", "C) Coletor de impostos", "D) Carpinteiro"], "correta": "B"},
        ]
    }

    premios = [1000, 2000, 3000, 4000, 5000, 10000, 20000, 40000, 80000, 150000, 300000, 500000, 1000000]
    pulos = 3
    ajuda_universitarios = 1
    ajuda_cartas = 1
    
    nivel_atual = 0
    print("--- BEM-VINDO AO SHOW DO MILHÃO BÍBLICO ---")

    while nivel_atual < len(premios):
        # Define a dificuldade com base no progresso
        if nivel_atual < 4: diff = "facil"
        elif nivel_atual < 8: diff = "medio"
        else: diff = "dificil"

        quest = random.choice(perguntas[diff])
        print(f"\nPergunta valendo R$ {premios[nivel_atual]}")
        print(quest["pergunta"])
        for opt in quest["opcoes"]: print(opt)

        print(f"\n[AJUDAS DISPONÍVEIS: Pulos: {pulos} | Universitários: {ajuda_universitarios} | Cartas: {ajuda_cartas}]")
        escolha = input("Sua resposta (ou digite 'pular', 'universitarios', 'cartas'): ").upper()

        # Lógica de Pular
        if escolha == "PULAR":
            if pulos > 0:
                pulos -= 1
                print("Você pulou a pergunta!")
                continue
            else:
                print("Você não tem mais pulos!")
                continue

        # Lógica de Universitários (Dão a resposta certa 70% das vezes)
        if escolha == "UNIVERSITARIOS":
            if ajuda_universitarios > 0:
                ajuda_universitarios -= 1
                chance = random.random()
                dica = quest["correta"] if chance < 0.8 else random.choice(["A", "B", "C", "D"])
                print(f"Os universitários acham que a resposta é: {dica}")
                escolha = input("Sua resposta final: ").upper()
            else:
                print("Ajuda já utilizada!")
                continue

        # Lógica das Cartas (Elimina opções falsas)
        if escolha == "CARTAS":
            if ajuda_cartas > 0:
                ajuda_cartas -= 1
                cartas = [0, 1, 2, 3] # Representando o Rei, Ás, 2 e 3
                escolhida = random.choice(cartas)
                print(f"Você tirou a carta {escolhida}. Eliminando {escolhida} alternativa(s) incorreta(s)...")
                # Lógica simplificada: remove opções que não são a correta
                opcoes_falsas = [opt[0] for opt in quest["opcoes"] if opt[0] != quest["correta"]]
                eliminadas = random.sample(opcoes_falsas, min(escolhida, len(opcoes_falsas)))
                print(f"Alternativas eliminadas: {eliminadas}")
                escolha = input("Sua resposta final: ").upper()
            else:
                print("Ajuda já utilizada!")
                continue

        # Verificação da Resposta
        if escolha == quest["correta"]:
            print(f"ACERTOU! Você tem R$ {premios[nivel_atual]}")
            nivel_atual += 1
        else:
            print(f"ERROU! A resposta era {quest['correta']}. Fim de jogo.")
            break

    if nivel_atual == len(premios):
        print("PARABÉNS! VOCÊ É O NOVO MILIONÁRIO!")

jogar_show_do_milhao()
