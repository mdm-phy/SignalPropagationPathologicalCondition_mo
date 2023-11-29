### Original Article:

Hunley, C., Mohsin, M., & Marucho, M. (2022). Electrical impulse characterization along actin filaments in pathological conditions. Computer Physics Communications, 275, 108317. https://doi.org/10.1016/j.cpc.2022.108317

### Abstract:

_We present an interactive Mathematica notebook that characterizes the electrical impulses along actin filaments in both muscle and non-muscle cells for a wide range of physiological and pathological conditions. The simplicity of the theoretical formulation, and high performance of the Mathematica software, enable the analysis of multiple conditions without computational restrictions. The program is based on a multi-scale (atomic \[RightArrow] monomer \[RightArrow] filament) approach capable of accounting for the atomistic details of a protein molecular structure, its biological environment, and their impact on the travel distance, velocity, and attenuation of monovalent ionic wave packets propagating along microfilaments. The interactive component allows investigators to choose the experimental conditions (intracellular Vs in vitro), nucleotide state (ATP Vs ADP), actin isoform (alpha, gamma, beta, and muscle or non-muscle cell), as well as a conformation model that covers a variety of mutants and wild-type (the control) actin filaments. We used the computational tool to analyze environmental changes such as temperature effects and pH changes of the surrounding solutions, as well as structural changes to an actin monomer due to radius changes. Additionally, we investigated for the first time the electrostatic consequences of actin mutations from different disease conditions. These studies may provide an unprecedented molecular understanding of why and how age, inheritance, and disease conditions induce dysfunctions in the biophysical mechanisms underlying the propagation of electrical signals along actin filaments._

### A brief description of the field and our focus:

Actin is an abundant biopolymer inside all eukaryotic (animals, plants, and fungi) cells. Actin, along with two other biopolymers, gives cells their shape and rigidity; that is why they are called cytoskeleton (skeleton of cell). Cytoskeleton polymers also help cell division and cellular cargo transport in subcellular compartments. Besides those well-understood biological and biophysical roles, cytoskeleton has an emerging attribute.

Actin and microtubules have significant negative surface charges. Therefore, these polymers can attract positive ions (sodium, potassium, and calcium) from the cytoplasm. These condensed ions (counter-ions) can then transmit along the cytoskeleton polymer, forming an ionic current and giving cytoskeleton transmission line-like properties. Experimental evidence shows ionic signals can transport, amplify, and oscillate along actin and microtubule. Thus, these filaments have the potential to act as bio-transistors and can take part in information processing in neuronal cells. We can have answers to unknown questions regarding the distinctive formation of memory and conscience, learning and perception. Also, the electrical activities of these conducting polymers can be either used or mimicked to develop biological computers. However, we still need to establish theories and models for explaining the electrical properties of the cytoskeleton, which is crucial for the advancement of the field and for the development of new technologies.

Our group studies the electrical properties of the cytoskeleton experimentally and develops theories and computational models. We have a multiscale theory for ionic current along actin. Using that theory, we wrote a notebook to analyze the electrical impacts of various environmental factors and mutations of actin filaments. 

### About the notebook:

This notebook can be an excellent resource for studying ionic currents along actin. The notebook can also be a good pedagogical tool for scientific computations, data representations, and Mathematica. The notebook uses graphical user interfaces (GUI) for taking user input and displaying success message. It utilizes advanced plotting techniques in Mathematica to get scientifically useful and highly interactive plots and animations. Moreover, the notebook uses advanced programming techniques and coding styles, memoization techniques and packed arrays for memory efficiency,  and parallel computing techniques for time efficiency.

