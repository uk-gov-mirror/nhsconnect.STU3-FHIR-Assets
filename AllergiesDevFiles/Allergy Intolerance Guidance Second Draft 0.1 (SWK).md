
## Guidance for producers and consumers of the AllergyIntolerance  FHIR&reg; profile

The recording of Allergy and Intolerance information in patient records is a major component of communicating the effects of external substances/compounds on patient health.

The Allergy and Intolerance concept is broad and multidimensional.
* the causation of Allergy and Intolerance may be linked to specific medications or pharmaceuticals or substances (biological or chemical) in the environment
* the weight and significance that may be attached to recorded Allergy and Intolerance is affected by a number of factors including the certainty of the allergy, the severity of the reaction and the likelihood of occurrence
* Allergies and Intolerances may be linked to other clinical events, such as diagnostic tests that confirm the presence of the allergy or linked to instances of illness caused by the allergy
* Allergies and Intolerances may be dynamic and evolving, increasing in severity over time, recurrent or perhaps only active and observed within defined periods

The recording and handling of Allergy and Intolerance information has an important role to play in patient safety, not only with regard to clinical decision making but also in the realm of prescribing decision support, where the presence of allergy information linked to causative agents can trigger automated alerts and restrictions when prescribing.

Given the complexity and depth of the Allergy and Intolerance domain there are significant differences and variations in the implementation of the Allergy and Intolerance concept across participating systems in terms of structure, terminology and the linkages between terminology and decision support. These differences limit the current interoperability of Allergies and Intolerances.

The GP Connect AllergyIntolerance FHIR resource aims to improve the interoperability of Allergies and Intolerances through a standardised structure and common terminology.

The clinical importance of Allergy and Intolerance information coupled with the variability of implementations across participating systems means that there is a need for clear guidance on the utilisation of the GP Connect AllergyIntolerance resource by both producers and consumers.

This page provides the required guidance:
* usage of the FHIR resource elements to represent Allergy and Intolerance concepts from participating systems
* guidance for producers on the correct representation of Allergy/Intolerance concepts as FHIR resources
* guidance for consumers on the handling of the FHIR resources in terms of expectations for what can be present in the resource and the handling of variations between systems

# Roadmap and vision
The Allergy and Intolerance FHIR resource has been developed to address current Allergy and Intolerance interoperability limitations. As such it has been designed to enable a future state in which greater levels of Allergy and Intolerance interoperability are achieved by utilisation of SNOMED CT concepts from the specified Allergy and Intolerance subset. 

The FHIR structure and standard is only an enabler for greater drug allergy interoperability. Drug allergy interoperability is only achieved when drug allergy concepts are understood by receiving systems i.e. trigger equivalent prescribing decision support. Therefore the benefits will not be achieved without participating systems being able to consistently process codes from the defined causative agent subset as concepts capable of triggering prescribing decision support in receiving systems. 

The set of changes required to make the causative agent subset consistently processable by prescribing decision support modules across participating systems falls outside the scope of this guidance document.

In the interim state it is expected that with the gradual adoption of the FHIR resource and associated terminologies, drug allergy interoperability will continue to be partial.

*In the interim period tactical approaches to drug allergy interoperability based on mappings between DM+D products and wider SNOMED CT allergy concepts e.g. Adverse reactions could provide interoperability benefits*

The AllergyIntolerance resource adopts common approaches for expressing certainty and severity, increasing interoperability of qualifiers associated with Allergies and Intolerances. 

Greater expressivity around dates (end dates, onset, occurrence) is also supported.

It is recognised that current support for the full range of severity qualifiers is limited and variable across systems and support for the full range of date concepts will also be limited.

It is also recognised that there will be interim challenges in mapping existing Allergy and Intolerance record structures to the AllergyIntolerance resource. In some systems, Allergy and Intolerance information may be a post-coordinated triple of allergy code, reaction/manifestation code and causative agent code. In other systems, a single pre-coordinated code serves to describe the Allergy/Intolerance concept and the causative agent. In the former case, the AllergyIntolerance resource may not fully support the three coded concepts and in the latter case, there is currently no distinct identification of causative agent and reaction/manifestation.

## Guidelines

