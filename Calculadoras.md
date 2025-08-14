---
atqTipo: Filo
armadura: Sin Armadura
ataque: 175
defensa: 50
aturdido: true
flanco: false
derribadoATQ: true
sorprendido: true
retaguardia: false
derribadoDEF: false
retenidoATQ: false
retenidoDEF: false
ataqueF: "145"
trabado: true
coverturaP: false
coverturaT: false
aturdidoM: |-
  - No acciones completas 
   - Parada 1/2 BC
sorprendidoM: |-
  - No puede atacar 
   - Acciones gratuitas o parciales 
   - No DEF escudo 
   - Arma de mano +10 CRIT
derribadoATQM: |-
  - No armas 2 manos 
   - Levantarse = Accion completa
derribadoDEFM: ""
retenidoATQM: ""
dificultad: Normal
BonusHabilidad: 
Ayuda: 2
AyudaE: 3
ayuda: 
ayudaE: 
resultadoT: Fallo Critico
centralP: false
yelmo: false
improvisado: false
tresM: false
diezM: false
veinteM: false
treintaM: false
concentracion: 
ataqueS: 0
resultadoHabilidad: "00"
tresS: false
ataqueM: 0
inmovil: false
concentracionS: 
contactoS: false
quinceS: false
treintaS: false
noventaS: false
noventaMas: false
ataqueSor: 75
resultadoSor: Exito
bonusMagia: 75
resultadoTextoSor: Hechizo se ejecuta sin complicaciones
resultadoSalvacion: "50"
resultadoF: 28 LET
---

