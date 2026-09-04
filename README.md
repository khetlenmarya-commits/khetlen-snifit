===SISTEMA HDL ±6.3 | MENOS VULNERÁVEL ===
Id: sistema_estavel_6_3 | Tipo: VHDL | Bits: 12 (ponto fixo)
Características: Reset assíncrono, sincronização total, suporte ±, sem glitches

[CÓDIGO]
library IEEE;use IEEE.STD_LOGIC_1164.ALL;use IEEE.NUMERIC_STD.ALL;
entity sistema_estavel_6_3 is Port(clk,reset,habilita,modo_pos:in STD_LOGIC;saida:out STD_LOGIC_VECTOR(11 downto 0));end;
architecture top of sistema_estavel_6_3 is constant POS:signed(11 downto 0):="000001100100";constant NEG:signed(11 downto 0):="100001100100";signal r:signed(11 downto 0):=(others=>'0');
begin saida<=std_logic_vector(r);
process(clk,reset)
begin if reset='1'then r<=(others=>'0');elsif rising_edge(clk)then if habilita='1'then r<=POS when modo_pos='1'else NEG;end if;end if;
end process;end top;

[Uso] inter
clk=Relógio | reset=1→zera | habilita=1→atualiza | modo_pos=1→+6.3,0→-6.3
Saída: 12b formato [Sinal][Int7b][Frac4b] aprox 6.3 decimal