`Button["Click this box to run the notebook. Once prompted insert appropriate inputs and click 'Proceed'. Wait for the message 'The calculations are over.' Use the sliders and check boxes (if available) to change the parameters to see the changes in plots.",

# The notebook
---
`Button["Click this box to run the notebook. Once prompted insert  
appropriate inputs and click 'Proceed'. Wait for the message 'The  
calculations are over.' Use the sliders and check boxes (if  
available) to change the parameters to see the changes in plots.",
 FrontEndExecute[
  FrontEndToken[
   InputNotebook[], "EvaluateNotebook"
   ]
  ],
 ImageSize -> {700, 150},
 BaseStyle -> "Subsection"]`

 ![initial dialogue](https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/610c3a75-e611-4692-9cc1-700c3df8a297)

 `ClearAll["Global*"]`
 
 `Needs["Developer"]`

 ## Datasets for actin mutations

 Here, we create dictionaries (Mathematica associations) of all reported actin mutations and corresponding diseases. The dictionaries are used for user inputs and in later calculations.

 ### ACTG2

 `ACTG2mutations = {{"Arg36His", 
    "Chronic intestinal pseudo obstruction"}, {"Arg38Cys", 
    "MMIHS"}, {"Arg38His", "MMIHS"}, {"Met43Thr", 
    "MMIHS"}, {"Arg61Gln", "MMIHS"}, {"Arg61Gly", 
    "MMIHS"}, {"Lys117Arg", 
    "Visceral myopathy, familial"}, {"Tyr132Asn", 
    "MMIHS"}, {"Gly145Cys", 
    "Chronic intestinal pseudo obstruction"}, {"Arg146Leu", 
    "Chronic intestinal pseudo obstruction"}, {"Arg146Ser", 
    "Visceral myopathy, familial"}, {"Arg176Cys", 
    "MMIHS"}, {"Arg176His", "MMIHS"}, {"Arg176Leu", 
    "MMIHS"}, {"Arg176Ser", "MMIHS"}, {"Thr193Ile", 
    "Chronic intestinal pseudo obstruction"}, {"Gly196Asp", 
    "MMIHS"}, {"Ala203Thr", 
    "Micro-colon megacystic syndrome"}, {"Arg209Gln", 
    "Visceral myopathy, familial"}, {"Arg209Term", 
    "Severe intestinal pseudo-obstruction"}, {"Arg255Cys", 
    "MMIHS"}, {"Arg255His", "Visceral myopathy, familial"}};`

    `ACTG2mutationsAssoc = AssociationThread[ACTG2mutations[[All, 1]] -> ACTG2mutations[[All, 2]]];`

   ### ACTA2

   `ACTA2mutations = {{"Glu3Gln", 
    "Thoracis aortic disorder"}, {"Cys17Arg", 
    "Aortic disease"}, {"Gly20Ser", "Aortic disease"}, {"Asp24Tyr", 
    "Thoracic aortic aneurysms and dissections"}, {"Asp25Gly", 
    "Thoracic aortic aneurysms and dissections"}, {"Gly36Arg", 
    "Thoracic aortic aneurysms and dissections"}, {"Arg37Cys", 
    "Thoracic aortic aneurysms and dissections"}, {"Arg37Gly", 
    "Aortic disease"}, {"Arg38His", 
    "Thoracic aortic disease, coronary artery disease and strokes"},
{"Arg37Ser", "Aortic dissection, acute"}, {"Pro38Ser", 
    "Thoracic aortic aneurysms and dissections"}, {"His40Asn", 
    "Thoracic aortic aneurysms and dissections"}, {"Val43Leu", 
    "Thoracic aortic aneurysms and dissections"}, {"Met44Arg", 
    "Patent Ductus Arteriosus"}, {"Met47Val", 
    "Thoracic aortic aneurysms and dissections"}, {"Gly48Val", 
    "Aortic disease"}, {"Asp56Asn", 
    "Aortic dissection, acute"}, {"Ala58Glu", 
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
    "Thoracic aortic disease, coronary artery disease and strokes"},
{"Glu241Lys", 
    "Thoracic aortic aneurysms and dissections"}, {"Leu242Phe", 
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
    "Thoracic aortic disease, coronary artery disease and strokes"},
{"Lys326Asn", 
    "Thoracic aortic aneurysms and dissections"}, {"Gly342Ser", 
    "Aortic dissection, acute"}, {"Leu346Arg", 
    "Thoracic aortic aneurysms and dissections"}, {"Thr351Asn", 
    "Thoracic aortic aneurysms and dissections"}, {"Gly366Arg", 
    "Schizophrenia"}, {"Arg372Cys", "Thoracic aortic disorder"}};`

    `ACTA2mutationsAssoc = AssociationThread[ACTA2mutations[[All, 1]] -> ACTA2mutations[[All, 2]]];`
    
### ACTC1

`ACTC1mutations = {{"Asp1His", "DCM"}, {"Leu8Met", "HCM"}, {"Ala19Val",
     "HCM, myocardial noncompaction & transmural crypts"},
{"Phe21Leu", "HCM"}, {"Asp25Asn", "HCM"}, {"Ala26Val", 
    "HCM"}, {"Val35Ala", "HCM"}, {"His40Tyr", "HCM"}, {"Met47Leu", 
    "HCM"}, {"Gly48Ser", "HCM"}, {"Gly63Asp", "HCM"}, {"Ile75Val", 
    "HCM"}, {"Ile76Asn", "Developmental disorder"}, {"Met82Thr", 
    "Congenital heart defects"}, {"His88Tyr", "HCM"}, {"Tyr91Cys", 
    "HCM"}, {"Tyr91His", 
    "Noncompaction, left ventricular"}, {"Asn92Ser", 
    "Noncompaction, left ventricular"}, {"Arg95Cys", 
    "HCM"}, {"Glu99Lys", "HCM"}, {"His101Gln", "HCM"}, {"Ala108Val", 
    "Noncompaction, left ventricular"}, {"Glu117Gln", 
    "DCM"}, {"Met119Val", "HCM"}, {"Met123Val", 
    "Atrial septal defect"}, {"Thr126Il2", "DCM"}, {"Asp157Asn", 
    "DCM"}, {"Pro164Ala", "HCM"}, {"Tyr166Cys", "HCM"}, {"Ala170Thr", 
    "HCM"}, {"His173Arg", "DCM"}, {"Met176Ley", 
    "Atrial septal defect"}, {"Arg206His", "DCM"}, {"Arg210His", 
    "Noncompaction, left ventricular, DCM, HCM"}, {"Tyr218His", 
    "DCM"}, {"Tyr218Ser", 
    "Noncompaction, left ventricular"}, {"Asp222Tyr", 
    "Noncompaction, left ventricular"}, {"Thr229Arg", 
    "Noncompaction, left ventricular with arrhythmias"}, {"Ala230Thr",
     "HCM and arrhythmias"}, {"Ala230Val", "HCM"}, {"Ser234Phe", 
    "HCM"}, {"Thr249Ser", "HCM"}, {"Ile250Met", "DCM"}, {"Ile250Thr", 
    "DCM"}, {"Gln263Glu", "HCM"}, {"Pro264Leu", "HCM"}, {"Ile267Thr", 
    "DCM"}, {"Met269Val", 
    "Cardiomyopathy, noncompaction, left ventricular"}, {"Ser271Phe", 
    "HCM"}, {"Ile282Phe", "HCM"}, {"Ile287Thr", 
    "Cardiomyopathy, noncompaction, left ventricular"}, {"Arg290Gly", 
    "Thoracic aortic aneurysms and dissections"}, {"Tyr294Asn", 
    "HCM"}, {"Tyr294His", 
    "HCM, DCM, noncompaction left ventricular"}, {"Ala295Ser", 
    "HCM"}, {"Met305Leu", "HCM"}, {"Asp311His", 
    "Cardiomyopathy, restrictive"}, {"Arg312Cys", 
    "HCM"}, {"Arg312His", "DCM"}, {"Ala321Val", "HCM"}, {"Ile327Thr", 
    "Cardiomyopathy, non-compaction, left ventricular"}, {"Ile329Asn",
     "HCM"}, {"Ala331Pro", "HCM"}, {"Met355Val", "HCM"}, {"Glu361Gly",
     "DCM"}, {"Ala365Thr", "HCM"}, {"Ile369Thr", "DCM"}};`

     `ACTC1mutationsAssoc = AssociationThread[ACTC1mutations[[All, 1]] -> ACTC1mutations[[All, 2]]];`

### ACTA1

`ACTA1mutations = {{"Asp1Tyr", "Core myopathy"}, {"Glu4Lys", 
    "Nemaline myopathy"}, {"Asp11Asn", 
    "Nemaline myopathy"}, {"Gly15Arg", "Actin myopathy"}, {"Gly15Ser",
     "Nemaline myopathy"}, {"Gly15Asp", 
    "Fetal akinesia"}, {"Asp25Asn", "Nemaline myopathy"}, {"Val35Leu",
     "Nemaline myopathy"}, {"Val35Ala", 
    "Nemaline myopathy"}, {"Gly36Ala", 
    "Nemaline myopathy"}, {"Arg38His", 
    "Fetal abnormalities"}, {"Pro38Leu", 
    "Nemaline myopathy"}, {"Arg39Term", 
    "Nemaline myopathy"}, {"His40Tyr", 
    "Nemaline myopathy"}, {"Gln41Arg", 
    "Nemaline myopathy"}, {"Gly42Val", 
    "Nemaline myopathy"}, {"Val43Phe", 
    "Nemaline myopathy"}, {"Met44Thr", 
    "Nemaline myopathy"}, {"Gly46Ala", 
    "Fibre type disproportion, congenital and DCM"}, {"Gly46Asp", 
    "Nemaline myopathy"}, {"Gly46Cys", 
    "Nemaline myopathy"}, {"Gly46Ser", 
    "Congenital myopathy, mild"}, {"Met47Val", 
    "Nemaline myopathy"}, {"Gly48Asp", 
    "Prominent finger flexor and rimmed vacuoles"}, {"Gly48Cys", 
    "Congenital myopathy with fibre-type disproportion"}, {"Gly55Arg",
     "Nemaline myopathy"}, {"Ile64Asn", 
    "Nemaline myopathy"}, {"Ile64Ser", 
    "Nemaline myopathy"}, {"Thr66Asn", 
    "Nemaline myopathy"}, {"Thr66Ile", 
    "Nemaline myopathy"}, {"Lys68Arg", 
    "Nemaline myopathy"}, {"Pro70Arg", 
    "Congenital myopathy"}, {"Ile71Phe", 
    "Nemaline myopathy"}, {"Ile71Val", 
    "Nemaline myopathy"}, {"Glu72Lys", 
    "Nemaline myopathy"}, {"His73Arg", 
    "Nemaline myopathy"}, {"His73Asn", 
    "Nemaline myopathy"}, {"His73Leu", 
    "Nemaline myopathy"}, {"Gly74Asp", 
    "Nemaline myopathy"}, {"Ile75Leu", 
    "Nemaline myopathy"}, {"Ile75Ser", 
    "Nemaline myopathy"}, {"The77Ala", 
    "Nemaline myopathy"}, {"Glu83Lys", 
    "Nemaline myopathy"}, {"Asn92Lys", 
    "Congenital myopathy, nemaline myopathy"}, {"Leu94Pro", 
    "Nemaline myopathy"}, {"Glu107Asp", 
    "Nemaline myopathy"}, {"Asn111Ser", 
    "Nemaline myopathy"}, {"Pro112Leu", 
    "Muscular dystrophy"}, {"Lys113Glu", 
    "Nemaline myopathy"}, {"Ala114Ser", 
    "Nemaline myopathy"}, {"Ala114Thr", 
    "Nemaline myopathy"}, {"Ala114Val", 
    "Congenital myopathy"}, {"Asn115Ser", 
    "Nemaline myopathy"}, {"Asn115Thr", 
    "Nemaline myopathy"}, {"Arg116His", 
    "Nemaline myopathy"}, {"Glu117Gln", 
    "Nemaline myopathy"}, {"Thr120Ser", 
    "Nemaline myopathy"}, {"Met132Ile", 
    "Nemaline myopathy"}, {"Met132Val", 
    "Nemaline myopathy"}, {"Val134Ala", 
    "Nemaline myopathy"}, {"Ile136Met", 
    "Nemaline myopathy"}, {"Ile136Thr", 
    "Nemaline myopathy"}, {"Gln137His", 
    "Nemaline myopathy"}, {"Ala138Asp", 
    "Nemaline myopathy"}, {"Ala138Pro", 
    "Nemaline myopathy"}, {"Val139Ala", 
    "Nemaline myopathy"}, {"Leu140Pro", 
    "Nemaline myopathy"}, {"Leu142Phe", 
    "Nemaline myopathy"}, {"Tyr143Term", 
    "Nemaline myopathy"}, {"Ala144Val", 
    "Muscular dystrophy, limb girdle"}, {"Gly146Asp", 
    "Actin myopathy"}, {"Gly146Ser", 
    "Nemaline myopathy"}, {"Arg147Lys", 
    "Nemaline myopathy"}, {"Thr148Ala", 
    "Nemaline myopathy"}, {"Thr148Asp", 
    "Nemaline myopathy"}, {"Thr148Ile", 
    "Intranuclear rod myopathy"}, {"Thr148Ser", 
    "Nemaline myopathy"}, {"Gly150Ala", 
    "Congenital myopathy"}, {"Val152Leu", 
    "Muscular dystrophy with rigid spine"}, {"Asp154Asn", 
    "Actin myopathy"}, {"Gly158Cys", 
    "Nemaline myopathy"}, {"His161Asp", 
    "Nemaline myopathy"}, {"Val163Leu", 
    "Actin myopathy"}, {"Val163Leu", "Actin myopathy"}, {"Val163Met", 
    "Nemaline myopathy"}, {"Ala170Glu", 
    "Nemaline myopathy"}, {"Ala170GLy", 
    "Nemaline myopathy"}, {"Leu178Pro", 
    "Nemaline myopathy"}, {"Asp179Asn", 
    "Nemaline myopathy"}, {"Asp179Gly", 
    "Nemaline myopathy"}, {"Asp179His", 
    "Nemaline myopathy"}, {"Ala181Thr", 
    "Nemaline myopathy"}, {"Gly182Asp", 
    "Nemaline myopathy"}, {"Arg183Cys", 
    "Nemaline myopathy"}, {"Arg183Gly", 
    "Nemaline myopathy"}, {"Arg183Leu", 
    "Nemaline myopathy"}, {"Arg183Ser", 
    "Nemaline myopathy"}, {"Asp184Gly", 
    "Nemaline myopathy"}, {"Asp184His", 
    "Myopathy, thin filament"}, {"Tyr188Term", 
    "Nemaline myopathy"}, {"Leu189Pro", "Myopathy"}, {"Lys191Asn", 
    "Nemaline myopathy"}, {"Thr194Pro", 
    "Nemaline myopathy"}, {"Glu195Asp", 
    "Distal myopathy with nemaline rods, neuromuscular disorder"},
{"Arg196Cys", "Nemaline myopathy"}, {"Arg196His", 
    "Nemaline myopathy"}, {"Arg196Leu", 
    "Nemaline myopathy"}, {"Arg196Ser", 
    "Nemaline myopathy"}, {"Gly197Ser", 
    "Nemaline myopathy"}, {"Tyr198Cys", 
    "Nemaline myopathy"}, {"Thr202Ile", 
    "Nemaline myopathy"}, {"Ala204Thr", 
    "Nemaline myopathy"}, {"Glu205Asp", 
    "Congenital myopathy with fibre-type disproportion"},
{"Glu205Gly", "Nemaline myopathy"}, {"Glu207Asp", 
    "Nemaline myopathy"}, {"Lys215Term", 
    "Nemaline myopathy"}, {"Leu221Pro", 
    "Congenital myopathy with fibre-type disproportion"},
{"Glu224Gln", "Nemaline myopathy"}, {"Glu224Gly", 
    "Nemaline myopathy"}, {"Glu226Gln", 
    "Nemaline myopathy"}, {"Glu226Term", 
    "Myopathy, early onset"}, {"Met227Ile", 
    "Nemaline myopathy"}, {"Met227Thr", 
    "Nemaline myopathy"}, {"Met227Val", 
    "Nemaline myopathy"}, {"Ala230Val", 
    "Nemaline myopathy"}, {"Glu237Lys", 
    "Nemaline myopathy and HCM"}, {"Glu237Term", 
    "Nemaline myopathy"}, {"Glu241Lys", 
    "Nemaline myopathy"}, {"Asp244Glu", 
    "Nemaline myopathy"}, {"Gly245Arg", 
    "Nemaline myopathy"}, {"Gln246Arg", 
    "Nemaline myopathy"}, {"Gln246Lys", 
    "Nemaline myopathy"}, {"Ile248Thr", 
    "Myofibrillar myopathy"}, {"Gly251Arg", 
    "Distal myopathy"}, {"Gly251Asp", 
    "Nemaline myopathy"}, {"Asn252Tyr", 
    "Nemaline myopathy"}, {"Glu253Gly", 
    "Nemaline myopathy"}, {"Arg254Gly", 
    "DCM, skeletal myopathy"}, {"Arg254His", "DCM"}, {"Phe255Cys", 
    "Nemaline myopathy"}, {"Arg256His", 
    "Nemaline myopathy"}, {"Arg256Leu", 
    "Nemaline myopathy"}, {"Glu259Val", 
    "Nemaline myopathy"}, {"Gln263Leu", 
    "Nemaline myopathy"}, {"Pro264Thr", 
    "Nemaline myopathy"}, {"Ser265Cys", 
    "Nemaline myopathy"}, {"Phe266Leu", 
    "Nemaline myopathy"}, {"Gly268Arg", 
    "Nemaline myopathy"}, {"Gly268Asp", 
    "Nemaline myopathy"}, {"Gly268Cys", 
    "Nemaline myopathy"}, {"Gly268Ser", 
    "Nemaline myopathy"}, {"Met269Arg", 
    "Nemaline myopathy"}, {"Met269Val", 
    "Facioscapuloperoneal myopathy"}, {"Glu270Gln", 
    "Nemaline myopathy"}, {"Ala282Glu", 
    "Nemaline myopathy"}, {"Ala272Val", "Myopathy"}, {"Tyr279His", 
    "Nemaline myopathy"}, {"Asn280Lys", 
    "Nemaline myopathy"}, {"Met283Arg", 
    "Nemaline myopathy"}, {"Met283Lys", 
    "Nemaline myopathy"}, {"Asp286Gly", 
    "Nemaline myopathy"}, {"Asp288Asn", 
    "Nemaline myopathy"}, {"Asp288His", 
    "Nemaline myopathy"}, {"Ile289Phe", 
    "Nemaline myopathy"}, {"Asp292Val", 
    "Congenital myopathy with fibre-type disproportion"},
{"Ala295Thr", "Myopathy/muscular dystrophy"}, {"Met299Lys", 
    "Nemaline myopathy"}, {"Tyr306Cys", 
    "Muscular dystrophy and congenital myopathy"}, {"Ser323Arg", 
    "Muscle weakness"}, {"Met325Lys", 
    "Fibre-type disproportion, congenital"}, {"Lys326Asn", 
    "Nemaline myopathy"}, {"Pro332Arg", 
    "Nemaline myopathy"}, {"Pro332Ser", 
    "Congenital myopathy with fibre-type disproportion"},
{"Glu334Ala", "Core myopathy"}, {"Glu334Lys", 
    "Nemaline myopathy"}, {"Lys336GLu", 
    "Nemaline myopathy, HCM"}, {"Lys336Ile", 
    "Nemaline myopathy"}, {"Lys336Thr", 
    "Nemaline myopathy"}, {"Leu346Gln", 
    "Zebra-body myopathy"}, {"Ser348Leu", 
    "Actin myopathy"}, {"Thr351Ala", 
    "Myopathy/muscular dystrophy"}, {"Phe352Ser", 
    "Nemaline myopathy"}, {"Phe352Tyr", 
    "Nemaline myopathy"}, {"Trp356Cys", 
    "Nemaline myopathy and DCM"}, {"Ile357Leu", 
    "Nemaline myopathy"}, {"Pro367Leu", 
    "Nemaline myopathy"}, {"Ile369Leu", 
    "Nemaline myopathy"}, {"Ile369Phe", 
    "Nemaline myopathy"}, {"Val370Phe", 
    "Nemaline myopathy"}, {"Arg372Cys", 
    "Nemaline myopathy"}, {"Arg372Ser", 
    "Nemaline myopathy"}, {"Lys373Asn", 
    "Nemaline myopathy"}, {"Lys373Gln", 
    "Nemaline myopathy"}, {"Lys373Glu", 
    "Nemaline myopathy"}, {"Cys374Ser", 
    "Nemaline myopathy"}, {"Phe375Cys", 
    "Nemaline myopathy"}, {"Phe375Tyr", "Nemaline myopathy"}};`

    `ACTA1mutationsAssoc = AssociationThread[ACTA1mutations[[All, 1]] -> ACTA1mutations[[All, 2]]];`

  ### ACTG1

  `ACTG1mutations = {{"Asn10Asp", 
    "Baraitser-Winter syndrome"}, {"Pro30Ser", 
    "Hearing loss, non-syndromic"}, {"His38Tyr", 
    "Baraitser-Winter syndrome"}, {"Gly46Arg", 
    "Deafness, dominant progressive"}, {"Asp49Asn", 
    "Deafness, dominant progressive"}, {"Ala56Val", 
    "Baraitser-Winter syndrome"}, {"Thr64Ile", 
    "Hearing loss"}, {"Pro68Leu", "Ocular coloboma"}, {"Ile73Leu", 
    "Microlissencephaly"}, {"Met80Leu", "Hearing loss"}, {"Thr87Ile", 
    "Deafness, dominant progressive"}, {"Lys116Asn", 
    "Deafness, dominant progressive"}, {"Lys116Met", 
    "Deafness, dominant progressive"}, {"Thr118Ile", 
    "Baraitser-Winter syndrome"}, {"Ile120Val", 
    "Deafness, dominant progressive"}, {"Ala133Val", 
    "Baraitser-Winter syndrome"}, {"Ser143Cys", 
    "Sensorineural deafness, nonsyndromic"}, {"Met151Ile", 
    "Microlissencephaly"}, {"Ser153Phe", 
    "Baraitser-Winter syndrome"}, {"Thr161Met", 
    "Deafness"}, {"Glu166Lys", 
    "Diaphragmatic hernia, congenital"}, {"Asp176Tyr", 
    "Baraitser-Winter syndrome"}, {"Ala179Gly", 
    "Hearing loss"}, {"Arg181Gln", 
    "Sensorineural deafness"}, {"Asp185His", 
    "Hearing loss"}, {"Ile190Phe", 
    "Multiple congenital anomalies"}, {"Thr201Lys", 
    "Baraitser-Winter syndrome"}, {"Thr201Met", 
    "Agenesis of corpus callosum and neuronal heterotopia"},
{"Arg208Cys", "Baraitser-Winter syndrome"}, {"Lys211Arg", 
    "Hearing impairment, non-syndromic, autosomal dominant"},
{"Glu239Lys", "Deafness, dominant progressive"}, {"Pro241Leu", 
    "Microlissencephaly"}, {"Glu251Lys", 
    "Congenital heart disease"}, {"Arg252Trp", 
    "Baraitser-Winter syndrome"}, {"Arg254Trp", 
    "Baraitser-Winter syndrome"}, {"Pro256Leu", 
    "Hearing impairment"}, {"Pro262Leu", 
    "Deafness, dominant progressive"}, {"Gly266Ser", 
    "Hearing loss, early-childhood"}, {"Thr276Ile", 
    "Deafness, dominant progressive"}, {"Met281Thr", 
    "Hearing loss, sensorineural"}, {"Met281Val", 
    "Hearing loss"}, {"Leu297Val", "Deafness"}, {"Met303Thr", 
    "Hearing loss, non-syndromic"}, {"Glu314Lys", 
    "Hearing loss"}, {"Met323Lys", "Hearing loss"}, {"Pro330Ala", 
    "Deafness, dominant progressive"}, {"Pro330Ser", 
    "Hearing loss, sensorineural"}, {"Glu332Gln", 
    "Baraitser-Winter syndrome"}, {"Arg333His", 
    "Baraitser-Winter syndrome"}, {"Leu347Met", 
    "Hearing loss"}, {"Val368Ala", "Deafness, dominant progressive"}};`

    `ACTG1mutationsAssoc = AssociationThread[ACTG1mutations[[All, 1]] -> ACTG1mutations[[All, 2]]];`

 ### ACTB

 `ACTBmutations = {{"Asn10Asp", 
    "Baraitser-Winter syndrome"}, {"Asn10His", 
    "Baraitser-Winter syndrome"}, {"Val41Met", 
    "Baraitser-Winter syndrome"}, {"Met45Thr", 
    "Baraitser-Winter syndrome"}, {"Gln57Arg", 
    "Baraitser-Winter syndrome"}, {"Leu63Phe", 
    "Baraitser-Winter syndrome"}, {"Leu63Val", 
    "Baraitser-Winter syndrome"}, {"Pro68Ala", 
    "Baraitser-Winter syndrome"}, {"Pro68Leu", 
    "Baraitser-Winter syndrome"}, {"His71Leu", 
    "Baraitser-Winter syndrome"}, {"Gly72Ser", 
    "Baraitser-Winter syndrome"}, {"Ile73Thr", 
    "Baraitser-Winter syndrome"}, {"Val01Leu", 
    "Baraitser-Winter syndrome"}, {"Glu115Asp", 
    "Neurodevelopmental disorder"}, {"Glu115Lys", 
    "Baraitser-Winter syndrome"}, {"Met117Thr", 
    "Baraitser-Winter syndrome"}, {"Thr118Ile", 
    "Baraitser-Winter syndrome"}, {"Thr147Ile", 
    "Baraitser-Winter syndrome"}, {"Thr161Ala", 
    "Baraitser-Winter syndrome"}, {"Leu169Phe", 
    "Developmental delay, facial dysmorphia, ventricular arrhythmia
and thrombocytopaenia"}, {"Asp176Glu", "Epilepsy"}, {"Arg181Tyr", 
    "Developmental malformations, sensory hearing loss & dystonia"},
{"Arg194Cys", "Baraitser-Winter syndrome"}, {"Arg194His", 
    "Baraitser-Winter syndrome"}, {"Arg194Ser", 
    "Baraitser-Winter syndrome"}, {"Ala202Gly", 
    "Baraitser-Winter syndrome"}, {"Arg202Gln", 
    "Cerebral abnormalities"}, {"Val207Leu", 
    "Leukaemia, acute lymphoblastic"}, {"Val207Met", 
    "Baraitser-Winter syndrome"}, {"Gly243Ser", 
    "Baraitser-Winter syndrome"}, {"Gly266Arg", 
    "Baraitser-Winter syndrome"}, {"Met311Arg", 
    "Developmental disability, microcephaly and thrombocytopenia"},
{"Ala329Val", 
    "Developmental disability, microcephaly and thrombocytopenia"},
{"Glu362Lys", 
    "Neutrophil dysfunction and recurrent infection"}, {"Ser363Leu", 
    "Developmental disability, microcephaly and thrombocytopenia"}};`

    `ACTBmutationsAssoc = AssociationThread[ACTBmutations[[All, 1]] -> ACTBmutations[[All, 2]]];`

 ## Taking User Inputs

 This section takes and processes inputs from the user using **Graphical User Interfaces** (GUIs). All the parameters have default values; optionally, users can input their values.

### Generating Dialogue with Default Values for the Input Parameters

`
xtmivc = 298;
xtmicc = 310;
xln = 23.83;
wnucleotide = "ATP";
conform = "alpha-skeletal(ACTA1)";
wmut = "wild type";
DialogInput[
  DialogNotebook[{TextCell[
     "Radius in Agmstrons (>= 23.83 \[Angstrom]): "], 
    InputField[Dynamic[xln], Number], 
    TextCell[
     "In-vitro Temperature in Kelvin(typically between 295K and
320K):" ], InputField[Dynamic[xtmivc], Number], 
    TextCell[
     "Intracellular Temperature in Kelvin(typically between 295K and
320K):" ], InputField[Dynamic[xtmicc], Number], 
    TextCell["Select Nucletoide state model"], 
    RadioButtonBar[Dynamic[wnucleotide], {"ATP", "ADP"}], 
    TextCell["Select isoform model"], 
    RadioButtonBar[
     Dynamic[conform], {"alpha-skeletal(ACTA1)", 
      "alpha-cardiac(ACTC1)", "alpha-smooth(ACTA2)", 
      "gamma-smooth(ACTG2)", "beta-cytoplasmic(ACTB)", 
      "gamma-cytoplasmic(ACTG1)"}, 
     Appearance -> "Vertical" -> {Automatic, 3}], 
    TextCell["Select conformation model"], 
    RadioButtonBar[
     Dynamic[wmut], {"wild type", "mutant (options in next screen)"}],
     Button["Proceed", 
     DialogReturn[{len = xln, ivctemp = xtmivc, icctemp = xtmicc, 
       isoform = conform, nucleotide = wnucleotide, mut = wmut}]]}]];`

### Generating Dialogues for Isoform Selection and Mutation or Wild Type Selection

`disfq = Boole[(mut == "mutant (options in next screen)")];
disfq21 = Boole[(isoform == "beta-cytoplasmic(ACTB)")];
disfq22 = Boole[(isoform == "gamma-cytoplasmic(ACTG1)")];
disfq23 = Boole[(isoform == "alpha-skeletal(ACTA1)")];
disfq24 = Boole[(isoform == "alpha-cardiac(ACTC1)")];
disfq25 = Boole[(isoform == "alpha-smooth(ACTA2)")];
disfq26 = Boole[(isoform == "gamma-smooth(ACTG2)")];`

`If[disfq + disfq21 == 2, MessageDialog[Dataset[ACTBmutationsAssoc]]];`

`If[disfq + disfq22 == 2, MessageDialog[Dataset[ACTG1mutationsAssoc]]];`

`If[disfq + disfq23 == 2, MessageDialog[Dataset[ACTA1mutationsAssoc]]];`

`If[disfq + disfq24 == 2, MessageDialog[Dataset[ACTC1mutationsAssoc]]];`

`If[disfq + disfq25 == 2, 
  MessageDialog[Dataset[ACTA2mutationsAssoc]]];