> [!danger]- Calculadora de Ataques  
> Ataque
> ---
> Bonus de Ataque: `INPUT[number(placeholder(______)):ataque]`
> 
> Tipo de Ataque:
>```meta-bind
>INPUT[select(
>		option(Filo),
>		option(Contundente),
>		option(Proyectil),
>		option(Desarmado/Presa),
>		option(Sortilegio de Area),
>		option(Sortilegio de Rayo),
>		option(Bestias)
>		):atqTipo]
>```
>Modificadores de Sortilegio Rayo/Area
>---
>|Modificador Generales|    |Modificador Distancia|     |
>|---|:---:|---|:---:|
>|Punto central (Area)|`INPUT[toggle:centralP]`|Hasta 3 metros|`INPUT[toggle:tresM]`|
>|Lleva yelmo|`INPUT[toggle:yelmo]`|De 4 a 10 metros|`INPUT[toggle:diezM]`|
>|Improvisado|`INPUT[toggle:improvisado]`|De 11 a 20 metros|`INPUT[toggle:veinteM]`|
>|Concentracion|`INPUT[number(placeholder(______)):concentracion]`|De 21 a 30 metros|`INPUT[toggle:treintaM]`|
>
>```meta-bind-js-view
>{centralP} as centralP
>{yelmo} as yelmo
>{improvisado} as improvisado
>{concentracion} as concentracion
>{tresM} as tresM
>{diezM} as diezM
>{veinteM} as veinteM
>{treintaM} as treintaM
>save to {ataqueS}
>hidden
>---
>let atqSor = 0;
> if(context.bound.centralP){
> 	atqSor += 20;
> }
> if(context.bound.yelmo){
> 	atqSor -= 10;
> }
>  if(context.bound.improvisado){
> 	atqSor -= 10;
> }
>   if(context.bound.concentracion > 0 && context.bound.concentracion < 4){
> 	atqSor += (context.bound.concentracion * 10);
> } else if(context.bound.concentracion >= 4) {
> 	atqSor += 40;
> }
>  if(context.bound.tresM){
> 	atqSor += 35;
> }
> if(context.bound.diezM){
> 	atqSor += 10;
> }
>  if(context.bound.treintaM){
> 	atqSor -= 20;
> }
> return atqSor;
>```
>
>Defensa
>---
>Bonus de Defensa: `INPUT[number(placeholder(______)):defensa]`
>
>Tipo de Armadura:  
>```meta-bind
>INPUT[select(
>		option(Sin Armadura),
>		option(Armadura Ligera),
>		option(Armadura Media),
>		option(Armadura Pesada)
>		):armadura]
>```
>Estados
>----
>|Estado|    |Estado|     |
>|---|---|---|---|
>|Aturdido|`INPUT[toggle(class(check)):aturdido]`|Sorprendido|`INPUT[toggle:sorprendido]`|
>|Flanco|`INPUT[toggle:flanco]`|Retaguardia|`INPUT[toggle:retaguardia]`|
>|Derribado (ATQ)|`INPUT[toggle:derribadoATQ]`|Derribado(DEF)|`INPUT[toggle:derribadoDEF]`|
>|Retenido(ATQ)|`INPUT[toggle:retenidoATQ]`|Retenido(DEF)|`INPUT[toggle:retenidoDEF]`|
>|Covertura(Parcial)|`INPUT[toggle:coverturaP]`|Covertura(Total)|`INPUT[toggle:coverturaT]`|
>|Trabado|`INPUT[toggle:trabado]`|
>Resultado de la tirada
>----
>```meta-bind-js-view
>{ataque} as ataque
>{defensa} as defensa
>{atqTipo} as atqTipo
>{aturdido} as aturdido
>{sorprendido} as sorprendido
>{flanco} as flanco
>{retaguardia} as retaguardia
>{derribadoATQ} as derribadoATQ
>{derribadoDEF} as derribadoDEF
>{retenidoATQ} as retenidoATQ
>{retenidoDEF} as retenidoDEF 
>{coverturaP} as coverturaP
>{coverturaT} as coverturaT
>{trabado} as trabado
>{ataqueS} as ataqueS
>save to {ataqueF}
>hidden
>---
>let atqTotal = context.bound.ataque - context.bound.defensa;
>let atqS =context.bound.ataqueS ;
>function applyStatus(atqTotal){
> 	if(context.bound.aturdido){
> 		atqTotal = atqTotal + 20;
> 	}
> 	if(context.bound.sorprendido){
> 		atqTotal = atqTotal + 20;
> 	}
> 	if(context.bound.flanco){
> 		atqTotal = atqTotal + 15;
> 	}
> 	if(context.bound.retaguardia){
> 		atqTotal = atqTotal + 30;
> 	}
> 	if(context.bound.derribadoATQ){
> 		atqTotal = atqTotal - 20;
> 	}
> 	if(context.bound.derribadoDEF){
> 		if(context.bound.trabado){
> 			atqTotal = atqTotal + 20;
> 			
> 		} else if(context.bound.atqTipo === 'Proyectil' || context.bound.atqTipo === 'Sortilegio de Area' || context.bound.atqTipo === 'Sortilegio de Rayo'){
> 			atqTotal = atqTotal - 20;
> 		}
> 	}
> 	if(context.bound.retenidoATQ){
> 		atqTotal = atqTotal - 30;
> 	}
> 	if(context.bound.retenidoDEF){
> 		atqTotal = atqTotal + 30;
> 		if(context.bound.atqTipo !== 'Proyectil' && context.bound.atqTipo !== 'Sortilegio de Area' && context.bound.atqTipo !== 'Sortilegio de Rayo'){
> 			atqTotal = atqTotal + 30;
> 		}
> 	}
> 	if(context.bound.coverturaP){
> 		atqTotal = atqTotal - 20;
> 	}
> 	if(context.bound.coverturaT){
> 		atqTotal = atqTotal - 50;
> 	}
> 	if(context.bound.atqTipo === 'Sortilegio de Area' || context.bound.atqTipo === 'Sortilegio de Rayo'){
> 		atqTotal = atqTotal + atqS;
> 	}
> 	return atqTotal;
> }
>return `${applyStatus(atqTotal)}`;
>```
>```meta-bind-js-view
>{armadura} as armadura
>{atqTipo} as atqTipo
>{ataqueF} as ataqueF
>save to {resultadoF}
>hidden
>---
>const tablaFilo = [
>	{arm: 'Sin Armadura', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Sin Armadura', atqMIN:11, atqMAX:35, value: '-'},
>	{arm: 'Sin Armadura', atqMIN:36, atqMAX:40, value: '-'},
>	{arm: 'Sin Armadura', atqMIN:41, atqMAX:45, value: '-'},
>	{arm: 'Sin Armadura', atqMIN:46, atqMAX:50, value: '-'},
>	{arm: 'Sin Armadura', atqMIN:51, atqMAX:55, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:56, atqMAX:60, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:61, atqMAX:65, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:66, atqMAX:70, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:71, atqMAX:75, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:76, atqMAX:80, value: '7 SUP'},
>	{arm: 'Sin Armadura', atqMIN:81, atqMAX:85, value: '9 SUP'},
>	{arm: 'Sin Armadura', atqMIN:86, atqMAX:90, value: '10 LEV'},
>	{arm: 'Sin Armadura', atqMIN:91, atqMAX:95, value: '11 LEV'},
>	{arm: 'Sin Armadura', atqMIN:96, atqMAX:100, value: '13 MOD'},
>	{arm: 'Sin Armadura', atqMIN:101, atqMAX:105, value: '15 MOD'},
>	{arm: 'Sin Armadura', atqMIN:106, atqMAX:110, value: '17 GRA'},
>	{arm: 'Sin Armadura', atqMIN:111, atqMAX:115, value: '19 GRA'},
>	{arm: 'Sin Armadura', atqMIN:116, atqMAX:120, value: '20 GRA'},
>	{arm: 'Sin Armadura', atqMIN:121, atqMAX:125, value: '21 LET'},
>	{arm: 'Sin Armadura', atqMIN:126, atqMAX:130, value: '23 LET'},
>	{arm: 'Sin Armadura', atqMIN:131, atqMAX:135, value: '25 LET'},
>	{arm: 'Sin Armadura', atqMIN:136, atqMAX:140, value: '27 LET'},
>	{arm: 'Sin Armadura', atqMIN:141, atqMAX:145, value: '28 LET'},
>	{arm: 'Sin Armadura', atqMIN:146, atqMAX:150, value: '30 LET'},
>	{arm: 'Sin Armadura', atqMIN:151, atqMAX:155, value: '34 LET'},
>	{arm: 'Sin Armadura', atqMIN:156, atqMAX:160, value: '38 LET'},
>	{arm: 'Sin Armadura', atqMIN:161, atqMAX:165, value: '42 LET'},
>	{arm: 'Sin Armadura', atqMIN:166, atqMAX:170, value: '46 LET'},
>	{arm: 'Sin Armadura', atqMIN:171, atqMAX:9999, value: '50 LET'},
>	
>	{arm: 'Armadura Ligera', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Ligera', atqMIN:11, atqMAX:45, value: '-'},
>	{arm: 'Armadura Ligera', atqMIN:46, atqMAX:65, value: '0'},
>	{arm: 'Armadura Ligera', atqMIN:66, atqMAX:70, value: '2'},
>	{arm: 'Armadura Ligera', atqMIN:71, atqMAX:75, value: '3'},
>	{arm: 'Armadura Ligera', atqMIN:76, atqMAX:80, value: '5'},
>	{arm: 'Armadura Ligera', atqMIN:81, atqMAX:85, value: '6'},
>	{arm: 'Armadura Ligera', atqMIN:86, atqMAX:90, value: '7'},
>	{arm: 'Armadura Ligera', atqMIN:91, atqMAX:95, value: '9 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:96, atqMAX:100, value: '10 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:101, atqMAX:105, value: '11 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:106, atqMAX:110, value: '12 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:111, atqMAX:115, value: '13 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:116, atqMAX:120, value: '15 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:121, atqMAX:125, value: '16 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:126, atqMAX:130, value: '17 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:131, atqMAX:135, value: '18 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:136, atqMAX:140, value: '20 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:141, atqMAX:145, value: '21 LET'},
>	{arm: 'Armadura Ligera', atqMIN:146, atqMAX:150, value: '22 LET'},
>	{arm: 'Armadura Ligera', atqMIN:151, atqMAX:155, value: '26 LET'},
>	{arm: 'Armadura Ligera', atqMIN:156, atqMAX:160, value: '30 LET'},
>	{arm: 'Armadura Ligera', atqMIN:161, atqMAX:165, value: '34 LET'},
>	{arm: 'Armadura Ligera', atqMIN:166, atqMAX:170, value: '37 LET'},
>	{arm: 'Armadura Ligera', atqMIN:171, atqMAX:9999, value: '40 LET'},
>	
>	{arm: 'Armadura Media', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Media', atqMIN:11, atqMAX:40, value: '-'},
>	{arm: 'Armadura Media', atqMIN:41, atqMAX:55, value: '0'},
>	{arm: 'Armadura Media', atqMIN:56, atqMAX:60, value: '1'},
>	{arm: 'Armadura Media', atqMIN:61, atqMAX:65, value: '2'},
>	{arm: 'Armadura Media', atqMIN:66, atqMAX:70, value: '3'},
>	{arm: 'Armadura Media', atqMIN:71, atqMAX:75, value: '4'},
>	{arm: 'Armadura Media', atqMIN:76, atqMAX:80, value: '5'},
>	{arm: 'Armadura Media', atqMIN:81, atqMAX:85, value: '6'},
>	{arm: 'Armadura Media', atqMIN:86, atqMAX:90, value: '7'},
>	{arm: 'Armadura Media', atqMIN:91, atqMAX:95, value: '8'},
>	{arm: 'Armadura Media', atqMIN:96, atqMAX:100, value: '9'},
>	{arm: 'Armadura Media', atqMIN:101, atqMAX:105, value: '10 SUP'},
>	{arm: 'Armadura Media', atqMIN:106, atqMAX:110, value: '11 SUP'},
>	{arm: 'Armadura Media', atqMIN:111, atqMAX:115, value: '12 LEV'},
>	{arm: 'Armadura Media', atqMIN:116, atqMAX:120, value: '13 LEV'},
>	{arm: 'Armadura Media', atqMIN:121, atqMAX:125, value: '13 MOD'},
>	{arm: 'Armadura Media', atqMIN:126, atqMAX:130, value: '14 MOD'},
>	{arm: 'Armadura Media', atqMIN:131, atqMAX:135, value: '15 MOD'},
>	{arm: 'Armadura Media', atqMIN:136, atqMAX:140, value: '16 GRA'},
>	{arm: 'Armadura Media', atqMIN:141, atqMAX:145, value: '17 GRA'},
>	{arm: 'Armadura Media', atqMIN:146, atqMAX:150, value: '18 LET'},
>	{arm: 'Armadura Media', atqMIN:151, atqMAX:155, value: '21 LET'},
>	{arm: 'Armadura Media', atqMIN:156, atqMAX:160, value: '24 LET'},
>	{arm: 'Armadura Media', atqMIN:161, atqMAX:165, value: '27 LET'},
>	{arm: 'Armadura Media', atqMIN:166, atqMAX:170, value: '30 LET'},
>	{arm: 'Armadura Media', atqMIN:171, atqMAX:9999, value: '33 LET'},
>	
>	{arm: 'Armadura Pesada', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Pesada', atqMIN:11, atqMAX:35, value: '-'},
>	{arm: 'Armadura Pesada', atqMIN:36, atqMAX:45, value: '0'},
>	{arm: 'Armadura Pesada', atqMIN:46, atqMAX:55, value: '1'},
>	{arm: 'Armadura Pesada', atqMIN:56, atqMAX:65, value: '2'},
>	{arm: 'Armadura Pesada', atqMIN:66, atqMAX:75, value: '3'},
>	{arm: 'Armadura Pesada', atqMIN:76, atqMAX:80, value: '4'},
>	{arm: 'Armadura Pesada', atqMIN:81, atqMAX:90, value: '5'},
>	{arm: 'Armadura Pesada', atqMIN:91, atqMAX:100, value: '6'},
>	{arm: 'Armadura Pesada', atqMIN:101, atqMAX:105, value: '7'},
>	{arm: 'Armadura Pesada', atqMIN:106, atqMAX:110, value: '8'},
>	{arm: 'Armadura Pesada', atqMIN:111, atqMAX:115, value: '8 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:116, atqMAX:120, value: '9 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:121, atqMAX:125, value: '10 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:126, atqMAX:130, value: '10 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:131, atqMAX:135, value: '10 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:136, atqMAX:140, value: '11 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:141, atqMAX:145, value: '11 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:146, atqMAX:150, value: '12 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:151, atqMAX:155, value: '14 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:156, atqMAX:160, value: '16 LET'},
>	{arm: 'Armadura Pesada', atqMIN:161, atqMAX:165, value: '18 LET'},
>	{arm: 'Armadura Pesada', atqMIN:166, atqMAX:170, value: '20 LET'},
>	{arm: 'Armadura Pesada', atqMIN:171, atqMAX:9999, value: '22 LET'}
>];
>
>const tablaContundente = [
>	{arm: 'Sin Armadura', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Sin Armadura', atqMIN:11, atqMAX:35, value: '-'},
>	{arm: 'Sin Armadura', atqMIN:36, atqMAX:40, value: '-'},
>	{arm: 'Sin Armadura', atqMIN:41, atqMAX:45, value: '-'},
>	{arm: 'Sin Armadura', atqMIN:46, atqMAX:50, value: '-'},
>	{arm: 'Sin Armadura', atqMIN:51, atqMAX:55, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:56, atqMAX:60, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:61, atqMAX:65, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:66, atqMAX:70, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:71, atqMAX:75, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:76, atqMAX:80, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:81, atqMAX:85, value: '6'},
>	{arm: 'Sin Armadura', atqMIN:86, atqMAX:90, value: '8'},
>	{arm: 'Sin Armadura', atqMIN:91, atqMAX:95, value: '9 SUP'},
>	{arm: 'Sin Armadura', atqMIN:96, atqMAX:100, value: '10 LEV'},
>	{arm: 'Sin Armadura', atqMIN:101, atqMAX:105, value: '12 MOD'},
>	{arm: 'Sin Armadura', atqMIN:106, atqMAX:110, value: '13 MOD'},
>	{arm: 'Sin Armadura', atqMIN:111, atqMAX:115, value: '14 GRA'},
>	{arm: 'Sin Armadura', atqMIN:116, atqMAX:120, value: '15 GRA'},
>	{arm: 'Sin Armadura', atqMIN:121, atqMAX:125, value: '17 GRA'},
>	{arm: 'Sin Armadura', atqMIN:126, atqMAX:130, value: '18 LET'},
>	{arm: 'Sin Armadura', atqMIN:131, atqMAX:135, value: '19 LET'},
>	{arm: 'Sin Armadura', atqMIN:136, atqMAX:140, value: '21 LET'},
>	{arm: 'Sin Armadura', atqMIN:141, atqMAX:145, value: '22 LET'},
>	{arm: 'Sin Armadura', atqMIN:146, atqMAX:150, value: '23 LET'},
>	{arm: 'Sin Armadura', atqMIN:151, atqMAX:155, value: '26 LET'},
>	{arm: 'Sin Armadura', atqMIN:156, atqMAX:160, value: '29 LET'},
>	{arm: 'Sin Armadura', atqMIN:161, atqMAX:165, value: '32 LET'},
>	{arm: 'Sin Armadura', atqMIN:166, atqMAX:170, value: '34 LET'},
>	{arm: 'Sin Armadura', atqMIN:171, atqMAX:9999, value: '36 LET'},
>	
>	{arm: 'Armadura Ligera', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Ligera', atqMIN:11, atqMAX:45, value: '-'},
>	{arm: 'Armadura Ligera', atqMIN:46, atqMAX:50, value: '2'},
>	{arm: 'Armadura Ligera', atqMIN:51, atqMAX:60, value: '3'},
>	{arm: 'Armadura Ligera', atqMIN:61, atqMAX:65, value: '4'},
>	{arm: 'Armadura Ligera', atqMIN:66, atqMAX:75, value: '5'},
>	{arm: 'Armadura Ligera', atqMIN:76, atqMAX:80, value: '6'},
>	{arm: 'Armadura Ligera', atqMIN:81, atqMAX:85, value: '7'},
>	{arm: 'Armadura Ligera', atqMIN:86, atqMAX:90, value: '8'},
>	{arm: 'Armadura Ligera', atqMIN:91, atqMAX:95, value: '8 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:96, atqMAX:100, value: '9 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:101, atqMAX:105, value: '10 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:106, atqMAX:110, value: '11 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:111, atqMAX:115, value: '12 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:116, atqMAX:120, value: '13 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:121, atqMAX:125, value: '15 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:126, atqMAX:130, value: '16 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:131, atqMAX:135, value: '17 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:136, atqMAX:140, value: '18 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:141, atqMAX:145, value: '19 LET'},
>	{arm: 'Armadura Ligera', atqMIN:146, atqMAX:150, value: '20 LET'},
>	{arm: 'Armadura Ligera', atqMIN:151, atqMAX:155, value: '22 LET'},
>	{arm: 'Armadura Ligera', atqMIN:156, atqMAX:160, value: '24 LET'},
>	{arm: 'Armadura Ligera', atqMIN:161, atqMAX:165, value: '26 LET'},
>	{arm: 'Armadura Ligera', atqMIN:166, atqMAX:170, value: '28 LET'},
>	{arm: 'Armadura Ligera', atqMIN:171, atqMAX:9999, value: '30 LET'},
>	
>	{arm: 'Armadura Media', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Media', atqMIN:11, atqMAX:40, value: '-'},
>	{arm: 'Armadura Media', atqMIN:41, atqMAX:45, value: '1'},
>	{arm: 'Armadura Media', atqMIN:45, atqMAX:50, value: '2'},
>	{arm: 'Armadura Media', atqMIN:50, atqMAX:55, value: '3'},
>	{arm: 'Armadura Media', atqMIN:56, atqMAX:60, value: '4'},
>	{arm: 'Armadura Media', atqMIN:61, atqMAX:65, value: '5'},
>	{arm: 'Armadura Media', atqMIN:66, atqMAX:70, value: '6'},
>	{arm: 'Armadura Media', atqMIN:71, atqMAX:75, value: '7'},
>	{arm: 'Armadura Media', atqMIN:76, atqMAX:80, value: '8'},
>	{arm: 'Armadura Media', atqMIN:81, atqMAX:85, value: '9'},
>	{arm: 'Armadura Media', atqMIN:86, atqMAX:90, value: '10'},
>	{arm: 'Armadura Media', atqMIN:91, atqMAX:95, value: '11'},
>	{arm: 'Armadura Media', atqMIN:96, atqMAX:100, value: '12 SUP'},
>	{arm: 'Armadura Media', atqMIN:101, atqMAX:105, value: '13 SUP'},
>	{arm: 'Armadura Media', atqMIN:106, atqMAX:110, value: '14 LEV'},
>	{arm: 'Armadura Media', atqMIN:111, atqMAX:115, value: '15 LEV'},
>	{arm: 'Armadura Media', atqMIN:116, atqMAX:120, value: '16 MOD'},
>	{arm: 'Armadura Media', atqMIN:121, atqMAX:125, value: '17 MOD'},
>	{arm: 'Armadura Media', atqMIN:126, atqMAX:130, value: '18 MOD'},
>	{arm: 'Armadura Media', atqMIN:131, atqMAX:135, value: '19 GRA'},
>	{arm: 'Armadura Media', atqMIN:136, atqMAX:140, value: '20 GRA'},
>	{arm: 'Armadura Media', atqMIN:141, atqMAX:145, value: '21 GRA'},
>	{arm: 'Armadura Media', atqMIN:146, atqMAX:150, value: '22 LET'},
>	{arm: 'Armadura Media', atqMIN:151, atqMAX:155, value: '23 LET'},
>	{arm: 'Armadura Media', atqMIN:156, atqMAX:160, value: '24 LET'},
>	{arm: 'Armadura Media', atqMIN:161, atqMAX:165, value: '25 LET'},
>	{arm: 'Armadura Media', atqMIN:166, atqMAX:170, value: '26 LET'},
>	{arm: 'Armadura Media', atqMIN:171, atqMAX:9999, value: '28 LET'},
>	
>	{arm: 'Armadura Pesada', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Pesada', atqMIN:11, atqMAX:35, value: '-'},
>	{arm: 'Armadura Pesada', atqMIN:36, atqMAX:40, value: '0'},
>	{arm: 'Armadura Pesada', atqMIN:41, atqMAX:45, value: '1'},
>	{arm: 'Armadura Pesada', atqMIN:46, atqMAX:50, value: '2'},
>	{arm: 'Armadura Pesada', atqMIN:51, atqMAX:60, value: '3'},
>	{arm: 'Armadura Pesada', atqMIN:61, atqMAX:65, value: '4'},
>	{arm: 'Armadura Pesada', atqMIN:66, atqMAX:75, value: '5'},
>	{arm: 'Armadura Pesada', atqMIN:76, atqMAX:80, value: '6'},
>	{arm: 'Armadura Pesada', atqMIN:81, atqMAX:90, value: '7'},
>	{arm: 'Armadura Pesada', atqMIN:91, atqMAX:95, value: '8'},
>	{arm: 'Armadura Pesada', atqMIN:95, atqMAX:100, value: '9'},
>	{arm: 'Armadura Pesada', atqMIN:101, atqMAX:105, value: '10'},
>	{arm: 'Armadura Pesada', atqMIN:106, atqMAX:110, value: '10 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:111, atqMAX:115, value: '11 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:116, atqMAX:120, value: '12 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:121, atqMAX:125, value: '13 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:126, atqMAX:130, value: '13 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:131, atqMAX:135, value: '14 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:136, atqMAX:140, value: '15 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:141, atqMAX:145, value: '16 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:146, atqMAX:150, value: '16 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:151, atqMAX:155, value: '17 LET'},
>	{arm: 'Armadura Pesada', atqMIN:156, atqMAX:160, value: '17 LET'},
>	{arm: 'Armadura Pesada', atqMIN:161, atqMAX:165, value: '18 LET'},
>	{arm: 'Armadura Pesada', atqMIN:166, atqMAX:170, value: '18 LET'},
>	{arm: 'Armadura Pesada', atqMIN:171, atqMAX:9999, value: '19 LET'}
>];
>
>const tablaProyectil = [
>	{arm: 'Sin Armadura', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Sin Armadura', atqMIN:11, atqMAX:90, value: '-'},
>	{arm: 'Sin Armadura', atqMIN:91, atqMAX:95, value: '8 SUP'},
>	{arm: 'Sin Armadura', atqMIN:96, atqMAX:100, value: '10 LEV'},
>	{arm: 'Sin Armadura', atqMIN:101, atqMAX:105, value: '11 MOD'},
>	{arm: 'Sin Armadura', atqMIN:106, atqMAX:110, value: '13 MOD'},
>	{arm: 'Sin Armadura', atqMIN:111, atqMAX:115, value: '15 MOD'},
>	{arm: 'Sin Armadura', atqMIN:116, atqMAX:120, value: '16 GRA'},
>	{arm: 'Sin Armadura', atqMIN:121, atqMAX:125, value: '18 GRA'},
>	{arm: 'Sin Armadura', atqMIN:126, atqMAX:130, value: '20 GRA'},
>	{arm: 'Sin Armadura', atqMIN:131, atqMAX:135, value: '21 LET'},
>	{arm: 'Sin Armadura', atqMIN:136, atqMAX:140, value: '23 LET'},
>	{arm: 'Sin Armadura', atqMIN:141, atqMAX:145, value: '25 LET'},
>	{arm: 'Sin Armadura', atqMIN:146, atqMAX:150, value: '27 LET'},
>	{arm: 'Sin Armadura', atqMIN:151, atqMAX:155, value: '29 LET'},
>	{arm: 'Sin Armadura', atqMIN:156, atqMAX:160, value: '31 LET'},
>	{arm: 'Sin Armadura', atqMIN:161, atqMAX:165, value: '33 LET'},
>	{arm: 'Sin Armadura', atqMIN:166, atqMAX:170, value: '35 LET'},
>	{arm: 'Sin Armadura', atqMIN:171, atqMAX:9999, value: '37 LET'},
>	
>	{arm: 'Armadura Ligera', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Ligera', atqMIN:11, atqMAX:70, value: '-'},
>	{arm: 'Armadura Ligera', atqMIN:71, atqMAX:80, value: '0'},
>	{arm: 'Armadura Ligera', atqMIN:81, atqMAX:85, value: '3'},
>	{arm: 'Armadura Ligera', atqMIN:86, atqMAX:90, value: '5'},
>	{arm: 'Armadura Ligera', atqMIN:91, atqMAX:95, value: '7 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:96, atqMAX:100, value: '9 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:101, atqMAX:105, value: '10 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:106, atqMAX:110, value: '12 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:111, atqMAX:115, value: '13 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:116, atqMAX:120, value: '15 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:121, atqMAX:125, value: '17 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:126, atqMAX:130, value: '19 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:131, atqMAX:135, value: '21 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:136, atqMAX:140, value: '23 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:141, atqMAX:145, value: '25 LET'},
>	{arm: 'Armadura Ligera', atqMIN:146, atqMAX:150, value: '26 LET'},
>	{arm: 'Armadura Ligera', atqMIN:151, atqMAX:155, value: '28 LET'},
>	{arm: 'Armadura Ligera', atqMIN:156, atqMAX:160, value: '30 LET'},
>	{arm: 'Armadura Ligera', atqMIN:161, atqMAX:165, value: '32 LET'},
>	{arm: 'Armadura Ligera', atqMIN:166, atqMAX:170, value: '33 LET'},
>	{arm: 'Armadura Ligera', atqMIN:171, atqMAX:9999, value: '34 LET'},
>	
>	{arm: 'Armadura Media', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Media', atqMIN:11, atqMAX:60, value: '-'},
>	{arm: 'Armadura Media', atqMIN:61, atqMAX:75, value: '0'},
>	{arm: 'Armadura Media', atqMIN:76, atqMAX:80, value: '2'},
>	{arm: 'Armadura Media', atqMIN:81, atqMAX:85, value: '4'},
>	{arm: 'Armadura Media', atqMIN:86, atqMAX:90, value: '6'},
>	{arm: 'Armadura Media', atqMIN:91, atqMAX:95, value: '7'},
>	{arm: 'Armadura Media', atqMIN:96, atqMAX:100, value: '8 SUP'},
>	{arm: 'Armadura Media', atqMIN:101, atqMAX:105, value: '10 SUP'},
>	{arm: 'Armadura Media', atqMIN:106, atqMAX:110, value: '13 LEV'},
>	{arm: 'Armadura Media', atqMIN:111, atqMAX:115, value: '14 LEV'},
>	{arm: 'Armadura Media', atqMIN:116, atqMAX:120, value: '16 LEV'},
>	{arm: 'Armadura Media', atqMIN:121, atqMAX:125, value: '17 MOD'},
>	{arm: 'Armadura Media', atqMIN:126, atqMAX:130, value: '19 MOD'},
>	{arm: 'Armadura Media', atqMIN:131, atqMAX:135, value: '20 GRA'},
>	{arm: 'Armadura Media', atqMIN:136, atqMAX:140, value: '22 GRA'},
>	{arm: 'Armadura Media', atqMIN:141, atqMAX:145, value: '23 LET'},
>	{arm: 'Armadura Media', atqMIN:146, atqMAX:150, value: '25 LET'},
>	{arm: 'Armadura Media', atqMIN:151, atqMAX:155, value: '26 LET'},
>	{arm: 'Armadura Media', atqMIN:156, atqMAX:160, value: '27 LET'},
>	{arm: 'Armadura Media', atqMIN:161, atqMAX:165, value: '28 LET'},
>	{arm: 'Armadura Media', atqMIN:166, atqMAX:170, value: '29 LET'},
>	{arm: 'Armadura Media', atqMIN:171, atqMAX:9999, value: '30 LET'},
>	
>	{arm: 'Armadura Pesada', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Pesada', atqMIN:11, atqMAX:50, value: '-'},
>	{arm: 'Armadura Pesada', atqMIN:51, atqMAX:70, value: '0'},
>	{arm: 'Armadura Pesada', atqMIN:71, atqMAX:75, value: '1'},
>	{arm: 'Armadura Pesada', atqMIN:76, atqMAX:80, value: '2'},
>	{arm: 'Armadura Pesada', atqMIN:81, atqMAX:86, value: '3'},
>	{arm: 'Armadura Pesada', atqMIN:85, atqMAX:90, value: '4'},
>	{arm: 'Armadura Pesada', atqMIN:91, atqMAX:95, value: '5'},
>	{arm: 'Armadura Pesada', atqMIN:95, atqMAX:100, value: '6'},
>	{arm: 'Armadura Pesada', atqMIN:101, atqMAX:105, value: '7'},
>	{arm: 'Armadura Pesada', atqMIN:106, atqMAX:110, value: '8 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:111, atqMAX:115, value: '9 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:116, atqMAX:120, value: '10 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:121, atqMAX:125, value: '10 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:126, atqMAX:130, value: '11 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:131, atqMAX:135, value: '12 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:136, atqMAX:140, value: '13 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:141, atqMAX:145, value: '14 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:146, atqMAX:150, value: '15 LET'},
>	{arm: 'Armadura Pesada', atqMIN:151, atqMAX:155, value: '16 LET'},
>	{arm: 'Armadura Pesada', atqMIN:156, atqMAX:160, value: '17 LET'},
>	{arm: 'Armadura Pesada', atqMIN:161, atqMAX:165, value: '18 LET'},
>	{arm: 'Armadura Pesada', atqMIN:166, atqMAX:170, value: '19 LET'},
>	{arm: 'Armadura Pesada', atqMIN:171, atqMAX:9999, value: '20 LET'}
>];
>
>const tablaDesarmado = [
>	{arm: 'Sin Armadura', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Sin Armadura', atqMIN:11, atqMAX:35, value: '-'},
>	{arm: 'Sin Armadura', atqMIN:36, atqMAX:50, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:51, atqMAX:60, value: '1'},
>	{arm: 'Sin Armadura', atqMIN:61, atqMAX:70, value: '2'},
>	{arm: 'Sin Armadura', atqMIN:71, atqMAX:75, value: '3'},
>	{arm: 'Sin Armadura', atqMIN:76, atqMAX:80, value: '4'},
>	{arm: 'Sin Armadura', atqMIN:81, atqMAX:85, value: '5'},
>	{arm: 'Sin Armadura', atqMIN:86, atqMAX:90, value: '6'},
>	{arm: 'Sin Armadura', atqMIN:91, atqMAX:95, value: '7'},
>	{arm: 'Sin Armadura', atqMIN:96, atqMAX:100, value: '8'},
>	{arm: 'Sin Armadura', atqMIN:101, atqMAX:105, value: '9 SUP'},
>	{arm: 'Sin Armadura', atqMIN:106, atqMAX:110, value: '10 SUP'},
>	{arm: 'Sin Armadura', atqMIN:111, atqMAX:115, value: '11 SUP'},
>	{arm: 'Sin Armadura', atqMIN:116, atqMAX:120, value: '12 LEV'},
>	{arm: 'Sin Armadura', atqMIN:121, atqMAX:125, value: '14 LEV'},
>	{arm: 'Sin Armadura', atqMIN:126, atqMAX:130, value: '15 LEV'},
>	{arm: 'Sin Armadura', atqMIN:131, atqMAX:135, value: '16 MOD'},
>	{arm: 'Sin Armadura', atqMIN:136, atqMAX:140, value: '17 MOD'},
>	{arm: 'Sin Armadura', atqMIN:141, atqMAX:145, value: '18 MOD'},
>	{arm: 'Sin Armadura', atqMIN:146, atqMAX:150, value: '19 GRA'},
>	{arm: 'Sin Armadura', atqMIN:151, atqMAX:155, value: '20 GRA'},
>	{arm: 'Sin Armadura', atqMIN:156, atqMAX:160, value: '22 GRA'},
>	{arm: 'Sin Armadura', atqMIN:161, atqMAX:165, value: '24 LET'},
>	{arm: 'Sin Armadura', atqMIN:166, atqMAX:170, value: '26 LET'},
>	{arm: 'Sin Armadura', atqMIN:171, atqMAX:9999, value: '28 LET'},
>	
>	{arm: 'Armadura Ligera', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Ligera', atqMIN:11, atqMAX:35, value: '-'},
>	{arm: 'Armadura Ligera', atqMIN:36, atqMAX:75, value: '0'},
>	{arm: 'Armadura Ligera', atqMIN:76, atqMAX:80, value: '1'},
>	{arm: 'Armadura Ligera', atqMIN:81, atqMAX:85, value: '2'},
>	{arm: 'Armadura Ligera', atqMIN:86, atqMAX:90, value: '3'},
>	{arm: 'Armadura Ligera', atqMIN:91, atqMAX:95, value: '4'},
>	{arm: 'Armadura Ligera', atqMIN:96, atqMAX:100, value: '5'},
>	{arm: 'Armadura Ligera', atqMIN:101, atqMAX:105, value: '6'},
>	{arm: 'Armadura Ligera', atqMIN:106, atqMAX:110, value: '7 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:111, atqMAX:115, value: '8 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:116, atqMAX:120, value: '9 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:121, atqMAX:125, value: '10 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:126, atqMAX:130, value: '11 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:131, atqMAX:135, value: '12 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:136, atqMAX:140, value: '13 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:141, atqMAX:145, value: '14 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:146, atqMAX:150, value: '15 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:151, atqMAX:155, value: '16 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:156, atqMAX:160, value: '18 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:161, atqMAX:165, value: '20 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:166, atqMAX:170, value: '22 LET'},
>	{arm: 'Armadura Ligera', atqMIN:171, atqMAX:9999, value: '24 LET'},
>	
>	{arm: 'Armadura Media', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Media', atqMIN:11, atqMAX:35, value: '-'},
>	{arm: 'Armadura Media', atqMIN:36, atqMAX:85, value: '0'},
>	{arm: 'Armadura Media', atqMIN:86, atqMAX:90, value: '1'},
>	{arm: 'Armadura Media', atqMIN:91, atqMAX:95, value: '2'},
>	{arm: 'Armadura Media', atqMIN:96, atqMAX:100, value: '3'},
>	{arm: 'Armadura Media', atqMIN:101, atqMAX:105, value: '4'},
>	{arm: 'Armadura Media', atqMIN:106, atqMAX:110, value: '5'},
>	{arm: 'Armadura Media', atqMIN:111, atqMAX:115, value: '6'},
>	{arm: 'Armadura Media', atqMIN:116, atqMAX:120, value: '7 SUP'},
>	{arm: 'Armadura Media', atqMIN:121, atqMAX:125, value: '8 SUP'},
>	{arm: 'Armadura Media', atqMIN:126, atqMAX:130, value: '9 SUP'},
>	{arm: 'Armadura Media', atqMIN:131, atqMAX:135, value: '10 LEV'},
>	{arm: 'Armadura Media', atqMIN:136, atqMAX:140, value: '11 LEV'},
>	{arm: 'Armadura Media', atqMIN:141, atqMAX:145, value: '12 LEV'},
>	{arm: 'Armadura Media', atqMIN:146, atqMAX:150, value: '13 MOD'},
>	{arm: 'Armadura Media', atqMIN:151, atqMAX:155, value: '14 MOD'},
>	{arm: 'Armadura Media', atqMIN:156, atqMAX:160, value: '15 MOD'},
>	{arm: 'Armadura Media', atqMIN:161, atqMAX:165, value: '16 GRA'},
>	{arm: 'Armadura Media', atqMIN:166, atqMAX:170, value: '18 GRA'},
>	{arm: 'Armadura Media', atqMIN:171, atqMAX:9999, value: '20 LET'},
>	
>	{arm: 'Armadura Pesada', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Pesada', atqMIN:11, atqMAX:35, value: '-'},
>	{arm: 'Armadura Pesada', atqMIN:36, atqMAX:95, value: '0'},
>	{arm: 'Armadura Pesada', atqMIN:95, atqMAX:100, value: '1'},
>	{arm: 'Armadura Pesada', atqMIN:101, atqMAX:105, value: '2'},
>	{arm: 'Armadura Pesada', atqMIN:106, atqMAX:110, value: '3'},
>	{arm: 'Armadura Pesada', atqMIN:111, atqMAX:115, value: '4'},
>	{arm: 'Armadura Pesada', atqMIN:116, atqMAX:120, value: '5'},
>	{arm: 'Armadura Pesada', atqMIN:121, atqMAX:125, value: '6'},
>	{arm: 'Armadura Pesada', atqMIN:126, atqMAX:130, value: '7 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:131, atqMAX:135, value: '8 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:136, atqMAX:140, value: '9 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:141, atqMAX:145, value: '10 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:146, atqMAX:150, value: '11 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:151, atqMAX:155, value: '12 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:156, atqMAX:160, value: '13 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:161, atqMAX:165, value: '14 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:166, atqMAX:170, value: '15 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:171, atqMAX:9999, value: '16 GRA'}
>]; 
>
>const tablaArea = [
>	{arm: 'Sin Armadura', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Sin Armadura', atqMIN:11, atqMAX:55, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:56, atqMAX:60, value: '1'},
>	{arm: 'Sin Armadura', atqMIN:61, atqMAX:65, value: '2'},
>	{arm: 'Sin Armadura', atqMIN:66, atqMAX:70, value: '3'},
>	{arm: 'Sin Armadura', atqMIN:71, atqMAX:75, value: '4'},
>	{arm: 'Sin Armadura', atqMIN:76, atqMAX:80, value: '5'},
>	{arm: 'Sin Armadura', atqMIN:81, atqMAX:85, value: '6'},
>	{arm: 'Sin Armadura', atqMIN:86, atqMAX:90, value: '7 SUP'},
>	{arm: 'Sin Armadura', atqMIN:91, atqMAX:95, value: '8 SUP'},
>	{arm: 'Sin Armadura', atqMIN:96, atqMAX:100, value: '9 SUP'},
>	{arm: 'Sin Armadura', atqMIN:101, atqMAX:105, value: '10 SUP'},
>	{arm: 'Sin Armadura', atqMIN:106, atqMAX:110, value: '11 SUP'},
>	{arm: 'Sin Armadura', atqMIN:111, atqMAX:115, value: '12 LEV'},
>	{arm: 'Sin Armadura', atqMIN:116, atqMAX:120, value: '13 LEV'},
>	{arm: 'Sin Armadura', atqMIN:121, atqMAX:125, value: '14 LEV'},
>	{arm: 'Sin Armadura', atqMIN:126, atqMAX:130, value: '15 LEV'},
>	{arm: 'Sin Armadura', atqMIN:131, atqMAX:135, value: '16 MOD'},
>	{arm: 'Sin Armadura', atqMIN:136, atqMAX:140, value: '18 MOD'},
>	{arm: 'Sin Armadura', atqMIN:141, atqMAX:145, value: '20 MOD'},
>	{arm: 'Sin Armadura', atqMIN:146, atqMAX:150, value: '21 MOD'},
>	{arm: 'Sin Armadura', atqMIN:151, atqMAX:155, value: '22 MOD'},
>	{arm: 'Sin Armadura', atqMIN:156, atqMAX:160, value: '24 GRA'},
>	{arm: 'Sin Armadura', atqMIN:161, atqMAX:165, value: '26 GRA'},
>	{arm: 'Sin Armadura', atqMIN:166, atqMAX:170, value: '28 GRA'},
>	{arm: 'Sin Armadura', atqMIN:171, atqMAX:9999, value: '34 LET'},
>	
>	{arm: 'Armadura Ligera', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Ligera', atqMIN:11, atqMAX:85, value: '0'},
>	{arm: 'Armadura Ligera', atqMIN:86, atqMAX:90, value: '1'},
>	{arm: 'Armadura Ligera', atqMIN:91, atqMAX:95, value: '2'},
>	{arm: 'Armadura Ligera', atqMIN:96, atqMAX:100, value: '3'},
>	{arm: 'Armadura Ligera', atqMIN:101, atqMAX:105, value: '4 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:106, atqMAX:110, value: '5 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:111, atqMAX:115, value: '6 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:116, atqMAX:120, value: '7 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:121, atqMAX:125, value: '8 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:126, atqMAX:130, value: '10 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:131, atqMAX:135, value: '12 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:136, atqMAX:140, value: '13 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:141, atqMAX:145, value: '14 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:146, atqMAX:150, value: '16 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:151, atqMAX:155, value: '18 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:156, atqMAX:160, value: '20 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:161, atqMAX:165, value: '22 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:166, atqMAX:170, value: '24 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:171, atqMAX:9999, value: '26 LET'},
>	
>	{arm: 'Armadura Media', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Media', atqMIN:11, atqMAX:85, value: '0'},
>	{arm: 'Armadura Media', atqMIN:86, atqMAX:90, value: '1'},
>	{arm: 'Armadura Media', atqMIN:91, atqMAX:95, value: '2'},
>	{arm: 'Armadura Media', atqMIN:96, atqMAX:100, value: '3'},
>	{arm: 'Armadura Media', atqMIN:101, atqMAX:105, value: '4'},
>	{arm: 'Armadura Media', atqMIN:106, atqMAX:110, value: '5 SUP'},
>	{arm: 'Armadura Media', atqMIN:111, atqMAX:115, value: '6 SUP'},
>	{arm: 'Armadura Media', atqMIN:116, atqMAX:120, value: '7 SUP'},
>	{arm: 'Armadura Media', atqMIN:121, atqMAX:125, value: '8 SUP'},
>	{arm: 'Armadura Media', atqMIN:126, atqMAX:130, value: '8 LEV'},
>	{arm: 'Armadura Media', atqMIN:131, atqMAX:135, value: '9 LEV'},
>	{arm: 'Armadura Media', atqMIN:136, atqMAX:140, value: '10 LEV'},
>	{arm: 'Armadura Media', atqMIN:141, atqMAX:145, value: '10 MOD'},
>	{arm: 'Armadura Media', atqMIN:146, atqMAX:150, value: '12 MOD'},
>	{arm: 'Armadura Media', atqMIN:151, atqMAX:155, value: '14 MOD'},
>	{arm: 'Armadura Media', atqMIN:156, atqMAX:160, value: '15 MOD'},
>	{arm: 'Armadura Media', atqMIN:161, atqMAX:165, value: '16 GRA'},
>	{arm: 'Armadura Media', atqMIN:166, atqMAX:170, value: '18 GRA'},
>	{arm: 'Armadura Media', atqMIN:171, atqMAX:9999, value: '20 LET'},
>	
>	{arm: 'Armadura Pesada', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Pesada', atqMIN:11, atqMAX:85, value: '0'},
>	{arm: 'Armadura Pesada', atqMIN:86, atqMAX:90, value: '1'},
>	{arm: 'Armadura Pesada', atqMIN:91, atqMAX:95, value: '2'},
>	{arm: 'Armadura Pesada', atqMIN:96, atqMAX:100, value: '3'},
>	{arm: 'Armadura Pesada', atqMIN:101, atqMAX:105, value: '4'},
>	{arm: 'Armadura Pesada', atqMIN:106, atqMAX:110, value: '5'},
>	{arm: 'Armadura Pesada', atqMIN:111, atqMAX:115, value: '5 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:116, atqMAX:120, value: '6 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:121, atqMAX:125, value: '7 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:126, atqMAX:130, value: '7 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:131, atqMAX:135, value: '7 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:136, atqMAX:140, value: '8 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:141, atqMAX:145, value: '9 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:146, atqMAX:150, value: '9 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:151, atqMAX:155, value: '10 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:156, atqMAX:160, value: '12 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:161, atqMAX:165, value: '14 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:166, atqMAX:170, value: '16 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:171, atqMAX:9999, value: '18 LET'}
>];
>
>const tablaRayo = [
>	{arm: 'Sin Armadura', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Sin Armadura', atqMIN:11, atqMAX:75, value: '-'},
>	{arm: 'Sin Armadura', atqMIN:76, atqMAX:90, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:91, atqMAX:95, value: '8 SUP'},
>	{arm: 'Sin Armadura', atqMIN:96, atqMAX:100, value: '10 SUP'},
>	{arm: 'Sin Armadura', atqMIN:101, atqMAX:105, value: '11 SUP'},
>	{arm: 'Sin Armadura', atqMIN:106, atqMAX:110, value: '12 LEV'},
>	{arm: 'Sin Armadura', atqMIN:111, atqMAX:115, value: '14 LEV'},
>	{arm: 'Sin Armadura', atqMIN:116, atqMAX:120, value: '16 LEV'},
>	{arm: 'Sin Armadura', atqMIN:121, atqMAX:125, value: '18 MOD'},
>	{arm: 'Sin Armadura', atqMIN:126, atqMAX:130, value: '21 MOD'},
>	{arm: 'Sin Armadura', atqMIN:131, atqMAX:135, value: '24 MOD'},
>	{arm: 'Sin Armadura', atqMIN:136, atqMAX:140, value: '27 GRA'},
>	{arm: 'Sin Armadura', atqMIN:141, atqMAX:145, value: '30 GRA'},
>	{arm: 'Sin Armadura', atqMIN:146, atqMAX:150, value: '32 GRA'},
>	{arm: 'Sin Armadura', atqMIN:151, atqMAX:155, value: '34 LET'},
>	{arm: 'Sin Armadura', atqMIN:156, atqMAX:160, value: '36 LET'},
>	{arm: 'Sin Armadura', atqMIN:161, atqMAX:165, value: '38 LET'},
>	{arm: 'Sin Armadura', atqMIN:166, atqMAX:170, value: '40 LET'},
>	{arm: 'Sin Armadura', atqMIN:171, atqMAX:9999, value: '42 LET'},
>	
>	{arm: 'Armadura Ligera', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Ligera', atqMIN:11, atqMAX:65, value: '-'},
>	{arm: 'Armadura Ligera', atqMIN:66, atqMAX:80, value: '0'},
>	{arm: 'Armadura Ligera', atqMIN:81, atqMAX:85, value: '1'},
>	{arm: 'Armadura Ligera', atqMIN:86, atqMAX:90, value: '2'},
>	{arm: 'Armadura Ligera', atqMIN:91, atqMAX:95, value: '3'},
>	{arm: 'Armadura Ligera', atqMIN:96, atqMAX:100, value: '4'},
>	{arm: 'Armadura Ligera', atqMIN:101, atqMAX:105, value: '5 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:106, atqMAX:110, value: '6 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:111, atqMAX:115, value: '8 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:116, atqMAX:120, value: '10 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:121, atqMAX:125, value: '12 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:126, atqMAX:130, value: '14 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:131, atqMAX:135, value: '16 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:136, atqMAX:140, value: '17 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:141, atqMAX:145, value: '18 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:146, atqMAX:150, value: '19 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:151, atqMAX:155, value: '20 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:156, atqMAX:160, value: '22 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:161, atqMAX:165, value: '25 LET'},
>	{arm: 'Armadura Ligera', atqMIN:166, atqMAX:170, value: '28 LET'},
>	{arm: 'Armadura Ligera', atqMIN:171, atqMAX:9999, value: '31 LET'},
>	
>	{arm: 'Armadura Media', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Media', atqMIN:11, atqMAX:55, value: '-'},
>	{arm: 'Armadura Media', atqMIN:56, atqMAX:65, value: '0'},
>	{arm: 'Armadura Media', atqMIN:66, atqMAX:70, value: '1'},
>	{arm: 'Armadura Media', atqMIN:71, atqMAX:90, value: '3'},
>	{arm: 'Armadura Media', atqMIN:91, atqMAX:95, value: '4'},
>	{arm: 'Armadura Media', atqMIN:96, atqMAX:100, value: '5 SUP'},
>	{arm: 'Armadura Media', atqMIN:101, atqMAX:105, value: '6 SUP'},
>	{arm: 'Armadura Media', atqMIN:106, atqMAX:110, value: '7 SUP'},
>	{arm: 'Armadura Media', atqMIN:111, atqMAX:115, value: '8 SUP'},
>	{arm: 'Armadura Media', atqMIN:116, atqMAX:120, value: '10 LEV'},
>	{arm: 'Armadura Media', atqMIN:121, atqMAX:125, value: '12 LEV'},
>	{arm: 'Armadura Media', atqMIN:126, atqMAX:130, value: '14 LEV'},
>	{arm: 'Armadura Media', atqMIN:131, atqMAX:135, value: '15 LEV'},
>	{arm: 'Armadura Media', atqMIN:136, atqMAX:140, value: '16 MOD'},
>	{arm: 'Armadura Media', atqMIN:141, atqMAX:145, value: '17 MOD'},
>	{arm: 'Armadura Media', atqMIN:146, atqMAX:150, value: '18 MOD'},
>	{arm: 'Armadura Media', atqMIN:151, atqMAX:155, value: '20 MOD'},
>	{arm: 'Armadura Media', atqMIN:156, atqMAX:160, value: '22 GRA'},
>	{arm: 'Armadura Media', atqMIN:161, atqMAX:165, value: '24 GRA'},
>	{arm: 'Armadura Media', atqMIN:166, atqMAX:170, value: '26 LET'},
>	{arm: 'Armadura Media', atqMIN:171, atqMAX:9999, value: '28 LET'},
>	
>	{arm: 'Armadura Pesada', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Pesada', atqMIN:11, atqMAX:45, value: '-'},
>	{arm: 'Armadura Pesada', atqMIN:46, atqMAX:65, value: '0'},
>	{arm: 'Armadura Pesada', atqMIN:66, atqMAX:75, value: '1'},
>	{arm: 'Armadura Pesada', atqMIN:76, atqMAX:85, value: '2'},
>	{arm: 'Armadura Pesada', atqMIN:86, atqMAX:95, value: '3'},
>	{arm: 'Armadura Pesada', atqMIN:96, atqMAX:100, value: '4 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:101, atqMAX:105, value: '5 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:106, atqMAX:110, value: '6 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:111, atqMAX:115, value: '7 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:116, atqMAX:120, value: '8 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:121, atqMAX:125, value: '12 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:126, atqMAX:130, value: '13 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:131, atqMAX:135, value: '14 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:136, atqMAX:140, value: '15 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:141, atqMAX:145, value: '16 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:146, atqMAX:150, value: '17 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:151, atqMAX:155, value: '20 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:156, atqMAX:160, value: '22 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:161, atqMAX:165, value: '24 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:166, atqMAX:170, value: '26 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:171, atqMAX:9999, value: '26 LET'}
>];
>
>const tablaBestias = [
>	{arm: 'Sin Armadura', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Sin Armadura', atqMIN:11, atqMAX:40, value: '-'},
>	{arm: 'Sin Armadura', atqMIN:41, atqMAX:45, value: '0'},
>	{arm: 'Sin Armadura', atqMIN:46, atqMAX:50, value: '1'},
>	{arm: 'Sin Armadura', atqMIN:51, atqMAX:55, value: '2'},
>	{arm: 'Sin Armadura', atqMIN:56, atqMAX:60, value: '4'},
>	{arm: 'Sin Armadura', atqMIN:61, atqMAX:65, value: '5'},
>	{arm: 'Sin Armadura', atqMIN:66, atqMAX:70, value: '6'},
>	{arm: 'Sin Armadura', atqMIN:71, atqMAX:75, value: '8'},
>	{arm: 'Sin Armadura', atqMIN:76, atqMAX:80, value: '9 SUP'},
>	{arm: 'Sin Armadura', atqMIN:81, atqMAX:85, value: '10 SUP'},
>	{arm: 'Sin Armadura', atqMIN:86, atqMAX:90, value: '12 SUP'},
>	{arm: 'Sin Armadura', atqMIN:91, atqMAX:95, value: '13 LEV'},
>	{arm: 'Sin Armadura', atqMIN:96, atqMAX:100, value: '14 LEV'},
>	{arm: 'Sin Armadura', atqMIN:101, atqMAX:105, value: '15 LEV'},
>	{arm: 'Sin Armadura', atqMIN:106, atqMAX:110, value: '17 MOD'},
>	{arm: 'Sin Armadura', atqMIN:111, atqMAX:115, value: '19 MOD'},
>	{arm: 'Sin Armadura', atqMIN:116, atqMAX:120, value: '23 GRA'},
>	{arm: 'Sin Armadura', atqMIN:121, atqMAX:125, value: '26 GRA'},
>	{arm: 'Sin Armadura', atqMIN:126, atqMAX:130, value: '28 LET'},
>	{arm: 'Sin Armadura', atqMIN:131, atqMAX:135, value: '30 LET'},
>	{arm: 'Sin Armadura', atqMIN:136, atqMAX:140, value: '32 LET'},
>	{arm: 'Sin Armadura', atqMIN:141, atqMAX:145, value: '34 LET'},
>	{arm: 'Sin Armadura', atqMIN:146, atqMAX:150, value: '36 LET'},
>	{arm: 'Sin Armadura', atqMIN:151, atqMAX:155, value: '38 LET'},
>	{arm: 'Sin Armadura', atqMIN:156, atqMAX:160, value: '40 LET'},
>	{arm: 'Sin Armadura', atqMIN:161, atqMAX:165, value: '42 LET'},
>	{arm: 'Sin Armadura', atqMIN:166, atqMAX:170, value: '44 LET'},
>	{arm: 'Sin Armadura', atqMIN:171, atqMAX:9999, value: '46 LET'},
>	
>	{arm: 'Armadura Ligera', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Ligera', atqMIN:11, atqMAX:40, value: '-'},
>	{arm: 'Armadura Ligera', atqMIN:41, atqMAX:60, value: '0'},
>	{arm: 'Armadura Ligera', atqMIN:61, atqMAX:65, value: '1'},
>	{arm: 'Armadura Ligera', atqMIN:66, atqMAX:70, value: '2'},
>	{arm: 'Armadura Ligera', atqMIN:71, atqMAX:75, value: '3'},
>	{arm: 'Armadura Ligera', atqMIN:76, atqMAX:80, value: '5'},
>	{arm: 'Armadura Ligera', atqMIN:81, atqMAX:85, value: '7'},
>	{arm: 'Armadura Ligera', atqMIN:86, atqMAX:90, value: '8'},
>	{arm: 'Armadura Ligera', atqMIN:91, atqMAX:95, value: '9 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:96, atqMAX:100, value: '10 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:101, atqMAX:105, value: '11 SUP'},
>	{arm: 'Armadura Ligera', atqMIN:106, atqMAX:110, value: '12 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:111, atqMAX:115, value: '13 LEV'},
>	{arm: 'Armadura Ligera', atqMIN:116, atqMAX:120, value: '14 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:121, atqMAX:125, value: '16 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:126, atqMAX:130, value: '18 MOD'},
>	{arm: 'Armadura Ligera', atqMIN:131, atqMAX:135, value: '20 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:136, atqMAX:140, value: '22 GRA'},
>	{arm: 'Armadura Ligera', atqMIN:141, atqMAX:145, value: '24 LET'},
>	{arm: 'Armadura Ligera', atqMIN:146, atqMAX:150, value: '26 LET'},
>	{arm: 'Armadura Ligera', atqMIN:151, atqMAX:155, value: '28 LET'},
>	{arm: 'Armadura Ligera', atqMIN:156, atqMAX:160, value: '30 LET'},
>	{arm: 'Armadura Ligera', atqMIN:161, atqMAX:165, value: '32 LET'},
>	{arm: 'Armadura Ligera', atqMIN:166, atqMAX:170, value: '34 LET'},
>	{arm: 'Armadura Ligera', atqMIN:171, atqMAX:9999, value: '36 LET'},
>	
>	{arm: 'Armadura Media', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Media', atqMIN:11, atqMAX:40, value: '-'},
>	{arm: 'Armadura Media', atqMIN:41, atqMAX:60, value: '0'},
>	{arm: 'Armadura Media', atqMIN:61, atqMAX:65, value: '1'},
>	{arm: 'Armadura Media', atqMIN:66, atqMAX:70, value: '2'},
>	{arm: 'Armadura Media', atqMIN:71, atqMAX:75, value: '3'},
>	{arm: 'Armadura Media', atqMIN:76, atqMAX:80, value: '4'},
>	{arm: 'Armadura Media', atqMIN:81, atqMAX:85, value: '5'},
>	{arm: 'Armadura Media', atqMIN:86, atqMAX:90, value: '6'},
>	{arm: 'Armadura Media', atqMIN:91, atqMAX:95, value: '7'},
>	{arm: 'Armadura Media', atqMIN:96, atqMAX:100, value: '8 SUP'},
>	{arm: 'Armadura Media', atqMIN:101, atqMAX:105, value: '9 SUP'},
>	{arm: 'Armadura Media', atqMIN:106, atqMAX:110, value: '10 SUP'},
>	{arm: 'Armadura Media', atqMIN:111, atqMAX:115, value: '11 LEV'},
>	{arm: 'Armadura Media', atqMIN:116, atqMAX:120, value: '12 LEV'},
>	{arm: 'Armadura Media', atqMIN:121, atqMAX:125, value: '14 LEV'},
>	{arm: 'Armadura Media', atqMIN:126, atqMAX:130, value: '16 MOD'},
>	{arm: 'Armadura Media', atqMIN:131, atqMAX:135, value: '18 MOD'},
>	{arm: 'Armadura Media', atqMIN:136, atqMAX:140, value: '20 GRA'},
>	{arm: 'Armadura Media', atqMIN:141, atqMAX:145, value: '22 GRA'},
>	{arm: 'Armadura Media', atqMIN:146, atqMAX:150, value: '24 GRA'},
>	{arm: 'Armadura Media', atqMIN:151, atqMAX:155, value: '26 LET'},
>	{arm: 'Armadura Media', atqMIN:156, atqMAX:160, value: '28 LET'},
>	{arm: 'Armadura Media', atqMIN:161, atqMAX:165, value: '30 LET'},
>	{arm: 'Armadura Media', atqMIN:166, atqMAX:170, value: '32 LET'},
>	{arm: 'Armadura Media', atqMIN:171, atqMAX:9999, value: '34 LET'},
>	
>	{arm: 'Armadura Pesada', atqMIN:-9999, atqMAX:10, value: 'posible pifia'},
>	{arm: 'Armadura Pesada', atqMIN:11, atqMAX:40, value: '-'},
>	{arm: 'Armadura Pesada', atqMIN:41, atqMAX:55, value: '0'},
>	{arm: 'Armadura Pesada', atqMIN:56, atqMAX:65, value: '1'},
>	{arm: 'Armadura Pesada', atqMIN:66, atqMAX:70, value: '2'},
>	{arm: 'Armadura Pesada', atqMIN:71, atqMAX:75, value: '3'},
>	{arm: 'Armadura Pesada', atqMIN:76, atqMAX:80, value: '4'},
>	{arm: 'Armadura Pesada', atqMIN:81, atqMAX:85, value: '5'},
>	{arm: 'Armadura Pesada', atqMIN:86, atqMAX:95, value: '6'},
>	{arm: 'Armadura Pesada', atqMIN:96, atqMAX:100, value: '7'},
>	{arm: 'Armadura Pesada', atqMIN:101, atqMAX:105, value: '7 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:106, atqMAX:110, value: '8 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:111, atqMAX:115, value: '9 SUP'},
>	{arm: 'Armadura Pesada', atqMIN:116, atqMAX:120, value: '10 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:121, atqMAX:125, value: '12 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:126, atqMAX:130, value: '14 LEV'},
>	{arm: 'Armadura Pesada', atqMIN:131, atqMAX:135, value: '16 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:136, atqMAX:140, value: '18 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:141, atqMAX:145, value: '20 MOD'},
>	{arm: 'Armadura Pesada', atqMIN:146, atqMAX:150, value: '22 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:151, atqMAX:155, value: '24 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:156, atqMAX:160, value: '26 GRA'},
>	{arm: 'Armadura Pesada', atqMIN:161, atqMAX:165, value: '28 LET'},
>	{arm: 'Armadura Pesada', atqMIN:166, atqMAX:170, value: '30 LET'},
>	{arm: 'Armadura Pesada', atqMIN:171, atqMAX:9999, value: '32 LET'}
>];
>
>function getDano(){
>		let atqTotal = context.bound.ataqueF;
>		const armTipo = context.bound.armadura;
>		const atqTipo = context.bound.atqTipo;
>		let resultado = "";
>		 
>		switch(atqTipo){
>			case 'Filo':
>				resultado = tablaFilo.find(row =>
>				row.arm === armTipo && 
>				atqTotal >= row.atqMIN &&
>				atqTotal <= row.atqMAX
>				);
>				break;
>			case 'Contundente':
>				resultado = tablaContundente.find(row =>
>				row.arm === armTipo && 
>				atqTotal >= row.atqMIN &&
>				atqTotal <= row.atqMAX
>				);
>				break;
>			case 'Proyectil':
>				resultado = tablaProyectil.find(row =>
>				row.arm === armTipo && 
>				atqTotal >= row.atqMIN &&
>				atqTotal <= row.atqMAX
>				);
>				break;
>			case 'Desarmado/Presa':
>				resultado = tablaDesarmado.find(row =>
>				row.arm === armTipo && 
>				atqTotal >= row.atqMIN &&
>				atqTotal <= row.atqMAX
>				);
>				break;
>			case 'Sortilegio de Area':
>				resultado = tablaArea.find(row =>
>				row.arm === armTipo && 
>				atqTotal >= row.atqMIN &&
>				atqTotal <= row.atqMAX
>				);
>				break;
>			case 'Sortilegio de Rayo':
>				resultado = tablaRayo.find(row =>
>				row.arm === armTipo && 
>				atqTotal >= row.atqMIN &&
>				atqTotal <= row.atqMAX
>				);
>				break;
>			case 'Bestias':
>				resultado = tablaBestias.find(row =>
>				row.arm === armTipo && 
>				atqTotal >= row.atqMIN &&
>				atqTotal <= row.atqMAX
>				);
>				break;
>		}
>		
>		return resultado ? resultado.value : null;
>}
>
>return `${getDano()}`;
>```
>```meta-bind-js-view
>{aturdido} as aturdido
>save to {aturdidoM}
>hidden
>---
>let estadoMen = "";
>if(context.bound.aturdido){
>	estadoMen = "- No acciones completas \n - Parada 1/2 BC"
>}
>return estadoMen;
>```
>```meta-bind-js-view
>{sorprendido} as sorprendido
>save to {sorprendidoM}
>hidden
>---
>let estadoMen = "";
>if(context.bound.sorprendido){
>	estadoMen = "- No puede atacar \n - Acciones gratuitas o parciales \n - No DEF escudo \n - Arma de mano +10 CRIT"
>}
>return estadoMen;
>```
>```meta-bind-js-view
>{derribadoATQ} as derribadoATQ
>save to {derribadoATQM}
>hidden
>---
>let estadoMen = "";
>if(context.bound.derribadoATQ){
>	estadoMen = "- No armas 2 manos \n - Levantarse = Accion completa"
>}
>return estadoMen;
>```
>```meta-bind-js-view
>{derribadoDEF} as derribadoDEF
>save to {derribadoDEFM}
>hidden
>---
>let estadoMen = "";
>if(context.bound.derribadoDEF){
>	estadoMen = "- Terreno elevado"
>}
>return estadoMen;
>```
>```meta-bind-js-view
>{retenidoATQ} as retenidoATQ
>save to {retenidoATQM}
>hidden
>---
>let estadoMen = "";
>if(context.bound.retenidoATQ){
>	estadoMen = "- Solo armas cortas o de mano"
>}
>return estadoMen;
>```
>|Resultado|Total Ataque|Tipo de ataque|Aturdido|Sorprendido|Derribado (ATQ)|Derribado (DEF)|Retenido (ATQ)|
>|:---:|:---:|:---:|---|---|---|---|---|
>|`VIEW[{resultadoF}]`|`VIEW[{ataqueF}]`|`VIEW[{atqTipo}]`|`VIEW[{aturdidoM}]`|`VIEW[{sorprendidoM}]`|`VIEW[{derribadoATQM}]`|`VIEW[{derribadoDEFM}]`|`VIEW[{retenidoATQM}]`|
>

