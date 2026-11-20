# Formulation Science and Safety Logic for a Personalized Women's Supplement Engine (Vilo), as of Nov 2026

Sourcing notes for the report writer:
- Research date: 2026-11-20. Findings come from web searches run this session. Direct page fetches were blocked for most primary hosts (ods.od.nih.gov, tga.gov.au, obesity.org, contemporaryobgyn.net), and the shared web-search budget ran out partway through. So many figures come from search-result abstracts of the primary documents, not full-text reads.
- **[NV] = not live-verified this session.** These are standard reference values or guideline positions, cited to their canonical primary source (mostly NIH ODS fact sheets, NASEM DRI tables, USPSTF, EFSA) from prior knowledge, because the host could not be fetched. They are well-established values. Still, re-check every [NV] number against the source before encoding it in production rules.
- Claims with no [NV] tag were confirmed in this session's search results.
- Proposed engine rules appear under "Inferences". They are my synthesis, not sourced clinical guidance, and a clinical advisory board must ratify them.

---

## 1. Does personalized nutrition / personalized supplementation improve outcomes vs a standard approach or multivitamin?

### Takeaway
Personalized *dietary advice* beats generic advice by a modest margin in two credible RCTs (Food4Me; ZOE METHOD). But in Food4Me, adding phenotypic or genotypic data did not improve results over diet-based personalization alone. I found **no RCT showing that biomarker-guided personalized supplements beat a standard multivitamin on clinical outcomes**. The evidence-backed form of "personalization" is narrower: finding and correcting documented deficiencies (iron, vitamin D, B12, iodine/folate in pregnancy) with lab-guided doses, and avoiding harm (interactions, upper limits, pregnancy). Claims beyond that are not yet evidence-backed.