If[disfq + disfq26 == 2, MessageDialog[Dataset[ACTG2mutationsAssoc]]];`

### Taking Mutation Selection

`If[disfq + disfq21 == 2, 
  DialogInput[
   DialogNotebook[{TextCell["Please select the mutation"], 
     PopupMenu[Dynamic[missense], ACTBmutations[[All, 1]]], 
     Button["Proceed", 
      DialogReturn[{mutation = 
         If[MemberQ[{"Lys", "Arg"}, StringTake[missense, 3]], -1, 
           If[MemberQ[{"Asp", "Glu"}, StringTake[missense, 3]], 1, 
            0]] + If[
           MemberQ[{"Lys", "Arg"}, StringTake[missense, -3]], 1, 
           If[MemberQ[{"Asp", "Glu"}, StringTake[missense, -3]], -1, 
            0]]}]]}]]];`

`If[disfq + disfq22 == 2, 
  DialogInput[
   DialogNotebook[{TextCell["Please select the mutation"], 
     PopupMenu[Dynamic[missense], ACTG1mutations[[All, 1]]], 
     Button["Proceed", 
      DialogReturn[{mutation = 
         If[MemberQ[{"Lys", "Arg"}, StringTake[missense, 3]], -1, 
           If[MemberQ[{"Asp", "Glu"}, StringTake[missense, 3]], 1, 
            0]] + If[
           MemberQ[{"Lys", "Arg"}, StringTake[missense, -3]], 1, 
           If[MemberQ[{"Asp", "Glu"}, StringTake[missense, -3]], -1, 
            0]]}]]}]]];`

`If[disfq + disfq23 == 2, 
  DialogInput[
   DialogNotebook[{TextCell["Please select the mutation"], 
     PopupMenu[Dynamic[missense], ACTA1mutations[[All, 1]]], 
     Button["Proceed", 
      DialogReturn[{mutation = 
         If[MemberQ[{"Lys", "Arg"}, StringTake[missense, 3]], -1, 
           If[MemberQ[{"Asp", "Glu"}, StringTake[missense, 3]], 1, 
            0]] + If[
           MemberQ[{"Lys", "Arg"}, StringTake[missense, -3]], 1, 
           If[MemberQ[{"Asp", "Glu"}, StringTake[missense, -3]], -1, 
            0]]}]]}]]];`

`If[disfq + disfq24 == 2, 
  DialogInput[
   DialogNotebook[{TextCell["Please select the mutation"], 
     PopupMenu[Dynamic[missense], ACTC1mutations[[All, 1]]], 
     Button["Proceed", 
      DialogReturn[{mutation = 
         If[MemberQ[{"Lys", "Arg"}, StringTake[missense, 3]], -1, 
           If[MemberQ[{"Asp", "Glu"}, StringTake[missense, 3]], 1, 
            0]] + If[
           MemberQ[{"Lys", "Arg"}, StringTake[missense, -3]], 1, 
           If[MemberQ[{"Asp", "Glu"}, StringTake[missense, -3]], -1, 
            0]]}]]}]]];`

`If[disfq + disfq25 == 2, 
  DialogInput[
   DialogNotebook[{TextCell["Please select the mutation"], 
     PopupMenu[Dynamic[missense], ACTA2mutations[[All, 1]]], 
     Button["Proceed", 
      DialogReturn[{mutation = 
         If[MemberQ[{"Lys", "Arg"}, StringTake[missense, 3]], -1, 
           If[MemberQ[{"Asp", "Glu"}, StringTake[missense, 3]], 1, 
            0]] + If[
           MemberQ[{"Lys", "Arg"}, StringTake[missense, -3]], 1, 
           If[MemberQ[{"Asp", "Glu"}, StringTake[missense, -3]], -1, 
            0]]}]]}]]];`

`If[disfq + disfq26 == 2, 
  DialogInput[
   DialogNotebook[{TextCell["Please select the mutation"], 
     PopupMenu[Dynamic[missense], ACTG2mutations[[All, 1]]], 
     Button["Proceed", 
      DialogReturn[{mutation = 
         If[MemberQ[{"Lys", "Arg"}, StringTake[missense, 3]], -1, 
           If[MemberQ[{"Asp", "Glu"}, StringTake[missense, 3]], 1, 
            0]] + If[
           MemberQ[{"Lys", "Arg"}, StringTake[missense, -3]], 1, 
           If[MemberQ[{"Asp", "Glu"}, StringTake[missense, -3]], -1, 
            0]]}]]}]]];`

**Interfaces**

<img width="612" alt="initial input window" src="https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/3e04c467-def2-49c7-8bc4-334c1002ce8e">

Here user can over write on the default values of for the radius of the filament and temperature. They can also slelct actin isoform and wild type or mutant. The execuation will halt until users press on 'Proceed'. If they select 'wild type', the calculation will be finished immediately. If they select 'mutant', there will be two additional interfaces.

<img width="140" alt="drop down for mutation selection" src="https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/89fcc9ea-c9b6-4ce1-aeb1-1b7d5413aa7f">

This gives a drop down list to select a mutant for the selected isoform.

<img width="354" alt="guide to select mutation" src="https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/737b6a33-47d1-4b1d-b21a-9295198360bb">

This interface is provided as a reference to select a mutant in the drop down list above.

Again, execuation will start when users press the 'Proceed' button.


## Parameters

This section uses physical constants and inputs from the previous section to calculate quantities like **electrical resistance**, **capacitance**, and **impedance** for **intracellular** and **in-vitro** ionic conditions. As these quantities are functions of environmental properties (**pH**, **temperature**) and structural properties (**length**, **radius**, **conformations**), we define functions capable of incorporating those in calculations.

### Cylinder (Actin is Modeled as Cylinder) and Electrolyte Parameters and Physical Constants

#### Cylinder Parameters

We model the actin polymer as cylindrical. Here, we evaluate the cylinder parameters: **length**, **radius**, and **surface charge density**. We use user inputs and values extracted from protein databank structures.

`QpHicong = 
  QuantityArray[{23, -82, -154, -184, -222}, "ElementaryCharge"];
