# Biosample analysis

Repo for analysis of biosamples in INSDC

Questions to explore

 - which attributes/properties are used
 - are these conformant to standards?
    - E.g. are MIxS fields used
    - Does the range constraint apply?
 - Can we mine ontology terms, e.g. ENVO from text descriptions
 - can we auto-populate metadata fields

# Workflow

See Makefile for details

# Analysis Data
In addition to the data in the target directory, sample data that is too large for GitHub is stored our Google drive [here](https://drive.google.com/drive/u/1/folders/1eL0v0stoduahjDpoDJIk3z2pJBAU4b2Y).  
Files include:
- [biosample_set.xml.gz](https://drive.google.com/file/d/1YNp7Sj4k0jfZZa3DSsqO0QQ64m0_DT3e/view?usp=sharing)  
  This is the full raw biosample dataset formatted as XML.
- [harmonized-values-eav.tsv.gz](https://drive.google.com/file/d/1CgLykW37ZDjgSSxz3GFPGZoDlSwG3N9e/view?usp=sharing)
  A tab-delimited file containing data extracted from `biosample_set.xml.gz` that contains the biosample's primary id and only the biosample attributes that have `harmonized_name` property.
  The data is in entity-attribute-value ([EAV](https://en.wikipedia.org/wiki/Entity–attribute–value_model)) format. The columns in the file are `primary_id|attribute|value`.
  If necessary, use `make target/harmonized-table.tsv` to create the (non-zipped) file locally.
- [harmonized-table.tsv.gz](https://drive.google.com/file/d/1chyK2dS8XoPBXriERvi70N9xIhZFUbcy/view?usp=sharing)
  A tab-delimited file in the data from `harmonized-table.tsv.gz` has been "pivoted" into a standard tabular format (i.e., the attributes are column headers).
  If necessary, use `make harmonized-table.tsv` to create the (non-zipped) file locally.
- [harmonized-attribute-value.ttl.gz](https://drive.google.com/file/d/1id30HwYoghNtki6zPsxz82ew2dDIeiL1/view?usp=sharing)
  A tab-delimited file in which the data from `harmonized-values-eav.tsv.gz` have been transformed into sets of turtle triples.  
  If necessary, use `make harmonized-attribute-value.ttl` to create the (non-zipped) file locally.

# Related

https://github.com/cmungall/metadata_converter

# Example bad data

## Depth

MIxS specifies this should be `{number} {unit}`

Some example values that do not conform:

 - N40.1164_W88.2543
 - 25 santimeters
 - 0 – 20 cm
 - 3.149
 - 30-60cm replicate6
 - 1800, 1800
 - 30ft
 - 5m, 32m, 70m, 110m, 200m, 320m, 1000m
 - Surface soil from deep water
 - 0 m water depth
 - Metamorph4 (19dpf) biological replicate 3

## pH

 - pH 7.9
 - 6.0-9.5
 - 8,156
 - NA1
 - 2.75 (orig)
 - 5.11±0.10
 - Missing: Not reported
 - Not collected
 - 7.0-7.5 um
 - Moderately alkaline

## ammonium

Should be {float} {unit}

 - 0.71 micro molar
 - 14.941
 - -0.024
 - 1.9 g NH4-N L-1
 - Below the deteciton limit (2 microM)
 - 3.09µg/L

Units vary from 'micro molar' through uM through mg/L

## geo_loc_name

MIxS:

_The geographical origin of the sample as defined by the country or sea name followed by specific region name. Country or sea names should be chosen from the INSDC country list (http://insdc.org/country.html), or the GAZ ontology (v 1.512) (http://purl.bioontology.org/ontology/GAZ)_

` {term};{term};{text}`

 - USA: WA
 - USA:MO
 - USA: Boston, MA
 - USA:CA:Davis
 - United Kingdom: Midlands and East of England
 - Malawi: GAZ
 
 