### Entries of allergy concepts as 'non-allergies' in source systems
Participating systems have a variety of record types/structures that explicitly represent Allergy and Intolerance structures within the patient record. These structures are explicitly selected by users to record Allergy and Intolerance information in the record or may be automatically triggered by attempts to enter allergy codes/concepts into the patient record. As these structures readily identify the presence of Allergy/Intolerance concepts in the record they are readily identifiable and mappable to the GP Connect AllergyIntolerance request when processing FHIR requests. 

It is also possible in some cases to bypass these data entry features and enter allergy codes/concepts as ordinary coded record entries in the patient record. Such entries may appear in the source system as ordinary journal entries and may not appear as Allergies/Intolerances in patient summaries or Allergy/Intolerance lists in source systems. 

*Where a record entry in a source system is not recognised by the source system as an Allergy/Intolerance it should not be represented as such in FHIR interactions*

### Allergy/Intolerance interoperability and clinical safety
It is recognised that Allergy/Intolerance information may not be fully interoperable between participating systems. Where Allergy/Intolerance information is not fully understood by a receiving system then it is the responsibility of the receiver to mitigate any risks arising and make related workflows as safe as possible. In other contexts, techniques such as prescribing prevention in the presence of non-understood (degraded) drug allergies have been employed. 

*Suppliers should seek appropriate clinical safety guidance when considering the implementation of use cases that involve Allergy/Intolerance interoperability.*

### Orthogonality to problem orientation
On some participating systems it is possible to manage Allergy/Intolerance information via problem orientation. This means, for example, making an Allergy/Intolerance record entry a problem heading with associated episodicities, priorities, linkage (to other record entries) and even start and end dates for the problem, independent of the Allergy/Intolerance record entry.

*The dual representation of an Allergy/Intolerance as a problem should not affect the representation of the Allergy/Intolerance via the FHIR resource*

### Unsupported qualifiers
It is possible on some participating systems to attach system specific qualifiers to Allergy/Intolerance record entries, for example a priority for the Allergy/Intolerance record entry or an episodicity. Similarly, some systems support richer sets of values for severity than are catered for via the criticality and reaction/severity elements. The certainty qualifiers that exist in participating systems are not supported. In all cases, the full set of qualifiers and values that are associated with an Allergy/Intolerance in the source system should be rendered as text (suitable formatted name/value pairs) and placed in the note element.

### Adoption of single notes field
Rather than split descriptive and user entered text across a number of notes fields the AllergyIntolerance/note element is used as the single notes field to convey all qualifiers and user-entered text associated with the Allergy/Intolerance in a single place. Qualifiers and values should be appropriately labelled and formatted and where user notes have been entered against explicit fields such as Certainty then appropriate labels should be used.

### 'Ended' allergies and intolerances
On some systems it is possible to explicitly 'end' an Allergy/Intolerance such that it still appears in the patient record but is no longer active, for example ended drug allergies that no longer interact with prescribing decision support. This inactivation may be achieved by explicit entry of an end date or a user action that alters the status of the Allergy and Intolerance. Allergies and Intolerances which have been explicitly ended should not accessible as AllergyIntolerance resources. That is, they should not be visible via Allergy and Intolerance lists to external systems.
The corollary is that these record entries should still be accessible as other resource types.

### Relationship to yellow card 
Allergy and Intolerance information may co-exist alongside system support for the capture of medication adverse reactions via the MHRA Yellow Card scheme. Suppliers should ensure that only information directly associated with the Allergy and Intolerance entry in the system is included in the AllergyIntolerance resource.

### AllergyIntolerance category
It is expected that it will always be possible to assign a category of medication for drug allergies or environmental for all other types of Allergy/Intolerance. Generally, the choice in a given system is explicit. In some cases, the type of Allergy/Intolerance may be more general - for example, a system type of 'Other' or equivalent. In such cases, if the Allergy/Intolerance entry interacts with prescribing decision support it should be assigned a category of medication, otherwise the category of 'environmental' should be used.

### Date usage
Where there is a single user alterable date associated with the Allergy/Intolerance on the original system, this is the onsetDateTime.
The assertedDate is explicitly the 'Date Record was believed accurate' and unless there is a user alterable date field on the source system that explicitly attests to the 'Date Record was believed accurate', then assertedDate is considered to be the audit trail datetime for the AllergyIntolerance i.e. when the record entry was made or modified and should be populated as such.

### Unsupported codes
In some of the participating systems, an additional code may be entered that represents the Allergy/Intolerance in addition to coding of the causative agent and reaction. These additional codes are not explicitly supported by the AllergyIntolerance resource. The unsupported allergy code should be encoded as a textual qualifier in the note element.