### Cited Findings
- **Food4Me (Celis-Morales et al., Int J Epidemiol 2017;46(2):578–588).** 6-month, 4-arm RCT in 7 European countries, 1,269 completers. Arms: conventional advice, or personalized advice based on (a) diet, (b) diet + phenotype, (c) diet + phenotype + genotype. The personalized arms cut red meat, salt and saturated fat and raised Healthy Eating Index scores vs control. **"No evidence that including phenotypic and phenotypic plus genotypic information enhanced the effectiveness of the PN advice."** — [PubMed 27524815](https://pubmed.ncbi.nlm.nih.gov/27524815/); [IJE](https://academic.oup.com/ije/article/46/2/578/2614369); [NutraIngredients coverage](https://www.nutraingredients.com/Article/2016/08/16/Strong-7-country-evidence-for-personalised-nutrition-but-not-phenotype-genotype-role)
- **ZOE METHOD (Bermingham et al., Nature Medicine, 8 May 2024).** 18-week RCT: n=177 got a personalized dietary program (app-based, driven by microbiome/glucose/TG data); n=170 controls got USDA Dietary Guidelines advice. The primary outcome (triglycerides) fell significantly more with personalization; LDL-C did not differ. Weight, waist, HbA1c, diet quality and microbiome diversity improved more, especially in adherent participants. — [PMC11271409](https://pmc.ncbi.nlm.nih.gov/articles/PMC11271409); [Nature Med PDF](https://www.nature.com/articles/s41591-024-02951-6.pdf)
- **ZOE METHOD critique.** An outside dietitian argued the trial "did not test whether their novel 'biologically-driven' personalized advice was better than generic healthy eating advice." The intervention arm also got far more app support and engagement than controls, which confounds the result. — [FoodNavigator](https://www.foodnavigator.com/Article/2024/05/10/Zoe-hails-personalized-nutrition-trial-success-results-come-under-scrutiny/)
- **PREDICT 1 (Berry et al., Nature Medicine 2020).** Found large between-person variation in postprandial glucose and TG responses to identical meals. Genetics explained only a minority of that variation. This is the scientific basis for diet personalization, but it concerns meal responses, not micronutrient needs. — [Nature Medicine 2020](https://www.nature.com/articles/s41591-020-0934-0) [NV]
- **No head-to-head RCT of personalized vs standard multivitamin was found.** The closest study is a 2025 *Life* (MDPI) retrospective, observational, pre-post analysis of a biomarker-guided program (targeted vitamin D, omega-3, B vitamins, etc.). It reported lower inflammatory markers, and its authors call for RCTs to confirm causality. — [MDPI Life 2025](https://www.mdpi.com/2075-1729/15/12/1887)
- **Supplements do move biomarkers, which is a surrogate outcome.** In a 12-week trial in healthy premenopausal women, a multivitamin + omega-3 raised serum micronutrients and RBC fatty acids vs placebo. — [PMC8313763](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8313763/). In healthy 55–65-year-olds, 16 weeks of multivitamin improved blood biomarkers **without improving cognitive function**. — [PMC4446780](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4446780/)
- **USPSTF 2022.** Evidence is insufficient (I statement) for multivitamins to prevent CVD or cancer. USPSTF recommends **against** beta-carotene and vitamin E supplements for that purpose. The statement does not apply to pregnant people or people with known deficiencies. — [USPSTF 2022](https://www.uspreventiveservicestaskforce.org/uspstf/recommendation/vitamin-supplementation-to-prevent-cvd-and-cancer-preventive-medication) [NV]
- **Industry precedent (Bioniq).** Bioniq says its algorithm uses blood data from >40,000 people (~4 million data points) and "updates itself" from historical results. These are company claims; no peer-reviewed outcome trial was found. — [AgFunderNews](https://agfundernews.com/meet-the-founder-nutrition-gets-personal-for-bioniqs-vadim-fedotov); [Endurance.biz](https://endurance.biz/2023/industry-news/bioniq-pro-offers-up-personalized-supplements-based-on-4m-data-points/)

### Inferences
- **Defensible claims for Vilo:** (1) lab-guided correction of documented insufficiency (e.g., ferritin-guided iron, B12 in metformin users); (2) life-stage-appropriate composition (preconception/prenatal folate, iodine, choline, DHA); (3) safety personalization: interaction screening, UL caps counting diet intake, pregnancy lockouts. **Not defensible:** "personalized formula outperforms a multivitamin," genotype-based (e.g., MTHFR) formulation, and cycle-phase or wearable-driven dosing (see sections 6–7).
- Food4Me's null result for added genotype/phenotype suggests that much of the benefit of "personalization" comes from engagement and feedback, not from the biological inputs. Vilo should evaluate its engine against an active comparator (a well-designed standard women's multi), not against placebo.
- Vilo could produce real evidence: a pragmatic RCT in which personalized formula + retesting is compared with a standard multi + retesting, with endpoints like proportion with ferritin ≥30 ng/mL at 6 months, 25(OH)D, symptom scores and adherence. As far as I found, no company in this category has published one.

### Gaps
- No published RCTs by Persona, Rootine, Baze, Bioniq, Nourished, Vitl, Thorne, InsideTracker or Function Health on clinical outcomes were found. This may reflect limited search reach rather than absence.
- A 400-adult Chinese 12-week RCT of personalized nutrition advice turned up in search, but I could not confirm the exact citation. The personalized advice included multivitamin use, so the supplement effect cannot be isolated.

---

## 2. Highest-evidence nutrient interventions for women, by biomarker and life stage

### Takeaway
The strongest, guideline-backed interventions are: **folic acid 400–800 mcg** for anyone who could become pregnant; **iron, guided by ferritin**, using the new 2026 ASH threshold of ≤30 ng/mL (≤50 in heavy menstrual bleeding); **iodine 150 mcg and choline in pregnancy/lactation**; **omega-3 (≥500 mg DHA) in pregnancy for preterm-birth reduction**; **B12 in metformin/PPI users and vegans**; **B6 for nausea in pregnancy**; and vitamin D at RDA-level doses (the Endocrine Society 2024 now advises against routine testing and against high-dose targets in healthy adults under 75). Evidence is moderate for magnesium and riboflavin in migraine, calcium and B6 for PMS, and creatine for lean mass in postmenopausal women. Evidence is weak or inconclusive for myo-inositol in PCOS, botanicals for menopause (black cohosh carries a liver-injury signal), K2, collagen, generic probiotics, MTHFR-driven methylfolate and magnesium for sleep.

### Cited Findings

**Iron (ferritin thresholds, dosing schedule, forms)**
- **ASH 2026 guideline (Blood Advances; evidence through July 2025).** For menstruating individuals, ASH suggests a ferritin threshold of **≤30 ng/mL** to diagnose iron deficiency, and suggests **against ≤15 ng/mL** (conditional recommendation, low-certainty evidence). The higher threshold may also suit people with symptoms or risk factors, imminent surgery, or plans to become pregnant. For heavy menstrual bleeding and pregnant patients with anemia, **≤50 ng/mL may be considered**. — [US Pharmacist, Aug 17 2026](https://www.uspharmacist.com/article/ash-guidelines-raise-ferritin-thresholds-for-iron-deficiency/); [News-Medical, Oct 2026](https://www.news-medical.net/news/20261009/New-iron-deficiency-guidelines-raise-key-blood-test-cutoffs.aspx)
- WHO still uses ferritin **<15 µg/L** for women, based on expert opinion; guidance is in transition. — [WHO 2020 ferritin guideline](https://www.who.int/publications/i/item/9789240000124) [NV]. A 2024 cost-effectiveness model favored <25 µg/L for US women. — [HCPLive](https://www.hcplive.com/view/universal-25-g-l-threshold-for-iron-deficiency-is-cost-effective-could-improve-management-in-us-women)
- **Alternate-day dosing.** Stoffel et al., *Lancet Haematology* 2017, ran two RCTs in iron-depleted women. Cumulative fractional absorption was **21.8% with alternate-day vs 16.3% with consecutive-day** dosing. Splitting into twice-daily doses gave no absorption gain over once daily. The authors conclude single doses on alternate days optimize absorption. — [ETH Research Collection](https://www.research-collection.ethz.ch/handle/20.500.11850/233029?show=full); [Consultant360](https://www.consultant360.com/story/iron-absorption-better-alternate-day-dosing)
- A 2019 crossover study in women *with iron-deficiency anemia* (100 and 200 mg doses) also favored alternate-day dosing because it sharply raises fractional absorption. — [Haematologica](https://haematologica.org/article/view/9379/68315)
- **Von Siebenthal/Stoffel, EClinicalMedicine 2023.** Double-blind RCT in 150 Swiss women with ferritin ≤30 µg/L, equal total doses. Ferritin ended the same (43.8 vs 44.8 µg/L, P=0.98), but **alternate-day dosing caused fewer GI side effects**. — [DOAJ/EClinicalMedicine](https://doaj.org/article/628bd28bfd6645a5820f45e50dda2c27)
- **Mechanism.** Oral doses of roughly ≥60 mg raise serum hepcidin for about 24 h, which lowers absorption of the next day's dose. — [Moretti et al., Blood 2015](https://doi.org/10.1182/blood-2015-05-642223) [NV]
- **Ferrous bisglycinate.** A 2023 *Nutrition Reviews* meta-analysis of 17 RCTs (comparators were mixed iron salts) found, in pregnancy, a hemoglobin SMD of **+0.54 g/dL** (95% CI 0.15–0.94) vs other salts and **GI adverse events IRR 0.36** (95% CI 0.17–0.76), i.e., about 64% fewer. The pooled trials were few and heterogeneous. — [PubMed 36728680](https://pubmed.ncbi.nlm.nih.gov/36728680/); [PMC10331582](https://pmc.ncbi.nlm.nih.gov/articles/PMC10331582)
- In pregnancy, 25 mg elemental iron as bisglycinate was **non-inferior** to 50 mg as ferrous sulfate and caused fewer GI complaints (small trial, about 40 per arm). — [PubMed 24152889](https://pubmed.ncbi.nlm.nih.gov/24152889/)
- RDA [NV]: 18 mg/day for women aged 19–50, 8 mg at 51+, **27 mg in pregnancy**. US UL is **45 mg/day elemental**, set on GI side effects. Hereditary hemochromatosis means a risk of iron overload from supplements. — [ODS Iron](https://ods.od.nih.gov/factsheets/Iron-HealthProfessional/) [NV]
- **EFSA 2024 set no UL for iron.** It set a **"safe level of intake" of 40 mg/day** for adults (no black stools at 20–25 mg/day supplemental on top of ~15 mg/day from diet). It explicitly does not apply to medically supervised treatment of iron-deficiency anemia. — [EFSA Journal 2024 / PubMed 38868106](https://pubmed.ncbi.nlm.nih.gov/38868106/); [EFSA plain-language summary](https://www.efsa.europa.eu/en/node/18677)

**Vitamin D**
- **Endocrine Society 2024 (JCEM 109(8):1907–1947).** Suggests **against routine 25(OH)D testing** in all populations studied, including pregnant people and adults with obesity. The panel **could not define thresholds** for adequacy or target levels and dropped the sufficiency/insufficiency/deficiency categories. For healthy adults under 75 it advises against doses above the DRI. It suggests empiric supplementation above the DRI for adults ≥75, pregnant people, adults with high-risk prediabetes, and children/adolescents. — [PubMed 38828931](https://pubmed.ncbi.nlm.nih.gov/38828931/); [Endocrine News](https://endocrinenews.endocrine.org/endocrine-society-guideline-recommends-healthy-adults-under-the-age-of-75-take-the-recommended-daily-allowance-of-vitamin-d)
- Testing is still appropriate for specific indications such as hypocalcemia, malabsorption, and increased losses or catabolism. — [AAFP 2026 summary](https://www.aafp.org/afp/2026/0300/practice-guidelines-vitamin-d-disease-prevention.html)
- The guideline is contested. Holick argues its reliance on RCTs omits potential benefits. — [BU Medicine](https://www.bumc.bu.edu/camed/2024/12/04/revisiting-vitamin-d-guidelines)
- **Dose-response.** In a large observational dataset, 25(OH)D rose about **12 nmol/L (~4.8 ng/mL) per 1,000 IU/day** at intakes of 0–1,000 IU/day. The gain flattened to about 1.1 nmol/L per 1,000 IU at 15,000–20,000 IU/day. BMI was the better predictor of response, and obese participants averaged 19.8 nmol/L lower 25(OH)D. — [PMC4220998](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4220998/)
- A small trial in BMI ≥35 concluded that obese people may need about **40% more vitamin D** to reach the same level. — [BMC Obesity 2015](https://link.springer.com/article/10.1186/s40608-015-0056-2) (attribution per search summary)
- RDA 600 IU (15 mcg) for ages 19–70; UL **4,000 IU (100 mcg)**. Toxicity (hypercalcemia) is generally associated with serum 25(OH)D >150 ng/mL (375 nmol/L). — [ODS Vitamin D](https://ods.od.nih.gov/factsheets/VitaminD-HealthProfessional/) [NV]
- D3 raises serum 25(OH)D more effectively than D2. — [Tripkovic et al., AJCN 2012 meta-analysis, PubMed 22552031](https://pubmed.ncbi.nlm.nih.gov/22552031/) [NV]

**Calcium and vitamin D for bone (peri/postmenopause)**
- **USPSTF 2018.** **D (recommends against)** daily ≤400 IU vitamin D + ≤1,000 mg calcium for primary fracture prevention in community-dwelling postmenopausal women; this low-dose combination raises kidney-stone incidence. **I (insufficient)** for higher doses and for premenopausal women. An update was listed as in progress. — [USPSTF](https://www.uspreventiveservicestaskforce.org/uspstf/recommendation/vitamin-d-calcium-or-combined-supplementation-for-the-primary-prevention-of-fractures-in-adults-preventive-medication); [AAFP 2018](https://www.aafp.org/pubs/afp/issues/2018/0815/od2.html)
- Calcium RDA [NV]: 1,000 mg (19–50), 1,200 mg (women 51+). UL 2,500 mg (19–50) and 2,000 mg (51+). Absorption is best at ≤500 mg per dose. — [ODS Calcium](https://ods.od.nih.gov/factsheets/Calcium-HealthProfessional/) [NV]

**Folate / folic acid vs methylfolate (MTHFR)**
- **USPSTF 2023 (Grade A).** All persons planning or capable of pregnancy should take a daily supplement with **0.4–0.8 mg (400–800 mcg) folic acid**. This does not cover people at high risk (e.g., a prior NTD-affected pregnancy), who need higher, clinician-directed doses. — [USPSTF 2023](https://www.uspreventiveservicestaskforce.org/uspstf/recommendation/folic-acid-for-the-prevention-of-neural-tube-defects-preventive-medication) [NV]
- **ACMG 2013** advises against MTHFR polymorphism genotyping (minimal clinical utility). **MTHFR status does not change the advice** that women of childbearing age take standard-dose folic acid. ACMG reaffirmed this in 2020 and reclassified it as a Clinical Practice Resource. — [PubMed 23288205](https://pubmed.ncbi.nlm.nih.gov/23288205/); [GeneReviews/NCBI](https://www.ncbi.nlm.nih.gov/books/NBK66131/); [Genet Med 2020 addendum](https://www.nature.com/articles/s41436-020-0843-0.pdf)
- Citing CDC, CHOP states that special folate forms are unnecessary even with MTHFR variants. — [CHOP](https://www.chop.edu/pediatric-health-chat/what-to-know-about-mthfr-testing)
- UL is **1,000 mcg/day of synthetic folic acid** (supplements + fortified foods; food folate excluded). It was set because high folic acid can mask the anemia of B12 deficiency while neurologic damage progresses. — [ODS Folate](https://ods.od.nih.gov/factsheets/Folate-HealthProfessional/) [NV]

**Vitamin B12**
- ADA Standards of Care 2025 (Section 9): consider periodic B12 measurement in metformin-treated people, especially with anemia or peripheral neuropathy (Grade B). — [PubMed 39651989](https://pubmed.ncbi.nlm.nih.gov/39651989/); same in [AAFP 2018](https://www.aafp.org/pubs/afp/issues/2018/0801/p187.html)
- B12 has no UL. Absorption from high oral doses relies on passive diffusion (~1%), which is why oral doses of 500–1,000 mcg can treat deficiency without intrinsic factor. Cyanocobalamin is the best-studied form, and other forms have not been shown superior. PPIs/H2 blockers and metformin reduce absorption, and vegans are at risk. — [ODS B12](https://ods.od.nih.gov/factsheets/VitaminB12-HealthProfessional/) [NV]

**Vitamin B6 (PMS, nausea of pregnancy)**
- **Nausea/vomiting of pregnancy.** ACOG Practice Bulletin 153 (2015; later updated) makes **B6 alone, or B6 + doxylamine, first-line**. AAFP gives B6 as **10–25 mg every 8 hours**; the combination reduces symptoms by about 70%. — [AAFP 2014](https://www.aafp.org/pubs/afp/issues/2014/0615/p965.html); [HealthDay on ACOG](https://www.healthday.com/healthpro-news/pregnancy/acog-best-evidence-for-rx-of-nausea-vomiting-in-pregnancy-702451.html)
- **PMS.** The Wyatt et al. BMJ 1999 meta-analysis (9 trials, 940 patients) found B6 better than placebo for premenstrual symptoms, with **no dose-response**; trial quality was poor. The search summary gave OR 2.12 (1.80–2.48); my recollection of the abstract is OR 2.32 for overall symptoms. Verify. — [PubMed 10334745](https://pubmed.ncbi.nlm.nih.gov/10334745/)
- A 2024 systematic review found that **B6, calcium and zinc consistently improved psychological PMS symptoms**. Evidence was insufficient for magnesium, vitamin D, B1, multivitamins and PMS diets. — [PMC11723155](https://pmc.ncbi.nlm.nih.gov/articles/PMC11723155/)
- **Mg + B6** (200 mg Mg + 50 mg B6; De Souza 2000, n=44 crossover) had a small synergistic effect on premenstrual anxiety symptoms. The authors note that MgO absorption is poor and that more than 1 month is needed. — [PubMed 10746516](https://pubmed.ncbi.nlm.nih.gov/10746516/)
- **Calcium for PMS.** Thys-Jacobs 1998 (AJOG; ~500 women) found that 1,200 mg/day calcium carbonate reduced symptom scores vs placebo (~48% vs ~30% reduction). — [PubMed 9731815](https://pubmed.ncbi.nlm.nih.gov/9731815/) [NV]

**Magnesium (migraine, PMS, sleep)**
- **Migraine.** AHS cites magnesium oxide **400–500 mg/day**. BASH 2019 lists 400 mg/day (range 200–600). In a pivotal trial, riboflavin **400 mg/day** gave ≥50% fewer monthly migraine days in 53% vs 15% on placebo, and NICE says riboflavin 400 mg may reduce migraine frequency. Combination products (Mg + riboflavin + CoQ10) have given mixed results. — [AHS](https://americanheadachesociety.org/news/incorporating-nutraceuticals-for-migraine-prevention); [Schoenen & Lisicki chapter](https://orbi.uliege.be/bitstream/2268/334523/1/Schoenen%20%26%20LisickiChap%2035%20C035_9780443247057.pdf); [Migraine Trust](https://migrainetrust.org/?p=628); [J Headache Pain combo trial](https://thejournalofheadacheandpain.biomedcentral.com/articles/10.1186/s10194-015-0516-6)
- The 2012 AAN/AHS guideline rated magnesium, riboflavin and feverfew as Level B ("probably effective") for episodic migraine prevention. Butterbur's earlier Level A rating was later retracted over hepatotoxicity concerns with PA-containing products. — [Holland et al., Neurology 2012, PubMed 22529203](https://pubmed.ncbi.nlm.nih.gov/22529203/) [NV]
- RDA [NV]: 310 mg (19–30), 320 mg (31+), 350–360 mg in pregnancy. The **UL of 350 mg applies to supplemental magnesium only** (diarrhea). — [ODS Magnesium](https://ods.od.nih.gov/factsheets/Magnesium-HealthProfessional/) [NV]
- Magnesium for sleep: evidence not retrieved (search budget exhausted). See Gaps.

**Omega-3 (EPA/DHA)**
- **Cochrane 2018 (Middleton et al., CD003402; 70 RCTs, 19,927 women).** Omega-3 LCPUFA reduced **preterm birth <37 wk (RR 0.89, 0.81–0.97)** and **early preterm <34 wk (RR 0.58, 0.44–0.77)**, both high-quality evidence. The authors' suggested optimum is **500–1,000 mg/day LC omega-3 with ≥500 mg DHA, starting ~12 weeks**. NNT is 68 for preterm and 55 for early preterm. — [Cochrane news](https://www.cochrane.org/news/new-research-finds-omega-3-fatty-acids-reduce-risk-premature-birth); [AAFP Cochrane for Clinicians](https://www.aafp.org/afp/2020/0101/p17.html)
- A 2026 ACOG-related prenatal resource from CRN, an industry trade group, says "new guidelines recommend high-dose supplementation to reduce the risk of preterm birth." This is unverified against a primary ACOG document. — [CRN/ACOG 2026 resource](https://crnusa.org/sites/default/files/pdfs/Prenatal-resource-ACOG-2026-(FINAL).pdf)
- FDA/ODS: up to 5 g/day EPA+DHA from supplements is not associated with safety concerns. — [ODS Omega-3](https://ods.od.nih.gov/factsheets/Omega3FattyAcids-HealthProfessional/) [NV]. The proposed omega-3 index target is **≥8%** of RBC fatty acids (cardioprotective; <4% high risk). — [Harris & von Schacky 2004, PubMed 15208005](https://pubmed.ncbi.nlm.nih.gov/15208005/) [NV]

**Iodine and choline (preconception, pregnancy, lactation)**
- ODS: iodine intake recommendation in pregnancy is **220 mcg**, and **some prenatal supplements contain no iodine**. Choline AI in pregnancy is **450 mg**, and prenatals often contain little or no choline. — [ODS Pregnancy fact sheet](https://ods.od.nih.gov/factsheets/Pregnancy-HealthProfessional/)
- The ATA (2017 thyroid-in-pregnancy guideline) recommends **150 mcg/day iodine as potassium iodide** during preconception, pregnancy and lactation. — [Alexander et al., Thyroid 2017](https://www.liebertpub.com/doi/10.1089/thy.2016.0457) [NV]. Iodine UL is 1,100 mcg (EFSA 600 µg). Excess iodine can trigger thyroid dysfunction in autoimmune thyroid disease. — [ODS Iodine](https://ods.od.nih.gov/factsheets/Iodine-HealthProfessional/) [NV]
- Choline AI [NV]: 425 mg for nonpregnant women, 550 mg in lactation. UL 3,500 mg (fishy body odor, hypotension). — [ODS Choline](https://ods.od.nih.gov/factsheets/Choline-HealthProfessional/) [NV]

**Prenatal vitamin A**
- The UL for **preformed** vitamin A in pregnancy (≥19 y) is **3,000 mcg RAE** (2,800 for ages 14–18). It applies only to retinol/retinyl esters, not beta-carotene. Some studies suggest birth-defect risk rises at ≥10,000 IU/day preformed vitamin A, others only above 25,000 IU. MotherToBaby advises avoiding >10,000 IU/day; its March 2026 version cites >20,000 IU. — [MotherToBaby](https://mothertobaby.org/fact-sheets/vitamin-a/)
- The UK Committee on Toxicity derived 3,000 µg RE/day for women of childbearing age (NOAEL 4,500 µg RE/day ÷ UF 1.5). — [UK COT statement](https://cot.food.gov.uk/sites/default/files/2022-12/Statement%20on%20the%20effects%20of%20excess%20Vitamin%20A%20on%20maternal%20health%20Acc%20V.pdf); [gov.uk](https://www.gov.uk/government/publications/vitamin-a/statement-on-the-effects-of-excess-vitamin-a-on-maternal-health)

**Myo-inositol for PCOS**
- The systematic review behind the 2023 International PCOS Guideline (Tay et al., JCEM; 30 trials, n=2,230) found that MI or DCI *may* improve waist-hip ratio and hirsutism, with **likely no difference in reproductive outcomes**. MI causes fewer GI adverse events than metformin. The review calls the overall evidence **"limited and inconclusive."** — [PMC11099481](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11099481/); [2023 guideline (Hum Reprod, dead156)](https://pure.eur.nl/ws/portalfiles/portal/102751380/dead156.pdf)

**Creatine**
- A 2026 systematic review/meta-analysis in postmenopausal women found **≥5 g/day creatine monohydrate with resistance training** gives small but meaningful gains in lean mass and strength without evidence of harm. **Effects on bone density remain unclear.** — [PubMed 42141930](https://pubmed.ncbi.nlm.nih.gov/42141930/)
- The 2025 Smith-Ryan et al. narrative review (menstruation → pregnancy → menopause) reports strength and body-composition benefits mainly with resistance training and preliminary mood/cognition data. A cited 2-year RCT (237 postmenopausal women) improved bone geometry. — [PMC12086928](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12086928/); [NutraIngredients](https://www.nutraingredients.com/Article/2025/05/30/expert-review-recaps-effects-of-creatine-in-women/)
- A 2021 lifespan review found no adverse GI, renal, hepatic or cardiovascular effects in women. — [PMC7998865](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7998865/)

**Perimenopause/menopause botanicals**
- The Menopause Society (NAMS) 2023 Nonhormone Therapy Position Statement lists supplements and herbal remedies among therapies **not recommended** for vasomotor symptoms. — [Healio](https://www.healio.com/news/womens-health-ob-gyn/20230607/nams-releases-recommendations-to-treat-menopause-symptoms-with-nonhormone-therapies); [Statement PDF](https://depts.washington.edu/mbwc/content/page-files/NAMS_2023-nonhormone-therapy-position-statement_(1)22.pdf). The Australasian Menopause Society is somewhat more permissive about isopropanolic black cohosh extracts but flags safety concerns. — [AMS fact sheet](https://menopause.org.au/images/factsheets/AMS_Complementary_Therapies_Fact_Sheet.pdf)
- **Black cohosh liver safety.** NIH LiverTox (updated April 2025) rates products sold as black cohosh as a **"well established cause of clinically apparent liver injury."** The injury appears idiosyncratic, and contamination or misidentification may contribute. — [LiverTox NBK547990](https://www.ncbi.nlm.nih.gov/books/NBK547990/)
- USP reviewed 30 liver-damage reports (all "possible" causality) and required the caution "In rare cases black cohosh has been reported to affect the liver." There is a case of fulminant hepatic failure requiring transplant, and the American Botanical Council disputed the warning. — [NutraIngredients on USP](https://nutraingredients.com/Article/2007/06/27/usp-calls-for-caution-on-black-cohosh-and-green-tea-extracts); [PMC4100270](https://pmc.ncbi.nlm.nih.gov/articles/PMC4100270); [ABC objection](https://newhope.com/industry-insights/black-cohosh-does-not-require-label-caution-says-american-botanical-council)

**GLP-1 receptor agonist users (a growing women's segment)**
- The May 30, 2025 joint advisory (ACLM, ASN, Obesity Medicine Association, The Obesity Society) sets 8 priorities, including **prevention of micronutrient deficiencies** and **adequate protein intake with strength training** to preserve lean mass, with baseline assessment of muscle strength and body composition. — [PubMed 40450457](https://pubmed.ncbi.nlm.nih.gov/40450457/); [News-Medical](https://www.news-medical.net/news/20250531/Leading-health-organizations-release-guidance-on-nutrition-support-for-GLP-1-obesity-therapies.aspx); [Obesity Society](https://obesity.org/nutritional-priorities-to-support-glp-1-therapy-for-obesity)

### Inferences
Proposed core decision rules. These synthesize the evidence above; they are not guideline text and must be ratified clinically.
- **Iron**
  - Ferritin ≤30 ng/mL (≤50 with heavy menstrual bleeding or pregnancy planning) and Hb normal → iron 60–65 mg elemental (bisglycinate or sulfate) **on alternate days, as a single morning dose**, then retest ferritin in about 8–12 weeks.
  - Ferritin 30–50 → maintenance dose of 18 mg/day or none.
  - Ferritin >100–150, or TSAT >45%, or known HFE hemochromatosis → **no iron**.
  - No ferritin result → cap at RDA (18 mg) only if menstruating; otherwise 0. Postmenopausal default is 0–8 mg.
  - Total iron above 45 mg/day, as therapy not prevention, should come with clinician oversight and an anemia work-up referral when Hb is low.
- **Vitamin D**
  - Default 600–1,000 IU D3. Avoid encoding a "target 25(OH)D" goal as if guideline-endorsed; the Endocrine Society 2024 explicitly declined thresholds.
  - If a lab result exists, a pragmatic rule is to raise to 1,000–2,000 IU when 25(OH)D is <20 ng/mL and to 2,000 IU when obese. Never exceed a total of 4,000 IU/day without clinician involvement.
  - Retest no sooner than about 3 months.
- **Folate**: 400 mcg folic acid for every user who could become pregnant (800 mcg allowed). Methylfolate can be an *option* but must not replace folic acid in the preconception rule set. Do not use MTHFR genotype as an input.
- **B12**: add 250–1,000 mcg if metformin, PPI >1 yr, vegan/vegetarian, or age >50. Serum B12 <200 pg/mL with neurologic symptoms → physician (may need intramuscular B12).
- **Pregnancy/preconception module**: folic acid 400–800 mcg; iodine 150 mcg (KI); choline toward 450 mg total, accounting for diet; DHA ≥200 mg, or 500–1,000 mg LC n-3 per the Cochrane optimum; iron 27 mg; D 600–2,000 IU; vitamin A only as beta-carotene or ≤750 mcg RAE retinol. Hard exclusions: botanicals, high-dose B6 (except nausea doses per clinician), retinol >3,000 mcg total.
- **PMS module**: calcium 500–1,200 mg/day total (diet + supplement), B6 ≤50 mg/day (see UL/TGA section), magnesium 200–360 mg supplemental. All daily, not phase-timed. Do not claim treatment of PMDD; refer.
- **Migraine module** (user-reported diagnosis): magnesium 400 mg + riboflavin 400 mg, with the expectation of a 3-month trial. Note that riboflavin colors urine bright yellow.
- **Menopause module**: calcium to reach 1,200 mg total (diet first), D 800–1,000 IU, creatine 3–5 g (powder) if resistance training, protein reminders. **Exclude black cohosh by default**, or gate it behind liver-function confirmation, clinician review and explicit warnings.
- **PCOS module**: myo-inositol (commonly 2–4 g/day; sachet format) only with "limited evidence" framing.

### Gaps
- Magnesium for sleep: no current meta-analysis was retrieved (search budget exhausted). My recollection is that the evidence is low quality, from small trials mostly in older adults. Verify before any sleep claim.
- Probiotics, collagen and vitamin K2: not searched because the budget ran out. My understanding [NV]: AGA 2020 guidelines recommend probiotics only within clinical trials for most GI indications ([AGA 2020](https://www.gastrojournal.org/article/S0016-5085(20)34729-6/fulltext)); collagen-for-skin meta-analyses show small effects and are heavily industry-funded; K2 (MK-7) bone data are mixed. All three should be treated as low-evidence add-ons.
- The exact wording and strength of the 2023 PCOS guideline's inositol recommendation was not retrieved (the reviewing meta-analysis was).
- Black cohosh wording in the NAMS 2023 statement was not retrieved verbatim.
- The ACOG primary text on DHA and choline doses was not retrieved. The 2026 claim of an ACOG high-dose omega-3 recommendation is unverified and comes from an industry-produced document.
- Specific GLP-1 advisory protein targets (g/kg) and its list of micronutrients were not retrieved.
- Zinc: only the PMS signal was retrieved. Women's RDA is 8 mg, UL 40 mg [NV].

---

## 3. Upper limits, toxicity, and accounting for diet + supplement intake

### Takeaway
The engine must enforce ULs on **total intake (diet + Vilo + other supplements)** for most nutrients. A few ULs apply only to supplemental or synthetic sources: magnesium, folic acid, niacin, vitamin E, and preformed vitamin A. Several EU limits are far stricter than US limits: **B6 12 mg (EFSA) vs 100 mg (US)**, zinc 25 vs 40 mg, magnesium 250 vs 350 mg supplemental, iodine 600 vs 1,100 mcg, vitamin E 300 vs 1,000 mg, and iron with a 40 mg safe level. B6 neuropathy is the most active regulatory safety issue (Australia's TGA final decision of Nov 2025). Retinol in pregnancy and iron overload are the main hard stops.

### Cited Findings
- **B6, Australia (TGA).** In the final decision of **25 Nov 2025**, products above **50 mg/day** (maximum recommended daily dose) become **pharmacist-only** or require a prescription from **1 June 2027**. ≤50 mg stays general sale, and the 50 mg cut-off matches the NHMRC adult UL. At least 125 products on the market contained >50 to ≤200 mg. There were **250 peripheral neuropathy reports linked to B6 products between Jan 2023 and Oct 2025**. The NHMRC is reviewing the B6 UL, due early 2027; further label changes are possible; and a safety alert was issued in Feb 2026. — [NutraIngredients](https://www.nutraingredients.com/Article/2025/11/25/vitamin-b6-supplements-face-new-regulation-in-australia); [TGA safety update](https://www.tga.gov.au/news/safety-updates/medicines-containing-vitamin-b6-pyridoxine-pyridoxal-or-pyridoxamine) (search summary; page fetch blocked); [Australian Pharmacist](https://www.australianpharmacist.com.au/?p=30976). Medical Republic notes >200 mg remains prescription-only. — [Medical Republic](https://www.medicalrepublic.com.au/tga-makes-final-decision-on-vitamin-b6-regulation/121769)
- **B6, EU (EFSA 2023).** UL **12 mg/day** for adults, *including pregnant and lactating women*, based on peripheral neuropathy. EU populations are unlikely to exceed it except regular users of high-dose B6 supplements. — [PMC10189633](https://pmc.ncbi.nlm.nih.gov/articles/PMC10189633); [Ulster portal](https://pure.ulster.ac.uk/en/publications/scientific-opinion-on-the-tolerable-upper-intake-level-for-vitami/)
- **Iron, EU (EFSA 2024).** No UL; **safe level 40 mg/day** for adults; not applicable to supervised anemia treatment. — [PubMed 38868106](https://pubmed.ncbi.nlm.nih.gov/38868106/)
- **Preformed vitamin A in pregnancy.** UL 3,000 mcg RAE; avoid >10,000 IU/day preformed; beta-carotene is not teratogenic. — [MotherToBaby](https://mothertobaby.org/fact-sheets/vitamin-a/); [UK COT](https://cot.food.gov.uk/sites/default/files/2022-12/Statement%20on%20the%20effects%20of%20excess%20Vitamin%20A%20on%20maternal%20health%20Acc%20V.pdf)
- **Vitamin D.** UL 4,000 IU; toxicity at 25(OH)D >150 ng/mL [NV]. The Endocrine Society advises against above-DRI doses in healthy adults <75. — [ODS Vitamin D](https://ods.od.nih.gov/factsheets/VitaminD-HealthProfessional/) [NV]; [PubMed 38828931](https://pubmed.ncbi.nlm.nih.gov/38828931/)
- **Calcium + D.** Low-dose combined supplementation raises kidney-stone incidence (USPSTF). — [USPSTF](https://www.uspreventiveservicestaskforce.org/uspstf/recommendation/vitamin-d-calcium-or-combined-supplementation-for-the-primary-prevention-of-fractures-in-adults-preventive-medication)
- **Botanical hepatotoxicity.** USP cautions on both black cohosh and **green tea extract**. — [NutraIngredients on USP](https://nutraingredients.com/Article/2007/06/27/usp-calls-for-caution-on-black-cohosh-and-green-tea-extracts); [LiverTox](https://www.ncbi.nlm.nih.gov/books/NBK547990/)

**UL reference table (adult women 19+, including pregnancy unless noted).** US values are from the NASEM DRI summary tables and ODS fact sheets ([NASEM DRI tables, NCBI NBK545442](https://www.ncbi.nlm.nih.gov/books/NBK545442/); ODS fact sheets). EFSA values are from the [EFSA UL summary](https://www.efsa.europa.eu/sites/default/files/assets/UL_Summary_tables.pdf) and 2023–2024 opinions. **All [NV] unless marked ✓ (verified this session).**

| Nutrient | US UL | US UL applies to | EFSA (adults) | Engine note |
|---|---|---|---|---|
| Vitamin A (preformed) | 3,000 mcg RAE (10,000 IU) ✓ | retinol/esters only ✓ | 3,000 µg RE ✓ | Pregnancy hard cap; prefer beta-carotene for reproductive-age women |
| Beta-carotene | none | — | none | USPSTF recommends against supplements (smokers: lung cancer) |
| Vitamin D | 100 mcg (4,000 IU) | total | 100 µg | ES 2024: RDA-level for healthy adults <75 ✓ |
| Vitamin E | 1,000 mg α-tocopherol | supplemental | 300 mg | Bleeding with anticoagulants |
| Vitamin C | 2,000 mg | total | not set | GI upset; kidney stones |
| Niacin | 35 mg | supplemental/fortified | nicotinic acid 10 mg; nicotinamide 900 mg | Use niacinamide |
| Vitamin B6 | 100 mg | total | **12 mg ✓** | AUS: >50 mg pharmacist-only from Jun 2027 ✓ |
| Folate | 1,000 mcg | synthetic folic acid | 1,000 µg | Masks B12 deficiency |
| Choline | 3,500 mg | total | not set | Bulk limits dose before toxicity |
| Calcium | 2,500 mg (19–50); 2,000 mg (51+) | total | 2,500 mg | Kidney stones ✓ |
| Iron | 45 mg | total | **safe level 40 mg ✓** | Hemochromatosis lockout |
| Zinc | 40 mg | total | 25 mg | Copper deficiency with chronic excess |
| Magnesium | 350 mg | **supplemental only** | 250 mg supplemental | Diarrhea; caution in CKD |
| Iodine | 1,100 mcg | total | 600 µg | Thyroid disease caution |
| Selenium | 400 mcg | total | 255 µg (2023) | Narrow margin |
| Copper | 10 mg | total | 5 mg | Pair with zinc |
| Manganese | 11 mg | total | safe level 8 mg (2023) | Usually omit |
| Molybdenum | 2 mg | total | 0.6 mg | — |
| Boron | 20 mg | total | 10 mg | — |
| B12, thiamin, riboflavin, biotin, pantothenate, vitamin K, chromium | none set | — | none | Biotin: lab interference (section 4) |

### Inferences
- **Intake accounting algorithm:**
  1. Estimate dietary intake per nutrient (FFQ or food log). For nutrients with total-intake ULs, use a conservative high estimate, e.g., the user's estimate plus a margin, or the NHANES 90th percentile for her demographic if no diet data.
  2. Add all declared non-Vilo supplements (parse their labels; the ODS Dietary Supplement Label Database is a usable reference).
  3. Add fortified-food folic acid and niacin.
  4. Vilo dose ≤ UL − (diet + other supplements), with a safety buffer: target ≤80% of UL for total-intake nutrients.
  5. For supplement-only ULs (Mg, folic acid, niacin, vitamin E, preformed A), count only supplements and fortificants.
- **Global market setting**: if Vilo ever ships to the EU/UK or Australia, use the stricter jurisdiction's limits. For B6, even in the US, a **default cap of ≤25 mg/day (and ≤50 mg/day in a PMS module, time-limited)** is defensible given TGA neuropathy reports and EFSA's 12 mg UL, though the US UL is 100 mg.
- **Hard lockouts:**
  - Pregnancy or trying to conceive → retinol >3,000 mcg total, botanicals, and high-dose B6 (outside nausea doses) blocked.
  - Hemochromatosis or high ferritin/TSAT → iron blocked.
  - Anticoagulant use → vitamin K changes and high-dose fish oil/vitamin E blocked.
  - Isotretinoin → vitamin A blocked.
  - Under-18s → excluded, or a separate UL set (ages 14–18 have lower ULs, e.g., vitamin A 2,800 mcg, folate 800 mcg, zinc 34 mg, B6 80 mg [NV]).

### Gaps
- Precise current TGA label-warning thresholds below 50 mg (Australia has had B6 neuropathy warning statements on lower-dose products) were not verified because the TGA page was blocked.
- The 2023–2024 EFSA values for selenium, manganese, vitamin E, vitamin A/beta-carotene, folic acid and vitamin D were not individually verified this session.
- No source was found on the minimum B6 dose associated with neuropathy case reports (some reports involve <50 mg/day; unverified).

---

## 4. Drug–nutrient interactions and depletions the engine must encode

### Takeaway
The highest-priority interaction rules for a women's product are:
1. **Levothyroxine**: separate calcium, iron and magnesium by about 4 h.
2. **Biotin**: interferes with thyroid and troponin immunoassays.
3. **Warfarin**: vitamin K consistency, plus St John's wort, vitamin E and fish oil.
4. **SSRIs and hormonal contraceptives**: St John's wort is excluded.
5. **Metformin and PPIs**: B12; PPIs also magnesium.
6. **Isotretinoin**: no vitamin A.
7. **GLP-1 RAs**: micronutrient adequacy and protein.

Contraceptive "depletion" claims are only partly supported: B6 most consistently, plus zinc/copper shifts. Evidence for folate depletion with modern low-dose pills is weak.

### Cited Findings
- **Hormonal contraceptives.** Palmery et al. 2013 (review) list folate, B2, B6, B12, C, E, Mg, Se and Zn as possibly depleted. — [PubMed 23852908](https://pubmed.ncbi.nlm.nih.gov/23852908/). A *Nutrition Reviews* 2011 analysis found **data do not support that current OCs negatively affect folate status**, while low-dose OCs **may lower B6 status**; serum B12 falls but **functional B12 indicators are not significantly affected**. — [PubMed 21967158](https://pubmed.ncbi.nlm.nih.gov/21967158/). Zinc tends to fall and copper to rise with OC use. — per the search summary of the same literature (e.g., [PubMed 35856377](https://pubmed.ncbi.nlm.nih.gov/35856377/))
- **Levothyroxine.** Patient.info, Drugs.com and GoodRx advise separating iron, calcium and mineral-containing multivitamins by about **4 hours** (bind in the gut). PeaceHealth rates the evidence as preliminary/weak but keeps the 4-h advice. Practical pattern: levothyroxine first thing on an empty stomach, minerals later. — [Patient.info](https://patient.info/medication-interactions/iron-and-levothyroxine-interaction); [Drugs.com](https://drugs.com/medical-answers/take-other-medications-levothyroxine-3562434); [PeaceHealth](https://www.peacehealth.org/medical-topics/id/hn-10000162)
- **Biotin assay interference.** FDA (2017, updated Nov 2019): biotin can cause **undetected incorrect lab results**, including falsely low troponin; one death has been linked. FDA listed 17 troponin assays still affected. Thyroid assays are affected too (falsely low TSH and falsely high T4/T3 pattern, which can mimic Graves'). Per lab bulletins, standard multivitamin biotin levels (30–60 µg) pose no interference risk. — [FDA](https://www.fda.gov/medical-devices/in-vitro-diagnostics/biotin-interference-troponin-lab-tests-assays-subject-biotin-interference); [U Utah pharmacy alert](https://pharmacyservices.utah.edu/alerts/2019/biotin.php); [U Iowa lab bulletin](https://www.healthcare.uiowa.edu/path_handbook/lab_bulletins/archived/2017/BiotinInterference-LabTests.html)
- **Warfarin.**
  - St John's wort reduces INR via enzyme induction.
  - Vitamin K in supplements and multis reduces warfarin effect, so intake must be kept consistent.
  - Vitamin E >400 IU/day raised INR in a case with rechallenge, though one trial showed no interaction.
  - Fish oil: case reports of elevated INR, but a clinical study found no anticoagulation effect; the bleeding concern remains.
  - Monitor INR whenever a supplement starts or stops; effects can appear 3–4 days later.
  — [UCSD Anticoagulation](https://health.ucsd.edu/for-health-care-professionals/anticoagulation-guidelines/warfarin/supplement-interactions); [AAFP 2008](https://www.aafp.org/pubs/afp/issues/2008/0101/p73.html)
- **St John's wort** can reduce the effectiveness of hormonal contraceptives and causes serotonin syndrome risk with SSRIs/SNRIs. — [NCCIH](https://www.nccih.nih.gov/health/st-johns-wort) [NV]
- **Metformin → B12.** ADA Grade B: periodic B12 assessment. — [PubMed 39651989](https://pubmed.ncbi.nlm.nih.gov/39651989/)
- **PPIs.** FDA 2011: hypomagnesemia with long-term use (usually >1 year). PPIs also reduce B12 absorption and non-heme iron and calcium carbonate absorption. — [FDA Drug Safety Communication 2011](https://www.fda.gov/drugs/drug-safety-and-availability/fda-drug-safety-communication-low-magnesium-levels-can-be-associated-long-term-use-proton-pump-inhibitor-drugs) [NV]; [ODS Magnesium](https://ods.od.nih.gov/factsheets/Magnesium-HealthProfessional/) [NV]
- **Statins → CoQ10.** Trials of CoQ10 for statin-associated muscle symptoms are mixed. — [NCCIH CoQ10](https://www.nccih.nih.gov/health/coenzyme-q10) [NV]
- **GLP-1 RAs.** Prioritize preventing micronutrient deficiencies and getting adequate protein with resistance training (joint advisory 2025). — [PubMed 40450457](https://pubmed.ncbi.nlm.nih.gov/40450457/)
- **Isotretinoin.** Avoid vitamin A supplements (additive toxicity); the drug is itself a potent teratogen. — [MedlinePlus isotretinoin](https://medlineplus.gov/druginfo/meds/a681043.html) [NV]
- **Bisphosphonates; tetracycline and fluoroquinolone antibiotics.** Calcium, magnesium, iron and zinc chelate or reduce absorption, so doses must be separated. — [ODS Magnesium](https://ods.od.nih.gov/factsheets/Magnesium-HealthProfessional/) [NV]; [ODS Calcium](https://ods.od.nih.gov/factsheets/Calcium-HealthProfessional/) [NV]

### Inferences
Proposed interaction rule table for the engine:

| User input | Rule |
|---|---|
| Levothyroxine / liothyronine | All Ca/Fe/Mg/Zn-containing units go in a PM pack, ≥4 h after the dose. No kelp/high iodine. Biotin ≤30–100 µg. Tell the user to pause biotin-containing products ~2–3 days before thyroid labs (verify the window). |
| Any upcoming blood test (Vilo's own) | Keep biotin at ≤ multivitamin levels so Vilo's own panels aren't confounded. Never sell high-dose "hair" biotin (5–10 mg). |
| Warfarin | Fixed, low vitamin K (or zero, with a note to keep consistent). No SJW, ginkgo, dong quai or high-dose curcumin. Vitamin E ≤ RDA. Fish oil only with clinician sign-off. Pharmacist review required. |
| DOACs / antiplatelets | Caution flag for fish oil >1 g, vitamin E, ginkgo, curcumin (additive bleeding risk; inference). |
| SSRIs/SNRIs/triptans/MAOIs | Exclude SJW, 5-HTP, tryptophan, SAMe. |
| Hormonal contraception | Exclude SJW. Optional B6 at RDA–10 mg. Folic acid 400 mcg is already default (pregnancy readiness). Do not market "pill depletion repair" beyond the evidence. |
| Metformin | Add B12 250–1,000 mcg and prompt B12/MMA testing. |
| PPI >1 yr | Add B12. Use calcium citrate, not carbonate. Prompt magnesium check. Iron absorption may be blunted. |
| GLP-1 RA | Multi at RDA level, protein reminders (1.2–1.6 g/kg is commonly cited; unverified, see Gaps), fiber/hydration prompts, iron/B12/D attention. Monitor for very low intake. |
| Isotretinoin / acitretin | No vitamin A beyond beta-carotene. Pregnancy-prevention context. |
| Spironolactone / ACEi / ARB (common in PCOS and acne care) | No potassium supplementation (inference; standard hyperkalemia caution). |
| Antiepileptics (valproate, carbamazepine, phenytoin, lamotrigine) | Clinician-directed folic acid (often higher). Vitamin D attention. Refer for preconception counseling. |
| Bisphosphonates; quinolone/tetracycline antibiotics | Mineral-pack spacing (2 h before / 4–6 h after for antibiotics; bisphosphonate first, minerals ≥30–60 min later). [NV] |
| Lithium, immunosuppressants, chemotherapy, transplant | Route to pharmacist/physician; no botanicals. |

### Gaps
- The Lexicomp/Natural Medicines interaction databases are paywalled and were not accessed. A commercial interaction database license is likely needed for production.
- Exact biotin washout guidance was not retrieved. Commonly cited windows are 8 h for standard doses and ≥48–72 h (or longer) for high doses.
- The GLP-1 advisory's specific protein g/kg and micronutrient list were not retrieved; the 1.2–1.6 g/kg figure above is unverified.

---

## 5. Nutrient–nutrient interactions, timing and AM/PM pack logic

### Takeaway
Iron has the most timing-sensitive logic: single dose, alternate days, away from calcium, coffee/tea and possibly zinc, with or without vitamin C. Calcium should be split into doses of ≤500 mg. Fat-soluble vitamins and omega-3 go with meals. Zinc needs copper balancing at higher doses. Folic acid can mask B12 deficiency. A two-pack (AM/PM) design is sufficient to separate the main antagonists and to accommodate levothyroxine users.

### Cited Findings
- Iron: alternate-day single doses maximize fractional absorption; twice-daily splitting gives no benefit. — [Stoffel 2017 via ETH](https://www.research-collection.ethz.ch/handle/20.500.11850/233029?show=full). Hepcidin rises for ~24 h after doses of roughly ≥60 mg. — [Moretti 2015](https://doi.org/10.1182/blood-2015-05-642223) [NV]
- Calcium inhibits non-heme and heme iron absorption, and vitamin C enhances non-heme iron absorption. — [ODS Iron](https://ods.od.nih.gov/factsheets/Iron-HealthProfessional/) [NV]
- Calcium absorption is highest at doses ≤500 mg. — [ODS Calcium](https://ods.od.nih.gov/factsheets/Calcium-HealthProfessional/) [NV]
- Chronic high zinc intake induces copper deficiency. — [ODS Zinc](https://ods.od.nih.gov/factsheets/Zinc-HealthProfessional/) [NV]
- Folic acid >1,000 mcg can mask B12-deficiency anemia. — [ODS Folate](https://ods.od.nih.gov/factsheets/Folate-HealthProfessional/) [NV]
- MgO absorption is poor, and Mg repletion needs more than 1 month. — [De Souza 2000](https://pubmed.ncbi.nlm.nih.gov/10746516/)
- Levothyroxine needs mineral spacing (~4 h). — [Patient.info](https://patient.info/medication-interactions/iron-and-levothyroxine-interaction)

### Inferences
- **Proposed pack architecture:**
  - **AM pack** (with breakfast, not with coffee/tea or dairy): B-complex (low B6), folate, B12, iodine, vitamin D3 (+K if used; take with a fat-containing meal), vitamin C, omega-3 softgel (or move to dinner for reflux).
  - **Iron**: on alternate days (Mon/Wed/Fri/Sun), as a separate unit in the AM pack. That needs an alternating-day pack SKU or a clearly marked iron capsule.
  - **PM pack** (with dinner): calcium (≤500 mg per dose), magnesium, zinc + copper. Creatine or collagen powders can be taken at any time.
  - **Levothyroxine users**: shift the AM pack to lunch and keep minerals in the PM pack, ensuring ≥4 h after the thyroid dose.
- Keep the zinc:copper ratio at roughly 8–15:1 (e.g., 8–15 mg Zn with 1 mg Cu). Keep zinc out of the iron unit.
- Calcium >500 mg supplemental → split between AM and PM, but not in the same unit as iron.
- Pair any folic acid ≥800 mcg with B12 (cheap insurance against masking).
- Iron-deficient users who drink coffee or tea with breakfast should get a "take iron 1 h before or 2 h after coffee/tea" instruction rather than complicating the pack.

### Gaps
- No RCTs were found showing that AM/PM splitting improves outcomes (beyond absorption studies). The vitamin C co-administration benefit on hemoglobin recovery is contested; I recall a 2020 JAMA Netw Open RCT finding no added benefit (unverified).

---

## 6. "Cycle syncing" supplementation: what holds up?

### Takeaway
There is **essentially no evidence** for changing nutrient doses by follicular vs luteal phase. Reviews find little to no support for cycle syncing of diet, exercise or supplements, and phase-specific supplement lists come from blogs that cite no studies. What does hold up is **symptom-targeted** supplementation for PMS (B6, calcium, possibly magnesium ± B6), and the trials mostly used **continuous daily dosing**. Menstrual blood loss is a real driver of iron needs, but ferritin is a slow-moving store, so phase-timing iron makes no physiological sense.

### Cited Findings
- A 2023 *Journal of Applied Physiology* review found "little to no evidence supporting cycle syncing, or any other chic advice on eating, exercising or taking supplements during menstruation." Few or no consistent phase differences appeared in substrate use, muscle growth or vascular function. — [UPI/HealthDay coverage](https://www.upi.com/Health_News/2023/12/06/women-exercise-menstrual-cycle/2311701875870/); [MedicalXpress](https://medicalxpress.com/news/2023-12-reliable-evidence-based-scarce-women-menstrual.pdf)
- A later BMJ analysis found no convincing evidence that cycle phase changes performance, injury risk or health enough to justify broad cycle-syncing rules, and called phase-based nutrition studies inconclusive. — [mindbodygreen summary](https://www.mindbodygreen.com/articles/weve-been-told-to-work-with-our-cycles-but-science-isnt-so-simple)
- Retail and wellness sources (e.g., "iron and magnesium during menstruation; B vitamins and zinc in follicular") **cite no studies**. — search synthesis of [iHerb blog](https://ug.iherb.com/blog/cycle-syncing/2164) and [Superpower guide](https://superpower.com/guides/cycle-syncing-hormones-evidence-based-practices)
- PMS evidence: B6, calcium and zinc consistently help psychological symptoms; magnesium evidence is insufficient alone. — [PMC11723155](https://pmc.ncbi.nlm.nih.gov/articles/PMC11723155/). B6 meta-analysis — [PubMed 10334745](https://pubmed.ncbi.nlm.nih.gov/10334745/). Mg + B6 small anxiety effect — [PubMed 10746516](https://pubmed.ncbi.nlm.nih.gov/10746516/)

### Inferences
- **Holds up:** "If you report moderate–severe premenstrual symptoms, we add calcium (to ~1,000–1,200 mg total), low-dose B6 and magnesium, *taken daily*, and reassess after 2–3 cycles using a validated symptom diary (e.g., DRSP)." Iron dosing based on reported heavy menstrual bleeding and ferritin is also valid; HMB should also trigger a gyn referral (inference: HMB is a treatable cause of iron deficiency).
- **Marketing, not evidence:** different capsules for follicular vs luteal phases; "seed cycling"; phase-timed zinc, B vitamins or adaptogens. If Vilo wants a phase-aware UX, use it for **symptom tracking and reassessment timing**, not dose changes, and avoid efficacy claims.
- Possible exception: luteal-phase-only *dosing* is evidence-based for SSRIs in PMDD (drug, not supplement). Some PMS supplement trials used luteal-only regimens, but none were found showing luteal-only beats continuous dosing.

### Gaps
- ACOG Clinical Practice Guideline No. 7 (2023, premenstrual disorders) text on calcium, B6 and chasteberry was not retrieved.
- No trial was found that directly compares phase-timed vs continuous supplementation.

---

## 7. Wearable-driven adjustments (HRV, sleep, temperature)

### Takeaway
I found **no evidence** that HRV, sleep-stage or skin-temperature data should change micronutrient doses. Wearables are legitimately useful for (a) estimating cycle phase and ovulation from temperature, (b) tracking outcomes and adherence, and (c) prompting symptom check-ins. None of these justifies automatic dose changes.

### Cited Findings
- Searches for evidence linking HRV or sleep metrics to supplement dosing returned nothing usable; the targeted query could not run because the search budget was exhausted. No guideline from any society reviewed uses wearable metrics as a dosing input. — (absence finding; see Gaps)
- Cycle-phase rules lack evidence anyway, so temperature-derived phase detection has no validated dosing use. — [J Appl Physiol 2023 review coverage](https://www.upi.com/Health_News/2023/12/06/women-exercise-menstrual-cycle/2311701875870/)

### Inferences
- Use wearables as **outcome measures**, e.g., to judge whether a magnesium trial for self-reported poor sleep coincides with better sleep efficiency (an n-of-1 framing), never to auto-titrate.
- Possible **safety** uses:
  - A sustained temperature rise beyond the luteal norm, plus a missed period, → a "possible pregnancy" prompt that switches to the prenatal-safe formula until a test confirms. That is a valuable guardrail.
  - Large drops in activity or weight (e.g., on GLP-1 RAs) → prompt protein and nutrition review.
- Marketing claims such as "your formula adapts to your HRV" would be unsupported.

### Gaps
- No RCTs or validation studies were found for wearable-guided supplementation. A dedicated search (e.g., "HRV magnesium RCT," "Oura supplement") could not run because of the search budget.

---

## 8. Forms, bioavailability, and what physical formats can hold

### Takeaway
Form choices with real evidence:
- **ferrous bisglycinate** (fewer GI effects; equal or better efficacy at lower elemental dose)
- **D3 over D2**
- **folic acid as the evidence-based preconception form** (methylfolate optional, not superior)
- **cyanocobalamin** (well-studied; methylcobalamin not proven superior)
- **avoiding magnesium oxide** when absorption matters
- **calcium citrate** for PPI users
- **KI for iodine**
- **beta-carotene rather than retinol** for reproductive-age women

Format physics is binding:
- **Gummies cannot carry meaningful iron or minerals.**
- **Calcium, magnesium, choline, inositol, creatine and collagen are bulky.** Gram-level doses (creatine 3–5 g, collagen ~10 g, myo-inositol 2–4 g, calcium ≥500 mg elemental) need powder/sachet or multiple capsules.

### Cited Findings
- Bisglycinate vs other iron salts: GI adverse events IRR 0.36; pregnancy Hb +0.54 SMD. 25 mg bisglycinate was non-inferior to 50 mg sulfate. — [PubMed 36728680](https://pubmed.ncbi.nlm.nih.gov/36728680/); [PubMed 24152889](https://pubmed.ncbi.nlm.nih.gov/24152889/)
- D3 is more effective than D2 at raising 25(OH)D. — [PubMed 22552031](https://pubmed.ncbi.nlm.nih.gov/22552031/) [NV]
- MgO is poorly absorbed. — [De Souza 2000](https://pubmed.ncbi.nlm.nih.gov/10746516/). AHS migraine dosing nevertheless uses MgO 400–500 mg. — [AHS](https://americanheadachesociety.org/news/incorporating-nutraceuticals-for-migraine-prevention)
- MTHFR genotype doesn't change folic acid advice, and special folate forms are not needed. — [ACMG](https://pubmed.ncbi.nlm.nih.gov/23288205/); [CHOP](https://www.chop.edu/pediatric-health-chat/what-to-know-about-mthfr-testing)
- **Gummies:**
  - Rarely contain iron, because of metallic taste and stability problems; mineral loading is limited, especially calcium. — [NutraIngredients-USA](https://www.nutraingredients-usa.com/Article/2018/05/07/Multivitamin-gummies-Experts-share-their-tips-on-how-to-formulate-them); [New Chapter](https://newchapter.com/blogs/wellness-blog/multivitamin-gummies-everything-you-need-to-know)
  - Vitamins degrade faster in gummies, so overages are used; USP allows 5–20 percentage points more leeway on maximums for gummies. — [ConsumerLab](https://www.consumerlab.com/answers/is-there-a-cause-for-concern-with-gummy-vitamins/gummy_vitamin_concern)
  - CSPI found none of 37 gummy multis a good substitute for a tablet multi. — [CSPI](https://www.cspinet.org/news/dont-rely-gummy-multivitamin-if-you-can-swallow-tablet-20171121)
  - Gummies are less suited to clinically relevant doses of key nutrients. — [Vitaquest](https://vitaquest.com/gummies-vs-capsules/)
- Calcium carbonate is ~40% elemental and best taken with food. Calcium citrate is ~21% elemental, absorbed without food and better with low stomach acid or PPIs. — [ODS Calcium](https://ods.od.nih.gov/factsheets/Calcium-HealthProfessional/) [NV]
- Cyanocobalamin is the most-studied form, and no form has been shown superior in healthy people. — [ODS B12](https://ods.od.nih.gov/factsheets/VitaminB12-HealthProfessional/) [NV]

### Inferences
**Stoichiometry: % elemental by mass**, my calculation from molecular weights. These figures decide how many capsules a dose needs:
- Mg oxide ~60%; Mg citrate (trimagnesium dicitrate) ~16%; **Mg bisglycinate ~14%**. Commercial "buffered" Mg glycinate is often ~18–20% because it is blended with MgO.
  - So 300 mg elemental Mg ≈ **~2.1 g pure bisglycinate**, or 0.5 g MgO.
- Calcium carbonate 40% / citrate tetrahydrate ~21%.
  - So 500 mg elemental Ca ≈ 1.25 g carbonate or ~2.4 g citrate.
- Ferrous bisglycinate ~27%; ferrous sulfate heptahydrate ~20% (dried ~30–33%).
  - So 60 mg Fe ≈ ~220 mg bisglycinate.

**Capsule capacity** [NV, industry rule of thumb]: a size 00 capsule holds roughly 0.9–0.95 mL, i.e., about **500–800 mg** of typical powder depending on bulk density.
- A daily pack of 4–6 capsules therefore holds about 3–4 g of total powder.
- Full RDA magnesium as glycinate plus 500 mg calcium alone would take ~5–7 capsules.

**Implications:**
- Use 1–2 "core" capsules (vitamins, trace minerals, iodine, folate, B12, D).
- Use separate mineral capsules or tablets (Ca/Mg), sized by tier.
- Use a separate omega-3 softgel (EPA/DHA cannot go in powder capsules).
- Use an optional **sachet** for gram-dose actives: creatine 3–5 g, myo-inositol 2–4 g, collagen, protein, fiber, high-dose magnesium citrate.
- Tablets compress better than capsules, giving more mg per unit, but are harder to personalize at batch size 1.
- Gummies should **not** be used for iron, calcium, magnesium or zinc at therapeutic doses.

**Form defaults (proposed):**
- D3 (cholecalciferol)
- folic acid; optional L-5-MTHF as Ca or glucosamine salt, at a folate-equivalent dose
- cyanocobalamin, or methylcobalamin as a marketing preference with no claim of superiority
- ferrous bisglycinate
- Mg glycinate/citrate (MgO only for migraine dosing or when the capsule count is constrained)
- calcium citrate (if PPI) or carbonate (with food)
- potassium iodide
- zinc bisglycinate or picolinate with copper bisglycinate
- beta-carotene for vitamin A
- omega-3 as rTG or EE fish/algal oil (algal DHA for vegans)
- riboflavin (plain) for migraine
- creatine monohydrate (the only well-studied form)

### Gaps
- No authoritative source was retrieved on capsule fill weights, sachet stability, or the maximum mineral load per gummy; the figures above are rules of thumb or my calculations. Manufacturing is out of scope and covered by another researcher.
- Omega-3 rTG vs EE bioavailability data were not retrieved (my understanding: differences shrink when taken with a fat-containing meal).

---

## 9. Engine architecture: rules vs ML, how competitors describe it, clinical review, and guardrails

### Takeaway
Given the evidence base, the defensible architecture is a **deterministic, versioned, rules-based clinical decision engine**: guideline-derived dose rules, hard UL/interaction/life-stage constraints, and red-flag referral. A clinical advisory board (MD, RD, PharmD) must own and audit it, and cases flagged as higher risk go to human review. ML, if used, belongs **upstream** (diet-intake estimation from food logs, adherence prediction, symptom triage, personalized vitamin D dose-response prediction) or **downstream** (UX and ranking among equally safe options). It should never sit inside the safety layer. Competitors' public descriptions are thin and marketing-heavy; Bioniq describes a data-trained algorithm, but no validation was published.

### Cited Findings
- **Bioniq.** "PRO" takes uploaded or partner-lab bloodwork; "GO" is questionnaire-based and uses "anonymized blood biomarker data from previous users." Bioniq claims a database of >40,000 people / 4M data points and a self-updating algorithm. — [AgFunderNews](https://agfundernews.com/meet-the-founder-nutrition-gets-personal-for-bioniqs-vadim-fedotov); [The Next Web](https://thenextweb.com/news/bioniq-taps-big-data-algorithms-to-make-supplements-bespoke); [Startups Magazine](https://startupsmagazine.co.uk/article-bioniqs-personalised-supplements-blood-test)
- Industry discussion of combining bloodwork, questionnaires and AI. — [NutraIngredients NutraCast 2023](https://www.nutraingredients.com/Article/2023/12/08/nutracast-bloodwork-questionnaires-and-ai-the-winning-formula-for-precision-nutrition)
- Persona Nutrition is owned by Nestlé Health Science (search snippet; details of its algorithm were not found). — [NutraIngredients NutraCast](https://www.nutraingredients.com/Article/2023/12/08/nutracast-bloodwork-questionnaires-and-ai-the-winning-formula-for-precision-nutrition) [NV for ownership details]
- **Guideline anchors that make rules feasible.** ASH 2026 ferritin cut-offs ([US Pharmacist](https://www.uspharmacist.com/article/ash-guidelines-raise-ferritin-thresholds-for-iron-deficiency/)); the Endocrine Society 2024 vitamin D position ([PubMed 38828931](https://pubmed.ncbi.nlm.nih.gov/38828931/)); USPSTF folic acid ([USPSTF](https://www.uspreventiveservicestaskforce.org/uspstf/recommendation/folic-acid-for-the-prevention-of-neural-tube-defects-preventive-medication) [NV]); ADA B12/metformin ([PubMed 39651989](https://pubmed.ncbi.nlm.nih.gov/39651989/)); TGA/EFSA B6 limits ([NutraIngredients](https://www.nutraingredients.com/Article/2025/11/25/vitamin-b6-supplements-face-new-regulation-in-australia); [PMC10189633](https://pmc.ncbi.nlm.nih.gov/articles/PMC10189633)); FDA biotin interference ([FDA](https://www.fda.gov/medical-devices/in-vitro-diagnostics/biotin-interference-troponin-lab-tests-assays-subject-biotin-interference)).
- The genotype → nutrition link did not add value in the largest PN RCT. — [Food4Me](https://pubmed.ncbi.nlm.nih.gov/27524815/). MTHFR testing is not recommended. — [ACMG](https://pubmed.ncbi.nlm.nih.gov/23288205/)

### Inferences
**Proposed engine pipeline.** All logic is versioned, every rule cites its source, and every formula is reproducible.
1. **Intake and normalization.**
   - Labs, with units normalized (ng/mL vs nmol/L; pg/mL vs pmol/L), reference ranges captured, collection date tracked, staleness rules applied (e.g., ferritin >6 months old = stale), and confounders flagged.
   - Confounders: CRP elevation inflates ferritin; recent biotin use; current supplement use.
   - Also captured: medications (RxNorm-coded), conditions, life stage, diet (FFQ), symptoms (validated instruments: DRSP for PMS, MIDAS for migraine, PSQI/ISI for sleep, MRS for menopause).
2. **Hard-stop / referral layer**, evaluated first. Proposed thresholds, **to be set by the clinical board; not sourced**:
   - Hb <12 g/dL (non-pregnant) → anemia; recommend physician work-up alongside iron. Hb <10 or symptomatic → urgent.
   - Ferritin <15 with heavy menstrual bleeding → gyn referral.
   - Ferritin >200 ng/mL with TSAT >45% → hold iron; physician (hemochromatosis/inflammation).
   - TSH outside ~0.4–4.5 mIU/L (or lab range) → no iodine/selenium/kelp/biotin changes; physician. TSH <0.1 or >10 → prompt referral.
   - 25(OH)D >100 ng/mL or serum calcium above range → stop vitamin D/calcium; physician.
   - B12 <150–200 pg/mL with neuro symptoms → physician.
   - eGFR <60 → no Mg >RDA, no creatine, no potassium; physician.
   - ALT/AST >2–3× ULN → no botanicals; physician.
   - HbA1c ≥6.5% → diabetes referral.
   - Pregnancy positive → switch to prenatal ruleset + OB prompt.
   - Prior NTD pregnancy or antiepileptic use → clinician-directed folic acid.
   - Anticoagulants, lithium, transplant, chemotherapy → pharmacist review before shipping.
   - Eating-disorder signals → clinician review.
3. **Base formula by life stage**: reproductive-age (not trying), trying to conceive, pregnant (by trimester if desired), lactating, perimenopause, postmenopause; plus diet pattern (vegan → B12, iodine, algal DHA, ± iron/zinc).
4. **Lab-driven adjustments**: ferritin/Hb for iron, 25(OH)D (if measured), B12/MMA, omega-3 index (if measured). Do not adjust on non-validated labs such as hair minerals or micronutrient "intracellular" panels (inference).
5. **Symptom and condition modules**: PMS, migraine, PCOS, menopause, GLP-1 users. Each carries its evidence grade and a time-boxed reassessment.
6. **Constraint solver.**
   - Sum diet + other supplements + Vilo per nutrient and enforce ≤UL (or ≤80% of UL buffer).
   - Apply interaction rules and pack placement (AM/PM, iron alternate days).
   - Apply format capacity (capsule count ≤ N; otherwise move to a sachet or drop the lowest-evidence item).
   - Prefer dropping low-evidence items over trimming high-evidence ones.
7. **Human review queue**: any flag, any medication on a watchlist, pregnancy, any dose above a "routine" tier (e.g., iron >45 mg, D >2,000 IU, B6 >25 mg). An RD or PharmD reviews, and an MD reviews referrals.
8. **Retest and feedback loop**: ferritin 8–12 weeks after starting iron; 25(OH)D ≥3 months after a change; symptoms every 2–3 cycles. Here, ML is legitimately useful for learning individual dose-response, e.g., vitamin D by BMI and baseline, within fixed safety bounds.

**ML role summary**: do not let ML pick doses outside rule-defined bounds, and do not use genotype. A transparent rules engine also makes regulator, clinician and advisory-board audit straightforward.

### Gaps
- Public algorithm descriptions for Persona, Rootine (which markets DNA + blood + lifestyle inputs, per my recollection [NV]), Baze, Nourished, Vitl, Thorne, InsideTracker and Function Health could not be retrieved; company science pages were not reachable within the budget.
- No published validation of any competitor's algorithm was found.
- Red-flag thresholds above are proposals from standard clinical practice, not from a single retrieved guideline. WHO anemia cut-offs (Hb <12 g/dL non-pregnant, <11 pregnant) are [NV].

---

## 10. Practical SKU strategy: how many ingredients and dose increments?

### Takeaway
No published source specifies an ingredient-library size for personalized supplements; this is inference. The evidence base above supports roughly **30–40 active ingredients**, most at **2–3 dose tiers**. Tiers should be set at clinically meaningful steps (e.g., D3 1,000 / 2,000 IU; iron 18 / 27 / 60 mg; Mg 100 / 200 / 300 mg). Physically, they map to roughly 1–2 core capsules, 0–4 tiered mineral or specialty capsules, 0–1 omega-3 softgels and 0–1 sachet. Most users will be covered by about 6 life-stage base blends plus about 10–15 tiered add-ons.

### Cited Findings
- No source found that describes a personalized-supplement ingredient library size or dose-tier design. (absence finding)
- The dose anchors used below come from the sources in sections 2–5:
  - iron alternate-day ~60 mg ([Stoffel](https://www.research-collection.ethz.ch/handle/20.500.11850/233029?show=full)); 25 mg bisglycinate in pregnancy ([PubMed 24152889](https://pubmed.ncbi.nlm.nih.gov/24152889/))
  - folic acid 400–800 mcg ([USPSTF](https://www.uspreventiveservicestaskforce.org/uspstf/recommendation/folic-acid-for-the-prevention-of-neural-tube-defects-preventive-medication) [NV])
  - DHA ≥500 mg / LC n-3 500–1,000 mg ([Cochrane](https://www.cochrane.org/news/new-research-finds-omega-3-fatty-acids-reduce-risk-premature-birth))
  - Mg 400–500 mg and riboflavin 400 mg for migraine ([AHS](https://americanheadachesociety.org/news/incorporating-nutraceuticals-for-migraine-prevention))
  - creatine ≥5 g ([PubMed 42141930](https://pubmed.ncbi.nlm.nih.gov/42141930/))
  - B6 10–25 mg for nausea ([AAFP](https://www.aafp.org/pubs/afp/issues/2014/0615/p965.html)), with ≤50 mg general cap ([TGA via NutraIngredients](https://www.nutraingredients.com/Article/2025/11/25/vitamin-b6-supplements-face-new-regulation-in-australia))
  - choline 450 mg, iodine 220 mcg total in pregnancy ([ODS Pregnancy](https://ods.od.nih.gov/factsheets/Pregnancy-HealthProfessional/))

### Inferences
Proposed ingredient library (≈35 actives) with dose tiers:

| Category | Ingredient (form) | Tiers (per day) | Unit type |
|---|---|---|---|
| Core vitamins | D3 | 600–1,000 / 2,000 IU (4,000 only with clinician) | core capsule |
| | Folic acid (± L-5-MTHF alt) | 0 / 400 / 800 mcg | core |
| | B12 (cyanocobalamin or methyl) | 2.4–25 / 250–500 / 1,000 mcg | core |
| | B6 (pyridoxine HCl or P5P) | 1.3–2 / 10 / 25 (PMS ≤50, time-boxed) mg | core / module |
| | Thiamin, riboflavin, niacinamide, pantothenate | ~RDA (1–2× RDA) | core |
| | Riboflavin high-dose | 400 mg | migraine capsule |
| | Biotin | 30 mcg (fixed; never high-dose) | core |
| | Vitamin C | 0 / 75–100 / 250 mg | core |
| | Vitamin E (d-α-tocopherol) | 0 / 15 mg | core |
| | Vitamin A as beta-carotene (retinol ≤750 mcg RAE only if non-pregnant and needed) | 0 / ~RDA | core |
| | Vitamin K1 or K2 (MK-7) | 0 / 90–120 mcg (lockout on warfarin) | core |
| | Choline (bitartrate or CDP) | 0 / 150 / 300 mg (bulk-limited) | capsule / sachet |
| Minerals | Iron bisglycinate | 0 / 18 / 27 / 60 mg alt-day (≥60 w/ clinician) | separate iron capsule |
| | Iodine (KI) | 0 / 150 mcg | core |
| | Zinc bisglycinate + copper (1 mg) | 0 / 8 / 15 mg Zn | PM capsule |
| | Selenium (selenomethionine) | 0 / 55 mcg | core |
| | Magnesium glycinate/citrate (MgO for migraine tier) | 0 / 100 / 200 / 300–400 mg elemental | PM capsules / sachet |
| | Calcium citrate or carbonate | 0 / 250 / 500 mg (split doses) | PM capsules |
| Lipids | Omega-3 EPA+DHA (fish or algal) | 0 / 500 / 1,000 mg (prenatal: ≥500 mg DHA) | softgel |
| Specialty | Myo-inositol (± DCI 40:1) | 2 / 4 g | sachet |
| | Creatine monohydrate | 3 / 5 g | sachet |
| | Collagen peptides | 5–10 g (low evidence) | sachet |
| | Protein (GLP-1 / menopause) | 10–20 g | sachet |
| | Psyllium/fiber | 3–5 g | sachet |
| | CoQ10 (ubiquinone or ubiquinol) | 0 / 100–200 mg (low evidence) | capsule |
| | Probiotic (strain-specific, e.g., for an indication with data) | fixed | separate capsule (viability) |
| Botanicals (gated) | Black cohosh, vitex, saffron, ashwagandha, curcumin, green tea extract | Default OFF; clinician-gated; LFT/pregnancy checks | — |

- **Base blends (~6)**: Reproductive (not TTC), TTC/Prenatal T1, Prenatal T2–T3, Lactation, Perimenopause, Postmenopause. Variants for vegan and for levothyroxine (timing split).
- **Coverage arithmetic**: 6 base blends × tiered add-ons (iron 4, Mg 4, Ca 3, D 2–3, B12 3, omega-3 3, zinc 3, specialty modules on/off) gives thousands of combinations from ~35 inventory SKUs. Build-to-order dispensing (pick-and-pack of discrete units) is likely simpler than compounding a unique blend per person. Manufacturing feasibility is out of scope; another researcher covers it.
- **Prioritize by evidence and prevalence**: iron, folate, D, B12, iodine, omega-3/DHA, choline, calcium and magnesium cover most of the evidence-backed personalization for women. Specialty modules (inositol, creatine, migraine, PMS) are second tier. Collagen, probiotics, CoQ10, K2 and botanicals are third tier, with honest evidence labels.

### Gaps
- No industry or academic benchmark for library size or dose-increment granularity was found.
- The prevalence data needed to size tiers (e.g., the share of US women with ferritin ≤30, or with low 25(OH)D) were not retrieved this session. NHANES is the likely source, and that prevalence data would sharpen tier design.
- Research limitations: the shared web-search budget was exhausted, and primary sites (ods.od.nih.gov, tga.gov.au, obesity.org, contemporaryobgyn.net) were blocked for direct fetch. The [NV] items should be re-verified once those hosts are allowed in the session's network settings.
