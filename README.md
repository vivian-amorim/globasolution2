# Maria assistente inteligente 

# Objetivo 
A Maria assistente inteligente e não intrusivo focado em prevenir a exaustão e promover o bem-estar no ambiente de trabalho remoto e híbrido. monitora o bem-estar cognitivo dos colaboradores de forma ética e não intrusiva, promovendo intervenções proativas para prevenir o burnout e garantir a sustentabilidade do capital humano.

Como a tecnologia pode tornar o trabalho mais humano, inclusivo e sustentável no futuro?
Humano: Oferece suporte proativo e personalizado à saúde mental.
Inclusivo: Fornece insights neutros para balancear a carga de trabalho.
Sustentável: Garante a produtividade e saúde do colaborador a longo prazo.

Conceito	                    Tecnologia / Ferramenta	                            Aplicação na Aura
Inteligência Artificial (IA)	Processamento de Linguagem Natural (NLP), LSTM	    Cálculo do Índice de Risco (IR) através da análise de sentimento e comportamento.
Análise de Dados	            Python, Pandas	                                    Coleta, estruturação e ponderação de features comportamentais e textuais.
Automação de Decisão	        Estruturas Condicionais (IF/ELSE)	                  Acionamento automático de alertas, sugestões de pausa e bloqueio de agenda.
Arquitetura	                  POO (Classes), Design Tecnológico	                  Estrutura modular da aplicação e mockups de interface (Dashboards).

# Dados de simulação
data = {
    'comunicacao_dia': ["Reunião de emergência às 21h, sem almoço.", "Projeto entregue com sucesso!"],
    'frequencia_reunioes': [5, 2],
    'horas_noturnas': [1.5, 0.0]
}
df = pd.DataFrame(data)
sid = SentimentIntensityAnalyzer()

def calcular_ir_simplificado(row):
    # Risco Sentimento: (1 - S_sentimento) * Peso
    risco_sentimento = 1.0 - (sid.polarity_scores(row['comunicacao_dia'])['compound'] + 1) / 2
    
    # Risco Reuniões (Normalizado)
    risco_reunioes = min(row['frequencia_reunioes'] / 8.0, 1.0)
    risco_noite = min(row['horas_noturnas'] / 4.0, 1.0)
    
    # Cálculo Ponderado (IR)
    IR = (-0.4 * risco_sentimento) + (0.3 * risco_reunioes) + (0.3 * risco_noite)
    
    return max(0, min(IR + 0.5, 1.0)) # Ajuste para range [0, 1]

df['IR'] = df.apply(calcular_ir_simplificado, axis=1)
print(df[['frequencia_reunioes', 'horas_noturnas', 'IR']])

# Resultado: Dia 1 (Alto IR), Dia 2 (Baixo IR)
🚦 Automação de Decisão (Estruturas Condicionais)A Aura transforma o IR em ações usando lógica de decisão, garantindo intervenções rápidas e objetivas.
Código Exemplo: Regra de Intervenção PessoalEsta regra aciona alertas e bloqueia a agenda automaticamente quando o risco é muito alto.Snippet de código// Constantes
LIMITE_ALERTA_AMARELO = 0.55
LIMITE_ALERTA_VERMELHO = 0.75

// Variáveis de Entrada
IR_ATUAL = 0.724  // Exemplo de IR Alto
HORAS_NOITE_HOJE = 1.5

FUNCAO Analisar_e_Intervir(IR_ATUAL, HORAS_NOITE_HOJE):
    SE IR_ATUAL > LIMITE_ALERTA_VERMELHO E HORAS_NOITE_HOJE > 1.0 ENTÃO
        // Intervenção Crítica
        Sistema.BloquearAgenda(30)
        Sistema.EnviarNotificacaoDesktop("URGENTE: Risco de Exaustão. Pausa forçada de 30 minutos.")
        
    SENÃO SE IR_ATUAL > LIMITE_ALERTA_AMARELO ENTÃO
        // Intervenção Moderada
        Sistema.EnviarNotificacaoChat("Seu foco está em declínio. Que tal 10 minutos de alongamento?")
        
    SENÃO
        // Sem Intervenção
        
    FIM SE

# Design Tecnológico 
O design da Maria foca em clareza e ação, utilizando o IR para guiar a interface.
Dashboard Colaborador: Visualiza o IR em um medidor colorido (Verde/Amarelo/Vermelho) com botões de ação (Bloquear Agenda / Sugerir Pausa).
Dashboard Gerencial: Apresenta um Mapa de Calor de Risco (Anonimizado) para identificar clusters de sobrecarga na equipe e sugere a redistribuição de tarefas (inclusão).

