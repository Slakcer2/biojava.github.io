---
title: BioJava:Cookbook:Sequence
permalink: wiki/BioJava%3ACookbook%3ASequence
---

How do I make a Sequence from a String or make a Sequence Object back into a String?
------------------------------------------------------------------------------------

A lot of the time we see a sequence represented as a String of
characters e.g. "atgccgtggcatcgaggcatatagc". It's a convenient method
for viewing and succinctly representing a more complex biological
polymer. BioJava makes use of SymbolLists and Sequences to represent
these biological polymers as Objects. Sequences extend SymbolLists and
provide extra methods to store things like the name of the sequence and
any features it might have but you can think of a Sequence as a
SymbolList.

Within Sequence and SymbolList the polymer is not stored as a String.
BioJava differentiates different polymer residues using Symbol objects
that come from different Alphabets. In this way it is easy to tell if a
sequence is DNA or RNA or something else and the 'A' symbol from DNA is
not equal to the 'A' symbol from RNA. The details of Symbols,
SymbolLists and Alphabets are covered here. The crucial part is there
needs to be a way for a programmer to convert between the easily
readable String and the BioJava Object and the reverse. To do this
BioJava has Tokenizers that can read a String of text and parse it into
a BioJava Sequence or SymbolList object. In the case of DNA, RNA and
Protein you can do this with a single method call. The call is made to a
static method from either DNATools, RNATools or ProteinTools.

### String to SymbolList

```java 
import org.biojava.bio.seq.\*; import org.biojava.bio.symbol.\*;

public class StringToSymbolList {

 public static void main(String[] args) {  
    
   try {  
     //create a DNA SymbolList from a String  
     SymbolList dna = DNATools.createDNA("atcggtcggctta");

     //create a RNA SymbolList from a String  
     SymbolList rna = RNATools.createRNA("auugccuacauaggc");

     //create a Protein SymbolList from a String  
     SymbolList aa = ProteinTools.createProtein("AGFAVENDSA");  
   }  
   catch (IllegalSymbolException ex) {  
     //this will happen if you use a character in one of your strings that is  
     //not an accepted IUB Character for that Symbol.  
     ex.printStackTrace();  
   }  
    
 }

} 
```

### String to Sequence

```java 
import org.biojava.bio.seq.\*; import org.biojava.bio.symbol.\*;

public class StringToSequence {

 public static void main(String[] args) {

   try {  
     //create a DNA sequence with the name dna_1  
     Sequence dna = DNATools.createDNASequence("atgctg", "dna_1");

     //create an RNA sequence with the name rna_1  
     Sequence rna = RNATools.createRNASequence("augcug", "rna_1");

     //create a Protein sequence with the name prot_1  
     Sequence prot = ProteinTools.createProteinSequence("AFHS", "prot_1");  
   }  
   catch (IllegalSymbolException ex) {  
     //an exception is thrown if you use a non IUB symbol  
     ex.printStackTrace();  
   }  
 }

} 
```

### SymbolList to String

You can call the seqString() method on either a SymbolList or a Sequence
to get it's Stringified version.

```java 
import org.biojava.bio.symbol.\*;

public class SymbolListToString {

 public static void main(String[] args) {  
   SymbolList sl = null;  
   //code here to instantiate sl  
    
   //convert sl into a String  
   String s = sl.seqString();  
 }

} 
```

The above example uses the process of 'tokenization' to create the
String, in this case hidden in the SeqString method. Different types of
tokenization can be used to control the output String.

```java

Alphabet alph; // An alphabet SymbolList sym; //A SymbolList

SymbolTokenization tok= alph.getTokenization("token"); String output =
tok.tokenizeSymbolList(sym)

```

Use "token" or "default" to represent nucleotides and amino acids in
lower case single characters; use "alternate" to represent DNA in single
capital letters and amino acids from the PROTEIN\_TERM alphabet in
character triplets (e.g. Arg) (see
[AlternateTokenization](http://www.biojava.org/docs/api1.8/org/biojava/bio/seq/io/AlternateTokenization.html)).