> [!info]- Calculadora de Habilidades  
> Bonificacion de Habilidad
> ---
> Bonus Total: `INPUT[number(placeholder(______)):BonusHabilidad]`
>  Numero de Ayuda: `INPUT[number(placeholder(______)):ayuda]`
>   Numero de Ayuda Excepcional: `INPUT[number(placeholder(______)):ayudaE]`
>  
>  Dificultad
> ---
> ```meta-bind
>INPUT[select(
>		option(Normal),
>		option(Desafiante),
>		option(Dificil),
>		option(Muy dificil),
>		option(Extremadamente dificil),
>		option(Heroica),
>		option(Demencial)
>		):dificultad]
>```
> ```meta-bind-js-view
> {BonusHabilidad} as BonusHabilidad
> {dificultad} as dificultad
> {ayuda} as ayuda
> {ayudaE} as ayudaE
> save to {resultadoHabilidad}
> hidden
> ---
> let bonusH = context.bound.BonusHabilidad;
> bonusH += ((context.bound.ayuda ?? 0) * 10);
>  bonusH += (context.bound.ayudaE * 20);
> if(context.bound.dificultad === 'Desafiante'){
> 	bonusH -= 10 
> } else if(context.bound.dificultad === 'Dificil'){
> 	bonusH -= 20
> } else if(context.bound.dificultad === 'Muy dificil'){
> 	bonusH -= 30
> } else if(context.bound.dificultad === 'Extremadamente dificil'){
> 	bonusH -= 40
> } else if(context.bound.dificultad === 'Heroica'){
> 	bonusH -= 50
> } else if(context.bound.dificultad === 'Demencial'){
> 	bonusH -= 70
> }
> return bonusH;
> ```
> ```meta-bind-js-view
> {resultadoHabilidad} as habilidadT
> save to {resultadoT}
> hidden
> ---
> let resultadoT = "";
> if(context.bound.habilidadT <= 4){
> 	resultadoT = "Fallo Critico";
> } else if (context.bound.habilidadT <= 74){
> 	resultadoT = "Fallo";
> } else if (context.bound.habilidadT <= 99){
> 	resultadoT = "Exito parcial";
> } else if (context.bound.habilidadT <= 174){
> 	resultadoT = "Exito";
> } else {
> 	resultadoT = "Exito excepcional";
> }
> return resultadoT;
> ```
> Resultado
> ---
> |Resultado Total| Resultado Habilidad|
> |---|---|
> |`VIEW[{resultadoHabilidad}]`|`VIEW[{resultadoT}]`|