isom = Which[isoform == "alpha-skeletal(ACTA1)", 0, 
   isoform == "alpha-cardiac(ACTC1)", 0, 
   isoform == "alpha-smooth(ACTA2)", 0, 
   isoform == "gamma-smooth(ACTG2)", 1, 
   isoform == "beta-cytoplasmic(ACTB)", 1, 
   isoform == "gamma-cytoplasmic(ACTG1)", 1];
nucl = Which[nucleotide == "ATP", 0, nucleotide == "ADP", 1];
state = Which[mut == "wild type", 0, 
   mut == "mutant (options in next screen)", 1];
QpHi = QpHicong + 
   14*QuantityArray[{isom + nucl + mutation*state, 
      isom + nucl + mutation*state, isom + nucl + mutation*state, 
      isom + nucl + mutation*state, isom + nucl + mutation*state}, 
     "ElementaryCharge"];
L = Quantity[422.20, "Angstroms"]; 
LAF = 422.20*10^-10;
CylRad = Quantity[len, "Angstroms"];
CylRadd = QuantityMagnitude[UnitConvert[CylRad]];
denom = 2*\[Pi]*CylRad;  
Lm = Quantity[5.4, "Nanometers"];
uLm = QuantityMagnitude[UnitConvert[Lm]];
sSurfCyl = 2*\[Pi]*CylRad*Lm;
SurfCyl = QuantityMagnitude[UnitConvert[sSurfCyl]];
rzp = CylRadd;`

#### Physical Constants

Here are the physical constants we need for our calculations.

`\[Epsilon]0 = N[QuantityMagnitude[UnitConvert[Quantity["ElectricConstant"]]]];
R = QuantityMagnitude[UnitConvert[Quantity["MolarGasConstant"]]];
F = QuantityMagnitude[UnitConvert[Quantity["FaradayConstant"]]];
ue = Quantity["ElementaryCharge"];
e = QuantityMagnitude[UnitConvert[Quantity["ElementaryCharge"]]];
uKb = Quantity["BoltzmannConstant"];
Kb = QuantityMagnitude[UnitConvert[Quantity["BoltzmannConstant"]]];
`

#### Intracellular and Invitro Viscosity and Relative Permittivity

`ivcmu = x /. 
   Solve[Log[10, x] == (-4.5318) +(-220.57)/(149.39 - ivctemp), x][[1]];
iccmu = x /. 
   Solve[Log[10, x] == (-4.5318) +(-220.57)/(149.39 - icctemp), x][[1]];`

`iccepsilon = 80*\[Epsilon]0 ;`

`ivcepsilon = 78.358*\[Epsilon]0 ;`

#### Electrolyte Parameters

Ion valence and ion mobility ...

`z = ToPackedArray[{1, 1, -1, -2}];
ivcum = ToPackedArray[{5.0148*^-10*Exp[-2.65449*^-20/(Kb*ivctemp)], 
    3.25164*^-10*Exp[-2.64948*^-20/(Kb*ivctemp)], 
    3.57995*^-10*Exp[-2.51681*^-20/(Kb*ivctemp)], 
    1.83587*^-10*Exp[-2.64948*^-20/(Kb*ivctemp)]}];
iccum = ToPackedArray[{5.0148*^-10*Exp[-2.65449*^-20/(Kb*icctemp)], 
    3.25164*^-10*Exp[-2.64948*^-20/(Kb*icctemp)], 
    3.57995*^-10*Exp[-2.51681*^-20/(Kb*icctemp)], 
    1.83587*^-10*Exp[-2.64948*^-20/(Kb*icctemp)]}];