*The reasoning being that as systems converge on interoperable coding of Allergies and Intolerances via AllergyIntolerance/code the need for another code to represent the Allergy/Intolerance concept diminishes*

### Negation - Handling 'no known allergies'
Where there is an explicit assertion of the 'No Known Allergies' concept in the record (equivalent to SNOMED CT concept 716186003 and children) and there are otherwise no Allergy/Intolerance entries in the patient record, then systems may respond to queries for all AllergyIntolerance resources for the patient with an empty List containing an emptyReason code of 'nilKnown' with the term of the 'No Known Allergies' present expressed as text.

Where there are no Allergy/Intolerance entries in the patient record, but no explicit recording of the 'No Known Allergies' concept and equivalents, then systems should return an empty list with an emptyReason code of 'notasked' – that is, no assertion that the patient has 'No Known Allergies' has been made.

### Degradation actions to be performed by consumers not producers
Producer systems should not in principle limit potential interoperability by pre-emptively degrading coded information in export. It is a consumer responsibility to determine the understandability/processability of received resources and degrade if appropriate. This differs from the approach taken to AllergyIntolerance interoperability in other contexts such as GP2GP, where in some cases producer systems pre-emptively degraded certain types of Allergy/Intolerance (e.g. drug allergies specified by Multilex action group or BNF chapter) on the basis that the concepts would never be generally interoperable.

### Reaction cardinality
The AllergyIntolerance/reaction element is optional, but where a severity is available in the source system it will be included to convey severity even if no other reaction details are explicitly available. If this is the case the reaction/manifestation should be coded as the nullFlavor NI.

By convention, only one resource should be expressed per allergy with only one manifestation per reaction.

# AllergyIntolerance resource definition
This guidance should be read in conjunction with the underlying resource definition. (TO DO: Check URL matches correct published StructureDef) [AllergyIntolerance](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1)

# Common and base element handling
Guidance for the general handling of common and base elements in GP Connect resources can be found [here - link required]()

# Element usage

**TO DO REMOVE
Assumptions about published StructureDefinition
Allergy End Data extension is removed
Probability of Recurrence is removed
Certainty extension removed from reaction
**

