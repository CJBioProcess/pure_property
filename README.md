# Property Model Parameters Estimation for Pure Component

**Author:** Jun-Woo Kim  
**Date:** 2024-02-29 (Version 1.0)

---

## Table of Contents

1. [Nomenclature for Process Variables](#nomenclature-for-process-variables)
2. [Reference Property Model Function List](#reference-property-model-function-list)
3. [Applied Property Model Function List](#applied-property-model-function-list)
4. [Parameter Estimation Function List](#parameter-estimation-function-list)
5. [Helper Function List for Numerical Analysis](#helper-function-list-for-numerical-analysis)

---

## Nomenclature for Process Variables

The unit of process variables has been recorded below each model function.

- M: Molecular weight
- T: Temperature
- P: Pressure
- V: Volume
- Tb: Normal boiling temperature
- Tc: Critical temperature
- Pc: Critical pressure
- Vc: Critical volume
- Hform: Heat of formation (ideal gas, 298 K)
- Gform: Gibbs energy of formation (ideal gas, 298 K)
- MUP: Dipole moment
- PL: Vapor pressure
- VL: Liquid molar volume
- omega: Pitzer acentric factor
- CPG: Ideal gas heat capacity
- DHVL: Enthalpy of vaporization
- MUL: Liquid viscosity
- MUG: Gas viscosity
- KL: Liquid thermal viscosity
- KG: Gas thermal viscosity
- SIGMA: Surface tension

---

## Reference Property Model Function List

1.1. **Joback Group Contribution Method for Scalar Properties**
   (It also serves as an applied model.)
   - [M, Tb, Tc, Pc, Vc, Hform, Gform, CPIG] = JOBACK(smiles)

1.2. **Riedel Model for Vapor Pressure**
   - PL = RIEDEL(T, Tb, Tc, Pc)

1.3. **Gunn-Yamada Model for Liquid Molar Volume**
   - VL = GUNN(T, Tc, Pc, omega)

1.4. **Redlich–Kwong Equation of State (RKEOS) Objective Function Form for Gas Molar Volume**
   - y = OBJRK(T, P, V, Tc, Pc)

1.5. **Clausius-Clapeyron Equation for Enthalpy of Vaporization**
   - DHVL = DHVLCC(T, Tc, Pc, RKTZRA, C)

1.6. **Letsou-Stiel Model for Liquid Viscosity**
   - MUL = LETSOU(T, Tc, Pc, M, omega)

1.7. **Chapman-Enskog-Brokaw Model for Gas Viscosity**
   (It also serves as an applied model.)
   - MUG = CHAPMAN(T, Tb, Vb, MUP, M)

1.8. **Sato-Riedel Model for Liquid Thermal Conductivity**
   - KL = SATO(T, Tb, Tc, M)

1.9. **Stiel-Thodos Model for Gas Thermal Conductivity**
   (It also serves as an applied model.)
   - KG = STIEL(T, Tb, Vb, MUP, M, C_CPIG)

1.10. **Block-Bird Model for Surface Tension**
   - SIGMA = BROCK(T, Tb, Tc, Pc)

---

## Applied Property Model Function List

2.1. **Extended Antoine Equation Parameters for Vapor Pressure**
   - PL = PLXANT(T, C)

2.2. **Rackett Model Parameter for Liquid Molar Volume**
   - VL = RACKETT(T, Tc, Pc, RKTZRA)

2.3. **Watson Model Parameters for Enthalpy of Vaporization**
   - DHVL = DHVLWT(T, Tc, C)

2.4. **Aspen Polynomial Model for Ideal Gas Heat Capacity**
   - CPG = CPIG(T, C)

2.5. **Andrade Model Parameters for Liquid Viscosity**
   - MUL = MULAND(T, C)

2.6. **DIPPR Equation 100 Model for Liquid Thermal Conductivity**
   - KL = KLDIP(T, Tc, C)

2.7. **DIPPR Equation 106 Model for Liquid Surface Tension**
   - SIGMA = SIGDIP(T, Tc, C)

---

## Parameter Estimation Function List

3.1. **PLXANT = PLXANT_PCES(Tb, Tc, Pc)**  
3.2. **OMEGA = OMEGA_PCES(Tc, Pc, PLXANT)**  
3.3. **RKTZRA = RKTZRA_PCES(omega)**  
3.3.1. **DHVLB = DHVLB_PCES(Tb, Tc, Pc, RKTZRA, PLXANT)**  
3.3.2. **DHVLWT = DHVLWT_PCES(Tb, Tc, Pc, DHVLB, RKTZRA, PLXANT)**  
3.4. **MULAND = MULAND_PCES(Tb, Tc, Pc, M, omega)**  
3.5. **KLDIP = KLDIP_PCES(Tb, Tc, M)**  
3.6. **SIGDIP = SIGDIP_PCES(Tb, Tc, Pc)**  

---

## Helper Function List for Numerical Analysis

4.1. **Newton-Raphson Method: newton()**  
4.2. **Nelder-Mead Method: nelder()**  
4.3. **Polynomial Curve Fitting: polyfit()**  
4.4. **MULAND Curve Fitting: MULANDfit()** 
