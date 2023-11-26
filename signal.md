Electrical signal propagation along Actin filaments in physiological and pathological conditions

Md Mohsin

University of Texas at San Antonio

Original Article:
Hunley, C., Mohsin, M., & Marucho, M. (2022). Electrical impulse characterization along actin filaments in pathological conditions. Computer Physics Communications, 275, 108317. https://doi.org/10.1016/j.cpc.2022.108317

Abstract:
We present an interactive Mathematica notebook that characterizes the electrical impulses along actin filaments in both muscle and non-muscle cells for a wide range of physiological and pathological conditions. The simplicity of the theoretical formulation, and high performance of the Mathematica software, enable the analysis of multiple conditions without computational restrictions. The program is based on a multi-scale (atomic \[RightArrow] monomer \[RightArrow] filament) approach capable of accounting for the atomistic details of a protein molecular structure, its biological environment, and their impact on the travel distance, velocity, and attenuation of monovalent ionic wave packets propagating along microfilaments. The interactive component allows investigators to choose the experimental conditions (intracellular Vs in vitro), nucleotide state (ATP Vs ADP), actin isoform (alpha, gamma, beta, and muscle or non-muscle cell), as well as a conformation model that covers a variety of mutants and wild-type (the control) actin filaments. We used the computational tool to analyze environmental changes such as temperature effects and pH changes of the surrounding solutions, as well as structural changes to an actin monomer due to radius changes. Additionally, we investigated for the first time the electrostatic consequences of actin mutations from different disease conditions. These studies may provide an unprecedented molecular understanding of why and how age, inheritance, and disease conditions induce dysfunctions in the biophysical mechanisms underlying the propagation of electrical signals along actin filaments.

A brief description of the field and our focus:
Actin is an abundant biopolymer inside all eukaryotic (animals, plants, and fungi) cells. Actin, along with two other biopolymers, gives cells their shape and rigidity; that is why they are called cytoskeleton (skeleton of cell). Cytoskeleton polymers also help cell division and cellular cargo transport in subcellular compartments. Besides those well-understood biological and biophysical roles, cytoskeleton has an emerging attribute.

Actin and microtubules have significant negative surface charges. Therefore, these polymers can attract positive ions (sodium, potassium, and calcium) from the cytoplasm. These condensed ions (counter-ions) can then transmit along the cytoskeleton polymer, forming an ionic current and giving cytoskeleton transmission line-like properties. Experimental evidence shows ionic signals can transport, amplify, and oscillate along actin and microtubule. Thus, these filaments have the potential to act as bio-transistors and can take part in information processing in neuronal cells. We can have answers to unknown questions regarding the distinctive formation of memory and conscience, learning and perception. Also, the electrical activities of these conducting polymers can be either used or mimicked to develop biological computers. However, we still need to establish theories and models for explaining the electrical properties of the cytoskeleton, which is crucial for the advancement of the field and for the development of new technologies.

Our group studies the electrical properties of the cytoskeleton experimentally and develops theories and computational models. We have a multiscale theory for ionic current along actin. Using that theory, we wrote a notebook to analyze the electrical impacts of various environmental factors and mutations of actin filaments. 

About the notebook:
This notebook can be an excellent resource for studying ionic currents along actin. The notebook can also be a good pedagogical tool for scientific computations, data representations, and Mathematica. The notebook uses advanced plotting techniques utilizing Mathematica options to get scientifically useful and highly interactive plots. Moreover, it uses good programming practices and coding styles, memoization techniques for memory efficiency,  and parallel computing techniques for time efficiency.

Memory required: ~ 0.1GB

Calculation time: ~ 1 minute

In[1]:= 
Button["Click this box to run the notebook. Once prompted insert appropriate \
inputs and click 'Proceed'. Wait for the message 'The calculations are over.' \
Use the sliders and check boxes (if available) to change the parameters to \
see the changes in plots.",
 FrontEndExecute[
  FrontEndToken[
   InputNotebook[], "EvaluateNotebook"
   ]
  ],
 ImageSize -> {700, 150},
 BaseStyle -> "Subsection"]