> [!tip]- Calculadora de Sortilegios  
>  Bonificacion de Habilidad
> ---
> Bonus Total: `INPUT[number(placeholder(______)):bonusMagia]`
> 
> Modificadores de Sortilegio 
>---
>|Modificador Generales|    |Modificador Distancia|     |
>|---|:---:|---|:---:|
>|Inmovil|`INPUT[toggle:inmovil]`|Contacto|`INPUT[toggle:contactoS]`|
>|Improvisado|`INPUT[toggle:improvisado]`|Hasta 3 metros|`INPUT[toggle:tresS]`|
>|   |  |De 4 a 15 metros|`INPUT[toggle:quinceS]`|
>|Concentracion|`INPUT[number(placeholder(______)):concentracionS]`|De 16 a 30 metros|`INPUT[toggle:treintaS]`|
>|   |  |De 31 a 90 metros|`INPUT[toggle:noventaS]`|
>|    | |Mas de 90 metros|`INPUT[toggle:noventaMas]`|
>
>```meta-bind-js-view
>{bonusMagia} as bonusMagia
>{inmovil} as inmovil
>{contactoS} as contactoS
>{improvisado} as improvisado
>{concentracionS} as concentracionS
>{tresS} as tresS
>{noventaMas} as noventaMas
>{treintaS} as treintaS
>{noventaS} as noventaS
>save to {ataqueSor}
>hidden
>---
>let atqSor = context.bound.bonusMagia;
> if(context.bound.inmovil){
> 	atqSor += 10;
> }
>  if(context.bound.improvisado){
> 	atqSor -= 10;
> }
>   if(context.bound.concentracionS > 0 && context.bound.concentracionS < 4){
> 	atqSor += (context.bound.concentracionS * 10);
> } else if(context.bound.concentracionS >= 4) {
> 	atqSor += 40;
> }
> if(context.bound.contactoS){
> 	atqSor += 30;
> }
>  if(context.bound.tresS){
> 	atqSor += 10;
> }
> if(context.bound.treintaS){
> 	atqSor -= 10;
> }
>  if(context.bound.noventaS){
> 	atqSor -= 20;
> }
> if(context.bound.noventaMas){
> 	atqSor -= 30;
> }
> return atqSor;
>```
>```meta-bind-js-view
> {ataqueSor} as ataqueSor
> save to {resultadoSor}
> hidden
> ---
> let resultadoSor = "";
> if(context.bound.ataqueSor <= 25){
> 	resultadoSor = "Fallo Sortilegio";
> } else if (context.bound.ataqueSor <= 50){
> 	resultadoSor = "Exito parcial";
> } else if (context.bound.ataqueSor <= 150){
> 	resultadoSor = "Exito";
> }else {
> 	resultadoSor = "Exito excepcional";
> }
> return resultadoSor;
> ```
> ```meta-bind-js-view
> {ataqueSor} as ataqueSor
> save to {resultadoTextoSor}
> hidden
> ---
> let resultadoSor = "";
> if(context.bound.ataqueSor <= 25){
> 	resultadoSor = "Tirar en tabla de fallo sortilegio";
> } else if (context.bound.ataqueSor <= 50){
> 	resultadoSor = "Tirada de salvacion superada automaticamente \nSi no elegir uno redondeado hacia abajo:  \n-Duracion hechizo 1/2  \n-Area de efecto 1/2 \n-No tiene efecto pero no pierde PM";
> } else if (context.bound.ataqueSor <= 150){
> 	resultadoSor = "Hechizo se ejecuta sin complicaciones";
> }else {
> 	resultadoSor = "Elegir una de las siguiente opciones: \n-Sortilegio cuesta 1/2 PM\n-Anadir una distorsion gratis cuyo coste no sea mas que 1/2 del hechizo ";
> }
> return resultadoSor;
> ```
> ```meta-bind-js-view
> {ataqueSor} as ataqueSor
> save to {resultadoSalvacion}
> hidden
> ---
> let ataqueMa = context.bound.ataqueSor;
>  let resultado = "";
> const tablaSalvacion = [
>	{atqMIN:-9999, atqMAX:25, value: '-'},
>	{atqMIN:26, atqMAX:50, value: '-'},
>	{atqMIN:51, atqMAX:80, value: '50'},
>	{atqMIN:81, atqMAX:95, value: '60'},
>	{atqMIN:96, atqMAX:105, value: '65'},
>	{atqMIN:106, atqMAX:110, value: '70'},
>	{atqMIN:111, atqMAX:120, value: '75'},
>	{atqMIN:121, atqMAX:130, value: '80'},
>	{atqMIN:131, atqMAX:135, value: '85'},
>	{atqMIN:136, atqMAX:140, value: '90'},
>	{atqMIN:141, atqMAX:145, value: '95'},
>	{atqMIN:146, atqMAX:150, value: '100'},
>	{atqMIN:151, atqMAX:155, value: '105'},
>	{atqMIN:156, atqMAX:160, value: '110'},
>	{atqMIN:161, atqMAX:165, value: '120'},
>	{atqMIN:166, atqMAX:170, value: '130'},
>	{atqMIN:171, atqMAX:175, value: '140'},
>	{atqMIN:176, atqMAX:9999, value: '150'}
>	];
>
>resultado = tablaSalvacion.find(row =>
>	ataqueMa >= row.atqMIN &&
>	ataqueMa <= row.atqMAX
>	);
>return resultado ? resultado.value : null;
>```
>| Resultado Total| Resultado Sotilegio | Salvacion | Efectos extra|
>|---|---|---|---|
>|`VIEW[{ataqueSor}]`| `VIEW[{resultadoSor}]`|`VIEW[{resultadoSalvacion}]`|`VIEW[{resultadoTextoSor}]`|