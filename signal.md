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