Out[1]= \!\(
ButtonBox["\<\"Click this box to run the notebook. Once prompted insert \
appropriate inputs and click 'Proceed'. Wait for the message 'The \
calculations are over.' Use the sliders and check boxes (if available) to \
change the parameters to see the changes in plots.\"\>",
Appearance->Automatic,
BaseStyle->"Subsection",
ButtonFunction:>FrontEndExecute[
FrontEndToken[
InputNotebook[], "EvaluateNotebook"]],
Evaluator->Automatic,
ImageSize->{700, 150},
Method->"Preemptive"]\)

In[2]:= ClearAll["Global`*"]

In[3]:= Needs["Developer`"]

1. Mutations

Here, we create dictionaries (Mathematica associations) of all reported actin mutations and corresponding diseases. The dictionaries are used for user inputs and in later calculations.

1.1 ACTG2

In[4]:= ACTG2mutations = {{"Arg36His", 
    "Chronic intestinal pseudo obstruction"}, {"Arg38Cys", 
    "MMIHS"}, {"Arg38His", "MMIHS"}, {"Met43Thr", "MMIHS"}, {"Arg61Gln", 
    "MMIHS"}, {"Arg61Gly", "MMIHS"}, {"Lys117Arg", 
    "Visceral myopathy, familial"}, {"Tyr132Asn", "MMIHS"}, {"Gly145Cys", 
    "Chronic intestinal pseudo obstruction"}, {"Arg146Leu", 
    "Chronic intestinal pseudo obstruction"}, {"Arg146Ser", 
    "Visceral myopathy, familial"}, {"Arg176Cys", "MMIHS"}, {"Arg176His", 
    "MMIHS"}, {"Arg176Leu", "MMIHS"}, {"Arg176Ser", "MMIHS"}, {"Thr193Ile", 
    "Chronic intestinal pseudo obstruction"}, {"Gly196Asp", 
    "MMIHS"}, {"Ala203Thr", "Micro-colon megacystic syndrome"}, {"Arg209Gln", 
    "Visceral myopathy, familial"}, {"Arg209Term", 
    "Severe intestinal pseudo-obstruction"}, {"Arg255Cys", 
    "MMIHS"}, {"Arg255His", "Visceral myopathy, familial"}};

In[203]:= ACTG2mutationsAssoc = 
  AssociationThread[ACTG2mutations[[All, 1]] -> ACTG2mutations[[All, 2]]];

1.2 ACTA2

