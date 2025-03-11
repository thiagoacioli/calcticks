import streamlit as st 

def calcular_ticks(odd_inicial, odd_atual):
    faixas = [
        (1.01, 2, 0.01),
        (2, 3, 0.02),
        (3, 4, 0.05),
        (4, 6, 0.10),
        (6, 10, 0.20),
        (10, 20, 0.50),
        (20, 30, 1.00),
        (30, 50, 2.00),
        (50, 100, 5.00),
        (100, 1000, 10.00)
    ]
    
    ticks = 0
    odd_atual_calc = odd_inicial
    
    while odd_atual_calc > odd_atual:
        for minimo, maximo, tick_valor in faixas:
            if minimo <= odd_atual_calc < maximo:
                odd_atual_calc -= tick_valor
                ticks += 1
                break
    
    return ticks

def calcular_tics_por_minuto(odd, minuto):
    if minuto == 0:
        return 0
    return ((odd - 1) * 100) / minuto

def determinar_zona(odd):
    if odd > 4:
        return "Lenta"
    elif 4 >= odd > 3.50:
        return "Média"
    elif 3.50 >= odd > 3:
        return "Lenta"
    elif 3 >= odd > 2.30:
        return "Rápida"
    elif 2.30 >= odd > 2:
        return "Lenta"
    elif 2 >= odd > 1.80:
        return "Rápida"
    elif 1.80 >= odd > 1.70:
        return "Média"
    elif 1.70 >= odd > 1.50:
        return "Rápida"
    elif 1.50 >= odd > 1.30:
        return "Média"
    else:
        return "Lenta"

def obter_percentual(odd):
    faixas_percentuais = [
        (1.01, 1.10, 0.87),
        (1.10, 1.20, 0.80),
        (1.20, 1.30, 0.74),
        (1.30, 1.40, 0.68),
        (1.40, 1.50, 0.64),
        (1.50, 1.60, 0.60),
        (1.60, 1.70, 0.56),
        (1.70, 1.80, 0.53),
        (1.80, 1.90, 0.50),
        (1.90, 2.00, 0.48),
        (2.00, 2.20, 0.87),
        (2.20, 2.40, 0.80),
        (2.40, 2.60, 0.74),
        (2.60, 2.80, 0.68),
        (2.80, 3.00, 0.64),
        (3.00, 3.50, 1.38),
        (3.50, 4.00, 1.20),
        (4.00, 5.00, 1.94),
        (5.00, 6.00, 1.61),
        (6.00, 8.00, 2.44),
        (8.00, 10.00, 1.94),
        (10.00, 15.00, 3.28),
    ]
    
    for minimo, maximo, percentual in faixas_percentuais:
        if minimo <= odd < maximo:
            return percentual
    return 0  # Se a odd estiver fora das faixas definidas

# Interface Streamlit
st.title("Calculadora Tics Odd Inicial e Atual")

# Inicializar valores padrão
st.session_state.setdefault("odd_inicial", 3.0)
st.session_state.setdefault("odd_atual", 1.80)

# Criar inputs
odd_inicial = st.number_input("Digite a odd inicial:", min_value=1.01, max_value=1000.0, value=st.session_state["odd_inicial"], step=0.01, key="odd_inicial_input")
odd_atual = st.number_input("Digite a odd atual:", min_value=1.01, max_value=1000.0, value=st.session_state["odd_atual"], step=0.01, key="odd_atual_input")

col1, col2 = st.columns(2)

with col1:
    if st.button("Calcular Ticks"):
        resultado = calcular_ticks(odd_inicial, odd_atual)
        st.write(f"O número de ticks de {odd_inicial} para {odd_atual} é: {resultado}")

with col2:
    if st.button("Reset"):
        st.session_state["odd_inicial"] = 3.0
        st.session_state["odd_atual"] = 1.80
        st.rerun()

# Adicionar seletores
st.title("Calculadora de Tics por Minuto")

minuto_atual = st.number_input("Minuto Atual:", min_value=0, max_value=90, value=0, step=1)
periodo = "HT" if minuto_atual <= 45 else "FT"
st.write(f"Período detectado: {periodo}")

col3, col4, col5 = st.columns(3)

with col3:
    under_limite = st.number_input("Under Limite:", min_value=1.01, max_value=1000.0, value=1.5, step=0.01)
    tics_minuto = calcular_tics_por_minuto(under_limite, minuto_atual)
    zona = determinar_zona(under_limite)
    st.write(f"Tics por minuto: {tics_minuto:.2f}")
    st.write(f"Zona: {zona}")

    # Novo cálculo percentual
    percentual = obter_percentual(under_limite)
    resultado_percentual = tics_minuto * percentual
    st.write(f"Multiplicação por percentual: {resultado_percentual:.2f}%")
with col4:
    under_a_frente = st.number_input("Under à Frente:", min_value=1.01, max_value=1000.0, value=1.8, step=0.01)
    tics_minuto = calcular_tics_por_minuto(under_a_frente, minuto_atual)
    zona = determinar_zona(under_a_frente)
    st.write(f"Tics por minuto: {tics_minuto:.2f}")
    st.write(f"Zona: {zona}")

    # Novo cálculo percentual
    percentual = obter_percentual(under_a_frente)
    resultado_percentual = tics_minuto * percentual
    st.write(f"Multiplicação por percentual: {resultado_percentual:.2f}%")

with col5:
    under_mais2_frente = st.number_input("Under +2 Frente:", min_value=1.01, max_value=1000.0, value=2.0, step=0.01)
    tics_minuto = calcular_tics_por_minuto(under_mais2_frente, minuto_atual)
    zona = determinar_zona(under_mais2_frente)
    st.write(f"Tics por minuto: {tics_minuto:.2f}")
    st.write(f"Zona: {zona}")

    # Novo cálculo percentual
    percentual = obter_percentual(under_mais2_frente)
    resultado_percentual = tics_minuto * percentual
    st.write(f"Multiplicação por percentual: {resultado_percentual:.2f}%")
