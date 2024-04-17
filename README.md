## Property model parameters estimation for pure component
## Jun-Woo Kim
## 2024-02-29 (version 1.0)
##
## The reference has been recorded below each model function.
## The function order follows the sequence in the manuscript, which is different from the below Python code order.
## (to prevent errors in the solution sequence)
##
##
##
## 0. Nomenclature for process variables
## The unit of process variable has been recorded below each model function.
##
## M : Molecular weight
## T : Temperature
## P : Pressure
## V : Volume
## Tb : Normal boiling temperature
## Tc : critical temperature
## Pc : critical pressure
## Vc : critical volume
## Hform : Heat of formation (ideal gas, 298 K)
## Gform : Gibbs energy of formation (ideal gas, 298 K)
## MUP : Dipole moment
## PL : Vapor pressure
## VL : Liquid molar volume
## omega: Pitzer acentric factor
## CPG : Ideal gas heat capacity
## DHVL : Enthalpy of vaporization
## MUL : Liquid viscosity
## MUG : Gas viscosity
## KL : Liquid thermal viscosity
## KG : Gas thermal viscosity
## SIGMA : Surface tension
##
##
##
## 1. Reference propertymodel function list
##
## 1.1 Joback group contribution method for scalar properties
## (It also serves as an applied model.)
## [M, Tb, Tc, Pc, Vc, Hform, Gform, CPIG] = JOBACK(smiles)
## 1.2 Riedel model for vapor pressure
## PL = RIEDEL(T, Tb, Tc, Pc)
## 1.3 Gunn-Yamada model for liquid molar volume
## VL = GUNN(T, Tc, Pc, omega)
## 1.4 Redlich–Kwong equation of state (RKEOS) objective function form for gas molar volume
## y = OBJRK(T, P, V, Tc, Pc)
## 1.5 Clausius-Clapeyron equation for Enthalpy of vaporization
## DHVL = DHVLCC(T, Tc, Pc, RKTZRA, C)
## 1.6 Letsou-Stiel model for liquid viscosity
## MUL = LETSOU(T, Tc, Pc, M, omega)
## 1.7 Chapman-Enskog-Brokaw model for gas viscosity
## (It also serves as an applied model.)
## MUG = CHAPMAN(T, Tb, Vb, MUP, M)
## 1.8 Sato-Riedel model for liquid thermal conductivity
## KL = SATO(T, Tb, Tc, M)
## 1.9 Stiel-Thodos model for gas thermal conductivity
## (It also serves as an applied model.)
## KG = STIEL(T, Tb, Vb, MUP, M, C_CPIG)
## 1.10 Block-Bird model for surface tension
## SIGMA = BROCK(T, Tb, Tc, Pc)
##
##
##
## 2. Applied propertymodel function list
##
## 2.1 Extended Antoine equation parameters for vapor pressure
## PL = PLXANT(T, C)
## 2.2 Rackett model parameter for liquid molar volume
## VL = RACKETT(T, Tc, Pc, RKTZRA)
## 2.3 Watson model parameters for enthalpy of vaporization
## DHVL = DHVLWT(T, Tc, C)
## 2.4 Aspen polynomial model for ideal gas heat capacity
## CPG = CPIG(T, C)
## 2.5 Andrade model parameters for liquid viscosity
## MUL = MULAND(T, C)
## 2.6 DIPPR equation 100 model for liquid thermal conductivity
## KL = KLDIP(T, Tc, C)
## 2.7 DIPPR equation 106 model for liquid surface tension
## SIGMA = SIGDIP(T, Tc, C)
##
##
##
## 3. Parameter estimation function list
##
## 3.1 PLXANT = PLXANT_PCES(Tb, Tc, Pc)
## 3.2 OMEGA = OMEGA_PCES(Tc, Pc, PLXANT)
## 3.2 RKTZRA = RKTZRA_PCES(omega)
## 3.3.1 DHVLB = DHVLB_PCES(Tb, Tc, Pc, RKTZRA, PLXANT)
## 3.3.2 DHVLWT = DHVLWT_PCES(Tb, Tc, Pc, DHVLB, RKTZRA, PLXANT)
## 3.4 MULAND = MULAND_PCES(Tb, Tc, Pc, M, omega)
## 3.5 KLDIP = KLDIP_PCES(Tb, Tc, M)
## 3.6 SIGDIP = SIGDIP_PCES(Tb, Tc, Pc)
##
##
##
## 4. Helper function list for numerial analysis
##
## 4.1 Newton-Raphson method, newton()
## 4.2 Nelder-Mead method, nelder()
## 4.3 Polynomial curve fitting, polyfit()
## 4.4 MULAND curve fitting, MULANDfit()