In[6]:= ACTA2mutations = {{"Glu3Gln", "Thoracis aortic disorder"}, {"Cys17Arg", 
    "Aortic disease"}, {"Gly20Ser", "Aortic disease"}, {"Asp24Tyr", 
    "Thoracic aortic aneurysms and dissections"}, {"Asp25Gly", 
    "Thoracic aortic aneurysms and dissections"}, {"Gly36Arg", 
    "Thoracic aortic aneurysms and dissections"}, {"Arg37Cys", 
    "Thoracic aortic aneurysms and dissections"}, {"Arg37Gly", 
    "Aortic disease"}, {"Arg38His", 
    "Thoracic aortic disease, coronary artery disease and strokes"}, \
{"Arg37Ser", "Aortic dissection, acute"}, {"Pro38Ser", 
    "Thoracic aortic aneurysms and dissections"}, {"His40Asn", 
    "Thoracic aortic aneurysms and dissections"}, {"Val43Leu", 
    "Thoracic aortic aneurysms and dissections"}, {"Met44Arg", 
    "Patent Ductus Arteriosus"}, {"Met47Val", 
    "Thoracic aortic aneurysms and dissections"}, {"Gly48Val", 
    "Aortic disease"}, {"Asp56Asn", "Aortic dissection, acute"}, {"Ala58Glu", 
    "Thoracic aortic disorder"}, {"Gln59Arg", 
    "Thoracic aortic aneurysms and dissections"}, {"Arg62Lys", 
    "Aortic disease"}, {"Leu67Gln", "Aortic disease"}, {"Pro70Gln", 
    "Thoracic aortic aneurysms and dissections"}, {"Asp80Glu", 
    "Thoracic aortic aneurysms and dissections"}, {"Trp86Arg", 
    "Aortic disease"}, {"Thr106Met", 
    "Thoracic aortic aneurysm"}, {"Asn111Thr", 
    "Thoracic aortic aneurysms and dissections"}, {"Asn115Ile", 
    "Thoracic aortic aneurysms and dissections"}, {"Asn115Ser", 
    "Thoracic aortic aneurysms and dissections"}, {"Asn115Thr", 
    "Thoracic aortic aneurysms and dissections"}, {"Arg116Gln", 
    "Thoracic aortic aneurysms and dissections"}, {"Met132Thr", 
    "Aortic dissection"}, {"Tyr133His", 
    "Thoracic aortic aneurysms and dissections"}, {"Ala138Val", 
    "Thoracic aortic aneurysms and dissections"}, {"Val139Ala", 
    "Aortic disease"}, {"Tyr143Cys", 
    "Thoracic aortic aneurysms and dissections"}, {"Gly146Arg", 
    "Aortic disease"}, {"Arg147Cys", 
    "Thoracic aortic aneurysms and dissections"}, {"Val152Ala", 
    "Thoracic aortic aneurysms and dissections"}, {"Gly158Asp", 
    "Thoracic aortic aneurysms and dissections"}, {"Val159Ala", 
    "Aortic aneurysm"}, {"His161Gln", "Aortic disease"}, {"Pro164Thr", 
    "Aortic disease"}, {"Tyr166Asn", 
    "Thoracic aortic aneurysms and dissections"}, {"Arg177Cys", 
    "Cardiovascular, autonomic and brain anomalies"}, {"Arg177His", 
    "Multisystem smooth muscle dysfunction"}, {"Arg177Leu", 
    "Cerebrovascular disease"}, {"Arg177Ser", 
    "Multisystem smooth muscle dysfunction"}, {"Arg183Gln", 
    "Thoracic disease and coronary artery disease"}, {"Tyr188Ser", 
    "Marfan syndrome with aortopathy"}, {"Met190Val", 
    "Aortic disease"}, {"Arg196Cys", "Aortic disease"}, {"Arg196His", 
    "Aortic disease"}, {"Val201Ile", 
    "Thoracic aortic aneurysms and dissections"}, {"Val201Leu", 
    "Thoracic aortic disorder"}, {"Arg210Gln", 
    "Thoracic aortic disease, coronary artery disease and strokes"}, \
{"Glu241Lys", "Thoracic aortic aneurysms and dissections"}, {"Leu242Phe", 
    "Aortic disease"}, {"Pro243His", 
    "Thoracic aortic disease and strokes"}, {"Pro243Leu", 
    "Aortic disease"}, {"Ile248Leu", 
    "Thoracic aortic disease and strokes"}, {"Arg254His", 
    "Thoracic aortic aneurysms and dissections"}, {"Arg256Cys", 
    "Thoracic aortic aneurysms and dissections"}, {"Arg256His", 
    "Thoracic aortic disease and strokes"}, {"Gly268Arg", 
    "Aortic disease"}, {"Gly268Glu", 
    "Thoracic aortic aneurysm"}, {"Gly273Ala", 
    "Thoracic aortic aneurysms and dissections"}, {"Thr277Ala", 
    "Thoracic aortic disorder"}, {"Ile282Asn", 
    "Thoracic aortic aneurysms and dissections"}, {"Met283Thr", 
    "Thoracic aortic disorder"}, {"Ser300Ala", 
    "Thoracic aortic aneurysms and dissections"}, {"Gly302Arg", 
    "Thoracic aortic aneurysms and dissections"}, {"Gly302Ser", 
    "Thoracic aortic disorder, nonsyndromic"}, {"Arg312Term", 
    "Thoracic aortic aneurysms and dissections"}, {"Thr324Asn", 
    "Thoracic aortic disease, coronary artery disease and strokes"}, \
{"Lys326Asn", "Thoracic aortic aneurysms and dissections"}, {"Gly342Ser", 
    "Aortic dissection, acute"}, {"Leu346Arg", 
    "Thoracic aortic aneurysms and dissections"}, {"Thr351Asn", 
    "Thoracic aortic aneurysms and dissections"}, {"Gly366Arg", 
    "Schizophrenia"}, {"Arg372Cys", "Thoracic aortic disorder"}};

    In[184]:= Manipulate[Labeled[ListLinePlot[
   {
    Table[{r, velocityinvitro[pH, r*10^-10]}, {r, 1*CylRadd/10^-10, 
      3*CylRadd/10^-10}],
    Table[{r, velocityintracellular[pH, r*10^-10]}, {r, 
      1*CylRadd/10^-10, 3*CylRadd/10^-10}]
    },
   
   AxesLabel -> {Style["r[\[Angstrom]]", Bold, 18], 
     Style["v[m/s]", Bold, 18]},
   
   PlotStyle -> {
     If[MemberQ[electrolyte, "in vitro"], {Blue, Thickness[0.006]}, 
      None],
     If[MemberQ[electrolyte, "intracellular"], {Orange, 
       Thickness[0.006]}, None]},
   
   AxesStyle -> Directive[Bold, 18], ImageSize -> 500],
  "Plot 2: Ion velocity as a function of the radial\nseparation \
distance for a voltage stimulus of 0.15V.", Bottom, 
  LabelStyle -> Directive[Bold, 18]],
 {{electrolyte, {"intracellular"}}, {"in vitro", "intracellular"}, 
  CheckboxBar},
 Delimiter,
 {{pH, 7}, 6, 8, Appearance -> "Labeled"}, SaveDefinitions -> True, 
 ContinuousAction -> False]

