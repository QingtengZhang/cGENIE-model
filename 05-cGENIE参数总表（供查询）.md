---

# 一、PDF
:::info
+ 参考文档：[cGENIE.Parameter_reference_guide.pdf](https://www.yuque.com/attachments/yuque/0/2025/pdf/44934637/1752505537800-f627ac77-1899-4301-a110-bf04fe03a6c5.pdf)

:::

---

![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505474616-8f5ead0a-50bc-4e84-8a56-899315c946c7.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505474636-6cacb035-7bb6-4ab1-8e1b-d3f6f203a2ff.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505474685-8d99e0c0-c3f0-4fd3-9105-5ad231edf848.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505474783-c48c0620-7be8-4ae4-93f9-f64184280a38.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505474793-eb361ffb-4445-4607-af5b-8936e05a5b6c.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505475127-0b76c7de-355d-473e-b186-24d40c9cbd2b.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505475248-54b2ef24-a8b5-4128-b261-3ccb7fce5556.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505475184-6353d2da-a70c-40d6-973b-4d7ddd7d4ea4.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505475226-54228bf7-aeff-47bb-b785-d5b3ae879d6d.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505475233-9e535cf7-e747-4e2e-8f14-b776483ffbea.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505475612-2b9d4df2-20aa-4d9f-90a3-e561f2fde828.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505475658-e2d8f1bd-9a59-40d4-8a8f-1b22a2d09622.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505475683-1ea7a931-3174-4ebf-8982-a93f555f7d4b.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505475668-8563e485-a98b-45ab-b38e-40f123d21090.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505475766-9cba0dda-b428-46af-91df-3b9cd84bed26.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505476081-c3478845-263a-46ea-ac52-8cde80117160.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505476118-c2125e2b-f8c9-49fe-a098-af243f5099b5.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505476136-545be207-9b7b-4f9c-ad7e-c2b1d7bcbd62.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505476238-79e15e71-7baa-4664-8571-3b7c326210f6.jpeg)![](https://cdn.nlark.com/yuque/0/2025/jpeg/44934637/1752505476500-92394ac0-40e2-40d0-be76-00c50fd30ebd.jpeg)

---

# 二、LaTeX
```latex
% cGENIE namelist table

% Babette Hoogakker, November 2010
%
% ---------------------------------------------------------------------------------------------------------------------------------
% 10/12/05: tidying-up and minor fixes
% 11/03/24: tidying-up and minor fixes
% 18/12/01: JS updated ocean and sediment tracers
% ---------------------------------------------------------------------------------------------------------------------------------

\documentclass[english,10pt,twoside]{article}
\usepackage[paper=a4paper,portrait=true,margin=2.5cm,voffset=0pt,ignorehead,footnotesep=1cm]{geometry}
\usepackage{babel}
\usepackage{graphicx}
\usepackage{hyperref}
\usepackage{paralist}
\usepackage{caption}
\usepackage{float}

\linespread{1.1}
\setlength{\pltopsep}{2.5pt}
\setlength{\plparsep}{2.5pt}
\setlength{\partopsep}{2.5pt}
\setlength{\parskip}{2.5pt}
\usepackage{multirow}
\usepackage{wasysym}

\title{A brief guide to cGENIE parameters ('namelists')}
\author{Babette Hoogakker, Jun Shao}
\date{\today}

\begin{document}


%=================================================================================================================================
%=== BEGIN DOCUMENT ==============================================================================================================
%=================================================================================================================================

\maketitle


%---------------------------------------------------------------------------------------------------------------------------------

Parameters in the model are controlled via `namelists'. The default parameter values are listed in the following Tables. To effect a change in parameter value, the parameter name is simply assigned the new value, typically in the user config file.
Namelist settings can simply be edited in the user config file if they are already present, or a namelist assignment can be added (either under a relevant heading, or at the bottom of the file - it does not matter). The assignment takes the form:
namelist = value\\
Note that where the value is a string, the syntax is:\\
\texttt{namelist = `string'}
The syntax for logical (true/false) assignments is:\\
\texttt{namelist = .true.}
\texttt{(or namelist = .false.)}

For selecting (or de-selecting) atmospheric tracers, the syntax is: gm\_atm\_select\_n = .true.
where n is the index of the tracer as detailed in the Tables. For ocean and sediment (particulate) tracers, the namlist names take the same form except with `ocn' or `sed' in the namlist parameter name.\\

NOTE: If the number of selected tracers in the ocean is changed, so to must the value of GOLDSTEINNTRACSOPTS, which sets the array dimensions in the ocean and the number of tracers that must be advected, convected, and diffused in the
ocean. For example, for 16 selected ocean tracers (including temperature and salinity), add the line:
GOLDSTEINNTRACSOPTS = `\$(DEFINE)GOLDSTEINNTRACS=16'\\

For setting initial values of atmospheric tracers, the syntax is:
gm\_atm\_init\_n = 278.0E-6\\
where again, n is the index of the tracer (detailed below). Ocean tracers are initialized similarly.\\
NOTE: There is no user-configurable initialization of deep-sea sediment composition (in SEDGEM).\\

   \begin{center}
   \resizebox{\textwidth}{!}{%
   \begin{tabular}{ | l | l | l | l | l | l | l |}
   \hline
    & &\multicolumn{2}{|l|}{SELECTION} &\multicolumn{2}{|l|}{INITILIZATION} & \\
    & &\multicolumn{2}{|l|}{gm\_atm\_select\_n} &\multicolumn{2}{|l|}{ac\_atm\_init\_n} & \\ \hline
   TRACER & INDEX & DEFAULT & UNITS & DEFAULT & UNITS & TRACER \\
   MNEMONIC & n & VALUE & & VALUE & & DESCRIPTION \\ \hline
   \multicolumn{7}{|l|}{ATMOSPHERIC (GASEOUS) TRACERS} \\ \hline
   ia\_temp & 1 & .true. & logical & n/a (0.0) & K & surface air temperature \\ \hline
   ia\_humidity & 2 & .true. & logical & n/a (0.0) &  & specific humidity \\ \hline
   ia\_pCO2 & 3 & .false. & logical & 0.0 & atm & carbon dioxide (CO$_{2}$) \\ \hline
   ia\_pCO2\_13C & 4 & .false. & logical & 0.0 & \permil & d$^{13}$C of CO$_{2}$ \\ \hline
   ia\_pCO2\_14C & 5 & .false. & logical&  0.0 & \permil & d$^{14}$C of CO$_{2}$ \\ \hline
   ia\_pO2 & 6 & .false. & logical & 0.0 & atm & oxygen (O$_{2}$) \\ \hline
   ia\_pO2\_18O & 7 & .false. & logical & 0.0 & \permil & $^{18}$O of O$_{2}$ \\ \hline
   ia\_pN2 & 8 & .false. & logical & 0.0 & atm & nitrogen (N$_{2}$) \\ \hline
   ia\_pN2\_15N & 9 & .false. & logical & 0.0 & \permil & $^{15}$N of N$_{2}$ \\ \hline
   ia\_pCH4 & 10 & .false. & logical & 0.0 & atm & methane (CH$_{4}$) \\ \hline
   ia\_pCH4\_13C & 11 & .false. & logical & 0.0 & \permil & $^{13}$C of CH$_{4}$ \\ \hline
   ia\_pCH4\_14C & 12 & .false. & logical & 0.0 & \permil & $^{14}$C of CH$_{4}$ \\ \hline
   ia\_pSF6 & 13 & .false. & logical & 0.0 & atm & sulphur hexafloride (SF6) \\ \hline
   ia\_pN2O & 14 & .false. & logical & 0.0 & atm & nitrous oxide (N$_{2}$O) \\ \hline
   ia\_pN2O\_15N & 15 & .false. & logical & 0.0 & \permil & $^{15}$N of N$_{2}$O \\ \hline
   ia\_pH2S & 16 & .false. & logical & 0.0 & atm & hydrogen sulphide (H$_{2}$S) \\ \hline
   ia-pH2S\_34S & 17 & .false. & logical & 0.0 & \permil & $^{34}$S of H$_{2}$S \\ \hline
   ia\_pCFC11 & 18 & .false. & logical & 0.0 & atm & CFC-11 \\ \hline
   ia\_pCFC12 & 19 & .false. & logical & 0.0 & atm & CFC-12 \\ \hline
   \end{tabular}
      } % 这行是 resizebox 的结束
   \end{center}

   \begin{center}
   \resizebox{\textwidth}{!}{%
   \begin{tabular}{ | l | l | l | l | l | l | l |}
   \hline
    & &\multicolumn{2}{|l|}{SELECTION} &\multicolumn{2}{|l|}{INITILIZATION} & \\
    & &\multicolumn{2}{|l|}{gm\_ocn\_select\_n} &\multicolumn{2}{|l|}{bg\_ocn\_init\_n} & \\ \hline
   TRACER & INDEX & DEFAULT & UNITS & DEFAULT & UNITS & TRACER \\
   MNEMONIC & n & VALUE & & VALUE & & DESCRIPTION \\ \hline
   \multicolumn{7}{|l|}{OCEAN (DISSOLVED) TRACERS} \\ \hline
   io\_temp & 1 & .true. & logical & n/a (0.0) & K & temperature \\ \hline
   io\_sal & 2 & .true. & logical & n/a (0.0) & PSU & salinity \\ \hline
   io\_DIC & 3 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved inorganic carbon (DIC) \\ \hline
   io\_DIC\_13C & 4 & .false. & logical & 0.0 &  \permil & d$^{13}$C of DIC \\ \hline
   io\_DIC\_14C & 5 & .false. & logical & 0.0 &  \permil  & d$^{14}$C of DIC \\ \hline
   io\_NO3 & 6 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved nitrate (NO$_{3}$) \\ \hline
   io\_NO3\_15N & 7 & .false. & logical & 0.0 &  \permil & d$^{15}$N of NO$_{3}$ \\ \hline
   io\_PO4 &8 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved phosphate (PO$_{4}$) \\ \hline
   io\_O2 & 10 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved oxygen (O$_{2}$) \\ \hline
   io\_O2\_18O & 11 & .false. & logical & 0.0 &  \permil & d$^{18}$O of O$_{2}$ \\ \hline
   io\_ALK & 12 & .false. & logical & 0.0 & mol kg$^{-1}$ & alkalinity (ALK) \\ \hline
   io\_SiO2 & 13 & .false. & logical & 0.0 & mol kg$^{-1}$ & aqueous silicic acid (H$_{4}$SiO$_{4}$) \\ \hline
   io\_SiO2\_30Si & 14 & .false. & logical & 0.0 &  \permil & d$^{30}$Si of H$_{4}$SiO$_{4}$ \\ \hline
   io\_DOM\_C & 15 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved organic matter (DOM); C \\ \hline
   io\_DOM\_C\_13C & 16 & .false. & logical & 0.0 &  \permil & d$^{13}$C of DOM-C \\ \hline
   io\_DOM\_C\_14C & 17 & .false. & logical & 0.0 &  \permil & d$^{14}$C of DOM-C \\ \hline
   io\_DOM\_N & 18 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved organic matter; nitrogen \\ \hline
   io\_DOM\_N\_15N & 19 & .false. & logical & 0.0 &  \permil & d$^{15}$N of DOM-N \\ \hline
   io\_DOM\_P & 20 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved organic matter; P \\ \hline
   io\_DOM\_Cd & 21 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved organic matter; cadmium \\ \hline
   io\_DOM\_Cd\_114Cd & 52 & .false. & logical & 0.0 & \permil & d$^{114}$Cd of DOM-Cd \\ \hline
   io\_DOM\_Fe & 22 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved organic matter; iron \\ \hline
   io\_DOM\_Fe\_56Fe & 81 & .false. & logical & 0.0 & \permil & d$^{56}$Fe of DOM-Fe  \\ \hline
   io\_DOM\_I & 94 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved organic matter; iodine \\ \hline 
   io\_RDOM\_C & 67 & .false. & logical & 0.0 & mol kg$^{-1}$ & R dissolved organic matter (RDOM); C \\ \hline
   io\_RDOM\_C\_13C & 68 & .false. & logical & 0.0 &  \permil & d$^{13}$C of RDOM-C \\ \hline
   io\_RDOM\_C\_14C & 69 & .false. & logical & 0.0 &  \permil  & d$^{14}$C of RDOM-C \\ \hline
   io\_RDOM\_N & 70 & .false. & logical & 0.0 & mol kg$^{-1}$ & R dissolved organic matter; nitrogen \\ \hline
   io\_RDOM\_N\_15N & 71 & .false. & logical & 0.0 &  \permil & d$^{15}$N of RDOM-N \\ \hline
   io\_RDOM\_P & 72 & .false. & logical & 0.0 & mol kg$^{-1}$ & R dissolved organic matter; P \\ \hline
   io\_RDOM\_Cd & 73 & .false. & logical & 0.0 & mol kg$^{-1}$ & R dissolved organic matter; cadmium \\ \hline
   io\_RDOM\_Cd\_114Cd & 74 & .false. & logical & 0.0 & \permil & d$^{114}$Cd of RDOM-Cd \\ \hline
   io\_RDOM\_Fe & 75 & .false. & logical & 0.0 & mol kg$^{-1}$ & R dissolved organic matter; iron \\ \hline
   io\_RDOM\_Fe\_56Fe & 82 & .false. & logical & 0.0 & \permil & d$^{56}$Fe of RDOM-Fe  \\ \hline
   io\_RDOM\_I & 95 & .false. & logical & 0.0 & mol kg$^{-1}$ & R dissolved organic matter; iodine \\ \hline  
   io\_CH4 & 25 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved methane (CH$_{4}$) \\ \hline
   io\_CH4\_13C & 26 & .false. & logical & 0.0 &  \permil & d$^{13}$C of CH$_{4}$ \\ \hline
   io\_CH4\_14C & 27 & .false. & logical & 0.0 &  \permil & d$^{14}$C of CH$_{4}$ \\ \hline
   io\_NH4 & 28 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved ammonium (NH$_{4}$) \\ \hline
   io\_NH4\_15N & 29 & .false. & logical & 0.0 &  \permil & d$^{15}$N of NH$_{4}$ \\ \hline
   io\_N2 & 30 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved nitrogen (N$_{2}$) \\ \hline
   io\_N2\_15N & 31 & .false. & logical & 0.0 &  \permil & d$^{15}$N of N$_{2}$ \\ \hline
   io\_N2O & 32 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved nitrous oxide (N$_{2}$O) \\ \hline
   io\_N2O\_15N & 33 & .false. & logical & 0.0 &  \permil & d$^{15}$N of N$_{2}$O \\ \hline
   io\_Cd & 34 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved cadmium (Cd) \\ \hline
   io\_Cd\_114 & 51 & .false. & logical & 0.0 &  \permil & d$^{114}$Cd of dissolved cadmium (Cd) \\ \hline
   io\_Ca & 35 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved calcium (Ca) \\ \hline
   io\_Ca\_44 & 76 & .false. & logical & 0.0 &  \permil & d$^{44}$Ca of dissolved calcium (Ca) \\ \hline
   \end{tabular}
   } % 这行是 resizebox 的结束
   \end{center}
   
   \begin{center}
   \resizebox{\textwidth}{!}{%
   \begin{tabular}{ | l | l | l | l | l | l | l |}
   \hline
    & &\multicolumn{2}{|l|}{SELECTION} &\multicolumn{2}{|l|}{INITILIZATION} & \\
    & &\multicolumn{2}{|l|}{gm\_ocn\_select\_n} &\multicolumn{2}{|l|}{bg\_ocn\_init\_n} & \\ \hline
   TRACER & INDEX & DEFAULT & UNITS & DEFAULT & UNITS & TRACER \\
   MNEMONIC & n & VALUE & & VALUE & & DESCRIPTION \\ \hline
   \multicolumn{7}{|l|}{OCEAN (DISSOLVED) TRACERS continued} \\ \hline
   io\_B & 36 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved boron (B) \\ \hline
   io\_F & 37 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved florine (F) \\ \hline
   io\_SO4 & 38 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved sulphate (SO$_{4}$) \\ \hline
   io\_SO4\_34S & 39 & .false. & logical & 0.0 &  \permil & d$^{34}$S of SO$_{4}$ \\ \hline
   io\_H2S & 40 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved hydrogen sulphide (H$_{2}$) \\ \hline
   io\_H2S\_34S & 41 & .false. & logical & 0.0 &  \permil  & d$^{34}$S of H$_{2}$S \\ \hline
   io\_Ge & 42 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved germanium (Ge) \\ \hline
   io\_Mo & 77 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved molybdenum (Mo) \\ \hline
   io\_Mo\_98Mo & 78 & .false. & logical & 0.0 &  \permil & d$^{98}$Mo of Mo\\ \hline
   io\_231Pa & 43 & .false. & logical & 0.0 & mol kg$^{-1}$ & $^{231}$Pa \\ \hline
   io\_230Th & 44 & .false. & logical & 0.0 & mol kg$^{-1}$ & $^{230}$Th \\ \hline
   io\_CFC11 & 45 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved CFC-11 \\ \hline
   io\_CFC12 & 46 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved CFC-12 \\ \hline
   io\_Mg & 50 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved magnesium (Mg) \\ \hline
   io\_Li & 53 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved lithium (Li) \\ \hline
   io\_Li\_7 & 54 & .false. & logical & 0.0 &  \permil & $^{7}$Li of Li \\ \hline
   io\_Nd & 55 & .false. & logical & 0.0 & mol  kg$^{-1}$ & dissolved neodymium (Nd) \\ \hline
   io\_Nd\_144 & 56 & .false. & logical & 0.0 &  \permil & $^{144}$Nd of Nd \\ \hline
   io\_SF6 & 47 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved sulphur hexafloride (SF6) \\ \hline
   io\_colr & 48 & .false. & logical & 0.0 & n/a & RED numerical (color) tracer \\ \hline
   io\_colb & 49 & .false. & logical & 0.0 & n/a & BLUE numerical (color) tracer \\ \hline
   io\_col0 & 57 & .false. & logical & 0.0 & n/a & numerical (color) tracer \\ \hline
   io\_col1 & 58 & .false. & logical & 0.0 & n/a & numerical (color) tracer \\ \hline
   io\_col2 & 59 & .false. & logical & 0.0 & n/a & numerical (color) tracer \\ \hline
   io\_col3 & 60 & .false. & logical & 0.0 & n/a & numerical (color) tracer \\ \hline
   io\_col4 & 61 & .false. & logical & 0.0 & n/a & numerical (color) tracer \\ \hline
   io\_col5 & 62 & .false. & logical & 0.0 & n/a & numerical (color) tracer \\ \hline
   io\_col6 & 63 & .false. & logical & 0.0 & n/a & numerical (color) tracer \\ \hline
   io\_col7 & 64 & .false. & logical & 0.0 & n/a & numerical (color) tracer \\ \hline
   io\_col8 & 65 & .false. & logical & 0.0 & n/a & numerical (color) tracer \\ \hline
   io\_col9 & 66 & .false. & logical & 0.0 & n/a & numerical (color) tracer \\ \hline
   io\_Fe & 9 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved iron III (Fe) \\ \hline
   io\_Fe2 & 83 & .false. & logical & 0.0 & mol kg$^{-1}$ & dissolved iron II (Fe) \\ \hline
   io\_L & 24 & .false. & logical & 0.0 & mol kg$^{-1}$ & free ligand (iron binding) \\ \hline
   io\_L2 & 84 & .false. & logical & 0.0 & mol kg$^{-1}$ & free ligand 2 (iron binding) \\ \hline
   io\_FeL & 23 & .false. & logical & 0.0 & mol kg$^{-1}$ & ligand-bound Fe \\ \hline
   io\_FeL2 & 85 & .false. & logical & 0.0 & mol kg$^{-1}$ & ligand2-bound Fe \\ \hline
   
   io\_Fe\_56Fe & 86 & .false. & logical & 0.0 &  \permil & $^{56}$Fe of dissolved iron III (Fe) \\ \hline
   io\_Fe2\_56 & 87 & .false. & logical & 0.0 &  \permil & $^{56}$Fe of dissolved iron II (Fe) \\ \hline
   io\_L\_56 & 88 & .false. & logical & 0.0 &  \permil & $^{56}$Fe of free ligand (iron binding) \\ \hline
   io\_L2\_56 & 89 & .false. & logical & 0.0 &  \permil & $^{56}$Fe of free ligand 2 (iron binding) \\ \hline
   io\_TDFe\_56Fe & 90 & .false. & logical & 0.0 & mol kg$^{-1}$ & total dissolved Fe \\ \hline
   io\_TDFe2\_56 & 91 & .false. & logical & 0.0 &  \permil & $^{56}$Fe of total dissolved Fe \\ \hline
   
   io\_TL & 42 & .false. & logical & 0.0 & mol kg$^{-1}$ & total dissolved ligand \\ \hline
   
   io\_I & 92 & .false. & logical & 0.0 & mol kg$^{-1}$ & iodide \\ \hline
   io\_IO3 & 93 & .false. & logical & 0.0 & mol kg$^{-1}$ & iodate \\ \hline

   io\_Ba & 96 & .false. & logical & 0.0 & mol  kg$^{-1}$ & dissolved barium (Ba) \\ \hline
   io\_Ba\_138Ba & 97 & .false. & logical & 0.0 &  \permil & $^{138}$Ba of Ba \\ \hline
   io\_Sr & 98 & .false. & logical & 0.0 & mol  kg$^{-1}$ & dissolved strontium (Sr) \\ \hline
   io\_Sr\_87Sr & 99 & .false. & logical & 0.0 &  \permil & $^{87}$Sr of Sr \\ \hline
   io\_Sr\_88Sr & 100 & .false. & logical & 0.0 &  \permil & $^{88}$Sr of Sr \\ \hline
  
   io\_H2O & 101 & .false. & logical & 0.0 & mol kg$^{-1}$ & water! \\ \hline
   
   
   \end{tabular}
      } % 这行是 resizebox 的结束
   \end{center}

   \begin{center}
   \resizebox{\textwidth}{!}{%
   \begin{tabular}{ | l | l | l | l | l | l | l |}
   \hline
    & &\multicolumn{2}{|l|}{SELECTION} &\multicolumn{2}{|l|}{INITILIZATION} & \\
    & &\multicolumn{2}{|l|}{gm\_sed\_select\_n} &\multicolumn{2}{|l|}{} & \\ \hline
   TRACER & INDEX & DEFAULT & UNITS & DEFAULT & UNITS & TRACER \\
   MNEMONIC & n & VALUE & & VALUE & & DESCRIPTION \\ \hline
   \multicolumn{7}{|l|}{SEDIMENT (SOLID, PARTICULATE) TRACERS} \\ \hline
   is\_NULL1 & 1 & .false. & logical & n/a & n/a & dummy index \\ \hline
   is\_NULL2 & 2 &  .false. & logical & n/a & n/a & dummy index \\ \hline
   is\_POC & 3 & .false. & logical & 0.0 & wt\% & particulate organic carbon (POC) \\ \hline
   is\_POC\_13C & 4 & .false. & logical & 0.0 &  \permil & d$^{13}$C of POC \\ \hline
   is\_POC\_14C & 5 & .false. & logical & 0.0 &  \permil & d$^{14}$C of POC \\ \hline
   is\_PON & 6 & .false. & logical & 0.0 & wt\% & particulate organic nitrogen (PON) \\ \hline
   is\_PON\_15N & 7 & .false. & logical & 0.0 &  \permil & d$^{15}$N of PON \\ \hline
   is\_POP & 8 & .false. & logical & 0.0 & wt\% & particulate organic phosphate \\
    & & & & & & (POP) \\ \hline
   is\_POCd & 9 & .false. & logical & 0.0 & wt\% & particulate organic cadmium \\
    & & & & & & (POCd) \\ \hline
   is\_POCd\_114Cd & 43 & .false. & logical & 0.0 &  \permil & d$^{114}$Cd of POC inorporated \\
    & & & & & & cadmium \\ \hline
   is\_POFe & 10 & .false. & logical & 0.0 & wt\% & particulate organic iron (POFe) \\ \hline
   is\_POI & 79 & .false. & logical & 0.0 & wt\% & particulate organic iodine (POI) \\ \hline
   is\_POBa & 80 & .false. & logical & 0.0 & wt\% & particulate organic barium (POBa) \\ \hline
   is\_POBa\_138Ba & 81 & .false. & logical & 0.0 & wt\% &d$^{138}$Ba pf particulate organic Ba (POBa) \\ \hline

   
   is\_POM\_231Pa & 11 & .false. & logical & 0.0 & wt\% & POM scavenged $^{231}$Pa \\ \hline
   is\_POM\_230Th & 12 & .false. & logical & 0.0 & wt\% & POM scavenged $^{230}$Th \\ \hline
   is\_POM\_Fe & 13 & .false. & logical & 0.0 & wt\% & POM scavenged Fe \\ \hline
   is\_POM\_Fe\_56Fe & 75 & .false. & logical & 0.0 &  \permil & d$^{56}$Fe of POM scavenged Fe\\ \hline
   is\_POM\_Nd & 47 & .false. & logical & 0.0 & wt\% & POM scavenged Nd \\ \hline
   is\_POM\_Nd\_144Nd & 48 & .false. & logical & 0.0 &  \permil & POM scavenged $^{144}$Nd \\ \hline
   

   is\_POM\_MoS2 & 58 & .false. & logical & 0.0 & wt\% & POM scavenged MoS2 \\ \hline
   is\_POM\_MoS2\_98Mo & 59 & .false. & logical & 0.0 &  \permil & POM scavenged $^{98}$Mo \\ \hline
   is\_POM\_MoS2\_34S & 60 & .false. & logical & 0.0 &  \permil & POM scavenged $^{34}$S \\ \hline
   is\_POM\_S & 73 & .false. & logical & 0.0 & wt\% & POM scavenged S \\ \hline
   is\_POM\_S\_34S & 74 & .false. & logical & 0.0 &  \permil & d$^{34}$S of POM scavenged S\\ \hline  
   is\_POM\_BaSO4 & 82 & .false. & logical & 0.0 & wt\% & POM scavenged BaSO4 \\ \hline
   is\_POM\_BaSO4\_138Ba & 83 & .false. & logical & 0.0 &  \permil & d$^{138}$Ba of POM scavenged BaSO4\\ \hline  
   
   is\_CaCO3 & 14 & .false. & logical & 0.0 & wt\% & calcium carbonate (CaCO$_{3}$) \\ \hline
   is\_CaCO3\_13C & 15 & .false. & logical & 0.0 &  \permil & d$^{13}$C of CaCO$_{3}$ \\ \hline
   is\_CaCO3\_14C & 16 & .false. & logical & 0.0 &  \permil & d$^{14}$C of CaCO$_{3}$ \\ \hline
   is\_CaCO3\_18O & 17 & .false. & logical & 0.0 &  \permil & d$^{18}$O of CaCO$_{3}$ \\ \hline
   is\_CaCO3\_44Ca & 17 & .false. & logical & 0.0 &  \permil & d$^{44}$Ca of CaCO$_{3}$ \\ \hline
   is\_CdCO3 & 18 & .false. & logical & 0.0 & wt\% & CaCO$_{3}$ incorporated cadmium \\ \hline
   is\_CdCO3\_114Cd & 44 & .false. & logical & 0.0 &  \permil & d$^{114}$Cd of CaCO$_{3}$ incorporated \\
    & & & & & & cadium \\ \hline
   is\_LiCO3 & 45 & .false. & logical & 0.0 & wt\% & CaCO$_{3}$ incorporated lithium \\ \hline
   is\_LiCO3\_7Li & 46 & .false. & logical & 0.0 &  \permil & d$^{7}$Li of CaCO$_{3}$ incorporated \\
    & & & & & & lithium \\ \hline
   is\_CaCO3\_231Pa & 19 & .false. & logical & 0.0 & wt\% & CaCO$_{3}$ scavenged $^{231}$Pa \\ \hline
   is\_CaCO3\_230Th & 20 & .false. & logical & 0.0 & wt\% & CaCO$_{3}$ scavenged $^{230}$Th \\ \hline
   is\_CaCO3\_Fe & 21 & .false. & logical & 0.0 & wt\% & CaCO$_{3}$ scavenged Fe \\ \hline
   is\_CaCO3\_Fe\_56Fe & 76 & .false. & logical & 0.0 & wt\% & d$^{56}$Fe of CaCO3 scavenged Fe \\ \hline
   is\_CaCO3\_Nd & 49 & .false. & logical & 0.0 & wt\% & CaCO$_{3}$ scavenged Nd \\ \hline
   is\_CaCO3\_Nd\_144Nd & 50 & .false. & logical & 0.0 &  \permil & CaCO$_{3}$ scavenged $^{144}$Nd \\ \hline
   is\_CaCO3\_MoS2 & 61 & .false. & logical & 0.0 & wt\% & CaCO3 scavenged MoS2 \\ \hline
   is\_CaCO3\_MoS2\_98Mo & 62 & .false. & logical & 0.0 &  \permil & CaCO3 scavenged $^{98}$Mo \\ \hline
   is\_CaCO3\_MoS2\_34S & 63 & .false. & logical & 0.0 &  \permil & CaCO3 scavenged $^{34}$S \\ \hline
   is\_SrCO3 & 84 & .false. & logical & 0.0 & wt\% & CaCO3 incorporated strontium \\ \hline
   is\_SrCO3\_87Sr & 85 & .false. & logical & 0.0 &  \permil & d$^{87}$Sr of SrCO$_{3}$ \\ \hline
   
   \end{tabular}
         } % 这行是 resizebox 的结束
   \end{center}

   \begin{center}
   \resizebox{\textwidth}{!}{%
   \begin{tabular}{ | l | l | l | l | l | l | l |}
   \hline
    & &\multicolumn{2}{|l|}{SELECTION} &\multicolumn{2}{|l|}{INITILIZATION} & \\
    & &\multicolumn{2}{|l|}{gm\_sed\_select\_n} &\multicolumn{2}{|l|}{} & \\ \hline
   TRACER & INDEX & DEFAULT & UNITS & DEFAULT & UNITS & TRACER \\
   MNEMONIC & n & VALUE & & VALUE & & DESCRIPTION \\ \hline
   \multicolumn{7}{|l|}{SEDIMENT (SOLID, PARTICULATE) TRACERS continued} \\ \hline
   is\_SrCO3\_88Sr & 86 & .false. & logical & 0.0 &  \permil & d$^{88}$Sr of SrCO$_{3}$ \\ \hline

   
   is\_det & 22 & .false. & logical & 0.0 & wt\% & detrital (refractory) material \\ \hline
   is\_det\_Li & 55 & .false. & logical & 0.0 & wt\% & detrital scavanged lithium \\ \hline
   is\_det\_Li\_7Li & 56 & .false. & logical & 0.0. &  \permil & detrital scavenged $^{7}$Li \\ \hline
   
   is\_det\_231Pa & 23 & .false. & logical & 0.0 & wt\% & detrital scavenged $^{231}$Pa \\ \hline
   is\_det\_230Th & 24 & .false. & logical & 0.0 & wt\% & detrital scavenged $^{230}$Th \\ \hline
   is\_det\_Fe & 25 & .false. & logical & 0.0 & wt\% & detrital scavenged Fe \\ \hline
   is\_det\_Fe\_56Fe & 77 & .false. & logical & 0.0 & wt\% & d$^{56}$Fe of detrital scavenged Fe \\ \hline
   is\_det\_Nd & 51 & .false. & logical & 0.0 & wt\% & detrital scavenged Nd \\ \hline
   is\_det\_Nd\_144Nd & 52 & .false. & logical & 0.0 &  \permil & detrital scavenged $^{144}$Nd \\ \hline
   is\_det\_MoS2 & 64 & .false. & logical & 0.0 & wt\% & det scavenged MoS2 \\ \hline
   is\_det\_MoS2\_98Mo & 65 & .false. & logical & 0.0 &  \permil & det scavenged $^{98}$Mo \\ \hline
   is\_det\_MoS2\_34S & 66 & .false. & logical & 0.0 &  \permil & det scavenged $^{34}$S \\ \hline

   is\_opal & 26 & .false. & logical & 0.0 & wt\% & opal \\ \hline
   is\_opal\_30Si & 27 & .false. & logical & 0.0 &  \permil & d$^{30}$Si of opal \\ \hline
   is\_opal\_Ge & 28 & .false. & logical & 0.0 & wt\% & opal incorporated germanium \\ \hline
   is\_opal\_231Pa & 29 & .false. & logical & 0.0 & wt\% & opal scavenged $^{231}$Pa \\ \hline
   is\_opal\_230Th & 30 & .false. & logical & 0.0 & wt\% & opal scavenged $^{230}$Th \\ \hline
   is\_opal\_Fe & 31 & .false. & logical & 0.0 & wt\% & opal scavenged Fe \\ \hline
   is\_opal\_Fe\_56Fe & 78 & .false. & logical & 0.0 & wt\% & d$^{56}$Fe of opal scavenged Fe \\ \hline
 
   
   is\_opal\_Nd & 53 & .false. & logical & 0.0 & wt\% & opal scavenged Nd \\ \hline
   is\_opal\_Nd\_144Nd & 54 & .false. & logical & 0.0 &  \permil & opal scavenged $^{144}$Nd \\ \hline
   
   is\_opal\_MoS2 & 67 & .false. & logical & 0.0 & wt\% & opal scavenged MoS2 \\ \hline
   is\_opal\_MoS2\_98Mo & 68 & .false. & logical & 0.0 &  \permil & opal scavenged $^{98}$Mo \\ \hline
   is\_opal\_MoS2\_34S & 69 & .false. & logical & 0.0 &  \permil & opal scavenged $^{34}$S \\ \hline
   is\_ash & 32 & .false. & logical & 0.0 & wt\% & ash \\ \hline
   is\_POC\_frac2 & 33 & .false. & logical & 0.0 & (ratio) & n/a \\ \hline
   is\_CaCO3\_frac2 & 34 & .false. & logical & 0.0 & (ratio) & n/a \\ \hline
   is\_opal\_frac2 & 35 & .false. & logical & 0.0 & (ratio) & n/a\\ \hline
      
%   \multicolumn{7}{|l|}{1- The ocean is initialized with no particulates in the ocean. Sediment composition is initialized with 100 wt percent ash in the surface sediment layer} & \\
%& &\multicolumn{7}{|l|}{and 100 wt percent detrital material in the underlying stack layers, so as to enable the construction of a constant sedimentation rate chronology (based)} & \\
%& &\multicolumn{7}{|l|}{on locating the consequential ash `peak'). These values are hard-coded} & \\
%& &\multicolumn{7}{|l|}{(in:~/genie/genie-sedgem/src/fortran/sedgem\_data.f90).} \\ \hline

%   \multicolumn{7}{|l|}{1- The ocean is initialized with no particulates in the ocean. Sediment composition is initialized with 100 wt percent ash in the surface sediment layer
%and 100 wt percent detrital material in the underlying stack layers, so as to enable the construction of a constant sedimentation rate chronology (based
%on locating the consequential ash `peak'). These values are hard-coded
%(in:~/genie/genie-sedgem/src/fortran/sedgem\_data.f90).\\
%2- The units are given for sediment composition. Particulate tracers in the ocean are in units of mol kg$^{-1}$ and per mil (\permil), corresponding to
%sediment units of wt percent and \permil, respectively.} \\ \hline

   is\_CaCO3\_age & 36 & .false. & logical & 0.0 & years & CaCO$_{3}$ numerical age tracer \\ \hline

   is\_ash\_age & 70 & .false. & logical & 0.0 & years & det numerical age tracer \\ \hline
   is\_POC\_size &  87 & .false. & logical & 0.0 & n/a & n/a \\ \hline
   is\_CaCO3\_red & 71 & .false. & logical & 0.0 & n/a &red numerical (color) tracer  \\ \hline
   is\_CaCO3\_blue & 72 & .false. & logical & 0.0 & n/a &blue numerical (color) tracer   \\ \hline
   
   is\_foram\_p\_13C & 37 & .false. & logical & 0.0 &  \permil & planktic foraminiferal CaCO$_{3}$ d$^{13}$C \\ \hline
   is\_foram\_p\_14C & 38 & .false. & logical & 0.0 &  \permil & planktic foraminiferal CaCO$_{3}$ d$^{14}$C \\ \hline
   is\_foram\_p\_18O & 39 & .false. & logical & 0.0 &  \permil & planktic foraminiferal CaCO$_{3}$ d$^{18}$O \\ \hline
   is\_foram\_b\_13C & 40 & .false. & logical & 0.0 &  \permil & benthic foraminiferal CaCO$_{3}$ d$^{13}$C \\ \hline
   is\_foram\_b\_14C & 41 & .false. & logical & 0.0 &  \permil & benthic foraminiferal CaCO$_{3}$ d$^{14}$C \\ \hline
   is\_foram\_b\_18O & 42 & .false. & logical & 0.0 &  \permil & benthic foraminiferal CaCO$_{3}$ d$^{18}$O \\ \hline
   \end{tabular}
            } % 这行是 resizebox 的结束
   \end{center}

   \begin{center}
   \resizebox{\textwidth}{!}{%
   \begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT VALUE & UNITS & DESCRIPTION \\ \hline
   \multicolumn{4}{|l|}{TIME STEPPING} \\ \hline
   ma\_koverall\_total & & (INTEGER) & overall model number of time-steps$^{1}$\\ \hline
   ma\_genie\_timestep & & s & length of each time-step \\ \hline
   bg\_par\_misc\_t\_start & 0.0 & years & simulation start year \\ \hline
   bg\_par\_misc\_t\_runtime & 1001.0 & years & simulation run length$^{2}$\\ \hline
   bg\_ctrl\_misc\_t\_BP & .false. & (LOGICAL) & simulation time scale as years Before Present \\ \hline
   sg\_par\_misc\_t\_runtime & 1001.0 & yr & simulation run length1 \\ \hline
   ma\_katm\_loop & 1 $^{3}$ & (INTEGER?) & \\ \hline
   ma\_ksic\_loop & 5 & (INTEGER) & relative frequency of updating of sea-ice \\ \hline
   ma\_kocn\_loop & 5 & (INTEGER) & relative frequency of updating of ocean \\ \hline
   ma\_conv\_kocn\_katchem & 5 & (INTEGER) & time-stepping ratio between ATCHEM and ocean \\ \hline
   ma\_conv\_kocn\_ksedgem & 50 & (INTEGER) & time-stepping ratio between SEDGEM and ocean \\ \hline
   ma\_conv\_kocn\_kbiogem & 5 & (INTEGER) & time-stepping ratio between BIOGEM and ocean \\ \hline
   ma\_conv\_kocn\_krokgem & 5 & (INTEGER) & time-stepping ratio between ROKGEM and ocean \\ \hline
   ma\_dt\_write & 720 & (INTEGER) & default interval of output $^{4}$ \\ \hline
   rg\_par\_screen\_output & 200 & (INTEGER) & ROKGEM reporting frequency \\
    & & & (in ROKGEM time-steps) \\ \hline
   ea\_3 & 1000 & (INTEGER) & frequency of 'health check' diagnostics reporting$^{5}$\\ \hline
   go\_3 & 1000 & (INTEGER) & frequency of 'health check' diagnostics reporting5 \\ \hline
   gs\_3 & 1000 & (INTEGER) & frequency of 'health check' diagnostics reporting5 \\ \hline
   ea\_5 & 100 & (INTEGER) & 'time series' frequency5 \\ \hline
   go\_5 & 100 & (INTEGER) & 'time series' frequency5 \\ \hline
   gs\_5 & 100 & (INTEGER) & 'time series' frequency5 \\ \hline
   ea\_6 & 50000 & (INTEGER) & 'average' frequency5 \\ \hline
   go\_6 & 50000 & (INTEGER) & 'average' frequency5 \\ \hline
   gs\_6 & 50000 & (INTEGER) & 'average' frequency5 \\ \hline
   \end{tabular}
   } % 这行是 resizebox 的结束
   \end{center}

      \begin{center}
 
   $^{1}$ This parameter sets the 'aging' of pre-existing (i.g., restart) sedimentary material consistent with the duration of a run. It must be equal to the run length of everything else. Obviously ;)\\
   $^{2}$ The length of each time-step is determined by the value of ma\_genie\_timestep (seconds), and is defined in genie\_eb\_go\_gs\_ac\_bg\_sg.config by: ma\_genie\_timestep = 365.25*24.0/500 * 3600.0, i.e., ma\_genie\_timestep=63115.2, giving 500 time-steps per year.\\
   $^{3}$ This means that the atmosphere (the EMBM in this case) is updated every GENIE time-step.\\
   $^{4}$ In multiples of the GENIE time-step.
   $^{5}$ When set equal to ma\_genie\_timestep+1, this effectively disables this feature.\\

   \end{center}
   
   \begin{center}
   \resizebox{\textwidth}{!}{%  
\begin{tabular}{ | l | l | l |}
   \hline
   \multicolumn{3}{|l|}{ARRAY SPECIFICATION: GRID} \\ \hline
   NAME & DEFAULT VALUE & DESCRIPTION \\ \hline
   GENIENXOPTS & `\$(DEFINE)GENIENX=36' & x (i) direction resolution in atmosphere \\ \hline
   GENIENYOPTS & `\$(DEFINE)GENIENY=36' & y (j) direction resolution in atmosphere \\ \hline
   GENIENLOPTS & `\$(DEFINE)GENIENL=1' & number of levels in atmosphere \\ \hline
   GOLDSTEINNLONSOPTS & `\$(DEFINE)GOLDSTEINNLONS=36' & x (i) direction resolution in ocean \\ \hline
   GOLDSTEINNLATSOPTS & `\$(DEFINE)GOLDSTEINNLATS=36' & y (j) direction resolution in oxcean \\ \hline
   GOLDSTEINNLEVSOPTS & `\$(DEFINE)GOLDSTEINNLEVS=8' & number of (depth) levels in ocean \\ \hline
   SEDGEMNLONSOPTS & `\$(DEFINE)SEDGEMNLONS=36' & x (i) direction resolution in sediments \\ \hline
   SEDGEMNLATSOPTS & `\$(DEFINE)SEDGEMNLATS=36' & y (j) direction resolution in sediments \\ \hline
   ROKGEMNLONSOPTS & `\$(DEFINE)ROKGEMNLONS=36' & x (i) direction resolution on land surface \\ \hline
   ROKGEMNLATSOPTS & `\$(DEFINE)ROKGEMNLATS=36' & y (j) direction resolution on land surface \\ \hline
   gm\_par\_grid\_lon\_offset & -260.0 & assumed longitudinal offset of the grid for \\
     &  & ATCHEM, BIOGEM, SEDGEM 2- and \\
     &  & 3-D field data saving \\
     &  & (units of degrees East) \\ \hline
   \multicolumn{3}{|l|}{ARRAY SPECIFICATION: NUMBER OF TRACERS} \\ \hline
   GOLDSTEINNTRACSOPTS & `\$(DEFINE)GOLDSTEINNTRACS=10' & number of dissolved tracers in ocean \\ \hline
   \end{tabular}
      } % 这行是 resizebox 的结束
   \end{center}

   
      \begin{center}
   \resizebox{\textwidth}{!}{% 
\begin{tabular}{ | l | l | l |}
   \hline
   NAME & DEFAULT VALUE & DESCRIPTION \\ \hline
   \multicolumn{3}{|l|}{RUN RE-START SPECIFICATION} \\ \hline
   ea\_7 & `n' & new/continuing run? (i.e., use restart?) \\ \hline
   ea\_rstdir\_name & `\$RUNTIME\_ROOT & \\
    & /genie-embm/data/input' & restart (input) directory \\ \hline
   ea\_35 & `tmp.1' & input ASCII restart file name \\ \hline
   ea\_29 & `spn' & output file number (restart file string) \\ \hline
   go\_7 & `n' & new/continuing run? (i.e., use restart?) \\ \hline
   go\_rstdir\_name & `\$RUNTIME\_ROOT & \\
    & /genie-goldsteindata/input' & restart (input) directory \\ \hline
   go\_23 & `tmp.1' & input ASCII restart file name \\ \hline
   go\_17 & `spn' & output file number (restart file string) \\ \hline
   gs\_7 & `n' & new/continuing run? (i.e., use restart?) \\ \hline
   gs\_rstdir\_name & `\$RUNTIME\_ROOT & \\
    & /genie-seaice/data/input' & restart (input) directory \\ \hline
   gs\_18 & `tmp.1' & input ASCII restart file name \\ \hline
   gs\_12 & `spn' & output file number (restart file string) \\ \hline
   ac\_ctrl\_continuing & .false. & continuing ATCHEM run? (i.e., use restart?) \\ \hline
   ac\_par\_rstdir\_name & `\$RUNTIME\_ROOT& \\
    & /genie-atchem/data/input' & ATCHEM restart (input) directory \\ \hline
   ac\_par\_infile\_name & `atchem' & input restart filename \\ \hline
   ac\_par\_outfile\_name & `atchem' & output restart filename \\ \hline
   bg\_ctrl\_continuing & .false. & continuing BIOGEM run? (i.e., use restart?) \\ \hline
   bg\_par\_rstdir\_name & '\$RUNTIME\_ROOT & \\
    & /genie-biogem/data/input' & BIOGEM restart (input) directory \\ \hline
   bg\_par\_infile\_name & `biogem' & input restart filename \\ \hline
   bg\_par\_outfile\_name & `biogem' & output restart filename \\ \hline
   sg\_ctrl\_continuing & .false. & continuing SEDGEM run? (i.e., use restart?) \\ \hline
   sg\_par\_rstdir\_name & `\$RUNTIME\_ROOT & \\
    & /genie-sedgem/data/input' & SEDGEM restart (input) directory \\ \hline
   sg\_par\_infile\_name & `sedgem' & input restart filename \\ \hline
   sg\_par\_outfile\_name & `sedgem' & output restart filename \\ \hline
   rg\_ctrl\_continuing & .false. & continuing ROKGEM run? (i.e., use restart?) \\ \hline
   - & - & - \\ \hline
   rg\_par\_infile\_name & `rokgem' & input restart filename \\ \hline
   rg\_par\_outfile\_name & `rokgem' & output restart filename \\ \hline
   \end{tabular}
       } % 这行是 resizebox 的结束
   \end{center}


        \begin{center}
   \resizebox{\textwidth}{!}{% 
   \begin{tabular}{ | l | l | l |}
   \hline
   NAME & DEFAULT VALUE & DESCRIPTION \\ \hline
   \multicolumn{3}{|l|}{INPUT/OUTPUT DIRECTORY SPECIFICATION} \\ \hline
   gm\_par\_gem\_indir\_name & `\$RUNTIME\_ROOT/ & \\
    & genie-main/data/input' & GEM data input directory \\ \hline
   ea\_1 & `\$RUNTIME\_ROOT & \\
    & /genie-embm/data/input' & data input directory \\ \hline
   ea\_2 & `\$RUNTIME\_OUTDIR & \\
    & /embm' & results output directory \\ \hline
   go\_1 & `\$RUNTIME\_ROOT & \\
    & /genie-goldstein/data/input' & data input directory \\ \hline
   go\_2 & `\$RUNTIME\_OUTDIR & \\
    & /goldstein' & results output directory \\ \hline
   gs\_1 & `\$RUNTIME\_ROOT & \\
    & /genie-seaice/data/input' & data input directory \\ \hline
   gs\_2 & `\$RUNTIME\_OUTDIR & \\
    & /seaice' & results output directory \\ \hline
   ac\_par\_indir\_name & `\$RUNTIME\_ROOT & \\
    & /genie-atchem/data/input'1 & ATCHEM data input directory \\ \hline
   ac\_par\_outdir\_name & `\$RUNTIME\_OUTDIR & \\
    & /atchem' & ATCHEM results output directory \\ \hline
   bg\_par\_indir\_name & `\$RUNTIME\_ROOT & \\
    & /genie-biogem/data/input' & BIOGEM data input directory \\ \hline
   bg\_par\_outdir\_name & `\$RUNTIME\_OUTDIR & \\
    & /biogem' & BIOGEM results output directory \\ \hline
   bg\_par\_fordir\_name & `\$RUNTIME\_ROOT & \\
    & /genie-biogem/data/input' & BIOGEM forcings (input) directory \\ \hline
   sg\_par\_indir\_name & `\$RUNTIME\_ROOT & \\
    & /genie-sedgem/data/input' & SEDGEM data input directory \\ \hline
   sg\_par\_outdir\_name & `\$RUNTIME\_OUTDIR & \\
    & /sedgem' & SEDGEM results output directory \\ \hline
   rg\_par\_indir\_name & `\$RUNTIME\_ROOT & \\
    & /genie-rokgem/data/input' & ROKEM data input directory \\ \hline
   rg\_par\_outdir\_name & `\$RUNTIME\_OUTDIR & \\
    & /rokgem' & ROKGEM results output directory \\ \hline
   \end{tabular}
         } % 这行是 resizebox 的结束
   \end{center}

          \begin{center}
   \resizebox{\textwidth}{!}{% 
\begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT VALUE & UNITS & DESCRIPTION \\ \hline
   \multicolumn{4}{|l|}{USEFUL(!) CLIMATE VARIABLES} \\ \hline 
   ma\_genie\_solar\_constant & 1368.0 & W m-2 & solar constant \\ \hline
   ea\_topo & `worbe2' & (STRING) & topography name1 \\ \hline
   ea\_dosc & .true. & (LOGICAL) & seasonal insolation forcing?2 \\ \hline
   ea\_diffa\_scl & 1.0 & (REAL) & atmospheric diffusivity scaling factor \\ \hline
   ea\_diffa\_len & 0 & (INTEGER) & grid point distance over which scalar is \\
    & & & applied (j direction) \\ \hline
   ea\_36 & `n' & ('y'/'n') & use ATCHEM CO2 to calculate radioative \\
    & & & forcing (else climate is invarient)? \\ \hline
   ea\_delf2x & 5.77 & W m-2 & climate sensitivity; radiative forcing \\
    & & & in W m-2 for a doubling of CO2 is \\
    & & & calculated as: delf2x x ln(2.0) \\ \hline
   go\_topo `worbe2' & (STRING) &  & topography filename1 \\ \hline
   go\_dosc & .true. & (LOGICAL) & seasonal insolation forcing?2 \\ \hline
   go\_ocnconv & 0 & (INTEGER) & ocean convection scheme3 \\ \hline
   gs\_dosc & .true. & (LOGICAL) & seasonal insolation forcing?2 \\ \hline
   \end{tabular}
        } % 这行是 resizebox 的结束
   \end{center}

1 Note that an extension of ``.k1'' is added automatically.
2 The three climate components modules must all include seasonal insolation forcing together or not (i.e., the 3 namelist prameter values must
have the same value).
1 Current options are: 0 = original; 1 = Mueller.
\begin{center}
\resizebox{\textwidth}{!}{% 
\begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT VALUE & UNITS & DESCRIPTION \\ \hline
   \multicolumn{4}{|l|}{GENERAL BIOGEOCHEMISTRY} \\ \hline
   gm\_par\_carbconstset\_name & ``Mehrbach'' & (STRING) & carbonate dissociation constants set \\ \hline
    & & &  \\ \hline
    & & &  \\ \hline
    & & &  \\ \hline
    & & &  \\ \hline
   \multicolumn{4}{|l|}{ATMOSPHERE BIOGEOCHEMISTRY} \\ \hline
   ac\_par\_atm\_wetlands\_FCH4 & 0.0  & mol yr$^{-1}$ & Wetlands CH$_{4}$ flux  \\ \hline
   ac\_par\_atm\_wetlands\_FCH4\_d13C & 0.0 & \permil & Wetlands CH$_{4}$ d$^{13}$C \\ \hline
   \end{tabular}
   } % 这行是 resizebox 的结束
   \end{center}


\begin{center}
\resizebox{\textwidth}{!}{% 
\begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT VALUE & UNITS & DESCRIPTION \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: MISC CONTROL} \\ \hline
   bg\_ctrl\_misc\_Snorm & .true. & (LOGICAL) & tracer update with salinity \\
    & & & normalization \\ \hline
   bg\_ctrl\_misc\_noSnorm & .false. & (LOGICAL) & tracer update without salinity \\
    & & & normalization \\ \hline
   bg\_ctrl\_misc\_nobioupdate & .false. & (LOGICAL) & tracer update with no \\
    & & & biological overprint \\ \hline
   bg\_ctrl\_misc\_brinerejection\_bgc & .false. & (LOGICAL) & Include biogeochem in Sea-ice brine \\
    & & & rejection? \\ \hline
   bg\_par\_misc\_brinerejection\_frac & 0.0 & (LOGICAL) & Sea-ice brine rejection fraction \\ \hline
   bg\_par\_misc\_brinerejection\_jmax & 36 & (LOGICAL & Max j for sea-ice brine rejection \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: BOUNDARY CONDITIONS} \\ \hline
   bg\_ctrl\_force\_sed\_closedsystem & .true. & (LOGICAL) & Dissolution flux = rain flux to \\
    & & & close system? \\ \hline
   bg\_ctrl\_force\_GOLDSTEInTS & .false. & (LOGICAL) & Allow temperature / salinity \\
    & & & forcing of climate? \\ \hline
   bg\_ctrl\_force\_seaice & .false. & (LOGICAL) & Replace internal fractional \\
    & & & sea-ice cover field? \\ \hline
   bg\_ctrl\_force\_windspeed & .true. & (LOGICAL) & Replace internal wind-speed field? \\ \hline
   bg\_ctrl\_force\_CaCO3toPOCrainratio & .false. & (LOGICAL) & Replace internal CaCO$_{3}$:POC \\
    & & & export rain ratio? \\ \hline
   bg\_ctrl\_force\_POCdtoPOCrainratio & .false. & (LOGICAL) & Replace internal POCd:POC \\
    & & & export rain ratio? \\ \hline
   bg\_ctrl\_force\_Cd\_alpha & .false. & (LOGICAL) & Replace internal [Cd/P]POM/\\
    & & & [Cd/P]SW alpha? \\ \hline
   bg\_ctrl\_force\_scav\_fpart\_POC & .false. & (LOGICAL) & Replace internal POC flux for $^{230}$Th\\
    & & &  and 231Pa isotope scavenging? \\ \hline
   bg\_ctrl\_force\_scav\_fpart\_CaCO3 & .false. & (LOGICAL) & Replace internal CaCO$_{3}$ flux for $^{230}$Th\\
    & & &  and $^{231}$Pa isotope scavenging? \\ \hline
   bg\_ctrl\_force\_scav\_fpart\_opal & .false. & (LOGICAL) & Replace internal opal flux for $^{230}$Th and \\
    & & & $^{231}$Pa isotope scavenging? \\ \hline
   bg\_ctrl\_force\_scav\_fpart\_det & .false. & (LOGICAL) & Replace internal det flux for $^{230}$Th \\
    & & & and $^{231}$Pa isotope scavenging? \\ \hline
   bg\_ctrl\_force\_solconst & .false. & (LOGICAL) & Replace solar constant \\
    & & & (with time-varying IP)? \\ \hline
   bg\_ctrl\_force\_oldformat & .false. & (LOGICAL) & Use old tracer forcing \\
    & & & file format? \\ \hline
   bg\_par\_seaice\_file & 'seaice.dat' & (STRING) & Filename for prescribed BIOGEM \\
    & & & seaice boundary condition \\ \hline
   bg\_par\_windspeed\_file & 'windspeed.dat' &(STRING) & Filename for prescribed \\
    & & & BIOGEM windspeed (air-sea gas\\
    & & &  exchange) boundary condition \\ \hline
   bg\_par\_CaCO3toPOCrainratio\_file & 'CaCO3toPOC' & (STRING) & Filename for prescribed \\
    & & & BIOGEM CaCO$_{3}$:POC rain \\
    & rainratio.dat' & & ratio boundary condition \\ \hline
   bg\_par\_POCdtoPOCrainratio\_file & 'POCdtoPOC' & (STRING) & Filename for prescribed \\
    & & & BIOGEM POCd:POC rain \\
    & rainratio.dat' & & ratio boundary condition \\ \hline
   bg\_par\_Cd\_alpha\_file 'Cd\_alpha.dat' & & (STRING) & Filename for prescribed Cd partition \\
    & & & coefficient alpha field \\ \hline
   bg\_par\_gastransfer\_a & 0.310 & ??? & Value of Wanninkhof [1992] gas \\
    & & & transfer coeff, a \\ \hline
   \end{tabular}
      } % 这行是 resizebox 的结束
   \end{center}

  \begin{center}
\resizebox{\textwidth}{!}{% 
  \begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT VALUE & UNITS & DESCRIPTION \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: MISC CONTROL continued ..} \\ \hline
   bg\_par\_scav\_fpart\_POC\_file & scav\_fpart\_POC.dat & (STRING) & \\ \hline
   bg\_par\_scav\_fpart\_CaCO3\_file & scav\_fpart\_CaCO3.dat & (STRING) & \\ \hline
   bg\_par\_scav\_fpart\_opal\_file & scav\_fpart\_opal.dat & (STRING) & \\ \hline
   bg\_par\_scav\_fpart\_det\_file & scav\_fpart\_det.dat & (STRING) & \\ \hline
   \end{tabular}
         } % 这行是 resizebox 的结束
   \end{center}

     \begin{center}
\resizebox{\textwidth}{!}{%
   \begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT VALUE & UNITS & DESCRIPTION \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: BIOLOGICAL NEW PRODUCTION} \\ \hline
   bg\_par\_bio\_prodopt & '1N1T\_PO4MM' & (STRING) & biological scheme ID \\ \hline
   bg\_par\_bio\_k0\_PO4 & 2.0E-06 & mol kg$^{-1}$ yr$^{-1}$ & maximum PO$_{4}$ consumption rate \\ \hline
   bg\_par\_bio\_k0\_NO3 & 32.0E-06 & mol kg$^{-1}$ yr$^{-1}$ & maximum NO3 consumption rate \\ \hline
   bg\_par\_bio\_c0\_PO4 & 0.050E-06 & mol kg$^{-1}$ & [PO$_{4}$] M-M half-sat value \\ \hline
   bg\_par\_bio\_c0\_NO3 & 3.200E-06 & mol kg$^{-1}$ & [NO3] M-M half-sat value \\ \hline
   bg\_par\_bio\_c0\_N & 1.600E-06 & mol kg$^{-1}$ & [NO3]+[NH$_{4}$] M-M half-sat value \\ \hline
   bg\_par\_bio\_c0\_Fe & 0.030E-09 & mol kg$^{-1}$ & [Fe] M-M half-sat value \\ \hline
   bg\_par\_bio\_c0\_Fe\_sp & 0.125E-09 & mol kg$^{-1}$ & [Fe] M-M half-sat value for siliceous \\
    & & & phytoplankton \\ \hline
   bg\_par\_bio\_c0\_Fe\_nsp & 0.067E-09 & mol kg$^{-1}$ & [Fe] M-M half-sat value for non-siliceous \\
    & & & phytoplankton \\ \hline
   bg\_par\_bio\_c0\_SiO2 & 10.0E-06 & mol kg$^{-1}$ & [H$_{4}$SiO$_{4}$] M-M half-sat value \\ \hline
   bg\_par\_bio\_zc & 75.0 & m & Biological production zone depth \\
    & & & (OCMIP-2) \\ \hline
   bg\_par\_bio\_tau & 15 & days & Biological production time-scale \\
    & & & (OCMIP-2) \\ \hline
   bg\_par\_bio\_relprod\_sp & 0.952381 & ratio &  Fractional production of siliceous \\
    & & & phytoplankton in Si/Fe-replete conditions. \\
    & & & (20:1 for siliceous to non-siliceous \\
    & & & phytoplanktion production \\
    & & & (Ridgwell, 2001, PhD. Thesis) \\ \hline
   bg\_par\_bio\_I\_eL & 20.0 & m & Light e-folding depth (OCMIP-2) \\ \hline
   bg\_par\_bio\_kT0 & 0.59 &  & coefficient for temperature-dependent \\
    & & & uptake rate modifier \\ \hline
   bg\_par\_bio\_kT\_eT & 15.8 & K & e-folding temperature for T-dep. \\
    & & & uptake rate modifier \\ \hline
   \end{tabular}
            } % 这行是 resizebox 的结束
   \end{center}
   
        \begin{center}
\resizebox{\textwidth}{!}{%
   \begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT & UNITS & DESCRIPTION \\
    & VALUE & & \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: ORGANIC MATTER UPTAKE (EXPORT) RATIOS} \\ \hline
   bg\_par\_bio\_red\_POP\_PON & 16.0 & n/a & N/P organic matter Redfield ratio \\ \hline
   bg\_par\_bio\_red\_POP\_POC & 106.0 & n/a & C/P organic matter Redfield ratio \\ \hline
   bg\_par\_bio\_red\_POP\_PO2 & -138.0 & n/a & O2/P organic matter pseudo-Redfield ratio \\ \hline
   bg\_par\_bio\_red\_PON\_ALK & -1.00 & n/a & ALK/N alkalinty correction factor \\ \hline
   bg\_par\_bio\_red\_DOMfrac & 0.66 & n/a & production fraction of dissolved organic matter \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: INORGANIC MATTER UPTAKE (EXPORT) RATIOS} \\ \hline
   bg\_par\_bio\_red\_POC\_CaCO3 & 0.2 & (LOGICAL) &  base CaCO$_{3}$:POC export ratio \\ \hline
   bg\_par\_bio\_red\_POC\_CaCO3\_pP & 0.0 & (LOGICAL) & exponent for modifier of \\
    & & & CaCO$_{3}$:POC export ratio \\ \hline
   bg\_par\_bio\_red\_POC\_opal & 1.0 & (LOGICAL) & base opal:POC export ratio \\ \hline
   \end{tabular}
               } % 这行是 resizebox 的结束
   \end{center}

           \begin{center}
\resizebox{\textwidth}{!}{%
\begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT & UNITS & DESCRIPTION \\
    & VALUE & & \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: REMINERALIZATION} \\ \hline
   bg\_par\_bio\_remin\_DOMlifetime & 0.5 & yrs & DOC lifetime \\ \hline
   bg\_par\_bio\_remin\_CH4rate & 1.0e-4 & d$^{-1}$ & Specific CH$_{4}$ oxidation rate \\ \hline
   bg\_ctrl\_bio\_remin\_POC\_fixed & .true. & (LOGICAL) & fixed-profile POM remineralization? \\ \hline
   bg\_ctrl\_bio\_remin\_POC\_ballast & .false. & (LOGICAL) & Ballasting parameterization? \\ \hline
   bg\_par\_bio\_remin\_POC\_frac2 & 0.05 & n/a & initial fractional abundance of fraction \#2 \\ \hline
   bg\_par\_bio\_remin\_POC\_eL1 & 500.0 & m & remineralization length: fraction \#1 \\ \hline
   bg\_par\_bio\_remin\_POC\_eL2 & 1000000.0 & m & remineralization length: fraction \#2 \\ \hline
   bg\_ctrl\_bio\_remin\_CaCO3\_fixed & .true. & (LOGICAL) & fixed-profile CaCO$_{3}$ remineralization? \\ \hline
   bg\_par\_bio\_remin\_CaCO3\_frac2 & 0.5 & n/a & initial fractional abundance of fraction \#2 \\ \hline
   bg\_par\_bio\_remin\_CaCO3\_eL1 & 1000.0 & m & remineralization length: fraction \#1 \\ \hline
   bg\_par\_bio\_remin\_CaCO3\_eL2 & 1000000.0 & m & remineralization length: fraction \#2 \\ \hline
   bg\_ctrl\_bio\_remin\_opal\_fixed & .false. & (LOGICAL) & fixed-profile opal remineralization? \\ \hline
   bg\_par\_bio\_remin\_opal\_frac2 & 0.5 & n/a & initial fractional abundance of fraction \#2 \\ \hline
   bg\_par\_bio\_remin\_opal\_eL1 & 1000.0 & m & remineralization length: fraction \#1 \\ \hline
   bg\_par\_bio\_remin\_opal\_eL2 & 1000000.0 & m & remineralization length: fraction \#2 \\ \hline
   bg\_par\_bio\_remin\_sinkingrate & 125.0 & m d$^{-1}$ & prescribed particle sinking rate \\ \hline
   bg\_par\_bio\_remin\_ballast\_kc & 0.130 & & Organic matter carrying capacity of CaCO$_{3}$ \\ \hline
   bg\_par\_bio\_remin\_ballast\_ko & 0.0 & & Organic matter carrying capacity of opal \\ \hline
   bg\_par\_bio\_remin\_ballast\_kl & 0.0 & & Organic matter carrying capacity of lithogenics \\ \hline
   bg\_ctrl\_bio\_remin\_ONtoNH4 & .false. & (LOGICAL) & aerobic remineralization of ON; \\
   & & &  NH$_{4}$ (not NO3) \\ \hline
   bg\_par\_bio\_remin\_denitrO2thresh & 0.0 & mol kg$^{-1}$ & Denitrification [O2] threshold \\ \hline
   bg\_ctrl\_bio\_remin\_reminfix & .false. & (LOGICAL) & Stop rapidly-oxidizing species going $<$ 0.0? \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: ISOTOPIC FRACTIONATION} \\ \hline
   bg\_par\_d13C\_DIC\_Corg\_ef & 25 & & Fractionation for intercellular C fixation \\
   & & & (Ridgwell, 2001, PhD. Thesis) \\ \hline
   bg\_par\_d13C\_DIC\_Corg\_ef\_sp & 25 & & Fractionation for intercellular C fixation of \\
   & & & siliceous phytoplanktion (Ridgwell, 2001, \\
    & & & PhD. Thesis) \\ \hline
   bg\_par\_d13C\_DIC\_Corg\_ef\_nsp & 20 & & Fractionation for intercellular C fixation of \\
   & & & non-siliceous phytoplanktion \\
   & & & (Ridgwell, 2001, PhD. Thesis) \\ \hline
   bg\_ar\_d30Si\_opal\_epsilon & -1.1 & \permil & Fractionation of $^{30}$ during opal formation by \\
   & & & diatoms. Default value: -1.1 \\
    & & & (De La Rocha et al., 1997) \\ \hline
   bg\_par\_d114Cd\_POCd\_epsilon & -1.0 & & \*\*\* d$^{114}$Cd = 1.0006 \*\*\* \\ \hline
   bg\_par\_d7Li\_LiCO3\_epsilon & 3.0 & & 7/6Li fractionation between Li and LiCO \\ \hline
   bg\_opt\_bio\_foram\_p\_13C\_delta & NONE & (STRING) & Planktic foram $^{13}$C fractionation \\
   & & & scheme ID string \\ \hline
   \end{tabular}
                  } % 这行是 resizebox 的结束
   \end{center}

              \begin{center}
\resizebox{\textwidth}{!}{%
\begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT & UNITS & DESCRIPTION \\
    & VALUE & & \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: IRON} \\ \hline
   bg\_par\_det\_Fe\_sol & 1.0 & n/a & fractional aeolian Fe solubility \\ \hline
   bg\_par\_det\_Fe\_sol\_exp & 1.0 & n/a & exponent for aeolian Fe solubility1 \\ \hline
   bg\_ctrl\_bio\_red\_fixedFetoC & .false. & (LOGICAL) & fixed cellular Fe:C ratio? \\ \hline
   bg\_par\_bio\_red\_POFe\_POC & 250000.0 & n/a & C/Fe organic matter ratio \\ \hline
   bg\_ctrl\_bio\_Fe\_fixedKscav & .false. & fixed scavening & \\
   & & rate & (if not: Parekh scheme)? \\ \hline
   bg\_par\_scav\_Fe\_Ks & 0.1E-3 & d$^{-1}$ & fixed Fe scavenging rate \\ \hline
   bg\_par\_scav\_Fe\_sf\_POC & 0.300 & n/a & Parekh Fe scavenging rate scale \\
   & & & factor: POC \\ \hline
   bg\_par\_scav\_Fe\_sf\_CaCO3 & 0.0 & n/a & Parekh Fe scavenging rate scale \\
   & & & factor: CaCO$_{3}$ \\ \hline
   bg\_par\_scav\_Fe\_sf\_opal & 0.0 & n/a & Parekh Fe scavenging rate scale \\
   & & & factor: opal \\ \hline
   bg\_par\_scav\_Fe\_sf\_det & 0.0 & n/a & Parekh Fe scavenging rate scale \\
   & & & factor: det \\ \hline
   bg\_par\_scav\_fremin & 1.0 & n/a & Fraction of scavenged Fe remineralizable \\ \hline
   bg\_ctrl\_bio\_NO\_fsedFe & .true. & (LOGICAL) & Prevent return of Fe \\
   & & & from the sediments? \\ \hline
   bg\_par\_K\_FeL\_pP & 11.0 & & log10 of Fe ligand stability constant K'(FeL) \\ \hline
   bg\_par\_bio\_FetoC\_pP & -0.4225 & & [FeT] dependent Fe:C ratio \\
   & & & [Ridgwell, 2001] -- power \\ \hline
   bg\_par\_bio\_FetoC\_K & 94500.0 & & [FeT] dependent Fe:C ratio \\
   & & & [Ridgwell, 2001] -- scaling \\ \hline
   bg\_par\_bio\_FetoC\_C & 0.0 & & [FeT] dependent Fe:C ratio \\
   & & & [Ridgwell, 2001] -- constant \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: SILICA} \\ \hline
    & & & \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: NITROGEN} \\ \hline
   bg\_par\_bio\_mu1 & 1.0 & yr$^{-1}$ mu$^{-1}$ & maximum rate of export production \\ \hline
   bg\_par\_bio\_mu2 & 0.2 & yr$^{-1}$ mu-2 & maximum rate of export production \\
   & & & from N$_{2}$-fixation \\ \hline
   bg\_par\_bio\_N2fixthresh & 100.0E-06 & mol yr$^{-1}$ & Threshold NO3 + NH$_{4}$ to \\
   & & & encourage N$_{2}$ fixation \\ \hline
   bg\_par\_bio\_Nstar\_offset & 2.90E-06 & mol yr$^{-1}$ & N-star calculation offset \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: TRACE METALS} \\ \hline
   bg\_par\_bio\_red\_POC\_POCd & 0.0E-6 & n/a & Default cellular C:Cd (Cd/C) ratio \\ \hline
   bg\_par\_bio\_red\_POC\_POCd\_alpha & 10.0 & n/a & [Cd/P]POM/[Cd/P]SW partition \\
   & & & coefficient (alpha) \\ \hline
   bg\_ctrl\_bio\_red\_CdtoC\_Felim & .true. & (LOGICAL) & Fe-limitation dependent \\
   & & & Cd:C 'Redfield' uptake ratio? \\ \hline
   bg\_par\_bio\_red\_CdtoC\_Felim\_min & 3.000E-6 & n/a & Minimum (Fe replete) \\
   & & & Cd:C uptake ratio \\ \hline
   bg\_par\_bio\_red\_CdtoC\_Felim\_max & 6.000E-6 & n/a & Maximum (Fe limited) \\
   & & & Cd:C uptake ratio \\ \hline
   bg\_par\_bio\_red\_CaCO3\_LiCO3 & 0.0E-6 & & Default CaCO$_{3}$ Ca:Li ratio \\ \hline
   bg\_par\_bio\_red\_CaCO3\_LiCO3\_alpha & 1.0 & & partition coefficient (alpha) \\ \hline
   \end{tabular}
   } % 这行是 resizebox 的结束
   \end{center}

   \begin{center}
   \resizebox{\textwidth}{!}{%
   \begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT & UNITS & DESCRIPTION \\ 
   & VALUE & & \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: $^{230}$Th AND $^{231}$Pa} \\ \hline
   bg\_par\_scav\_230Th\_scavopt & & (STRING) & Scavenging scheme ID string for $^{230}$Th \\ \hline
   bg\_par\_scav\_231Pa\_scavopt & & (STRING) & Scavenging scheme ID string for $^{231}$Pa \\ \hline
   bg\_par\_scav\_230Th\_KPOC & 1.e7 & & Equilibrium partition coefficient for POC associated \\
    & & & $^{230}$Th. Default value of 1e7 used by Siddall et al.\\
    & & & (2005) in their control simulation. \\ \hline
   bg\_par\_scav\_230Th\_KCaCO3 & 1.e7 & & Equilibrium partition coefficient for CaCO$_{3}$ \\
   & & & associated $^{230}$Th. Default value of 1e7 \\
   & & & used by Siddall et al. (2005) in their \\
   & & & control simulation. \\ \hline
   bg\_par\_scav\_230Th\_Kopal & 0.05e7 & & Equilibrium partition coefficient for opal associated \\
   & & & $^{230}$Th. Default value of 0.05e7 used by Siddall et al.\\
   & & & (2005)in their control simulation. \\ \hline
   bg\_par\_scav\_230Th\_Kdet & 0 & & Equilibrium partition coefficient for detrital \\
   & & & associated $^{230}$Th. Default value of 0 used by Siddall \\
   & & & et al. (2005) in their control simulation. \\ \hline
   bg\_par\_scav\_231Pa\_KPOC & 1.e7 & & quilibrium partition coefficient for POC associated \\
   & & & $^{231}$Pa. Default value of 1e7 used by Siddall \\
   & & & et al. (2005) in their control simulation. \\ \hline
   bg\_par\_scav\_231Pa\_KCaCO3 & 0.025e7 & & Equilibrium partition coefficient for CaCO$_{3}$ \\
   & & & associated $^{231}$Pa. Default value of 0.025e7 \\
   & & & used by Siddall et al. (2005) in their control \\
   & & & simulation. \\ \hline
   bg\_par\_scav\_231Pa\_Kopal & 0.1667e7 & & Equilibrium partition coefficient for opal \\
   & & & associated $^{231}$Pa. Default value of 0.1667e7 \\
   & & & used by Siddall et al. (2005)in their \\
   & & & control simulation. \\ \hline
   bg\_par\_scav\_231Pa\_Kdet & 0 & & Equilibrium partition coefficient for detrital \\
   & & & associated $^{231}$Pa. Default value of 1e7 used by \\
   & & & Siddall et al. (2005) in their control simulation. \\ \hline
   bg\_par\_scav\_230Th\_indepsinkingvel & 1000.0 & m yr$^{-1}$ & Independent scheme for sinking of particle \\
    & & & associated $^{230}$Th: non-zero velocity enables \\
    & & & independent scheme and  disables settling in \\
    & & & accord with the settling of the scavenging \\
    & & & particulate type. Default value of 1000.0 \\
    & & & used by Siddall et al. (2005)in their control \\
    & & & simulation. \\ \hline
   bg\_par\_scav\_231Pa\_indepsinkingvel & 1000.0 & m yr$^{-1}$ & Independent scheme for sinking of particle\\
    & & & associated $^{231}$Pa: non-zero velocity enables \\
    & & & independent scheme and disbles settling in \\
    & & & accord with the settling of the scavenging \\
    & & & particulate type. Default value of 1000.0 \\
    & & & used by Siddall et al. (2005)in their control \\
    & & & simulation. \\ \hline
   \end{tabular}
      } % 这行是 resizebox 的结束
   \end{center}

      \begin{center}
   \resizebox{\textwidth}{!}{%
\begin{tabular}{ | l | l | l |  l |}
   \hline
   NAME & DEFAULT VALUE & UNITS & DESCRIPTION \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: ABIOTIC PRECIPITATION} \\ \hline
   bg\_par\_bio\_CaCO3precip\_sf & 0.0 & & Scale factor for CaCO$_{3}$ precipitation \\ \hline
   bg\_par\_bio\_CaCO3precip\_exp & 0.0 & & Rate law power for CaCO$_{3}$ precipitation \\ \hline
   bg\_ctrl\_bio\_CaCO3precip & .false. & (LOGICAL) & Allow abiotic CaCO$_{3}$ precipitation? \\ \hline
   bg\_ctrl\_bio\_CaCO3precip\_sur & .true. & (LOGICAL) & Restrict precipitation to surface layer? \\ \hline
   \end{tabular}
         } % 这行是 resizebox 的结束
   \end{center}

1 Use a value of 1.0 for uniform solubility.

      \begin{center}
   \resizebox{\textwidth}{!}{%
\begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT VALUE & UNITS & DESCRIPTION \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: DATA SAVING: TIME-SLICES} \\ \hline
   bg\_ctrl\_data\_save\_slice\_ocnatm & .false. & (LOGICAL) & atmospheric (interface) composition (2D)? \\ \hline
   bg\_ctrl\_data\_save\_slice\_ocn & .true. & (LOGICAL) & ocean composition (3D)? \\ \hline
   bg\_ctrl\_data\_save\_slice\_ocnsed & .false. & (LOGICAL) & sediment (interface) composition (2D)? \\ \hline
   bg\_ctrl\_data\_save\_slice\_fairsea & .true. & (LOGICAL) & Air-sea gas exchange (2D)? \\ \hline
   bg\_ctrl\_data\_save\_slice\_focnatm & .false. & (LOGICAL) & ocean-atmosphere flux (2D)? \\ \hline
   bg\_ctrl\_data\_save\_slice\_focnsed & .false. & (LOGICAL) & ocean-sediment flux (2D)? \\ \hline
   bg\_ctrl\_data\_save\_slice\_fsedocn & .false. & (LOGICAL) & sediment-ocean flux (2D)? \\ \hline
   bg\_ctrl\_data\_save\_slice\_bio & .true. & (LOGICAL) & biological fluxes (3D)? \\ \hline
   bg\_ctrl\_data\_save\_slice\_carb & .true. & (LOGICAL) & aqueous carbonate system properties (3D)? \\ \hline
   bg\_ctrl\_data\_save\_slice\_carbconst & .false. & (LOGICAL) & aqueous carbonate system constants (3D)? \\ \hline
   bg\_ctrl\_data\_save\_slice\_phys\_atm & .false. & (LOGICAL) & atmospheric physical properties (2D)? \\ \hline
   bg\_ctrl\_data\_save\_slice\_phys\_ocn & .false. & (LOGICAL) & ocean physical properties (3D)? \\ \hline
   bg\_ctrl\_data\_save\_slice\_misc & .true. & (LOGICAL) & miscellaneous properties (-)? \\ \hline
   bg\_ctrl\_data\_save\_slice\_diag & .false. & (LOGICAL) & biogeochemical diagnostics? \\ \hline
   bg\_par\_data\_save\_slice\_dt & 1.0 & yr & integration interval \\ \hline
   bg\_par\_infile\_slice\_name & `biogem\_save & (STRING) & time-slice mid-point specification filename \\ 
   & \_timeslice.dat' & & \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: DATA SAVING: TIME-SERIES} \\ \hline
   bg\_ctrl\_data\_save\_sig\_ocnatm & .true. & (LOGICAL) & atmospheric (interface) composition? \\ \hline
   bg\_ctrl\_data\_save\_sig\_ocn & .true. & (LOGICAL) & oceanic composition? \\ \hline
   bg\_ctrl\_data\_save\_sig\_fexport & .true. & (LOGICAL) & export flux? \\ \hline
   bg\_ctrl\_data\_save\_sig\_fairsea & .true. & (LOGICAL) & Air-sea gas exchange? \\ \hline
   bg\_ctrl\_data\_save\_sig\_ocnsed & .true. & (LOGICAL) & sediment (interface) composition? \\ \hline
   bg\_ctrl\_data\_save\_sig\_focnatm & .false. & (LOGICAL) & ocean->atmosphere flux? \\ \hline
   bg\_ctrl\_data\_save\_sig\_focnsed & .true. & (LOGICAL) & ocean->sediment flux? \\ \hline
   bg\_ctrl\_data\_save\_sig\_fsedocn & .true. & (LOGICAL) & sediment->ocean flux? \\ \hline
   bg\_ctrl\_data\_save\_sig\_ocnSS & .true. & (LOGICAL) & ocean surface tracers? \\ \hline
   bg\_ctrl\_data\_save\_sig\_carbSS & .true. & (LOGICAL) & ocean surface carbonate chemistry? \\ \hline
   bg\_ctrl\_data\_save\_sig\_misc & .true. & (LOGICAL) & miscellaneous properties? \\ \hline
   bg\_ctrl\_data\_save\_sig\_diag & .true. & (LOGICAL) & biogeochemical diagnostics? \\ \hline
   bg\_par\_data\_save\_sig\_dt & 1.0 & yr & integration interval \\ \hline
   bg\_par\_infile\_sig\_name & `biogem\_save\_sig.dat' & (STRING) & time-slice mid-point specification filename \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: DATA SAVING: TIME-MISC} \\ \hline
   bg\_ctrl\_data\_save\_derived & .false. & (LOGICAL) & save `derived'1 data? \\ \hline
   bg\_ctrl\_data\_save\_GLOBAL & .true. & (LOGICAL) & save global diagnostics2? \\ \hline
   bg\_ctrl\_data\_save\_slice\_ascii & .false. & (LOGICAL) & save time-slices in ASCII format? \\ \hline
   bg\_ctrl\_data\_save\_sig\_ascii & .true. & (LOGICAL) & save time-series in ASCII format? \\ \hline
   \end{tabular}
            } % 这行是 resizebox 的结束
   \end{center}

         \begin{center}
   \resizebox{\textwidth}{!}{%
   \begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT VALUE & UNITS & DESCRIPTION \\ \hline
   \multicolumn{4}{|l|}{OCEAN BIOGEOCHEMISTRY: TRACER AUDITING AND DEBUGGING OPTIONS} \\ \hline
   bg\_ctrl\_audit & .true. & (LOGICAL) & audit tracer inventory? \\ \hline
   bg\_ctrl\_audit\_fatal & .false. & (LOGICAL) & halt on audit fail? \\ \hline
   bg\_par\_misc\_audit\_relerr & 1.0E-08 & n/a & threshold of relative inventory change to\\
    & & & trigger audit error \\ \hline
   bg\_ctrl\_debug\_reportwarnings & .false. & (LOGICAL) & report all run-time warnings? \\ \hline
   bg\_ctrl\_debug\_lvl1 & .false. & (LOGICAL) & report level \#1 debug? \\ \hline
   bg\_ctrl\_debug\_lvl2 & .false. & (LOGICAL) & report level \#2 debug? \\ \hline
   \end{tabular}
               } % 这行是 resizebox 的结束
   \end{center}

1 e.g., salinity-normalized ocean tracers, tracer inventories of each cell.
2 Saved at time-slice intervals.

         \begin{center}
   \resizebox{\textwidth}{!}{%
\begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT VALUE & UNITS & DESCRIPTION \\ \hline
   \multicolumn{4}{|l|}{DEEP-SEA SEDIMENTS: RUN CONTROL} \\ \hline
   sg\_ctrl\_continuing & .false. & (LOGICAL) & continuing sedgem? \\ \hline
   sg\_start\_year & 0.0 & & Simulation start year [REAL] \\ \hline
   sg\_par\_misc\_t\_runtime & 1000.0 & yr & Simulation run length \\ \hline
   \multicolumn{4}{|l|}{DEEP-SEA SEDIMENTS: PHYSICAL CONFIGURATION} \\ \hline
   sg\_par\_sed\_top\_th & 1.0 & cm & top ('well-mixed') sediment layer \\
    & & & thickness \\ \hline
   sg\_par\_sed\_poros\_det & 0.880 & cm3 cm-3 & detrital porosity \\ \hline
   sg\_par\_sed\_poros\_CaCO3 & 0.610 & cm3 cm-3 & carbonate porosity in top layer \\ \hline
   \multicolumn{4}{|l|}{DEEP-SEA SEDIMENTS: DIAGENESIS SCHEME: SELECTION} \\ \hline \\ \hline
   sg\_par\_sed\_diagen\_CaCO3opt & `archer1991explicit' & (STRING) & CaCO$_{3}$ diagenesis scheme \\ \hline
   sg\_par\_sed\_diagen\_opalopt & `none' & (STRING) & opal diagenesis scheme \\ \hline
   sg\_par\_sed\_diagen\_Corgopt 7 & `none' & (STRING) & organic matter diagenesis scheme \\ \hline
   \multicolumn{4}{|l|}{DEEP-SEA SEDIMENTS: DIAGENESIS SCHEME: CONTROl} \\ \hline
   sg\_ctrl\_sed\_bioturb & .true. & (LOGICAL) & bioturbate sediment stack? \\ \hline
   sg\_ctrl\_sed\_bioturb\_Archer & .true. & (LOGICAL) & use Archer et al. [2002] bioturbation \\
    & & & scheme? \\ \hline
   sg\_par\_n\_sed\_mix & 20 & n/a &maximum layer depth for bioturbation \\ \hline
   sg\_par\_sed\_mix\_k\_sur\_max & 0.15 & cm2 yr$^{-1}$ & maximum surface bioturbation mixing \\
   & & & rate \\ \hline
   sg\_par\_sed\_mix\_k\_sur\_min & 0.15 & cm2 yr$^{-1}$ & minimum surface bioturbation mixing \\
   & & & rate \\ \hline
   sg\_par\_sed\_fdet & 0.150 & g cm-2 kyr$^{-1}$ & prescribed (additional) flux of detrital\\
    & & & material to the seds \\ \hline
   sg\_par\_sed\_diagen\_fPOCfrac & 1.0 & n/a & fraction of POC rain available for driving \\
    & & & CaCO$_{3}$ dissolution \\ \hline
   \multicolumn{4}{|l|}{DEEP-SEA SEDIMENTS: DIAGENEIS SCHEME: ARCHER 1991} \\ \hline
   sg\_par\_sed\_archer1991\_dissc & 1.1574e-5 & -s & dissolution rate constant \\ \hline
   sg\_par\_sed\_archer1991\_dissn & 4.5 & n/a & dissolution rate order \\ \hline
   sg\_par\_sed\_archer1991\_rc & 2.E-9 & -s & organic degradation rate constant \\ \hline
   sg\_par\_sed\_archer1991\_iterationmax & 20 & & loop limit in 'o2org' subroutine \\ \hline
   \multicolumn{4}{|l|}{DEEP-SEA SEDIMENTS: MISC CONTROLS} \\ \hline
   sg\_par\_sed\_CaCO3precip\_sf & 0.0 & & CaCO$_{3}$ precipitation scale factor (abiotic) \\ \hline
   sg\_par\_sed\_CaCO3precip\_exp & 2.0 & & CaCO$_{3}$ precipitation rate law lower \\
   & & & (abiotic) \\ \hline
   sg\_par\_sed\_reef\_CaCO3precip\_sf & 0.0 & & CaCO$_{3}$ precipitation scale factor (corals) \\ \hline
   sg\_par\_sed\_reef\_CaCO3precip\_exp & 1.0 & & CaCO$_{3}$ precipitation rate law power\\
   & & &  (corals) \\ \hline
   sg\_par\_sed\_reef\_calcite & .true. & (LOGICAL) & CaCO$_{3}$ precipitation as calcite (otherwise \\
   & & & aragonite)? \\ \hline
   sg\_par\_sed\_CaCO3\_abioticohm\_min & 10.0 & & Min threshold for abiotic CaCO$_{3}$ \\
   & & & precipitation \\ \hline
   sg\_par\_sed\_CaCO3\_coralohm\_max & 10.0 & & Max threshold for coral CaCO$_{3}$ \\
   & & & precipitation \\ \hline
   sg\_par\_sed\_poros\_CaCO3\_reef & 0.5 & cm3 cm-3 & Reef CaCO$_{3}$ porosity \\ \hline
   \multicolumn{4}{|l|}{DEEP-SEA SEDIMENTS: DEEP-SEA SEDIMENTS: ISOTOPIC FRACTIONATION} \\ \hline
   sg\_opt\_sed\_foram\_b\_13C\_delta & NONE & (STRING) & Benthic foram $^{13}$C fractionation \\
   & & & scheme ID string \\ \hline
   \end{tabular}
                  } % 这行是 resizebox 的结束
   \end{center}

           \begin{center}
   \resizebox{\textwidth}{!}{%
   \begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT & UNITS & DESCRIPTION \\ 
   & VALUE & & \\ \hline
   \multicolumn{4}{|l|}{DEEP-SEA SEDIMENTS: DEEP-SEA SEDIMENTS: HYDROTHERMAL AND OCEAN CRUSTAL WEATHERING} \\ \hline
   sg\_par\_sed\_hydroip\_fLi & 0.0 & mol -yr & hydrothermal Li flux \\ \hline
   sg\_par\_sed\_hydroip\_fLi\_d7Li & 4.0 & \permil & hydrothermal Li flux d$^{7}$Li \\ \hline
   sg\_par\_sed\_lowTalt\_fLi\_alpha & 0.0 & mol -yr & Li low temperature alteration sink (Li/Ca normalized) \\ \hline
   sg\_par\_sed\_lowTalt\_7Li\_epsilon & -15.0 & \permil & Li low temperature alteration sink $^{7}$Li epsilon \\ \hline
   sg\_par\_sed\_clay\_fLi\_alpha & 0.0 & mol -yr & Li clay formation sink (Li/Ca normalized) \\ \hline
   sg\_par\_sed\_clay\_7Li\_epsilon & -15.0 & \permil & Li clay formation sink $^{7}$Li epsilon \\ \hline
   \multicolumn{4}{|l|}{DEEP-SEA SEDIMENTS: DEEP-SEA SEDIMENTS: MISC CONTROLS} \\ \hline
   sg\_ctrl\_sed\_forcedohmega\_ca & .true. & (LOGICAL) & Ca-only adjustment for forced ocean saturation? \\ \hline
   sg\_par\_sed\_ohmegamin & 0.00 & n/a & forced minimum saturation (calcite omega) anywhere \\ \hline
   sg\_par\_sed\_ohmegamin\_flux & 0.00 & mol Ca cm-2 & per time-step imposed sed->ocn flux for saturation \\ \hline
   \multicolumn{4}{|l|}{DEEP-SEA SEDIMENTS: DEEP-SEA SEDIMENTS: DATA FILENAMES} \\ \hline
   sg\_par\_sed\_topo\_D & `sedgem\_topo & (STRING) & sediment water depth grid name \\ 
   & \_D.36x36' & & \\ \hline
   sg\_par\_sedcore\_save\_mask\_name & `sedgem\_save & (STRING) & sediment core save mask name \\ 
   & \_mask.36x36' & & \\ \hline
   sg\_par\_sed\_mix\_k\_name & `'sedgem\_sed & (STRING) & biodiffusion profile name \\ 
   & \_mix\_k.dat' & & \\ \hline
   \multicolumn{4}{|l|}{DEEP-SEA SEDIMENTS: DEEP-SEA SEDIMENTS: I/O: MISC} \\ \hline
   sg\_ctrl\_data\_save\_ascii & .false. & (LOGICAL) & save 2-D data fields in ASCII format? \\ \hline
   sg\_ctrl\_data\_save\_wtfrac & .true. & (LOGICAL) & report sediment data as a mass fraction? \\ \hline
   sg\_ctrl\_misc\_debug1 & .false. & (LOGICAL) & debug level \#1? \\ \hline
   sg\_ctrl\_misc\_debug2 & .false. & (LOGICAL) & debug level \#2? \\ \hline
   sg\_ctrl\_misc\_debug3 & .false. & (LOGICAL) & debug level \#3? \\ \hline
   sg\_ctrl\_misc\_debug4 & .false. & (LOGICAL) & debug level \#4? \\ \hline
   sg\_ctrl\_misc\_report\_err & .false. & (LOGICAL) & report errors? \\ \hline
   sg\_par\_misc\_debug\_i & 1 & n/a & i sediment coordinate for debug reporting \\ \hline
   sg\_par\_misc\_debug\_j & 1 & n/a & j sediment coordinate for debug reporting \\ \hline
   \end{tabular}
                     } % 这行是 resizebox 的结束
   \end{center}

              \begin{center}
   \resizebox{\textwidth}{!}{%
\begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT & UNITS & DESCRIPTION \\ 
   & VALUE & & \\ \hline
   \multicolumn{4}{|l|}{TERRESTRIAL WEATHERING: RIVER ROUTING PARAMETERS} \\ \hline
   rg\_topo & 'worbe2.k1' & n/a & continental config and river routing \\
   & & & filename \\ \hline
   \multicolumn{4}{|l|}{TERRESTRIAL WEATHERING: WEATHERING SCHEME PARAMETER} \\ \hline
   rg\_par\_weathopt & `Global\_avg' & (STRING) & weathering option \\ \hline
   rg\_opt\_weather\_T\_Ca & .false. & (LOGICAL) & CaCO$_{3}$ weathering - temperature \\
   & & & feedback \\ \hline
   rg\_opt\_weather\_T\_Si & .false. & (LOGICAL) & CaSiO3 weathering - temperature \\
   & & & feedback \\ \hline
   rg\_opt\_weather\_R\_explicit & .true. & (LOGICAL) & if true then R/R\_0 is used rather than \\
   & & & the 1 + 0.045(T-T\_0) \\
   & & & parameterisation from GEOCARB \\ \hline
   rg\_opt\_weather\_R\_Ca & .false. & (LOGICAL) & CaCO$_{3}$ weathering - runoff feedback \\ \hline
   rg\_opt\_weather\_R\_Si & .false. & (LOGICAL) & CaSiO3 weathering - runoff feedback \\ \hline
   rg\_opt\_weather\_P\_explicit & .false. & (LOGICAL) & if true then P/P\_0 is used rather than \\
   & & & the [2RCO2/(1+RCO2)]\^0.4 \\
   & & & parameterisation from GEOCARB \\ \hline
   rg\_opt\_weather\_P\_Ca & .false. & (LOGICAL) & CaCO$_{3}$ weathering - productivity \\
   & & & feedback \\ \hline
   rg\_opt\_weather\_P\_Si & .false. & (LOGICAL) & CaSiO3 weathering - productivity \\
   & & & feedback \\ \hline
   rg\_par\_prodopt & `GPP' & (STRING) & prodictivity to use (`GPP' or `NPP') \\ \hline
   rg\_par\_weather\_T0 & 8.4777 & deg C & eathering reference mean global land \\
   & & & surface temperature \\ \hline
   rg\_par\_weather\_R0 & 5.619E-06 & mm -s & weathering reference mean global \\
   & & & runoff \\ \hline
   rg\_par\_weather\_P0 & 1.2585 & kg C m-2 yr$^{-1}$ & weathering reference mean global \\
   & & & land productivity \\ \hline
   rg\_par\_weather\_CO20 & 278 & ppm & weathering reference mean atmospheric \\
   & & & CO2 level \\ \hline
   rg\_par\_outgas\_CO2 & 0.0 & mol C yr$^{-1}$ & outgassing rate [5.00E12] \\ \hline
   rg\_par\_outgas\_CO2\_13C & -5.000 & \permil & mean volcanic/metamorphic d$^{13}$C \\ \hline
   \multicolumn{4}{|l|}{TERRESTRIAL WEATHERING: GLOBAL AVERAGE WEATHERING PARAMETERS} \\ \hline
   rg\_opt\_weather\_CaCO3 & .FALSE. & (LOGICAL) & CaCO$_{3}$\_weathering-temperature \\
   & & & feedback? \\ \hline
   rg\_opt\_weather\_CaSiO3 & .FALSE. & (LOGICAL) & CaSiO3\_weathering-temperature \\
   & & & feedback? \\ \hline
   rg\_opt\_weather\_P & .FALSE. & (LOGICAL) & productivity-weathering feedback \\ \hline
   rg\_par\_weather\_T0 & 8.451890 & C & weathering reference mean global land \\
   & & & surface temperature \\ \hline
   rg\_par\_weather\_P0 & 0.716 & kgC m-2 yr$^{-1}$ & weathering reference mean global \\
   & & & land productivity \\ \hline
   rg\_par\_outgas\_CO2 & 0.0 & mol C yr$^{-1}$ & CO2 outgassing rate \\ \hline
   rg\_par\_outgas\_CO2\_13C & -5.000 & \permil & mean volcanic/metamorphic d$^{13}$C \\ \hline
   rg\_par\_weather\_CaSiO3 & 0.0 & mol Ca2+ yr$^{-1}$ & global silicate weathering rate \\ \hline
   rg\_par\_weather\_CaCO3 & 10.00E+12 & mol Ca2+ yr$^{-1}$ & global carbonate weathering rate \\ \hline
   rg\_par\_weather\_CaCO3\_13C & 0.000 & \permil & mean carbonate d$^{13}$C \\ \hline
   rg\_par\_weather\_CaSiO3\_fracLi & 10.00E-6 & & global silicate Li abundance \\ \hline
   rg\_par\_weather\_CaSiO3\_Li\_d7Li & 4.000 & \permil & global silicate d$^{7}$Li \\ \hline
   rg\_par\_weather\_CaSiO3\_Li\_7Li\_epsilon & 15.000 & \permil & clay fractionation at normalized \\
   & & & weathering \\ \hline
   rg\_par\_weather\_CaSiO3\_Li\_7Li\_epsilon\_max & 1`5.000 & \permil & maximum clay fractionation \\ \hline
   \end{tabular}
                        } % 这行是 resizebox 的结束
   \end{center}

   
              \begin{center}
   \resizebox{\textwidth}{!}{%
   \begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT & UNITS & DESCRIPTION \\ 
   & VALUE & & \\ \hline
   \multicolumn{4}{|l|}{TERRESTRIAL WEATHERING: 2-D WEATHERING PARAMETERS} \\ \hline
   rg\_par\_lith\_data & GEM\_CO2 & (STRING) & name of lithological data set - \\
   & & & corresponding to directory genie-rokgem/\\
   & & & data/input/lithologies\_rg\_lith\_data\_\\
   & & & 036\_036 \\ \hline
   rg\_truncate\_to\_land & .true. & (LOGICAL) & truncate lithological maps to genie \\
   & & & land-mask -if option is set to false than \\
   & & & flux from land in genie ocean, goes \\
   & & & direct to ocean \\ \hline
   rg\_calibrate\_weath & .false. & (LOGICAL) & calibrate 2D weathering - if .true. \\
   & & & use values below \\ \hline
   rg\_calibrate\_weather\_GKWM\_CaCO3 & 1.583 & & calibratation value for 2D CaCO$_{3}$ \\
   & & & weathering for GKWM scheme -to \\
   & & & avoid drift, set equal to (half \\
   & & & of CaCO$_{3}$ sediment burrial flux)/\\
   & & & (original uncorrected flux) \\
   & & & (e.g. 1.583 for spun-up model)\\ \hline
   rg\_calibrate\_weather\_GEM\_CO2\_CaCO3 & 1.178 & & calibratation value for 2D CaCO$_{3}$ \\
   & & & weathering for GEM-CO2 scheme -\\
   & & & to avoid drift, set equal to \\
   & & & (half of CaCO$_{3}$ sediment burrial flux)/(\\
   & & & original uncorrected flux) \\
   & & & (e.g. 1.178 for spun-up model) \\ \hline
   rg\_calibrate\_weather\_GKWM\_CaSiO3 & 0.8548 & &c alibration value for 2D CaSiO3 \\
   & & & weathering for GKWM scheme - \\
   & & & to avoid drift, set equal to \\
   & & & (half of CaCO$_{3}$ sediment burrial flux)/\\
   & & & (original uncorrected flux) \\
   & & & (e.g. 0.8548 for spun-up model) \\ \hline
   rg\_calibrate\_weather\_GEM\_CO2\_CaSiO3 & 0.8878 & & calibration value for 2D CaSiO3 \\
   & & & weathering for GEM-CO2 scheme - \\
   & & & to avoid drift, set equal to \\
   & & & (half of CaCO$_{3}$ sediment burrial flux)/(\\
   & & & original uncorrected flux) \\
   & & & (e.g. 0.8878 for spun-up model)\\ \hline
   rg\_calibrate\_runoff & .false. & (LOGICAL) & calibrate runoff in 2D weathering \\
   & & & functions to values in papers \\ \hline
   \end{tabular}
                           } % 这行是 resizebox 的结束
   \end{center}

   
              \begin{center}
   \resizebox{\textwidth}{!}{%

   \begin{tabular}{ | l | l | l | l |}
   \hline
   NAME & DEFAULT VALUE & UNITS & DESCRIPTION \\ \hline
   \multicolumn{4}{|l|}{TERRESTRIAL WEATHERING: DATA FILENAMES} \\ \hline
   rg\_par\_output\_years\_file & `rokgem\_output\_years.dat' & (STRING) &  filename of file containing the times\\
    & & & (in years) at which output is to be generated \\ \hline
   \end{tabular}
                           } % 这行是 resizebox 的结束
   \end{center}

   



\end{document}



```

---

