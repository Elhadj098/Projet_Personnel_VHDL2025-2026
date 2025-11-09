# Projet_Personnel_VHDL2025-2026
# 🔧 Comparateur 3 Entrées – 8 bits  
### Réalisation en Logisim & Description matérielle VHDL  

---

## Description du projet

Ce projet implémente un **comparateur numérique parallèle** capable de comparer **trois mots binaires de 8 bits** notés `A`, `B` et `C`.  
Il a été conçu et simulé à la fois :
- sous **Logisim Evolution** (approche schématique matérielle),  
- et en **VHDL** (approche de description matérielle synthétisable sur FPGA).

---

## Objectif

- Comparer les trois entrées `A`, `B` et `C` entre elles.  
- Fournir **9 sorties logiques** indiquant les relations suivantes :  
  - `A>B`, `A=B`, `A<B`  
  - `A>C`, `A=C`, `A<C`  
  - `B>C`, `B=C`, `B<C`  
- Visualiser les résultats sur des **LEDs** dans Logisim ou en simulation VHDL.

---

## Fonctionnement

Chaque paire de signaux est comparée grâce à des opérateurs logiques (`>`, `<`, `=`).  
Les entrées `STD_LOGIC_VECTOR(7 downto 0)` sont converties en `UNSIGNED` pour permettre les comparaisons numériques.  
Le circuit est **purement combinatoire** (pas d’horloge, pas de mémoire).

---

## Code VHDL

```vhdl

-------------------------------------------------------------------------------
-- Nom du fichier     : comparateur_3_entrees.vhd
-- Titre du projet    : Comparateur parallèle à trois entrées (A, B, C)
-- Auteur             : Elhadji FALL
-- Date de création   : 09/11/2025
-- Description        :
--   Ce programme implémente un comparateur logique combinatoire à trois entrées
--   de 8 bits (A, B et C). 
--   Le circuit compare toutes les paires possibles (A/B, A/C, B/C) et génère
--   neuf signaux de sortie :
--       - A_sup_B, A_egal_B, A_inf_B
--       - A_sup_C, A_egal_C, A_inf_C
--       - B_sup_C, B_egal_C, B_inf_C
--
--   Chaque signal de sortie prend la valeur '1' lorsque la condition associée
--   est vraie, sinon '0'.
--
-- Technologies utilisées :
--   - Bibliothèque IEEE.STD_LOGIC_1164
--   - Bibliothèque IEEE.NUMERIC_STD pour les comparaisons sur type unsigned
--
-- Remarques :
--   - Les entrées A, B et C sont de type STD_LOGIC_VECTOR(7 downto 0)
--     et sont converties en type UNSIGNED pour permettre les opérations
--     arithmétiques et de comparaison.
--   - Le circuit est purement combinatoire (sans horloge ni mémoire).
--
-- Version             : 1.0
-------------------------------------------------------------------------------

library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;

entity comparateur_3_entrees is
    port (
        A, B, C : in  STD_LOGIC_VECTOR(7 downto 0);
        A_sup_B, A_egal_B, A_inf_B : out STD_LOGIC;
        A_sup_C, A_egal_C, A_inf_C : out STD_LOGIC;
        B_sup_C, B_egal_C, B_inf_C : out STD_LOGIC
    );
end comparateur_3_entrees;

architecture comportement of comparateur_3_entrees is
    signal A_u, B_u, C_u : unsigned(7 downto 0);
begin
    A_u <= unsigned(A);
    B_u <= unsigned(B);
    C_u <= unsigned(C);

    A_sup_B  <= '1' when A_u > B_u else '0';
    A_egal_B <= '1' when A_u = B_u else '0';
    A_inf_B  <= '1' when A_u < B_u else '0';

    A_sup_C  <= '1' when A_u > C_u else '0';
    A_egal_C <= '1' when A_u = C_u else '0';
    A_inf_C  <= '1' when A_u < C_u else '0';

    B_sup_C  <= '1' when B_u > C_u else '0';
    B_egal_C <= '1' when B_u = C_u else '0';
    B_inf_C  <= '1' when B_u < C_u else '0';
end comportement;
