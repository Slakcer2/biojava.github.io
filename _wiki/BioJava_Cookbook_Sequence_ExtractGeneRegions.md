---
title: BioJava:Cookbook:Sequence:ExtractGeneRegions
permalink: wiki/BioJava%3ACookbook%3ASequence%3AExtractGeneRegions
---

How can I extract all regions beeing marked (or not) with a special feature (e.g. 'gene' or 'CDS')?
---------------------------------------------------------------------------------------------------

```java

`  public Sequence sequenceJustFeatues(Sequence seq, String featureName)`  
`        throws Exception {`

`     Location loccollection = this.genLocationsOfSequence(seq, featureName);`

`     SymbolList extract = loccollection.symbols(seq);`

`     Sequence seqmodif = DNATools`  
`           .createDNASequence(extract.seqString(), "New Sequence");`  
`     return seqmodif;`  
`  }`

`  public Sequence sequenceWithoutFeature(Sequence seq, String featureName)`  
`        throws Exception {`  
`     // featureName: the name of the feature which describes genes: gene or CDS`

`     Location loccollection = this.genLocationsOfFeature(seq, featureName); // see below`

`     SimpleSymbolList modif = new SimpleSymbolList(seq);`

`     Edit e = null;`

`     for (int i = seq.length(); i > 0; i--){ // this is slow. For a better implementation drop me an email`  
`        if (loccollection.contains(i)) {`  
`           e = new Edit(i, 1, SymbolList.EMPTY_LIST);`  
`           modif.edit(e);`  
`        }`  
`     }`

`     Sequence seqmodif = DNATools.createDNASequence(modif.seqString(), "New Sequence");`  
`     return seqmodif;`  
`  }`

` public Location genLocationsOfFeature(Sequence seq, String featureName)`  
`        throws Exception {`  
`     Location loccollection = null;`

`     for (Iterator i = seq.features(); i.hasNext();) {`  
`        Feature f = (Feature) i.next();`

`        if (f.getType().equals(featureName)) {`

`           if (loccollection == null) {`  
`              loccollection = f.getLocation();`  
`           } else {`  
`              loccollection = loccollection.union(f.getLocation());`  
`           }`  
`        }`  
`     }`  
`     return loccollection;`  
`  }`

```
