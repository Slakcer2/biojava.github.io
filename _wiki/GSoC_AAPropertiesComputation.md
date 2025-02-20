---
title: GSoC:AAPropertiesComputation
permalink: wiki/GSoC%3AAAPropertiesComputation
---

**Amino Acids Physicochemical Properties Calculation**

*[Google Summer of Code](Google Summer of Code "wikilink") Project by
[Chuan Hock Koh](Chuan Hock Koh "wikilink")*

*Mentored by [Peter Troshin](http://biojava.org/wiki/User:Ptroshin)*

*Co-mentored by [Andreas Prlic](Andreas Prlic "wikilink")*

The calculation of physicochemical properties for biopolymers is an
important tool in the arsenal of molecular biologist. Theoretically
calculated quantities like extinction coefficients, isoelectric points,
hydrophobicities and instability indices are useful guides as to how a
molecule behaves in an experiment. Many tools for calculating these
properties exist, including widely used open-source implementations in
EMBOSS and BioPerl, but only some are currently available in BioJava3.
The aim of this project is to port or produce new implementations of
standard algorithms for a range of calculations within BioJava3 and make
them available in various levels (APIs, executable and web service).

Properties
----------

Listing the properties that could be considered for implementing. Mainly
based on the original proposal, PROFEAT and Sirius PSB. We welcome more
ideas for additional/removal of properties. Note: The semi-circle
bracket () after the name of a property indicates the number of values
this property will generate.

### Originally proposed properties

-   Molecular weight (1)
-   Extinction coefficient (2 – Assumes Cys are reduced and assumes Cys
    form cystines)
-   Instability index (1)
-   Aliphatic index (1)
-   Grand Average of Hydropathy (1)
-   Isoelectric point (1)
-   Number of amino acids in the protein (1)

### Other obvious properties to consider

-   Amino acid composition (20)
-   Dipeptide acid compostion (400)
-   Net Charge (1)

### PROFEAT properties

Sequences are first transformed into representation of different
attribute and each attribute has 3 groups. In PROFEAT, there are 7
different attributes.

-   Hydrophobicity (Polar, Neutral, Hydrophobicity)
-   Normalized van der Waals volume (Range 0 – 2.78, 2.95 – 4.0, 4.03 –
    8.08)
-   Polarity (Value 4.9 – 6.2, 8.0 – 9.2, 10.4 – 13.0)
-   Polarizability (Value 0 – 1.08, 0.128 – 0.186, 0.219 – 0.409)
-   Charge (Positive, Neutral, Negative)
-   Secondary structure (Helix, Strand, Coil)
-   Solvent accessibility (Buried, Exposed, Intermediate)

After transformation, PROFEAT computes three type of properties

-   Composition (3 \* 7 = 21)
-   Transition (3 \* 7 = 21) – [1\<-\>2, 1\<-\>3, 2\<-\>3]
    -   A transition from class 1 to 2 is the percent frequency with
        which 1 is followed by 2 or 2 is followed by 1 in the
        transformed sequence
-   Distribution (3 \* 5 \* 7 = 105)
    -   It measures the position percent in the whole sequence of
        encoded residue for first residue, 25%, 50%, 75%, 100%.

### Other PROFEAT properties

PROFEAT also computes a series of properties based on autocorrelations
and sequence-order which are harder to comprehend. Please see PROFEAT
[manual](http://jing.cz3.nus.edu.sg/prof/prof_manual.pdf) for details.

-   Normalized Moreau-Broto autocorrelation (240)
-   Moran autocorrelation (240)
-   Geary autocorrelation (240)
-   Sequence-order-coupling number (60)
-   Quasi-sequence-order descriptors (100)

### Sirius PSB properties

Likewise, Sirius PSB transforms sequences accordingly to their
respective grouping based on the different attributes. However, it
computes different properties from them.

-   Number of AA in (or Size) the maximum region (1 \* 7 = 7)
-   Value of the maximum region (1 \* 7 = 7)
-   Location of the maximum region (2 \* 7 = 14) – start and end
    -   Note: Maximum region is the region that has the highest value of
        a particular grouping. E.g. the most hydrophobic region in the
        sequence
-   Number of regions with at least size X (1 \* 7 = 7)
-   Number of regions with at least value Y (1 \* 7 = 7)

Timeline
--------

### Phase 1 (7 Weeks)

*April 25 to June 12* - Deliverables: APIs

-   Research and finalize with mentors the properties to be included
-   Start coding of APIs while writing the documentation concurrently

### Phase 2 (3 Weeks)

*June 13 to July 3* - Deliverables: Tested APIs and Documentations

-   Write test cases to ensure accuracy of the APIs
-   Clean up codes and documentation for readability
-   Update BioJava wiki page and write tutorial for using APIs
-   Check with mentor on areas of improvement

### Phase 3 (2 Weeks)

*July 4 - July 17* - Deliverables: Executable

-   Develop, test and document command line executable for generating
    properties
-   Update BioJava wiki page and write tutorial for using Executables

### Phase 4 (2 Weeks)

*July 18 - July 31* - Deliverables: SOAP web services

-   Expose APIs as SOAP web services within the JABAWS framework
-   Test and document the services

### Phase 5 (3 Weeks)

*August 1 to August 21*

-   Final touch-up based on mentors’ feedback

Progress Log
------------

### April 26 - May 4 (Week 1)

-   Set up project page in BioJava Wiki
-   Arranged to have weekly skype meeting every Tuesday 1600 London time
    (GMT +1) with both Mentors, Peter and Andreas.
-   Suggests properties to consider for this project.
-   Decision has been made to start working on the originally proposed
    APIs with only the addition of amino acid composition. More
    properties will be considered if there is time left after the
    completion of these properties.
-   Created a BioJava SVN account and successfully checkout biojava3 as
    Maven Projects.

### May 5 - May 12 (Week 2)

-   Completed initialization. Ready to start coding.
-   Created a user page for myself on BioJava Wiki.
-   Introduced to the biojava developer mailing list.
-   Request for input and suggestion from biojava developer mailing list
    on this project.
-   Committed the first draft of the interface class for the basic
    physicochemical properties.
-   Updated interface class for basic physicochemical properties based
    on Mentors' feedback.
-   Learned and better understand how to use Maven on Eclipse.

### May 13 - May 20 (Week 3)

-   Gathered websites/publications needed for constraints.
-   Refactoring packages and classes for more readability.
-   Learning to properly document work according to set standard.
-   Finalizing the approach for implementation.
-   Initial implementation of a few properties.

### May 21 - May 27 (Week 4)

-   Implemented all basic properties.
-   Verified them manually based on three web tools.
    -   <http://web.expasy.org/protparam/>
    -   <http://web.expasy.org/compute_pi/>
    -   <http://www.innovagen.se/custom-peptide-synthesis/peptide-property-calculator/peptide-property-calculator.asp>
-   Implemented adaptor methods for all basic properties.
-   Basic properties includes the following
    -   Molecular Weight
    -   Extinction Coefficient
    -   Instability Index
    -   Apliphatic Index
    -   Average Hydropathy
    -   Isoelectric Point
    -   Net Charge
    -   Amino Acid Composition

### May 28 - June 2 (Week 5)

-   Added several additional adaptor methods to make usage more user
    friendly.
    -   public static final double getEnrichment(String sequence, char
        aminoAcidCode)
    -   public static final double getEnrichment(String sequence, String
        aminoAcidCode)
    -   public static final Map<String, Double>
        getAACompositionString(String sequence)
    -   public static final Map<Character, Double>
        getAACompositionChar(String sequence)
-   Implemented an additional properties, absorbance.
-   Also implemented adaptor methods for making computation of
    absorbance more user friendly.
-   Implemented JUnit test cases for all properties.
    -   Based on <http://au.expasy.org/cgi-bin/protparam> and
        <http://www.innovagen.se/custom-peptide-synthesis/peptide-property-calculator/peptide-property-calculator-notes.asp>
    -   However, many does not pass assertEquals due to precision
        problem.
-   Added Javadoc for Constraints.java and PeptideProperties.java

### June 3 - June 10 (Week 6)

-   Removed Java docs from repository.
-   Slightly modified current adaptor methods to allow user to decide on
    the number of decimal places required for their usage.
-   Added adaptor methods with default decimal places.
-   All JUnit test cases passes now.
-   Added a new class, Utils under aaproperties with main objective to
    provide some utility methods that does not belong to any other
    available classes.
-   Added the following methods into Utils.
    -   public final static double roundToDecimals(double, int) - this
        method enable the rounding of value to desired decimal places.
    -   public final static boolean
        doesSequenceContainInvalidChar(String) - this method checks if
        the sequence contains invalid character. Return true if invalid
        character exists, false otherwise.
        -   Any character outside of the standard 20 amino acid codes
            are considered to be invalid.
    -   public final static String cleanSequence(String) - this method
        replaces any invalid character in sequence with '-'.
-   Added more test cases when invalid input are given to properties
    generating methods.
    -   Adjusted methods to handle such cases.
    -   If input protein sequence is null, a null exception will be
        thrown.

### June 11 - June 18 (Week 7)

-   Remove all catch exception in test cases and replace them with
    expected = NullPointerException.class.
-   Added several test methods to accommodate this.
-   Change all adaptor methods to return full precision by default.
-   Only fix the precision for the test cases to ensure they will not
    fail due to precision problem.
-   Created a new package - org.biojava3.aaproperties.xml
    -   Created two classes under this package - IsotopeType.java and
        IsotopeTable.java.
    -   The purpose of these package and classes are initial effort to
        learn and utilize JAXB for properties' value definition in
        particular for molecular weight.
-   Populated two elements based on Peter's Element class.
-   Create a ElementTester to test the generated xml and its computed
    standard atomic weight.
-   Also created several classes to prepare for the generation of
    PROFEAT properties.
-   Finished implementing APIs for generating PROFEAT properties and
    also added adaptor method for the ease of utilizing them

### June 19 - June 23 (Week 8)

-   Removed Utils.roundToDecimals from PeptidePropertiesImpl.java
-   Embedded all data from the element information website
-   Create Test Cases to ensure data are properly embedded
-   Generated XML files for Element Mass and Amino Acid Composition.
-   Able to read in XML files for Element Mass and Amino Acid
    Composition into Java via JAXB.
-   Create new methods to enable the usage of user specified xml file to
    compute molecular mass
-   Wrote test cases for these newly created methods

### June 24 - June 29 (Week 9)

-   Created ValidationEventHandler which allows the xml file to be
    validated
-   Validates xml files before they are unmarshal
-   Added an additional method to auto find a elementMass file in
    default location
-   Generated the schema for aminoacidcomposition.xsd
-   Change the XML file structure such that the element weight is
    directly recorded instead of computed
-   Remove all the test cases for the computation of the abundance.
-   Successfully generated an XML schema for ElementMass.xsd and
    AminoAcidComposition.xsd
-   Remove abundance from ElementMass.xml
-   Created in Cookbook with short examples showing how to utilize the
    APIs
-   How each properties are computed are also given (excluding
    Instability Index and Net Charge due to syntax technicalities)
-   Also added a test class in Maven to ensure that the short examples
    given are error-free

### June 30 - July 7 (Week 10)

-   Added several methods in different classes to enable the usable of
    methods that does not need to specify location of ElementMass.xml
-   Improve the CookbookTester.java to combine shortExample 4 and 5 plus
    utilizing methods that do not need to explicitly specify
    ElementMass.xml in shortExamples 2 and 3
-   Added annotations for AminoAcidComposition.java and Element.java.
-   Simplified MolecularWeight.xml and ElementMass.xml.
-   Work around JAXB inability to handle Map<K, V> and used List<E>
    instead so as to made the XML files annotated to requirements.
-   Adjust the XML requirements and made attributes as optional if
    possible
-   Checked that all Elements and Isotopes used in
    AminoAcidComposition.xml can be found in ElementMass.xml
-   Add CookBook pages on how Net Charge and Instability Index are
    computed.
-   Defined the standard and minimum XML files in the CookBook

### July 8 - July 13 (Week 11)

-   Clean up the codes on Computing Molecular Weights
-   Change the Minimum XML files to more compact
-   Change the naming of several XML attributes to more intuitive and
    generic terms
-   Created two advanced XML files to demonstrate how to define modified
    amino acids such as radioactive labelled and phosphorylation.
-   Did a simple test case for these advanced XML files as well.
-   Check the attribute values to ensure that symbols are single
    character and do not repeat themselves.
-   Also check to ensure that element/isotope names define are also
    found in ElementMass XML file.
-   Mass and counts are also checked to make sure that they are \> 0.
-   Emailed the BioJava community reporting the current status of the
    project and also looking for feedback and suggestions on the
    project.
-   Implemented the first draft of the command prompt executable.

### July 14 - July 21 (Week 12)

-   Created a new class ModifiedAminoAcidCompoundSet which enables any
    symbols to be specified in XML file to represent amino acids and
    modified amino acids.
-   Added three examples on how to run the tool.
-   Change output file to optional and default to standard output.
-   Set default decimal place to 4. Possible to change with -d argument.
-   Change to use BioJava FASTA reader.
-   Created CommandPromptTester.java to do testing of CommandPrompt.java
-   Improved Help - Follows unix "man" style.

### July 22 - July 29 (Week 13)

-   Updated the cookbook on using extended XML file and
    ModifiedAACompoundSet
-   Split up the CommandPrompt run to be more "unit" style
-   Had always assumed that cases are ignored, hence had to change many
    method to consider case difference
-   Introduced another class CaseFreeAminoAcidCompoundSet to ignore
    cases
-   By default, set ignore case. If they provide the XML file, then
    cases will be differentiated
-   Update the cookbook on Command Prompt

### July 30 - August 4 (Week 14)

-   Only consider cases difference for Molecular Weight. Revert all
    cases consideration for other properties.
-   Managed to link up with JABAWS via SVN. Could only checkout but not
    able to commit.
-   Able to commit after some configuration efforts.
-   Committed initial attempt to provide AAProperties as a service in
    JABAWS.
-   Added AAProperties.jar into jabaws/binaries/windows.
-   Added AAProperties description to conf/Executable.properties.
-   Created AAPropertiesLimits.xml and AAPropertiesParameters.xml.
-   Created AAProperties.java under compbio.runner.sequence and extends
    SkeletalExecutable<AAProperties>

### August 5 - August 12 (Week 15)

-   Wrote the parser for AAProperties.jar under JABAWS.
-   Prepared test case for the parser.
-   Uploaded a sample output of AAProperties.jar for testing purposes.
-   Change the return type of parseAAProp to ScoreManager
-   Adjust the configuration of pom.xml to generate a jar file with
    org.biojava3.aaproperties.CommandPrompt as the main class. However,
    need to rename it to AAProperties.jar
-   Added SequenceName in the output of AAProperties.jar (in the first
    column)
-   Modify the SequenceUtil.AAprop result parser to cater for the change
    above in the AAProperties.jar output
-   Managed to rename in the configuration of pom.xml to generate a jar
    file with name that includes AAProperties.

### August 13 - August 19 (Week 16)

-   Completed the integration of AAProperties.jar with JABAWS
-   Checked all links on
    <http://biojava.org/wiki/GSoC:AAPropertiesComputation>
-   Rectified two links <http://web.expasy.org/protparam/> and
    <http://web.expasy.org/compute_pi/>
-   Checked all links on <http://biojava.org/wiki/BioJava:CookBook>
    under Physicochemical Properties Computation
-   Linked up the executable jar file on maven to Cookbook
-   Simplified the section under Physicochemical Properties Computation
    on <http://biojava.org/wiki/BioJava:CookBook>
-   Added dummy id to be allowed in the xml file of
    AminoAcidComposition.
    -   It will be used in future as an option to compute the mass of
        amino acid instead of based only on elements.

### August 20 - Current (Week 17)

-   Shifted Profeat related classes to new packages called
    aaproperties.profeat and aaproperties.profeat.convertor
-   Added package-info.java for all packages
-   Create a test class to test PROFEAT properties
-   Added documentation in Cookbook on how to use PROFEAT properties API
-   Update the BioJava community on what is achieved for this Google
    Summer of Code project

Skype call notes
----------------

Weekly skype calls are on Thursday 08 AM PST

` `[`May` `5th`](aapropsSkype_20110505 "wikilink")  
` `[`May` `12th`](aapropsSkype_20110512 "wikilink")  
` `[`May` `19th`](aapropsSkype_20110519 "wikilink")  
` `[`May` `26th`](aapropsSkype_20110526 "wikilink")  
` `[`June` `2nd`](aapropsSkype_20110602 "wikilink")  
` `[`June` `9th`](aapropsSkype_20110609 "wikilink")  
` `[`June` `16th`](aapropsSkype_20110616 "wikilink")  
` `[`June` `23th`](aapropsSkype_20110623 "wikilink")  
` `[`June` `29th`](aapropsSkype_20110629 "wikilink")  
` `[`July` `6th`](aapropsSkype_20110706 "wikilink")  
` `[`July` `13th`](aapropsSkype_20110713 "wikilink")  
` `[`July` `21st`](aapropsSkype_20110721 "wikilink")  
` `[`July` `28th`](aapropsSkype_20110728 "wikilink")  
` `[`August` `4th`](aapropsSkype_20110804 "wikilink")  
` `[`August` `12th`](aapropsSkype_20110812 "wikilink")  
` `[`August` `17th`](aapropsSkype_20110817 "wikilink")

References
----------

-   [BioJava](http://bioinformatics.oxfordjournals.org/content/24/18/2096.abstract) -
    BioJava: an open-source framework for bioinformatics
-   [SiriusPSB](http://www.worldscinet.com/jbcb/07/0706/S0219720009004436.html) -
    Sirius PSB: A Generic System for Analysis of Biological Sequences
-   [PROFEAT](http://nar.oxfordjournals.org/content/34/suppl_2/W32.abstract) -
    PROFEAT: a web server for computing structural and physicochemical
    features of proteins and peptides from amino acid sequence

Comments
--------

*Please add comments here...*