Out[184]= Manipulate[Labeled[ListLinePlot[{Table[{r, \
velocityinvitro[pH, r/10^10]}, 
      {r, 1*(CylRadd/10^(-10)), 3*(CylRadd/10^(-10))}], 
     Table[{r, velocityintracellular[pH, r/10^10]}, {r, \
1*(CylRadd/10^(-10)), 
       3*(CylRadd/10^(-10))}]}, AxesLabel -> {Style["r[\[Angstrom]]", \
Bold, 18], 
      Style["v[m/s]", Bold, 18]}, PlotStyle -> 
     {If[MemberQ[electrolyte, "in vitro"], {Blue, Thickness[0.006]}, \
None], 
      If[MemberQ[electrolyte, "intracellular"], {Orange, \
Thickness[0.006]}, 
       None]}, AxesStyle -> Directive[Bold, 18], ImageSize -> 500], \
"Plot 2: \
Ion velocity as a function of the radial\nseparation distance for a \
voltage \
stimulus of 0.15V.", Bottom, LabelStyle -> Directive[Bold, 18]], 
  {{electrolyte, {"intracellular"}}, {"in vitro", "intracellular"}, 
   ControlType -> CheckboxBar}, Delimiter, 
  {{pH, 7}, 6, 8, Appearance -> "Labeled"}, ContinuousAction -> False, 
  Initialization :> {velocityinvitro[pH_, r_] := velocityinvitro[pH, \
r] = 
      (ivcepsilon*(Ez/ivcmu))*(ivcEp[pH, r/ivclambda] - 
        ivcEp[pH, CylRadd/ivclambda]), ivcepsilon = \
6.937964486353825*^-10, 
    Ez = 2.7777777777777772*^7, ivcmu = 0.0008962319925990682, 
    ivcEp[7, 2.4800422269488727] = -0.04555740909476498, 
    ivcEp[7, 2.5841144983273394] = -0.04028017780948568, 
    ivcEp[7, 2.6881867697058066] = -0.035639447014051376, 
    ivcEp[7, 2.792259041084274] = -0.0315540814695279, 
    ivcEp[7, 2.896331312462741] = -0.027954084091314984, 
    ivcEp[7, 3.000403583841208] = -0.02477891483605313, 
    ivcEp[7, 3.1044758552196754] = -0.021976093587404263, 
    ivcEp[7, 3.2085481265981426] = -0.01950003283471371, 
    ivcEp[7, 3.31262039797661] = -0.01731105760780135, 
    ivcEp[7, 3.416692669355077] = -0.01537457899623792, 
    ivcEp[7, 3.520764940733544] = -0.01366039438418175, 
    ivcEp[7, 3.6248372121120114] = -0.012142092800850343, 
    ivcEp[7, 3.7289094834904786] = -0.01079654790329017, 
    ivcEp[7, 3.8329817548689458] = -0.009603484350395153, 
    ivcEp[7, 3.937054026247413] = -0.008545105900076507, 
    ivcEp[7, 4.04112629762588] = -0.00760577561765522, 
    ivcEp[7, 4.145198569004347] = -0.0067717402375253545, 
    ivcEp[7, 4.249270840382814] = -0.006030892058755242, 
    ivcEp[7, 4.353343111761282] = -0.0053725628448913305, 
    ivcEp[7, 4.4574153831397485] = -0.00478734508988562, 
    ivcEp[7, 4.561487654518216] = -0.004266936745396506, 
    ivcEp[7, 4.665559925896683] = -0.0038040061106579238, 
    ivcEp[7, 4.7696321972751505] = -0.0033920740889969363, 
    ivcEp[7, 4.873704468653617] = -0.0030254114341505696, 
    ivcEp[7, 4.977776740032085] = -0.0026989489601021246, 
    ivcEp[7, 5.081849011410552] = -0.0024081989824819294, 
    ivcEp[7, 5.185921282789018] = -0.002149186507516932, 
    ivcEp[7, 5.289993554167486] = -0.0019183888940417838, 
    ivcEp[7, 5.394065825545953] = -0.0017126828916788053, 
    ivcEp[7, 5.4981380969244205] = -0.0015292981092439979, 
    ivcEp[7, 5.602210368302887] = -0.0013657760960754627, 
    ivcEp[7, 5.706282639681355] = -0.001219934328877702, 
    ivcEp[7, 5.810354911059822] = -0.0010898344907789782, 
    ivcEp[7, 5.914427182438289] = -0.0009737545100548583, 
    ivcEp[7, 6.018499453816756] = -0.000870163895415198, 
    ivcEp[7, 6.122571725195224] = -0.0007777019645842049, 
    ivcEp[7, 6.22664399657369] = -0.0006951586145484652, 
    ivcEp[7, 6.330716267952158] = -0.0006214573265027988, 
    ivcEp[7, 6.434788539330625] = -0.0005556401371976057, 
    ivcEp[7, 6.538860810709092] = -0.0004968543419362482, 
    ivcEp[7, 6.642933082087559] = -0.00044434072360956, 
    ivcEp[7, 6.747005353466026] = -0.00039742312750007603, 
    ivcEp[7, 6.851077624844494] = -0.00035549922366347566, 
    ivcEp[7, 6.95514989622296] = -0.00031803231794455886, 
    ivcEp[7, 7.059222167601428] = -0.0002845440894909295, 
    ivcEp[7, 7.163294438979895] = -0.0002546081473158537, 
    ivcEp[7, 7.267366710358362] = -0.0002278443113126959, 
    ivcEp[7, 7.371438981736829] = -0.0002039135343779294, 
    ivcEp[pH_, r_] := ivcEp[pH, r] = (f\[Sigma][pH]*ivclambda)*
       (BesselK[0, r]/(ivcepsilon*BesselK[1, CylRadd/ivclambda])), 
    f\[Sigma] = InterpolatingFunction[{{5., 9.}}, {5, 7, 0, {5}, {4}, \
0, 0, 0, 0, 
       Automatic, {}, {}, False}, {{5., 6., 7., 8., 9.}}, 
      {Developer`PackedArrayForm, {0, 1, 2, 3, 4, 5}, \
{0.005829295752909288, 
       -0.020782706597328764, -0.03903093678034914, \
-0.0466343660232743, 
       -0.05626537639764617}}, {Automatic}], 
    ivclambda = 9.608707360324824*^-10, CylRadd = \
2.3829999999999997*^-9, 
    velocityintracellular[pH_, r_] := velocityintracellular[pH, r] = 
      (iccepsilon*(Ez/iccmu))*(iccEP[pH, r/icclambda] - 
        iccEP[pH, CylRadd/icclambda]), iccepsilon = \
7.08335025024*^-10, 
    iccmu = 0.0006942672704656888, iccEP[7, 3.6177392190197115] = 
     -0.032104555573338404, iccEP[7, 3.7695537057599426] = 
     -0.02705168880961782, iccEP[7, 3.921368192500174] = 
     -0.022810781274291692, iccEP[7, 4.073182679240405] = 
     -0.01924778533765222, iccEP[7, 4.2249971659806365] = \
-0.016251574357204, 
    iccEP[7, 4.376811652720868] = -0.01372984211483183, 
    iccEP[7, 4.5286261394611] = -0.011605778781903383, 
    iccEP[7, 4.680440626201331] = -0.009815365883886176, 
    iccEP[7, 4.832255112941562] = -0.008305167315086166, 
    iccEP[7, 4.984069599681793] = -0.007030519771539993, 
    iccEP[7, 5.135884086422024] = -0.005954046175311411, 
    iccEP[7, 5.287698573162255] = -0.005044431299550988, 
    iccEP[7, 5.439513059902487] = -0.004275410991561296, 
    iccEP[7, 5.591327546642718] = -0.0036249359538601585, 
    iccEP[7, 5.7431420333829495] = -0.003074478591377587, 
    iccEP[7, 5.894956520123181] = -0.0026084574235584693, 
    iccEP[7, 6.046771006863412] = -0.0022137583384734157, 
    iccEP[7, 6.198585493603644] = -0.0018793357948587467, 
    iccEP[7, 6.350399980343875] = -0.0015958801588641565, 
    iccEP[7, 6.502214467084106] = -0.0013555398508326665, 
    iccEP[7, 6.654028953824337] = -0.0011516889946450494, 
    iccEP[7, 6.805843440564568] = -0.0009787329026096927, 
    iccEP[7, 6.9576579273048] = -0.0008319450669228376, 
    iccEP[7, 7.109472414045031] = -0.000707330423114221, 
    iccEP[7, 7.2612869007852625] = -0.0006015105482730518, 
    iccEP[7, 7.413101387525494] = -0.0005116271944126111, 
    iccEP[7, 7.564915874265725] = -0.00043526116485859156, 
    iccEP[7, 7.716730361005956] = -0.0003703640429709071, 
    iccEP[7, 7.868544847746188] = -0.00031520069713531087, 
    iccEP[7, 8.020359334486418] = -0.0002683008294104587, 
    iccEP[7, 8.17217382122665] = -0.0002284181201668219, 
    iccEP[7, 8.323988307966882] = -0.00019449575782618425, 
    iccEP[7, 8.475802794707112] = -0.00016563733982672728, 
    iccEP[7, 8.627617281447344] = -0.0001410822950897076, 
    iccEP[7, 8.779431768187575] = -0.00012018511519984453, 
    iccEP[7, 8.931246254927807] = -0.00010239779587627854, 
    iccEP[7, 9.083060741668039] = -0.00008725498592788766, 
    iccEP[7, 9.234875228408269] = -0.00007436142091015906, 
    iccEP[7, 9.386689715148501] = -0.00006338128573758693, 
    iccEP[7, 9.538504201888731] = -0.00005402920671355336, 
    iccEP[7, 9.690318688628963] = -0.00004606262060789344, 
    iccEP[7, 9.842133175369195] = -0.00003927530802621795, 
    iccEP[7, 9.993947662109425] = -0.000033491911609468775, 
    iccEP[7, 10.145762148849657] = -0.000028563287605149813, 
    iccEP[7, 10.297576635589888] = -0.000024362562920005, 
    iccEP[7, 10.44939112233012] = -0.000020781789612527568, 
    iccEP[7, 10.601205609070352] = -0.00001772910550975803, 
    iccEP[7, 10.753020095810582] = -0.00001512632373566172, 
    iccEP[pH_, r_] := iccEP[pH, r] = (f\[Sigma][pH]*icclambda)*
       (BesselK[0, r]/(iccepsilon*BesselK[1, CylRadd/icclambda])), 
    icclambda = 6.586986666898878*^-10}]![image](https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/922c72ce-fa3a-42c3-b886-646386927e61)