| Element  |Usage |Datatype   |Optionality|Guidance 
|---|---|---|---|---
|Evidence|Reference to confirmatory diagnostic report e.g. pathology RAST test result|Extension (valueReference)|O||
|clinicalStatus|Fixed value 'active' if present|Code|O||Care should be taken when sending non-active (inactive or resolved) allergies. It is suggested that inactive or resolved allergies are contained within a List resource (see https://www.hl7.org/fhir/references.html#contained) unless both parties are certain that inactive or resolved allergies will be handled correctly.|
|verificationStatus|Fixed value of 'unconfirmed'|Code|M|||
|type|Set to 'allergy' for reactions which are allergenic in nature (immunological), a value of 'intolerance may be used to indicate Adverse Reactions (not immunologic in nature). Where the type is unknown the type element may be omitted. |Code|O|Some systems allow explicit identification of Adverse Reactions and Intolerances and the type should be used to make this distinction where it exists. An absence of AllergyIntollerance.type implies that it is not known whether the reaction was allergic or intolerance||
|category|Use 'medication' for all drug allergy types, 'environmental' for all non-drug allergies. The other values in the ValueSet (food and biologic) should not be used by convention.|Code|M|See note on 'AllergyIntolerance Category'
|criticality|Distinguishes between life threatening (high) and non-life-threatening (low) potential as well as unable-to-assess. May be used in addition to severity within the reaction element to express severity e.g. systems that support a severity of life threatening may set to high|Code|O|May be used in conjunction with reaction/severity by systems which support a severity of 'Life Threatening' or equivalent
|code|The causative agent such as food, drug or substances that has caused or may cause an allergy, intolerance or adverse reaction in this patient.|CodeableConcept|M|Systems will evolve to use the specified vocabulary of SNOMED CT concepts from the specified subset. The subset includes concepts from the substance and product hierarchies and allows medication concepts from the DM+D SNOMED CT extension. In the interim this coded element will hold the primary code for the AllergyIntolerance which may in the case of drug allergies be a medication code or a pre-coordinated code which triggers decision support on the system. Where the AllergyIntolerance has no coded representation in the source system but is identified as such in the source record then the appropriate degrade code may be used and the text of the AllergyIntolerance placed in the text element of the code.Where there are no known allergies then Include codes from http://snomed.info/sct where concept is-a 716186003 (No known allergy)

For no information available the use text "Information not available" (using HL7 FHIR nullFlavor (http://hl7.org/fhir/v3/NullFlavor) "NI" No Information)

Degrade codes ( 196461000000101 | transfer-degraded drug allergy (record artifact) | & 196471000000108 | transfer-degraded non-drug allergy (record artifact) | ) can be used if only a text representation of the allergy is known & precoordinated allergy codes (fro example 213020009 | egg protein allergy | ).
|onset[dateTime]|Date when allergy/intolerance first manifested. Restricted to values of dateTime. |dateTime|O|Is the user modifiable date or datetime associated with the Allergy/Intolerance entry on the original system. May be unknown on source system and if so omitted
|assertedDate|The 'Date Record was believed accurate'. Unless the system has an explicit user alterable datetime that represents the 'Date record was believed to be accurate' then this is the audit trail datetime of when the record entry was 1st made or modified|dateTime|M|Mandatory element as audit trail datetime will always be available
|lastOccurrence|Represents the date and/or time of the last known occurrence of a reaction event|dateTime|O|May not currently be available from participating systems and may be omitted. Ommission should not prejudice the ability of producers and consumers to process this element if and when it is available. This is the onset date of the last reaction.
|note|All text associated with the AllergyIntolerance including user entered notes and qualifiers is grouped together and expressed in this field. Ensures mapped coded values are not lost|Annotation|O|
|reaction/note|NOT TO BE USED|O|AllergyIntolerance/note should contain all the consolidated text from the Allergy/Intolerance|Annotation|
|reaction/manifestation|Conveys the reaction resulting from the Allergy/Intolerance as a code. Where no code is available, but a textual description of the reaction is available then the nullFlavor UNC may be used and the textual description conveyed via reaction/description. If no reaction has explicitly been recorded but the reaction element is present to convey severity, then reaction/manifestation should be coded as the nullFlavor NI. If the patient has been asked but is unable to specify a reaction the nullFlavor 'ASKU' should be used |CodeableConcept|O|Where no code is known (but a manifestation needs to be recorded) then populate the Manifestation CodeableConcept with the HL7 FHIR nullFlavor (http://hl7.org/fhir/v3/NullFlavor) "UNC" - "un-encoded" & text of manifestation in reaction.description

When patient is asked about reaction, but doesn't know the reaction then use HL7 nullFlavor "ASKU" - "asked but unknown"

When the reaction details cannot be determined/verified, then use the HL7 nullFlavor "NI" - "No Information"

|reaction/description|Conveys the textual description of the manifestation where no code is available|String|O|A receiving system may concatenate the contents (appropriately labelled) with text in AllergyIntolerance/note if a textual description of the manifestation is not supported in the receiving system record structure|
|reaction/severity|Severities of mild, moderate, severe are mapped directly to FHIR ValueSet. Map life threatening to severe and populate criticality with high. |Code|O|Unmapped severity codes in original system should be expressed in AllergyIntolerance/note|
|reaction/exposureRoute|The route by which exposure to the substance causing the reaction occurred. Utilise the DM+D route codes|CodeableConcept|O|
|reaction/onset[x]|NOT TO BE USED|Choice|O|Onset explicitly supplied via AllergyIntolerance/onset[dateTime]|
|reaction/substance|NOT TO BE USED|CodeableConcept|O|The causative is explicitly and specifically coded via AllergyIntolerance/code. it is recommended not to populate this but to populate the top level causative agent.

It must be clinically safe to only process the 'code' and ignore the 'reaction.substance’. See FHIR rules http://hl7.org/fhir/stu3/allergyintolerance-definitions.html#AllergyIntolerance.reaction.substance

Coding of the specific substance (or pharmaceutical product) with a terminology capable of triggering decision support should be used wherever possible. The 'code' element allows for the use of a specific substance or pharmaceutical product, or a group or class of substances. In the case of an allergy or intolerance to a class of substances, (for example, "penicillins"), the 'reaction.substance' element could be used to code the specific substance that was identifed as having caused the reaction (for example, "amoxycillin"). Duplication of the value in the 'code' and 'reaction.substance' elements is acceptable when a specific substance has been recorded in 'code|


