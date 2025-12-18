# Final Project
# Verb Conjugator
# for Akkadian
Akkadian verbs conjugate for person, gender, number, tense, and some other categories. There is 1st, 2nd, 3rd person, masculine & feminine, singular & plural.
The verbs conjugate using prefixes, infixes, and suffixes.

The conjugator here works for G stem verbs, the most common type. It only works for roots with 3 consonants, also the most common type. It conjugates for all numbers and genders, but only the durative (≈present) and preterite (past) tenses. 
Given a 3 consonant root, it looks up theme vowels from a list that are specific to that particular verb. It uses these to form the new stem used for that tense. Then the affixes are added to give the conjugated verb form.

Here is the R code for that. A file for it can be found in this repository, along with a list of all the verb roots and their tense theme vowels.

```
conjugate <- function(v) {
c1 <- substr(v,1,1)  #this grabs the first consonant of the stem
c2 <- substr(v,2,2)  #this grabs the second consonant of the stem
c3 <- substr(v,3,3)  #this grabs the third consonant of the stem
vd <- VerbList$`Durative Theme Vowel`[VerbList$Root==v]  #this searches the dataframe VerbList for the root and returns the Durative Theme Vowel from the next column over
vp <- VerbList$`Preterite Theme Vowel`[VerbList$Root==v]  #this his searches the dataframe VerbList for the root and returns the Preterite Theme Vowel from the next next column over


#this section creates all the conjugations
droot <- paste(c1,c2,c2,vd,c3,sep="",collapse="-")  #this creates the durative stem from the root consonants & durative theme vowel

dsm1 <- paste("a",droot,sep="",collapse="-")    #adds the affixes to the durative stem to create the singular masculine first person conjugation
dsm2 <- paste("ta",droot,sep="",collapse="-")    #sg masc 2nd
dsm3 <- paste("i",droot,sep="",collapse="-")    #sg masc 3rd
dsf1 <- paste("a",droot,sep="",collapse="-")    #sg fem 1st
dsf2 <- paste("ta",droot,"i",sep="",collapse="-")    #sg fem 2nd
dsf3 <- paste("i",droot,sep="",collapse="-")    #sg fem 3rd
dpm1 <- paste("ni",droot,sep="",collapse="-")    #pl masc 1st
dpm2 <- paste("ta",droot,"a",sep="",collapse="-")    #pl masc 2nd
dpm3 <- paste("i",droot,"u",sep="",collapse="-")    #pl masc 3rd
dpf1 <- paste("ni",droot,sep="",collapse="-")    #pl fem 1st
dpf2 <- paste("ta",droot,"a",sep="",collapse="-")    #pl fem 2nd
dpf3 <- paste("i",droot,"a",sep="",collapse="-")    #pl fem 3rd

proot <- paste(c1,c2,vp,c3,sep="",collapse="-")    #creates preterite stem from root vowels and pret. theme vowel

psm1 <- paste("a",proot,sep="",collapse="-")    #sg masc 1st
psm2 <- paste("ta",proot,sep="",collapse="-")    #sg masc 2nd
psm3 <- paste("i",proot,sep="",collapse="-")    #sg masc 3rd
psf1 <- paste("a",proot,sep="",collapse="-")    #sg fem 1st
psf2 <- paste("ta",proot,"i",sep="",collapse="-")    #sg fem 2nd
psf3 <- paste("i",proot,sep="",collapse="-")    #sg fem 3rd
ppm1 <- paste("ni",proot,sep="",collapse="-")    #pl masc 1st
ppm2 <- paste("ta",proot,"a",sep="",collapse="-")    #pl masc 2nd
ppm3 <- paste("i",proot,"u",sep="",collapse="-")    #pl masc 3rd
ppf1 <- paste("i",proot,"u",sep="",collapse="-")    #pl fem 1st
ppf2 <- paste("ta",proot,"a",sep="",collapse="-")    #pl fem 2nd
ppf3 <- paste("i",proot,"a",sep="",collapse="-")    #pl fem 3rd


#this section puts all the conjugations into tables
Akkadian.Durative <- data.frame(
    Person = c("Durative","Person",1,2,3), 
    sg_masc = c("sg","masc",dsm1,dsm2,dsm3),
    sg_fem = c("sg","fem",dsf1,dsf2,dsf3),
    pl_masc = c("pl","masc",dpm1,dpm2,dpm3),
    pl_fem = c("pl","fem",dpf1,dpf2,dpf3),
    stringsAsFactors = FALSE
)
names(Akkadian.Durative) <- NULL

Akkadian.Preterite <- data.frame(
    Person = c("Preterite","Person",1,2,3), 
    sg_masc = c("sg","masc",psm1,psm2,psm3),
    sg_fem = c("sg","fem",psf1,psf2,psf3),
    pl_masc = c("pl","masc",ppm1,ppm2,ppm3),
    pl_fem = c("pl","fem",ppf1,ppf2,ppf3),
    stringsAsFactors = FALSE
)
names(Akkadian.Preterite) <- NULL
print(Akkadian.Durative)
print(Akkadian.Preterite)

}
```
Here is an example of the function in use:
```
conjugate("blṭ")
```
Which returns:
```
1 Durative      sg       sg       pl       pl
2   Person    masc      fem     masc      fem
3        1  abllaṭ   abllaṭ  nibllaṭ  nibllaṭ
4        2 tabllaṭ tabllaṭi tabllaṭa tabllaṭa
5        3  ibllaṭ   ibllaṭ  ibllaṭu  ibllaṭa
                                          
1 Preterite     sg      sg      pl      pl
2    Person   masc     fem    masc     fem
3         1  ablaṭ   ablaṭ  niblaṭ  iblaṭu
4         2 tablaṭ tablaṭi tablaṭa tablaṭa
5         3  iblaṭ   iblaṭ  iblaṭu  iblaṭa
```