s = QuantityArray[{3.04, 2.32, 3.34, 5.5}, "Angstroms"];`

#### Coefficients in the Theory

This section considers physiological ionic concentrations and calculates some of the quantities needed to evaluate the coefficients in our theory.

##### Intracellular

`icccbulk = ToPackedArray[{140, 12, 4, 74}];
iccT = icctemp;
icclambda = iccepsilon*R*iccT/F^2/((z^2*icccbulk) // Total) // Sqrt;
icclb = e^2/(4*Pi*iccepsilon*Kb*iccT);
iccalfa2 = F^3*z^3*iccum*icccbulk/R/iccT // Total;`

#### In-vitro

`ivccBulk = ToPackedArray[{100, 0, 100, 0}];
ivcT = ivctemp;
ivclambda = ivcepsilon*R*ivcT/F^2/(z^2*ivccBulk // Total) // Sqrt;
ivclb = e^2/(4*Pi*ivcepsilon*Kb*ivcT);
ivcalfa2 = F^3*(z^3*ivcum* ivccBulk)/R/ivcT // Total;`

#### Linear and surface charge density

Surface charge density as a function of pH is calculated.

`\[Lambda]pHi = QpHi/L;
\[Sigma]pHi = \[Lambda]pHi/denom;
\[Sigma]pH = UnitConvert[\[Sigma]pHi, "Coulombs"/"Meters"/"Meters"];
xpH = ToPackedArray[{5, 6, 7, 8, 9}];
y\[Sigma] = QuantityMagnitude[\[Sigma]pH];
f\[Sigma] = Interpolation[Transpose[{xpH, y\[Sigma]}]];`


### Current, Electric Potential, and Resistance

Here, we calculate ionic conductivity, ionic velocity, and electrical field. We use those to evaluate resistance as a function of pH.

#### Intracellular

`icckinf = F^2*z^2*iccum*icccbulk // Total;`

`ClearAll[icckeff];
icckeff[pH_] := (icckeff[pH] = 
   icckinf*(1 -(((2*F*f\[Sigma][pH]*icclambda^2*CylRadd)/(iccepsilon*
             R*iccT*((icclb + CylRadd)^2 - CylRadd^2)))*((z^3*iccum*
              icccbulk // Total)/(z^2 iccum icccbulk // 
             Total))*(1 - (((icclb + CylRadd)*
               BesselK[1, (icclb + CylRadd)/icclambda])/(CylRadd*
               BesselK[1, CylRadd/icclambda]))))))`


`iccG = (((BesselK[0, (CylRadd)/icclambda])^2 - (BesselK[
          1, (CylRadd)/icclambda])^2) + (2*icclambda*
       BesselK[0, (CylRadd)/icclambda]*
       BesselK[1, (CylRadd)/icclambda]/
        CylRadd) - ((((icclb + CylRadd)^2)/
         CylRadd^2)*((BesselK[
            0, (icclb + CylRadd)/icclambda])^2 - (BesselK[
            1, (icclb + CylRadd)/icclambda])^2)) - (2*
       icclambda*(icclb + CylRadd)/CylRadd^2*
       BesselK[0, (icclb + CylRadd)/icclambda]*
       BesselK[1, (icclb + CylRadd)/icclambda]))/((BesselK[1, 
       CylRadd/icclambda])^2);`

`ClearAll[iccEP];
iccEP[pH_, 
  r_] := (iccEP[pH, r] = 
   f\[Sigma][pH]*icclambda*
    BesselK[0, r]/(iccepsilon*BesselK[1, CylRadd/icclambda]))`

`ClearAll[DiccEP];
DiccEP[pH_, 
   r_] := (DiccEP[pH, r] = -((BesselK[1, r] f\[Sigma][pH])/(
     iccepsilon BesselK[1, CylRadd/icclambda])));`

`Ez = 0.15/uLm ;`

`ClearAll[velocityintracellular];
velocityintracellular[pH_, 
   r_] := (velocityintracellular[pH, r] = 
    iccepsilon*
     Ez/iccmu*(iccEP[pH, r/icclambda] - iccEP[pH, CylRadd/icclambda]));`

`ClearAll[krNL];
krNL[pH_, 
   r_] := (krNL[pH, r] = 
    F^2*z^2*iccum*icccbulk*
      Exp[-F*z/R/icctemp*iccEP[pH, r/icclambda]] // Total);`

`ClearAll[prhoNL];
prhoNL[pH_, 
   r_] := (prhoNL[pH, r] = 
    F*z*icccbulk*Exp[-F*z/R/icctemp*iccEP[pH, r/icclambda]] // Total);`

`ClearAll[idensNL];
idensNL[pH_, 
   r_] := (idensNL[pH, r] = 
    Ez*krNL[pH, r] + velocityintracellular[pH, r]*prhoNL[pH, r]);`

`ClearAll[LIICNL];
LIICNL[pH_] := (LIICNL[pH] = 
    2*Pi*NIntegrate[
      idensNL[pH, r]*r, {r, CylRadd, (CylRadd + icclb)}] );`

`ClearAll[RlintraNL];
RlintraNL[pH_] := (RlintraNL[pH] = 0.15/LIICNL[pH] );`

`ClearAll[idensrNL];
idensrNL[pH_, 
   r_] := (idensrNL[pH, 
     r] = -DiccEP[pH, r/icclambda]*F^2*z^2*iccum*icccbulk*
      Exp[-F*z/R/icctemp*iccEP[pH, r/icclambda]] // Total);`

`ClearAll[RIICNL];
RIICNL[pH_] := (RIICNL[pH] = 
   2*Pi*NIntegrate[
     idensrNL[pH, r]*r, {r, 
      CylRadd, (CylRadd + 
        icclb)}] )(*without approximation A6*)(*Dr Marucho notebook \
used idensNL*)`

`ClearAll[RrintraNL];
RrintraNL[
   pH_] := (RrintraNL[pH] = 
    Abs[(iccEP[pH, (CylRadd + icclb)/icclambda] - 
        iccEP[pH, CylRadd/icclambda])/RIICNL[pH]]);`

#### In-Vitro

`ivckinf = F^2*z^2*ivcum*ivccBulk // Total;`

`ClearAll[ivckeff];`

`ivckeff[pH_] := (ivckeff[pH] = 
   ivckinf*(1 - (((2*F*f\[Sigma][pH]*ivclambda^2*CylRadd)/(ivcepsilon*
            R*ivcT*((ivclb + CylRadd)^2 - CylRadd^2)))*((z^3*ivcum*
             ivccBulk // Total )/(z^2*ivcum*ivccBulk // 
            Total))*(1 - (((ivclb + CylRadd)*
              BesselK[1, (ivclb + CylRadd)/ivclambda])/(CylRadd*
              BesselK[1, CylRadd/ivclambda]))))))`

`ivcG = (((BesselK[0, (CylRadd)/ivclambda])^2 - (BesselK[
          1, (CylRadd)/ivclambda])^2) + (2*ivclambda*
       BesselK[0, (CylRadd)/ivclambda]*
       BesselK[1, (CylRadd)/ivclambda]/
        CylRadd) - ((((ivclb + CylRadd)^2)/
         CylRadd^2)*((BesselK[
            0, (ivclb + CylRadd)/ivclambda])^2 - (BesselK[
            1, (ivclb + CylRadd)/ivclambda])^2)) - (2*
       ivclambda*(ivclb + CylRadd)/CylRadd^2*
       BesselK[0, (ivclb + CylRadd)/ivclambda]*
       BesselK[1, (ivclb + CylRadd)/ivclambda]))/((BesselK[1, 
       CylRadd/ivclambda])^2);`

`ClearAll[ivcEp];
ivcEp[pH_, r_] := ( 
  ivcEp[pH, r] = 
   f\[Sigma][pH]*ivclambda*
    BesselK[0, r]/(ivcepsilon*BesselK[1, CylRadd/ivclambda]))`


`ClearAll[DivcEp];
DivcEp[pH_, 
   r_] := (DivcEp[pH, r] = -((BesselK[1, r] f\[Sigma][pH])/(
     ivcepsilon BesselK[1, CylRadd/ivclambda])));`

`ClearAll[velocityinvitro];
velocityinvitro[pH_, 
   r_] := (velocityinvitro[pH, r] = 
    ivcepsilon*
     Ez/ivcmu*(ivcEp[pH, r/ivclambda] - ivcEp[pH, CylRadd/ivclambda]));`

`ClearAll[krivNL];
krivNL[pH_, 
   r_] := (krivNL[pH, r] = 
    F^2*z^2*ivcum*ivccBulk*
      Exp[-F*z/R/ivctemp*ivcEp[pH, r/ivclambda]] // Total);`

`ClearAll[prhoivNL];
prhoivNL[pH_, 
   r_] := (prhoivNL[pH, r] = 
    F*z*ivccBulk*Exp[-F*z/R/ivctemp*ivcEp[pH, r/ivclambda]] // Total);`

`ClearAll[idensivNL];
idensivNL[pH_, 
   r_] := (idensivNL[pH, r] = 
    Ez*krivNL[pH, r] + velocityinvitro[pH, r]*prhoivNL[pH, r]);`

`ClearAll[LIIVNL];
LIIVNL[pH_] := (LIIVNL[pH] = 
    2*Pi*NIntegrate[
      idensivNL[pH, r]*r, {r, CylRadd, (CylRadd + ivclb)}]);`

`ClearAll[RlivNL];
RlivNL[pH_] := (RlivNL[pH] = 0.15/LIIVNL[pH]);`

`ClearAll[idensrivNL];
idensrivNL[pH_, 
   r_] := (idensrivNL[pH, 
     r] = -DivcEp[pH, r/ivclambda]*F^2*z^2*ivcum*ivccBulk*
      Exp[-F*z/R/ivctemp*ivcEp[pH, r/ivclambda]] // Total);`

`ClearAll[RIIVNL];
RIIVNL[pH_] := (RIIVNL[pH] = 
    2*Pi*NIntegrate[
      idensrivNL[pH, r]*r, {r, CylRadd, (CylRadd + ivclb)}]);`

`ClearAll[RrivNL];
RrivNL[pH_] := (RrivNL[pH] = 
    Abs[(ivcEp[pH, (CylRadd + ivclb)/ivclambda] - 
        ivcEp[pH, CylRadd/ivclambda])/RIIVNL[pH]]);`

### Capacitance

Capacitance is nonlinear with nonlinear parameter $b$ and linear capacitance $C_0$.

$C = C_0(1-bV)$

We used data from our classical density functional theory-based calculations to define interpolation functions for b and Subscript[C, 0] as functions of length and temperature. Using these interpolation functions, we can calculate b and Subscript[C, 0] for the user-defined values of length and temperature.

#### Intracellular

`iccbData = {{{23.83`, 292.15`}, -7.04520225907309`}, {{23.83`, 
     298.15`}, -6.89048276867725`}, {{23.83`, 
     304.15`}, -6.73416299607119`}, {{23.83`, 
     310.15`}, -6.59010575643678`}, {{23.83`, 
     316.15`}, -6.44534085018724`}, {{23.83`, 
     321.15`}, -6.34547837304308`}, {{30.3725`, 
     292.15`}, -6.28074214667302`}, {{30.3725`, 
     298.15`}, -6.13256380730967`}, {{30.3725`, 
     304.15`}, -6.00844292361789`}, {{30.3725`, 
     310.15`}, -5.87271744113126`}, {{30.3725`, 
     316.15`}, -5.75064914306211`}, {{30.3725`, 
     321.15`}, -6.06658584257457`}, {{36.915`, 
     292.15`}, -6.71607999857109`}, {{36.915`, 
     298.15`}, -6.56332216453148`}, {{36.915`, 
     304.15`}, -6.42280090664478`}, {{36.915`, 
     310.15`}, -6.29918390933296`}, {{36.915`, 
     316.15`}, -6.16096339871244`}, {{36.915`, 
     321.15`}, -6.04167350136179`}, {{43.4575`, 
     292.15`}, -5.81335886814075`}, {{43.4575`, 
     298.15`}, -6.28330683790706`}, {{43.4575`, 
     304.15`}, -6.15316214319245`}, {{43.4575`, 
     310.15`}, -6.02021369091225`}, {{43.4575`, 
     316.15`}, -5.89228243092949`}, {{43.4575`, 
     321.15`}, -5.80553826189667`}, {{50.`, 
     292.15`}, -6.40890056765745`}, {{50.`, 
     298.15`}, -6.28916671595026`}, {{50.`, 
     304.15`}, -6.1632113574831`}, {{50.`, 
     310.15`}, -6.01885334528184`}, {{50.`, 
     316.15`}, -5.89431507240758`}, {{50.`, 
     321.15`}, -5.79791718256665`}};`

`iccbFun = Interpolation[iccbData];`

`iccC0Data = {{{23.83`, 292.15`}, 
    1.0432863967024569`*^-16}, {{23.83`, 298.15`}, 
    1.0225407162208487`*^-16}, {{23.83`, 304.15`}, 
    1.0240047054821349`*^-16}, {{23.83`, 310.15`}, 
    1.0147916167007417`*^-16}, {{23.83`, 316.15`}, 
    1.0058125110484047`*^-16}, {{23.83`, 321.15`}, 
    9.981541303655341`*^-17}, {{30.3725`, 292.15`}, 
    1.0245714375729816`*^-16}, {{30.3725`, 298.15`}, 
    1.0153308060136974`*^-16}, {{30.3725`, 304.15`}, 
    1.0056365369761956`*^-16}, {{30.3725`, 310.15`}, 
    9.957074947621269`*^-17}, {{30.3725`, 316.15`}, 
    9.868265405226516`*^-17}, {{30.3725`, 321.15`}, 
    9.615463501293229`*^-17}, {{36.915`, 292.15`}, 
    9.868605741895497`*^-17}, {{36.915`, 298.15`}, 
    9.777019581758469`*^-17}, {{36.915`, 304.15`}, 
    9.685294018510589`*^-17}, {{36.915`, 310.15`}, 
    9.593633574318281`*^-17}, {{36.915`, 316.15`}, 
    9.509402148921713`*^-17}, {{36.915`, 321.15`}, 
    9.443797011149544`*^-17}, {{43.4575`, 292.15`}, 
    9.90639006818256`*^-17}, {{43.4575`, 298.15`}, 
    9.590310669527228`*^-17}, {{43.4575`, 304.15`}, 
    9.5017706825976`*^-17}, {{43.4575`, 310.15`}, 
    9.414436864934496`*^-17}, {{43.4575`, 316.15`}, 
    9.33190446317278`*^-17}, {{43.4575`, 321.15`}, 
    9.26085891621492`*^-17}, {{50.`, 292.15`}, 
    9.620430934089083`*^-17}, {{50.`, 298.15`}, 
    9.523858434731886`*^-17}, {{50.`, 304.15`}, 
    9.432743688284012`*^-17}, {{50.`, 310.15`}, 
    9.352201276152549`*^-17}, {{50.`, 316.15`}, 
    9.267796285438349`*^-17}, {{50.`, 321.15`}, 
    9.199418895175065`*^-17}};`

`iccC0Fun = Interpolation[iccC0Data];`

`iccb = iccbFun[len, iccT];`

`iccCo = iccC0Fun[len, iccT];`

#### In-vitro

`ivcbData = {{{23.83`, 292.15`}, 
    0.512614060478198`}, {{23.83`, 298.15`}, 
    0.496112993774198`}, {{23.83`, 304.15`}, 
    0.48000015056051`}, {{23.83`, 310.15`}, 
    0.463692421331974`}, {{23.83`, 316.15`}, 
    0.4501546397312`}, {{23.83`, 321.15`}, 
    0.437868439666967`}, {{30.3725`, 292.15`}, 
    0.494435455619035`}, {{30.3725`, 298.15`}, 
    0.478715620920394`}, {{30.3725`, 304.15`}, 
    0.463366352451184`}, {{30.3725`, 310.15`}, 
    0.448765590516653`}, {{30.3725`, 316.15`}, 
    0.435094020027823`}, {{30.3725`, 321.15`}, 
    0.424474639331011`}, {{36.915`, 292.15`}, 
    0.46134133753743`}, {{36.915`, 298.15`}, 
    0.447140405028992`}, {{36.915`, 304.15`}, 
    0.433496973413469`}, {{36.915`, 310.15`}, 
    0.419682536505783`}, {{36.915`, 316.15`}, 
    0.407422047242412`}, {{36.915`, 321.15`}, 
    0.397640024419504`}, {{43.4575`, 292.15`}, 
    0.458137872976017`}, {{43.4575`, 298.15`}, 
    0.44404148623797`}, {{43.4575`, 304.15`}, 
    0.430121203545348`}, {{43.4575`, 310.15`}, 
    0.417244264903387`}, {{43.4575`, 316.15`}, 
    0.405249964673119`}, {{43.4575`, 321.15`}, 
    0.396003970604199`}, {{50.`, 292.15`}, 
    0.43517276337073`}, {{50.`, 298.15`}, 
    0.422176238691349`}, {{50.`, 304.15`}, 
    0.409750878530536`}, {{50.`, 310.15`}, 
    0.396849308385956`}, {{50.`, 316.15`}, 
    0.386163854376989`}, {{50.`, 321.15`}, 0.375805319467776`}};`

`ivcbFun = Interpolation[ivcbData];`

`ivcC0Data = {{{23.83`, 292.15`}, 
    6.640814017717993`*^-17}, {{23.83`, 298.15`}, 
    6.592408079870895`*^-17}, {{23.83`, 304.15`}, 
    6.545092119222432`*^-17}, {{23.83`, 310.15`}, 
    6.499114706310157`*^-17}, {{23.83`, 316.15`}, 
    6.453953770303901`*^-17}, {{23.83`, 321.15`}, 
    6.416473404848236`*^-17}, {{30.3725`, 292.15`}, 
    6.5218973200139`*^-17}, {{30.3725`, 298.15`}, 
    6.469466109632775`*^-17}, {{30.3725`, 304.15`}, 
    6.41866292351118`*^-17}, {{30.3725`, 310.15`}, 
    6.368281522012187`*^-17}, {{30.3725`, 316.15`}, 
    6.320730227865516`*^-17}, {{30.3725`, 321.15`}, 
    6.281200101196005`*^-17}, {{36.915`, 292.15`}, 
    6.431594999916348`*^-17}, {{36.915`, 298.15`}, 
    6.376954132454964`*^-17}, {{36.915`, 304.15`}, 
    6.324016314164674`*^-17}, {{36.915`, 310.15`}, 
    6.272720435830382`*^-17}, {{36.915`, 316.15`}, 
    6.221883050573596`*^-17}, {{36.915`, 321.15`}, 
    6.181037881131177`*^-17}, {{43.4575`, 292.15`}, 
    6.35358079452262`*^-17}, {{43.4575`, 298.15`}, 
    6.297925407326382`*^-17}, {{43.4575`, 304.15`}, 
    6.243949482328686`*^-17}, {{43.4575`, 310.15`}, 
    6.191417125698059`*^-17}, {{43.4575`, 316.15`}, 
    6.140304933822448`*^-17}, {{43.4575`, 321.15`}, 
    6.098763350537723`*^-17}, {{50.`, 292.15`}, 
    6.297665667836784`*^-17}, {{50.`, 298.15`}, 
    6.241175728471172`*^-17}, {{50.`, 304.15`}, 
    6.186543060036394`*^-17}, {{50.`, 310.15`}, 
    6.13325437639383`*^-17}, {{50.`, 316.15`}, 
    6.081127300443368`*^-17}, {{50.`, 321.15`}, 
    6.039188360074647`*^-17}};`

`ivcC0Fun = Interpolation[ivcC0Data];`

`ivcb = ivcbFun[len, ivcT];`

`ivcCo = ivcC0Fun[len, ivcT];`

### Impedance

Impedance as a function of pH and input voltage ...

#### Intracellular

`ClearAll[iccZeNL];`

`iccZeNL[pH_, V1_] := (iccZeNl[pH, V1] =
    Sqrt[(32/225)*(25*\[Pi]^4*((RlintraNL[pH]))^2 + 
         80*iccb*\[Pi]^4*RlintraNL[pH]*RrintraNL[pH]*(V1) +64*
          iccb^2*\[Pi]^4*((RrintraNL[pH]))^2*V1^2) +(8/
         225)*\[Sqrt](-5625*\[Pi]^4*(RlintraNL[pH])^4 + 
          10000*\[Pi]^8*((RlintraNL[
             pH]))^4 -11250*\[Pi]^4*((RlintraNL[pH]))^3 RrintraNL[
            pH] -5625*\[Pi]^4*(RlintraNL[pH])^2*(RrintraNL[
             pH])^2 -18000*iccb*\[Pi]^4*(RlintraNL[pH])^3*
           RrintraNL[pH]*(V1) + 
          64000 iccb \[Pi]^8 (RlintraNL[pH])^3 RrintraNL[
            pH]*(V1) -36000 iccb \[Pi]^4 (RlintraNL[pH])^2 (RrintraNL[
             pH])^2*(V1) - 
          18000 iccb \[Pi]^4 RlintraNL[
            pH] (RrintraNL[pH])^3 V1 -14400 iccb^2 \[Pi]^4 (RlintraNL[
             pH])^2 (RrintraNL[
             pH])^2 V1^2 +153600 iccb^2 \[Pi]^8 (RlintraNL[
             pH])^2 (RrintraNL[
             pH])^2 V1^2 -28800 iccb^2 \[Pi]^4 RlintraNL[
            pH] (RrintraNL[
             pH])^3 V1^2 -14400 iccb^2 \[Pi]^4 (RrintraNL[
             pH])^4 V1^2 +163840 iccb^3 \[Pi]^8 RlintraNL[
            pH] (RrintraNL[
             pH])^3 V1^3 +65536 iccb^4 \[Pi]^8 (RrintraNL[
             pH])^4 V1^4)]);`

#### In-vitro

`ClearAll[ivcZeNL];`

`ivcZeNL[pH_, V1_] := (ivcZeNL[pH, V1] =
    Sqrt[(32/225)*(25*\[Pi]^4*((RlivNL[pH]))^2 + 
         80*ivcb*\[Pi]^4*RlivNL[pH]*RrivNL[pH]*(V1) +64*
          ivcb^2*\[Pi]^4*((RrivNL[pH]))^2*V1^2) +(8/
         225) \[Sqrt](-5625*\[Pi]^4*(RlivNL[pH])^4 + 
          10000*\[Pi]^8*((RlivNL[pH]))^4 -11250*\[Pi]^4*((RlivNL[
             pH]))^3 RrivNL[
            pH] -5625*\[Pi]^4*((RlivNL[pH]))^2*(RrivNL[pH])^2 -18000*
           ivcb*\[Pi]^4*(RlivNL[pH])^3*RrivNL[pH]*(V1) + 
          64000 ivcb \[Pi]^8 (RlivNL[pH])^3 RrivNL[
            pH]*(V1) -36000 ivcb \[Pi]^4 (RlivNL[pH])^2 (RrivNL[
             pH])^2*(V1) - 
          18000 ivcb \[Pi]^4 RlivNL[
            pH] (RrivNL[pH])^3 V1 -14400 ivcb^2 \[Pi]^4 (RlivNL[
             pH])^2 (RrivNL[
             pH])^2 V1^2 +153600 ivcb^2 \[Pi]^8 (RlivNL[
             pH])^2 (RrivNL[pH])^2 V1^2 -28800 ivcb^2 \[Pi]^4 RlivNL[
            pH] (RrivNL[pH])^3 V1^2 -14400 ivcb^2 \[Pi]^4 (RrivNL[
             pH])^4 V1^2 +163840 ivcb^3 \[Pi]^8 RlivNL[
            pH] (RrivNL[pH])^3 V1^3 +65536 ivcb^4 \[Pi]^8 (RrivNL[
             pH])^4 V1^4)]);`

## Multiscale Theory for Signal Propagation along Actin

This section uses the multiscale theory developed by our group to calculate voltage signals as functions of position, time, pH, and input voltage. The functions are then used to demonstrate results.

### Equations

$\gamma = \frac{3C_ 0Z}{bZ^{3/2}C_ 0}$

$\mu_2=\frac{6R_t}{Z}$

$\mu_3=\frac{24R_l}{Z}$

$\Omega_0=\sqrt{\frac{12 V_{\text{inp}}}{\lvert \gamma \rvert Z^{1/2}}}$

$\alpha = C_0 Z$

$\beta = 2 l$

$\Omega (\tau)=\sqrt{\frac{\Omega_0^2 e^{-\frac{4\tau \mu_3}{3}}}{1+\frac{4\mu_2 \Omega_0^2}{5 \mu_3}(1-e^{\frac{-4\tau \mu_3}{3}})}}$

$\eta (\tau)=\frac{-5\[4\mu_3 \tau+3 \ln{(5\mu_3)}-3\ln{(-4\Omega_0^2 \mu_2 + e^{\frac{4\tau \mu_3}{3}}(4\Omega_0^2 \mu_2+5\mu_3))}\]}{4\mu_2}$

$v(t)=-\frac{5\times \[4\mu_3-\frac{4e^{\frac{4\mu_3 t}{3}}\mu_3(4\Omega_0^2 \mu_2+5\mu_3)}{-4\Omega_0^2\mu_2+e^{\frac{4\mu_3 t}{3}}(4\Omega_0^2 \mu_2+5\mu_3)}\]}{4\mu_2}$

$t_d\equiv \frac{t_{\text{max}}}{24\alpha}$

$\frac{\Omega(t_d)}{\Omega(0)}=0.1$

$v_{\text{av}}=\frac{1}{24t_d \alpha}\int_0^{t_{\text{max}}=24t_d \alpha} \frac{\beta}{\alpha}\[1+v(\frac{t}{24\alpha})\]dt$

$W(x,t)=-2\Omega(\frac{t}{24\alpha})^2\text{sech}^2(\Omega(\frac{t}{24\alpha})\[(\frac{x}{\beta}-\frac{t}{\alpha})-\eta(\frac{t}{24\alpha})\])$

### Intracellular Calculations

`ClearAll[cgammaNL, c\[Mu]2NL, c\[Mu]3NL, cwoNL, calfaNL, cbeta, 
  c\[CapitalOmega]NL, c\[Eta]NL, cvelocitypropNL, cdecaytimeNL, 
  cvavgNL, cWxNL];`
  
`cgammaNL[pH_, 
   V1_] := (cgammaNL[pH, V1] = 
    3*(iccCo*iccZeNL[pH, V1])/(iccb*iccZeNL[pH, V1]^(3/2)*iccCo));`
    
`c\[Mu]2NL[pH_, 
   V1_] := (c\[Mu]2NL[pH, V1] = RrintraNL[pH]*6/iccZeNL[pH, V1]);`
   
`c\[Mu]3NL[pH_, 
   V1_] := (c\[Mu]3NL[pH, V1] = RlintraNL[pH]*24/iccZeNL[pH, V1]);`
   
`cwoNL[pH_, 
   V0_] := (cwoNL[pH, 
     V0] = (V0*12/(Abs[cgammaNL[pH, V0]]*iccZeNL[pH, V0]^(1/2)))^(1/
       2));`
       
`calfaNL[pH_, V1_] := (calfaNL[pH, V1] = (iccCo*iccZeNL[pH, V1]));
cbeta = 2*uLm;`

`c\[CapitalOmega]NL[\[Tau]_, pH_, 
   V0_] := (c\[CapitalOmega]NL[\[Tau], pH, V0] =
    \[Sqrt]((cwoNL[pH, V0]^2 E^(-((4 \[Tau] c\[Mu]3NL[pH, V0])/
          3)))/(1 +((4 c\[Mu]2NL[pH, V0] cwoNL[pH, 
               V0]^2)/(5 c\[Mu]3NL[pH, V0])) (1 - 
            E^(-((4 \[Tau] c\[Mu]3NL[pH, V0])/3))))));`

`c\[Eta]NL[\[Tau]_, pH_, V0_] := (c\[Eta]NL[\[Tau], pH, V0] =
     -((5 (4 c\[Mu]3NL[pH, V0] \[Tau] + 3 Log[5 c\[Mu]3NL[pH, V0]] - 
           3 Log[-4 cwoNL[pH, V0]^2 c\[Mu]2NL[pH, V0] + 
              E^((4 c\[Mu]3NL[pH, V0] \[Tau])/
               3) (4 cwoNL[pH, V0]^2 c\[Mu]2NL[pH, V0] + 
                 5 c\[Mu]3NL[pH, V0])]))/(4 c\[Mu]2NL[pH, V0])));`

`cvelocitypropNL[t_, pH_, V0_] := (cvelocitypropNL[t, pH, V0] =
    -((5 (4 c\[Mu]3NL[pH, 
             V0] -(4 E^((4 t c\[Mu]3NL[pH, V0])/3)
               c\[Mu]3NL[pH, 
               V0] (4 cwoNL[pH, V0]^2 c\[Mu]2NL[pH, V0] +5 c\[Mu]3NL[
                  pH, V0]))/(-4 cwoNL[pH, V0]^2 c\[Mu]2NL[pH, 
                V0] +E^((4 t c\[Mu]3NL[pH, V0])/
               3) (4 cwoNL[pH, V0]^2 c\[Mu]2NL[pH, V0] +5 c\[Mu]3NL[
                   pH, V0]))))/(4 c\[Mu]2NL[pH, V0])));`

`cdecaytimeNL[pH_, 
   V0_] := (cdecaytimeNL[pH, V0] = 
    Quiet[w /. 
      Solve[c\[CapitalOmega]NL[w, pH, V0] == 
         0.1*c\[CapitalOmega]NL[0, pH, V0], w][[1]]]);`

`cvavgNL[pH_, 
   V0_] := (cvavgNL[pH, V0] = 
    NIntegrate[(cvelocitypropNL[t/calfaNL[pH, V0]/24, pH, V0]/24 + 1)/
        calfaNL[pH, V0]*cbeta, {t, 0, 
       24*cdecaytimeNL[pH, V0]*calfaNL[pH, V0]}]/(24*
       cdecaytimeNL[pH, V0]*calfaNL[pH, V0]));`

`cWxNL[x_, t_, pH_, 
   V0_] := (cWxNL[x, t, pH, 
     V0] = -2*(c\[CapitalOmega]NL[t/calfaNL[pH, V0]/24, pH, 
        V0])^2*(Sech[
        c\[CapitalOmega]NL[t/calfaNL[pH, V0]/24, pH, 
          V0]*((x/cbeta - t/calfaNL[pH, V0]) - 
           c\[Eta]NL[t/calfaNL[pH, V0]/24, pH, V0])])^2);`

### In-vitro Calculations

`ClearAll[vgammaNL, v\[Mu]2NL, v\[Mu]3NL, vwoNL, valfaNL, vbeta, 
  v\[CapitalOmega]NL, v\[Eta]NL, vvelocitypropNL, vdecaytimeNL, 
  vvavgNL, vWxNL];`
  
`vgammaNL[pH_, 
   V1_] := (vgammaNL[pH, V1] = 
    3*(ivcCo*ivcZeNL[pH, V1])/(ivcb*ivcZeNL[pH, V1]^(3/2)*ivcCo));`

`v\[Mu]2NL[pH_, 
   V1_] := (v\[Mu]2NL[pH, V1] = RrivNL[pH]*6/ivcZeNL[pH, V1]);`

`v\[Mu]3NL[pH_, 
   V1_] := (v\[Mu]3NL[pH, V1] = RlivNL[pH]*24/ivcZeNL[pH, V1]);`

`vwoNL[pH_, 
   V0_] := (vwoNL[pH, 
     V0] = (V0*12/(Abs[vgammaNL[pH, V0]]*ivcZeNL[pH, V0]^(1/2)))^(1/
       2));`

`valfaNL[pH_, V1_] := (valfaNL[pH, V1] = (ivcCo*ivcZeNL[pH, V1]));`

`vbeta = 2*uLm;
v\[CapitalOmega]NL[\[Tau]_, pH_, 
   V0_] := (v\[CapitalOmega]NL[\[Tau], pH, 
     V0] = \[Sqrt]((vwoNL[pH, V0]^2 E^(-((4 \[Tau] v\[Mu]3NL[pH, V0])/
          3)))/(1 +((4 v\[Mu]2NL[pH, V0] vwoNL[pH, 
               V0]^2)/(5 v\[Mu]3NL[pH, V0])) (1 - 
            E^(-((4 \[Tau] v\[Mu]3NL[pH, V0])/3))))));`
 
`v\[Eta]NL[\[Tau]_, pH_, 
   V0_] := (v\[Eta]NL[\[Tau], pH, 
     V0] = - ((5 (4 v\[Mu]3NL[pH, V0] \[Tau] + 
           3 Log[5 v\[Mu]3NL[pH, V0]] - 
           3 Log[-4 vwoNL[pH, V0]^2 v\[Mu]2NL[pH, V0] + 
              E^((4 v\[Mu]3NL[pH, V0] \[Tau])/
               3) (4 vwoNL[pH, V0]^2 v\[Mu]2NL[pH, V0] + 
                 5 v\[Mu]3NL[pH, V0])]))/(4 v\[Mu]2NL[pH, V0])));`

 
`vvelocitypropNL[t_, pH_, 
   V0_] := (vvelocitypropNL[t, pH, 
     V0] = -((5 (4 v\[Mu]3NL[pH, 
             V0] -(4 E^((4 t v\[Mu]3NL[pH, V0])/3)
               v\[Mu]3NL[pH, 
               V0] (4 vwoNL[pH, V0]^2 v\[Mu]2NL[pH, V0] +5 v\[Mu]3NL[
                  pH, V0]))/(-4 vwoNL[pH, V0]^2 v\[Mu]2NL[pH, 
                V0] +E^((4 t v\[Mu]3NL[pH, V0])/
               3) (4 vwoNL[pH, V0]^2 v\[Mu]2NL[pH, V0] +5 v\[Mu]3NL[
                   pH, V0]))))/(4 v\[Mu]2NL[pH, V0])));`

`vdecaytimeNL[pH_, 
   V0_] := (vdecaytimeNL[pH, V0] = 
    Quiet[w /. 
      Solve[v\[CapitalOmega]NL[w, pH, V0] == 
         0.1*v\[CapitalOmega]NL[0, pH, V0], w][[1]]]);`

`vvavgNL[pH_, V0_] := (vvavgNL[pH, V0]
    = NIntegrate[(vvelocitypropNL[t/valfaNL[pH, V0]/24, pH, V0]/24 + 
          1)/valfaNL[pH, V0]*vbeta, {t, 0, 
       24*vdecaytimeNL[pH, V0]*valfaNL[pH, V0]}]/(24*
       vdecaytimeNL[pH, V0]*valfaNL[pH, V0]));`

`vWxNL[x_, t_, pH_, 
   V0_] := (vWxNL[x, t, pH, 
     V0] = -2*(v\[CapitalOmega]NL[t/valfaNL[pH, V0]/24, pH, 
        V0])^2*(Sech[
        v\[CapitalOmega]NL[t/valfaNL[pH, V0]/24, pH, 
          V0]*((x/vbeta - t/valfaNL[pH, V0]) - 
           v\[Eta]NL[t/valfaNL[pH, V0]/24, pH, V0])])^2);`

## Results
---

We present the results through interactive plots and animations (Mathematica manipulates). Users have already chosen some parameters in the beginning. Now, they have more control in viewing and analyzing the results. They can select ionic conditions (intracellular or in-vitro) and change pH and input voltage. Our considered range includes physiological, and all reported pathological conditions.

### Potential Profile

`Manipulate[Labeled[ListLinePlot[
   {
    Table[{r, ivcEp[pH, r*10^-10/ivclambda]}, {r, 1*CylRadd/10^-10, 
      3*CylRadd/10^-10}],
    Table[{r, iccEP[pH, r*10^-10/icclambda]}, {r, 1*CylRadd/10^-10, 
      3*CylRadd/10^-10}]
    },
   AxesLabel -> {Style["r[\[Angstrom]]", Bold, 18], 
     Style["\[Phi][V]", Bold, 18]},
   PlotStyle -> {
     If[MemberQ[electrolyte, "in vitro"], {Blue, Thickness[0.006]}, 
      None],
     If[MemberQ[electrolyte, "intracellular"], {Orange, 
       Thickness[0.006]}, None]
     },
   AxesStyle -> Directive[Bold, 18], PlotRange -> Full, 
   ImageSize -> 500],
  "Plot 1: Electric Potential as a function of the\nradial separation \
distance.", Bottom, LabelStyle -> Directive[Bold, 18]],
 {{electrolyte, {"intracellular"}}, {"in vitro", "intracellular"}, 
  CheckboxBar},
 Delimiter,
 {{pH, 7}, 6, 8, Appearance -> "Labeled"}, SaveDefinitions -> True, 
 ContinuousAction -> False]`

 ![plot5_1](https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/fcea44a7-9ccb-4106-ba22-a96e6df9d652)


### Ion Velocity Profile

`Manipulate[Labeled[ListLinePlot[
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
 ContinuousAction -> False]`

 ![plot5_2](https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/03b93087-b58a-4c36-938d-9a4f6badfde7)


### Effective electric conductivity

`Manipulate[Labeled[ListLinePlot[
   {
    Table[{r, 
      krivNL[pH, r*10^-10]}, {r, (CylRadd + 3.04/2*10^(-10))/10^-10, 
      3*CylRadd/10^-10}],
    Table[{r, 
      krNL[pH, r*10^-10]}, {r, (CylRadd + 3.04/2*10^(-10))/10^-10, 
      3*CylRadd/10^-10}]
    },
   AxesLabel -> {Style["r[\[Angstrom]]", Bold, 18], 
     Style["k[S]", Bold, 18]},
   PlotStyle -> {
     If[MemberQ[electrolyte, "in vitro"], {Blue, Thickness[0.006]}, 
      None],
     If[MemberQ[electrolyte, "intracellular"], {Orange, 
       Thickness[0.006]}, None]},
   AxesStyle -> Directive[Bold, 18], ImageSize -> 500, 
   PlotRange -> Full],
  "Plot 3: Effective electric conductivity as a function\nof the \
radial separation distance.", Bottom, 
  LabelStyle -> Directive[Bold, 18]],
 {{electrolyte, {"intracellular"}}, {"in vitro", "intracellular"}, 
  CheckboxBar},
 Delimiter,
 {{pH, 7}, 6, 8, Appearance -> "Labeled"}, SaveDefinitions -> True, 
 ContinuousAction -> False]`

 ![plot5_3](https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/29680be6-9cb6-4357-9143-db1d097a2734)


 ### Ion concentration profile

`Manipulate[Manipulate[Labeled[
   ListLinePlot[
    {
     Table[{r, 
       icccbulk[[ion]]*
        Exp[-F*z[[ion]]/R/icctemp*
          iccEP[pH, r*10^-10/icclambda]]}, {r, (CylRadd + 
          QuantityMagnitude[s[[ion]]]/2*10^(-10))/10^-10, 
       3*CylRadd/10^-10}],
     Table[{r, 
       ivccBulk[[ion]]*
        Exp[-F*z[[ion]]/R/ivctemp*
          ivcEp[pH, r*10^-10/icclambda]]}, {r, (CylRadd + 
          QuantityMagnitude[s[[ion]]]/2*10^(-10))/10^-10, 
       3*CylRadd/10^-10}]
     },
    AxesLabel -> {Style["r[\[Angstrom]]", Bold, 18], 
      Style["c[mM]", Bold, 18]},
    PlotStyle -> {
      If[electrolyte == 1, {Orange, Thickness[0.006]}, None],
      If[electrolyte == 2, {Blue, Thickness[0.006]}, None]
      },
    AxesStyle -> Directive[Bold, 18], ImageSize -> 500, 
    PlotRange -> Full],
   "Plot 4: Ion concentration as a function of the\nradial separation \
distance.", Bottom, LabelStyle -> Directive[Bold, 18]],
  {{ion, 1, "Ion (1: K^+, 2: Na^+, 3: Cl^-, 4: Subscript[HPO, 4]^(2-))"}, Range[1, 4, electrolyte]}],
 {{electrolyte, 1}, {1 -> "intracellular", 2 -> "in vitro"}, 
  ControlType -> RadioButtonBar},
 Delimiter,
 {{pH, 7}, 6, 8, Appearance -> "Labeled"}, SaveDefinitions -> True, 
 ContinuousAction -> False]`

 ![plot5_4](https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/e446e0cd-bffb-4058-adae-ae54061ff8c9)

 ### Ion Current density

 #### Longitudinal

`Manipulate[Labeled[ListLinePlot[
   {Table[{r, 
      idensivNL[pH, r*10^-10]}, {r, (CylRadd + 3.04/2*10^(-10))/
       10^-10, 3*CylRadd/10^-10}],
    Table[{r, 
      idensNL[pH, r*10^-10]}, {r, (CylRadd + 3.04/2*10^(-10))/10^-10, 
      3*CylRadd/10^-10}]
    },
   AxesLabel -> {Style["r[\[Angstrom]]", Bold, 18], Style["I[A/m^2]", Bold, 18]},
   PlotStyle -> {
     If[MemberQ[electrolyte, "in vitro"], {Blue, Thickness[0.006]}, 
      None],
     If[MemberQ[electrolyte, "intracellular"], {Orange, 
       Thickness[0.006]}, None]
     },
   AxesStyle -> Directive[Bold, 18], ImageSize -> 500, 
   PlotRange -> Full],
  "Plot 5: Longitudinal current density as a function of\nradial \
separation for a voltage stimulus of 0.15V.", Bottom, 
  LabelStyle -> Directive[Bold, 18]],
 {{electrolyte, {"intracellular"}}, {"in vitro", "intracellular"}, 
  CheckboxBar},
 Delimiter,
 {{pH, 7}, 6, 8, Appearance -> "Labeled"}, SaveDefinitions -> True, 
 ContinuousAction -> False]`

 ![plot5_5_1](https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/748e176c-8ddf-41ba-8032-cda80cb36b64)


#### Transversal

`Manipulate[Labeled[ListLinePlot[
   {
    Table[{r, -idensrivNL[pH, 
        r*10^-10]}, {r, (CylRadd + 3.04/2*10^(-10))/10^-10, 
      3*CylRadd/10^-10}],
    Table[{r, -idensrNL[pH, 
        r*10^-10]}, {r, (CylRadd + 3.04/2*10^(-10))/10^-10, 
      3*CylRadd/10^-10}]
    },
   AxesLabel -> {Style["r[\[Angstrom]]", Bold, 18], Style["I[A/m^2]", Bold, 18]},
   PlotStyle -> {
     If[MemberQ[electrolyte, "in vitro"], {Blue, Thickness[0.006]}, 
      None],
     If[MemberQ[electrolyte, "intracellular"], {Orange, 
       Thickness[0.006]}, None]
     },
   AxesStyle -> Directive[Bold, 18], ImageSize -> 500, 
   PlotRange -> Full],
  "Plot 6: Transversal current density as a function\nof radial \
separation.", Bottom, LabelStyle -> Directive[Bold, 18]],
 {{electrolyte, {"intracellular"}}, {"in vitro", "intracellular"}, 
  CheckboxBar},
 Delimiter,
 {{pH, 7}, 6, 8, Appearance -> "Labeled"}, SaveDefinitions -> True, 
 ContinuousAction -> False]`

![plot5_5_2](https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/dcd110e3-2274-4fc0-914c-86c9b40fe93d)


### Soliton (Electrical Signal Wave-packets) Velocity Plots

`Manipulate[Labeled[ListLinePlot[
   {
    Table[{inputvoltage, vvavgNL[pH, inputvoltage]}, {inputvoltage, 
      0.05, 0.4, 0.05}],
    Table[{inputvoltage, cvavgNL[pH, inputvoltage]}, {inputvoltage, 
      0.05, 0.4, 0.05}]
    },
   AxesLabel -> {Style["Volts", Bold, 18], 
     Style["v(m/s)", Bold, 18]},
   PlotStyle -> {
     If[MemberQ[electrolyte, "in vitro"], {Blue, Thickness[0.006]}, 
      None],
     If[MemberQ[electrolyte, "intracellular"], {Orange, 
       Thickness[0.006]}, None]
     },
   AxesStyle -> Directive[Bold, 18], ImageSize -> 500],
  "Plot 7: Soliton average velocity as a functuion\nof input \
voltage.", Bottom, LabelStyle -> Directive[Bold, 18]],
 {{electrolyte, {"intracellular"}}, {"in vitro", "intracellular"}, 
  CheckboxBar},
 Delimiter,
 {{pH, 7}, 6, 8, Appearance -> "Labeled"},
 SynchronousUpdating -> False, SaveDefinitions -> True, 
 ContinuousAction -> False]`

 ![plot5_6_1](https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/01670600-91d7-4ade-ad90-d39bd8b34816)


`Manipulate[Labeled[ListLinePlot[
   {
    Table[{pH, vvavgNL[pH, inputvoltage]}, {pH, 6, 8, 0.1}],
    Table[{pH, cvavgNL[pH, inputvoltage]}, {pH, 6, 8, 0.1}]
    },
   AxesLabel -> {Style["pH", Bold, 18], Style["v(m/s)", Bold, 18]},
   PlotStyle -> {
     If[MemberQ[electrolyte, "in vitro"], {Blue, Thickness[0.006]}, 
      None],
     If[MemberQ[electrolyte, "intracellular"], {Orange, 
       Thickness[0.006]}, None]
     },
   AxesStyle -> Directive[Bold, 18], ImageSize -> 500],
  "Plot 8: Soliton average velocity as a functuion\nof pH.", Bottom, 
  LabelStyle -> Directive[Bold, 18]],
 {{electrolyte, {"intracellular"}}, {"in vitro", "intracellular"}, 
  CheckboxBar},
 Delimiter,
 {inputvoltage, 0.05, 0.4, Appearance -> "Labeled"},
 SynchronousUpdating -> False, SaveDefinitions -> True, 
 ContinuousAction -> False]`

 
![plot5_6_2](https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/b8679087-80bd-49c0-b44a-03bcbb825158)


`Manipulate[Labeled[ListLinePlot[
   {
    Table[{24*vdecaytimeNL[pH, inputvoltage]*
       valfaNL[pH, inputvoltage]*10^6*(n - 1)/
        20, (vvelocitypropNL[(24*vdecaytimeNL[pH, inputvoltage]*
                 valfaNL[pH, inputvoltage]*(10^6)*(n - 1)/20)/
               valfaNL[pH, inputvoltage]/24*10^-6, pH, inputvoltage]/
           24 + 1)/valfaNL[pH, inputvoltage]*vbeta}, {n, 1, 20}],
    Table[{24*cdecaytimeNL[pH, inputvoltage]*
       calfaNL[pH, inputvoltage]*10^6*(n - 1)/
        20, (cvelocitypropNL[(24*cdecaytimeNL[pH, inputvoltage]*
                 calfaNL[pH, inputvoltage]*10^6*(n - 1)/20)/
               calfaNL[pH, inputvoltage]/24*10^-6, pH, inputvoltage]/
           24 + 1)/calfaNL[pH, inputvoltage]*cbeta}, {n, 1, 20}]
    },
   ImageSize -> 500, 
   AxesLabel -> {Style["t(\[Mu]s)", Bold, 18], 
     Style["v(m/s)", Bold, 18]}, AxesStyle -> Directive[Bold, 18],
   PlotRange -> Full,
    PlotStyle -> {
     If[MemberQ[electrolyte, "in vitro"], {Blue, Thickness[0.006]}, 
      None],
     If[MemberQ[electrolyte, "intracellular"], {Orange, 
       Thickness[0.006]}, None]
     }],
  "Plot 9: Soliton propagation velocity as a function\nof time.", 
  Bottom, LabelStyle -> Directive[Bold, 18]],
 {{electrolyte, {"intracellular"}}, {"in vitro", "intracellular"}, 
  CheckboxBar},
 Delimiter,
 {{pH, 7}, 6, 8, Appearance -> "Labeled"},
 {{inputvoltage, 0.15}, 0.05, 0.4, Appearance -> "Labeled"},
 SynchronousUpdating -> False, SaveDefinitions -> True, 
 ContinuousAction -> False]`

![plot5_6_3](https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/2b7f965d-229a-4952-adcf-32ff0401b6fb)

### Amplitude Attenuation Plots


`Manipulate[Labeled[ListLinePlot[
   {
    Table[{24*vdecaytimeNL[pH, inputvoltage]*
       valfaNL[pH, inputvoltage]*10^6*(n - 1)/20, 
      v\[CapitalOmega]NL[(24*vdecaytimeNL[pH, inputvoltage]*
              valfaNL[pH, inputvoltage]*10^6*(n - 1)/20)/
            valfaNL[pH, inputvoltage]/24*10^-6, pH, inputvoltage]^2*
       vgammaNL[pH, inputvoltage]*
       ivcZeNL[pH, inputvoltage]^(1/2)/12}, {n, 1, 20}],
    Table[{24*cdecaytimeNL[pH, inputvoltage]*
       calfaNL[pH, inputvoltage]*10^6*(n - 1)/
        20, -c\[CapitalOmega]NL[(24*cdecaytimeNL[pH, inputvoltage]*
               calfaNL[pH, inputvoltage]*10^6*(n - 1)/20)/
             calfaNL[pH, inputvoltage]/24*10^-6, pH, inputvoltage]^2*
       cgammaNL[pH, inputvoltage]*
       iccZeNL[pH, inputvoltage]^(1/2)/12}, {n, 1, 20}]
    },
   ImageSize -> 500, 
   AxesLabel -> {Style["t(\[Mu]s)", Bold, 18], 
     Style["Volts", Bold, 18]}, AxesStyle -> Directive[Bold, 18],
   PlotStyle -> {
     If[MemberQ[electrolyte, "in vitro"], {Blue, Thickness[0.006]}, 
      None],
     If[MemberQ[electrolyte, "intracellular"], {Orange, 
       Thickness[0.006]}, None]
     }],
  "Plot 10: Fall of voltage as a function of time.", Bottom, 
  LabelStyle -> Directive[Bold, 18]],
 {{electrolyte, {"intracellular"}}, {"in vitro", "intracellular"}, 
  CheckboxBar},
 Delimiter,
 {{pH, 7}, 6, 8, Appearance -> "Labeled"},
 {inputvoltage, 0.05, 0.4, Appearance -> "Labeled"},
 SaveDefinitions -> True, ContinuousAction -> False]`

 ![plot5_7_1](https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/9ba8589c-9b70-4e21-bb5f-a8b09fd2b5c8)


 
`Manipulate[Labeled[ListLinePlot[
   {
    Table[{24*vdecaytimeNL[pH, 0.15]*
       valfaNL[pH, 0.15]*10^6*(n - 1)/20, 
      v\[CapitalOmega]NL[(24*vdecaytimeNL[pH, 0.15]*
              valfaNL[pH, 0.15]*10^6*(n - 1)/20)/valfaNL[pH, 0.15]/
           24*10^-6, pH, 0.15]^2*vgammaNL[pH, 0.15]*
       ivcZeNL[pH, 0.15]^(1/2)/12}, {n, 1, 20}],
    Table[{24*cdecaytimeNL[pH, 0.15]*
       calfaNL[pH, 0.15]*10^6*(n - 1)/
        20, -c\[CapitalOmega]NL[(24*cdecaytimeNL[pH, 0.15]*
               calfaNL[pH, 0.15]*10^6*(n - 1)/20)/calfaNL[pH, 0.15]/
            24*10^-6, pH, 0.15]^2*cgammaNL[pH, 0.15]*
       iccZeNL[pH, 0.15]^(1/2)/12}, {n, 1, 20}],
    Table[{24*vdecaytimeNL[pH, 0.05]*
       valfaNL[pH, 0.05]*10^6*(n - 1)/20, 
      v\[CapitalOmega]NL[(24*vdecaytimeNL[pH, 0.05]*
              valfaNL[pH, 0.05]*10^6*(n - 1)/20)/valfaNL[pH, 0.05]/
           24*10^-6, pH, 0.05]^2*vgammaNL[pH, 0.05]*
       ivcZeNL[pH, 0.05]^(1/2)/12}, {n, 1, 20}],
    Table[{24*cdecaytimeNL[pH, 0.05]*
       calfaNL[pH, 0.05]*10^6*(n - 1)/
        20, -c\[CapitalOmega]NL[(24*cdecaytimeNL[pH, 0.05]*
               calfaNL[pH, 0.05]*10^6*(n - 1)/20)/calfaNL[pH, 0.05]/
            24*10^-6, pH, 0.05]^2*cgammaNL[pH, 0.05]*
       iccZeNL[pH, 0.05]^(1/2)/12}, {n, 1, 20}]
    },
   ImageSize -> 500, 
   AxesLabel -> {Style["t(\[Mu]s)", Bold, 18], 
     Style["Volts", Bold, 18]}, AxesStyle -> Directive[Bold, 18],
   PlotRange -> Full,
   PlotStyle -> {
     If[MemberQ[electrolyte, "in vitro"], {Blue, Thickness[0.006]}, 
      None],
     If[MemberQ[electrolyte, "intracellular"], {Orange, 
       Thickness[0.006]}, None],
     If[MemberQ[electrolyte, "in vitro"], {Blue, Dashed, 
       Thickness[0.006]}, None],
     If[MemberQ[electrolyte, "intracellular"], {Orange, Dashed, 
       Thickness[0.006]}, None]
     }],
  "Plot 11: Fall of voltage as a function of time\nfor input voltages \
0.05V and 0.015V.", Bottom, LabelStyle -> Directive[Bold, 18]],
 {{electrolyte, {"intracellular"}}, {"in vitro", "intracellular"}, 
  CheckboxBar},
 Delimiter,
 {{pH, 7}, 6, 8, Appearance -> "Labeled"},
 SaveDefinitions -> True, ContinuousAction -> False]`


 ![plot5_7_2](https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/562d00e2-45d2-4866-bf68-543167e0970d)

 
## Soliton profile animations in In-vitro electrolytes

Animations show ion signal wave-packet (soliton) propagation in in-vitro conditions.

`ListAnimate[
  ParallelTable[
   Labeled[Plot[{-vWxNL[x*10^-6, 
         24*vdecaytimeNL[7, 0.05]*valfaNL[7, 0.05]*(n - 1)/10, 7, 
         0.05]/(2*(v\[CapitalOmega]NL[0, 7, 0.05])^2), -vWxNL[x*10^-6,
          24*vdecaytimeNL[7, 0.15]*valfaNL[7, 0.15]*(n - 1)/10, 7, 
         0.15]/(2*(v\[CapitalOmega]NL[0, 7, 0.15])^2)}, {x, -25*
       vbeta*10^6, 235*vbeta*10^6}, 
     PlotRange -> {{-0.1, 1.}, {0, 1.05}}, 
     AxesLabel -> {Style["x(\[Mu]m)", Bold, 18], 
       Style["U/\!\(\*SubscriptBox[\(U\), \(0\)]\)", Bold, 18]}, 
     AxesStyle -> Directive[Bold, 18], ImageSize -> 500, 
     PlotStyle -> {{Blue, Dashed, Thickness[0.006]}, {Orange, 
        Thickness[0.006]}}, 
     PlotLegends -> {Style["0.05V", Bold, 18], 
       Style["0.15V", Bold, 18]}],
    "Plot 12: Animation for in-vitro soliton propagation\nfor pH 7 \
and input voltages 0.05V and 0.15V. [press\n'play' button (\
\[FilledRightTriangle]), to see again, move the slider\nback to the \
initial position and play again.]", Bottom, 
    LabelStyle -> Directive[Bold, 18]], {n, 1, 8.5, 1.5}], 
  AnimationRepetitions -> 1, AnimationRunning -> False]`

https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/713044f3-ca88-4e47-9a91-aacc414357f1


`ListAnimate[
  ParallelTable[
   Labeled[Plot[{-vWxNL[x*10^-6, 
         24*vdecaytimeNL[8, 0.15]*valfaNL[8, 0.15]*(n - 1)/10, 8, 
         0.15]/(2*(v\[CapitalOmega]NL[0, 8, 0.15])^2), -vWxNL[x*10^-6,
          24*vdecaytimeNL[7, 0.15]*valfaNL[7, 0.15]*(n - 1)/10, 7, 
         0.15]/(2*(v\[CapitalOmega]NL[0, 7, 0.15])^2), -vWxNL[x*10^-6,
          24*vdecaytimeNL[6, 0.15]*valfaNL[6, 0.15]*(n - 1)/10, 6, 
         0.15]/(2*(v\[CapitalOmega]NL[0, 6, 0.15])^2)}, {x, -25*
       vbeta*10^6, 235*vbeta*10^6}, 
     PlotRange -> {{-0.1, 1}, {0, 1.05}}, 
     AxesLabel -> {Style["x(\[Mu]m)", Bold, 18], 
       Style["U/\!\(\*SubscriptBox[\(U\), \(0\)]\)", Bold, 18]}, 
     AxesStyle -> Directive[Bold, 18], ImageSize -> 500, 
     PlotStyle -> {{Blue, Thickness[0.006]}, {Orange, 
        Thickness[0.006]}, {Green, Thickness[0.006]}}, 
     PlotLegends -> {Style["pH 8", Bold, 18], Style["pH 7", Bold, 18],
        Style["pH 6", Bold, 18]}], 
    "Plot 13: Animation for in-vitro soliton propagation\nfor input \
voltage 0.15V and pH 8, 7 and 6. [press \n'play' button (\
\[FilledRightTriangle]), to see again, move the slider\nback to the \
initial position and play again.]", Bottom, 
    LabelStyle -> Directive[Bold, 18]], {n, 1, 8.5, 1.5}], 
  AnimationRepetitions -> 1, AnimationRunning -> False]`

  

https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/31a9cdc9-d008-42b9-b539-2934e61e783b


## Soliton Profile Animations in Intracellular Electrolytes

Animations show ion signal wave-packet (soliton) propagation in intracellular conditions.

`ListAnimate[
 ParallelTable[
  Labeled[Plot[{-cWxNL[x*10^-6, 
        24*cdecaytimeNL[7, 0.05]*calfaNL[7, 0.05]*(n - 1)/10, 7, 
        0.05]/(2*(c\[CapitalOmega]NL[0, 7, 0.05])^2), -cWxNL[x*10^-6, 
        24*cdecaytimeNL[7, 0.15]*calfaNL[7, 0.15]*(n - 1)/10, 7, 
        0.15]/(2*(c\[CapitalOmega]NL[0, 7, 0.15])^2)}, {x, -25*
      cbeta*10^6, 235*cbeta*10^6}, 
    PlotRange -> {{-0.1, 1}, {0, 1.05}}, 
    AxesLabel -> {Style["x(\[Mu]m)", Bold, 18], 
      Style["U/\!\(\*SubscriptBox[\(U\), \(0\)]\)", Bold, 18]}, 
    AxesStyle -> Directive[Bold, 18], ImageSize -> 500, 
    PlotStyle -> {{Blue, Dashed, Thickness[0.006]}, {Orange, 
       Thickness[0.006]}}, 
    PlotLegends -> {Style["0.05V", Bold, 18], 
      Style["0.15V", Bold, 18]}], 
   "Plot 14: Animation for intracellular soliton propagation\nfor pH \
7 and input voltages 0.05V and 0.15V. [press\n'play' button (\
\[FilledRightTriangle]), to see again, move the slider back\nto \
initial position and play again.]", Bottom, 
   LabelStyle -> Directive[Bold, 18]], {n, 1, 8.5, 1.5}], 
 AnimationRepetitions -> 1, AnimationRunning -> False]`

 

https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/ba0a25a1-45a9-4e20-b260-0ccaeb1e5e42


`ListAnimate[
  ParallelTable[
   Labeled[Plot[{-cWxNL[x*10^-6, 
         24*cdecaytimeNL[8, 0.15]*calfaNL[8, 0.15]*(n - 1)/10, 8, 
         0.15]/(2*(c\[CapitalOmega]NL[0, 8, 0.15])^2), -cWxNL[x*10^-6,
          24*cdecaytimeNL[7, 0.15]*calfaNL[7, 0.15]*(n - 1)/10, 7, 
         0.15]/(2*(c\[CapitalOmega]NL[0, 7, 0.15])^2), -cWxNL[x*10^-6,
          24*cdecaytimeNL[6, 0.15]*calfaNL[6, 0.15]*(n - 1)/10, 6, 
         0.15]/(2*(c\[CapitalOmega]NL[0, 6, 0.15])^2)}, {x, -25*
       cbeta*10^6, 235*cbeta*10^6}, 
     PlotRange -> {{-0.1, 1}, {0, 1.05}}, 
     AxesLabel -> {Style["x(\[Mu]m)", Bold, 18], 
       Style["U/\!\(\*SubscriptBox[\(U\), \(0\)]\)", Bold, 18]}, 
     AxesStyle -> Directive[Bold, 18], ImageSize -> 500, 
     PlotStyle -> {{Blue, Thickness[0.006]}, {Orange, 
        Thickness[0.006]}, {Green, Thickness[0.006]}}, 
     PlotLegends -> {Style["pH 8", Bold, 18], Style["pH 7", Bold, 18],
        Style["pH 6", Bold, 18]}], 
    "Plot 15: Animation for intracellular soliton propagation\nfor \
input voltage 0.15V and pH 8, 7 and 6. [press 'play'\nbutton (\
\[FilledRightTriangle]), to see again, move the slider back to\n\
initial position and play again.]", Bottom, 
    LabelStyle -> Directive[Bold, 18]], {n, 1, 8.5, 1.5}], 
  AnimationRepetitions -> 1, AnimationRunning -> False]`

  


https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/82fbea9a-be6d-42ea-bd05-91bc9d90c268


## Exporting calculation data

Exports data in **.txt** files to the home directory.

`file = {{"Date: ", DateString[]}, {"In-vitro temperature(K): ", 
   ivctemp}, {"Intracellular temperature(K): ", 
   icctemp}, {"Nucleotide state: ", nucleotide}, {"Actin isoform: ", 
   isoform}, {"Mutation: ", 
   If[disfq == 1, missense, mut]}, {"Actin radius(\[Angstrom]): ", 
   len}, {"F-actin length(\[Angstrom]): ", 
   QuantityMagnitude[L]}, {"Actin monomer length(nm): ", 
   QuantityMagnitude[Lm]}, { "Intracellular dielectric constant: ", 
   iccepsilon/\[Epsilon]0 }, {"In-vitro dielectric constant: ", 
   ivcepsilon/\[Epsilon]0}}; tbl1 = ToString[TableForm[file]];
tbl2 = StringReplace[tbl1, "\n\n" -> "\n"];
Export["actin_input.txt", tbl2, OverwriteTarget -> "KeepBoth" ];`

### Generating Success Message

`MessageDialog["The calculations are over."];`

<img width="351" alt="success message" src="https://github.com/mdm-phy/SignalPropagationPathologicalCondition_mo/assets/85763187/fcff999e-fc90-43a4-951c-a5f937a10c4e">


