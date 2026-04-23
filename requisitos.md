Atue como um Engenheiro Geotécnico e Desenvolvedor Front-end. 
Sua tarefa é criar uma página única (index.html) para ser hospedada no GitHub Pages, contendo uma calculadora interativa de Capacidade de Carga de Fundações Rasas baseada na Teoria de Terzaghi (1943).

**Arquitetura:**
- HTML5, CSS e JavaScript no mesmo arquivo (ou divididos, se preferir).
- Use Bootstrap 5 via CDN para um design responsivo, limpo e profissional.
- Baseie o layout e a paleta de cores nas imagens de referência que estão no diretório.

**Campos de Entrada (Inputs):**
1. Propriedades do Solo: Coesão (c em kPa), Ângulo de Atrito (φ em graus), Peso Específico (γ em kN/m³), Profundidade do Nível d'Água (GWT em m).
2. Geometria da Fundação: Profundidade (Df em m), Largura/Diâmetro (B em m), Tipo de Fundação (Sapata Contínua, Quadrada ou Circular).
3. Critério: Fator de Segurança (FS).

**Campos de Saída (Outputs):**
- Fatores de Capacidade: Nc, Nq, Nγ
- Fatores de Forma: sc, sγ
- Parâmetros Efetivos: Sobrecarga na base (q), Peso Específico Efetivo abaixo da base (γ_efetivo).
- Resultados Finais: q_ult (Capacidade Última em kPa) e q_adm (Capacidade Admissível em kPa).

**Regras de Negócio e Cálculos (MUITO IMPORTANTE):**
1. Fatores de Forma:
   - Quadrada: sc = 1.3, sγ = 0.8
   - Circular: sc = 1.3, sγ = 0.6
   - Contínua (Strip): sc = 1.0, sγ = 1.0
2. Fatores de Capacidade:
   - Use a formulação exata de Terzaghi para Nq: Nq = (e^(2*(0.75*π - φ/2)*tan(φ))) / (2*cos²(45 + φ/2))
   - Nc = (Nq - 1) * cot(φ)
   - Nγ: Como a fórmula de Kpγ é complexa, implemente um array no JavaScript com os valores clássicos da tabela de Terzaghi para Nγ (de 0° a 50°) e faça uma interpolação linear simples para o ângulo de atrito fornecido.
3. Correção do Nível d'Água:
   - A lógica deve ajustar a sobrecarga (q) e o peso específico (γ) considerando se o NA está acima da base (GWT <= Df) ou abaixo da base (GWT > Df), calculando a profundidade da cunha de ruptura H = 0.5 * B * tan(45 + φ/2) para interpolar o peso específico efetivo quando aplicável.
4. Equação Final:
   q_ult = (c * Nc * sc) + (q * Nq) + (0.5 * γ_efetivo * B * Nγ * sγ)

Por favor, gere o código completo e funcional.