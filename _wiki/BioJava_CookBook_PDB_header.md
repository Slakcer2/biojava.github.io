---
title: BioJava:CookBook:PDB:header
permalink: wiki/BioJava%3ACookBook%3APDB%3Aheader
---

### How can I access the header information of a PDB file?

BioJava can parse the COMPND and SOURCE header files. Thanks to Jules
Jacobsen (EBI) for providing the patch. The contained information is
availabe via the
[Compound](http://www.biojava.org/docs/api/org/biojava/bio/structure/Compound.html)
class that can be accessed from
[structure.getCompounds()](http://www.biojava.org/docs/api/org/biojava/bio/structure/Structure.html).

```java

   public static void main(String[] args) throws Exception {  
         
       String code =  "1aoi";

       AtomCache cache = new AtomCache();  
         
       Structure struc = cache.getStructure(code);  
         
       PDBHeader header = struc.getPDBHeader();  
         
       System.out.println(header.toString());  
         
       System.out.println("available compounds:");  
       List<Compound> compounds = struc.getCompounds();  
       for (Compound compound:compounds){  
           System.out.println(compound);  
       }  
         
   }

```

gives the following output:

    Description: DNA BINDING PROTEIN/DNA BioAssemblies: {} NrBioAssemblies: 0 ExperimentalTechniques: [X-RAY DIFFRACTION] Classification: DNA BINDING PROTEIN/DNA DepDate: Thu Jul 03 00:00:00 CEST 1997 IdCode: 1AOI ModDate: Tue Feb 24 00:00:00 CET 2009 Title: COMPLEX BETWEEN NUCLEOSOME CORE PARTICLE (H3,H4,H2A,H2B) AND 146 BP LONG DNA FRAGMENT CrystallographicInfo: [P 21 21 21 - 106.04 181.78 110.12, 90.00 90.00 90.00] Resolution: 2.8 Rfree: 0.302 Authors: K.Luger,A.W.Maeder,R.K.Richmond,D.F.Sargent,T.J.Richmond 
    available compounds:
    Compound: 1 (PALINDROMIC 146 BP DNA REPEAT 8/9 FROM HUMAN X-CHROMOSOME ALPHA SATELLITE DNA) chains: I,J
    Compound: 2 (HISTONE H3) chains: A,E
    Compound: 3 (HISTONE H4) chains: B,F
    Compound: 4 (HISTONE H2A) chains: C,G
    Compound: 5 (HISTONE H2B) chains: D,H

Next: <BioJava:CookBook:PDB:seqres> - How to deal with SEQRES and ATOM
records
